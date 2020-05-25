

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

    rsync -auHx --info=progress2 --numeric-ids --exclude=/etc/fstab --exclude=/etc/network/* --exclude=/proc/* --exclude=/tmp/* --exclude=/sys/* --exclude
    =/dev/* --exclude=/mnt/* --exclude=/boot/* root@185.137.180.155:/* /
I cant set port and change old server's port to default (22)


## Problem with Mariadb

    root@vmi393968:~# systemctl status mysql
    ● mariadb.service - MariaDB 10.3.20 database server
       Loaded: loaded (/lib/systemd/system/mariadb.service; enabled; vendor preset: enabled)
      Drop-In: /etc/systemd/system/mariadb.service.d
               └─limits.conf, migrated-from-my.cnf-settings.conf
       Active: failed (Result: exit-code) since Mon 2020-05-25 21:06:08 UTC; 48s ago
         Docs: man:mysqld(8)
               https://mariadb.com/kb/en/library/systemd/
      Process: 2576 ExecStartPre=/usr/bin/install -m 755 -o mysql -g root -d /var/run/mysqld (code=exited, status=217/USER)
    
    May 25 21:06:08 vmi393968.contaboserver.net systemd[1]: Starting MariaDB 10.3.20 database server...
    May 25 21:06:08 vmi393968.contaboserver.net systemd[2576]: mariadb.service: Failed to determine user credentials: No such process
    May 25 21:06:08 vmi393968.contaboserver.net systemd[2576]: mariadb.service: Failed at step USER spawning /usr/bin/install: No such process
    May 25 21:06:08 vmi393968.contaboserver.net systemd[1]: mariadb.service: Control process exited, code=exited status=217
    May 25 21:06:08 vmi393968.contaboserver.net systemd[1]: mariadb.service: Failed with result 'exit-code'.
    May 25 21:06:08 vmi393968.contaboserver.net systemd[1]: Failed to start MariaDB 10.3.20 database server.

