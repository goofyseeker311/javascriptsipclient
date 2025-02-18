# JavaScript SIP Client

Example web page that implements html/javascript websocket SIP/VOIP client on a website.

Requirements (debian linux server):
 * Apache HTTP Server 2.4.47 or later with mod_proxy, mod_proxy_http and mod_rewrite enabled.
 * Websockify to convert websocket to normal raw local socket.

Install:
```
sudo apt install apache2
sudo apt install websockify
```

Enable apache proxy/rewrite mods:
```
sudo a2enmod proxy
sudo a2enmod proxy_http
sudo a2enmod rewrite
```

Enable websockify websocket mirror:
```
websockify -D --log-file=/var/log/websockify.log 5059 localhost:5060
```

Apache site enable websocket rewrite:
```
RewriteEngine On
RewriteCond %{HTTP:Upgrade} =websocket [NC]
RewriteRule /wssip ws://localhost:5059/ [P,L]
ProxyPass /wssip http://localhost:5059/
ProxyPassReverse /wssip http://localhost:5060/
```
