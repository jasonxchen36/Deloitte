1. Create and attach 8 GB disk (Provisioned IOPS, 400 IOPS) to the VM

2. Run the command below as root or sudo to root and select options as specified:

Assuming that the name of the new volume is nvme6n1 (can be found by running lsblk command)

   fdisk /dev/nvme6n1
	p ---> n ---> p ----> 1 ----> enter ----> enter ----> t ----> 82 ----> p ----> w 
	
3. partprobe

4. mkswap /dev/nvme6n1p1

5. vi /etc/fstab
UUID=<enter uuid for the disk>    	swap	    swap	defaults	0	0

6. mount -a 

7. swapon -a

8. free -m
 swapon -s