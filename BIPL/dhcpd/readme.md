## /etc/dhcp/dhchpd.conf
```conf
subnet 192.168.5.0 netmask 255.255.255.0 {
  range 192.168.5.100 192.168.5.150;
  option domain-name-servers rocky1.bmc.test;
  option domain-name "bmc.test";
  option routers 192.168.5.254;
  default-lease-time 600;
  max-lease-time 7200;
}

#
# DHCP Server Configuration file.
#   see /usr/share/doc/dhcp-server/dhcpd.conf.example
#   see dhcpd.conf(5) man page
```

## Firewall rule
```bash
sudo firewall-cmd --runtime-to-permanent --add-service=dhcp
sudo firewall-cmd --reload
```
