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

http://192.168.58.129


GNS3
IOS VIRL: https://www.eve-ng.net/index.php/documentation/howtos/howto-add-cisco-vios-from-virl/

		




