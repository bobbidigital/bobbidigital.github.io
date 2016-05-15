---
layout: post
title: Securely Connecting to Your Home Server
comments: true
author: Jeff
---

I've recently found the need to connect to my home network remotely quite a bit lately. There's a number of solutions out there to do this, including setting up your own [VPN tunnel](http://www.howtogeek.com/221001/how-to-set-up-your-own-home-vpn-server/) using some open source tools. While I am a fan of VPN, I've opted for a simpler solution using OpenSSH and port forwarding on your router.

The horror of [port forwarding](https://en.wikipedia.org/wiki/Port_forwarding) isn't necessarily the act of the forwarding itself, but the service in the background your forwarding to. I didn't feel comfortable having [Transmission](https://www.transmissionbt.com) or [Couchpotato](https://couchpota.to) publicly accessible from the web. It was less about someone submitting crazy torrent downloads and more about those services having potential vulnerabilities in their prepacked web servers. 


# Generating the SSH Keypair

The first thing you'll want to do is make sure you can login to the machine via a public/private key pair. In order to do that, you'll need to first generate a keypair.

```ssh-keygen -t rsa -b 4096 -o <key_file_name.key>```

You'll want a nice big fat key size (hence the 4096) just to future proof it. And considering this is for your home machine, the overhead you'll pay for it is largely irrelevant. This command will generate two files, the file name you specified as -o and a file of the same name with the .pub extension. 

**It is very important to understand the difference between these two keys**. One is the public key (.pub) which you are allowed to share with other systems for authentication. The other (without the .pub) is the private key, which you should **never, never, never** share. Your private key also requires specific file permissions, so you'll want to execute the following.

```chmod 700 <key_file_name.key>```

Now you need to get that public key on to the server. The easiest way to do that is using the command [ssh-copy-id](http://linux.die.net/man/1/ssh-copy-id). Once again, stress the importance of knowing the difference between the two keys, you should only copy your **public** key to the server. (The file ending in .pub)

```ssh-copy-id -i <key_file_name.key.pub> <user>@<ipaddress>```

It will ask you for your password and then copy the file to the correct location. Now to test that it works

```ssh -i <key_file_name.key> <user>@<ipaddress>```

If you set everything up right, you should be logged in without being prompted for a password. 



# Securing OpenSSH

The first thing you should do prior to forwarding OpenSSH

* Disable insecure ciphers. Out of the box OpenSSH has a number of insecure ciphers which can make your server susceptible to various attacks.

* Disable root logins. Seems odd that this is sometimes allowed depending on your distro. Very seldom do you want to allow root to login via an OpenSSH shell. It's better to have an unprivileged user login and then have to sudo to perform specific actions. This might seem like overkill for a single user system, but it's a good habit to get into.

* Disable the use of passwords. Sounds crazy right? Not really. You should only be using [public/private keypairs](http://readwrite.com/2013/09/19/keys-understanding-encryption/) to authenticate to your SSH server. This makes it impossible for your machine to be brute forced. Now you just have to make sure you protect your private key from other people accessing it.

Instead of just copy/pasting the OpenSSH config, I figured it made more sense to [put it on Github](https://github.com/bobbidigital/config_files/blob/master/sshd_config) so that we can continue to evolve and refine it over time. Check back periodically to see if there's any updates to the config.

# Enable Port Forwarding on your Router

Enabling port forwarding is specific to your router.  If you already know how to do it, then just make sure you forward port 22 to port 22 on your target server. If your home internet service provider is giving you a static IP address, then connecting is easy. If not you may want to look at a [dynamic DNS service](http://www.noip.com/free) so that as your IP address changes, your DNS record is updated.

If you need to check what your public IP address is, you can execute the follwoing

```
curl icanhazip.com
```
That should return your public IP address.

# SSH Tunneling

Now you can setup your SSH tunnel to send traffic over port 22 to any of the ports on the local machine. From your client, open a terminal and execute

```
ssh -i <private key> -L <port-to-forward-to>:<server ip>:<local port> <username>@<server ip>
```
So that's a handful. 

* The private key is from the key pair generated in the previous step.
*  port-to-forward - the port you want to connect to on the remote server. 
*  server ip - the public IP address (or DNS name if you set it up) of your router.  
*  Local port - the port on your local machine you'll connect to in order to connect to the remote server. For simplicity sake, I'd just use the port as the remote port. 
*  username@server ip - This is a combination of the user you'll be connecting to on the server along with the server ip. It will resemble an email address.

Example:  
```
ssh -i server.key -L 3000:plex.myserver.net:3000 jeff@plex.myserver.net
```

If you need to forward multiple ports, you can repeat the -L flag for as many ports as you need. 

The last step is to open your browser and go to "http://localhost:port"  where port is the local port you specified in the above command. Your port should be forwarded and connected to the remote server.

Voila, you're now communicating with your remote server securely.

**UPDATE**: Some folks have said that they have problems connecting remotely, with a "connection refused" or "server unexpectedly closed the connection". 

I've seen this happen on some setups and adding a localhost entry usually resolves the issue. In your /etc/hosts file just add an entry for 127.0.0.1 that matches your server's fully qualified domain name. (ex: plex.myserver.net)



