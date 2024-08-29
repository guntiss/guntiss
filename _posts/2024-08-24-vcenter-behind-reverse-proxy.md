---
title: "VCenter behind reverse proxy"
date: 2024-08-24
---

Recently I was met with a challange to put VMware VCenter behind reverse proxy In order to terminate with correct SSL certificate (without reconfiguring VCenter) and exposing it to another subnet (not internet).

After some research I Stumbled upon [this](https://www.reddit.com/r/vmware/comments/15lbl8n/vcenter_behind_reverse_proxy/) reddit post, that said

> "Running VCenter behind reverse proxy is not supported configuration"

But reading forward I was convinced that someone else had succeeded with this impossible task.

So I tested provided solution, but It didn't quite work for me. Most likely having newer VCenter version (8.0.2) was the reason.

After deeper debugging, reading nginx documentation, many postman requests, trial and error I finally got it working. It seems that security has been improved in recent version and now WebSocket endpoint checks if "Origin" header matches VCenter FQDN, otherwise it fails with Error 403.

The solution was to add Origin header with correct value, and here is the final working solution:

~~~conf
location / {
    sub_filter vcenter.internal.local vcenter.external.com;
    sub_filter_once off;
    proxy_http_version 1.1;
    proxy_set_header Host vcenter.internal.local;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
    proxy_set_header Origin "https://vcenter.internal.local";
    # my proxy doesnt have correct DNS, so I used IP here, but you can use domain
    proxy_pass https://10.1.2.3;
    proxy_redirect https://vcenter.internal.local/ https://vcenter.external.com/;
    # block access to external resources
    add_header Content-Security-Policy "connect-src 'self';";
}
~~~

For some reason `sub_filter` didn't replace redirection header, so I had to add `proxy_redirect` config as well.

As a bonus I added CSP that blocks browser connections to external domains (feedback.esp.vmware.com), to get rid of VMWare telemetry.

### Summary

Running this solution inside docker, behind another Traefik proxy that terminates SSL, everything is working great.

I just want to emphasize that you should never expose VCenter to public internet as it could be huge security risk. This is not for such usecase.
