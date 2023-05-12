# varnish-cache
Varnish Cache for Plesk
curl -o /tmp/default.vcl https://raw.githubusercontent.com/PDK-Online-Succes/varnish-cache/main/default.vcl?token=GHSAT0AAAAAACCSERWURK6WC66M4EMC36N4ZC6IGHA
hostname -I
sed -i 's/XXX.XXX.XXX.XXX/127.0.0.1/g' /tmp/default.vcl | docker cp - varnish:/etc/varnish/
docker exec -it varnish bash

