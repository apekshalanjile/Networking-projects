Apeksha Lanjile
apeksha7992@gmail.com



Bgp_implementation project description

IP assignment:

There are 16 P2P links. So 32 IP addresses are needed. But each link belongs to a different network. So 16 subnets are needed. This means each network should have 32/16 = 2 usable IP addresses. So a /30 network suffices this need. 
The assigned networks are
192.168.15.0/30
192.168.15.4/30
192.168.15.8/30
192.168.15.12/30
192.168.15.16/30
192.168.15.24/30
192.168.15.28/30
192.168.15.32/30
192.168.15.36/30
192.168.15.40/30
192.168.15.44/30
192.168.15.48/30
192.168.15.52/30
192.168.15.56/30
192.168.15.60/30
192.168.15.64/30

Note: There is no 192.168.15.20/30 network as I deleted that link between R1 and R7 after  I had completed IP assignment to all links. So I did not reconfigure all networks later to accommodate that IP address range.

Routing:
There is a topology of 9 routers - R1 to R9.
All are configured with OSPF protocol, but with different Area ID. 
R1 - R5 belong to OSPF Area 3
R6 - R7 belong to OSPF Area 11
R8 - R9 belong to OSPF Area 89
Also,
routers R1 - R7 belong to BGP AS 100. 
routers R8 - R9 belong to BGP AS 200.

Aim: At least 1 router in each area should be able to connect to 1 router in every other area even across different AS. 

Hence, I’ve designed my network such that All the OSPF routes are advertised through BGP in other areas and across the two AS.
R5 and R6 form BGP adjacency and OSPF routes of Area 11 and Area 3 are advertised through them.
R2 and R8 form BGP adjacency and OSPF routes of Area 3 and Area 89 are advertised through them.
R7 and R9 form BGP adjacency and OSPF routes of Area 11 and Area 89 are advertised through them.

Also, two redundant BGP routes are created incase the primary BGP routers fail.
R5 and R2 form BGP adjacency so that routers in Area 11, 3, 89 are connected through them.
R4 and R9 form adjacency so that routers in Area 3, 89 are connected through them.


All the start up configs are stored in <RouterName>.cfg files in the project folder. 
