
# GNS3, EVE-NG, PNETLAB

## Journey installing those

***

> putty logs tweak
>
> `&H-&Y&M&D-&T.log`

## GNS3, EVE-NG

***

### GNS3

- project is on GNS3 VM
[david bombal gns playlist](https://www.youtube.com/watch?v=Ibe3hgP8gCA&list=PLhfrWIlLOoKNFP_e5xcx5e2GDJIgk3ep6)
- [install gns3](https://www.youtube.com/watch?v=Ibe3hgP8gCA)
and [this](https://www.youtube.com/watch?v=A0DEnMi09LY)
- GNS VM not starting/stuck "request POST blabla" solution: [restart the program](https://www.youtube.com/watch?v=Fk2SeAUVbYI)
- IOS image [filename](https://youtu.be/jhh2_PP9JLU?list=PLhfrWIlLOoKNFP_e5xcx5e2GDJIgk3ep6&t=289)
- IOS [previous download](https://software.cisco.com/download/home) <- just a historical IOS download in my professional career
- [Connect GNS3 to internet](https://www.youtube.com/watch?v=XLaPqRLSHy4) <- with Cloud object (NAT Cloud)
[IOS image switch](https://upw.io/75f?pt=ZEVRek56VlJkRXRZVURnMFdITkpVak5rV2xsbWR6MDlPalhZVElLV0FEK2p6TUhSWUgwOUg2az0%3D)
[IOS image router](https://upw.io/75a?pt=Wm1ad1N6bHNjbE16WWtsd055OUtLMHhxUVZWT1FUMDlPbWsvMzgxUkpmdXl1TEJ6Y3BZMU1IOD0%3D)
- Import all the image by creating manual template
- `ip default-gateway` command doesnt work in the switch... when showing `ip route`, no gateway of last resort is set it said, although the `ip default-gateway` command is configured as 10.1.1.1.
Only when looking into [this](https://www.cisco.com/c/en/us/support/docs/ip/routing-information-protocol-rip/16448-default.html), it works <- use `ip route 0.0.0.0 0.0.0.0 10.1.1.1` command
- when trying to use csr1000v, qemu binary: `/usr/bin/qemu-system-x86-64` (v4.2.1) <- same with all other images

> GNS3 VM IP: `192.168.58.130` <- `VMnet8`

### EVE-NG

- Download EVE-NG Free Community ed. [here](https://www.eve-ng.net/index.php/download) - choose EVE-NG free community ed.
- JUST SHARING [VMPlayer URL](https://customerconnect.vmware.com/en/downloads/details?downloadGroup=WKST-PLAYER-1623-NEW&productId=1039&rPId=85399)
- Follow [this video](https://youtu.be/Kxt5dvuAfNk)
(seems better not to choose "install update automatically", takes time to finish, now already 1000 secs and still doing update)
  - did wireshark also to see the traffic between NAT adapter & the ubuntu server.
    - src: `192.168.58.129`, dst: ubuntu server
    - NAT subnet ip: `192.168.58.0/24`
    - DHCP setting: `.58.128` - `.254`
    - Under NAT setting: Gateway IP = `192.168.58.2`
- setup via CLI:
  - `root:eve` -> changed to `root:admin`
  - hostname: `eve-bernhard`
  - dns domain for the system: `example.com`
  - dhcp: accidentally set to dhcp, not static
  - ntp: `sg.pool.ntp.org`
  - how VM connect to internet: direct connection
  - `apt-get update`
  - `apt-get upgrade`
  - `shutdown -h now`, and then disconnect CD-ROM

> EVE-NG IP: `http://192.168.58.129` <- using NAT VMnet8

- GNS3 IOS VIRL [how to add Cisco vIOS from VIRL](https://www.eve-ng.net/index.php/documentation/howtos/howto-add-cisco-vios-from-virl)

## PNETLAB

> cppm ip: `192.168.174.10`
>
> sw ip: `192.168.174.12`
>
> eve-ng ip: `192.168.174.33`
>
> pnetlab ip: `192.168.174.34`

1. download the OVA
2. static ip the OVA
3. ssh to the OVA <- from the workstation:
    1. find the ip by using `ifconfig|more`
    2. find the nic `pnet0`
    3. then login with `root:admin`
4. pull image using ishare [here](https://www.youtube.com/watch?v=94NpE4a2gT0). ishare search IOL, ishare pull. Download the IOL from [here](https://drive.google.com/drive/folders/16i5bceR4XL4l_HMt8iPnxtGekVTcgUmc).
5. Must look into [here](https://www.eve-ng.net/index.php/documentation/howtos/howto-add-cisco-iol-ios-on-linux) to see where i should really copy the images <- `/opt/unetlab/addons/iol/bin/`
6. fix permission [here](https://youtu.be/94NpE4a2gT0), or use [david bombal video](https://www.youtube.com/watch?v=YKYdq3Ww_C0)
7. add node, under IOL, run/start the switch <- **use HTML5 GUI !!!**, double-click the switch to open console
8. [enable ssh]:(https://www.thegeekstuff.com/2013/08/enable-ssh-cisco)
9. pnetlab download winxp [here](https://drive.google.com/drive/u/1/folders/1KgR5VGgMzMHOgVD_WPM5bdAP8VEk5WwF) <- video org indo, request access; di si orang arab [here](https://drive.google.com/drive/folders/16bM0uDfS58OXr7GYBQ0dmfOEJy_uUemi)
10. pake winxp gak bisa, mgkn dot1x nya uda jadul, pakenya win10, copy ke sini imagenya `sftp://root@192.168.174.34/opt/unetlab/addons/qemu/win-xp-Lite` <- notice nama foldernya
11. go to GUI pnetlab, do fix permission again
12. when adding windows node, choose `E1000` as network adapter, dont use pcnet, pcnet is undetectable.
13. enter username: `Test123` <- there is the password hint at the image

> pnetlab login `192.168.18.13:20000` `174.34`
> `matchabear:tXnvwj4!#9P34PM`

## NAT

from `192.168.18.13` (VM host PC) to VMs
| IP Address @ VM Network | NAT Port | Description |
| :--- | :---: | ---: |
| `192.168.174.10` | `21932` | cppm 6.9.9 `https` |
| `192.168.174.34` | `20000` | pnetlab `GUI` |
| `192.168.174.34` | `20012` | pnetlab `ssh/sftp` |
| `192.168.174.10` | `26922` | cppm 6.9.9 `ssh` |
| `192.168.174.12` | `20022` | switch `ssh` <- open with putty |
| `192.168.174.12` | `20023` | switch `telnet` <- open with putty |
| `192.168.174.16` | `20160` | ldap `RDP`/port `389` |
| `192.168.174.16` | `20161` | ldaps `636` |
| `192.168.174.9` | `20689` | cppm 6.8.9 `https` |
| `192.168.174.9` | `26822` | cppm 6.8.9 `ssh` |
| `192.168.174.188` | `20180` | cpSGH `https` |
| `192.168.174.188` | `20182` | cpSGH `ssh` |
| `192.168.174.29` | `29699` | cp69subs `https` |
| `192.168.174.29` | `29622` | cp69subs `ssh` |
| `192.168.174.29` | `25432` | cp69subs `postgresql 5432` |
| `192.168.174.27` | `20122` | check point `ssh` |
| `192.168.174.84` | `30443` | cp610-1 `https` (cp-pub1) |
| `192.168.174.84` | `30022` | cp610-1 `ssh` (cp-pub1) |
| `192.168.174.94` | `31443` | cp610-2 `https` (cp-sub1) |
| `192.168.174.94` | `31022` | cp610-2 `ssh` (cp-sub1) |

NAT - from home router to 192.168.18.0 segment
| Router Inside Port | Host Port |
| :---: | :---: |
| 443 | 21932 |
| 488 | 26922 |
| 444 | 20000 |
| 442 | 20689 |
| 446 | 3389 |
| 448 | 20180 |
| 449 | 20182 |
| 447 | 29622 |
| 450 | 29699 |
| 451 | 5900 |

## Free DDNS

Step 1 - Create a Hostname. (this step is already complete)
Step 2 - Download the Dynamic Update Client (DUC).
The DUC keeps your hostname updated with your current IP address.
Step 3 - Port Forward your router.
Done with all 3 steps?

> cppm: `https://matchabear96.ddns.net:443`
>
> pnetlab: `matchabear96.ddns.net:444`
>
> rdp: `berrydemo.ddns.net:446`
>
> vnc mac: `berrydem0.ddns.net:451`

## ACTIVE DIRECTORY windows 2016 datacenter evaluation

> `administrator:P@ssw0rd1234`

1. install VMware Tools 11.3.5.18557794, choose `Complete` option
2. `administrator:P@ssw0rd1234`
3. add role ([how to](https://www.c-sharpcorner.com/blogs/active-directory-domain-services-in-windows-server-2016))
4. After installation, configuration required it says, then there is this `promote this server to domain controller`, click, `Add a new forest`, enter value: `bernhomelab.iamgood` <- root domain name
5. deselect DNS server as domain controller capabilities. GC cannot be deselected. Leave RODC unticked.
6. Directory Services Restore Mode (DSRM) password: `I@mG00D`
7. netbios name: `BERNHOMELAB`
8. DATABASE folder: `C:\Windows\NTDS`
9. LOG files folder: `C:\Windows\NTDS`
10. SYSVOL volder: `C:\Windows\SYSVOL`

### **SUMMARY**

> Configure this server as the first Active Directory domain controller in a new forest.
>
> The new domain name is `bernhomelab.iamgood` This is also the name of the new forest.
>
> The NetBIOS name of the domain: `BERNHOMELAB`
>
> Forest Functional Level: `Windows Server 2016`
>
> Domain Functional Level: `Windows Server 2016`
>
> **Additional Options:**
>
> Global catalog: `Yes`
> DNS Server: `No`
>
> Database folder: C:\Windows\NTDS
>
> Log file folder: C:\Windows\NTDS
>
> SYSVOL folder: C:\Windows\SYSVOL

The password of the new domain Administrator will be the same as the password of the local Administrator of this computer.

### Windows PowerShell script for AD DS Deployment

> Import-Module ADDSDeployment
>
> Install-ADDSForest `
>
> -DatabasePath "C:\Windows\NTDS" `
>
> -DomainMode "WinThreshold" `
>
> -DomainName "bernhomelab.iamgood" `
>
> -DomainNetbiosName "BERNHOMELAB" `
>
> -ForestMode "WinThreshold" `
>
> -InstallDns:$false `
>
> -LogPath "C:\Windows\NTDS" `
>
> -NoRebootOnCompletion:$false `
>
> -SysvolPath "C:\Windows\SYSVOL" `
>
> -Force:$true

Windows Server 2016 domain controllers have a default for the security setting named "Allow cryptography algorithms compatible with Windows NT 4.0" that prevents weaker cryptography algorithms when establishing security channel sessions.

> For more information about this setting, see Knowledge Base article [942564](http://go.microsoft.com/fwlink/?LinkId=104751).
***
Domain Controller Promotion (dcpromo)

1. click Install to promote, then server restarts.
2. user created: hello world `helloworld@bernhomelab.iamgood`, pass: `P@ssw0rd`, password never expires
    1. [Replace ClearPass default self-signed cert](https://aventistech.com/replace-clearpass-default-self-sign-ssl-certificate)
    2. [802.1x WLAN using Aruba Controller >< ClearPass](https://wifiwizardofoz.com/802-1x-wlan-using-aruba-controller-clearpass)
    3. [Aruba ClearPass admin authentication >< AD](https://wifiwizardofoz.com/aruba-clearpass-admin-authentication-ad)
    4. [LDAP Admin](https://www.ldapadministrator.com/support_faq.htm)
    5. [Common LDAP Error Message](https://docs.oracle.com/cd/E19683-01/817-4843/auto46/index.html#:~:text=Sometimes%20the%20N2L%20server%20logs,of%2Ddate%20or%20incomplete%20results)
3. create new authentication source di clearpass, use helloworld user as bind DN
4. from softerra LDAP browser 4.5: (after creating a new group profile & add the AD)
    1. host: `192.168.18.13:20160` <- port forwarding set at vmware workstation's virtual network editor
    2. base dn: `DC=bernhomelab,DC=iamgood`
    3. URL: `ldap://192.168.18.13:20160/DC=bernhomelab,DC=iamgood` <- auto-generated
    4. credentials tab > Other credentials: Principal: use `helloworld@bernhomelab.iamgood` , pass: `P@ssw0rd`
    5. save configuration in softerra: `C:\Users\bernh\Documents\softerra` <- saved config file is in here

Install VMware Tools:
right click on vm, `manage` > `install vmware tools`

## DNS server winserver 2016

> `administrator:P@ssw0rd12345`

1. add role `dns server`
2. check at `.net framework 3.5`
3. `next next` until `install`
4. once done, click `Tools` > `DNS`
5. right click at the server icon, configure a dns server
6. zone name: `berrylab.com`
7. file is stored @ `%systemroot%\system32\dns`
8. ip: `192.168.174.61/24` gw `.174.2`
9. A record: `clabv689` (`clabv689.berrylab.com`) -> `192.168.174.16`
10. back to cppm: configure dns server as `.174.61`, 2nd: `1.0.0.1`, 3rd: `8.8.4.4`

failed to join domain error:
> Adding host to AD domain...
>
> INFO - Fetched REALM 'BERNHOMELAB.IAMGOOD' from domain FQDN `'clabv689.berrylab.com'`
>
> INFO - Fetched the NETBIOS name 'BERNHOMELAB'
>
> INFO - Creating domain directories for 'BERNHOMELAB'
>
> INFO - Using Administrator as the CLABV689's username
>
> Enter Administrator's password:
>
> kinit succeeded but ads_sasl_spnego_gensec_bind(KRB5) failed for
ldap/clabv689.berrylab.com with user[Administrator] realm[BERNHOMELAB.IAMGOOD]: Unexpected information received
>
> Failed to join domain: failed to connect to AD: Unexpected
information received
>
> INFO - Restoring smb configuration
>
> INFO - Deleting domain directories for 'BERNHOMELAB'
>
> ERROR - cp68 failed to join the domain BERNHOMELAB.IAMGOOD with
domain controller as clabv689.berrylab.com

11. not working with zone `berrylab.com`, created a new one: `iamgood.com` (still not the actual domain name, should be `bernhomelab.iamgood`)
12. created A record: bernhomelab (bernhomelab.iamgood.com) -> `192.168.174.16`

### Join domain error message

> Join domain failed
>
> Adding host to AD domain...
>
> INFO - Fetched REALM 'BERNHOMELAB.IAMGOOD' from domain FQDN
'bernhomelab.iamgood.com'
> INFO - Fetched the NETBIOS name 'BERNHOMELAB'
>
> INFO - Creating domain directories for 'BERNHOMELAB'
>
> INFO - Using Administrator as the BERNHOMELAB's username
>
> Enter Administrator's password:
>
> kinit succeeded but ads_sasl_spnego_gensec_bind(KRB5) failed for
ldap/bernhomelab.iamgood.com with user[Administrator] realm[BERNHOMELAB.IAMGOOD]: Unexpected information received
>
> Failed to join domain: failed to connect to AD: Unexpected
information received
>
> INFO - Restoring smb configuration
>
> INFO - Deleting domain directories for 'BERNHOMELAB'
>
> ERROR - cp68 failed to join the domain BERNHOMELAB.IAMGOOD with
domain controller as bernhomelab.iamgood.com
>
> Join domain failed

13. not working again, created a new zone: `iamgood` DOANG

14. created A record: `bernhomelab` (`bernhomelab.iamgood`) -> `192.168.174.16`

[Error trying to join AD domain](https://community.arubanetworks.com/community-home/digestviewer/viewthread?MID=16959)

Default IIS folder:
`C:\Users\bernh\Downloads`

Default: `%SystemDrive%\inetpub\wwwroot`

[EOF]

How to :

1. Aduk telur
2. Masukan adonan

> Hati2 dengan jumlah cuka

3. Lanjutkan dengan masukan bumbu
4. Diamkan 15 menit.
