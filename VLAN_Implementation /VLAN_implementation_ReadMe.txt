Apeksha Lanjile
apeksha7992@gmail.com



Inter-Vlan network communication 
This project aims at understanding how to
- configure a network with multiple VLANs (VLANS)
- establish inter-Vlan communication by implementing router-on-a-stick (ROAS)
- establish L3 network connectivity by implementing EIGRP protocols on routers (EIGRP)
- Efficient use of given IP address range by using VLSM to minimize global IP address assignment (VLSM)

IP assignment:

There are 6 VLANs in the network - 10, 20, 30, 40, 50, 60.
Each Vlan is assigned IP addresses from a different network.
A network block of 10.10.10.0/26 is given.
Thus, all devices should be assigned an IP address within this range.
Since each Vlan should be in a different network, VLSM is used.
Thus following are the network IDs of each Vlan.


Vlan	#interfaces		Network ID
10	6		10.10.10.0/29
20	4		10.10.10.8/29
30	4		10.10.10.16/29
40	4		10.10.10.24/29
50	3		10.10.10.32/29
60	5		10.10.10.40/29

R1-R2	2		10.10.10.48/30
R2-R3	2		10.10.10.52/30


Routing:
Routers R1, R2 and R3 are configured with EIGRP protocol (All with AS 100) so as to achieve full network connectivity.
Inter-VLAN communication is achieved through Router on a stick configuration. The router interface that connects
the switch is configured with sub-interfaces.
VLSM reduces the IP range needed to configure the network. 


Challenges faced:
I could not connect a host to the topology because there were no VMs attached to GNS3. When I run GNS3 as a root user, a single host used my local machine’s NIC and made my machine a dummy one. Hence, this option didn’t solve my problem. Also, it made my internet connection dead on the local machine. I later realized that in order to only check the connectivity of topology a Virtual PC simulator (VPCS) could be used. Hence, I used that in my topology design.

I could not ping from Vlan 10 to Vlan 20. So, I had to troubleshoot R2 and R5 (Switch 2) to check for any configuration errors.
troubleshooting  steps included
- check if any host from vlan 10 could ping another host in the same vlan. Do this for vlan 20 too.
  This made sure my VLANs were configured correctly. 
- check if the switch interface connecting to the router was in the trunk mode
  This made sure packets from different VLANs could be trunked together
- check if the sub interfaces have IP addresses (default gateways) in the respective networks. 
  This made sure packets from one vlan could reach the other vlan.
  That is where I found configuration issue !! I had assigned correct IP addresses on sub-interfaces but on a different
  interface !!! Instead of Fa0/0, I had configured it on Fa1/0. Thus, I corrected it and then vlan 10 could connect to vlan 20.




Note: Don’t forget to save all your configs by typing copy run start before turning the device off. 
All the start up configs are stored in <RouterName>_startup-config.cfg files in the project folder.
