---
layout: post
status: publish
published: true
title: Configuring your NIC cards -- Solaris on Dell 2970/2950
author: Jeff
author_login: admin
author_email: jeff@allthingsdork.com
author_url: http://www.allthingsdork.com
excerpt: "Configuring the Solaris Network Interface\r\n\r\nIn this little installment
  I'll walk you through configuring your network interface card for Solaris. This
  was originally written for a client, but it should get you through it if you have
  ANY idea about computers.  Any questions feel free to drop me a line. \r\n"
wordpress_id: 250
wordpress_url: http://www.allthingsdork.com/?p=250
date: '2008-01-25 20:30:46 -0600'
date_gmt: '2008-01-26 00:30:46 -0600'
categories:
- linkedin
tags:
- linkedin
comments: []
---
<p>Configuring the Solaris Network Interface</p>
<p>In this little installment I'll walk you through configuring your network interface card for Solaris. This was originally written for a client, but it should get you through it if you have ANY idea about computers.  Any questions feel free to drop me a line.<br />
<a id="more"></a><a id="more-250"></a><br />
Once you've completed the Solaris install you'll need to remain at the console to do some preliminary configuration. First if thing we'll do is setup the Network Interface Card and it's appropriate settings. For this you'll need the Broadcom driver package. Login to the machine as the root user and insert the CD/DVD drive into the appropriate drive. NOTE: 2970 users should still be using the external drive. Once you've logged in launch a terminal session by right clicking on the empty desktop and clicking the "Terminal" option. At the command prompt execute the command `df`. If the "autofs" service is functioning correctly, the media you inserted should be automatically mounted.</p>
<p>Figure 2.<br />
Filesystem             size   used  avail capacity  Mounted on<br />
/dev/dsk/c4t0d0s0       99G    37G    60G    39%    /<br />
/devices                 0K     0K     0K     0%    /devices<br />
ctfs                     0K     0K     0K     0%    /system/contract<br />
proc                     0K     0K     0K     0%    /proc<br />
mnttab                   0K     0K     0K     0%    /etc/mnttab<br />
swap                    28G   876K    28G     1%    /etc/svc/volatile<br />
objfs                    0K     0K     0K     0%    /system/object<br />
/usr/lib/libc/libc_hwcap2.so.1<br />
                        99G    37G    60G    39%    /lib/libc.so.1<br />
fd                       0K     0K     0K     0%    /dev/fd<br />
swap                    28G   188K    28G     1%    /tmp<br />
swap                    28G    36K    28G     1%    /var/run<br />
/dev/dsk/c4t0d0s4      5.9G   6.0M   5.8G     1%    /globaldevices<br />
/dev/dsk/c4t0d0s3      295G   3.5G   289G     2%    /export/home<br />
/vol/dev/dsk/c2t0d0/sol_10_807_x86    421M   421M     0K   100%    /cdrom/sol_10_807_x86</p>
<p>You'll notice that the last line listed in the 'df' command shows the CD-rom is mounted on /cdrom/sol_10_807_x86. (Your output will probably differ slightly after the '/cdrom') To access the contents of the CD-rom simply 'cd' to the appropriate directory listed from the 'df' command. So using the above example we would execute 'cd /cdrom/sol_10_807_x86'. From here to add the Broadcom package you will execute the 'pkgadd' commmand and specify the device you would like to add. So from there you'll execute the command 'pkgadd -d ./BRCMbnx.pkg'.  You'll be prompted to confirm that this is indeed the file you want to add.</p>
<p>Figure 3.<br />
The following packages are available:<br />
  1  BRCMbnx                          Broadcom NetXtreme II Gigabit Ethernet Adapter Driver<br />
                                      (i386) 11.10.0,REV=2007.06.20.13.12</p>
