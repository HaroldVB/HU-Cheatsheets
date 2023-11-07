## /etc/named.conf
```
//
// named.conf
//
// Provided by Red Hat bind package to configure the ISC BIND named(8) DNS
// server as a caching only nameserver (as a localhost DNS resolver only).
//
// See /usr/share/doc/bind*/sample/ for example named configuration files.
//

options {
        listen-on port 53 { 127.0.0.1; 192.168.4.220; };
        allow-query     { localhost; 192.168.4.0/24; };
        directory       "/var/named/bmctest";
};

zone "bmc.test" IN {
        type master;
        file "/var/named/bmc.test.db";
};
```

