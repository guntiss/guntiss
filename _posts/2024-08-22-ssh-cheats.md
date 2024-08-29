---
title: "SSH Cheats a.k.a. useful shortcuts"
date: 2024-08-22
---

In this article I will post all my favorite SSH features.

SSH is super powerful tool if you know how to use it properly.

## SSH Aliases

Instead of typing `ssh root@some-db-server-in-the-cloud.com -P 2222` you can set up aliases to use something like `ssh db1`, which will save you a lot of time on typing. To do that, open your `.ssh/config` file and create following entry:

```
Host db1
    hostname some-db-server-in-the-cloud.com 
    User root
    Port 2222
```

It will also work anywhere SSH protocol is used - `scp`, `rsync`, git origins, etc.

You will also have a static entry in VSCode connect to remote host list, which is very handy.
![Book logo](/assets/vcsode-ssh-remotes.png)
