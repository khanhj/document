https://archlinuxarm.org/platforms/armv5/seagate-goflex-home
- These instructions will void your warranty. While every precaution is taken to ensure nothing bad happens, all actions are at your own risk.
- my.pogoplug.com, the mobile applications, and the desktop Pogoplug connector will no longer work.
- Make sure to back up any data on the drive you plan to install on. Formatting the drive will delete any data on the drive.

1. With only the drive you intend to install Arch Linux ARM to plugged in (all data will be erased), switch on the power.
2. Set up a user in the device's web interface. If needed, perform a full reset by holding the reset button for at least 10 seconds.
3. With the device on and online, SSH in to the GoFlex Home.
    - Take note of the IP address associated with the device.
    - Take note of the product key located on the bottom of the unit, it will be in the format XXXX-XXXX-XXXX-XXXX.
    - Replacing USERNAME with the user you have set up in the Home's web interface, and using that user's password, SSH in:
```
ssh USERNAME_hipserv2_seagateplug_XXXX-XXXX-XXXX-XXXX@GOFLEX_HOME_IP
```
4. Gain root access:
```
sudo -E -s
```
5. Stop multiple daemons so they don't interfere with the install process (you can copy/paste):
```
killall -9 mynetworkd access-patrol seagate-lifecycle oe-spd xinetd udevd httpd avahi-daemon smbd nmbd vsftpd afpd minidlna mt-daapd check_igd.pl igd-daemon
```
6. Turn off swap:
```
/sbin/swapoff -a
```
7. Unmount the SATA drive so it can be formatted:
```
while [ `mount | grep sda1 | wc -l` -gt 0 ]; do umount -f /dev/sda1; done
```
8. Verify the drive is no longer mounted by looking for /dev/sda1 in the mount list:
```
mount | grep sda
```
9. Start fdisk to partition the SATA drive:
```
/sbin/fdisk /dev/sda
```
10. At the fdisk prompt, delete old partitions and create a new one:
    - Type o. This will clear out any partitions on the drive.
    - Type p to list partitions. There should be no partitions left.
    - Now type n, then p for primary, 1 for the first partition on the drive, and then press ENTER, to accept the default value for the beginning of the partition and +20G for the next prompt.
    - Create a partition for the remainder of the drive. Type n, then p for primary, 2 for the second partition on the drive, and then press ENTER to accept the rest of the default values.
    - Exit by typing w.
11. Create the ext3 filesystem:
```
cd /tmp
wget http://os.archlinuxarm.org/os/pogoplug/mke2fs
chmod +x mke2fs
./mke2fs -j /dev/sda1
mkdir alarm
mount /dev/sda1 alarm
```
12. Download and install Arch Linux ARM:
```
cd alarm
wget http://os.archlinuxarm.org/os/pogoplug/bsdtar
chmod +x bsdtar
wget http://os.archlinuxarm.org/os/ArchLinuxARM-kirkwood-latest.tar.gz
./bsdtar -xpf ArchLinuxARM-kirkwood-latest.tar.gz
cd ..
umount alarm
```
13. Download the U-Boot installer
```
wget http://os.archlinuxarm.org/os/armv5te/boot/goflexhome/goflexhome.sh
chmod +x goflexhome.sh
```
14. Run the installer to download and flash U-Boot:
```
./goflexhome.sh
```
15. If successful, reboot:
```
/sbin/reboot
```
16. The GoFlex Home will now reboot into Arch Linux ARM.
    - Login as the default user `alarm` with the password `alarm`.
    - The default `root` password is `root`.
17. Initialize the pacman keyring and populate the Arch Linux ARM [package signing](https://archlinuxarm.org/about/package-signing) keys:
```
pacman-key --init
pacman-key --populate archlinuxarm
```


CONVERT GOFLEX TO OLD VERSION:
-

After all sorts of banging my head against various brick walls trying to get my stupid goflex home back to stock, I think I finally figured it out. I couldn't get uboot to work, or net console, and all my attempts failed miserably. Eventually I found this:
http://projects.doozan.com/uboot/
Where he explains how to flash the NAND or mtd0 back to the stock firmware. The problem was the firmware was for the doskstar and he warned against using it. As a last ditch effort i tried using the kwb file from here:
http://goflex.scottn.us/
The resulting code is:
CODE: SELECT ALL
wget http://goflex.scottn.us/uboot-mtd0-orig-goflexhome.kwb
flash_erase /dev/mtd0 0 4
nandwrite /dev/mtd0 uboot-mtd0-orig-goflexhome.kwb


So far so good, it seems to have reverted back to the stock firmware, without even needing to go through the seagate flash process! Please keep in mind that I am a linux noob and may have totally botched this, but upon first looks, it seems that all is well! Use at your own risk!
Here are the specific steps I took:
1. SSH into your goflex home
2. enter
```
wget http://goflex.scottn.us/uboot-mtd0-orig-goflexhome.kwb
flash_erase /dev/mtd0 0 4
nandwrite /dev/mtd0 uboot-mtd0-orig-goflexhome.kwb
```
3. Reboot!
```
reboot
```
4. Check your router to see what ip the goflex has been assigned and use that IP to sign into the WebGui!
5. Be done!!!
6. Login account after reboot success:
```
ssh -oKexAlgorithms=+diffie-hellman-group1-sha1 admin_hipserv2_seagateplug_AAAA-BBBB-CCCC-DDDD@192.168.1.13
 admin_hipserv2_seagateplug_AAAA-BBBB-CCCC-DDDD
 admin1
```

CLONE DISK
-
```
dd if=/dev/sdb of=/dev/sdc bs=64K conv=noerror,sync status=progress

```
