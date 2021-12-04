Task 1's Questions
1. What is the output of “nodes” and “net”
The output of "nodes" is:
available nodes are:
c0 h1 h2 h3 h4 h5 h6 h7 h8 s1 s2 s3 s4 s5 s6 s7

The output of "net" is:
h1 h1-eth0:s3-eth2
h2 h2-eth0:s3-eth3
h3 h3-eth0:s4-eth2
h4 h4-eth0:s4-eth3
h5 h5-eth0:s6-eth2
h6 h6-eth0:s6-eth3
h7 h7-eth0:s7-eth2
h8 h8-eth0:s7-eth3
s1 lo:  s1-eth1:s2-eth1 s1-eth2:s5-eth1
s2 lo:  s2-eth1:s1-eth1 s2-eth2:s3-eth1 s2-eth3:s4-eth1
s3 lo:  s3-eth1:s2-eth2 s3-eth2:h1-eth0 s3-eth3:h2-eth0
s4 lo:  s4-eth1:s2-eth3 s4-eth2:h3-eth0 s4-eth3:h4-eth0
s5 lo:  s5-eth1:s1-eth2 s5-eth2:s6-eth1 s5-eth3:s7-eth1
s6 lo:  s6-eth1:s5-eth2 s6-eth2:h5-eth0 s6-eth3:h6-eth0
s7 lo:  s7-eth1:s5-eth3 s7-eth2:h7-eth0 s7-eth3:h8-eth0
c0

2. What is the output of “h7 ifconfig”
The output of "h7 ifconfig" is:
h7-eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.0.0.7  netmask 255.0.0.0  broadcast 10.255.255.255
        inet6 fe80::f8b7:62ff:fe35:b103  prefixlen 64  scopeid 0x20<link>
        ether fa:b7:62:35:b1:03  txqueuelen 1000  (Ethernet)
        RX packets 69  bytes 5302 (5.3 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 11  bytes 866 (866.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0



Task 2's Questions
1.
Once a packet comes to the controller:
_handle_PacketIn() -> act_like_hub() -> resend_packet()

2.
a.
For h1 ping h2, it takes 3.590ms on average.
For h1 ping h8, it takes 20.992ms on average.
b.
For h1 ping h2, the minimum ping is 1.753ms, and the maximum ping is 9.151ms.
For h1 ping h8, the minimum ping is 9.899ms, and the maximum ping is 112.490ms.
c.
The time cost by h1 ping h8 is longer than h1 ping h2.
Because h1 ping h8 only needs s3 to forward packets, but h1 ping h8 needs s3, s2, s1, s5, s7 to forward packets.

3.
a.
"iperf" can create TCP and UDP data streams and measure the throughput of a network that is carrying them.
b.
For "iperf h1 h2", the throughputs are:
Results: ['3.59 Mbits/sec', '4.14 Mbits/sec']
For "iperf h1 h8",  the throughputs are:
Results: ['1.76 Mbits/sec', '2.22 Mbits/sec']
c.
The throughput from h1 to h2 is larger than which from h1 to h8.
Because from h1 to h8, there are more switches needed to forward packets.

4.
For "iperf h1 h2", s3 observes traffic.
For "iperf h1 h8", s3, s2, s1, s5, s7 observe traffic.


Task 3's Questions
1.
If the source MAC isn't in the map mac_to_port, add the {MAC, Port} into the map mac_to_port.
If the destination MAC is in the map, send the packet out the port associated with the MAC.
If  the destination MAC isn't in the map, output to all ports but the input port.

2.
a.
For h1 ping h2, it takes 2.824ms on average.
For h1 ping h8, it takes 10.486ms on average.
b.
For h1 ping h2, the minimum ping is 1.826ms, and the maximum ping is 6.001ms.
For h1 ping h8, the minimum ping is 5.635ms, and the maximum ping is 20.242ms.
c.
Compared to Task 2, it takes less time.
Because it has the mac_to_port map to save time.

3.
a.
For "iperf h1 h2", the throughputs are:
Results: ['28.2 Mbits/sec', '29.9 Mbits/sec']
For "iperf h1 h8",  the throughputs are:
Results: ['2.35 Mbits/sec', '2.75 Mbits/sec']
b.
"iperf h1 h2" has much larger throughput.
Because "iperf h1 h2" in Task 3 don't need flood packets everywhere after the mac_to_port map learnt the ports.
