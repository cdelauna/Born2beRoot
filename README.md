# Born2beRoot

script :

    archicteture : uname -a 
    network: hostname -I (ip link | grep "link/ether" | awk '{print $2}')
    user log: user | wc -w
