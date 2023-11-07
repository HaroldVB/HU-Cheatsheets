## Nieuwe schijf tot LVM maken
```bash
sudo parted /dev/sdb mklabel gpt
sudo parted /dev/sdb mkpart primary ext4 1MiB 100%
sudo pvcreate /dev/sdb1
sudo vgcreate myvg /dev/sdb1
sudo lvcreate -n mylv -l 100%FREE myvg
sudo mkfs.ext4 /dev/myvg/mylv
sudo mkdir /mnt/mylv
sudo mount /dev/myvg/mylv /mnt/mylv
echo '/dev/myvg/mylv /mnt/mylv ext4 defaults 0 0' | sudo tee -a /etc/fstab
```