# portainer_ddns
A docker-compose stack to get portainer running on your home pc, featuring ddns and https
---

## Guide
1. Get yourself a dynamic-dns pointing to your public internet IP address.
For thie example, I will be using https://www.noip.com as my provider and my custom hostname will be **example.ddns.net**
Create a new **"A" record**.

2. Make sure your home pc is getting assigned a static IP address from your router. The following step depends on this.

This is also known as *static IP address* or *IP reservation*. This varies depending on the device model and manufacturer, but you can take a look on this guide [here](http://blog.dlink.com/mastering-static-ip-addresses-2/)

3. Add 2 port forwarding rules from the external world to you home pc
 
80 -> 192.168.0.2:80

443 -> 192.168.0.2:443

4. Make sure you have docker and docker-compose installed

5. Clone this repo
```
$ git clone
```

6. Start the stack
```
$ cd portainer_ddns
$ docker-compose up -d
```

7. Access 

---
## Environment variables
CADDY_CERT_EMAIL

CADDY_DDNS_HOST

---
## Features provided by Caddy

* HTTP -> HTTPS automatic redirection
* GZIP Compresion
* Automatic, free SSL certificates provided by Lets Encrypt
