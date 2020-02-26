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
172.20.20.10---eth3--| rt2 |--eth2--10.10.0.20--+---10.10.0.0/24
                     +-----+                    |
                                                |
                                                |
                     +-----+                    |
172.20.30.10---eth3--| rt3 |--eth2--10.10.0.30--+
                     +-----+
```

Your objective is to configure OSPF between rt1/rt2/rt3 to enable connectity between 172.20.x.x/24 networks.
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
vagrant@rt0:~$ show interfaces
Codes: S - State, L - Link, u - Up, D - Down, A - Admin Down
Interface        IP Address                        S/L  Description
---------        ----------                        ---  -----------
eth0             10.0.2.15/24                      u/u
eth1             10.10.0.1/24                      u/u
eth2             172.20.0.1/24                     u/u
lo               127.0.0.1/8                       u/u
                 ::1/128
vagrant@rt0:~$ show ip route
Codes: K - kernel route, C - connected, S - static, R - RIP, O - OSPF,
       I - ISIS, B - BGP, > - selected route, * - FIB route

S>* 0.0.0.0/0 [210/0] via 10.0.2.2, eth0
O   10.0.2.0/24 [110/10] is directly connected, eth0, 00:02:28
C>* 10.0.2.0/24 is directly connected, eth0
O   10.10.0.0/24 [110/10] is directly connected, eth1, 00:02:28
C>* 10.10.0.0/24 is directly connected, eth1
C>* 127.0.0.0/8 is directly connected, lo
O   172.20.0.0/24 [110/10] is directly connected, eth2, 00:02:28
C>* 172.20.0.0/24 is directly connected, eth2
O>* 172.20.10.0/24 [110/20] via 10.10.0.10, eth1, 00:01:56
O>* 172.20.20.0/24 [110/20] via 10.10.0.20, eth1, 00:02:06
vagrant@rt0:~$ ping 172.20.20.1 interface 172.20.0.1
PING 172.20.20.1 (172.20.20.1) from 172.20.0.1 : 56(84) bytes of data.
64 bytes from 172.20.20.1: icmp_req=1 ttl=64 time=0.630 ms
64 bytes from 172.20.20.1: icmp_req=2 ttl=64 time=0.439 ms
^C
--- 172.20.20.1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1001ms
rtt min/avg/max/mdev = 0.439/0.534/0.630/0.098 ms
vagrant@rt0:~$
```


#### 5. Destroy VM
```vagrant destroy```