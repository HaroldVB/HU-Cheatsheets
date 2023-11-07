## Installeer Samba
`sudo dnf install samba -y`
## Rocky Linux commando's
```bash
sudo firewall-cmd --add-service=samba --runtime-to-permanent
sudo firewall-cmd --reload
sudo useradd hu                                 # een nieuwe user
sudo groupadd smbgrp                            # een nieuwe groep
sudo usermod -a -G smbgrp hu                    # we voegen de user hu toe aan de groep
sudo smbpasswd -a hu                            # we geven de user een Samba password
sudo mkdir /home/secure
sudo chown -R hu:smbgrp /home/secure/           # hu=owner, smbgrp=group
sudo chmod -R 0770 /home/secure/                # De owner+groep mag schrijven
sudo chcon -t samba_share_t /home/secure/       # ivm SELinux 
sudo systemctl restart smb nmb                  # Herstart SMB en NMB
sudo testparm                                   # SMB config test
```
## /etc/samba/smb.conf
```conf
[global]
workgroup = bmc
server string = Samba Server %v
netbios name = rocky1
security = user
map to guest = bad user
dns proxy = no
#==================== Share Definitions ======================
[secure]
path = /home/secure
valid users = @smbgrp
guest ok = no
writable = yes
browsable = yes
```