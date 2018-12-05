# nanopi-m4-ubuntu-base-minimal

Ubuntu 18.04 base minimal image for RK3399 (NanoPi M4 / NEO4)


OS Image for development with the following tidbits:

* Kernel 4.4.y (with the best of both world, rockchip bsp kernel + kernel.org 4.4.y)
* Gbps
* Wifi
* Bluetooth
* 3D mali gpu (fbdev / lxde)
* VPU (X11 / lxde)
* camera (WiP)

You need *wget* and *curl* installed to grab the files in a Linux distro.

Get the latest files by running (or seee below to fetch specific Release version files):


	wget $(curl -s https://api.github.com/repos/avafinger/nanopi-m4-ubuntu-base-minimal/releases/latest | grep -oP '"browser_download_url": "\K(.*)(?=")')


then

	sudo ./flash_sd.sh /dev/sdX (or /dev/mmcblkY) where X is a letter from b,c.. and Y is a number from 0,1..)



**WARNING**
Find the correct device letter for your USB SD CARD or you may wipe your hdd.


# Release v1.0

These are the raw files for building the OS Image with kernel 4.4.166-rockchip

# Release v1.1

* minor fixes and optimizations (4K, journaling , heart-beat)
* DHCP enabled (default)
* We're ready to roll


		user: ubuntu
		password: ubuntu


Get v1.1 files:

		wget $(curl -s https://api.github.com/repos/avafinger/nanopi-m4-ubuntu-base-minimal/releases | grep -oP '"browser_download_url": "\K(.*)(?=")' | grep v1.1)


Boot takes about 10 seconds or less depending on SD card in use. 
**Tip**: If you can't see anything on screen, type enter twice!


On first login:

	sudo apt-get update
	sudo apt-get dist-upgrade



**Tip**: You may need to update the file **resolver.conf** to reflect you network (DNS)



type in the shell:	df -lh


	Filesystem      Size  Used Avail Use% Mounted on
	/dev/mmcblk0p2  7.3G  582M  6.4G   9% /
	devtmpfs        963M     0  963M   0% /dev
	tmpfs           964M     0  964M   0% /dev/shm
	tmpfs           964M   17M  947M   2% /run
	tmpfs           5.0M     0  5.0M   0% /run/lock
	tmpfs           964M     0  964M   0% /sys/fs/cgroup
	/dev/mmcblk0p1  113M   21M   84M  20% /boot
	tmpfs           193M     0  193M   0% /run/user/1000



type in the shell: free -m


	              total        used        free      shared  buff/cache   available
	Mem:           1926          47        1798          24          80        1793
	Swap:             0           0           0



Now we can start installing and/or configuring things:

* ssh
* wifi
* 3D mali user space for OpenGLES 3.1 / OpenCL 1.2 ( fbdev and X11 )	
* bluetooth
* VPU ( encode / decoding )
* camera ( when ready !?! )

**Instructions and DEB packages coming soon**

# Remote access the board

Install ssh to be able to login remotely:


		sudo apt-get install ssh


from your PC:

		ssh ubuntu@IP
		where IP is the board IP assigned by DHCP


# 3D Mali (fbdev)

To be able to use OpenGL ES 2 / 3 we need to install the Mali user space lib.

* Download files:

		wget $(curl -s https://api.github.com/repos/avafinger/nanopi-m4-ubuntu-base-minimal/releases | grep -oP '"browser_download_url": "\K(.*)(?=")' | grep v1.2)

* Install the necessary packages:

		sudo apt-get install libjpeg-turbo8 libjpeg8 libpng16-16 libegl1 libegl-mesa0 libpng-dev libjpeg-dev

* Install Mali


		sudo dpkg -i --force-all mali-t86x-rk3399-linux-4.4.y_1.0-1.deb

Ignore the warnings.


* Install enhanced htop:

You can monitor the health of you RK3399 (CPU Temp, CPU Freq and CPU VCore, enter F2 and add these monitors)

		sudo dpkg -i htop_2.1.1-3_arm64.deb 


* Install tools for benchmarking mali on fbdev:


		sudo dpkg -i glmark2-data_2014.03+git20150611.fa71af2d-0ubuntu5_all.deb 
		sudo dpkg -i glmark2-es2-fbdev_2014.03+git20150611.fa71af2d-0ubuntu5_arm64.deb 


If everithing is Okay, then you can test it:

		
		sudo glmark2-es2-fbdev (test it remotely)

