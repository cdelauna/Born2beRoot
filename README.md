# Born2beRoot

script :

    archicteture : uname -a 
    CPU physical :
    vcpu :
    ram : free --meta |akw '$1 == "Mem:" .......' 
    Disk usage:
    CPU load :
    last reboot : who -b | awk '$1 == "system" {print $3 " " $4}'
    LVM active : if [ $(lsblk | grep "lvm" | wc -l) -gt 0 ]; then echo yes; else echo no; fi
    TCP connection : ss -ta | grep ESTAB | wc -l
    user log: user | wc -w
    network: hostname -I (ip link | grep "link/ether" | awk '{print $2}')
    sudo command :
