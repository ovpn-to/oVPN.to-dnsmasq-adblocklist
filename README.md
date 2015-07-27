# oVPN.to-dnsmasq-adblocklist

    # dnsmasq ads blocking list
    curl -s "http://hosts-file.net/ad_servers.txt" "https://adaway.org/hosts.txt" "http://pgl.yoyo.org/adservers/serverlist.php?hostformat=hosts&showintro=0&mimetype=plaintext" "http://winhelp2002.mvps.org/hosts.txt" "https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts" > hosts.dnstmp
    DATA=`grep -vE "#|localhost" hosts.dnstmp |dos2unix|column -t|sed 's/0\.0\.0\.0//g'|sed 's/127\.0\.0\.1//g'|sed -e 's/^[ \t]*//'| rev | cut -d. -f1,2,3,4 | rev | sort -u`
    for x in $DATA; do echo "server=/${x}/"; done > hosts.dnsblock && wc -l hosts.dnsblock
    finally add file "hosts.dnsblock" to dnsmasq.conf
