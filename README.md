# GNS3-EVENG
 journey installing those



GNS3, EVE-NG

====================

gns3: project is on gns3 vm
david bombal gns playlist: https://www.youtube.com/watch?v=Ibe3hgP8gCA&list=PLhfrWIlLOoKNFP_e5xcx5e2GDJIgk3ep6
install gns3: https://www.youtube.com/watch?v=Ibe3hgP8gCA
and this: https://www.youtube.com/watch?v=A0DEnMi09LY
gns vm not starting/stuck "request POST blabla" solution: restart the program https://www.youtube.com/watch?v=Fk2SeAUVbYI
IOS image filename: https://youtu.be/jhh2_PP9JLU?list=PLhfrWIlLOoKNFP_e5xcx5e2GDJIgk3ep6&t=289
IOS previous download: https://software.cisco.com/download/home <- just a historical IOS download in my professional career

Connect GNS3 to internet: https://www.youtube.com/watch?v=XLaPqRLSHy4 <- with Cloud object (NAT Cloud)
IOS image switch: https://upw.io/75f?pt=ZEVRek56VlJkRXRZVURnMFdITkpVak5rV2xsbWR6MDlPalhZVElLV0FEK2p6TUhSWUgwOUg2az0%3D
IOS image router: https://upw.io/75a?pt=Wm1ad1N6bHNjbE16WWtsd055OUtLMHhxUVZWT1FUMDlPbWsvMzgxUkpmdXl1TEJ6Y3BZMU1IOD0%3D

	- Import all the image by creating manual template

**IP DEFAULT-GATEWAY** command doesnt work in the switch... when showing ip route, no gateway of last resort is set it said, although the ip default-gateway command is configured as 10.1.1.1
Only when looking into this, it works: https://www.cisco.com/c/en/us/support/docs/ip/routing-information-protocol-rip/16448-default.html <- use ip route 0.0.0.0 0.0.0.0 10.1.1.1 command

when trying to use csr1000v, qemu binary: /usr/bin/qemu-system-x86-64 (v4.2.1) <- same with all other images

GNS3 VM IP: 192.168.58.130 <- VMnet8

https://www.eve-ng.net/index.php/download/ - choose EVE-NG free community ed.
JUST SHARING (vmplayer url) https://customerconnect.vmware.com/en/downloads/details?downloadGroup=WKST-PLAYER-1623-NEW&productId=1039&rPId=85399

follow this video: https://youtu.be/Kxt5dvuAfNk
(seems better not to choose "install update automatically", takes time to finish, now already 1000 secs and still doing update.
	- did wireshark also to see the traffic between NAT adapter & the ubuntu server.
		- src: 192.168.58.129, dst: ubuntu server
		- NAT subnet ip: 192.168.58.0/24
		- DHCP setting: 58.128-.254
		- Under NAT setting: Gateway IP = 192.168.58.2
	
root:eve -> changed to root:admin
hostname: eve-bernhard
dns domain for the system: example.com
dhcp: accidentally set to dhcp, not static
ntp: sg.pool.ntp.org
how VM connect to internet: direct connection
apt-get update
apt-get upgrade
shutdown -h now, and then disconnect CD-ROM

EVE-NG IP: http://192.168.58.129 <- using NAT VMnet8


GNS3
IOS VIRL: https://www.eve-ng.net/index.php/documentation/howtos/howto-add-cisco-vios-from-virl/

		
======================

PNETLAB
1. download the OVA
2. static ip the OVA
3. ssh to the OVA <- find the ip by using: "ifconfig|more" , find the nic "pnet0"
4. pull image using ishare https://www.youtube.com/watch?v=nKJsGjzpOck
5. 



