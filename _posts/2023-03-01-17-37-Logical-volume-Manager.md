---
layout: post
title: Logical Volume Manager
catagory: [Linux, Storage]
---

* Add disk via VC - Edit setting on VM, Add a new disk ( separate disks for each VGs)
* Scan disk - Find your host bus ID : # ls /sys/class/scsi_host then 
* Scan SCSI host : # echo "-  -  -" > /sys/class/scsi_host/hostX/scan   ( x is host number)
* Partition Disk : # (echo n; echo p; echo 1; echo ''; echo ''; echo t; echo 8e; echo w) | fdisk /dev/sdx
* Create a new PV  # pvcreate /dev/sdx1
* Create a new VG # vgcreate vg1 /dev/sdx1
* Extend VG  # vgextend vg1 /dev/sdx1
* Create a new LV  # lvcreate -n lv1 -L +10G vg1 or lvcreate -n lv1 -l +100%FREE vg1
* Extend LV # lvextend -L +10T /dev/mapper/vg1-name or lvextend -l +100%FREE /dev/mapper/vg1-nam
* Format LV  # mkfs.extX /dev/mapper/vg1-lv1 (Determine fs with df -TH command)
* Mount LV # mount /dev/vg1/lv1 /opt/SP/mountname -o rw,user