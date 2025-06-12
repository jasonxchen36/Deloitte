This wiki page outlines the steps to fix Splunk if one of the disk volumes (such as cold storage) fails and is unable to be recovered.

Example of disk failure event:
![image.png](/.attachments/image-3974522b-6b4e-478a-be51-3b5a51c905a7.png)

# **Resolution Steps:**
1. Stop the corrupted VM and deattach the failed disks
2. Create a temporary recovery VM (must be in the same availbility zone as the corrupted VM)
3. Unmount the root volume disk from the corrupted VM (sda1)
4. SSH into the recovery VM and run the following commands as root:


```
[ec2-user@ip-10-241-205-122 ~]$ sudo su
[root@ip-10-241-205-122 ec2-user]# lsblk
NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
xvda    202:0    0   8G  0 disk
└─xvda1 202:1    0   8G  0 part /
xvdf    202:80   0  52G  0 disk
├─xvdf1 202:81   0   1M  0 part
└─xvdf2 202:82   0  52G  0 part
[root@ip-10-241-205-122 ec2-user]# mount /dev/xvdf2 /mnt/
[root@ip-10-241-205-122 ec2-user]# lsblk
NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
xvda    202:0    0   8G  0 disk
└─xvda1 202:1    0   8G  0 part /
xvdf    202:80   0  52G  0 disk
├─xvdf1 202:81   0   1M  0 part
└─xvdf2 202:82   0  52G  0 part /mnt
```


5. Comment out the other disk volume UUIDs in the fstab file:

```
[root@ip-10-241-205-122 ec2-user]# vi /mnt/etc/fstab
[root@ip-10-241-205-122 ec2-user]# cat /mnt/etc/fstab

#
# /etc/fstab
# Created by anaconda on Mon Sep 23 10:08:16 2019
#
# Accessible filesystems, by reference, are maintained under '/dev/disk'
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
#
UUID=4f462461-aef2-46ee-a16e-8548d8f7fbf7 /                       xfs     defaults        0 0
tmpfs /dev/shm tmpfs defaults,nodev,nosuid,noexec 0 0
#UUID=73e1eb2b-ee00-418d-8b02-9e3511d612ae              /opt/splunk             xfs     defaults        0       0
#UUID=fa884299-19e5-4862-ae17-ed35705f7539              /opt/splunk/var/lib/splunk/hot          xfs     defaults        0       0
#UUID=6b88c387-ab14-412d-aad2-d9d59eb02878              /opt/splunk/var/lib/splunk/cold         xfs     defaults        0       0
#UUID=88502da7-b0af-46cc-b7c3-c98af4d97384              /tmp            xfs     defaults,nodev,nosuid,noexec    0       0
#UUID=65b6e01d-f8b4-4445-ae38-654c31646829      swap    swap    defaults        0       0
```


6. Unmount the root volume disk on the recovery VM:

```
[root@ip-10-241-205-122 ec2-user]# umount /mnt/
[root@ip-10-241-205-122 ec2-user]# lsblk
NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
xvda    202:0    0   8G  0 disk
└─xvda1 202:1    0   8G  0 part /
xvdf    202:80   0  52G  0 disk
├─xvdf1 202:81   0   1M  0 part
└─xvdf2 202:82   0  52G  0 part
```


7. Attach the root volume disk to the corrupt VM in the /dev/sda1 directory

8. Uncomment the UUIDs in the fstab file for the working Splunk directories and run the mount command:

```
[[root@aw1436l015 a-ddefibaugh]# vi /etc/fstab
[root@aw1436l015 a-ddefibaugh]# lsblk
NAME        MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
nvme0n1     259:7    0   52G  0 disk
├─nvme0n1p1 259:8    0    1M  0 part
└─nvme0n1p2 259:9    0   52G  0 part /
nvme1n1     259:4    0  126G  0 disk /tmp
nvme2n1     259:1    0   16T  0 disk
nvme3n1     259:0    0   16T  0 disk
nvme4n1     259:5    0    1T  0 disk /opt/splunk
nvme5n1     259:2    0  3.1T  0 disk /opt/splunk/var/lib/splunk/hot
nvme6n1     259:3    0    8G  0 disk
└─nvme6n1p1 259:6    0    8G  0 part
```

 
9. Attach new clean volumes to the VM to replace the Splunk corrupted disk
10. Mount the new volumes to the Splunk directories (example is for cold storage):


