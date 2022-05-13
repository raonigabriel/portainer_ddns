# portainer_ddns
A docker-compose stack to get portainer running on your home pc / cloud vm, featuring ddns and https
---
## Features
* [Reverse proxy](https://caddyserver.com/docs/quick-starts/reverse-proxy) to Portainer UI
* [Automatic, free SSL certificates](https://caddyserver.com/docs/automatic-https) provided by [Lets Encrypt](https://letsencrypt.org/)
* [Automatic redirects HTTP](https://caddyserver.com/docs/automatic-https) calls to HTTPS
* [HTTP/2 right out of the box](https://caddyserver.com/)
* [GZIP Compression](https://caddyserver.com/docs/gzip)
* [Static web site](https://caddyserver.com/docs/quick-starts/static-files) hosting
* [Precompressed assets with brotli](https://misterorion.com/caddy-server-brotli/)
* [Cache-Control header](https://gtmetrix.com/serve-static-assets-with-an-efficient-cache-policy.html)  on jsdos assets
* HTTP/2 [Server Push](https://en.wikipedia.org/wiki/HTTP/2_Server_Push) on a big wasm file
---
## Environment variables (change them to your values)
* CADDY_CERT_EMAIL=me@example.com
* CADDY_HOSTNAME_PORTAINER=myportainer.ddns.net
* CADDY_HOSTNAME_SITE=mysite.sytes.net

You need to set those ENV variables on your host. You can add them [just for one single command](https://www.baeldung.com/linux/set-env-variables-bash-command#setting-multiple-variables-only-for-a-single-command) or [permanently](https://phoenixnap.com/kb/linux-set-environment-variable). I will use the first approach.

---
## Guide
1. Get yourself a dynamic-dns pointing to your public internet IP address.
For this example, I will be using https://www.noip.com as my provider and my custom hostnames will be: **myportainer.ddns.net** and **mysite.sytes.net**

Create a new **A** record for **myportainer.ddns.net** pointing to [your external IP](https://whatismyipaddress.com/). 

Create a new **CNAME** record for **mysite.sytes.net** pointing to **myportainer.ddns.net**


2. Make sure your home pc is getting assigned a static IP address from your router. The following step depends on this.

For this demo, imagine that your router IP address is **192.168.0.1** and your pc IP address is **192.168.0.2**

This is also known as *static IP address* or *IP reservation*. This varies depending on the device model and manufacturer, but you can take a look on this guide [here](http://blog.dlink.com/mastering-static-ip-addresses-2/)

3. Add 2 port forwarding rules from the external world to you home pc:

 
[EXTERNAL] 80 -> 192.168.0.2:80

[EXTERNAL] 443 -> 192.168.0.2:443

4. Make sure you have docker and docker-compose installed

5. Clone this repo
```
$ git clone https://github.com/raonigabriel/portainer_ddns.git
```

6. Start the stack, passing the variables **BEFORE** the docker-compose command
```
$ cd portainer_ddns
$ CADDY_CERT_EMAIL=me@example.com CADDY_HOSTNAME_PORTAINER=myportainer.ddns.net CADDY_HOSTNAME_SITE=mysite.sytes.net docker-compose up -d
```

7. Browse to your portainer at https://myportainer.ddns.net or your site at https://mysite.sytes.net
