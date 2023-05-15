# varnish-cache
Varnish Cache for Plesk
curl -o /tmp/default.vcl https://raw.githubusercontent.com/PDK-Online-Succes/varnish-cache/main/default.vcl
hostname -I
sed -i -e 's/XXX.XXX.XXX.XXX/[PUBLIC_IP]/g' -e 's/xxx.xxx.xxx.xxx/[LOCAL_IP(hostname -I)]/g' /tmp/default.vcl && docker cp /tmp/default.vcl varnish:/etc/varnish/default.vcl
docker exec -it varnish bash
nano default.vcl
docker restart varnish
Permanent SEO-safe 301 redirect from HTTP to HTTPS uitzetten
http instellen:
SetEnvIf X-Forwarded-Proto "https" HTTPS=on
Header append Vary: X-Forwarded-Proto

<IfModule mod_rewrite.c>
RewriteEngine on
RewriteCond %{HTTPS} !=on
RewriteCond %{HTTP:X-Forwarded-Proto} !https [NC]
RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
</IfModule>
proxy instellen
wp-rocket addon aanzetten
