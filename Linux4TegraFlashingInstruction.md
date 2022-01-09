```
REF-link if dead: https://developer.download.nvidia.com/embedded/L4T/r21_Release_v8.0/release_files/l4t_quick_start_guide.txt?GxjjpZmyHe6AwGtbzPPUZ88m-0CYUlpLCBA0R5q3-mQTtFgQa_bE3FBwNrtJEIdrAYU8I9NKmupFQqNrpDqaDKeCTfOvKohwERO8A_1HWk0Z2ufUjzEuZC6S5ygwZ5y3j5-A5UvQEo3e8vtYzYHpXkB4YRWsPOCFC7I1y_MS_bfYhMqB&t=eyJscyI6ImdzZW8iLCJsc2QiOiJodHRwczpcL1wvd3d3Lmdvb2dsZS5jb21cLyJ9
```

NVIDIA TEGRA LINUX DRIVER PACKAGE QUICK-START GUIDE

The information here is intended to help you quickly get started using
NVIDIA Tegra Linux Driver package (L4T).

ASSUMPTIONS:

- You have a Jetson-tk1 Tegra Developer System, equipped with the NVIDIA
  Tegra K1 32 bit family processor.
- You have a host machine that is running Linux.
- Your developer system is cabled as follows:
  - USB Micro-B cable connecting Jetson-tk1 (J1E1 USB0) to your Linux host for
    flashing.
  - (Not included in the developer kit)
    * Connect USB peripherals such as keyboard, mouse, and USB hub.
    * An HDMI cable plugged into "J1C1 HDMI1" on the target which
      is connected to an external HDMI display.
    * An Ethernet cable plugged into the J1D1 on board Ethernet port.
    * If you would like to connect to the debug console, a female to
      female NULL modem cable is required to plug into the serial port
      J1A2 UART4 on the target connected to your Linux host directly or
      through a serial-to-USB converter.
- The following directions will create a 14 GiB partition on the eMMC device
  (internal storage) and will flash the root file system to that location.

INSTRUCTIONS:

The directions below assume that ${RELEASE_NAME} refers to the
respective package name as follows:
```
    (${BOARD} refers to 'jetson-tk1')

    Jetson-tk1: Tegra124_Linux_R21.8.0_armhf.tbz2
```
1. Download the latest L4T release package for your developer system and the
   sample file system from https://developer.nvidia.com/linux-tegra

   If NVIDIA does not yet provide public release for the developer system you
   have, please contact your NVIDIA support representative to obtain the latest
   L4T release package for use with the developer board.

2. Untar the files and assemble the rootfs:
```
   sudo tar xpf ${RELEASE_NAME}
   cd Linux_for_Tegra/rootfs/
   sudo tar xpf ../../Tegra_Linux_Sample-Root-Filesystem_R21.8.0_armhf.tbz2
   cd ../
   sudo ./apply_binaries.sh
```
3. Flash the rootfs onto the system's internal eMMC.

   a) Put your system into "reset recovery mode" by holding down the RECOVERY
      button and press RESET button once on the main board.
      
   b) Ensure your Linux host system is connected to the target device
      through the USB cable for flashing.
```
      sudo ./flash.sh ${BOARD} mmcblk0p1  #This will take less than 10 minutes.
```
4. The target will automatically reboot upon completion of the flash. The
   command prompt will show up over the display that you have attached to
   the target. Log in as user login:ubuntu and password:ubuntu. All actions
   are completed unless you wish to configure the graphical desktop on your
   setup. You now have Linux running on your developer system.

5. Installing the graphical desktop on your target board (if not already
   installed):

   a) Make sure the Ethernet cable is connected.
   
   b) Use eth0 for the built-in Ethernet port:
```
      sudo dhclient eth0
```
   c) Check to see if Ethernet is up and running. You should see an IP address
      associated with eth0.
```
      ifconfig
      sudo apt-get update
      sudo apt-get install ubuntu-desktop
```
   d) Reboot and the system will boot to the graphical desktop.

   NOTE: the above steps can be used to install other packages with
```        
 sudo apt-get install
```
Please refer to the release notes provided with your software for up-to-date
information on platform features and use.


LOG
---

