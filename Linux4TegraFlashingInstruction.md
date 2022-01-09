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

    (${BOARD} refers to 'jetson-tk1')

    Jetson-tk1: Tegra124_Linux_R21.8.0_armhf.tbz2

1. Download the latest L4T release package for your developer system and the
   sample file system from https://developer.nvidia.com/linux-tegra

   If NVIDIA does not yet provide public release for the developer system you
   have, please contact your NVIDIA support representative to obtain the latest
   L4T release package for use with the developer board.

2. Untar the files and assemble the rootfs:

   sudo tar xpf ${RELEASE_NAME}
   cd Linux_for_Tegra/rootfs/
   sudo tar xpf ../../Tegra_Linux_Sample-Root-Filesystem_R21.8.0_armhf.tbz2
   cd ../
   sudo ./apply_binaries.sh

3. Flash the rootfs onto the system's internal eMMC.

   a) Put your system into "reset recovery mode" by holding down the RECOVERY
      button and press RESET button once on the main board.
   b) Ensure your Linux host system is connected to the target device
      through the USB cable for flashing.

      sudo ./flash.sh ${BOARD} mmcblk0p1  #This will take less than 10 minutes.

4. The target will automatically reboot upon completion of the flash. The
   command prompt will show up over the display that you have attached to
   the target. Log in as user login:ubuntu and password:ubuntu. All actions
   are completed unless you wish to configure the graphical desktop on your
   setup. You now have Linux running on your developer system.

5. Installing the graphical desktop on your target board (if not already
   installed):

   a) Make sure the Ethernet cable is connected.
   b) Use eth0 for the built-in Ethernet port:

      sudo dhclient eth0

   c) Check to see if Ethernet is up and running. You should see an IP address
      associated with eth0.

      ifconfig
      sudo apt-get update
      sudo apt-get install ubuntu-desktop

   d) Reboot and the system will boot to the graphical desktop.

   NOTE: the above steps can be used to install other packages with
         "sudo apt-get install".

Please refer to the release notes provided with your software for up-to-date
information on platform features and use.