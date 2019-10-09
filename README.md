# ip-country
IP addresses / Countries stuff: ripe-country-ips, ip2country, etc.

## Install GeoIP and ip2country (Debian 9 Stretch example)

    dpkg -l | grep -i geoip
    apt remove geoip-bin geoip-database geoip-database-contrib

    #?	ls -Al /usr/share/GeoIP/
    #?	rm -rf /usr/share/GeoIP/

    find /etc/cron* -iname "*geoip*"
    grep -i geoip /etc/crontab

    #? rm /etc/cron.../geoip...

    apt install geoipupdate mmdb-bin

    cp -v /usr/share/doc/geoipupdate/examples/GeoIP.conf.default /etc/GeoIP.conf

    # cat /etc/GeoIP.conf

> UserId 0<br>
> LicenseKey 000000000000<br>
> ProductIds GeoLite2-Country GeoLite2-City<br>

    geoipupdate

    echo "04 04 * * 2 root /usr/bin/geoipupdate" >>/etc/crontab

    # grep -ri geo /etc/cron*



    wget https://raw.github.com/mivk/ip-country/master/ip2country
    chmod -c +x ip2country
    mv -v ip2country /usr/local/bin/

