# Born2beRoot

## script :                                                                            /usr/local/bin/monitoring.sh                                                                                         
    #!/bin/bash

    architecture=$(uname -a)

    cpu_physical=$(grep "physical id" /proc/cpuinfo | sort -u | wc -l)

    cpu_virtuel=$(grep "processor" /proc/cpuinfo | wc -l)

    ram_total=$(free --mega | awk '$1 == "Mem:" {print $2}')
    ram_use=$(free --mega | awk '$1 == "Mem:" {print $3}')
    ram_percent=$(free --mega | awk '$1 == "Mem:" {printf("%.2f%%",$3/$2*100)}')

    disk_total=$(df --total -h | grep "total" | awk '{printf("%s", $2)}')
    disk_use=$(df --total -h | grep "total" | awk '{printf("%s", $3)}')
    disk_percent=$(df --total -h | grep "total" | awk '{printf("%s", $5)}')

    cpu_load=$(vmstat -w 1 2 | tail -1 | awk '{printf("%.1f%%",100 - $15)}')

    last_boot=$(who -b | awk ' {print $3 " " $4}')

    lvm_use=$(if [ $(lsblk | grep "lvm" | wc -l) -gt 0 ]; then echo yes; else echo no; fi)

    tcp_co=$(ss -ta | grep ESTAB | wc -l)

    user_log=$(users | tr ' ' '\n'| sort -u | wc -l)

    ip=$(hostname -I)
    mac=$(ip link | grep "link/ether" | awk '{print $2}')

    sudo_cmd=$(journalctl _COMM=sudo | grep COMMAND | wc -l)

    wall "#Architecture : $architecture
    #CPU physical : $cpu_physical
    #vCPU : $cpu_virtuel
    #Memory Usage : $ram_use/$ram_total MB ($ram_percent)
    #Disk Usage : $disk_use/$disk_total ($disk_percent)
    #CPU load: $cpu_load
    #Last boot: $last_boot
    #LVM use: $lvm_use
    #Connections TCP: $tcp_co ESTABLISHED
    #User log: $user_log
    #Network: IP $ip ($mac)
    #Sudo: $sudo_cmd cmd"

## commande eval utile :

creer un user : 

    useradd <name>
    addgroup <group> #creer un group
    adduser <name> <group> #met user dans un group:

changer de hostname :

    sudo nano /etc/hostname 
