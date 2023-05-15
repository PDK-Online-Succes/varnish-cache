## 
Install Docker on plesk version 6.6.2

![App Screenshot](https://github.com/PDK-Online-Succes/varnish-cache/blob/main/Readme%20Screenshots/Install_Docker.png?raw=true)

![App Screenshot](https://github.com/PDK-Online-Succes/varnish-cache/blob/main/Readme%20Screenshots/Install_Docker-2.png?raw=true)

## 
Install default.vcl to root

```bash
curl -o /tmp/default.vcl https://raw.githubusercontent.com/PDK-Online-Succes/varnish-cache/main/default.vcl
```

## 
Lookup public and local IP
```bash
Hostname -I
```

## 
Copy default.vcl to docker container and fill PUBLIC_IP and LOCAL_IP
```bash
sed -i -e 's/XXX.XXX.XXX.XXX/[PUBLIC_IP]/g' -e 's/xxx.xxx.xxx.xxx/[LOCAL_IP(hostname -I)]/g' /tmp/default.vcl && docker cp /tmp/default.vcl varnish:/etc/varnish/default.vcl
```

## 
Check default.vcl in docker container
```bash
docker exec -it varnish bash
```
```bash
apt-get update
```
```bash
apt-get Install nano
```
```bash
nano default.vcl
```

## 
Go back to root and restart docker container

```bash
docker restart varnish
```

## 
Disable "Permanent SEO-safe 301 redirect from HTTP to HTTPS" in Domain settings > Hosting & DNS > Hosting

![App Screenshot](https://github.com/PDK-Online-Succes/varnish-cache/blob/main/Readme%20Screenshots/Disable_301.png?raw=true)

## 
Add HTTP Header in Domain > Hosting & DNS > Apache & nginx > Additional directives for HTTP
```bash
SetEnvIf X-Forwarded-Proto "https" HTTPS=on
Header append Vary: X-Forwarded-Proto

<IfModule mod_rewrite.c>
RewriteEngine on
RewriteCond %{HTTPS} !=on
RewriteCond %{HTTP:X-Forwarded-Proto} !https [NC]
RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
</IfModule>
```
## 
Install Proxy on Domain > Dashboard > Docker Proxy Rules

![App Screenshot](https://github.com/PDK-Online-Succes/varnish-cache/blob/main/Readme%20Screenshots/Add_Proxy.png?raw=true)

## 
Enable Varnish add-on in WP-Rocket

![App Screenshot](https://github.com/PDK-Online-Succes/varnish-cache/blob/main/Readme%20Screenshots/Enable_Varnish.png?raw=true)
