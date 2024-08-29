---
title: "Using rsync for backups and OS cloning"
date: 2024-08-21
---

Rsync is very powerful tool for file copying. It's more advanced and effective than `scp`. For example, rsync allows copying only modified files, thus saving bandwidth and time. This can be especially useful for backups and even server migration.

## Backups using rsync

For simple cases you can use simple cronjob with rsync command to store backups on same or remote host. When you want to store backups remotely I would advise to use pulling principle instead of pushing. Main benefit is that in case source machine gets compromised it's not possible to access the backups on remote host.

So in order to set it up you would need to:
- generate a seperate SSH key on backup server
- authorize SSH key on source server
- create an rsync cronjob on backup server.

Backup command can be as simple as:
```sh
rsync -av remotehost:/data /opt/backups/
```

Make sure you have set up [SSH Alias](./2024-07-22-ssh-cheats.md#ssh-aliases) for `remotehost`.

Importan Notes:
- If files are removed at source, they will still remain in backups machine. Add `--delete` in order to also reflect deleted files.
- After each rsync finishes it would be smart to archive received backups and keep them for necesssary period. This way you will have multiple restore points instead of one.

## Clone OS using rsync

Sometimes only option to migrate VM is using rsync.
Preconditinos:
- Target server should have same OS.
- Target server SSH key is authorized at source server

Sample rsync command to run on target server:

```sh
rsync -avzl --delete --stats --progress \
    --exclude '/boot' \
    --exclude '/swapfile' \
    --exclude '/var/log/*' \
    --exclude '/tmp/*' \
    --exclude '/sys/*' \
    --exclude '/proc/*' \
    --exclude 'lost+found/*' \
    --exclude '/etc/fstab' \
    --exclude '/etc/mtab' \
    --exclude '/etc/network/interfaces' \
    --dry-run \
    sourceserver:/ /
```

*Notes:*
- Make sure you know remote host user/pass, as sync will replace /etc/passwd and shadow files.
- Check "mount" and "df -h" output, make sure to exclude all mounted FS!
- Skip `/etc/mdadm.conf` if there is RAID set up.
- If process is halted, you can lose private key and other files (on target server), due to `--delete` flag, so use with caution.
