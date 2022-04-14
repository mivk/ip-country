# ip-country
IP addresses / Countries stuff

## Install get-ripe-ips

    wget https://github.com/mivk/ip-country/raw/master/get-ripe-ips
    chmod -c +x get-ripe-ips 
    mv -v get-ripe-ips /usr/local/bin/

Also make sure you have the [`jq` JSON processor](https://stedolan.github.io/jq/)  (install with `apt install jq` or similar)
## Install GeoIP and ip2country

### Cleanup old stuff

    dpkg -l | grep -i geoip
    apt remove geoip-bin geoip-database geoip-database-contrib

    #?	ls -Al /usr/share/GeoIP/
    #?	rm -rf /usr/share/GeoIP/

    find /etc/cron* -iname "*geoip*"
    grep -ri geo /etc/cron*

    #? rm /etc/cron.../geoip...

### Debian 9 Stretch

    apt install geoipupdate mmdb-bin

### Debian 8 (Jessie)

    wget http://ftp.ch.debian.org/debian/pool/main/libm/libmaxminddb/libmaxminddb0_1.2.0-1+b1_amd64.deb
    wget http://ftp.ch.debian.org/debian/pool/main/libm/libmaxminddb/mmdb-bin_1.2.0-1+b1_amd64.deb
    wget http://ftp.ch.debian.org/debian/pool/contrib/g/geoipupdate/geoipupdate_2.3.1-1_amd64.deb

    dpkg -i libmaxminddb0_1.2.0-1+b1_amd64.deb mmdb-bin_1.2.0-1+b1_amd64.deb geoipupdate_2.3.1-1_amd64.deb

### Finally

    cp -v /usr/share/doc/geoipupdate/examples/GeoIP.conf.default /etc/GeoIP.conf

    # cat /etc/GeoIP.conf

> UserId 0<br>
> LicenseKey 000000000000<br>
> ProductIds GeoLite2-Country GeoLite2-City<br>

    geoipupdate

    m=$(( RANDOM % 60 )); h=$(( RANDOM % 24 )); d=$(( RANDOM % 7 ))
    echo "$m $h * * $d root /usr/bin/geoipupdate" >>/etc/crontab

    wget https://raw.github.com/mivk/ip-country/master/ip2country
    chmod -c +x ip2country
    mv -v ip2country /usr/local/bin/