```
[a-ddefibaugh@aw1436l015 ~]$ sudo su
[root@aw1436l015 a-ddefibaugh]# lsblk
NAME        MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
nvme0n1     259:7    0   52G  0 disk
├─nvme0n1p1 259:8    0    1M  0 part
└─nvme0n1p2 259:9    0   52G  0 part /
nvme1n1     259:4    0  126G  0 disk /tmp
nvme2n1     259:1    0   16T  0 disk
nvme3n1     259:0    0   16T  0 disk
nvme4n1     259:5    0    1T  0 disk /opt/splunk
nvme5n1     259:2    0  3.1T  0 disk /opt/splunk/var/lib/splunk/hot
nvme6n1     259:3    0    8G  0 disk
└─nvme6n1p1 259:6    0    8G  0 part
[root@aw1436l015 a-ddefibaugh]# pvcreate /dev/nvme2n1 /dev/nvme3n1
  Physical volume "/dev/nvme2n1" successfully created.
  Physical volume "/dev/nvme3n1" successfully created.
[root@aw1436l015 a-ddefibaugh]# vgcreate splunkcoldvg /dev/nvme2n1 /dev/nvme3n1
  Volume group "splunkcoldvg" successfully created
[root@aw1436l015 a-ddefibaugh]# pvdisplay
  --- Physical volume ---
  PV Name               /dev/nvme2n1
  VG Name               splunkcoldvg
  PV Size               16.00 TiB / not usable 4.00 MiB
  Allocatable           yes
  PE Size               4.00 MiB
  Total PE              4194303
  Free PE               4194303
  Allocated PE          0
  PV UUID               YTqwql-drk6-qf5i-fYSW-LaWV-IJZ7-I4ulte

  --- Physical volume ---
  PV Name               /dev/nvme3n1
  VG Name               splunkcoldvg
  PV Size               16.00 TiB / not usable 4.00 MiB
  Allocatable           yes
  PE Size               4.00 MiB
  Total PE              4194303
  Free PE               4194303
  Allocated PE          0
  PV UUID               Rm3JoN-VcWw-Rd8H-9elO-RIun-JwhI-r9CZE3

[root@aw1436l015 a-ddefibaugh]# vgdisplay
  --- Volume group ---
  VG Name               splunkcoldvg
  System ID
  Format                lvm2
  Metadata Areas        2
  Metadata Sequence No  1
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                0
  Open LV               0
  Max PV                0
  Cur PV                2
  Act PV                2
  VG Size               <32.00 TiB
  PE Size               4.00 MiB
  Total PE              8388606
  Alloc PE / Size       0 / 0
  Free  PE / Size       8388606 / <32.00 TiB
  VG UUID               D5fpoU-vPvf-2nqu-A7t3-h0aE-debL-8Te6mH

[root@aw1436l015 a-ddefibaugh]# lvcreate -l +100%FREE -n splunkcoldlv splunkcoldvg
  Logical volume "splunkcoldlv" created.
[root@aw1436l015 a-ddefibaugh]# lvdisplay
  --- Logical volume ---
  LV Path                /dev/splunkcoldvg/splunkcoldlv
  LV Name                splunkcoldlv
  VG Name                splunkcoldvg
  LV UUID                7IcwXO-zJWG-GHfu-USrT-t8Ky-Vek8-ZinPt3
  LV Write Access        read/write
  LV Creation host, time aw1436l015, 2023-02-07 19:26:58 +0000
  LV Status              available
  # open                 0
  LV Size                <32.00 TiB
  Current LE             8388606
  Segments               2
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     8192
  Block device           253:0

[root@aw1436l015 a-ddefibaugh]# mkfs.xfs -f /dev/splunkcoldvg/splunkcoldlv
meta-data=/dev/splunkcoldvg/splunkcoldlv isize=512    agcount=32, agsize=268435455 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=1        finobt=0, sparse=0
data     =                       bsize=4096   blocks=8589932544, imaxpct=5
         =                       sunit=0      swidth=0 blks
naming   =version 2              bsize=4096   ascii-ci=0 ftype=1
log      =internal log           bsize=4096   blocks=521728, version=2
         =                       sectsz=512   sunit=0 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
[root@aw1436l015 a-ddefibaugh]# blkid
/dev/nvme0n1p2: UUID="4f462461-aef2-46ee-a16e-8548d8f7fbf7" TYPE="xfs" PARTUUID="ee3a88bc-8450-4bb9-ab80-adf19a9de971"
/dev/nvme2n1: UUID="YTqwql-drk6-qf5i-fYSW-LaWV-IJZ7-I4ulte" TYPE="LVM2_member"
/dev/nvme5n1: UUID="fa884299-19e5-4862-ae17-ed35705f7539" TYPE="xfs"
/dev/nvme6n1: UUID="f8c61145-444a-45a4-a9be-def893e71c3b" TYPE="swap" PTTYPE="dos"
/dev/nvme6n1p1: UUID="65b6e01d-f8b4-4445-ae38-654c31646829" TYPE="swap"
/dev/nvme1n1: UUID="88502da7-b0af-46cc-b7c3-c98af4d97384" TYPE="xfs"
/dev/nvme4n1: UUID="73e1eb2b-ee00-418d-8b02-9e3511d612ae" TYPE="xfs"
/dev/nvme3n1: UUID="Rm3JoN-VcWw-Rd8H-9elO-RIun-JwhI-r9CZE3" TYPE="LVM2_member"
/dev/nvme0n1: PTTYPE="gpt"
/dev/nvme0n1p1: PARTUUID="c48ead58-29ca-4c3e-b1cb-63478fc409ce"
/dev/mapper/splunkcoldvg-splunkcoldlv: UUID="366ee404-f7ca-49b9-81f2-295c078faf26" TYPE="xfs"
[root@aw1436l015 a-ddefibaugh]# cat /etc/fstab

#
# /etc/fstab
# Created by anaconda on Mon Sep 23 10:08:16 2019
#
# Accessible filesystems, by reference, are maintained under '/dev/disk'
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
#
UUID=4f462461-aef2-46ee-a16e-8548d8f7fbf7 /                       xfs     defaults        0 0
tmpfs /dev/shm tmpfs defaults,nodev,nosuid,noexec 0 0
UUID=73e1eb2b-ee00-418d-8b02-9e3511d612ae               /opt/splunk             xfs     defaults        0       0
UUID=fa884299-19e5-4862-ae17-ed35705f7539               /opt/splunk/var/lib/splunk/hot          xfs     defaults        0       0
#UUID=6b88c387-ab14-412d-aad2-d9d59eb02878              /opt/splunk/var/lib/splunk/cold         xfs     defaults        0       0
UUID=88502da7-b0af-46cc-b7c3-c98af4d97384               /tmp            xfs     defaults,nodev,nosuid,noexec    0       0
UUID=65b6e01d-f8b4-4445-ae38-654c31646829       swap    swap    defaults        0       0
[root@aw1436l015 a-ddefibaugh]# mkdir -p /opt/splunk/var/lib/splunk/cold
[root@aw1436l015 a-ddefibaugh]# vi /etc/fstab
[root@aw1436l015 a-ddefibaugh]# cat /etc/fstab

#
# /etc/fstab
# Created by anaconda on Mon Sep 23 10:08:16 2019
#
# Accessible filesystems, by reference, are maintained under '/dev/disk'
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
#
UUID=4f462461-aef2-46ee-a16e-8548d8f7fbf7 /                       xfs     defaults        0 0
tmpfs /dev/shm tmpfs defaults,nodev,nosuid,noexec 0 0
UUID=73e1eb2b-ee00-418d-8b02-9e3511d612ae               /opt/splunk             xfs     defaults        0       0
UUID=fa884299-19e5-4862-ae17-ed35705f7539               /opt/splunk/var/lib/splunk/hot          xfs     defaults        0       0
UUID=366ee404-f7ca-49b9-81f2-295c078faf26               /opt/splunk/var/lib/splunk/cold         xfs     defaults        0       0
UUID=88502da7-b0af-46cc-b7c3-c98af4d97384               /tmp            xfs     defaults,nodev,nosuid,noexec    0       0
UUID=65b6e01d-f8b4-4445-ae38-654c31646829       swap    swap    defaults        0       0
[root@aw1436l015 a-ddefibaugh]# mount /dev/mapper/splunkcoldvg-splunkcoldlv /opt/splunk/var/lib/splunk/cold/
[root@aw1436l015 a-ddefibaugh]# lsblk
NAME                        MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
nvme0n1                     259:7    0   52G  0 disk
├─nvme0n1p1                 259:8    0    1M  0 part
└─nvme0n1p2                 259:9    0   52G  0 part /
nvme1n1                     259:4    0  126G  0 disk /tmp
nvme2n1                     259:1    0   16T  0 disk
└─splunkcoldvg-splunkcoldlv 253:0    0   32T  0 lvm  /opt/splunk/var/lib/splunk/cold
nvme3n1                     259:0    0   16T  0 disk
└─splunkcoldvg-splunkcoldlv 253:0    0   32T  0 lvm  /opt/splunk/var/lib/splunk/cold
nvme4n1                     259:5    0    1T  0 disk /opt/splunk
nvme5n1                     259:2    0  3.1T  0 disk /opt/splunk/var/lib/splunk/hot
nvme6n1                     259:3    0    8G  0 disk
└─nvme6n1p1                 259:6    0    8G  0 part
[root@aw1436l015 a-ddefibaugh]# df -h
Filesystem                             Size  Used Avail Use% Mounted on
devtmpfs                                62G     0   62G   0% /dev
tmpfs                                   62G     0   62G   0% /dev/shm
tmpfs                                   62G   17M   62G   1% /run
tmpfs                                   62G     0   62G   0% /sys/fs/cgroup
/dev/nvme0n1p2                          52G  9.4G   43G  18% /
tmpfs                                   13G     0   13G   0% /run/user/168367320
/dev/nvme1n1                           126G   33M  126G   1% /tmp
/dev/nvme4n1                           1.0T  108G  916G  11% /opt/splunk
/dev/nvme5n1                           3.2T  2.9T  234G  93% /opt/splunk/var/lib/splunk/hot
/dev/mapper/splunkcoldvg-splunkcoldlv   32T   34M   32T   1% /opt/splunk/var/lib/splunk/cold
[root@aw1436l015 a-ddefibaugh]# chown -R dtt_sc_splunk_prd:"dttlatrame service accounts" /opt/splunk
```


