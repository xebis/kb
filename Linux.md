# Linux

**This** cheat sheet **is NOT complete!**

## Tools

```bash
watch -d -n 60 cmd # watch - run repeatedly cmd every 60 seconds and highlight differences
```

## Disk Tools

### Partitioning

- Choose **MBR** for BIOS (legacy mode), choose **GPT** for EFI

```bash
parted -l # list partitions
parted # to enter parted session, commands print, help, mklabel, mkpart
(parted) help command # parted command help
(parted) /dev/dda mklabel gpt mkpart primary ext4 0 64GiB name 'My Primary'
(parted) quit # to quit parted session
```

### LUKS

```bash
cryptsetup #todo
cryptsetup luksFormat --hash=sha512 --key-size=512 /dev/sda7
cryptsetup open --type=luks /dev/sda7 rootfs
```

### LVM

```bash
pvs && vgs && lvs # list physical volumes, volume groups, logical volumes
# see also: vgscan, vgchange -ay

pvcreate /dev/sda6 # create physical volume
pvresize /dev/sda6 # expand physical volume after partition extension, add --setphysicalvolumesize size to shrink
pvdisplay /dev/sda6 # display physical volume information
# see also: pvmove

vgcreate vgname /dev/sda6 ... # create volume group
vgextend vgname /dev/hda1 # extend volume group
vgreduce vgname /dev/hda1 # reduce volume group
# see also: vgchange, vgrename

lvcreate -n lvname -L 32G vgname # create logical volume
lvremove vgname/lvname # remove logical volume (unmount it first)
lvresize -L +10G --resizefs vgname/lvname # resize logical volume (including filesystem)
lvextend -L 16G vgname/lvname # extend logical volume (extend filesystem later)
lvreduce -L 16G vgname/lvname # reduce logical volume (unmount it first, reduce filesystem first, mount later)
# see also: lvrename, lvcreate --type raidlevel

lvcreate -s -n lvbackup -L 4G lvname # create logical volume snapshot
lvconvert --merge lvbackup # merge snapshot back
# see also: lvcreate --type cache, lvconvert --uncache
```

### File Systems

```bash

```

## Sources

- [TLDP: GNU/Linux Command-Line Tools Summary](https://tldp.org/LDP/GNU-Linux-Tools-Summary/html/book1.htm)
- [ArchWiki: Partitioning](https://wiki.archlinux.org/index.php/partitioning)
- [TLDP: LVM HOWTO](https://tldp.org/HOWTO/LVM-HOWTO/)
- [ArchWiki: LVM](https://wiki.archlinux.org/index.php/LVM)
