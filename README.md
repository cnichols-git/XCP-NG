# XCP-NG
To create VM's you will need to load iso images. There are many other things you can do but this call out is about storing ISO images to create new VMs.  

This first issue I encountered was storage space for SRs (Software Repositories). This is becuase a default SR set up locally will only provide approx. 15 GB and that will fill up with a win11.iso and a Windows server.iso. 

I have an Ubuntu server that I will install and set up NFS and store the files there, I will have plenty of space.  

### Install NFS software
I have a Ubuntu server that will server the mounts and this is how I did that.  
`sudo apt install nfs-kernel-server`  

### Create directory to house the files
create directory  
`sudo mkdir /nfs-exports/ISOs`  
`sudo chmod -R 775 /nfs-exports/`  

### Back up and edit a new NFS config file to define the directories it will use.  

I choose to rename the original file as a back up  
`mv /etc/exports /etc/exports.orig`  

and create a new file  
`sudo vi /etc/exports  `  
*depeing on your edtor you are using.*  
`sudo nano /etc/exports`  

and add the following :  
/nfs-exports/ISOs 192.168. *. */255.255.255.0(rw,no_subtree_check)   
***ensure you put your servers IP address and not what I have entered.*  

The file is telling showing the Server file location/the directory the sever IP and subbet(it is in and *rw* read write permission).  

### Change the ownership of the directory and all its subfolders  
`sudo chown -R nobody:nogroup /nfs-exports/`  
 
