---
title: "Connect to airgapped host using VSCode"
date: 2024-08-24
---

Working in airgapped or firewalled environment can be though, when you don't have access to internet.

Hopefully you already have VSCode server installed on your local machine (WSL in my case) which is working fine. But when you try to connect to remote server for first time - VSCode will still try to download some files from internet to this server instead of transferring from your device. And in case this server does not have access to Internet It will fail and you will not be able to connect.

Luckily I have found a super simple workaround for this problem. All you have to do is copy your local `.vscode-server` directory to remote server:

```sh
scp -r .vscode-server remoteserver:
```

As a bonus, you will also have all extensions pre-installed on remote host. Make sure you have set up `remoteserver` [SSH Alias](./2024-07-22-ssh-cheats.
md#ssh-aliases) set up.

Note: `scp` is slow, better alternative would be to use [rsync](./2024-07-21-rsync-backups.md) or create tar/zip archive first, uploading it and extracting at destination host.