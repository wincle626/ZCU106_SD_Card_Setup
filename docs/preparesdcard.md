## Prepare SD card [(This is copied from Xilinx wiki website)](https://xilinx-wiki.atlassian.net/wiki/spaces/A/pages/18841655/Prepare+Boot+Medium)

### 1. Format the SD card

The following commands will use '/dev/sdX' to refer to the SD card device. Replace this with the actual device on your system. Executing the following commands on the wrong device may corrupt your data on other file systems. Also, all data on your SD card will be destroyed.

The fdisk utility does not seem to erase the first few bytes of the first sector in the card when the partition table is saved. Use dd to erase the first sector.

#### dd if=/dev/zero of=/dev/sdX bs=1024 count=1

Calculate the new_cylinders value

#### fdisk -l /dev/sdX

The output should look similar to this

Disk /dev/sdb: 8068 MB, 8068792320 bytes

249 heads, 62 sectors/track, 1020 cylinders, total 15759360 sectors

Units = sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disk identifier: 0x00000000




  
Disk /dev/sdb doesn't contain a valid partition table

Look for the size of the device in bytes and calculate the new number of cylinders using the following formula, dropping all fractions:

new_cylinders = <size> / 8225280
  
For the example output given above, we would write down new_cylinders = 8068792320 / 8225280 = 980

Partition the SD card. We will create two partitions on the SD card. One 200 MB sized boot partition. And a second partition taking the remaining space on the SD card.






#### fdisk /dev/sdX

The dd command should have wiped all existing partition tables, if this is not the case, delete all existing partitions on the SD card.



Command (m for help):

Partition number (1-4): 1



Repeat this for all valid partitions numbers.

Now configure the sectors, heads and cylinders of the SD card.



Command (m for help): x

Expert command (m for help): h

Number of heads (1-256, default 30): 255

Expert command (m for help): s

Number of sectors (1-63, default 29): 63

Expert command (m for help): c

Number of cylinders (1-1048576, default 2286): <new_cylinders calculated from above>

Command (m for help): r



Now the actual partitions can be created



Command (m for help): n

Partition type:

 p primary (0 primary, 0 extended, 4 free)
 
 e extended
 
Select (default p): p

Partition number (1-4, default 1): 1

First sector (2048-15759359, default 2048):

Using default value 2048

Last sector, +sectors or +size{K,M,G} (2048-15759359, default 15759359): +200M
  
Command (m for help): n

Partition type:

 p primary (1 primary, 0 extended, 3 free)
 
 e extended
 
Select (default p): p

Partition number (1-4, default 2): 2

First sector (411648-15759359, default 411648):

Using default value 411648

Last sector, +sectors or +size{K,M,G} (411648-15759359, default 15759359):

Using default value 15759359



Now, set the bootable flag and partition IDs



Command (m for help): a

Partition number (1-4): 1
  
Command (m for help): t

Partition number (1-4): 1

Hex code (type L to list codes): c

Changed system type of partition 1 to c (W95 FAT32 (LBA))
  
Command (m for help): t

Partition number (1-4): 2

Hex code (type L to list codes): 83



Check the new partition table and write the changes



Command (m for help): p
  
Disk /dev/sdb: 8068 MB, 8068792320 bytes

249 heads, 62 sectors/track, 1020 cylinders, total 15759360 sectors

Units = sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disk identifier: 0x920c958b

Device Boot Start End Blocks Id System
 
/dev/sdb1 * 2048 411647 204800 c W95 FAT32 (LBA)

/dev/sdb2 411648 15759359 7673856 83 Linux
  
Command (m for help): w

The partition table has been altered!
  
Calling ioctl() to re-read partition table.
  
WARNING: If you have created or modified any DOS 6.x partitions, please see the fdisk manual page for additional
information.

Syncing disks.



Create file systems on the new partitions



#### mkfs.vfat -F 32 -n boot /dev/sdX1

#### mkfs.ext4 -L root /dev/sdX2



### 2. Unzip/copy rootfs from Zcu106_Ubuntu_Desktop_Release_2019_1/Ubuntu_rootfs to the ext4 partition

### 3. For image build from source: 

#### copy 

### 4. For image build from PetaLinux: 

#### Copy zcu106_project/xilinx-zcu106-2019.1/images/linux/Boot.bin and zcu106_project/xilinx-zcu106-2019.1/images/linux/Image.ub to the fat32 parition.

