## /etc/named.conf
```
options {
        listen-on port 53 { 127.0.0.1; 192.168.4.220; };
        allow-query     { localhost; 192.168.4.0/24; };
        directory       "/var/named/bmctest";
        ## Vergeet directory niet aan te maken!
};

zone "bmc.test" IN {
        type master;
        file "/var/named/bmc.test.db";
};

zone "4.168.192.in-addr.arpa" in {
        type master;
        file "/var/named/4.168.192.db";
};
```
## /var/named/bmc.test.db
```conf
$TTL 5M
@       IN       SOA     rocky1.bmc.test. hostmaster.bmc.test. (
                                        2023100604      ; serial
                                        3M      ; refresh
                                        1M      ; retry
                                        30D     ; expire
                                        1M )    ; minimum

        IN      NS      rocky1.bmc.test.

rocky1.bmc.test.        IN      A       192.168.4.220
rhel1.bmc.test.         IN      A       192.168.4.219
www.bmc.test.           IN      CNAME   rocky1.bmc.test.
```
## /var/named/4.168.192.db
```conf
$TTL 5M
@       IN      SOA     rocky1.bmc.test.        hostmaster.bmc.test. (
                        2023100401  ; Serial Number (YYYYMMDDNN)
                        180         ; Refresh
                        60          ; Retry
                        2592000     ; Expire
                        60 )        ; Minimum TTL

        IN      NS      rocky1.bmc.test.

220     IN      PTR     rocky1.bmc.test.
254     IN      PTR     bmc-dc-01.bmc.test.
```
## Firewall rule
```bash
sudo firewall-cmd --runtime-to-permanent --add-service=dns
sudo firewall-cmd --reload
```
## DNS test
`dig +noall +answer rocky1.bmc.test @127.0.0.1`
## Config test
`sudo -u named named-checkconf -z`