# raspberrypi_ubuntu

How to edit Ubuntu image of Raspberry Pi

## ubuntu-18.04.2-preinstalled-server-arm64+raspi3.img.xz

```sh
cd ~/Downloads
curl -O http://cdimage.ubuntu.com/ubuntu/releases/bionic/release/ubuntu-18.04.2-preinstalled-server-arm64+raspi3.img.xz
xz -kdv ubuntu-18.04.2-preinstalled-server-arm64+raspi3.img.xz
sudo kpartx -a ubuntu-18.04.2-preinstalled-server-arm64+raspi3.img
sudo mount /dev/mapper/loop11p2 /mnt
cd /mnt/etc/apt/apt.conf.d/
sudo sed -i 's/1/0/g' 20auto-upgrades
cd /mnt/etc/systemd/system/network-online.target.wants
sudo rm -rf systemd-networkd-wait-online.service
sudo ln -s '/dev/null' systemd-networkd-wait-online.service
sudo dd if=/dev/zero of=/mnt/dummy bs=4096
sudo rm /mnt/dummy
cd ~/Downloads
sudo umount /mnt
sudo kpartx -d /dev/loop11
sudo losetup -d /dev/loop11
mv ubuntu-18.04.2-preinstalled-server-arm64+raspi3.img ubuntu-18.04.2-preinstalled-server-arm64+raspi3-20190303.img
xz -kvz ubuntu-18.04.2-preinstalled-server-arm64+raspi3-20190303.img
```
