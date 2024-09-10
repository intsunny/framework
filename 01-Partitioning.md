## Partitioning

### Fedora default partition

This is what Fedora does if you specify no customizations

#### Partition table

```
(parted) print
Model: WD_BLACK SN850X 1000GB (nvme)
Disk /dev/nvme0n1: 1000GB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags: 
 
Number  Start   End     Size    File system  Name                  Flags
 1      1049kB  630MB   629MB   fat32        EFI System Partition  boot, esp
 2      630MB   1704MB  1074MB  ext4                               bls_boot
 3      1704MB  1000GB  999GB
```

#### Live mounts


```
oot@fedora:~# mount  | grep nvm
/dev/nvme0n1p2 on /boot type ext4 (rw,relatime,seclabel)
/dev/nvme0n1p1 on /boot/efi type vfat (rw,relatime,fmask=0077,dmask=0077,codepage=437,iocharset=ascii,shortname=winnt,errors=remount-ro)
 
root@fedora:~# mount  | grep luk
/dev/mapper/luks-7f46120f-654b-XXXX on / type btrfs (rw,relatime,seclabel,compress=zstd:1,ssd,space_cache=v2,subvolid=257,subvol=/root)
/dev/mapper/luks-7f46120f-654b-XXXX on /home type btrfs (rw,relatime,seclabel,compress=zstd:1,ssd,space_cache=v2,subvolid=256,subvol=/home)
```

#### /etc configs


`/etc/fstab`:
````
#
# /etc/fstab
# Created by anaconda on Tue Sep 10 03:34:57 2024
#
# Accessible filesystems, by reference, are maintained under '/dev/disk/'.
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info.
#
# After editing this file, run 'systemctl daemon-reload' to update systemd
# units generated from this file.
#
UUID=a1b2ed50-f191-40ac-8f22-XXXX /                       btrfs   subvol=root,compress=zstd:1,x-systemd.device-timeout=0 0 0
UUID=96c4b190-ca4d-4255-a23f-XXXX /boot                   ext4    defaults        1 2
UUID=632B-3663          /boot/efi               vfat    umask=0077,shortname=winnt 0 2
UUID=a1b2ed50-f191-40ac-8f22-XXXX /home                   btrfs   subvol=home,compress=zstd:1,x-systemd.device-timeout=0 0 0
````

`/etc/crypttab`:

````
luks-7f46120f-654b-4f35-ad49-XXXX UUID=7f46120f-654b-4f35-ad49-XXXX none discard
````
