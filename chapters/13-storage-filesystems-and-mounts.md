# 13. Storage, filesystems, and mounts

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Networking and SSH](./12-networking-and-ssh.md) | [Notes index](../README.md) | [Next: Services, systemd, and logs](./14-services-systemd-and-logs.md) |

## Disk, partition, filesystem, and mount point

A disk is a storage device. It may be divided into partitions. A filesystem organizes files within a partition or another storage volume. A mount point is a directory where that filesystem becomes part of the Linux directory tree.

The device name alone does not tell you which filesystems are mounted or how much space is available. Inspect before changing storage:

~~~sh
lsblk -f
df -hT
~~~

<code>lsblk -f</code> lists block devices, partitions, filesystem types, labels, and identifiers. <code>df -hT</code> shows mounted filesystems, their type, used space, and free space in readable units.

## Measure a directory

<code>du</code> estimates how much space files under a path use:

~~~sh
du -sh "$HOME/Downloads"
du -h --max-depth=1 "$HOME"
~~~

The maximum-depth option is provided by GNU coreutils. Other implementations of <code>du</code> may use different options. Large directory trees can take time to scan.

## Mount and unmount

Mounting attaches a filesystem to a directory. The directory should exist, and a device should only be mounted after you have identified it correctly.

The following shows the form of a read-only mount. Replace the placeholders only after verifying the actual device and mount directory:

~~~sh
sudo mkdir -p /mnt/inspection
sudo mount -o ro /dev/DEVICE /mnt/inspection
find /mnt/inspection -maxdepth 2 -type f -print
sudo umount /mnt/inspection
~~~

A read-only mount prevents this session from writing to that filesystem, but the chosen device must still be correct. Never copy a sample device name and assume it points to the storage you intend.

## Persistent mounts

The <code>/etc/fstab</code> file describes filesystems that should be mounted automatically. Use filesystem UUIDs rather than assuming a disk will always receive the same device letter. Inspect the file and device identifiers before editing:

~~~sh
lsblk -f
sudo findmnt --verify
~~~

A malformed <code>fstab</code> entry can interfere with boot. Keep a backup of the original file, verify each field, and test changes before restarting the system. The <code>findmnt --verify</code> command checks the table syntax and related configuration.

## Formatting and data loss

Creating a filesystem on a device, repartitioning a disk, or changing mount configuration can make data inaccessible or erase it. Commands such as <code>mkfs</code> are destructive when they initialize a device. Confirm the device name, preserve needed data elsewhere, and do not run formatting commands as a learning exercise on a disk that contains files you need.

## Practice questions

1. What is a filesystem responsible for?
2. What does a mount point connect?
3. Which command shows filesystem types for block devices?
4. What does <code>df -hT</code> report?
5. How does <code>du</code> differ from <code>df</code>?
6. What does the <code>-o ro</code> mount option request?
7. Why are UUIDs useful in persistent mount configuration?
8. Why must a device be verified before formatting it?

## References

- [Ubuntu Server documentation](https://ubuntu.com/server/docs/)
- [Linux manual page for lsblk](https://man7.org/linux/man-pages/man8/lsblk.8.html)
- [Linux manual page for mount](https://man7.org/linux/man-pages/man8/mount.8.html)
- [Linux manual page for fstab](https://man7.org/linux/man-pages/man5/fstab.5.html)
- [Linux manual page for findmnt](https://man7.org/linux/man-pages/man8/findmnt.8.html)