<p>Select package(s) you wish to process (or 'all' to process<br />
all packages). (default: all) [?,??,q]:</p>
<p>There should only be one package offered in this option, in which case we can say 'all' to this and any other prompt that is given. You may receive several prompts, simply answer 'all' or 'y' to them appropriately. Once complete you'll have completed the installation of the NIC card driver, now we have to configure the device.</p>
<p>To configure the NIC card the first thing we need to do is 'plumb' the interface. Plumbing the interface makes it available to the Operating system. To do this, simply execute the command 'ifconfig bnx0 plumb'.  Lets breakdown the command a bit. The ifconfig command is the command used to do almost all interface configuration. (it's in fact short for InterFace CONFIGuration) Bnx0 is the interface ID. BNX being the name of the driver used to control the interface and the number being the number of the interface that is responding to that driver starting with 0. So if you have 3 Broadcom interfaces on this machine, then you'll have interfaces bnx0, bnx1 and bnx2 available for configuration. The 'plumb' keyword is just the command given to the interface to make it available for configuration and use by the OS. ALL interfaces must be plumbed prior to their use.</p>
<p>Now that the interface has been plumbed, we can begin configuring it. To assign the interface an ip address simply execute the command 'ifconfig bnx0 <ip addresss> netmask <netmask address>'. So for example if this interface was going to be 10.12.116.161 with a netmask of 255.255.255.0 we would execute the command 'ifconfig bnx0 10.12.116.161 netmask 255.255.255.0'. Once that's complete if we execute the command 'ifconfig -a' to list all the interfaces configured on the box we'll see our new interface with it's new address.</p>
<p>Figure 4.</p>
<p># ifconfig -a<br />
lo0: flags=2001000849<UP,LOOPBACK,RUNNING,MULTICAST,IPv4,VIRTUAL> mtu 8232 index 1<br />
        inet 127.0.0.1 netmask ff000000<br />
lo0:1: flags=2001000849<UP,LOOPBACK,RUNNING,MULTICAST,IPv4,VIRTUAL> mtu 8232 index 1<br />
        zone bpnode2<br />
        inet 127.0.0.1 netmask ff000000<br />
bnx0: flags=1000843<UP,BROADCAST,RUNNING,MULTICAST,IPv4> mtu 1500 index 2<br />
        inet 10.12.116.161 netmask ffffff00 broadcast 10.12.116.255<br />
        ether 0:1d:9:64:44:5e</p>
<p>Note that interfaces that have NOT been plumbed will not show up in the 'ifconfig -a' command. Only plumbed interfaces will appear. Now we need to bring the interface up by executing the command 'ifconfig bnx0 up'.  (Similarly 'ifconfig bnx0 down' will bring the interface down)</p>
<p>So now we have a configured interface, but we don't want to have to plumb it everytime we boot. Luckily there is a way to do this automatically. By creating a file in the '/etc/' directory called 'hostname.<interface name>' the system will automatically plumb the interface. If the file contains an IP address then that IP address will automatically be assigned to the interface once it's been plumbed. So to quickly create that we'll execute the command<br />
'echo <ip address> > /etc/hostname.<interface name'. So sticking with the above example the actual command will be</p>
<p>'echo 10.12.116.161 > /etc/hostname.bnx0'</p>
<p>For windows users you probably realize we haven't specified a default gateway for this interface. It's handled slightly different in the unix world. We're going to handle default gateways for the system as a whole. In order to do that we'll need to leverage the 'route' command to specify specific routes. The command is executed like so: 'route add <network> <gateway>'.  So if you wanted to route all traffic to the 172.16.2.0 network through 172.16.2.1 you would execute 'route add 172.16.2.0 172.16.2.1'.  Now our situation is a little different because we need a default gateway, but example given will be used later as we setup the cluster interfaces.  To create the default gateway we'll employ a slightly different method of the route command.</p>
<p>'route add default <gateway>'. This will tell us to what our DEFAULT route will be when a specific route isn't given. So lets assume our default gateway for our network is 10.12.116.1. The command executed will be 'route add default 10.12.116.1'.  Executing the command 'netstat -r' will display the routing table.</p>
<p>Figure 5.  Output of the 'netstat -r' command</p>
<p>Routing Table: IPv4<br />
  Destination           Gateway           Flags  Ref     Use     Interface<br />
-------------------- -------------------- ----- ----- ---------- ---------<br />
default              10.12.116.1          UG        1         20<br />
10.12.116.0          simsoldb1            U         1          9 bnx0<br />
localhost            localhost            UH        2        312 lo0</p>
<p>Showing us that our default route goes through the 10.12.116.1 gateway.</p>
<p>Again we don't want to have to add this every time we boot, so we'll take advantage of another special file called '/etc/defaultrouter'. When this file exists, the IP address inside the file will be used as the default route everytime the system is booted. So again we'll execute the command 'echo <gateway IP> > /etc/defaultrouter' or to continue with the above example 'echo 10.12.116.1 > /etc/defaultrouter'. Now on a reboot the gateway will be auto configured.</p>
<p>Next we need to add our network address to the '/etc/netmasks' file. The netmasks file contains a list of all the networks that system is aware of and what that networks netmask is. This aides in certain routing decisions by the system. To edit the /etc/netmasks file we'll need to use the VI editor. If you're not familiar with VI, you may want to read a quick primer in the appendix. VI is quite different than any Windows tool you've probably ever used.</p>
<p>Edit the netmask file and at the end of the file add the network address that you are part of and it's netmask. So if your network is 10.12.116 with a subnet mask of 255.255.255.0, you would add into the netmasks file</p>
<p>10.12.116.0    255.255.255.0</p>
<p>Save the file and continue to the next step.</p>
<p>Next we'll need to add our hostname to the /etc/hosts file. The /etc/hosts file is the Unix equivilant of the LMHOSTS file in windows. It's an address-to-server table that is used in the absence of DNS. If you're using DNS then chances are you don't need to make this addition. Simply add your server's IP address and it's hostname to the file using VI. So sticking with our example you would add:    </p>
<p>10.12.116.161    simsoldb1</p>
<p>Now just to ensure that we've got everything configured appropriately, try to ping your default gateway. To do this simply type 'ping <ip address>' just as you would in windows. Success should report back:</p>
<p>"10.12.116.1 is alive!"</p>
<p>failure will simply hang at the command for a few moments before reporting back:</p>
<p>If pinging your gateway did not work, go back and ensure that 1) You have your cables plugged into the CORRECT interface card.   2) That your interface card is in fact plugged into the network.  3) That you've brought the interface online with the 'ifconfig bnx0 up' command</p>
<p>Now assuming pinging your gateway does work, try pinging a machine that is not on your local network segment. This will test that your default gateway has been setup appropriately. If so you should receive the same succesful message. If not, verify that you've 1) added the default gateway 2) used the correct IP address 3) Can communicate with the gateway through a ping.</p>
<p>Now if you were not prompted for DNS information during the install, then we'll need to configure DNS manually. If you were prompted than you can skip this section.</p>
<p>Solaris gets it's DNS configuration information from a special file called '/etc/resolv.conf'. It holds all DNS related infomration including which nameservers to use, which domain your machine is part of as well as what search domains should be used when an FQDN is not supplied. To start using DNS, the first thing you'll need to do is create /etc/resolv.conf file and add to it (at the very least) a name server directive. You do this by typing on a single line 'nameserver <ip address of DNS server>'. So if our DNS server was 10.30.5.70, you would specify 'nameserver 10.30.5.70'. Only one directive is allowed per line. Other directives include</p>
<p>search -- A domain suffix to search for when an FQDN isn't specified<br />
domain -- what Domain this box currently belongs to.</p>
<p>The file is read from the top down, so directives are processed in the order they're found in the file.</p>
<p>Figure 6. Sample '/etc/resolv.conf'</p>
<p>nameserver 10.30.5.70<br />
nameserver 10.30.5.122<br />
search allthingsdork.com<br />
search BPD.allthingsdork.com</p>
<p>Next you'll need to edit the /etc/nsswitch.conf file. This file tells the system where it should be looking for hostname information. Open /etc/nsswitch.conf and scroll down to the "hosts" entry. Just make sure the line reads:</p>
<p>hosts    file dns</p>
<p>This tells Solaris to first look for host information in /etc/hosts, followed by a search through DNS. This should complete your network setup. </p>