```
khanhj@4x4:~/Documents/D/L4T$ sudo tar xpf Tegra124_Linux_R21.8.0_armhf.tbz2 
khanhj@4x4:~/Documents/D/L4T$ ls
Linux_for_Tegra
Tegra124_Linux_R21.8.0_armhf.tbz2
Tegra_Linux_Sample-Root-Filesystem_R21.8.0_armhf.tbz2
ubuntu_trusty-l4t_hard_src.tbz2
khanhj@4x4:~/Documents/D/L4T$ cd Linux_for_Tegra/rootfs/
khanhj@4x4:~/Documents/D/L4T/Linux_for_Tegra/rootfs$ sudo tar xpf ../../Tegra_Linux_Sample-Root-Filesystem_R21.8.0_armhf.tbz2 
khanhj@4x4:~/Documents/D/L4T/Linux_for_Tegra/rootfs$ 
khanhj@4x4:~/Documents/D/L4T/Linux_for_Tegra/rootfs$ 
khanhj@4x4:~/Documents/D/L4T/Linux_for_Tegra/rootfs$ cd ..
khanhj@4x4:~/Documents/D/L4T/Linux_for_Tegra$ ls
apply_binaries.sh  bootloader  jetson-tk1.conf  laguna.conf       nv_tegra  shield.conf
ardbeg.conf        flash.sh    kernel           laguna_t124.conf  rootfs    source_sync.sh
khanhj@4x4:~/Documents/D/L4T/Linux_for_Tegra$ ./apply_binaries.sh 
This script requires root privilege
khanhj@4x4:~/Documents/D/L4T/Linux_for_Tegra$ sudo ./apply_binaries.sh 
Using rootfs directory of: /home/khanhj/Documents/D/L4T/Linux_for_Tegra/rootfs
Extracting the NVIDIA user space components to /home/khanhj/Documents/D/L4T/Linux_for_Tegra/rootfs
Extracting the BSP test tools to /home/khanhj/Documents/D/L4T/Linux_for_Tegra/rootfs
Extracting the NVIDIA gst test applications to /home/khanhj/Documents/D/L4T/Linux_for_Tegra/rootfs
Extracting the configuration files for the supplied root filesystem to /home/khanhj/Documents/D/L4T/Linux_for_Tegra/rootfs
Creating a symbolic link nvgstplayer pointing to nvgstplayer-1.0
Creating a symbolic link nvgstcapture pointing to nvgstcapture-1.0
Adding symlink /home/khanhj/Documents/D/L4T/Linux_for_Tegra/rootfs/usr/lib/arm-linux-gnueabihf/tegra/libcuda.so --> /home/khanhj/Documents/D/L4T/Linux_for_Tegra/rootfs/usr/lib/arm-linux-gnueabihf/tegra/libcuda.so.1.1
Adding symlink /home/khanhj/Documents/D/L4T/Linux_for_Tegra/rootfs/usr/lib/arm-linux-gnueabihf/tegra/libGL.so --> /home/khanhj/Documents/D/L4T/Linux_for_Tegra/rootfs/usr/lib/arm-linux-gnueabihf/tegra/libGL.so.1
Adding symlink /home/khanhj/Documents/D/L4T/Linux_for_Tegra/rootfs/usr/lib/arm-linux-gnueabihf/libcuda.so --> /home/khanhj/Documents/D/L4T/Linux_for_Tegra/rootfs/usr/lib/arm-linux-gnueabihf/tegra/libcuda.so
Adding symlink /home/khanhj/Documents/D/L4T/Linux_for_Tegra/rootfs/usr/lib/arm-linux-gnueabihf/tegra-egl/libEGL.so --> /home/khanhj/Documents/D/L4T/Linux_for_Tegra/rootfs/usr/lib/arm-linux-gnueabihf/tegra-egl/libEGL.so.1
Adding symlinks for systemd nv.service and nvfb.service
Extracting the firmwares and kernel modules to /home/khanhj/Documents/D/L4T/Linux_for_Tegra/rootfs
Extracting the kernel headers to /home/khanhj/Documents/D/L4T/Linux_for_Tegra/rootfs/usr/src
Adding symlink /home/khanhj/Documents/D/L4T/Linux_for_Tegra/rootfs/lib/modules/3.10.40-ge16a41a05c9e/build --> /usr/src/linux-headers-3.10.40-ge16a41a05c9e
Installing zImage into /home/khanhj/Documents/D/L4T/Linux_for_Tegra/rootfs/boot
Installing jetson-tk1_extlinux.conf* into /home/khanhj/Documents/D/L4T/Linux_for_Tegra/rootfs/boot/extlinux
Installing the board *.dtb files into /home/khanhj/Documents/D/L4T/Linux_for_Tegra/rootfs/boot
Success!
khanhj@4x4:~/Documents/D/L4T/Linux_for_Tegra$ ls
apply_binaries.sh  bootloader  jetson-tk1.conf  laguna.conf       nv_tegra  shield.conf
ardbeg.conf        flash.sh    kernel           laguna_t124.conf  rootfs    source_sync.sh
khanhj@4x4:~/Documents/D/L4T/Linux_for_Tegra$ sudo ./flash.sh jetson-tk1 mmcblk0p1
copying bctfile(/home/khanhj/Documents/D/L4T/Linux_for_Tegra/bootloader/ardbeg/BCT/PM375_Hynix_2GB_H5TC4G63AFR_H5TC4G63CFR_RDA_924MHz.cfg)... done.
copying bootloader(/home/khanhj/Documents/D/L4T/Linux_for_Tegra/bootloader/ardbeg/u-boot.bin)... done.
	populating kernel to rootfs... done.
	populating jetson-tk1_extlinux.conf.emmc to rootfs... done.
done.
Making system.img... 
	populating rootfs from /home/khanhj/Documents/D/L4T/Linux_for_Tegra/rootfs ... done.
	Sync'ing system.img ... done.
	Converting RAW image to Sparse image... 

---- Raw to Sparse Image Converter v1.0 ----------------------------
  0: RAW:     4231168(   1033 blks) ==>          28:4231180
  1: SKP:       40960(     10 blks) ==>     4231208:40972
  2: RAW:        8192(      2 blks) ==>     4231220:8204
  3: SKP:       57344(     14 blks) ==>     4239424:57356
  4: RAW:     2154496(    526 blks) ==>     4239436:2154508
  5: SKP:    31399936(   7666 blks) ==>     6393944:31399948
  6: RAW:     7786496(   1901 blks) ==>     6393956:7786508
  7: SKP:    88539136(  21616 blks) ==>    14180464:88539148
  8: RAW:       12288(      3 blks) ==>    14180476:12300
  9: SKP:     4194304(   1024 blks) ==>    14192776:4194316
 10: RAW:    14106624(   3444 blks) ==>    14192788:14106636
 11: SKP:        4096(      1 blks) ==>    28299424:4108
 12: RAW:    52289536(  12766 blks) ==>    28299436:52289548
 13: SKP:        4096(      1 blks) ==>    80588984:4108
 14: RAW:    11702272(   2857 blks) ==>    80588996:11702284
 15: SKP:        4096(      1 blks) ==>    92291280:4108
 16: RAW:      249856(     61 blks) ==>    92291292:249868
 17: SKP:        4096(      1 blks) ==>    92541160:4108
 18: RAW:     1585152(    387 blks) ==>    92541172:1585164
 19: SKP:       12288(      3 blks) ==>    94126336:12300
 20: RAW:      303104(     74 blks) ==>    94126348:303116
 21: SKP:        8192(      2 blks) ==>    94429464:8204
 22: RAW:      151552(     37 blks) ==>    94429476:151564
 23: SKP:        8192(      2 blks) ==>    94581040:8204
 24: RAW:      114688(     28 blks) ==>    94581052:114700
 25: SKP:       24576(      6 blks) ==>    94695752:24588
 26: RAW:      192512(     47 blks) ==>    94695764:192524
 27: SKP:       40960(     10 blks) ==>    94888288:40972
 28: RAW:      561152(    137 blks) ==>    94888300:561164
 29: SKP:        8192(      2 blks) ==>    95449464:8204
 30: RAW:       24576(      6 blks) ==>    95449476:24588
 31: SKP:       24576(      6 blks) ==>    95474064:24588
 32: RAW:      253952(     62 blks) ==>    95474076:253964
 33: SKP:       40960(     10 blks) ==>    95728040:40972
 34: RAW:      180224(     44 blks) ==>    95728052:180236
 35: SKP:       36864(      9 blks) ==>    95908288:36876
 36: RAW:      307200(     75 blks) ==>    95908300:307212
 37: SKP:       28672(      7 blks) ==>    96215512:28684
 38: RAW:      204800(     50 blks) ==>    96215524:204812
 39: SKP:       24576(      6 blks) ==>    96420336:24588
 40: RAW:       20480(      5 blks) ==>    96420348:20492
 41: SKP:       12288(      3 blks) ==>    96440840:12300
 42: RAW:      221184(     54 blks) ==>    96440852:221196
 43: SKP:       24576(      6 blks) ==>    96662048:24588
 44: RAW:       24576(      6 blks) ==>    96662060:24588
 45: SKP:        8192(      2 blks) ==>    96686648:8204
 46: RAW:      552960(    135 blks) ==>    96686660:552972
 47: SKP:       24576(      6 blks) ==>    97239632:24588
 48: RAW:      196608(     48 blks) ==>    97239644:196620
 49: SKP:       36864(      9 blks) ==>    97436264:36876
 50: RAW:       32768(      8 blks) ==>    97436276:32780
 51: SKP:       12288(      3 blks) ==>    97469056:12300
 52: RAW:      233472(     57 blks) ==>    97469068:233484
 53: SKP:       12288(      3 blks) ==>    97702552:12300
 54: RAW:       24576(      6 blks) ==>    97702564:24588
 55: SKP:       36864(      9 blks) ==>    97727152:36876
 56: RAW:      180224(     44 blks) ==>    97727164:180236
 57: SKP:       40960(     10 blks) ==>    97907400:40972
 58: RAW:       20480(      5 blks) ==>    97907412:20492
 59: SKP:       53248(     13 blks) ==>    97927904:53260
 60: RAW:      151552(     37 blks) ==>    97927916:151564
 61: SKP:       53248(     13 blks) ==>    98079480:53260
 62: RAW:      303104(     74 blks) ==>    98079492:303116
 63: SKP:       24576(      6 blks) ==>    98382608:24588
 64: RAW:      225280(     55 blks) ==>    98382620:225292
 65: SKP:        8192(      2 blks) ==>    98607912:8204
 66: RAW:       32768(      8 blks) ==>    98607924:32780
 67: SKP:       40960(     10 blks) ==>    98640704:40972
 68: RAW:      180224(     44 blks) ==>    98640716:180236
 69: SKP:       36864(      9 blks) ==>    98820952:36876
 70: RAW:      868352(    212 blks) ==>    98820964:868364
 71: SKP:       36864(      9 blks) ==>    99689328:36876
 72: RAW:      180224(     44 blks) ==>    99689340:180236
 73: SKP:       40960(     10 blks) ==>    99869576:40972
 74: RAW:       20480(      5 blks) ==>    99869588:20492
 75: SKP:       12288(      3 blks) ==>    99890080:12300
 76: RAW:      221184(     54 blks) ==>    99890092:221196
 77: SKP:       24576(      6 blks) ==>   100111288:24588
 78: RAW:       24576(      6 blks) ==>   100111300:24588
 79: SKP:       24576(      6 blks) ==>   100135888:24588
 80: RAW:      192512(     47 blks) ==>   100135900:192524
 81: SKP:       40960(     10 blks) ==>   100328424:40972
 82: RAW:       24576(      6 blks) ==>   100328436:24588
 83: SKP:        8192(      2 blks) ==>   100353024:8204
 84: RAW:      237568(     58 blks) ==>   100353036:237580
 85: SKP:       12288(      3 blks) ==>   100590616:12300
 86: RAW:      831488(    203 blks) ==>   100590628:831500
 87: SKP:        8192(      2 blks) ==>   101422128:8204
 88: RAW:      258048(     63 blks) ==>   101422140:258060
 89: SKP:       24576(      6 blks) ==>   101680200:24588
 90: RAW:      303104(     74 blks) ==>   101680212:303116
 91: SKP:       24576(      6 blks) ==>   101983328:24588
 92: RAW:      208896(     51 blks) ==>   101983340:208908
 93: SKP:       24576(      6 blks) ==>   102192248:24588
 94: RAW:      864256(    211 blks) ==>   102192260:864268
 95: SKP:       53248(     13 blks) ==>   103056528:53260
 96: RAW:      151552(     37 blks) ==>   103056540:151564
 97: SKP:       53248(     13 blks) ==>   103208104:53260
 98: RAW:      303104(     74 blks) ==>   103208116:303116
 99: SKP:       40960(     10 blks) ==>   103511232:40972
100: RAW:      176128(     43 blks) ==>   103511244:176140
101: SKP:       40960(     10 blks) ==>   103687384:40972
102: RAW:      270336(     66 blks) ==>   103687396:270348
103: SKP:       12288(      3 blks) ==>   103957744:12300
104: RAW:       20480(      5 blks) ==>   103957756:20492
105: SKP:       40960(     10 blks) ==>   103978248:40972
106: RAW:      180224(     44 blks) ==>   103978260:180236
107: SKP:       36864(      9 blks) ==>   104158496:36876
108: RAW:       24576(      6 blks) ==>   104158508:24588
109: SKP:        8192(      2 blks) ==>   104183096:8204
110: RAW:      237568(     58 blks) ==>   104183108:237580
111: SKP:       12288(      3 blks) ==>   104420688:12300
112: RAW:       20480(      5 blks) ==>   104420700:20492
113: SKP:       40960(     10 blks) ==>   104441192:40972
114: RAW:      180224(     44 blks) ==>   104441204:180236
115: SKP:       36864(      9 blks) ==>   104621440:36876
116: RAW:       24576(      6 blks) ==>   104621452:24588
117: SKP:       12288(      3 blks) ==>   104646040:12300
118: RAW:      233472(     57 blks) ==>   104646052:233484
119: SKP:       12288(      3 blks) ==>   104879536:12300
120: RAW:      258048(     63 blks) ==>   104879548:258060
121: SKP:       24576(      6 blks) ==>   105137608:24588
122: RAW:      303104(     74 blks) ==>   105137620:303116
123: SKP:       12288(      3 blks) ==>   105440736:12300
124: RAW:      233472(     57 blks) ==>   105440748:233484
125: SKP:       12288(      3 blks) ==>   105674232:12300
126: RAW:       24576(      6 blks) ==>   105674244:24588
127: SKP:       36864(      9 blks) ==>   105698832:36876
128: RAW:      208896(     51 blks) ==>   105698844:208908
129: SKP:       12288(      3 blks) ==>   105907752:12300
130: RAW:      270336(     66 blks) ==>   105907764:270348
131: SKP:        8192(      2 blks) ==>   106178112:8204
132: RAW:      303104(     74 blks) ==>   106178124:303116
133: SKP:       28672(      7 blks) ==>   106481240:28684
134: RAW:      192512(     47 blks) ==>   106481252:192524
135: SKP:       36864(      9 blks) ==>   106673776:36876
136: RAW:       24576(      6 blks) ==>   106673788:24588
137: SKP:       24576(      6 blks) ==>   106698376:24588
138: RAW:      208896(     51 blks) ==>   106698388:208908
139: SKP:       24576(      6 blks) ==>   106907296:24588
140: RAW:       24576(      6 blks) ==>   106907308:24588
141: SKP:       24576(      6 blks) ==>   106931896:24588
142: RAW:      253952(     62 blks) ==>   106931908:253964
143: SKP:       53248(     13 blks) ==>   107185872:53260
144: RAW:      167936(     41 blks) ==>   107185884:167948
145: SKP:       36864(      9 blks) ==>   107353832:36876
146: RAW:       24576(      6 blks) ==>   107353844:24588
147: SKP:        8192(      2 blks) ==>   107378432:8204
148: RAW:      237568(     58 blks) ==>   107378444:237580
149: SKP:       12288(      3 blks) ==>   107616024:12300
150: RAW:       20480(      5 blks) ==>   107616036:20492
151: SKP:       12288(      3 blks) ==>   107636528:12300
152: RAW:      237568(     58 blks) ==>   107636540:237580
153: SKP:        8192(      2 blks) ==>   107874120:8204
154: RAW:       24576(      6 blks) ==>   107874132:24588
155: SKP:       40960(     10 blks) ==>   107898720:40972
156: RAW:      180224(     44 blks) ==>   107898732:180236
157: SKP:       36864(      9 blks) ==>   108078968:36876
158: RAW:      278528(     68 blks) ==>   108078980:278540
159: SKP:       12288(      3 blks) ==>   108357520:12300
160: RAW:       24576(      6 blks) ==>   108357532:24588
161: SKP:        8192(      2 blks) ==>   108382120:8204
162: RAW:      237568(     58 blks) ==>   108382132:237580
163: SKP:       12288(      3 blks) ==>   108619712:12300
164: RAW:      303104(     74 blks) ==>   108619724:303116
165: SKP:        8192(      2 blks) ==>   108922840:8204
166: RAW:      270336(     66 blks) ==>   108922852:270348
167: SKP:       53248(     13 blks) ==>   109193200:53260
168: RAW:      167936(     41 blks) ==>   109193212:167948
169: SKP:       36864(      9 blks) ==>   109361160:36876
170: RAW:       24576(      6 blks) ==>   109361172:24588
171: SKP:       12288(      3 blks) ==>   109385760:12300
172: RAW:      237568(     58 blks) ==>   109385772:237580
173: SKP:        8192(      2 blks) ==>   109623352:8204
174: RAW:       24576(      6 blks) ==>   109623364:24588
175: SKP:        8192(      2 blks) ==>   109647952:8204
176: RAW:      237568(     58 blks) ==>   109647964:237580
177: SKP:       12288(      3 blks) ==>   109885544:12300
178: RAW:       20480(      5 blks) ==>   109885556:20492
179: SKP:       12288(      3 blks) ==>   109906048:12300
180: RAW:      237568(     58 blks) ==>   109906060:237580
181: SKP:        8192(      2 blks) ==>   110143640:8204
182: RAW:       24576(      6 blks) ==>   110143652:24588
183: SKP:       24576(      6 blks) ==>   110168240:24588
184: RAW:      258048(     63 blks) ==>   110168252:258060
185: SKP:        8192(      2 blks) ==>   110426312:8204
186: RAW:      270336(     66 blks) ==>   110426324:270348
187: SKP:       12288(      3 blks) ==>   110696672:12300
188: RAW:      237568(     58 blks) ==>   110696684:237580
189: SKP:        8192(      2 blks) ==>   110934264:8204
190: RAW:       24576(      6 blks) ==>   110934276:24588
191: SKP:        8192(      2 blks) ==>   110958864:8204
192: RAW:      270336(     66 blks) ==>   110958876:270348
193: SKP:       28672(      7 blks) ==>   111229224:28684
194: RAW:      204800(     50 blks) ==>   111229236:204812
195: SKP:       24576(      6 blks) ==>   111434048:24588
196: RAW:       24576(      6 blks) ==>   111434060:24588
197: SKP:       12288(      3 blks) ==>   111458648:12300
198: RAW:      233472(     57 blks) ==>   111458660:233484
199: SKP:       12288(      3 blks) ==>   111692144:12300
200: RAW:      303104(     74 blks) ==>   111692156:303116
201: SKP:       12288(      3 blks) ==>   111995272:12300
202: RAW:      221184(     54 blks) ==>   111995284:221196
203: SKP:       24576(      6 blks) ==>   112216480:24588
204: RAW:       24576(      6 blks) ==>   112216492:24588
205: SKP:       24576(      6 blks) ==>   112241080:24588
206: RAW:      208896(     51 blks) ==>   112241092:208908
207: SKP:       24576(      6 blks) ==>   112450000:24588
208: RAW:       20480(      5 blks) ==>   112450012:20492
209: SKP:       57344(     14 blks) ==>   112470504:57356
210: RAW:      147456(     36 blks) ==>   112470516:147468
211: SKP:       53248(     13 blks) ==>   112617984:53260
212: RAW:      274432(     67 blks) ==>   112617996:274444
213: SKP:        8192(      2 blks) ==>   112892440:8204
214: RAW:      303104(     74 blks) ==>   112892452:303116
215: SKP:       24576(      6 blks) ==>   113195568:24588
216: RAW:      208896(     51 blks) ==>   113195580:208908
217: SKP:       24576(      6 blks) ==>   113404488:24588
218: RAW:      307200(     75 blks) ==>   113404500:307212
219: SKP:       24576(      6 blks) ==>   113711712:24588
220: RAW:      221184(     54 blks) ==>   113711724:221196
221: SKP:       12288(      3 blks) ==>   113932920:12300
222: RAW:      303104(     74 blks) ==>   113932932:303116
223: SKP:        8192(      2 blks) ==>   114236048:8204
224: RAW:      225280(     55 blks) ==>   114236060:225292
225: SKP:       24576(      6 blks) ==>   114461352:24588
226: RAW:       20480(      5 blks) ==>   114461364:20492
227: SKP:       28672(      7 blks) ==>   114481856:28684
228: RAW:      192512(     47 blks) ==>   114481868:192524
229: SKP:       36864(      9 blks) ==>   114674392:36876
230: RAW:       24576(      6 blks) ==>   114674404:24588
231: SKP:       24576(      6 blks) ==>   114698992:24588
232: RAW:      208896(     51 blks) ==>   114699004:208908
233: SKP:       24576(      6 blks) ==>   114907912:24588
234: RAW:      303104(     74 blks) ==>   114907924:303116
235: SKP:       12288(      3 blks) ==>   115211040:12300
236: RAW:      237568(     58 blks) ==>   115211052:237580
237: SKP:        8192(      2 blks) ==>   115448632:8204
238: RAW:       24576(      6 blks) ==>   115448644:24588
239: SKP:        8192(      2 blks) ==>   115473232:8204
240: RAW:      237568(     58 blks) ==>   115473244:237580
241: SKP:       12288(      3 blks) ==>   115710824:12300
242: RAW:       24576(      6 blks) ==>   115710836:24588
243: SKP:        8192(      2 blks) ==>   115735424:8204
244: RAW:      237568(     58 blks) ==>   115735436:237580
245: SKP:       12288(      3 blks) ==>   115973016:12300
246: RAW:       20480(      5 blks) ==>   115973028:20492
247: SKP:       53248(     13 blks) ==>   115993520:53260
248: RAW:      151552(     37 blks) ==>   115993532:151564
249: SKP:       53248(     13 blks) ==>   116145096:53260
250: RAW:      413696(    101 blks) ==>   116145108:413708
251: SKP:       12288(      3 blks) ==>   116558816:12300
252: RAW:     1114112(    272 blks) ==>   116558828:1114124
253: SKP:        8192(      2 blks) ==>   117672952:8204
254: RAW:      237568(     58 blks) ==>   117672964:237580
255: SKP:       12288(      3 blks) ==>   117910544:12300
256: RAW:       24576(      6 blks) ==>   117910556:24588
257: SKP:        8192(      2 blks) ==>   117935144:8204
258: RAW:      237568(     58 blks) ==>   117935156:237580
259: SKP:       12288(      3 blks) ==>   118172736:12300
260: RAW:       20480(      5 blks) ==>   118172748:20492
261: SKP:       12288(      3 blks) ==>   118193240:12300
262: RAW:      237568(     58 blks) ==>   118193252:237580
263: SKP:        8192(      2 blks) ==>   118430832:8204
264: RAW:       24576(      6 blks) ==>   118430844:24588
265: SKP:       24576(      6 blks) ==>   118455432:24588
266: RAW:      208896(     51 blks) ==>   118455444:208908
267: SKP:       24576(      6 blks) ==>   118664352:24588
268: RAW:       20480(      5 blks) ==>   118664364:20492
269: SKP:       24576(      6 blks) ==>   118684856:24588
270: RAW:      258048(     63 blks) ==>   118684868:258060
271: SKP:       12288(      3 blks) ==>   118942928:12300
272: RAW:      270336(     66 blks) ==>   118942940:270348
273: SKP:       28672(      7 blks) ==>   119213288:28684
274: RAW:      499712(    122 blks) ==>   119213300:499724
275: SKP:        8192(      2 blks) ==>   119713024:8204
276: RAW:      303104(     74 blks) ==>   119713036:303116
277: SKP:       28672(      7 blks) ==>   120016152:28684
278: RAW:      204800(     50 blks) ==>   120016164:204812
279: SKP:       24576(      6 blks) ==>   120220976:24588
280: RAW:      307200(     75 blks) ==>   120220988:307212
281: SKP:       36864(      9 blks) ==>   120528200:36876
282: RAW:      180224(     44 blks) ==>   120528212:180236
283: SKP:       40960(     10 blks) ==>   120708448:40972
284: RAW:       20480(      5 blks) ==>   120708460:20492
285: SKP:       12288(      3 blks) ==>   120728952:12300
286: RAW:      270336(     66 blks) ==>   120728964:270348
287: SKP:       53248(     13 blks) ==>   120999312:53260
288: RAW:      151552(     37 blks) ==>   120999324:151564
289: SKP:       53248(     13 blks) ==>   121150888:53260
290: RAW:       24576(      6 blks) ==>   121150900:24588
291: SKP:       36864(      9 blks) ==>   121175488:36876
292: RAW:      180224(     44 blks) ==>   121175500:180236
293: SKP:       40960(     10 blks) ==>   121355736:40972
294: RAW:       20480(      5 blks) ==>   121355748:20492
295: SKP:        8192(      2 blks) ==>   121376240:8204
296: RAW:      229376(     56 blks) ==>   121376252:229388
297: SKP:       20480(      5 blks) ==>   121605640:20492
298: RAW:      270336(     66 blks) ==>   121605652:270348
299: SKP:       12288(      3 blks) ==>   121876000:12300
300: RAW:      270336(     66 blks) ==>   121876012:270348
301: SKP:        8192(      2 blks) ==>   122146360:8204
302: RAW:       24576(      6 blks) ==>   122146372:24588
303: SKP:       12288(      3 blks) ==>   122170960:12300
304: RAW:      233472(     57 blks) ==>   122170972:233484
305: SKP:       12288(      3 blks) ==>   122404456:12300
306: RAW:       32768(      8 blks) ==>   122404468:32780
307: SKP:       24576(      6 blks) ==>   122437248:24588
308: RAW:      225280(     55 blks) ==>   122437260:225292
309: SKP:        8192(      2 blks) ==>   122662552:8204
310: RAW:      552960(    135 blks) ==>   122662564:552972
311: SKP:        8192(      2 blks) ==>   123215536:8204
312: RAW:      552960(    135 blks) ==>   123215548:552972
313: SKP:        8192(      2 blks) ==>   123768520:8204
314: RAW:      585728(    143 blks) ==>   123768532:585740
315: SKP:       12288(      3 blks) ==>   124354272:12300
316: RAW:      237568(     58 blks) ==>   124354284:237580
317: SKP:        8192(      2 blks) ==>   124591864:8204
318: RAW:      585728(    143 blks) ==>   124591876:585740
319: SKP:       24576(      6 blks) ==>   125177616:24588
320: RAW:      208896(     51 blks) ==>   125177628:208908
321: SKP:       24576(      6 blks) ==>   125386536:24588
322: RAW:      303104(     74 blks) ==>   125386548:303116
323: SKP:       12288(      3 blks) ==>   125689664:12300
324: RAW:      237568(     58 blks) ==>   125689676:237580
325: SKP:        8192(      2 blks) ==>   125927256:8204
326: RAW:       24576(      6 blks) ==>   125927268:24588
327: SKP:        8192(      2 blks) ==>   125951856:8204
328: RAW:      241664(     59 blks) ==>   125951868:241676
329: SKP:        8192(      2 blks) ==>   126193544:8204
330: RAW:       24576(      6 blks) ==>   126193556:24588
331: SKP:       36864(      9 blks) ==>   126218144:36876
332: RAW:      180224(     44 blks) ==>   126218156:180236
333: SKP:       40960(     10 blks) ==>   126398392:40972
334: RAW:      303104(     74 blks) ==>   126398404:303116
335: SKP:       24576(      6 blks) ==>   126701520:24588
336: RAW:      221184(     54 blks) ==>   126701532:221196
337: SKP:       12288(      3 blks) ==>   126922728:12300
338: RAW:       20480(      5 blks) ==>   126922740:20492
339: SKP:       24576(      6 blks) ==>   126943232:24588
340: RAW:      196608(     48 blks) ==>   126943244:196620
341: SKP:       36864(      9 blks) ==>   127139864:36876
342: RAW:      270336(     66 blks) ==>   127139876:270348
343: SKP:       12288(      3 blks) ==>   127410224:12300
344: RAW:      585728(    143 blks) ==>   127410236:585740
345: SKP:        8192(      2 blks) ==>   127995976:8204
346: RAW:      237568(     58 blks) ==>   127995988:237580
347: SKP:       12288(      3 blks) ==>   128233568:12300
348: RAW:       20480(      5 blks) ==>   128233580:20492
349: SKP:       40960(     10 blks) ==>   128254072:40972
350: RAW:      192512(     47 blks) ==>   128254084:192524
351: SKP:       24576(      6 blks) ==>   128446608:24588
352: RAW:       24576(      6 blks) ==>   128446620:24588
353: SKP:       40960(     10 blks) ==>   128471208:40972
354: RAW:      180224(     44 blks) ==>   128471220:180236
355: SKP:       36864(      9 blks) ==>   128651456:36876
356: RAW:       24576(      6 blks) ==>   128651468:24588
357: SKP:        8192(      2 blks) ==>   128676056:8204
358: RAW:      270336(     66 blks) ==>   128676068:270348
359: SKP:       12288(      3 blks) ==>   128946416:12300
360: RAW:      561152(    137 blks) ==>   128946428:561164
361: SKP:        8192(      2 blks) ==>   129507592:8204
362: RAW:      282624(     69 blks) ==>   129507604:282636
363: SKP:        8192(      2 blks) ==>   129790240:8204
364: RAW:      237568(     58 blks) ==>   129790252:237580
365: SKP:       12288(      3 blks) ==>   130027832:12300
366: RAW:       20480(      5 blks) ==>   130027844:20492
367: SKP:       12288(      3 blks) ==>   130048336:12300
368: RAW:      237568(     58 blks) ==>   130048348:237580
369: SKP:        8192(      2 blks) ==>   130285928:8204
370: RAW:       24576(      6 blks) ==>   130285940:24588
371: SKP:       53248(     13 blks) ==>   130310528:53260
372: RAW:      151552(     37 blks) ==>   130310540:151564
373: SKP:       53248(     13 blks) ==>   130462104:53260
374: RAW:       32768(      8 blks) ==>   130462116:32780
375: SKP:        8192(      2 blks) ==>   130494896:8204
376: RAW:      237568(     58 blks) ==>   130494908:237580
377: SKP:       12288(      3 blks) ==>   130732488:12300
378: RAW:     1114112(    272 blks) ==>   130732500:1114124
379: SKP:        8192(      2 blks) ==>   131846624:8204
380: RAW:      270336(     66 blks) ==>   131846636:270348
381: SKP:       12288(      3 blks) ==>   132116984:12300
382: RAW:       32768(      8 blks) ==>   132116996:32780
383: SKP:        8192(      2 blks) ==>   132149776:8204
384: RAW:      237568(     58 blks) ==>   132149788:237580
385: SKP:       12288(      3 blks) ==>   132387368:12300
386: RAW:      303104(     74 blks) ==>   132387380:303116
387: SKP:       24576(      6 blks) ==>   132690496:24588
388: RAW:      208896(     51 blks) ==>   132690508:208908
389: SKP:       24576(      6 blks) ==>   132899416:24588
390: RAW:      303104(     74 blks) ==>   132899428:303116
391: SKP:       12288(      3 blks) ==>   133202544:12300
392: RAW:      237568(     58 blks) ==>   133202556:237580
393: SKP:        8192(      2 blks) ==>   133440136:8204
394: RAW:       24576(      6 blks) ==>   133440148:24588
395: SKP:        8192(      2 blks) ==>   133464736:8204
396: RAW:      237568(     58 blks) ==>   133464748:237580
397: SKP:       12288(      3 blks) ==>   133702328:12300
398: RAW:       20480(      5 blks) ==>   133702340:20492
399: SKP:       40960(     10 blks) ==>   133722832:40972
400: RAW:      163840(     40 blks) ==>   133722844:163852
401: SKP:       53248(     13 blks) ==>   133886696:53260
402: RAW:       24576(      6 blks) ==>   133886708:24588
403: SKP:       12288(      3 blks) ==>   133911296:12300
404: RAW:      270336(     66 blks) ==>   133911308:270348
405: SKP:       24576(      6 blks) ==>   134181656:24588
406: RAW:      208896(     51 blks) ==>   134181668:208908
407: SKP:       24576(      6 blks) ==>   134390576:24588
408: RAW:       20480(      5 blks) ==>   134390588:20492
409: SKP:       40960(     10 blks) ==>   134411080:40972
410: RAW:      180224(     44 blks) ==>   134411092:180236
411: SKP:       36864(      9 blks) ==>   134591328:36876
412: RAW:       24576(      6 blks) ==>   134591340:24588
413: SKP:       24576(      6 blks) ==>   134615928:24588
414: RAW:      192512(     47 blks) ==>   134615940:192524
415: SKP:       40960(     10 blks) ==>   134808464:40972
416: RAW:      270336(     66 blks) ==>   134808476:270348
417: SKP:       12288(      3 blks) ==>   135078824:12300
418: RAW:       20480(      5 blks) ==>   135078836:20492
419: SKP:        8192(      2 blks) ==>   135099328:8204
420: RAW:      241664(     59 blks) ==>   135099340:241676
421: SKP:        8192(      2 blks) ==>   135341016:8204
422: RAW:       24576(      6 blks) ==>   135341028:24588
423: SKP:       24576(      6 blks) ==>   135365616:24588
424: RAW:      208896(     51 blks) ==>   135365628:208908
425: SKP:       24576(      6 blks) ==>   135574536:24588
426: RAW:       20480(      5 blks) ==>   135574548:20492
427: SKP:       40960(     10 blks) ==>   135595040:40972
428: RAW:      180224(     44 blks) ==>   135595052:180236
429: SKP:       36864(      9 blks) ==>   135775288:36876
430: RAW:      270336(     66 blks) ==>   135775300:270348
431: SKP:       12288(      3 blks) ==>   136045648:12300
432: RAW:       24576(      6 blks) ==>   136045660:24588
433: SKP:        8192(      2 blks) ==>   136070248:8204
434: RAW:      270336(     66 blks) ==>   136070260:270348
435: SKP:       12288(      3 blks) ==>   136340608:12300
436: RAW:      548864(    134 blks) ==>   136340620:548876
437: SKP:       12288(      3 blks) ==>   136889496:12300
438: RAW:      270336(     66 blks) ==>   136889508:270348
439: SKP:       12288(      3 blks) ==>   137159856:12300
440: RAW:      233472(     57 blks) ==>   137159868:233484
441: SKP:       12288(      3 blks) ==>   137393352:12300
442: RAW:       24576(      6 blks) ==>   137393364:24588
443: SKP:        4096(      1 blks) ==>   137417952:4108
444: RAW:      229376(     56 blks) ==>   137417964:229388
445: SKP:       24576(      6 blks) ==>   137647352:24588
446: RAW:      548864(    134 blks) ==>   137647364:548876
447: SKP:       12288(      3 blks) ==>   138196240:12300
448: RAW:       24576(      6 blks) ==>   138196252:24588
449: SKP:       24576(      6 blks) ==>   138220840:24588
450: RAW:      221184(     54 blks) ==>   138220852:221196
451: SKP:       12288(      3 blks) ==>   138442048:12300
452: RAW:       20480(      5 blks) ==>   138442060:20492
453: SKP:       12288(      3 blks) ==>   138462552:12300
454: RAW:      237568(     58 blks) ==>   138462564:237580
455: SKP:        8192(      2 blks) ==>   138700144:8204
456: RAW:      303104(     74 blks) ==>   138700156:303116
457: SKP:       28672(      7 blks) ==>   139003272:28684
458: RAW:      208896(     51 blks) ==>   139003284:208908
459: SKP:       20480(      5 blks) ==>   139212192:20492
460: RAW:       24576(      6 blks) ==>   139212204:24588
461: SKP:       53248(     13 blks) ==>   139236792:53260
462: RAW:      151552(     37 blks) ==>   139236804:151564
463: SKP:       53248(     13 blks) ==>   139388368:53260
464: RAW:       24576(      6 blks) ==>   139388380:24588
465: SKP:       36864(      9 blks) ==>   139412968:36876
466: RAW:      196608(     48 blks) ==>   139412980:196620
467: SKP:       24576(      6 blks) ==>   139609600:24588
468: RAW:       20480(      5 blks) ==>   139609612:20492
469: SKP:       12288(      3 blks) ==>   139630104:12300
470: RAW:      278528(     68 blks) ==>   139630116:278540
471: SKP:       24576(      6 blks) ==>   139908656:24588
472: RAW:      208896(     51 blks) ==>   139908668:208908
473: SKP:       24576(      6 blks) ==>   140117576:24588
474: RAW:      303104(     74 blks) ==>   140117588:303116
475: SKP:       12288(      3 blks) ==>   140420704:12300
476: RAW:      237568(     58 blks) ==>   140420716:237580
477: SKP:        8192(      2 blks) ==>   140658296:8204
478: RAW:       24576(      6 blks) ==>   140658308:24588
479: SKP:       12288(      3 blks) ==>   140682896:12300
480: RAW:      233472(     57 blks) ==>   140682908:233484
481: SKP:       12288(      3 blks) ==>   140916392:12300
482: RAW:       24576(      6 blks) ==>   140916404:24588
483: SKP:        8192(      2 blks) ==>   140940992:8204
484: RAW:      790528(    193 blks) ==>   140941004:790540
485: SKP:       12288(      3 blks) ==>   141731544:12300
486: RAW:      249856(     61 blks) ==>   141731556:249868
487: SKP:       36864(      9 blks) ==>   141981424:36876
488: RAW:       24576(      6 blks) ==>   141981436:24588
489: SKP:       53248(     13 blks) ==>   142006024:53260
490: RAW:      151552(     37 blks) ==>   142006036:151564
491: SKP:       53248(     13 blks) ==>   142157600:53260
492: RAW:      303104(     74 blks) ==>   142157612:303116
493: SKP:       12288(      3 blks) ==>   142460728:12300
494: RAW:      237568(     58 blks) ==>   142460740:237580
495: SKP:        8192(      2 blks) ==>   142698320:8204
496: RAW:       24576(      6 blks) ==>   142698332:24588
497: SKP:       53248(     13 blks) ==>   142722920:53260
498: RAW:      135168(     33 blks) ==>   142722932:135180
499: SKP:       69632(     17 blks) ==>   142858112:69644
500: RAW:       20480(      5 blks) ==>   142858124:20492
501: SKP:       40960(     10 blks) ==>   142878616:40972
502: RAW:      180224(     44 blks) ==>   142878628:180236
503: SKP:       36864(      9 blks) ==>   143058864:36876
504: RAW:       24576(      6 blks) ==>   143058876:24588
505: SKP:       53248(     13 blks) ==>   143083464:53260
506: RAW:      151552(     37 blks) ==>   143083476:151564
507: SKP:       53248(     13 blks) ==>   143235040:53260
508: RAW:      585728(    143 blks) ==>   143235052:585740
509: SKP:        8192(      2 blks) ==>   143820792:8204
510: RAW:      552960(    135 blks) ==>   143820804:552972
511: SKP:       12288(      3 blks) ==>   144373776:12300
512: RAW:      548864(    134 blks) ==>   144373788:548876
513: SKP:       24576(      6 blks) ==>   144922664:24588
514: RAW:      196608(     48 blks) ==>   144922676:196620
515: SKP:       36864(      9 blks) ==>   145119296:36876
516: RAW:      585728(    143 blks) ==>   145119308:585740
517: SKP:       69632(     17 blks) ==>   145705048:69644
518: RAW:      151552(     37 blks) ==>   145705060:151564
519: SKP:       36864(      9 blks) ==>   145856624:36876
520: RAW:       24576(      6 blks) ==>   145856636:24588
521: SKP:        8192(      2 blks) ==>   145881224:8204
522: RAW:      270336(     66 blks) ==>   145881236:270348
523: SKP:       57344(     14 blks) ==>   146151584:57356
524: RAW:      163840(     40 blks) ==>   146151596:163852
525: SKP:       36864(      9 blks) ==>   146315448:36876
526: RAW:       24576(      6 blks) ==>   146315460:24588
527: SKP:       12288(      3 blks) ==>   146340048:12300
528: RAW:      548864(    134 blks) ==>   146340060:548876
529: SKP:       12288(      3 blks) ==>   146888936:12300
530: RAW:      237568(     58 blks) ==>   146888948:237580
531: SKP:        8192(      2 blks) ==>   147126528:8204
532: RAW:      585728(    143 blks) ==>   147126540:585740
533: SKP:       24576(      6 blks) ==>   147712280:24588
534: RAW:      208896(     51 blks) ==>   147712292:208908
535: SKP:       24576(      6 blks) ==>   147921200:24588
536: RAW:      303104(     74 blks) ==>   147921212:303116
537: SKP:       12288(      3 blks) ==>   148224328:12300
538: RAW:      221184(     54 blks) ==>   148224340:221196
539: SKP:       24576(      6 blks) ==>   148445536:24588
540: RAW:       24576(      6 blks) ==>   148445548:24588
541: SKP:       12288(      3 blks) ==>   148470136:12300
542: RAW:      233472(     57 blks) ==>   148470148:233484
543: SKP:       12288(      3 blks) ==>   148703632:12300
544: RAW:      303104(     74 blks) ==>   148703644:303116
545: SKP:       53248(     13 blks) ==>   149006760:53260
546: RAW:      151552(     37 blks) ==>   149006772:151564
547: SKP:       53248(     13 blks) ==>   149158336:53260
548: RAW:       24576(      6 blks) ==>   149158348:24588
549: SKP:       24576(      6 blks) ==>   149182936:24588
550: RAW:      536576(    131 blks) ==>   149182948:536588
551: SKP:        4096(      1 blks) ==>   149719536:4108
552: RAW:      249856(     61 blks) ==>   149719548:249868
553: SKP:        4096(      1 blks) ==>   149969416:4108
554: RAW:      831488(    203 blks) ==>   149969428:831500
555: SKP:       12288(      3 blks) ==>   150800928:12300
556: RAW:       24576(      6 blks) ==>   150800940:24588
557: SKP:        8192(      2 blks) ==>   150825528:8204
558: RAW:      237568(     58 blks) ==>   150825540:237580
559: SKP:       12288(      3 blks) ==>   151063120:12300
560: RAW:       20480(      5 blks) ==>   151063132:20492
561: SKP:       12288(      3 blks) ==>   151083624:12300
562: RAW:      237568(     58 blks) ==>   151083636:237580
563: SKP:        8192(      2 blks) ==>   151321216:8204
564: RAW:       24576(      6 blks) ==>   151321228:24588
565: SKP:       24576(      6 blks) ==>   151345816:24588
566: RAW:      212992(     52 blks) ==>   151345828:213004
567: SKP:       20480(      5 blks) ==>   151558832:20492
568: RAW:      270336(     66 blks) ==>   151558844:270348
569: SKP:        8192(      2 blks) ==>   151829192:8204
570: RAW:      585728(    143 blks) ==>   151829204:585740
571: SKP:       12288(      3 blks) ==>   152414944:12300
572: RAW:      552960(    135 blks) ==>   152414956:552972
573: SKP:       36864(      9 blks) ==>   152967928:36876
574: RAW:      180224(     44 blks) ==>   152967940:180236
575: SKP:       40960(     10 blks) ==>   153148176:40972
576: RAW:       20480(      5 blks) ==>   153148188:20492
577: SKP:       12288(      3 blks) ==>   153168680:12300
578: RAW:      237568(     58 blks) ==>   153168692:237580
579: SKP:        8192(      2 blks) ==>   153406272:8204
580: RAW:       24576(      6 blks) ==>   153406284:24588
581: SKP:        8192(      2 blks) ==>   153430872:8204
582: RAW:      270336(     66 blks) ==>   153430884:270348
583: SKP:       28672(      7 blks) ==>   153701232:28684
584: RAW:      200704(     49 blks) ==>   153701244:200716
585: SKP:       28672(      7 blks) ==>   153901960:28684
586: RAW:       24576(      6 blks) ==>   153901972:24588
587: SKP:       12288(      3 blks) ==>   153926560:12300
588: RAW:      270336(     66 blks) ==>   153926572:270348
589: SKP:        8192(      2 blks) ==>   154196920:8204
590: RAW:      241664(     59 blks) ==>   154196932:241676
591: SKP:        8192(      2 blks) ==>   154438608:8204
592: RAW:      303104(     74 blks) ==>   154438620:303116
593: SKP:        8192(      2 blks) ==>   154741736:8204
594: RAW:      237568(     58 blks) ==>   154741748:237580
595: SKP:       12288(      3 blks) ==>   154979328:12300
596: RAW:       24576(      6 blks) ==>   154979340:24588
597: SKP:        8192(      2 blks) ==>   155003928:8204
598: RAW:      237568(     58 blks) ==>   155003940:237580
599: SKP:       12288(      3 blks) ==>   155241520:12300
600: RAW:       20480(      5 blks) ==>   155241532:20492
601: SKP:       12288(      3 blks) ==>   155262024:12300
602: RAW:      237568(     58 blks) ==>   155262036:237580
603: SKP:        8192(      2 blks) ==>   155499616:8204
604: RAW:      303104(     74 blks) ==>   155499628:303116
605: SKP:       12288(      3 blks) ==>   155802744:12300
606: RAW:      241664(     59 blks) ==>   155802756:241676
607: SKP:        4096(      1 blks) ==>   156044432:4108
608: RAW:       24576(      6 blks) ==>   156044444:24588
609: SKP:       12288(      3 blks) ==>   156069032:12300
610: RAW:      233472(     57 blks) ==>   156069044:233484
611: SKP:       12288(      3 blks) ==>   156302528:12300
612: RAW:       24576(      6 blks) ==>   156302540:24588
613: SKP:        8192(      2 blks) ==>   156327128:8204
614: RAW:      237568(     58 blks) ==>   156327140:237580
615: SKP:       12288(      3 blks) ==>   156564720:12300
616: RAW:      581632(    142 blks) ==>   156564732:581644
617: SKP:       28672(      7 blks) ==>   157146376:28684
618: RAW:      221184(     54 blks) ==>   157146388:221196
619: SKP:        8192(      2 blks) ==>   157367584:8204
620: RAW:       24576(      6 blks) ==>   157367596:24588
621: SKP:       12288(      3 blks) ==>   157392184:12300
622: RAW:      221184(     54 blks) ==>   157392196:221196
623: SKP:       24576(      6 blks) ==>   157613392:24588
624: RAW:       24576(      6 blks) ==>   157613404:24588
625: SKP:        8192(      2 blks) ==>   157637992:8204
626: RAW:      225280(     55 blks) ==>   157638004:225292
627: SKP:       24576(      6 blks) ==>   157863296:24588
628: RAW:      585728(    143 blks) ==>   157863308:585740
629: SKP:        8192(      2 blks) ==>   158449048:8204
630: RAW:      270336(     66 blks) ==>   158449060:270348
631: SKP:       40960(     10 blks) ==>   158719408:40972
632: RAW:      200704(     49 blks) ==>   158719420:200716
633: SKP:       16384(      4 blks) ==>   158920136:16396
634: RAW:       24576(      6 blks) ==>   158920148:24588
635: SKP:        8192(      2 blks) ==>   158944736:8204
636: RAW:      237568(     58 blks) ==>   158944748:237580
637: SKP:       12288(      3 blks) ==>   159182328:12300
638: RAW:      303104(     74 blks) ==>   159182340:303116
639: SKP:       24576(      6 blks) ==>   159485456:24588
640: RAW:      208896(     51 blks) ==>   159485468:208908
641: SKP:       24576(      6 blks) ==>   159694376:24588
642: RAW:      303104(     74 blks) ==>   159694388:303116
643: SKP:       69632(     17 blks) ==>   159997504:69644
644: RAW:      122880(     30 blks) ==>   159997516:122892
645: SKP:       65536(     16 blks) ==>   160120408:65548
646: RAW:       24576(      6 blks) ==>   160120420:24588
647: SKP:       36864(      9 blks) ==>   160145008:36876
648: RAW:      241664(     59 blks) ==>   160145020:241676
649: SKP:       12288(      3 blks) ==>   160386696:12300
650: RAW:      237568(     58 blks) ==>   160386708:237580
651: SKP:        8192(      2 blks) ==>   160624288:8204
652: RAW:      270336(     66 blks) ==>   160624300:270348
653: SKP:       12288(      3 blks) ==>   160894648:12300
654: RAW:       24576(      6 blks) ==>   160894660:24588
655: SKP:       36864(      9 blks) ==>   160919248:36876
656: RAW:      241664(     59 blks) ==>   160919260:241676
657: SKP:       12288(      3 blks) ==>   161160936:12300
658: RAW:      221184(     54 blks) ==>   161160948:221196
659: SKP:       24576(      6 blks) ==>   161382144:24588
660: RAW:       24576(      6 blks) ==>   161382156:24588
661: SKP:       40960(     10 blks) ==>   161406744:40972
662: RAW:      196608(     48 blks) ==>   161406756:196620
663: SKP:       20480(      5 blks) ==>   161603376:20492
664: RAW:       24576(      6 blks) ==>   161603388:24588
665: SKP:        8192(      2 blks) ==>   161627976:8204
666: RAW:      270336(     66 blks) ==>   161627988:270348
667: SKP:       12288(      3 blks) ==>   161898336:12300
668: RAW:     1392640(    340 blks) ==>   161898348:1392652
669: SKP:       24576(      6 blks) ==>   163291000:24588
670: RAW:      208896(     51 blks) ==>   163291012:208908
671: SKP:       24576(      6 blks) ==>   163499920:24588
672: RAW:      307200(     75 blks) ==>   163499932:307212
673: SKP:        8192(      2 blks) ==>   163807144:8204
674: RAW:      221184(     54 blks) ==>   163807156:221196
675: SKP:       28672(      7 blks) ==>   164028352:28684
676: RAW:      303104(     74 blks) ==>   164028364:303116
677: SKP:       65536(     16 blks) ==>   164331480:65548
678: RAW:      139264(     34 blks) ==>   164331492:139276
679: SKP:       53248(     13 blks) ==>   164470768:53260
680: RAW:       20480(      5 blks) ==>   164470780:20492
681: SKP:       12288(      3 blks) ==>   164491272:12300
682: RAW:      237568(     58 blks) ==>   164491284:237580
683: SKP:        8192(      2 blks) ==>   164728864:8204
684: RAW:      307200(     75 blks) ==>   164728876:307212
685: SKP:       53248(     13 blks) ==>   165036088:53260
686: RAW:      151552(     37 blks) ==>   165036100:151564
687: SKP:       53248(     13 blks) ==>   165187664:53260
688: RAW:      548864(    134 blks) ==>   165187676:548876
689: SKP:       12288(      3 blks) ==>   165736552:12300
690: RAW:       20480(      5 blks) ==>   165736564:20492
691: SKP:       12288(      3 blks) ==>   165757056:12300
692: RAW:      221184(     54 blks) ==>   165757068:221196
693: SKP:       24576(      6 blks) ==>   165978264:24588
694: RAW:      299008(     73 blks) ==>   165978276:299020
695: SKP:        8192(      2 blks) ==>   166277296:8204
696: RAW:      557056(    136 blks) ==>   166277308:557068
697: SKP:        8192(      2 blks) ==>   166834376:8204
698: RAW:      237568(     58 blks) ==>   166834388:237580
699: SKP:       12288(      3 blks) ==>   167071968:12300
700: RAW:      552960(    135 blks) ==>   167071980:552972
701: SKP:        8192(      2 blks) ==>   167624952:8204
702: RAW:       24576(      6 blks) ==>   167624964:24588
703: SKP:       24576(      6 blks) ==>   167649552:24588
704: RAW:      208896(     51 blks) ==>   167649564:208908
705: SKP:       24576(      6 blks) ==>   167858472:24588
706: RAW:      270336(     66 blks) ==>   167858484:270348
707: SKP:        8192(      2 blks) ==>   168128832:8204
708: RAW:       24576(      6 blks) ==>   168128844:24588
709: SKP:       12288(      3 blks) ==>   168153432:12300
710: RAW:      233472(     57 blks) ==>   168153444:233484
711: SKP:       12288(      3 blks) ==>   168386928:12300
712: RAW:       24576(      6 blks) ==>   168386940:24588
713: SKP:       24576(      6 blks) ==>   168411528:24588
714: RAW:      192512(     47 blks) ==>   168411540:192524
715: SKP:       40960(     10 blks) ==>   168604064:40972
716: RAW:       20480(      5 blks) ==>   168604076:20492
717: SKP:       12288(      3 blks) ==>   168624568:12300
718: RAW:      237568(     58 blks) ==>   168624580:237580
719: SKP:        8192(      2 blks) ==>   168862160:8204
720: RAW:       24576(      6 blks) ==>   168862172:24588
721: SKP:        8192(      2 blks) ==>   168886760:8204
722: RAW:      237568(     58 blks) ==>   168886772:237580
723: SKP:       12288(      3 blks) ==>   169124352:12300
724: RAW:       20480(      5 blks) ==>   169124364:20492
725: SKP:       40960(     10 blks) ==>   169144856:40972
726: RAW:      180224(     44 blks) ==>   169144868:180236
727: SKP:       36864(      9 blks) ==>   169325104:36876
728: RAW:       24576(      6 blks) ==>   169325116:24588
729: SKP:       24576(      6 blks) ==>   169349704:24588
730: RAW:      208896(     51 blks) ==>   169349716:208908
731: SKP:       24576(      6 blks) ==>   169558624:24588
732: RAW:       32768(      8 blks) ==>   169558636:32780
733: SKP:       40960(     10 blks) ==>   169591416:40972
734: RAW:      208896(     51 blks) ==>   169591428:208908
735: SKP:        8192(      2 blks) ==>   169800336:8204
736: RAW:      303104(     74 blks) ==>   169800348:303116
737: SKP:       53248(     13 blks) ==>   170103464:53260
738: RAW:      151552(     37 blks) ==>   170103476:151564
739: SKP:       53248(     13 blks) ==>   170255040:53260
740: RAW:       24576(      6 blks) ==>   170255052:24588
741: SKP:       24576(      6 blks) ==>   170279640:24588
742: RAW:      192512(     47 blks) ==>   170279652:192524
743: SKP:       40960(     10 blks) ==>   170472176:40972
744: RAW:       20480(      5 blks) ==>   170472188:20492
745: SKP:       28672(      7 blks) ==>   170492680:28684
746: RAW:      212992(     52 blks) ==>   170492692:213004
747: SKP:       16384(      4 blks) ==>   170705696:16396
748: RAW:      585728(    143 blks) ==>   170705708:585740
749: SKP:       12288(      3 blks) ==>   171291448:12300
750: RAW:      237568(     58 blks) ==>   171291460:237580
751: SKP:        8192(      2 blks) ==>   171529040:8204
752: RAW:       24576(      6 blks) ==>   171529052:24588
753: SKP:        8192(      2 blks) ==>   171553640:8204
754: RAW:      241664(     59 blks) ==>   171553652:241676
755: SKP:        8192(      2 blks) ==>   171795328:8204
756: RAW:      270336(     66 blks) ==>   171795340:270348
757: SKP:       12288(      3 blks) ==>   172065688:12300
758: RAW:       20480(      5 blks) ==>   172065700:20492
759: SKP:       12288(      3 blks) ==>   172086192:12300
760: RAW:      237568(     58 blks) ==>   172086204:237580
761: SKP:        8192(      2 blks) ==>   172323784:8204
762: RAW:       24576(      6 blks) ==>   172323796:24588
763: SKP:        8192(      2 blks) ==>   172348384:8204
764: RAW:      237568(     58 blks) ==>   172348396:237580
765: SKP:       12288(      3 blks) ==>   172585976:12300
766: RAW:       20480(      5 blks) ==>   172585988:20492
767: SKP:       24576(      6 blks) ==>   172606480:24588
768: RAW:      258048(     63 blks) ==>   172606492:258060
769: SKP:       12288(      3 blks) ==>   172864552:12300
770: RAW:      233472(     57 blks) ==>   172864564:233484
771: SKP:       12288(      3 blks) ==>   173098048:12300
772: RAW:      303104(     74 blks) ==>   173098060:303116
773: SKP:       12288(      3 blks) ==>   173401176:12300
774: RAW:      221184(     54 blks) ==>   173401188:221196
775: SKP:       24576(      6 blks) ==>   173622384:24588
776: RAW:     1146880(    280 blks) ==>   173622396:1146892
777: SKP:       12288(      3 blks) ==>   174769288:12300
778: RAW:      237568(     58 blks) ==>   174769300:237580
779: SKP:        8192(      2 blks) ==>   175006880:8204
780: RAW:      307200(     75 blks) ==>   175006892:307212
781: SKP:        8192(      2 blks) ==>   175314104:8204
782: RAW:      237568(     58 blks) ==>   175314116:237580
783: SKP:       12288(      3 blks) ==>   175551696:12300
784: RAW:       20480(      5 blks) ==>   175551708:20492
785: SKP:       12288(      3 blks) ==>   175572200:12300
786: RAW:      278528(     68 blks) ==>   175572212:278540
787: SKP:       12288(      3 blks) ==>   175850752:12300
788: RAW:      233472(     57 blks) ==>   175850764:233484
789: SKP:       12288(      3 blks) ==>   176084248:12300
790: RAW:       24576(      6 blks) ==>   176084260:24588
791: SKP:        8192(      2 blks) ==>   176108848:8204
792: RAW:      270336(     66 blks) ==>   176108860:270348
793: SKP:       12288(      3 blks) ==>   176379208:12300
794: RAW:      237568(     58 blks) ==>   176379220:237580
795: SKP:        8192(      2 blks) ==>   176616800:8204
796: RAW:       24576(      6 blks) ==>   176616812:24588
797: SKP:       12288(      3 blks) ==>   176641400:12300
798: RAW:      233472(     57 blks) ==>   176641412:233484
799: SKP:       12288(      3 blks) ==>   176874896:12300
800: RAW:      270336(     66 blks) ==>   176874908:270348
801: SKP:       12288(      3 blks) ==>   177145256:12300
802: RAW:       20480(      5 blks) ==>   177145268:20492
803: SKP:       12288(      3 blks) ==>   177165760:12300
804: RAW:      270336(     66 blks) ==>   177165772:270348
805: SKP:        8192(      2 blks) ==>   177436120:8204
806: RAW:      835584(    204 blks) ==>   177436132:835596
807: SKP:        8192(      2 blks) ==>   178271728:8204
808: RAW:      225280(     55 blks) ==>   178271740:225292
809: SKP:       24576(      6 blks) ==>   178497032:24588
810: RAW:       20480(      5 blks) ==>   178497044:20492
811: SKP:       40960(     10 blks) ==>   178517536:40972
812: RAW:      106496(     26 blks) ==>   178517548:106508
813: SKP:        8192(      2 blks) ==>   178624056:8204
814: RAW:       98304(     24 blks) ==>   178624068:98316
815: SKP:        4096(      1 blks) ==>   178722384:4108
816: RAW:      303104(     74 blks) ==>   178722396:303116
817: SKP:       40960(     10 blks) ==>   179025512:40972
818: RAW:      180224(     44 blks) ==>   179025524:180236
819: SKP:       36864(      9 blks) ==>   179205760:36876
820: RAW:      307200(     75 blks) ==>   179205772:307212
821: SKP:       36864(      9 blks) ==>   179512984:36876
822: RAW:      180224(     44 blks) ==>   179512996:180236
823: SKP:       40960(     10 blks) ==>   179693232:40972
824: RAW:       20480(      5 blks) ==>   179693244:20492
825: SKP:       98304(     24 blks) ==>   179713736:98316
826: RAW:       65536(     16 blks) ==>   179713748:65548
827: SKP:       94208(     23 blks) ==>   179779296:94220
828: RAW:      585728(    143 blks) ==>   179779308:585740
829: SKP:       24576(      6 blks) ==>   180365048:24588
830: RAW:      208896(     51 blks) ==>   180365060:208908
831: SKP:       24576(      6 blks) ==>   180573968:24588
832: RAW:       24576(      6 blks) ==>   180573980:24588
833: SKP:       24576(      6 blks) ==>   180598568:24588
834: RAW:      221184(     54 blks) ==>   180598580:221196
835: SKP:       12288(      3 blks) ==>   180819776:12300
836: RAW:      864256(    211 blks) ==>   180819788:864268
837: SKP:       12288(      3 blks) ==>   181684056:12300
838: RAW:      270336(     66 blks) ==>   181684068:270348
839: SKP:        8192(      2 blks) ==>   181954416:8204
840: RAW:      237568(     58 blks) ==>   181954428:237580
841: SKP:       12288(      3 blks) ==>   182192008:12300
842: RAW:      270336(     66 blks) ==>   182192020:270348
843: SKP:       12288(      3 blks) ==>   182462368:12300
844: RAW:      303104(     74 blks) ==>   182462380:303116
845: SKP:        8192(      2 blks) ==>   182765496:8204
846: RAW:      237568(     58 blks) ==>   182765508:237580
847: SKP:       12288(      3 blks) ==>   183003088:12300
848: RAW:       20480(      5 blks) ==>   183003100:20492
849: SKP:       12288(      3 blks) ==>   183023592:12300
850: RAW:      221184(     54 blks) ==>   183023604:221196
851: SKP:       24576(      6 blks) ==>   183244800:24588
852: RAW:       24576(      6 blks) ==>   183244812:24588
853: SKP:       53248(     13 blks) ==>   183269400:53260
854: RAW:      167936(     41 blks) ==>   183269412:167948
855: SKP:       36864(      9 blks) ==>   183437360:36876
856: RAW:       24576(      6 blks) ==>   183437372:24588
857: SKP:        8192(      2 blks) ==>   183461960:8204
858: RAW:      237568(     58 blks) ==>   183461972:237580
859: SKP:       12288(      3 blks) ==>   183699552:12300
860: RAW:      585728(    143 blks) ==>   183699564:585740
861: SKP:       20480(      5 blks) ==>   184285304:20492
862: RAW:      208896(     51 blks) ==>   184285316:208908
863: SKP:       28672(      7 blks) ==>   184494224:28684
864: RAW:       20480(      5 blks) ==>   184494236:20492
865: SKP:       53248(     13 blks) ==>   184514728:53260
866: RAW:      151552(     37 blks) ==>   184514740:151564
867: SKP:       53248(     13 blks) ==>   184666304:53260
868: RAW:       24576(      6 blks) ==>   184666316:24588
869: SKP:        8192(      2 blks) ==>   184690904:8204
870: RAW:      237568(     58 blks) ==>   184690916:237580
871: SKP:       12288(      3 blks) ==>   184928496:12300
872: RAW:      557056(    136 blks) ==>   184928508:557068
873: SKP:        4096(      1 blks) ==>   185485576:4108
874: RAW:      303104(     74 blks) ==>   185485588:303116
875: SKP:       24576(      6 blks) ==>   185788704:24588
876: RAW:      225280(     55 blks) ==>   185788716:225292
877: SKP:        8192(      2 blks) ==>   186014008:8204
878: RAW:     1150976(    281 blks) ==>   186014020:1150988
879: SKP:       12288(      3 blks) ==>   187165008:12300
880: RAW:      237568(     58 blks) ==>   187165020:237580
881: SKP:        8192(      2 blks) ==>   187402600:8204
882: RAW:      307200(     75 blks) ==>   187402612:307212
883: SKP:       36864(      9 blks) ==>   187709824:36876
884: RAW:      180224(     44 blks) ==>   187709836:180236
885: SKP:       40960(     10 blks) ==>   187890072:40972
886: RAW:       20480(      5 blks) ==>   187890084:20492
887: SKP:       12288(      3 blks) ==>   187910576:12300
888: RAW:      237568(     58 blks) ==>   187910588:237580
889: SKP:        8192(      2 blks) ==>   188148168:8204
890: RAW:      303104(     74 blks) ==>   188148180:303116
891: SKP:       40960(     10 blks) ==>   188451296:40972
892: RAW:      180224(     44 blks) ==>   188451308:180236
893: SKP:       36864(      9 blks) ==>   188631544:36876
894: RAW:       24576(      6 blks) ==>   188631556:24588
895: SKP:       24576(      6 blks) ==>   188656144:24588
896: RAW:      208896(     51 blks) ==>   188656156:208908
897: SKP:       24576(      6 blks) ==>   188865064:24588
898: RAW:       32768(      8 blks) ==>   188865076:32780
899: SKP:       12288(      3 blks) ==>   188897856:12300
900: RAW:      233472(     57 blks) ==>   188897868:233484
901: SKP:       12288(      3 blks) ==>   189131352:12300
902: RAW:      303104(     74 blks) ==>   189131364:303116
903: SKP:       12288(      3 blks) ==>   189434480:12300
904: RAW:      237568(     58 blks) ==>   189434492:237580
905: SKP:        8192(      2 blks) ==>   189672072:8204
906: RAW:      552960(    135 blks) ==>   189672084:552972
907: SKP:        8192(      2 blks) ==>   190225056:8204
908: RAW:       24576(      6 blks) ==>   190225068:24588
909: SKP:        4096(      1 blks) ==>   190249656:4108
910: RAW:      229376(     56 blks) ==>   190249668:229388
911: SKP:       24576(      6 blks) ==>   190479056:24588
912: RAW:      303104(     74 blks) ==>   190479068:303116
913: SKP:       12288(      3 blks) ==>   190782184:12300
914: RAW:      270336(     66 blks) ==>   190782196:270348
915: SKP:       36864(      9 blks) ==>   191052544:36876
916: RAW:      180224(     44 blks) ==>   191052556:180236
917: SKP:       40960(     10 blks) ==>   191232792:40972
918: RAW:      864256(    211 blks) ==>   191232804:864268
919: SKP:       12288(      3 blks) ==>   192097072:12300
920: RAW:      270336(     66 blks) ==>   192097084:270348
921: SKP:        8192(      2 blks) ==>   192367432:8204
922: RAW:      274432(     67 blks) ==>   192367444:274444
923: SKP:       36864(      9 blks) ==>   192641888:36876
924: RAW:      180224(     44 blks) ==>   192641900:180236
925: SKP:       40960(     10 blks) ==>   192822136:40972
926: RAW:       20480(      5 blks) ==>   192822148:20492
927: SKP:       69632(     17 blks) ==>   192842640:69644
928: RAW:      122880(     30 blks) ==>   192842652:122892
929: SKP:       65536(     16 blks) ==>   192965544:65548
930: RAW:      303104(     74 blks) ==>   192965556:303116
931: SKP:       12288(      3 blks) ==>   193268672:12300
932: RAW:      237568(     58 blks) ==>   193268684:237580
933: SKP:        8192(      2 blks) ==>   193506264:8204
934: RAW:       24576(      6 blks) ==>   193506276:24588
935: SKP:       12288(      3 blks) ==>   193530864:12300
936: RAW:      233472(     57 blks) ==>   193530876:233484
937: SKP:       12288(      3 blks) ==>   193764360:12300
938: RAW:      585728(    143 blks) ==>   193764372:585740
939: SKP:       24576(      6 blks) ==>   194350112:24588
940: RAW:      208896(     51 blks) ==>   194350124:208908
941: SKP:       24576(      6 blks) ==>   194559032:24588
942: RAW:       40960(     10 blks) ==>   194559044:40972
943: SKP:       12288(      3 blks) ==>   194600016:12300
944: RAW:      233472(     57 blks) ==>   194600028:233484
945: SKP:       12288(      3 blks) ==>   194833512:12300
946: RAW:       24576(      6 blks) ==>   194833524:24588
947: SKP:       36864(      9 blks) ==>   194858112:36876
948: RAW:      180224(     44 blks) ==>   194858124:180236
949: SKP:       40960(     10 blks) ==>   195038360:40972
950: RAW:       20480(      5 blks) ==>   195038372:20492
951: SKP:       24576(      6 blks) ==>   195058864:24588
952: RAW:      208896(     51 blks) ==>   195058876:208908
953: SKP:       24576(      6 blks) ==>   195267784:24588
954: RAW:       24576(      6 blks) ==>   195267796:24588
955: SKP:       24576(      6 blks) ==>   195292384:24588
956: RAW:      221184(     54 blks) ==>   195292396:221196
957: SKP:       12288(      3 blks) ==>   195513592:12300
958: RAW:       24576(      6 blks) ==>   195513604:24588
959: SKP:        8192(      2 blks) ==>   195538192:8204
960: RAW:      843776(    206 blks) ==>   195538204:843788
961: SKP:       24576(      6 blks) ==>   196381992:24588
962: RAW:      208896(     51 blks) ==>   196382004:208908
963: SKP:       24576(      6 blks) ==>   196590912:24588
964: RAW:       20480(      5 blks) ==>   196590924:20492
965: SKP:       12288(      3 blks) ==>   196611416:12300
966: RAW:      552960(    135 blks) ==>   196611428:552972
967: SKP:        8192(      2 blks) ==>   197164400:8204
968: RAW:      237568(     58 blks) ==>   197164412:237580
969: SKP:       12288(      3 blks) ==>   197401992:12300
970: RAW:       20480(      5 blks) ==>   197402004:20492
971: SKP:       53248(     13 blks) ==>   197422496:53260
972: RAW:      167936(     41 blks) ==>   197422508:167948
973: SKP:       36864(      9 blks) ==>   197590456:36876
974: RAW:       24576(      6 blks) ==>   197590468:24588
975: SKP:        8192(      2 blks) ==>   197615056:8204
976: RAW:      270336(     66 blks) ==>   197615068:270348
977: SKP:       12288(      3 blks) ==>   197885416:12300
978: RAW:     1081344(    264 blks) ==>   197885428:1081356
979: SKP:        8192(      2 blks) ==>   198966784:8204
980: RAW:       24576(      6 blks) ==>   198966796:24588
981: SKP:       24576(      6 blks) ==>   198991384:24588
982: RAW:      192512(     47 blks) ==>   198991396:192524
983: SKP:       40960(     10 blks) ==>   199183920:40972
984: RAW:      831488(    203 blks) ==>   199183932:831500
985: SKP:       12288(      3 blks) ==>   200015432:12300
986: RAW:       20480(      5 blks) ==>   200015444:20492
987: SKP:       12288(      3 blks) ==>   200035936:12300
988: RAW:      221184(     54 blks) ==>   200035948:221196
989: SKP:       24576(      6 blks) ==>   200257144:24588
990: RAW:       24576(      6 blks) ==>   200257156:24588
991: SKP:       12288(      3 blks) ==>   200281744:12300
992: RAW:      221184(     54 blks) ==>   200281756:221196
993: SKP:       24576(      6 blks) ==>   200502952:24588
994: RAW:       24576(      6 blks) ==>   200502964:24588
995: SKP:        8192(      2 blks) ==>   200527552:8204
996: RAW:      237568(     58 blks) ==>   200527564:237580
997: SKP:       12288(      3 blks) ==>   200765144:12300
998: RAW:      303104(     74 blks) ==>   200765156:303116
999: SKP:        8192(      2 blks) ==>   201068272:8204
1000: RAW:      270336(     66 blks) ==>   201068284:270348
1001: SKP:       12288(      3 blks) ==>   201338632:12300
1002: RAW:      221184(     54 blks) ==>   201338644:221196
1003: SKP:       24576(      6 blks) ==>   201559840:24588
1004: RAW:       24576(      6 blks) ==>   201559852:24588
1005: SKP:       40960(     10 blks) ==>   201584440:40972
1006: RAW:      176128(     43 blks) ==>   201584452:176140
1007: SKP:       40960(     10 blks) ==>   201760592:40972
1008: RAW:      303104(     74 blks) ==>   201760604:303116
1009: SKP:       12288(      3 blks) ==>   202063720:12300
1010: RAW:      237568(     58 blks) ==>   202063732:237580
1011: SKP:        8192(      2 blks) ==>   202301312:8204
1012: RAW:       28672(      7 blks) ==>   202301324:28684
1013: SKP:        8192(      2 blks) ==>   202330008:8204
1014: RAW:      237568(     58 blks) ==>   202330020:237580
1015: SKP:       12288(      3 blks) ==>   202567600:12300
1016: RAW:      552960(    135 blks) ==>   202567612:552972
1017: SKP:        8192(      2 blks) ==>   203120584:8204
1018: RAW:    61861888(  15103 blks) ==>   203120596:61861900
1019: SKP:        4096(      1 blks) ==>   264982496:4108
1020: RAW:     2424832(    592 blks) ==>   264982508:2424844
1021: SKP:     4194304(   1024 blks) ==>   267407352:4194316
1022: RAW:     9793536(   2391 blks) ==>   267407364:9793548
1023: SKP:        4096(      1 blks) ==>   277200912:4108
1024: RAW:     9924608(   2423 blks) ==>   277200924:9924620
1025: SKP:      454656(    111 blks) ==>   287125544:454668
1026: RAW:       12288(      3 blks) ==>   287125556:12300
1027: SKP:      770048(    188 blks) ==>   287137856:770060
1028: RAW:     3330048(    813 blks) ==>   287137868:3330060
1029: SKP:       12288(      3 blks) ==>   290467928:12300
1030: RAW:        8192(      2 blks) ==>   290467940:8204
1031: SKP:       16384(      4 blks) ==>   290476144:16396
1032: RAW:      610304(    149 blks) ==>   290476156:610316
1033: SKP:        4096(      1 blks) ==>   291086472:4108
1034: RAW:        8192(      2 blks) ==>   291086484:8204
1035: SKP:        4096(      1 blks) ==>   291094688:4108
1036: RAW:        8192(      2 blks) ==>   291094700:8204
1037: SKP:        4096(      1 blks) ==>   291102904:4108
1038: RAW:      278528(     68 blks) ==>   291102916:278540
1039: SKP:        4096(      1 blks) ==>   291381456:4108
1040: RAW:        8192(      2 blks) ==>   291381468:8204
1041: SKP:        4096(      1 blks) ==>   291389672:4108
1042: RAW:      303104(     74 blks) ==>   291389684:303116
1043: SKP:        4096(      1 blks) ==>   291692800:4108
1044: RAW:       45056(     11 blks) ==>   291692812:45068
1045: SKP:        4096(      1 blks) ==>   291737880:4108
1046: RAW:       24576(      6 blks) ==>   291737892:24588
1047: SKP:        4096(      1 blks) ==>   291762480:4108
1048: RAW:       16384(      4 blks) ==>   291762492:16396
1049: SKP:        4096(      1 blks) ==>   291778888:4108
1050: RAW:       24576(      6 blks) ==>   291778900:24588
1051: SKP:        4096(      1 blks) ==>   291803488:4108
1052: RAW:       16384(      4 blks) ==>   291803500:16396
1053: SKP:        4096(      1 blks) ==>   291819896:4108
1054: RAW:       24576(      6 blks) ==>   291819908:24588
1055: SKP:        4096(      1 blks) ==>   291844496:4108
1056: RAW:       24576(      6 blks) ==>   291844508:24588
1057: SKP:        4096(      1 blks) ==>   291869096:4108
1058: RAW:       16384(      4 blks) ==>   291869108:16396
1059: SKP:        4096(      1 blks) ==>   291885504:4108
1060: RAW:       24576(      6 blks) ==>   291885516:24588
1061: SKP:        4096(      1 blks) ==>   291910104:4108
1062: RAW:       16384(      4 blks) ==>   291910116:16396
1063: SKP:        4096(      1 blks) ==>   291926512:4108
1064: RAW:       24576(      6 blks) ==>   291926524:24588
1065: SKP:        4096(      1 blks) ==>   291951112:4108
1066: RAW:       16384(      4 blks) ==>   291951124:16396
1067: SKP:        4096(      1 blks) ==>   291967520:4108
1068: RAW:       24576(      6 blks) ==>   291967532:24588
1069: SKP:        4096(      1 blks) ==>   291992120:4108
1070: RAW:       24576(      6 blks) ==>   291992132:24588
1071: SKP:        4096(      1 blks) ==>   292016720:4108
1072: RAW:       16384(      4 blks) ==>   292016732:16396
1073: SKP:        4096(      1 blks) ==>   292033128:4108
1074: RAW:       24576(      6 blks) ==>   292033140:24588
1075: SKP:        4096(      1 blks) ==>   292057728:4108
1076: RAW:       16384(      4 blks) ==>   292057740:16396
1077: SKP:        4096(      1 blks) ==>   292074136:4108
1078: RAW:       24576(      6 blks) ==>   292074148:24588
1079: SKP:        4096(      1 blks) ==>   292098736:4108
1080: RAW:       16384(      4 blks) ==>   292098748:16396
1081: SKP:        4096(      1 blks) ==>   292115144:4108
1082: RAW:      585728(    143 blks) ==>   292115156:585740
1083: SKP:     1568768(    383 blks) ==>   292700896:1568780
1084: RAW:       12288(      3 blks) ==>   292700908:12300
1085: SKP:     1114112(    272 blks) ==>   292713208:1114124
1086: RAW:    20840448(   5088 blks) ==>   292713220:20840460
1087: SKP:        8192(      2 blks) ==>   313553680:8204
1088: RAW:     2818048(    688 blks) ==>   313553692:2818060
1089: SKP:        4096(      1 blks) ==>   316371752:4108
1090: RAW:    10964992(   2677 blks) ==>   316371764:10965004
1091: SKP:        4096(      1 blks) ==>   327336768:4108
1092: RAW:     5107712(   1247 blks) ==>   327336780:5107724
1093: SKP:     2195456(    536 blks) ==>   332444504:2195468
1094: RAW:    40288256(   9836 blks) ==>   332444516:40288268
1095: SKP:     1654784(    404 blks) ==>   372732784:1654796
1096: RAW:    16797696(   4101 blks) ==>   372732796:16797708
1097: SKP:       49152(     12 blks) ==>   389530504:49164
1098: RAW:        4096(      1 blks) ==>   389530516:4108
1099: SKP:       61440(     15 blks) ==>   389534624:61452
1100: RAW:     4059136(    991 blks) ==>   389534636:4059148
1101: SKP:        4096(      1 blks) ==>   393593784:4108
1102: RAW:        8192(      2 blks) ==>   393593796:8204
1103: SKP:       49152(     12 blks) ==>   393602000:49164
1104: RAW:        4096(      1 blks) ==>   393602012:4108
1105: SKP:       61440(     15 blks) ==>   393606120:61452
1106: RAW:      970752(    237 blks) ==>   393606132:970764
1107: SKP:      118784(     29 blks) ==>   394576896:118796
1108: RAW:       24576(      6 blks) ==>   394576908:24588
1109: SKP:      176128(     43 blks) ==>   394601496:176140
1110: RAW:       16384(      4 blks) ==>   394601508:16396
1111: SKP:      167936(     41 blks) ==>   394617904:167948
1112: RAW:       16384(      4 blks) ==>   394617916:16396
1113: SKP:      163840(     40 blks) ==>   394634312:163852
1114: RAW:        8192(      2 blks) ==>   394634324:8204
1115: SKP:      155648(     38 blks) ==>   394642528:155660
1116: RAW:     1339392(    327 blks) ==>   394642540:1339404
1117: SKP:      909312(    222 blks) ==>   395981944:909324
1118: RAW:    30941184(   7554 blks) ==>   395981956:30941196
1119: SKP:       12288(      3 blks) ==>   426923152:12300
1120: RAW:     1830912(    447 blks) ==>   426923164:1830924
1121: SKP:      159744(     39 blks) ==>   428754088:159756
1122: RAW:       65536(     16 blks) ==>   428754100:65548
1123: SKP:       12288(      3 blks) ==>   428819648:12300
1124: RAW:       12288(      3 blks) ==>   428819660:12300
1125: SKP:       12288(      3 blks) ==>   428831960:12300
1126: RAW:       12288(      3 blks) ==>   428831972:12300
1127: SKP:       69632(     17 blks) ==>   428844272:69644
1128: RAW:       45056(     11 blks) ==>   428844284:45068
1129: SKP:        4096(      1 blks) ==>   428889352:4108
1130: RAW:       12288(      3 blks) ==>   428889364:12300
1131: SKP:       16384(      4 blks) ==>   428901664:16396
1132: RAW:        8192(      2 blks) ==>   428901676:8204
1133: SKP:       16384(      4 blks) ==>   428909880:16396
1134: RAW:        8192(      2 blks) ==>   428909892:8204
1135: SKP:       16384(      4 blks) ==>   428918096:16396
1136: RAW:        8192(      2 blks) ==>   428918108:8204
1137: SKP:       16384(      4 blks) ==>   428926312:16396
1138: RAW:        8192(      2 blks) ==>   428926324:8204
1139: SKP:       12288(      3 blks) ==>   428934528:12300
1140: RAW:       53248(     13 blks) ==>   428934540:53260
1141: SKP:        4096(      1 blks) ==>   428987800:4108
1142: RAW:       12288(      3 blks) ==>   428987812:12300
1143: SKP:      122880(     30 blks) ==>   429000112:122892
1144: RAW:       20480(      5 blks) ==>   429000124:20492
1145: SKP:       40960(     10 blks) ==>   429020616:40972
1146: RAW:    23298048(   5688 blks) ==>   429020628:23298060
1147: SKP:     1867776(    456 blks) ==>   452318688:1867788
1148: RAW:    48115712(  11747 blks) ==>   452318700:48115724
1149: SKP:        8192(      2 blks) ==>   500434424:8204
1150: RAW:      425984(    104 blks) ==>   500434436:425996
1151: SKP:        4096(      1 blks) ==>   500860432:4108
1152: RAW:    11530240(   2815 blks) ==>   500860444:11530252
1153: SKP:        4096(      1 blks) ==>   512390696:4108
1154: RAW:     1925120(    470 blks) ==>   512390708:1925132
1155: SKP:     5095424(   1244 blks) ==>   514315840:5095436
1156: RAW:       12288(      3 blks) ==>   514315852:12300
1157: SKP:     4194304(   1024 blks) ==>   514328152:4194316
1158: RAW:      446464(    109 blks) ==>   514328164:446476
1159: SKP:        8192(      2 blks) ==>   514774640:8204
1160: RAW:     7905280(   1930 blks) ==>   514774652:7905292
1161: SKP:     4210688(   1028 blks) ==>   522679944:4210700
1162: RAW:    14827520(   3620 blks) ==>   522679956:14827532
1163: SKP:        8192(      2 blks) ==>   537507488:8204
1164: RAW:     2609152(    637 blks) ==>   537507500:2609164
1165: SKP:        8192(      2 blks) ==>   540116664:8204
1166: RAW:     7491584(   1829 blks) ==>   540116676:7491596
1167: SKP:      221184(     54 blks) ==>   547608272:221196
1168: RAW:    16777216(   4096 blks) ==>   547608284:16777228
1169: SKP:   209715200(  51200 blks) ==>   564385512:209715212
1170: RAW:       12288(      3 blks) ==>   564385524:12300
1171: SKP:   268423168(  65533 blks) ==>   564397824:268423180
1172: RAW:       12288(      3 blks) ==>   564397836:12300
1173: SKP:   939511808( 229373 blks) ==>   564410136:939511820
1174: RAW:       16384(      4 blks) ==>   564410148:16396
1175: SKP:       49152(     12 blks) ==>   564426544:49164
1176: RAW:        8192(      2 blks) ==>   564426556:8204
1177: SKP:       57344(     14 blks) ==>   564434760:57356
1178: RAW:     4124672(   1007 blks) ==>   564434772:4124684
1179: SKP:    29429760(   7185 blks) ==>   568559456:29429772
1180: RAW:     7958528(   1943 blks) ==>   568559468:7958540
1181: SKP:    92573696(  22601 blks) ==>   576518008:92573708
1182: RAW:    37486592(   9152 blks) ==>   576518020:37486604
1183: SKP:       28672(      7 blks) ==>   614004624:28684
1184: RAW:     3403776(    831 blks) ==>   614004636:3403788
1185: SKP:        4096(      1 blks) ==>   617408424:4108
1186: RAW:     1060864(    259 blks) ==>   617408436:1060876
1187: SKP:        4096(      1 blks) ==>   618469312:4108
1188: RAW:    58560512(  14297 blks) ==>   618469324:58560524
1189: SKP:        8192(      2 blks) ==>   677029848:8204
1190: RAW:       73728(     18 blks) ==>   677029860:73740
1191: SKP:        8192(      2 blks) ==>   677103600:8204
1192: RAW:    56094720(  13695 blks) ==>   677103612:56094732
1193: SKP:        4096(      1 blks) ==>   733198344:4108
1194: RAW:    44711936(  10916 blks) ==>   733198356:44711948
1195: SKP:        4096(      1 blks) ==>   777910304:4108
1196: RAW:    66433024(  16219 blks) ==>   777910316:66433036
1197: SKP:        4096(      1 blks) ==>   844343352:4108
1198: RAW:      192512(     47 blks) ==>   844343364:192524
1199: SKP:        4096(      1 blks) ==>   844535888:4108
1200: RAW:       40960(     10 blks) ==>   844535900:40972
1201: SKP:        4096(      1 blks) ==>   844576872:4108
1202: RAW:       36864(      9 blks) ==>   844576884:36876
1203: SKP:        8192(      2 blks) ==>   844613760:8204
1204: RAW:       40960(     10 blks) ==>   844613772:40972
1205: SKP:        4096(      1 blks) ==>   844654744:4108
1206: RAW:       32768(      8 blks) ==>   844654756:32780
1207: SKP:        4096(      1 blks) ==>   844687536:4108
1208: RAW:       32768(      8 blks) ==>   844687548:32780
1209: SKP:        4096(      1 blks) ==>   844720328:4108
1210: RAW:       36864(      9 blks) ==>   844720340:36876
1211: SKP:        4096(      1 blks) ==>   844757216:4108
1212: RAW:       32768(      8 blks) ==>   844757228:32780
1213: SKP:        4096(      1 blks) ==>   844790008:4108
1214: RAW:      389120(     95 blks) ==>   844790020:389132
1215: SKP:        4096(      1 blks) ==>   845179152:4108
1216: RAW:       32768(      8 blks) ==>   845179164:32780
1217: SKP:        4096(      1 blks) ==>   845211944:4108
1218: RAW:      122880(     30 blks) ==>   845211956:122892
1219: SKP:        4096(      1 blks) ==>   845334848:4108
1220: RAW:       40960(     10 blks) ==>   845334860:40972
1221: SKP:        4096(      1 blks) ==>   845375832:4108
1222: RAW:       32768(      8 blks) ==>   845375844:32780
1223: SKP:        4096(      1 blks) ==>   845408624:4108
1224: RAW:       32768(      8 blks) ==>   845408636:32780
1225: SKP:        4096(      1 blks) ==>   845441416:4108
1226: RAW:       36864(      9 blks) ==>   845441428:36876
1227: SKP:        4096(      1 blks) ==>   845478304:4108
1228: RAW:       98304(     24 blks) ==>   845478316:98316
1229: SKP:        4096(      1 blks) ==>   845576632:4108
1230: RAW:       32768(      8 blks) ==>   845576644:32780
1231: SKP:        4096(      1 blks) ==>   845609424:4108
1232: RAW:       32768(      8 blks) ==>   845609436:32780
1233: SKP:        4096(      1 blks) ==>   845642216:4108
1234: RAW:       32768(      8 blks) ==>   845642228:32780
1235: SKP:        4096(      1 blks) ==>   845675008:4108
1236: RAW:       32768(      8 blks) ==>   845675020:32780
1237: SKP:        8192(      2 blks) ==>   845707800:8204
1238: RAW:       32768(      8 blks) ==>   845707812:32780
1239: SKP:        4096(      1 blks) ==>   845740592:4108
1240: RAW:      106496(     26 blks) ==>   845740604:106508
1241: SKP:        4096(      1 blks) ==>   845847112:4108
1242: RAW:      122880(     30 blks) ==>   845847124:122892
1243: SKP:        4096(      1 blks) ==>   845970016:4108
1244: RAW:     5152768(   1258 blks) ==>   845970028:5152780
1245: SKP:        4096(      1 blks) ==>   851122808:4108
1246: RAW:       98304(     24 blks) ==>   851122820:98316
1247: SKP:        8192(      2 blks) ==>   851221136:8204
1248: RAW:      413696(    101 blks) ==>   851221148:413708
1249: SKP:        4096(      1 blks) ==>   851634856:4108
1250: RAW:       28672(      7 blks) ==>   851634868:28684
1251: SKP:        4096(      1 blks) ==>   851663552:4108
1252: RAW:       28672(      7 blks) ==>   851663564:28684
1253: SKP:        4096(      1 blks) ==>   851692248:4108
1254: RAW:       98304(     24 blks) ==>   851692260:98316
1255: SKP:        4096(      1 blks) ==>   851790576:4108
1256: RAW:     2359296(    576 blks) ==>   851790588:2359308
1257: SKP:        4096(      1 blks) ==>   854149896:4108
1258: RAW:     6455296(   1576 blks) ==>   854149908:6455308
1259: SKP:   789454848( 192738 blks) ==>   860605216:789454860
1260: RAW:       12288(      3 blks) ==>   860605228:12300
1261: SKP:   268423168(  65533 blks) ==>   860617528:268423180
1262: RAW:       12288(      3 blks) ==>   860617540:12300
1263: SKP:   671076352( 163837 blks) ==>   860629840:671076364
1264: RAW:        8192(      2 blks) ==>   860629852:8204
1265: SKP:       16384(      4 blks) ==>   860638056:16396
1266: RAW:        4096(      1 blks) ==>   860638068:4108
1267: SKP:       36864(      9 blks) ==>   860642176:36876
1268: RAW:       24576(      6 blks) ==>   860642188:24588
1269: SKP:       40960(     10 blks) ==>   860666776:40972
1270: RAW:    11464704(   2799 blks) ==>   860666788:11464716
1271: SKP:    22089728(   5393 blks) ==>   872131504:22089740
1272: RAW:    47063040(  11490 blks) ==>   872131516:47063052
1273: SKP:    53469184(  13054 blks) ==>   919194568:53469196
1274: RAW:    37793792(   9227 blks) ==>   919194580:37793804
1275: SKP:        4096(      1 blks) ==>   956988384:4108
1276: RAW:       90112(     22 blks) ==>   956988396:90124
1277: SKP:        8192(      2 blks) ==>   957078520:8204
1278: RAW:       40960(     10 blks) ==>   957078532:40972
1279: SKP:        4096(      1 blks) ==>   957119504:4108
1280: RAW:    31617024(   7719 blks) ==>   957119516:31617036
1281: SKP:        8192(      2 blks) ==>   988736552:8204
1282: RAW:       40960(     10 blks) ==>   988736564:40972
1283: SKP:        4096(      1 blks) ==>   988777536:4108
1284: RAW:       24576(      6 blks) ==>   988777548:24588
1285: SKP:        4096(      1 blks) ==>   988802136:4108
1286: RAW:       40960(     10 blks) ==>   988802148:40972
1287: SKP:        8192(      2 blks) ==>   988843120:8204
1288: RAW:       40960(     10 blks) ==>   988843132:40972
1289: SKP:        4096(      1 blks) ==>   988884104:4108
1290: RAW:       20480(      5 blks) ==>   988884116:20492
1291: SKP:        4096(      1 blks) ==>   988904608:4108
1292: RAW:       12288(      3 blks) ==>   988904620:12300
1293: SKP:        4096(      1 blks) ==>   988916920:4108
1294: RAW:       49152(     12 blks) ==>   988916932:49164
1295: SKP:        4096(      1 blks) ==>   988966096:4108
1296: RAW:       32768(      8 blks) ==>   988966108:32780
1297: SKP:        4096(      1 blks) ==>   988998888:4108
1298: RAW:       69632(     17 blks) ==>   988998900:69644
1299: SKP:        8192(      2 blks) ==>   989068544:8204
1300: RAW:       40960(     10 blks) ==>   989068556:40972
1301: SKP:        4096(      1 blks) ==>   989109528:4108
1302: RAW:       86016(     21 blks) ==>   989109540:86028
1303: SKP:        8192(      2 blks) ==>   989195568:8204
1304: RAW:       20480(      5 blks) ==>   989195580:20492
1305: SKP:        4096(      1 blks) ==>   989216072:4108
1306: RAW:       57344(     14 blks) ==>   989216084:57356
1307: SKP:        4096(      1 blks) ==>   989273440:4108
1308: RAW:       40960(     10 blks) ==>   989273452:40972
1309: SKP:        8192(      2 blks) ==>   989314424:8204
1310: RAW:       45056(     11 blks) ==>   989314436:45068
1311: SKP:        4096(      1 blks) ==>   989359504:4108
1312: RAW:       94208(     23 blks) ==>   989359516:94220
1313: SKP:        4096(      1 blks) ==>   989453736:4108
1314: RAW:       40960(     10 blks) ==>   989453748:40972
1315: SKP:        4096(      1 blks) ==>   989494720:4108
1316: RAW:       40960(     10 blks) ==>   989494732:40972
1317: SKP:        8192(      2 blks) ==>   989535704:8204
1318: RAW:       36864(      9 blks) ==>   989535716:36876
1319: SKP:        4096(      1 blks) ==>   989572592:4108
1320: RAW:       45056(     11 blks) ==>   989572604:45068
1321: SKP:        4096(      1 blks) ==>   989617672:4108
1322: RAW:       40960(     10 blks) ==>   989617684:40972
1323: SKP:        8192(      2 blks) ==>   989658656:8204
1324: RAW:       40960(     10 blks) ==>   989658668:40972
1325: SKP:        4096(      1 blks) ==>   989699640:4108
1326: RAW:       40960(     10 blks) ==>   989699652:40972
1327: SKP:        8192(      2 blks) ==>   989740624:8204
1328: RAW:      106496(     26 blks) ==>   989740636:106508
1329: SKP:        4096(      1 blks) ==>   989847144:4108
1330: RAW:       40960(     10 blks) ==>   989847156:40972
1331: SKP:        8192(      2 blks) ==>   989888128:8204
1332: RAW:       40960(     10 blks) ==>   989888140:40972
1333: SKP:        8192(      2 blks) ==>   989929112:8204
1334: RAW:       40960(     10 blks) ==>   989929124:40972
1335: SKP:        8192(      2 blks) ==>   989970096:8204
1336: RAW:       45056(     11 blks) ==>   989970108:45068
1337: SKP:        4096(      1 blks) ==>   990015176:4108
1338: RAW:       36864(      9 blks) ==>   990015188:36876
1339: SKP:        4096(      1 blks) ==>   990052064:4108
1340: RAW:       45056(     11 blks) ==>   990052076:45068
1341: SKP:        4096(      1 blks) ==>   990097144:4108
1342: RAW:       40960(     10 blks) ==>   990097156:40972
1343: SKP:        4096(      1 blks) ==>   990138128:4108
1344: RAW:       36864(      9 blks) ==>   990138140:36876
1345: SKP:        4096(      1 blks) ==>   990175016:4108
1346: RAW:       40960(     10 blks) ==>   990175028:40972
1347: SKP:        4096(      1 blks) ==>   990216000:4108
1348: RAW:       53248(     13 blks) ==>   990216012:53260
1349: SKP:        4096(      1 blks) ==>   990269272:4108
1350: RAW:    61431808(  14998 blks) ==>   990269284:61431820
1351: SKP:        4096(      1 blks) ==>  1051701104:4108
1352: RAW:     1503232(    367 blks) ==>  1051701116:1503244
1353: SKP:   536870912( 131072 blks) ==>  1053204360:536870924
1354: RAW:       12288(      3 blks) ==>  1053204372:12300
1355: SKP:        4096(      1 blks) ==>  1053216672:4108
1356: RAW:        4096(      1 blks) ==>  1053216684:4108
1357: SKP:       45056(     11 blks) ==>  1053220792:45068
1358: RAW:        8192(      2 blks) ==>  1053220804:8204
1359: SKP:        4096(      1 blks) ==>  1053229008:4108
1360: RAW:    33476608(   8173 blks) ==>  1053229020:33476620
1361: SKP:    33554432(   8192 blks) ==>  1086705640:33554444
1362: RAW:    10645504(   2599 blks) ==>  1086705652:10645516
1363: SKP:        4096(      1 blks) ==>  1097351168:4108
1364: RAW:      589824(    144 blks) ==>  1097351180:589836
1365: SKP:       32768(      8 blks) ==>  1097941016:32780
1366: RAW:     1544192(    377 blks) ==>  1097941028:1544204
1367: SKP:        4096(      1 blks) ==>  1099485232:4108
1368: RAW:        8192(      2 blks) ==>  1099485244:8204
1369: SKP:  1262239744( 308164 blks) ==>  1099493448:1262239756
1370: RAW:        8192(      2 blks) ==>  1099493460:8204
1371: SKP:        8192(      2 blks) ==>  1099501664:8204
1372: RAW:        4096(      1 blks) ==>  1099501676:4108
1373: SKP:        4096(      1 blks) ==>  1099505784:4108
1374: RAW:       16384(      4 blks) ==>  1099505796:16396
1375: SKP:       24576(      6 blks) ==>  1099522192:24588
1376: RAW:       24576(      6 blks) ==>  1099522204:24588
1377: SKP:       40960(     10 blks) ==>  1099546792:40972
1378: RAW:    11350016(   2771 blks) ==>  1099546804:11350028
1379: SKP:    22204416(   5421 blks) ==>  1110896832:22204428
1380: RAW:    37126144(   9064 blks) ==>  1110896844:37126156
1381: SKP:    63406080(  15480 blks) ==>  1148023000:63406092
1382: RAW:       12288(      3 blks) ==>  1148023012:12300
1383: SKP:     4194304(   1024 blks) ==>  1148035312:4194316
1384: RAW:    67108864(  16384 blks) ==>  1148035324:67108876
1385: SKP:   331337728(  80893 blks) ==>  1215144200:331337740
1386: RAW:    47652864(  11634 blks) ==>  1215144212:47652876
1387: SKP:        4096(      1 blks) ==>  1262797088:4108
1388: RAW:    86560768(  21133 blks) ==>  1262797100:86560780
1389: SKP:   134217728(  32768 blks) ==>  1349357880:134217740
1390: RAW:    60686336(  14816 blks) ==>  1349357892:60686348
1391: SKP:       24576(      6 blks) ==>  1410044240:24588
1392: RAW:    20127744(   4914 blks) ==>  1410044252:20127756
1393: SKP:        4096(      1 blks) ==>  1430172008:4108
1394: RAW:     4141056(   1011 blks) ==>  1430172020:4141068
1395: SKP:      118784(     29 blks) ==>  1434313088:118796
1396: RAW:    32116736(   7841 blks) ==>  1434313100:32116748
1397: SKP:       65536(     16 blks) ==>  1466429848:65548
1398: RAW:       16384(      4 blks) ==>  1466429860:16396
1399: SKP:       28672(      7 blks) ==>  1466446256:28684
1400: RAW:       24576(      6 blks) ==>  1466446268:24588
1401: SKP:        8192(      2 blks) ==>  1466470856:8204
1402: RAW:       16384(      4 blks) ==>  1466470868:16396
1403: SKP:        8192(      2 blks) ==>  1466487264:8204
1404: RAW:       45056(     11 blks) ==>  1466487276:45068
1405: SKP:       28672(      7 blks) ==>  1466532344:28684
1406: RAW:        8192(      2 blks) ==>  1466532356:8204
1407: SKP:        4096(      1 blks) ==>  1466540560:4108
1408: RAW:      143360(     35 blks) ==>  1466540572:143372
1409: SKP:       77824(     19 blks) ==>  1466683944:77836
1410: RAW:       53248(     13 blks) ==>  1466683956:53260
1411: SKP:       77824(     19 blks) ==>  1466737216:77836
1412: RAW:       57344(     14 blks) ==>  1466737228:57356
1413: SKP:        8192(      2 blks) ==>  1466794584:8204
1414: RAW:       16384(      4 blks) ==>  1466794596:16396
1415: SKP:        8192(      2 blks) ==>  1466810992:8204
1416: RAW:       45056(     11 blks) ==>  1466811004:45068
1417: SKP:       28672(      7 blks) ==>  1466856072:28684
1418: RAW:        8192(      2 blks) ==>  1466856084:8204
1419: SKP:        8192(      2 blks) ==>  1466864288:8204
1420: RAW:        8192(      2 blks) ==>  1466864300:8204
1421: SKP:        8192(      2 blks) ==>  1466872504:8204
1422: RAW:        4096(      1 blks) ==>  1466872516:4108
1423: SKP:       20480(      5 blks) ==>  1466876624:20492
1424: RAW:       45056(     11 blks) ==>  1466876636:45068
1425: SKP:       32768(      8 blks) ==>  1466921704:32780
1426: RAW:        4096(      1 blks) ==>  1466921716:4108
1427: SKP:        4096(      1 blks) ==>  1466925824:4108
1428: RAW:      258048(     63 blks) ==>  1466925836:258060
1429: SKP:       61440(     15 blks) ==>  1467183896:61452
1430: RAW:       20480(      5 blks) ==>  1467183908:20492
1431: SKP:       28672(      7 blks) ==>  1467204400:28684
1432: RAW:        8192(      2 blks) ==>  1467204412:8204
1433: SKP:        8192(      2 blks) ==>  1467212616:8204
1434: RAW:        4096(      1 blks) ==>  1467212628:4108
1435: SKP:       12288(      3 blks) ==>  1467216736:12300
1436: RAW:        4096(      1 blks) ==>  1467216748:4108
1437: SKP:        4096(      1 blks) ==>  1467220856:4108
1438: RAW:        4096(      1 blks) ==>  1467220868:4108
1439: SKP:        8192(      2 blks) ==>  1467224976:8204
1440: RAW:       49152(     12 blks) ==>  1467224988:49164
1441: SKP:       40960(     10 blks) ==>  1467274152:40972
1442: RAW:       12288(      3 blks) ==>  1467274164:12300
1443: SKP:       77824(     19 blks) ==>  1467286464:77836
1444: RAW:       53248(     13 blks) ==>  1467286476:53260
1445: SKP:       77824(     19 blks) ==>  1467339736:77836
1446: RAW:       57344(     14 blks) ==>  1467339748:57356
1447: SKP:        8192(      2 blks) ==>  1467397104:8204
1448: RAW:       12288(      3 blks) ==>  1467397116:12300
1449: SKP:       12288(      3 blks) ==>  1467409416:12300
1450: RAW:       45056(     11 blks) ==>  1467409428:45068
1451: SKP:       28672(      7 blks) ==>  1467454496:28684
1452: RAW:        8192(      2 blks) ==>  1467454508:8204
1453: SKP:        8192(      2 blks) ==>  1467462712:8204
1454: RAW:        8192(      2 blks) ==>  1467462724:8204
1455: SKP:        8192(      2 blks) ==>  1467470928:8204
1456: RAW:        4096(      1 blks) ==>  1467470940:4108
1457: SKP:       20480(      5 blks) ==>  1467475048:20492
1458: RAW:       45056(     11 blks) ==>  1467475060:45068
1459: SKP:       32768(      8 blks) ==>  1467520128:32780
1460: RAW:        4096(      1 blks) ==>  1467520140:4108
1461: SKP:        8192(      2 blks) ==>  1467524248:8204
1462: RAW:    56688640(  13840 blks) ==>  1467524260:56688652
1463: SKP:        4096(      1 blks) ==>  1524212912:4108
1464: RAW:        8192(      2 blks) ==>  1524212924:8204
1465: SKP:       49152(     12 blks) ==>  1524221128:49164
1466: RAW:        4096(      1 blks) ==>  1524221140:4108
1467: SKP:       61440(     15 blks) ==>  1524225248:61452
1468: RAW:       20480(      5 blks) ==>  1524225260:20492
1469: SKP:        4096(      1 blks) ==>  1524245752:4108
1470: RAW:     3436544(    839 blks) ==>  1524245764:3436556
1471: SKP:      258048(     63 blks) ==>  1527682320:258060
1472: RAW:    15228928(   3718 blks) ==>  1527682332:15228940
1473: SKP:        4096(      1 blks) ==>  1542911272:4108
1474: RAW:    12017664(   2934 blks) ==>  1542911284:12017676
1475: SKP:        4096(      1 blks) ==>  1554928960:4108
1476: RAW:    28164096(   6876 blks) ==>  1554928972:28164108
1477: SKP:      258048(     63 blks) ==>  1583093080:258060
1478: RAW:    10092544(   2464 blks) ==>  1583093092:10092556
1479: SKP:        8192(      2 blks) ==>  1593185648:8204
1480: RAW:       12288(      3 blks) ==>  1593185660:12300
1481: SKP:        8192(      2 blks) ==>  1593197960:8204
1482: RAW:    41267200(  10075 blks) ==>  1593197972:41267212
1483: SKP:       20480(      5 blks) ==>  1634465184:20492
1484: RAW:     1691648(    413 blks) ==>  1634465196:1691660
1485: SKP:        4096(      1 blks) ==>  1636156856:4108
1486: RAW:    18059264(   4409 blks) ==>  1636156868:18059276
1487: SKP:       16384(      4 blks) ==>  1654216144:16396
1488: RAW:       20480(      5 blks) ==>  1654216156:20492
1489: SKP:       16384(      4 blks) ==>  1654236648:16396
1490: RAW:       20480(      5 blks) ==>  1654236660:20492
1491: SKP:       12288(      3 blks) ==>  1654257152:12300
1492: RAW:       20480(      5 blks) ==>  1654257164:20492
1493: SKP:       16384(      4 blks) ==>  1654277656:16396
1494: RAW:       20480(      5 blks) ==>  1654277668:20492
1495: SKP:       16384(      4 blks) ==>  1654298160:16396
1496: RAW:       20480(      5 blks) ==>  1654298172:20492
1497: SKP:       16384(      4 blks) ==>  1654318664:16396
1498: RAW:       77824(     19 blks) ==>  1654318676:77836
1499: SKP:       16384(      4 blks) ==>  1654396512:16396
1500: RAW:       24576(      6 blks) ==>  1654396524:24588
1501: SKP:       16384(      4 blks) ==>  1654421112:16396
1502: RAW:       20480(      5 blks) ==>  1654421124:20492
1503: SKP:       16384(      4 blks) ==>  1654441616:16396
1504: RAW:       24576(      6 blks) ==>  1654441628:24588
1505: SKP:       12288(      3 blks) ==>  1654466216:12300
1506: RAW:       24576(      6 blks) ==>  1654466228:24588
1507: SKP:       12288(      3 blks) ==>  1654490816:12300
1508: RAW:       20480(      5 blks) ==>  1654490828:20492
1509: SKP:       16384(      4 blks) ==>  1654511320:16396
1510: RAW:       36864(      9 blks) ==>  1654511332:36876
1511: SKP:       12288(      3 blks) ==>  1654548208:12300
1512: RAW:       24576(      6 blks) ==>  1654548220:24588
1513: SKP:       12288(      3 blks) ==>  1654572808:12300
1514: RAW:       49152(     12 blks) ==>  1654572820:49164
1515: SKP:        4096(      1 blks) ==>  1654621984:4108
1516: RAW:    13651968(   3333 blks) ==>  1654621996:13651980
1517: SKP:        4096(      1 blks) ==>  1668273976:4108
1518: RAW:     1703936(    416 blks) ==>  1668273988:1703948
1519: SKP:        4096(      1 blks) ==>  1669977936:4108
1520: RAW:     9375744(   2289 blks) ==>  1669977948:9375756
1521: SKP:        8192(      2 blks) ==>  1679353704:8204
1522: RAW:     1949696(    476 blks) ==>  1679353716:1949708
1523: SKP:        8192(      2 blks) ==>  1681303424:8204
1524: RAW:      364544(     89 blks) ==>  1681303436:364556
1525: SKP:        4096(      1 blks) ==>  1681667992:4108
1526: RAW:        4096(      1 blks) ==>  1681668004:4108
1527: SKP:        8192(      2 blks) ==>  1681672112:8204
1528: RAW:    14053376(   3431 blks) ==>  1681672124:14053388
1529: SKP:        4096(      1 blks) ==>  1695725512:4108
1530: RAW:     2969600(    725 blks) ==>  1695725524:2969612
1531: SKP:        4096(      1 blks) ==>  1698695136:4108
1532: RAW:    12718080(   3105 blks) ==>  1698695148:12718092
1533: SKP:       12288(      3 blks) ==>  1711413240:12300
1534: RAW:      266240(     65 blks) ==>  1711413252:266252
1535: SKP:    38367232(   9367 blks) ==>  1711679504:38367244
1536: RAW:     6520832(   1592 blks) ==>  1711679516:6520844
1537: SKP:        4096(      1 blks) ==>  1718200360:4108
1538: RAW:        8192(      2 blks) ==>  1718200372:8204
1539: SKP:       49152(     12 blks) ==>  1718208576:49164
1540: RAW:        4096(      1 blks) ==>  1718208588:4108
1541: SKP:       61440(     15 blks) ==>  1718212696:61452
1542: RAW:     4603904(   1124 blks) ==>  1718212708:4603916
1543: SKP:       12288(      3 blks) ==>  1722816624:12300
1544: RAW:       90112(     22 blks) ==>  1722816636:90124
1545: SKP:       12288(      3 blks) ==>  1722906760:12300
1546: RAW:       94208(     23 blks) ==>  1722906772:94220
1547: SKP:       12288(      3 blks) ==>  1723000992:12300
1548: RAW:       90112(     22 blks) ==>  1723001004:90124
1549: SKP:       12288(      3 blks) ==>  1723091128:12300
1550: RAW:        4096(      1 blks) ==>  1723091140:4108
1551: SKP:        4096(      1 blks) ==>  1723095248:4108
1552: RAW:       81920(     20 blks) ==>  1723095260:81932
1553: SKP:       12288(      3 blks) ==>  1723177192:12300
1554: RAW:       90112(     22 blks) ==>  1723177204:90124
1555: SKP:       12288(      3 blks) ==>  1723267328:12300
1556: RAW:       94208(     23 blks) ==>  1723267340:94220
1557: SKP:       12288(      3 blks) ==>  1723361560:12300
1558: RAW:       90112(     22 blks) ==>  1723361572:90124
1559: SKP:       12288(      3 blks) ==>  1723451696:12300
1560: RAW:        4096(      1 blks) ==>  1723451708:4108
1561: SKP:        4096(      1 blks) ==>  1723455816:4108
1562: RAW:       81920(     20 blks) ==>  1723455828:81932
1563: SKP:       12288(      3 blks) ==>  1723537760:12300
1564: RAW:       90112(     22 blks) ==>  1723537772:90124
1565: SKP:       12288(      3 blks) ==>  1723627896:12300
1566: RAW:     2404352(    587 blks) ==>  1723627908:2404364
1567: SKP:   924925952( 225812 blks) ==>  1726032272:924925964
1568: RAW:        8192(      2 blks) ==>  1726032284:8204
1569: SKP:        4096(      1 blks) ==>  1726040488:4108
1570: RAW:        8192(      2 blks) ==>  1726040500:8204
1571: SKP:       45056(     11 blks) ==>  1726048704:45068
1572: RAW:       12288(      3 blks) ==>  1726048716:12300
1573: SKP:       53248(     13 blks) ==>  1726061016:53260
1574: RAW:     5255168(   1283 blks) ==>  1726061028:5255180
1575: SKP:    28299264(   6909 blks) ==>  1731316208:28299276
1576: RAW:     5947392(   1452 blks) ==>  1731316220:5947404
1577: SKP:    94584832(  23092 blks) ==>  1737263624:94584844
1578: RAW:   134217728(  32768 blks) ==>  1737263636:134217740
1579: SKP:   134217728(  32768 blks) ==>  1871481376:134217740
1580: RAW:    20004864(   4884 blks) ==>  1871481388:20004876
1581: SKP:       24576(      6 blks) ==>  1891486264:24588
1582: RAW:      356352(     87 blks) ==>  1891486276:356364
1583: SKP:        8192(      2 blks) ==>  1891842640:8204
1584: RAW:      794624(    194 blks) ==>  1891842652:794636
1585: SKP:       12288(      3 blks) ==>  1892637288:12300
1586: RAW:      114688(     28 blks) ==>  1892637300:114700
1587: SKP:       20480(      5 blks) ==>  1892752000:20492
1588: RAW:       65536(     16 blks) ==>  1892752012:65548
1589: SKP:        8192(      2 blks) ==>  1892817560:8204
1590: RAW:    29597696(   7226 blks) ==>  1892817572:29597708
1591: SKP:        4096(      1 blks) ==>  1922415280:4108
1592: RAW:     8388608(   2048 blks) ==>  1922415292:8388620
1593: SKP:        4096(      1 blks) ==>  1930803912:4108
1594: RAW:    78045184(  19054 blks) ==>  1930803924:78045196
1595: SKP:  1607380992( 392427 blks) ==>  2008849120:1607381004
1596: RAW:        8192(      2 blks) ==>  2008849132:8204
1597: SKP:       57344(     14 blks) ==>  2008857336:57356
1598: RAW:        4096(      1 blks) ==>  2008857348:4108
1599: SKP:       61440(     15 blks) ==>  2008861456:61452
1600: RAW:     2068480(    505 blks) ==>  2008861468:2068492
1601: SKP:    31485952(   7687 blks) ==>  2010929960:31485964
1602: RAW:     1773568(    433 blks) ==>  2010929972:1773580
1603: SKP:    98758656(  24111 blks) ==>  2012703552:98758668
1604: RAW:       12288(      3 blks) ==>  2012703564:12300
1605: SKP:     4194304(   1024 blks) ==>  2012715864:4194316
1606: RAW:     6238208(   1523 blks) ==>  2012715876:6238220
1607: SKP:        4096(      1 blks) ==>  2018954096:4108
1608: RAW:       36864(      9 blks) ==>  2018954108:36876
1609: SKP:        4096(      1 blks) ==>  2018990984:4108
1610: RAW:       12288(      3 blks) ==>  2018990996:12300
1611: SKP:        4096(      1 blks) ==>  2019003296:4108
1612: RAW:       20480(      5 blks) ==>  2019003308:20492
1613: SKP:        4096(      1 blks) ==>  2019023800:4108
1614: RAW:       45056(     11 blks) ==>  2019023812:45068
1615: SKP:        4096(      1 blks) ==>  2019068880:4108
1616: RAW:        8192(      2 blks) ==>  2019068892:8204
1617: SKP:        4096(      1 blks) ==>  2019077096:4108
1618: RAW:     4976640(   1215 blks) ==>  2019077108:4976652
1619: SKP:        4096(      1 blks) ==>  2024053760:4108
1620: RAW:     5279744(   1289 blks) ==>  2024053772:5279756
1621: SKP:        4096(      1 blks) ==>  2029333528:4108
1622: RAW:       94208(     23 blks) ==>  2029333540:94220
1623: SKP:        4096(      1 blks) ==>  2029427760:4108
1624: RAW:      163840(     40 blks) ==>  2029427772:163852
1625: SKP:        4096(      1 blks) ==>  2029591624:4108
1626: RAW:      409600(    100 blks) ==>  2029591636:409612
1627: SKP:        4096(      1 blks) ==>  2030001248:4108
1628: RAW:      155648(     38 blks) ==>  2030001260:155660
1629: SKP:        4096(      1 blks) ==>  2030156920:4108
1630: RAW:    45412352(  11087 blks) ==>  2030156932:45412364
1631: SKP:    33554432(   8192 blks) ==>  2075569296:33554444
1632: RAW:    11685888(   2853 blks) ==>  2075569308:11685900
1633: SKP:        4096(      1 blks) ==>  2087255208:4108
1634: RAW:     5222400(   1275 blks) ==>  2087255220:5222412
1635: SKP:  1895690240( 462815 blks) ==>  2092477632:1895690252
1636: RAW:       12288(      3 blks) ==>  2092477644:12300
1637: SKP:       53248(     13 blks) ==>  2092489944:53260
1638: RAW:        8192(      2 blks) ==>  2092489956:8204
1639: SKP:       57344(     14 blks) ==>  2092498160:57356
1640: RAW:     3547136(    866 blks) ==>  2092498172:3547148
1641: SKP:    30007296(   7326 blks) ==>  2096045320:30007308
1642: RAW:     7950336(   1941 blks) ==>  2096045332:7950348
1643: SKP:    92581888(  22603 blks) ==>  2103995680:92581900
1644: RAW:     8110080(   1980 blks) ==>  2103995692:8110092
1645: SKP:        4096(      1 blks) ==>  2112105784:4108
1646: RAW:    22007808(   5373 blks) ==>  2112105796:22007820
1647: SKP:        4096(      1 blks) ==>  2134113616:4108
1648: RAW:    45768704(  11174 blks) ==>  2134113628:45768716
1649: SKP:        4096(      1 blks) ==>  2179882344:4108
1650: RAW:       16384(      4 blks) ==>  2179882356:16396
1651: SKP:        4096(      1 blks) ==>  2179898752:4108
1652: RAW:       49152(     12 blks) ==>  2179898764:49164
1653: SKP:        4096(      1 blks) ==>  2179947928:4108
1654: RAW:       45056(     11 blks) ==>  2179947940:45068
1655: SKP:        4096(      1 blks) ==>  2179993008:4108
1656: RAW:        8192(      2 blks) ==>  2179993020:8204
1657: SKP:        4096(      1 blks) ==>  2180001224:4108
1658: RAW:       20480(      5 blks) ==>  2180001236:20492
1659: SKP:        4096(      1 blks) ==>  2180021728:4108
1660: RAW:       16384(      4 blks) ==>  2180021740:16396
1661: SKP:        4096(      1 blks) ==>  2180038136:4108
1662: RAW:        8192(      2 blks) ==>  2180038148:8204
1663: SKP:        4096(      1 blks) ==>  2180046352:4108
1664: RAW:       28672(      7 blks) ==>  2180046364:28684
1665: SKP:        4096(      1 blks) ==>  2180075048:4108
1666: RAW:       20480(      5 blks) ==>  2180075060:20492
1667: SKP:        4096(      1 blks) ==>  2180095552:4108
1668: RAW:        8192(      2 blks) ==>  2180095564:8204
1669: SKP:        4096(      1 blks) ==>  2180103768:4108
1670: RAW:       16384(      4 blks) ==>  2180103780:16396
1671: SKP:        4096(      1 blks) ==>  2180120176:4108
1672: RAW:       20480(      5 blks) ==>  2180120188:20492
1673: SKP:        4096(      1 blks) ==>  2180140680:4108
1674: RAW:        4096(      1 blks) ==>  2180140692:4108
1675: SKP:        4096(      1 blks) ==>  2180144800:4108
1676: RAW:        8192(      2 blks) ==>  2180144812:8204
1677: SKP:        4096(      1 blks) ==>  2180153016:4108
1678: RAW:        4096(      1 blks) ==>  2180153028:4108
1679: SKP:        4096(      1 blks) ==>  2180157136:4108
1680: RAW:       40960(     10 blks) ==>  2180157148:40972
1681: SKP:        4096(      1 blks) ==>  2180198120:4108
1682: RAW:       90112(     22 blks) ==>  2180198132:90124
1683: SKP:        4096(      1 blks) ==>  2180288256:4108
1684: RAW:       16384(      4 blks) ==>  2180288268:16396
1685: SKP:        4096(      1 blks) ==>  2180304664:4108
1686: RAW:      745472(    182 blks) ==>  2180304676:745484
1687: SKP:        4096(      1 blks) ==>  2181050160:4108
1688: RAW:       20480(      5 blks) ==>  2181050172:20492
1689: SKP:        4096(      1 blks) ==>  2181070664:4108
1690: RAW:       12288(      3 blks) ==>  2181070676:12300
1691: SKP:        4096(      1 blks) ==>  2181082976:4108
1692: RAW:        8192(      2 blks) ==>  2181082988:8204
1693: SKP:        4096(      1 blks) ==>  2181091192:4108
1694: RAW:        4096(      1 blks) ==>  2181091204:4108
1695: SKP:        4096(      1 blks) ==>  2181095312:4108
1696: RAW:       16384(      4 blks) ==>  2181095324:16396
1697: SKP:        4096(      1 blks) ==>  2181111720:4108
1698: RAW:        8192(      2 blks) ==>  2181111732:8204
1699: SKP:        4096(      1 blks) ==>  2181119936:4108
1700: RAW:       16384(      4 blks) ==>  2181119948:16396
1701: SKP:        4096(      1 blks) ==>  2181136344:4108
1702: RAW:       45056(     11 blks) ==>  2181136356:45068
1703: SKP:        4096(      1 blks) ==>  2181181424:4108
1704: RAW:       32768(      8 blks) ==>  2181181436:32780
1705: SKP:        4096(      1 blks) ==>  2181214216:4108
1706: RAW:       20480(      5 blks) ==>  2181214228:20492
1707: SKP:        4096(      1 blks) ==>  2181234720:4108
1708: RAW:       16384(      4 blks) ==>  2181234732:16396
1709: SKP:        4096(      1 blks) ==>  2181251128:4108
1710: RAW:       16384(      4 blks) ==>  2181251140:16396
1711: SKP:        4096(      1 blks) ==>  2181267536:4108
1712: RAW:        8192(      2 blks) ==>  2181267548:8204
1713: SKP:        4096(      1 blks) ==>  2181275752:4108
1714: RAW:       24576(      6 blks) ==>  2181275764:24588
1715: SKP:        4096(      1 blks) ==>  2181300352:4108
1716: RAW:        8192(      2 blks) ==>  2181300364:8204
1717: SKP:        4096(      1 blks) ==>  2181308568:4108
1718: RAW:        4096(      1 blks) ==>  2181308580:4108
1719: SKP:        4096(      1 blks) ==>  2181312688:4108
1720: RAW:        8192(      2 blks) ==>  2181312700:8204
1721: SKP:        4096(      1 blks) ==>  2181320904:4108
1722: RAW:        4096(      1 blks) ==>  2181320916:4108
1723: SKP:        4096(      1 blks) ==>  2181325024:4108
1724: RAW:        8192(      2 blks) ==>  2181325036:8204
1725: SKP:        4096(      1 blks) ==>  2181333240:4108
1726: RAW:        8192(      2 blks) ==>  2181333252:8204
1727: SKP:        4096(      1 blks) ==>  2181341456:4108
1728: RAW:        8192(      2 blks) ==>  2181341468:8204
1729: SKP:        4096(      1 blks) ==>  2181349672:4108
1730: RAW:        4096(      1 blks) ==>  2181349684:4108
1731: SKP:        4096(      1 blks) ==>  2181353792:4108
1732: RAW:        8192(      2 blks) ==>  2181353804:8204
1733: SKP:        4096(      1 blks) ==>  2181362008:4108
1734: RAW:       16384(      4 blks) ==>  2181362020:16396
1735: SKP:        4096(      1 blks) ==>  2181378416:4108
1736: RAW:        8192(      2 blks) ==>  2181378428:8204
1737: SKP:        4096(      1 blks) ==>  2181386632:4108
1738: RAW:        8192(      2 blks) ==>  2181386644:8204
1739: SKP:        4096(      1 blks) ==>  2181394848:4108
1740: RAW:       32768(      8 blks) ==>  2181394860:32780
1741: SKP:        4096(      1 blks) ==>  2181427640:4108
1742: RAW:       12288(      3 blks) ==>  2181427652:12300
1743: SKP:        4096(      1 blks) ==>  2181439952:4108
1744: RAW:        8192(      2 blks) ==>  2181439964:8204
1745: SKP:        4096(      1 blks) ==>  2181448168:4108
1746: RAW:        8192(      2 blks) ==>  2181448180:8204
1747: SKP:        4096(      1 blks) ==>  2181456384:4108
1748: RAW:       28672(      7 blks) ==>  2181456396:28684
1749: SKP:        4096(      1 blks) ==>  2181485080:4108
1750: RAW:       12288(      3 blks) ==>  2181485092:12300
1751: SKP:        4096(      1 blks) ==>  2181497392:4108
1752: RAW:       49152(     12 blks) ==>  2181497404:49164
1753: SKP:        4096(      1 blks) ==>  2181546568:4108
1754: RAW:        8192(      2 blks) ==>  2181546580:8204
1755: SKP:        4096(      1 blks) ==>  2181554784:4108
1756: RAW:        4096(      1 blks) ==>  2181554796:4108
1757: SKP:        4096(      1 blks) ==>  2181558904:4108
1758: RAW:        8192(      2 blks) ==>  2181558916:8204
1759: SKP:        4096(      1 blks) ==>  2181567120:4108
1760: RAW:       20480(      5 blks) ==>  2181567132:20492
1761: SKP:        4096(      1 blks) ==>  2181587624:4108
1762: RAW:       16384(      4 blks) ==>  2181587636:16396
1763: SKP:        4096(      1 blks) ==>  2181604032:4108
1764: RAW:      380928(     93 blks) ==>  2181604044:380940
1765: SKP:        4096(      1 blks) ==>  2181984984:4108
1766: RAW:       28672(      7 blks) ==>  2181984996:28684
1767: SKP:        4096(      1 blks) ==>  2182013680:4108
1768: RAW:        4096(      1 blks) ==>  2182013692:4108
1769: SKP:        4096(      1 blks) ==>  2182017800:4108
1770: RAW:    95666176(  23356 blks) ==>  2182017812:95666188
1771: SKP:    27381760(   6685 blks) ==>  2277684000:27381772
1772: RAW:    33554432(   8192 blks) ==>  2277684012:33554444
1773: SKP:  1778384896( 434176 blks) ==>  2311238456:1778384908
-- Total: -----------------------------------------------------------
1774 CHUNK 15032385536(3670016 blks) ==>  2311238468(564262 blks)

done.
system.img built successfully. 
copying dtbfile(/home/khanhj/Documents/D/L4T/Linux_for_Tegra/kernel/dtb/tegra124-jetson_tk1-pm375-000-c00-00.dtb)... done.
copying cfgfile(/home/khanhj/Documents/D/L4T/Linux_for_Tegra/bootloader/ardbeg/cfg/gnu_linux_fastboot_emmc_full.cfg) to flash.cfg... done.
creating gpt(ppt.img)... 

*** GPT Parameters ***
Device Sector Size ------- 512
device size -------------- 15766388736
bootpart size ------------ 8388608
userpart size ------------ 15758000128
Erase Block Size --------- 2097152
FS Buffer size ----------- 4096
Partition Config file ---- flash.cfg
Visible partition flag --- GP1
Primary GPT output ------- PPT->ppt.img
Secondary GPT output ----- GPT->gpt.img
Target device name ------- none

*** PARTITION LAYOUT(20 partitions) ***
[     BCT] BH            0        16383       8.0MiB 
[     PPT] UH            0         4095       2.0MiB ppt.img
[      PT] UH         4096         8191       2.0MiB 
[     EBT] UH         8192        16383       4.0MiB u-boot.bin
[     LNX] UH        16384        49151      16.0MiB 
[     SOS] UH        49152        61439       6.0MiB 
[     NVC] UH        61440        65535       2.0MiB 
[     MPB] UH        65536        77823       6.0MiB 
[     MBP] UH        77824        90111       6.0MiB 
[     GP1] UH        90112        94207       2.0MiB 
[     APP] UV        94208     29454335   14336.0MiB system.img
[     DTB] UV     29454336     29462527       4.0MiB tegra124-jetson_tk1-pm375-000-c00-00.dtb
[     EFI] UV     29462528     29593599      64.0MiB 
[     USP] UV     29593600     29601791       4.0MiB 
[     TP1] UV     29601792     29609983       4.0MiB 
[     TP2] UV     29609984     29618175       4.0MiB 
[     TP3] UV     29618176     29626367       4.0MiB 
[     WB0] UV     29626368     29630463       2.0MiB 
[     UDA] UV     29630464     30773247     558.0MiB 
[     GPT] UH     30773248     30777343       2.0MiB gpt.img
copying flasher(/home/khanhj/Documents/D/L4T/Linux_for_Tegra/bootloader/ardbeg/fastboot.bin)... done.
Existing flashapp(/home/khanhj/Documents/D/L4T/Linux_for_Tegra/bootloader/nvflash) reused.
*** Flashing target device started. ***
./nvflash  --bct PM375_Hynix_2GB_H5TC4G63AFR_H5TC4G63CFR_RDA_924MHz.cfg --setbct --configfile flash.cfg  --create --bl fastboot.bin --odmdata 0x6009C000 --go
Nvflash 4.13.0000 started
BR_CID: 0x34001001741141021c00000005048340
rcm version 0X400001
Skipping BoardID read at miniloader level
System Information:
   chip name: unknown
   chip id: 0x40 major: 1 minor: 1
   chip sku: 0x0
   chip uid: 0x00000001741141021c00000005048340
   macrovision: disabled
   hdcp: disabled
   jtag: disabled
   sbk burned: false
   board id: 0
   warranty fuse: 0
   dk burned: false
   boot device: emmc
   operating mode: 3
   device config strap: 0
   device config fuse: 0
   sdram config strap: 0

RCM communication completed
BCT sent successfully
sending file: tegra124-jetson_tk1-pm375-000-c00-00.dtb
- 59966/59966 bytes sent
tegra124-jetson_tk1-pm375-000-c00-00.dtb sent successfully
odm data: 0x6009c000
downloading bootloader -- load address: 0x83d88000 entry point: 0x83d88000
sending file: fastboot.bin
- 594363/594363 bytes sent
fastboot.bin sent successfully
waiting for bootloader to initialize
bootloader downloaded successfully
ML execution and Cpu Handover took 1 Secs
Partition backup took 0 Secs
setting device: 2 3
deleting device partitions
creating partition: BCT
creating partition: PPT
creating partition: PT
creating partition: EBT
creating partition: LNX
creating partition: SOS
creating partition: NVC
creating partition: MPB
creating partition: MBP
creating partition: GP1
creating partition: APP
creating partition: DTB
creating partition: EFI
creating partition: USP
creating partition: TP1
creating partition: TP2
creating partition: TP3
creating partition: WB0
creating partition: UDA
creating partition: GPT
sending file: ppt.img
\ 2097152/2097152 bytes sent
ppt.img sent successfully
padded 8 bytes to bootloader
sending file: u-boot.bin
- 625776/625776 bytes sent
u-boot.bin sent successfully
sending file: system.img
- 2311238468/2311238468 bytes sent
system.img sent successfully
sending file: tegra124-jetson_tk1-pm375-000-c00-00.dtb
- 59966/59966 bytes sent
tegra124-jetson_tk1-pm375-000-c00-00.dtb sent successfully
sending file: gpt.img
\ 2097152/2097152 bytes sent
gpt.img sent successfully
Create, format and download  took 166 Secs
Time taken for flashing 169 Secs
*** The target ardbeg has been flashed successfully. ***
Reset the board to boot from internal eMMC.
```
