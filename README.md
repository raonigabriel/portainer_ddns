# portainer_ddns
A docker-compose stack to get portainer running on your home pc / cloud vm, featuring ddns and https
---

## Guide
1. Get yourself a dynamic-dns pointing to your public internet IP address.
For this example, I will be using https://www.noip.com as my provider and my custom hostnames will be: **myportainer.ddns.net** and **mysite.servehttp.com**

Create a new **A** record for **myportainer.ddns.net** pointing to [your external IP](https://whatismyipaddress.com/). 

Create a new **CNAME** recor for **mysite.servehttp.com** pointing to **myportainer.ddns.net**


2. Make sure your home pc is getting assigned a static IP address from your router. The following step depends on this.

This is also known as *static IP address* or *IP reservation*. This varies depending on the device model and manufacturer, but you can take a look on this guide [here](http://blog.dlink.com/mastering-static-ip-addresses-2/)

3. Add 2 port forwarding rules from the external world to you home pc:
For this example, imagine that your router IP address is 192.168.0.1 and your pc IP address is **192.168.0.2**
 
80 -> 192.168.0.2:80

443 -> 192.168.0.2:443

4. Make sure you have docker and docker-compose installed

5. Clone this repo
```
$ git clone https://github.com/raonigabriel/portainer_ddns.git
```

6. Start the stack
```
$ cd portainer_ddns
$ docker-compose up -d
```

7. Browse to your portainer at https://myportainer.ddns or your site at https://mysite.servehttp.com

---
## Environment variables
* CADDY_CERT_EMAIL
* CADDY_HOSTNAME_PORTAINER
* CADDY_HOSTNAME_STATIC

---
## Features provided by Caddy

* HTTP -> HTTPS automatic redirection
* GZIP Compression
* Automatic, free SSL certificates provided by Lets Encrypt
* Static web site hosting