----

# **Commands Appendix:**
### Initialize Physical Volumes (disks) that is used by LVM (Logical Volume Manager):
`pvcreate /dev/nvme2n1 /dev/nvme3n1`

###Confirm Partitions are into Physical Volumes:
`pvdisplay`
		
###Create the LVM volume group (vg):
`vgcreate splunkcoldvg /dev/nvme2n1 /dev/nvme3n1`

###Confirm the LVM vg is created
`pvdisplay`
`vgdisplay`

###Create Logical Volume:
`lvcreate -l +100%FREE -n splunkcoldlv splunkcoldvg`

###View Logical Volume and their status:
`lvdisplay`
		
### Build the Linux File System for each disk name:
`mkfs.xfs -f /dev/splunkcoldvg/splunkcoldlv`

### List the Universally Unique Identified (UUID) of the block devices
`blkid`

### Verify the fstab file has the corresponding UUID:
`cat /etc/fstab`

### Create the Splunk directories:
`mkdir -p /opt/splunk/var/lib/splunk/cold`

### Mount the cold file system to the disks:
`mount /dev/mapper/splunkcoldvg-splunkcoldlv /opt/splunk/var/lib/splunk/cold`

### Set ownership & permissions:
`chown -R dtt_sc_splunk_prd:"dttlatrame service accounts" /opt/splunk`