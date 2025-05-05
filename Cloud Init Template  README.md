# Prommox
Prommox
Cloud Init  setup guide 

Create disk 

qm create 5000 --memory 8096 --core 8 --name ubuntu-cloud --net0 virtio,bridge=vmbr0 

 

cd into directory bellow 

cd /var/lib/vz/template/iso/ 

 

import disk using previously downloaded cloud image 

qm importdisk 5000 “insert name of cloud image here”” (example)lunar-server-cloudimg-amd64-disk-kvm.img Ceph-Fast 

 

create disk settings from imported vm bellow 

qm set 5000 --scsihw virtio-scsi-pci --scsi0 <Ceph-Fast>:5000/vm-5000-disk-0.raw 

 

setup cloud init drive  

qm set 5000 -- scsi <Ceph-Fast>:cloudinit 

 

make disk bootable 

qm set 5000 --boot c --bootdisk scsi0 

 

NOTE run this command to make vm bootable by proxmox console 

qm set 5000 --serial0 socket --vga serial0 

 

 

Once the above steps have been completed do the following 

 

NOTE 

DO NOT START VM once it is created 

Right click on the vm id 5000 you have created and hit convert to template 
