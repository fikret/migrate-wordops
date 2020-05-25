

# migrate-wordops
Migrate WordOps Server to Another Machine

https://lowendbox.com/blog/how-to-migrate-a-hosted-server-in-5-easy-steps-with-rsync/

## 1. Check Kernel version

    uname -a
OLD
> Linux server03 4.15.0-101-generic #102-Ubuntu SMP Mon May 11 10:07:26
> UTC 2020 x86_64 x86_64 x86_64 GNU/Linux

NEW
> Linux ...er.net 4.15.0-101-generic #102-Ubuntu SMP
> Mon May 11 10:07:26 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux

## 2. Check ssh new to old

    ssh user@oldserver

## 3. Check rsync

    which rsync

## 4.Prepare Exclude Lıst

    /etc/fstab  
    /etc/sysconfig/network-scripts/* (CentOS distros)  
    /etc/network/* (Ubuntu distros)  
    /proc/*  
    /tmp/*  
    /sys/*  
    /dev/*  
    /mnt/*  
    /boot/*

## 5. Stop Serverices
    wo stack stop --all

## 6. RSYNC


