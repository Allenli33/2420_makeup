# ACIT 2420 Linux Makeup Assignment

## Completed by Hao Li

- This README.MD guides you how to Install a base Arch Linux OS using the official Arch Linux installation guide:

- Resources/Technologies Used

- Vitural box
- Arch Linux

**Note:** Download an Arch Linux iso file from the download link below
https://mirror.csclub.uwaterloo.ca/archlinux/iso/2022.12.01/

![](1.png)

**IMPORTANT** It has to be one file in .iso at the end.

## Open Vitrual Box create a new VM

- Give whatever name you like but make the type is Linux

![](2.png)

- Set a memory size, you can set 2048MB if you have enough room

![](3.png)

- Hard disk: as default: create a hard disk now, no need to change

![](4.png)

- Hard disk type: also leave as default

![](5.png)

## Storage on physical hard disk we choose:

`Fixed size`

![](6.png)

- File location and size

![](7.png)

- Create and done

![](8.png)

## open the setting of the new VM you created

- At `storage` choose the iso file you download before and import it.

![](9.png)

## Start your VM

![](10.png)

## Set the console keyboard layout

- List all avaliable layouts

```
# ls /usr/share/kbd/keymaps/**/*.map.gz
```

![](11.png)

- The default is `US` we just leave as default

![](12.png)

## Vertify the boot mode

`# ls /sys/firmware/efi/efivars`

![](13.png)

## Connect to the internet

`# ip link`

![](14.png)

## Update the system clock

`# timedatectl status`

![](15.png)

## Partition the disks

`# fdisk -l`

**NOTE**If you want to create any stacked block devices for LVM, system encryption or RAID, do it now.

`# fdisk /dev/the_disk_to_be_partitioned`

![](16.png)

## Format the partitions

- Once the partitions have been created, each newly created partition must be formatted with an appropriate file system.

- eg: `# mkfs.ext4 /dev/root_partition`

**Warning** Only format the EFI system partition if you created it during the partitioning step. If there already was an EFI system partition on disk beforehand, reformatting it can destroy the boot loaders of other installed operating systems.

`# mkfs.fat -F 32 /dev/efi_system_partition`

## Mount file systems

- eg : `# mount /dev/root_partition /mnt`

## Installation

- Select the mirrors: which defines in `/etc/pacman.d/mirrorlist`

- Install essential packages

`# pacstrap -K /mnt base linux linux-firmware`

## Configure the system

- Fstab

`# genfstab -U /mnt >> /mnt/etc/fstab`

![](17.png)

- Chroot

`# arch-chroot /mnt`

![](18.png)

- Timezone

`# ln -sf /usr/share/zoneinfo/Region/City /etc/localtime`
`# hwclock --systohc`

![](19.png)

## Localization

- `sudo vim /etc/locale.gen` edit this file and uncomment this

![](20.png)

![](21.png)

- Create file `sudo vim /etc/locale.conf`

![](22.png)

![](23.png)

## Add new user and set password

![](26.png)

## Reboot

**NOTE** before you doing reboot, you need to remove the disk

![](25.png)

- Finally do reboot command and done!

![](24.png)
