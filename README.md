# GNS3-EVENG
 journey installing those

==========================
putty logs tweak
&H-&Y&M&D-&T.log
==========================


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
3. ssh to the OVA <- from the workstation: find the ip by using "ifconfig|more" , find the nic "pnet0" , then login with root:admin
4. pull image using ishare https://www.youtube.com/watch?v=94NpE4a2gT0 : ishare search iol, ishare pull
.. download the iol from here: https://drive.google.com/drive/folders/16i5bceR4XL4l_HMt8iPnxtGekVTcgUmc
.. must look into here to see where i should really copy the images: https://www.eve-ng.net/index.php/documentation/howtos/howto-add-cisco-iol-ios-on-linux/ <- /opt/unetlab/addons/iol/bin/
5. fix permission: https://youtu.be/94NpE4a2gT0 , or use david bombal video: https://www.youtube.com/watch?v=YKYdq3Ww_C0
6. add node, under IOL , run / start the switch <- **use HTML5 GUI !!!** , double-click the switch to open console
7. enable ssh: https://www.thegeekstuff.com/2013/08/enable-ssh-cisco/
	- cppm ip: 192.168.174.10, sw ip: 192.168.174.12, eve-ng ip: 192.168.174.33, pnetlab ip: 192.168.174.34
8. pnetlab download winxp: https://drive.google.com/drive/u/1/folders/1KgR5VGgMzMHOgVD_WPM5bdAP8VEk5WwF <- video org indo, request access
	- di si arab: https://drive.google.com/drive/folders/16bM0uDfS58OXr7GYBQ0dmfOEJy_uUemi
9. pake winxp gak bisa, mgkn dot1x nya uda jadul, pakenya win10, copy ke sini imagenya sftp://root@192.168.174.34/opt/unetlab/addons/qemu/win-xp-Lite <- notice nama foldernya
10. go to GUI pnetlab, do fix permission again
11. when adding windows node, choose E1000 as network adapter, dont use pcnet, pcnet is undetectable.
12. enter username: Test123 <- there is the password hint at the image


======================
pnetlab login 192.168.18.13:20000 174.34
matchabear
tXnvwj4!#9P34PM
======================

NAT
21932 -> cppm
20000 -> pnetlab
======================

free ddns

Step 1 - Create a Hostname. (this step is already complete)
Step 2 - Download the Dynamic Update Client (DUC).
The DUC keeps your hostname updated with your current IP address.
Step 3 - Port Forward your router.
Done with all 3 steps?

cppm: https://matchabear96.ddns.net:443
pnetlab: matchabear96.ddns.net:444


======================
ACTIVE DIRECTORY windows 2016 datacenter evaluation
======================
1. install vmware tools 11.3.5.18557794, choose Complete option
2. administrator:P@ssw0rd1234
3. add role https://www.c-sharpcorner.com/blogs/active-directory-domain-services-in-windows-server-2016
4. After installation, configuration required it says, then there is this promote this server to domain controller, click, Add a new forest , "bernhomelab.iamgood" <- root domain name
5. deselect DNS server as domain controller capabilities. GC cannot be deselected. Leave RODC unticked.
6. Directory Services Restore Mode (DSRM) password: I@mG00D
7. netbios name: BERNHOMELAB
8. DATABASE folder: C:\Windows\NTDS
LOG files folder: C:\Windows\NTDS
SYSVOL volder: C:\Windows\SYSVOL
===============
SUMMARY:
Configure this server as the first Active Directory domain controller in a new forest.

The new domain name is "bernhomelab.iamgood". This is also the name of the new forest.

The NetBIOS name of the domain: BERNHOMELAB

Forest Functional Level: Windows Server 2016

Domain Functional Level: Windows Server 2016

Additional Options:

  Global catalog: Yes

  DNS Server: No

Database folder: C:\Windows\NTDS

Log file folder: C:\Windows\NTDS

SYSVOL folder: C:\Windows\SYSVOL

The password of the new domain Administrator will be the same as the password of the local Administrator of this computer.
===============
#
# Windows PowerShell script for AD DS Deployment
#

Import-Module ADDSDeployment
Install-ADDSForest `
-DatabasePath "C:\Windows\NTDS" `
-DomainMode "WinThreshold" `
-DomainName "bernhomelab.iamgood" `
-DomainNetbiosName "BERNHOMELAB" `
-ForestMode "WinThreshold" `
-InstallDns:$false `
-LogPath "C:\Windows\NTDS" `
-NoRebootOnCompletion:$false `
-SysvolPath "C:\Windows\SYSVOL" `
-Force:$true
===============
Windows Server 2016 domain controllers have a default for the security setting named "Allow cryptography algorithms compatible with Windows NT 4.0" that prevents weaker cryptography algorithms when establishing security channel sessions.

For more information about this setting, see Knowledge Base article 942564 (http://go.microsoft.com/fwlink/?LinkId=104751).
===============
9. click Install to promote, then server restarts.
10. user created: hello world helloworld@bernhomelab.iamgood , pass: P@ssw0rd, password never expires
https://aventistech.com/replace-clearpass-default-self-sign-ssl-certificate/
https://wifiwizardofoz.com/802-1x-wlan-using-aruba-controller-clearpass
https://wifiwizardofoz.com/aruba-clearpass-admin-authentication-ad/
https://www.ldapadministrator.com/support_faq.htm
https://docs.oracle.com/cd/E19683-01/817-4843/auto46/index.html#:~:text=Sometimes%20the%20N2L%20server%20logs,of%2Ddate%20or%20incomplete%20results.
11. create new authentication source di clearpass, use helloworld user as bind DN
12. from softerra LDAP browser 4.5: (after creating a new group profile & add the AD)
- host: 192.168.18.13:20160 <- port forwarding set at vmware workstation's virtual network editor
- base dn: DC=bernhomelab,DC=iamgood
- URL: ldap://192.168.18.13:20160/DC=bernhomelab,DC=iamgood <- auto-generated
- credentials tab > Other credentials: Principal: use helloworld@bernhomelab.iamgood , pass: P@ssw0rd