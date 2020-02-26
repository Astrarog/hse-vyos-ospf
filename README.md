# VyOS OSPF Practical Activity
### Task description
You have the following topology:
```

                     +-----+
172.20.10.10---eth3--| rt1 |--eth2--10.10.0.10--+
                     +-----+                    |
                                                |
                                                | 
                     +-----+                    |
172.20.20.10---eth3--| rt2 |--eth2--10.10.0.20--|---10.10.0.0/24
                     +-----+                    |
                                                |
                                                |
                     +-----+                    |
172.20.30.10---eth3--| rt3 |--eth2--10.10.0.30--+
                     +-----+
```

Your objective is to configure OSPF between rt1/rt2/rt3 to enable connectivity between 172.20.x.0/24 networks.
#### 1. Setup Vagrant
Download from https://www.vagrantup.com/downloads.html and install
#### 2. Pull repository
```git clone https://github.com/ivanlysogor/hse-vyos-ospf```
#### 3. Setup environment
```
cd hse-vyos-ospf
vagrant up
```
#### 4. Configure virtual routers
Configure virtual routers:
- hostname
- ospf zones

Hints:
- you can connect to you virtual routers with command ```vagrant ssh rt0```
- VyOS configuration documentation: https://docs.vyos.io/en/latest/

#### 5. Validate
Try to ping rt2 eth2 interface from rt0 eth2 interface
```
vagrant@rt1:~$ show ip ospf ne

    Neighbor ID Pri State           Dead Time Address         Interface            RXmtL RqstL DBsmL
10.10.0.20        1 Full/DROther      36.133s 10.10.0.20      eth1:10.10.0.10          0     0     0
10.10.0.30        1 Full/DR           36.645s 10.10.0.30      eth1:10.10.0.10          0     0     0
vagrant@rt1:~$ show ip route
Codes: K - kernel route, C - connected, S - static, R - RIP, O - OSPF,
       I - ISIS, B - BGP, > - selected route, * - FIB route

S>* 0.0.0.0/0 [210/0] via 10.0.2.2, eth0
O   10.0.2.0/24 [110/10] is directly connected, eth0, 00:03:34
C>* 10.0.2.0/24 is directly connected, eth0
O   10.10.0.0/24 [110/10] is directly connected, eth1, 00:03:34
C>* 10.10.0.0/24 is directly connected, eth1
C>* 127.0.0.0/8 is directly connected, lo
O   172.20.10.0/24 [110/10] is directly connected, eth2, 00:03:34
C>* 172.20.10.0/24 is directly connected, eth2
O>* 172.20.20.0/24 [110/20] via 10.10.0.20, eth1, 00:00:14
O>* 172.20.30.0/24 [110/20] via 10.10.0.30, eth1, 00:02:37
vagrant@rt1:~$ ping 172.30.30.10 interface 172.20.10.10
PING 172.30.30.10 (172.30.30.10) from 172.20.10.10 : 56(84) bytes of data.
^C
--- 172.30.30.10 ping statistics ---
4 packets transmitted, 0 received, 100% packet loss, time 3002ms

vagrant@rt1:~$ ping 172.20.30.10 interface 172.20.10.10
PING 172.20.30.10 (172.20.30.10) from 172.20.10.10 : 56(84) bytes of data.
64 bytes from 172.20.30.10: icmp_req=1 ttl=64 time=0.431 ms
64 bytes from 172.20.30.10: icmp_req=2 ttl=64 time=0.297 ms
64 bytes from 172.20.30.10: icmp_req=3 ttl=64 time=0.384 ms
^C
--- 172.20.30.10 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 1998ms
rtt min/avg/max/mdev = 0.297/0.370/0.431/0.059 ms
vagrant@rt1:~$
```


#### 5. Destroy VM
```vagrant destroy```