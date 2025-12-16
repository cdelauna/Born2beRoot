# Born2beRoot

## script :

    archicteture : uname -a 
    CPU physical : grep "physical id" /proc/cpuinfo | wc -l
    vcpu : grep "processor" /proc/cpuinfo | wc -l
    ram : free --meta |akw '$1 == "Mem:" .......' 
    Disk usage:
    CPU load : (vmstat 1 2 | tail -1 | awk '{printf $15}') - 100
    last reboot : who -b | awk '$1 == "system" {print $3 " " $4}'
    LVM active : if [ $(lsblk | grep "lvm" | wc -l) -gt 0 ]; then echo yes; else echo no; fi
    TCP connection : ss -ta | grep ESTAB | wc -l
    user log: user | wc -w
    network: hostname -I (ip link | grep "link/ether" | awk '{print $2}')
    sudo command : journalctl _COMM=sudo | grep COMMAND | wc -l

## commande eval utile :

changer de hostname :

    sudo nano /etc/hostname 
