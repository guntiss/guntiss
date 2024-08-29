---
title: "Do I need LVM?"
date: 2024-08-20
---

If you've ever install Linux OS you'll most likely have gone through disk partitioning.

As a default installer suggests using LVM. I had this question to myself quite often - "Do I need LVM, or not?", usually just keeping the default option.

## What is LVM

As stated on the interwebz:
> The most obvious benefit of LVM is that it provides an easy and flexible way to scale storage capacity. Admins can scale capacity up or down as users' storage needs change by simply adding or removing extents from an LV.

Also good read - https://www.reddit.com/r/linux/comments/6w046b/to_lvm_or_not_to_lvm_that_is_the_question/

## Expanding disk

In case you run out of virtual disk space and resize it, you will need to make some adjustments. For LVM this is slightly:
```sh
lsblk # find disk name
echo 1 > /sys/class/block/sda/device/rescan
lsblk # size should now be expanded
growpart /dev/sda 3 # extetend parittion to use whole disk
pvresize /dev/sda3
lvextend -l +100%FREE  /dev/mapper/ubuntu--vg-ubuntu--lv # Use name from `df -h /`
resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv
```

If there was no LVM, you would be done after `growpart` command. 

## Performance

My usual case is running Docker or kubernetes.

I'll just copy answer from [stackoverflow post](https://devops.stackexchange.com/a/19625) that summarizes it quite well:
<blockquote>
1. Is this intended/expected?
Yes, it can be expected. The overlay2 storage driver operates at the file level, and when combined with LVM, there can be additional overhead due to the abstraction layer that it introduces. Thus, slower performance compared to using a direct ext4 filesystem.


2. Is a LVM a recommended setup for Docker usage?
LVM is not typically recommended for Docker’s overlay2 storage driver due to the potential performance overhead. Docker’s documentation suggests using overlay2 with a direct filesystem like ext4 or xfs for better performance. LVM can be useful for other purposes, such as managing disk space more flexibly, but it might not be ideal for Docker’s storage needs.
</blockquote>


## Conclusion

If you plan to use single partition, just go without LVM.

But keep in mind:
> You don't need it, until you do.
