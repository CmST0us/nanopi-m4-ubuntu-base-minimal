# nanopi-m4-ubuntu-base-minimal

Ubuntu 18.04 base minimal image for RK3399 (NanoPi M4 / NEO4)

OS Image for development with the following tidbits:

* Kernel 4.4.y (with the best of both world, rockchip bsp kernel + kernel.org 4.4.y)
* Gbps
* Wifi
* Bluetooth
* 3D mali gpu (fbdev / gbm / x11)
* VPU (GBM / X11 / lxde)
* camera (WiP)

**OS Image**
* [OS Image Install Howto](#os-image)

**BSP Kernel 4.4**
* [Release v1.0](#release-v10)
* [Release v1.1](#release-v11)
* [Remote access - ssh](#remote-access-the-board)
* [mali - fbdev](#3d-mali-fbdev)
* [Wifi - wlan](#wifi)
* [GBM - mali](#gbm)
* [Release v1.0](#release-v11)
* [Kodi Media Center on RK3399](#kodi-media-center-on-rk3399)
* [Release v1.3  - Kernel 4.4.168](#release-v13)
* [Release v1.4  - Kernel 4.4.169](#release-v14)
* [Release v1.8  - Kernel 4.4.169 eMMC install](#release-v18-os-image-for-emmc-only)
* [Release v1.9  - Kernel 4.4.170](#release-v19)
* [Release v1.10 - Kernel 4.4.171](#release-v110)
* [Release v1.11 - Kernel 4.4.172](#release-v111)
* [Release v1.13 - Kernel 4.4.173](#release-v113)
* [Release v1.15 - Kernel 4.4.173-rk3399](#release-v115)
* [Release v1.18 - Kernel 4.4.175-rk3399](#release-v118)
* [Release v1.19 - Kernel 4.4.177-rk3399](#release-v119)
* [Fix for memory leak and crash](#fix-for-memory-leak-and-random-crahes)
* [Bluetooth](#bluetooth)
* [Kodi on login](#libreelec-or-not-libreelec)
* [Kodi 19](#building-kodi-19)
* [Building Kodi 19](#building-kodi-19)

**Mainline Kernel 5.x**
* [Mainline Kernel on NanoPi M4](#mainline-kernel-on-nanopi-m4)
* [Mainline Kernel 5.0-rc2](#mainline-kernel-50-rc2-ubuntu-minimal-1804)
* [Release v1.14 - Experimental](#release-v114-experimental)
* [Mainline Kernel 5.1-rc6](mainline-kernel-51-rc6---release-123-experimental)
* [Mainline Kernel 5.2.0](#mainline-kernel-520)
* [Mainline Kernel 5.6.2](#mainline-kernel-562)
* [Building Mainline Instructions](#build-mainline-kernel-on-nanopi-m4-on-board)


**Ubuntu 19.10 - EOAN Ermine**
* [Ubuntu 19.10](#nanopi-m4-ubuntu-base-minimal-1910-development)
* [Kernel 5.3.0-rc7](#mainline-linux-kernel-530-rc7)
* [Kernel 5.3.1](#mainline-linux-kernel-531)
* [Kernel 5.4.0-rc4](#mainline-linux-kernel-540-rc4)
* [Bluetooth Ubuntu 19.10](#mainline-bluetooth)
* [Building Kernel 5.3.1 on board](#build-instructions)

**Status of the Mainline Kernel 5.4.y**
* [Kernel 5.4.0-rc7](#mainline-kernel-54y-follow-up)
* [Kernel 5.4.0-rc8](#mainline-kernel-54y-follow-up)
* [Kernel 5.4.0](#mainline-kernel-54y-follow-up)
* [Kernel 5.4.1](#mainline-kernel-54y-follow-up)
* [3D Panfrost](#panfrost-3d-graphics)
* [Kodi on mainline 5.4](#kodi-on-540)


**Fixing Wifi on Mainline Kernel**
* [2.4 GHz and 5 GHz](#fix-wifi-on-mainline-kernels)

**Status of the Mainline Kernel 5.7.y**
* [Kernel 5.7.0-rc4](#mainline-57y-status)
* [Kernel 5.7.0 linux-image](#mainline-kernel-570)

# Mainline 5.7.y status

|  SBC Dev Board tested  |        NanoPi M4             |
|------------------------|------------------------------|
| kernel version         |       5.7.1                  |
| gcc version            |       9.2.1                  |
| display                |       hdmi                   |
| graphical interface    |       CLI                    |
| idle Temp ºC / freq    |   33 ºC / 408 Mhz            |
| full Temp ºC / freq    |   55 ºC / 1.20 GHz - 1.99 GHz|
| RAM memory usage (avg) |      101   Mbytes            |
| i2c                    |       yes                    |
| spi                    |                              |
| hdmi sound out         |       yes                    |
| rt5651                 |       yes                    |
| spdif                  | yes (need some testing)      |
| Camera                 |                              |
| Wifi                   |       yes (new firmware)     |
| BT                     |       yes                    |
| ethernet               |       Gbps / 100Mbps         |
| sound                  |   hdmi-sound and Bluetooth   |
| gpu            	 |      panfrost	        |
| vpu            	 |      yes (common formats)  	|
| DVFS           	 |      yes	        	|
|------------------------|------------------------------|

(*) Problems / Issues

* Reboot

## Mainline Kernel 5.7.1

Bootlog: https://gist.github.com/avafinger/54a1d590308215a37e437d1a93033c15

Support for:

* DVFS
* GPU / VPU
* Wifi
* Eth
* BT
* hdmi
* hdmi-sound
* rt5651 (jack)
* spdif (?)

**Basic Benchmark**

* 7z b

	7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
	p7zip Version 16.02 (locale=C.UTF-8,Utf16=on,HugeFiles=on,64 bits,6 CPUs LE)

	LE
	CPU Freq: - - - - - - 512000000 - -

	RAM size:    1924 MB,  # CPU hardware threads:   6
	RAM usage:   1323 MB,  # Benchmark threads:      6

			       Compressing  |                  Decompressing
	Dict     Speed Usage    R/U Rating  |      Speed Usage    R/U Rating
		 KiB/s     %   MIPS   MIPS  |      KiB/s     %   MIPS   MIPS

	22:       5692   502   1102   5538  |      98576   504   1668   8407
	23:       4857   431   1147   4949  |      96575   504   1658   8357
	24:       4589   431   1144   4935  |      94597   503   1650   8303
	25:       5601   527   1213   6396  |      93156   505   1643   8290
	----------------------------------  | ------------------------------
	Avr:             473   1152   5454  |              504   1654   8339
	Tot:             489   1403   6897


* openssl speed sha256 aes-128-cbc rsa2048
	Doing sha256 for 3s on 16 size blocks: 9658979 sha256's in 2.99s
	Doing sha256 for 3s on 64 size blocks: 7291386 sha256's in 3.00s
	Doing sha256 for 3s on 256 size blocks: 4299091 sha256's in 2.99s
	Doing sha256 for 3s on 1024 size blocks: 1621935 sha256's in 3.00s
	Doing sha256 for 3s on 8192 size blocks: 238842 sha256's in 2.99s
	Doing sha256 for 3s on 16384 size blocks: 120378 sha256's in 2.99s
	Doing aes-128 cbc for 3s on 16 size blocks: 10267243 aes-128 cbc's in 3.00s
	Doing aes-128 cbc for 3s on 64 size blocks: 2790474 aes-128 cbc's in 2.99s
	Doing aes-128 cbc for 3s on 256 size blocks: 718036 aes-128 cbc's in 3.00s
	Doing aes-128 cbc for 3s on 1024 size blocks: 180829 aes-128 cbc's in 2.99s
	Doing aes-128 cbc for 3s on 8192 size blocks: 22646 aes-128 cbc's in 3.00s
	Doing aes-128 cbc for 3s on 16384 size blocks: 11302 aes-128 cbc's in 2.99s
	Doing 2048 bits private rsa's for 10s: 1400 2048 bits private RSA's in 9.98s
	Doing 2048 bits public rsa's for 10s: 52169 2048 bits public RSA's in 9.98s
	OpenSSL 1.1.1c  28 May 2019
	built on: Wed May 27 19:04:47 2020 UTC
	options:bn(64,64) rc4(char) des(int) aes(partial) blowfish(ptr) 
	compiler: gcc -fPIC -pthread -Wa,--noexecstack -Wall -Wa,--noexecstack -g -O2 -fdebug-prefix-map=/build/openssl-KZTQCo/openssl-1.1.1c=. -fstack-protector-strong -Wformat -Werror=format-security -DOPENSSL_USE_NODELETE -DOPENSSL_PIC -DOPENSSL_CPUID_OBJ -DOPENSSL_BN_ASM_MONT -DSHA1_ASM -DSHA256_ASM -DSHA512_ASM -DKECCAK1600_ASM -DVPAES_ASM -DECP_NISTZ256_ASM -DPOLY1305_ASM -DNDEBUG -Wdate-time -D_FORTIFY_SOURCE=2
	The 'numbers' are in 1000s of bytes per second processed.
	type             16 bytes     64 bytes    256 bytes   1024 bytes   8192 bytes  16384 bytes
	aes-128 cbc      54758.63k    59729.21k    61272.41k    61929.40k    61838.68k    61930.42k
	sha256           51686.84k   155549.57k   368082.71k   553620.48k   654379.15k   659623.13k
			  sign    verify    sign/s verify/s
	rsa 2048 bits 0.007129s 0.000191s    140.3   5227.4

## Mainline Kernel 5.7.0

* linux-image 5.7.0

https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/releases/tag/v1.35

# Testing rt5651

There is support for rt5651 but the trick to make it work is described on Armbian forum.
Alsamixer must set the following:

	amixer set 'HPO L' on
	amixer set 'HPO R' on
	amixer set 'HPOVOL L' on
	amixer set 'HPOVOL R' on
	amixer set 'HPO MIX HPVOL' on
	amixer set 'OUT MIXL DAC L1' on
	amixer set 'OUT MIXR DAC R1' on
	amixer set 'Stereo DAC MIXL DAC L1' on
	amixer set 'Stereo DAC MIXR DAC R1' on


* Check sound devices

	ubuntu@nanopi-m4:~$ aplay -l
	**** List of PLAYBACK Hardware Devices ****
	card 0: realtekrt5651co [realtek,rt5651-codec], device 0: ff890000.i2s-rt5651-aif1 rt5651-aif1-0 [ff890000.i2s-rt5651-aif1 rt5651-aif1-0]
	  Subdevices: 1/1
	  Subdevice #0: subdevice #0
	card 1: ROCKCHIPSPDIF [ROCKCHIP,SPDIF], device 0: ff870000.spdif-dit-hifi dit-hifi-0 [ff870000.spdif-dit-hifi dit-hifi-0]
	  Subdevices: 1/1
	  Subdevice #0: subdevice #0
	card 2: hdmisound [hdmi-sound], device 0: ff8a0000.i2s-i2s-hifi i2s-hifi-0 [ff8a0000.i2s-i2s-hifi i2s-hifi-0]
	  Subdevices: 1/1
	  Subdevice #0: subdevice #0


Playing sound on every device:

**rt5651**
	
	aplay -D sysdefault:CARD=0 /usr/share/sounds/alsa/Front_Right.wav

**SPDIF**

	aplay -D sysdefault:CARD=1 /usr/share/sounds/alsa/Front_Right.wav
	
**hdmi-sound**

	aplay -D sysdefault:CARD=2 /usr/share/sounds/alsa/Front_Right.wav


# Testing GPU and VPU

There is support for GPU (panfrost) and VPU (hantro and rkvdec). Most H264 (1920x1080) works smooth.
You can also build **Kodi**.

If you output decoded video to a framebuffer:

	ffmpeg -hwaccel drm -i Big_Buck_Bunny_1080_10s_30MB.mp4 -pix_fmt bgra -f fbdev /dev/fb0
	

There is a small penalty to be paid for converting the drm_prime format to bgra that increases CPU usage, while output to a drm_prime surface like Kodi does not.

FFmpeg used to test hw decoding: ffmpeg version 4.2.2-Matrix-Alpha1-26-g6029b361f2-Kodi

You can learn more reading Mainline VPU on Armbian forum

# Testing Wifi

Wifi and BT works fine with the latest brcm firmware provided on previous image.
2.4 GHz and 5 GHz has been working without any glitch, read the previous info.


## Mainline Kernel 5.7.0-rc4

* linux-image 5.7.0-rc4 plus brcm firmware update

https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/releases/tag/v1.34


# Panfrost 3D graphics

Panfrost works on linux-image 5.4.0-rc8.
It has been tested with latest Mesa 3D and kmscube.

Mesa 3D: https://gitlab.freedesktop.org/mesa/mesa
Kmscube: https://gitlab.freedesktop.org/mesa/kmscube


![Panfrost Monitoring](https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/raw/master/img/panfrost.png)

Panfrost Output:

	ubuntu@nanopi-m4:~/kmscube$ sudo ./kmscube
	[sudo] password for ubuntu: 
	Using display 0xaaaad69887e0 with EGL version 1.4
	===================================
	EGL information:
	  version: "1.4"
	  vendor: "Mesa Project"
	  client extensions: "EGL_EXT_client_extensions EGL_EXT_device_base EGL_EXT_device_enumeration EGL_EXT_device_query EGL_EXT_platform_base EGL_KHR_client_get_all_proc_addresses EGL_KHR_debug EGL_EXT_platform_wayland EGL_EXT_platform_x11 EGL_MESA_platform_gbm EGL_MESA_platform_surfaceless EGL_EXT_platform_device"
	  display extensions: "EGL_ANDROID_blob_cache EGL_EXT_buffer_age EGL_EXT_image_dma_buf_import EGL_KHR_cl_event2 EGL_KHR_config_attribs EGL_KHR_create_context EGL_KHR_create_context_no_error EGL_KHR_fence_sync EGL_KHR_get_all_proc_addresses EGL_KHR_gl_colorspace EGL_KHR_gl_renderbuffer_image EGL_KHR_gl_texture_2D_image EGL_KHR_gl_texture_3D_image EGL_KHR_gl_texture_cubemap_image EGL_KHR_image EGL_KHR_image_base EGL_KHR_image_pixmap EGL_KHR_no_config_context EGL_KHR_partial_update EGL_KHR_reusable_sync EGL_KHR_surfaceless_context EGL_EXT_pixel_format_float EGL_KHR_wait_sync EGL_MESA_configless_context EGL_MESA_drm_image EGL_MESA_image_dma_buf_export EGL_MESA_query_driver EGL_WL_bind_wayland_display "
	===================================
	OpenGL ES 2.x information:
	  version: "OpenGL ES 2.0 Mesa 20.0.0-devel (git-02d63ee5a4)"
	  shading language version: "OpenGL ES GLSL ES 1.0.16"
	  vendor: "panfrost"
	  renderer: "panfrost"
	  extensions: "GL_EXT_blend_minmax GL_EXT_multi_draw_arrays GL_EXT_texture_format_BGRA8888 GL_OES_compressed_ETC1_RGB8_texture GL_OES_depth24 GL_OES_element_index_uint GL_OES_fbo_render_mipmap GL_OES_mapbuffer GL_OES_rgb8_rgba8 GL_OES_stencil8 GL_OES_texture_3D GL_OES_texture_float GL_OES_texture_float_linear GL_OES_texture_half_float GL_OES_texture_half_float_linear GL_OES_texture_npot GL_OES_vertex_half_float GL_OES_EGL_image GL_OES_depth_texture GL_OES_packed_depth_stencil GL_EXT_texture_type_2_10_10_10_REV GL_OES_get_program_binary GL_APPLE_texture_max_level GL_EXT_discard_framebuffer GL_EXT_read_format_bgra GL_EXT_frag_depth GL_NV_fbo_color_attachments GL_OES_EGL_image_external GL_OES_EGL_sync GL_OES_vertex_array_object GL_EXT_occlusion_query_boolean GL_EXT_texture_rg GL_EXT_unpack_subimage GL_NV_draw_buffers GL_NV_read_buffer GL_NV_read_depth GL_NV_read_depth_stencil GL_NV_read_stencil GL_EXT_draw_buffers GL_EXT_map_buffer_range GL_KHR_debug GL_KHR_texture_compression_astc_ldr GL_OES_required_internalformat GL_OES_surfaceless_context GL_EXT_separate_shader_objects GL_EXT_compressed_ETC1_RGB8_sub_texture GL_EXT_draw_elements_base_vertex GL_EXT_texture_border_clamp GL_KHR_context_flush_control GL_OES_draw_elements_base_vertex GL_OES_texture_border_clamp GL_KHR_no_error GL_KHR_texture_compression_astc_sliced_3d GL_KHR_parallel_shader_compile "
	===================================
	Using modifier ffffffffffffff
	Modifiers failed!
	Using modifier ffffffffffffff
	Modifiers failed!


# How to build 3D Mesa 20.0 for Panfrost

* Update Kernel and packages
* Install dependencies (libdrm, libgbm, wayland protocols, x11 protocols)
* Install meson build

       https://mesonbuild.com/Quick-guide.html

* Build and install

# Kodi on 5.4.0

I have built Kodi with same parameters as for the Mali way, but for some reason it crashed when launched.
It is known to be possible to run Kodi with Panfrost since Kernel 5.2, but something is missing on my Kodi build.
No luck yet.

# Mainline Kernel 5.4.y follow up

* Kernel 5.4.0-rc8 Boot log with hdmi-sound

      https://gist.github.com/avafinger/c0651125c1209b4c8a7920a1595ed239

* Kernel 5.4.0-rc7 Boot log

      https://gist.github.com/avafinger/99108b3255596080490f3b4d0030230d
      
      
* linux-image 5.4.0-rc8 Deb package

      https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/releases/tag/v1.30
  

* linux-image 5.4.0 Deb package

      https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/releases/tag/v1.31
      
      
* linux-image 5.4.1 Deb package      

      https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/releases/tag/v1.32
  
  Wifi enabled generates cpu load and heat, not recommended.
  https://gist.github.com/avafinger/bc9b1a8b0ea4fb482afee088b7c711d1
  
  To activate Wlan0 you need to recompile kernel 5.4.1 with BRCM module enabled and edit /etc/networks/interface and enable wlan

* linux-image 5.4.8 Deb package      

      https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/releases/tag/v1.33


# OS Image

* Image file (8GB SD card) is available here:


	  https://mega.nz/#!YLZhlYJb!uqvCIjpeBoGyfhaNYPJwb67kma7wmGTn5ZObe-CPrb4 
	  (use 7z / zip to unzip and flash into SD card with Win32DiskImager or etcher)


* Flash SD CARD from Linux Box:


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
		sudo apt-get install libgles2-mesa-dev ocl-icd-opencl-dev 


* Install Mali


		sudo dpkg -i --force-all mali-t86x-rk3399-linux-4.4.y_1.0-1.deb

  Ignore the warnings.


* Install enhanced htop:

  You can monitor the health of you RK3399 (CPU Temp, CPU Freq and CPU VCore, enter F2 and add these monitors)

		sudo dpkg -i htop_2.1.1-3_arm64.deb 


* Install tools for benchmarking mali on fbdev:


		sudo dpkg -i glmark2-data_2014.03+git20150611.fa71af2d-0ubuntu5_all.deb 
		sudo dpkg -i glmark2-es2-fbdev_2014.03+git20150611.fa71af2d-0ubuntu5_arm64.deb 


  If everything is Okay, then you can test it:

		
		sudo glmark2-es2-fbdev (test it remotely)

# Wifi

  Install packages:

		sudo apt-get install crda wpasupplicant


  Enable wifi editing the file /etc/network/interfaces and adding:


		allow-hotplug wlan0
		iface wlan0 inet dhcp
			wpa-ssid SID
			#psk="00012345678901234567890"
			wpa-psk afde07531d767050796db24c3d449e26a449c15b98bfaf20148970ec43242078
			dns-nameservers 8.8.8.8 8.8.4.4
			wireless-power off


  Where SID os you AP name and xxxxxxxxx is your encrypted password.
  Generate encrypted password like so:

		wpa_passphrase SSID xxxxxxxxx

  and finally boot and connect to Wifi

# GBM

  We have now fbdev working and with OpenGLES 3.2 (fbdev) we can go further and install GBM (Graphic Buffer Management) libraries
  to be able to use DRM for a non-Desktop environment (no X11/Wayland). VPU has support for DRM/GBM and not for fbdev yet.
   

  There is a DEB package ready to install VPU support. Mali user space for GBM is needed in order to be able to use GL and/or GLES 2/3.
  The nice thing here is that we can have Kodi Media Center to run on NanoPi M4 / NEO / T4 or any other RK3399 if you wish.

  Install the gbm libraries and VPU deb package so we can have Hardware Decoding and HW accelerated display with Mali T86x.


		sudo apt-get install libgbm-dev



  Test if GBM is fully working with **gbm_es2_demo (170 Kb)**  or **kmscube (1.4 Mb)**
  Get file with in https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/releases/tag/v1.7 


		./gbm_es2_demo 
		using card: '/dev/dri/card0': Success
		Using display 0x557241ccf0 with EGL version 1.4
		EGL Version "1.4 Midgard-"r14p0-01rel0""
		EGL Vendor "ARM"
		EGL Extensions "EGL_KHR_partial_update EGL_KHR_image_pixmap EGL_EXT_image_dma_buf_import EGL_KHR_config_attribs EGL_KHR_image EGL_KHR_image_base EGL_KHR_fence_sync EGL_KHR_wait_sync EGL_KHR_gl_colorspace EGL_KHR_get_all_proc_addresses EGL_IMG_context_priority EGL_ARM_pixmap_multisample_discard EGL_KHR_gl_texture_2D_image EGL_KHR_gl_renderbuffer_image EGL_KHR_create_context EGL_KHR_surfaceless_context EGL_KHR_gl_texture_cubemap_image EGL_EXT_create_context_robustness EGL_KHR_cl_event2"
		FPS: 0.002751 
		FPS: 59.027754 
		FPS: 59.989142 
		FPS: 60.001338 
		FPS: 60.008244 
		FPS: 60.007122 
		FPS: 59.988592 
		FPS: 60.013970 
		FPS: 59.988422 
		FPS: 60.008008 
		FPS: 60.001338 
		FPS: 60.000630 
		FPS: 59.995440 
		FPS: 60.001102 
		FPS: 60.006768 
		FPS: 59.995967 
		FPS: 60.001397 
		FPS: 60.007831 


  or kmscube

		./kmscube 
		Using display 0x55b89fca00 with EGL version 1.4
		===================================
		EGL information:
		  version: "1.4 Midgard-"r14p0-01rel0""
		  vendor: "ARM"
		  client extensions: "EGL_EXT_client_extensions EGL_EXT_platform_base EGL_KHR_client_get_all_proc_addresses EGL_KHR_platform_gbm EGL_MESA_platform_gbm"
		  display extensions: "EGL_KHR_partial_update EGL_KHR_image_pixmap EGL_EXT_image_dma_buf_import EGL_KHR_config_attribs EGL_KHR_image EGL_KHR_image_base EGL_KHR_fence_sync EGL_KHR_wait_sync EGL_KHR_gl_colorspace EGL_KHR_get_all_proc_addresses EGL_IMG_context_priority EGL_ARM_pixmap_multisample_discard EGL_KHR_gl_texture_2D_image EGL_KHR_gl_renderbuffer_image EGL_KHR_create_context EGL_KHR_surfaceless_context EGL_KHR_gl_texture_cubemap_image EGL_EXT_create_context_robustness EGL_KHR_cl_event2"
		===================================
		OpenGL ES 2.x information:
		  version: "OpenGL ES 3.2 v1.r14p0-01rel0-git(966ed26).2e3fa7564ebca70897f04bd9fb7bc67e"
		  shading language version: "OpenGL ES GLSL ES 3.20"
		  vendor: "ARM"
		  renderer: "Mali-T860"
		  extensions: "GL_ARM_rgba8 GL_ARM_mali_shader_binary GL_OES_depth24 GL_OES_depth_texture GL_OES_depth_texture_cube_map GL_OES_packed_depth_stencil GL_OES_rgb8_rgba8 GL_EXT_read_format_bgra GL_OES_compressed_paletted_texture GL_OES_compressed_ETC1_RGB8_texture GL_OES_standard_derivatives GL_OES_EGL_image GL_OES_EGL_image_external GL_OES_EGL_image_external_essl3 GL_OES_EGL_sync GL_OES_texture_npot GL_OES_vertex_half_float GL_OES_required_internalformat GL_OES_vertex_array_object GL_OES_mapbuffer GL_EXT_texture_format_BGRA8888 GL_EXT_texture_rg GL_EXT_texture_type_2_10_10_10_REV GL_OES_fbo_render_mipmap GL_OES_element_index_uint GL_EXT_shadow_samplers GL_OES_texture_compression_astc GL_KHR_texture_compression_astc_ldr GL_KHR_texture_compression_astc_hdr GL_KHR_texture_compression_astc_sliced_3d GL_KHR_debug GL_EXT_occlusion_query_boolean GL_EXT_disjoint_timer_query GL_EXT_blend_minmax GL_EXT_discard_framebuffer GL_OES_get_program_binary GL_OES_texture_3D GL_EXT_texture_storage GL_EXT_multisampled_render_to_texture GL_OES_surfaceless_context GL_OES_texture_stencil8 GL_EXT_shader_pixel_local_storage GL_ARM_shader_framebuffer_fetch GL_ARM_shader_framebuffer_fetch_depth_stencil GL_ARM_mali_program_binary GL_EXT_sRGB GL_EXT_sRGB_write_control GL_EXT_texture_sRGB_decode GL_KHR_blend_equation_advanced GL_KHR_blend_equation_advanced_coherent GL_OES_texture_storage_multisample_2d_array GL_OES_shader_image_atomic GL_EXT_robustness GL_EXT_draw_buffers_indexed GL_OES_draw_buffers_indexed GL_EXT_texture_border_clamp GL_OES_texture_border_clamp GL_EXT_texture_cube_map_array GL_OES_texture_cube_map_array GL_OES_sample_variables GL_OES_sample_shading GL_OES_shader_multisample_interpolation GL_EXT_shader_io_blocks GL_OES_shader_io_blocks GL_EXT_tessellation_shader GL_OES_tessellation_shader GL_EXT_primitive_bounding_box GL_OES_primitive_bounding_box GL_EXT_geometry_shader GL_OES_geometry_shader GL_ANDROID_extension_pack_es31a GL_EXT_gpu_shader5 GL_OES_gpu_shader5 GL_EXT_texture_buffer GL_OES_texture_buffer GL_EXT_copy_image GL_OES_copy_image GL_EXT_color_buffer_half_float GL_EXT_color_buffer_float GL_EXT_YUV_target GL_OVR_multiview GL_OVR_multiview2 GL_OVR_multiview_multisampled_render_to_texture GL_KHR_robustness GL_KHR_robust_buffer_access_behavior GL_EXT_draw_elements_base_vertex GL_OES_draw_elements_base_vertex "
		===================================


  If the installation is Okay, you will see a spinning 3D cube.


# Kodi Media Center on RK3399

  Kodi has support for GBM (DRM) and can run on our NanoPi M4 setup. Kodi 18-RC5 has been compiled succesfully.
  Building instructions are provided here: https://github.com/xbmc/xbmc/blob/master/docs/README.Linux.md#4-build-kodi

  Tips to build Kodi v18.0 RC5 on RK3399:

  * Install gcc8 and cpp8
  * Install GBM and libdrm on top of fbdev (mali-gbm user space)
  * Install VPU support (rkmpp)
  * Build ffmpeg-rockchip and add the codecs missing
  * Install ffmpeg (rkmpp)
  * Build Kodi

  **If you installed Kodi v18.0 B5 remove it and install Kodi v18.0 rc5 for RK3399**


		sudo apt-get remove --purge kodi-18b5-rk3399-gbm

 
  then install Kodi 18.0 RC5


		sudo dpkg -i kodi-18rc5-rk3399-gbm_1.0-2.deb


Splash screen Kodi 18rc5 on NanoPi M4 (RK3399)
![Kodi 1](https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/raw/master/kodi/sch1.png)

Kodi 18rc5 on NanoPi M4
![Kodi NanoPi M4 1](https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/raw/master/kodi/sch3.png)

Kodi 18rc5 on NanoPi M4 with kernel 4.4.169-rk3399
![Kodi NanoPi M4 2](https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/raw/master/kodi/sch2.png)


Kodi 18rc5 screenshot 1
![Kodi NanoPi M4 2](https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/raw/master/kodi/sch4.png)

Kodi 18rc5 screenshot 2
![Kodi NanoPi M4 2](https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/raw/master/kodi/sch5.png)

Kodi 18rc5 screenshot 3
![Kodi NanoPi M4 2](https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/raw/master/kodi/sch6.png)

Kodi 18rc5 screenshot 4
![Kodi NanoPi M4 2](https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/raw/master/kodi/sch7.png)

Kodi 18rc5 screenshot 5
![Kodi NanoPi M4 2](https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/raw/master/kodi/sch8.png)



Splash screen Kodi 18b5
![Kodi 1](https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/raw/master/kodi/screenshot000.png)

ScreenShot 1
![Kodi 1](https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/raw/master/kodi/screenshot001.png)

ScreenShot 2
![Kodi 1](https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/raw/master/kodi/screenshot002.png)

ScreenShot 3
![Kodi 1](https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/raw/master/kodi/screenshot003.png)

ScreenShot 4
![Kodi 1](https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/raw/master/kodi/screenshot004.png)

ScreenShot 5
![Kodi 1](https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/raw/master/kodi/screenshot005.png)

ScreenShot 6
![Kodi 1](https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/raw/master/kodi/screenshot006.png)


# Release v1.3

  * Kernel 4.4.168
  * Faster boot times (~7 secs)
  * gcc (Ubuntu 8.2.0-1ubuntu2~18.04) 8.2.0
  * All dependencies updated and installed for Kodi Multimedia Theather (18rc3) - RK3399 
  * eDP LCD was removed from the tree, for some reason, EDP-1 is the main output and HDMI-1 is the second monitor
    this can be trouble if you want to install a Graphics Desktop, you get a dual header even if eDP LCD is not attached.
  * Rootfs ready to deploy Kodi Multimedia Center giving your NanoPi M4 / NEO4 a full-blown Media Center (hopefully ;)


  **Instructions:**

  * Download files:



		wget $(curl -s https://api.github.com/repos/avafinger/nanopi-m4-ubuntu-base-minimal/releases | grep -oP '"browser_download_url": "\K(.*)(?=")' | grep v1.3)




  * Flash Image



		sudo ./flash_kodi_sd.sh /dev/sdX (or /dev/mmcblkY) where X is a letter from b,c.. and Y is a number from 0,1..)


# Release v1.4

  * Kernel 4.4.169 (linux-image && kernel headers)
  * The best of BSP and mainline in one kernel


  **Instructions:**

  * Download deb file:




		wget $(curl -s https://api.github.com/repos/avafinger/nanopi-m4-ubuntu-base-minimal/releases | grep -oP '"browser_download_url": "\K(.*)(?=")' | grep v1.4)




  * Install



		sudo dpkg -i linux-image-4.4.169-rk3399_1.0-1.deb
		sudo shutdown -h now (or **sync && sudo reboot** if you are **brave**)



# Release v1.8 (OS Image for eMMC only)

  * Boot from eMMC
  * Kernel 4.4.169 (linux-image && kernel headers)
  * The best of BSP and mainline in one kernel
  * KODI 18.0 RC5


  **Instructions:**

  * boot from SD CARD and with eMMC attached
  * install **parted**:




		sudo apt-get install parted




  * create a temporary directory:



		mkdir -p emmc
		cd emmc



  * Download the files to flash eMMC:




		wget $(curl -s https://api.github.com/repos/avafinger/nanopi-m4-ubuntu-base-minimal/releases | grep -oP '"browser_download_url": "\K(.*)(?=")' | grep v1.8)



    
    Make sure the download is complete, check with md5sum atfer download! (bad SD card or bad USB sdhc writer can corrupt the file contents):

		
		
		0521a81ed44c7274c906ae3d98769bc4  boot_kodi_emmc.tar.gz
		e88855ba0775235475618309381c3759  rootfs_kodi.tar.gz




  * Install (Burn OS Image to eMMC)




		sudo ./flash_kodi_emmc.sh /dev/mmcblk1
		sudo shutdown -h now (remone power and sd card)




     **Boot** without the **sd card**



# Release v1.9

  * Kernel 4.4.170 (linux-image && kernel headers)
  * The best of BSP and mainline in one kernel


  **Instructions:**

  * Download deb file:




		wget $(curl -s https://api.github.com/repos/avafinger/nanopi-m4-ubuntu-base-minimal/releases | grep -oP '"browser_download_url": "\K(.*)(?=")' | grep v1.9)




  * Install



		sudo dpkg -i linux-image-4.4.170-rk3399_1.0-2.deb
		sudo shutdown -h now (or **sync && sudo reboot** if you are **brave**)



# Release v1.10

  * Kernel 4.4.171 (linux-image && kernel headers)
  * Changelog here (if worth upgrade): https://cdn.kernel.org/pub/linux/kernel/v4.x/ChangeLog-4.4.171
  * The best of BSP and mainline in one kernel


  **Instructions:**

  * Download deb file:




		wget $(curl -s https://api.github.com/repos/avafinger/nanopi-m4-ubuntu-base-minimal/releases | grep -oP '"browser_download_url": "\K(.*)(?=")' | grep v1.10)




  * Install



		sudo dpkg -i linux-image-4.4.171-rk3399_1.0-3.deb
		sudo shutdown -h now (or **sync && sudo reboot** if you are **brave**)


# Release v1.11

  * Kernel 4.4.172 (linux-image && kernel headers)
  * support for ov13850 + ov4689 included
  * F2FS code has been touched only, minor fix, need a complete re-write so it is more BSP than Mainline (you have been warned)


  **Instructions:**

  * Download deb file:




		wget $(curl -s https://api.github.com/repos/avafinger/nanopi-m4-ubuntu-base-minimal/releases | grep -oP '"browser_download_url": "\K(.*)(?=")' | grep v1.11)




  * Install



		sudo dpkg -i linux-image-4.4.172-rk3399_1.0-4.deb
		sudo shutdown -h now (or **sync && sudo reboot** if you are **brave**)



# Release v1.13

  * Kernel 4.4.173 (linux-image && kernel headers)
  * modified rfkill-bt
  * modified wifi
  * mainline 4.4.173 patches

  **Instructions:**

  * Download deb file:




		wget $(curl -s https://api.github.com/repos/avafinger/nanopi-m4-ubuntu-base-minimal/releases | grep -oP '"browser_download_url": "\K(.*)(?=")' | grep v1.13)




  * Install

  You need at least 20 Mbytes free on /boot


		sudo dpkg -i linux-image-4.4.173_1.0-5.deb
		sudo shutdown -h now (or **sync && sudo reboot** if you are **brave**)




# Release v1.15

  * Linux Image 4.4.174-rk3399 (linux-image && kernel headers)
  * built with gcc 8.2
  * mainline 4.4.174 patches (https://cdn.kernel.org/pub/linux/kernel/v4.x/ChangeLog-4.4.174)

  **Instructions:**

  * Download deb file:

    https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/releases/tag/v1.15


		wget $(curl -s https://api.github.com/repos/avafinger/nanopi-m4-ubuntu-base-minimal/releases | grep -oP '"browser_download_url": "\K(.*)(?=")' | grep v1.15)




  * Install

  You need at least 20 Mbytes free on /boot


		sudo dpkg -i linux-image-4.4.174-rk3399_1.0-7.deb
		sudo shutdown -h now (or **sync && sudo reboot** if you are **brave**)



# Release v1.18

  * Linux Image 4.4.175-rk3399 (linux-image && kernel headers)
  * built with gcc 7.3
  * CPU freq back to 2 GHz (2.0 / 1.5 Ghz)
  * mainline 4.4.175 patches (https://cdn.kernel.org/pub/linux/kernel/v4.x/ChangeLog-4.4.175)

  **Instructions:**

  * Download deb file:

    https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/releases/tag/v1.18


		wget $(curl -s https://api.github.com/repos/avafinger/nanopi-m4-ubuntu-base-minimal/releases | grep -oP '"browser_download_url": "\K(.*)(?=")' | grep v1.18)




  * Install

  You need at least 20 Mbytes free on /boot


		sudo dpkg -i linux-image-4.4.175-rk3399_1.0-8.deb
		sudo shutdown -h now (or **sync && sudo reboot** if you are **brave**)


# Release v1.19

  * Linux Image 4.4.177-rk3399 (linux-image && kernel headers)
  * built with gcc 7.3
  * CPU freq back to 2 GHz (2.0 / 1.5 Ghz)
  * DRM workaround to run latest Kodi

  **Instructions:**

  * Download deb file:

    https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/releases/tag/v1.19


		wget $(curl -s https://api.github.com/repos/avafinger/nanopi-m4-ubuntu-base-minimal/releases | grep -oP '"browser_download_url": "\K(.*)(?=")' | grep v1.19)




  * Install

  You need at least 20 Mbytes free on /boot


		sudo dpkg -i linux-image-4.4.177-rk3399_1.0-9.deb
		sudo shutdown -h now (or **sync && sudo reboot** if you are **brave**)


# Bluetooth

We are going to set up the BT in an old fashioned way to bypass some limitations and later install a systemd service to boot with BT enabled.
Kernel has been patched to hopefully fix the "timeout" issue with Bluez but still have some issues with hctool.
For this we will use brcm_patchram_plus to load the firmware and turn ON the BT and have a stable BT experience.

  * Install BT service

		
		sudo dpkg -i bluetooth-rk3399_1.0-1.deb
		sudo sync && sudo reboot


     After a reboot you can check if BT is on with:


		hcitool devi
		Devices:
			hci0	CC:4B:73:23:D4:33



    The service should be the last service to be run, if not you get the "timeout" issue and BT will be useless.
    A trick to make BT stable is as follow:

      * Disable the BT service

        	sudo systemctl disable brcm_patchram_plus.service

      * Install our trick to rc.local service that is the last service that gets pulled from systemd
        
        Copy and past each complete command line below:

			sudo printf '%s\n' '#!/bin/bash' 'pulseaudio -D' 'brcm_patchram_plus -d --enable_hci --no2bytes --use_baudrate_for_download --tosleep 200000 --baudrate 1500000 --patchram /system/etc/firmware/bcm4356a2.hcd --enable_lpm /dev/ttyS0 > /tmp/bt.log 2>&1 &' 'exit 0' | sudo tee -a /etc/rc.local
			sudo chmod +x /etc/rc.local
			sync && sudo reboot


	Check with :

			hcitool devi
			Devices:
				hci0	CC:4B:73:23:D4:33
		

  * Pairing a Phone with our NanoPi M4

    Install the packages if not already installed:


		sudo apt-get install rfkill bluez

    Run pulseaudio required to pair with a phone (**if not running!**).


		pulseaudio -D


    If you have not installed pulse and alsa you need to to do it and check if it is working:


		ubuntu@nanopi-m4:~$ ps -e |grep pulse
		  583 ?        00:00:00 pulseaudio


    Check alsamixer and turn on everything:


		alsamixer
		aplay -l
		**** List of PLAYBACK Hardware Devices ****
		card 0: realtekrt5651co [realtek,rt5651-codec], device 0: ff890000.i2s-rt5651-aif1 rt5651-aif1-0 []
		  Subdevices: 0/1
		  Subdevice #0: subdevice #0
		card 1: rockchiphdmi [rockchip,hdmi], device 0: ff8a0000.i2s-i2s-hifi i2s-hifi-0 []
		  Subdevices: 0/1
		  Subdevice #0: subdevice #0


  * Pairing test

		ubuntu@nanopi-m4:~$ sudo bluetoothctl
		[sudo] password for ubuntu: 
		[NEW] Controller CC:4B:73:23:D4:33 nanopi-m4 [default]
		Agent registered
		[bluetooth]# list
		Controller CC:4B:73:23:D4:33 nanopi-m4 [default]
		[bluetooth]# power on
		Changing power on succeeded
		[bluetooth]# agent on
		Agent is already registered
		[bluetooth]# default-agent
		Default agent request successful
		[bluetooth]# scan on
		Discovery started
		[CHG] Controller CC:4B:73:23:D4:33 Discovering: yes
		[NEW] Device 00:17:CA:F7:38:18 Haier HW-W910
		[bluetooth]# pair 00:17:CA:F7:38:18
		Attempting to pair with 00:17:CA:F7:38:18
		[CHG] Device 00:17:CA:F7:38:18 Connected: yes
		Request confirmation
		[Haie1m[agent] Confirm passkey 552791 (yes/no): Request canceled
		[agent] Confirm passkey 552791 (yes/no): Failed to pair: org.bluez.Error.AuthenticationFailed
		[CHG] Device 00:17:CA:F7:38:18 Connected: no
		[bluetooth]# pair 00:17:CA:F7:38:18
		Attempting to pair with 00:17:CA:F7:38:18
		[CHG] Device 00:17:CA:F7:38:18 Connected: yes
		Request confirmation
		[Haie1m[agent] Confirm passkey 053012 (yes/no): yes
		[CHG] Device 00:17:CA:F7:38:18 Modalias: usb:v000Ap0000d0000
		[CHG] Device 00:17:CA:F7:38:18 UUIDs: 00001105-0000-1000-8000-00805f9b34fb
		[CHG] Device 00:17:CA:F7:38:18 UUIDs: 0000110a-0000-1000-8000-00805f9b34fb
		[CHG] Device 00:17:CA:F7:38:18 UUIDs: 0000110c-0000-1000-8000-00805f9b34fb
		[CHG] Device 00:17:CA:F7:38:18 UUIDs: 00001112-0000-1000-8000-00805f9b34fb
		[CHG] Device 00:17:CA:F7:38:18 UUIDs: 00001116-0000-1000-8000-00805f9b34fb
		[CHG] Device 00:17:CA:F7:38:18 UUIDs: 0000111f-0000-1000-8000-00805f9b34fb
		[CHG] Device 00:17:CA:F7:38:18 UUIDs: 0000112f-0000-1000-8000-00805f9b34fb
		[CHG] Device 00:17:CA:F7:38:18 UUIDs: 00001132-0000-1000-8000-00805f9b34fb
		[CHG] Device 00:17:CA:F7:38:18 UUIDs: 00001200-0000-1000-8000-00805f9b34fb
		[CHG] Device 00:17:CA:F7:38:18 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
		[CHG] Device 00:17:CA:F7:38:18 UUIDs: 00001801-0000-1000-8000-00805f9b34fb
		[CHG] Device 00:17:CA:F7:38:18 ServicesResolved: yes
		[CHG] Device 00:17:CA:F7:38:18 Paired: yes
		Pairing successful
		[CHG] Device 00:17:CA:F7:38:18 ServicesResolved: no
		[CHG] Device 00:17:CA:F7:38:18 Connected: no
		[bluetooth]# info
		Missing device address argument
		[bluetooth]# info 00:17:CA:F7:38:18
		Device 00:17:CA:F7:38:18 (public)
			Name: Haier HW-W910
			Alias: Haier HW-W910
			Class: 0x005a020c
			Icon: phone
			Paired: yes
			Trusted: no
			Blocked: no
			Connected: no
			LegacyPairing: yes
			UUID: OBEX Object Push          (00001105-0000-1000-8000-00805f9b34fb)
			UUID: Audio Source              (0000110a-0000-1000-8000-00805f9b34fb)
			UUID: A/V Remote Control Target (0000110c-0000-1000-8000-00805f9b34fb)
			UUID: Headset AG                (00001112-0000-1000-8000-00805f9b34fb)
			UUID: NAP                       (00001116-0000-1000-8000-00805f9b34fb)
			UUID: Handsfree Audio Gateway   (0000111f-0000-1000-8000-00805f9b34fb)
			UUID: Phonebook Access Server   (0000112f-0000-1000-8000-00805f9b34fb)
			UUID: Message Access Server     (00001132-0000-1000-8000-00805f9b34fb)
			UUID: PnP Information           (00001200-0000-1000-8000-00805f9b34fb)
			UUID: Generic Access Profile    (00001800-0000-1000-8000-00805f9b34fb)
			UUID: Generic Attribute Profile (00001801-0000-1000-8000-00805f9b34fb)
			Modalias: usb:v000Ap0000d0000
			RSSI: -82
		[bluetooth]# connect 00:17:CA:F7:38:18
		Attempting to connect to 00:17:CA:F7:38:18
		[CHG] Device 00:17:CA:F7:38:18 Connected: yes
		Connection successful
		[CHG] Device 00:17:CA:F7:38:18 ServicesResolved: yes
		[CHG] Device 00:17:CA:F7:38:18 UUIDs: 00001105-0000-1000-8000-00805f9b34fb
		[CHG] Device 00:17:CA:F7:38:18 UUIDs: 00001108-0000-1000-8000-00805f9b34fb
		[CHG] Device 00:17:CA:F7:38:18 UUIDs: 0000110a-0000-1000-8000-00805f9b34fb
		[CHG] Device 00:17:CA:F7:38:18 UUIDs: 0000110c-0000-1000-8000-00805f9b34fb
		[CHG] Device 00:17:CA:F7:38:18 UUIDs: 00001112-0000-1000-8000-00805f9b34fb
		[CHG] Device 00:17:CA:F7:38:18 UUIDs: 00001116-0000-1000-8000-00805f9b34fb
		[CHG] Device 00:17:CA:F7:38:18 UUIDs: 0000111f-0000-1000-8000-00805f9b34fb
		[CHG] Device 00:17:CA:F7:38:18 UUIDs: 0000112f-0000-1000-8000-00805f9b34fb
		[CHG] Device 00:17:CA:F7:38:18 UUIDs: 00001132-0000-1000-8000-00805f9b34fb
		[CHG] Device 00:17:CA:F7:38:18 UUIDs: 00001200-0000-1000-8000-00805f9b34fb
		[CHG] Device 00:17:CA:F7:38:18 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
		[CHG] Device 00:17:CA:F7:38:18 UUIDs: 00001801-0000-1000-8000-00805f9b34fb
		Authorize service
		[Haie1m[agent] Authorize service 00001108-0000-1000-8000-00805f9b34fb (yes/no): yes
		[Haier HW-W910]# trust 00:17:CA:F7:38:18
		[CHG] Device 00:17:CA:F7:38:18 Trusted: yes
		Changing 00:17:CA:F7:38:18 trust succeeded
		[Haier HW-W910]# info 00:17:CA:F7:38:18
		Device 00:17:CA:F7:38:18 (public)
			Name: Haier HW-W910
			Alias: Haier HW-W910
			Class: 0x005a020c
			Icon: phone
			Paired: yes
			Trusted: yes
			Blocked: no
			Connected: yes
			LegacyPairing: yes
			UUID: OBEX Object Push          (00001105-0000-1000-8000-00805f9b34fb)
			UUID: Headset                   (00001108-0000-1000-8000-00805f9b34fb)
			UUID: Audio Source              (0000110a-0000-1000-8000-00805f9b34fb)
			UUID: A/V Remote Control Target (0000110c-0000-1000-8000-00805f9b34fb)
			UUID: Headset AG                (00001112-0000-1000-8000-00805f9b34fb)
			UUID: NAP                       (00001116-0000-1000-8000-00805f9b34fb)
			UUID: Handsfree Audio Gateway   (0000111f-0000-1000-8000-00805f9b34fb)
			UUID: Phonebook Access Server   (0000112f-0000-1000-8000-00805f9b34fb)
			UUID: Message Access Server     (00001132-0000-1000-8000-00805f9b34fb)
			UUID: PnP Information           (00001200-0000-1000-8000-00805f9b34fb)
			UUID: Generic Access Profile    (00001800-0000-1000-8000-00805f9b34fb)
			UUID: Generic Attribute Profile (00001801-0000-1000-8000-00805f9b34fb)
			Modalias: usb:v000Ap0000d0000
			RSSI: -82
		[Haier HW-W910]# untrust 00:17:CA:F7:38:18
		[CHG] Device 00:17:CA:F7:38:18 Trusted: no
		Changing 00:17:CA:F7:38:18 untrust succeeded
		[Haier HW-W910]# disconnect 00:17:CA:F7:38:18
		Attempting to disconnect from 00:17:CA:F7:38:18
		[CHG] Device 00:17:CA:F7:38:18 ServicesResolved: no
		Successful disconnected
		[CHG] Device 00:17:CA:F7:38:18 Connected: no
		[bluetooth]# remove 00:17:CA:F7:38:18
		[DEL] Device 00:17:CA:F7:38:18 Haier HW-W910
		Device has been removed
		[NEW] Device 00:17:CA:F7:38:18 Haier HW-W910
		[bluetooth]# scan off
		Discovery stopped
		[CHG] Controller CC:4B:73:23:D4:33 Discovering: no
		[CHG] Device 00:17:CA:F7:38:18 RSSI is nil
		[bluetooth]# quit
		Agent unregistered
		[DEL] Controller CC:4B:73:23:D4:33 nanopi-m4 [default]
		ubuntu@nanopi-m4:~$ 

# LibreElec or not LibreElec

  If you want to run Kodi automatically without the need of logging in you can do this:

  * Boot automatically


		 sudo systemctl edit getty@tty1.service

    and copy & paste:

		[Service]
		ExecStart=
		ExecStart=-/sbin/agetty --noissue --autologin ubuntu %I $TERM
		Type=idle


     Save and Exit

  * Run Kodi right after login:


		echo "kodi" >> .profile 

    Then:

		sync && sudo reboot


     **Important**

     For every login, kodi will run. If you login via ssh you get **kodi** on main screen.
     Remember to exit **kodi** if you are going to access the board remotely


# Mainline Kernel on NanoPi M4

  A litle follow-up on the status of Mainline kernel 5.0.0-rc2 on RK3399.

  What works:

  * HDMI
  * Bluetooth
  * USB 2
  * DVFS
  * ethernet


  Some Logs here: https://gist.github.com/avafinger/a8474938b0dfb31e462ad332192b324d

  Mainline kernel 5.0.0-rc3 built with gcc 8.2 
  Some logs: https://gist.github.com/avafinger/05048dd20cef3953559a0bddef8f5930
  
  Boosted oop to 2.0 GHz and 1.5 GHz and board is still stable!
  Results here: https://gist.github.com/avafinger/a8474938b0dfb31e462ad332192b324d

Increase oop to 2.0 / 1.5 GHz **7z b**

![Kodi 1](https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/raw/master/img/mainline_5.0.0-rc2_boosted.png)

# Mainline Kernel 5.0-rc2 (Ubuntu minimal 18.04)

I have provided an OS Image tested on NanoPi M4:

 * rk3399_ubuntu-minimal-mainline-kernel-5-rc2.7z

Download from: https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/releases/tag/v1.12

# Release v1.14 (Experimental)

  * Kernel 5.0.0-rc5 (linux-image && kernel headers)

  **Instructions:**

  * Download deb file:



		wget $(curl -s https://api.github.com/repos/avafinger/nanopi-m4-ubuntu-base-minimal/releases | grep -oP '"browser_download_url": "\K(.*)(?=")' | grep v1.14)



  * Install

  You need at least 19 Mbytes free on /boot


		sudo dpkg -i inux-image-mainline-5.0_1.0-6.deb
		sudo shutdown -h now

 
# Release v1.16 (Experimental)

  * Kernel 5.0.0-rc6-rk3399 (linux-image && kernel headers)

  **Instructions:**

  * Download deb file:



		wget $(curl -s https://api.github.com/repos/avafinger/nanopi-m4-ubuntu-base-minimal/releases | grep -oP '"browser_download_url": "\K(.*)(?=")' | grep v1.16)



  * Install

  You need at least 19 Mbytes free on /boot


		sudo dpkg -i linux-image-mainline-5.0_1.0-7.deb
		sudo shutdown -h now
		Reboot..


# Release v1.17 (Experimental)

  * Kernel 5.0.0-rc7 (linux-image && kernel headers)

  **Instructions:**

  * Download deb file:



		wget $(curl -s https://api.github.com/repos/avafinger/nanopi-m4-ubuntu-base-minimal/releases | grep -oP '"browser_download_url": "\K(.*)(?=")' | grep v1.17)



  * Install

  You need at least 19 Mbytes free on /boot


		sudo dpkg -i linux-image-mainline-5.0_1.0-8.deb
		sudo shutdown -h now
		Reboot..


# Release v1.20 (Experimental)

  * Kernel 5.0.3 (linux-image && kernel headers)

  **Instructions:**

  * Download deb file:



		wget $(curl -s https://api.github.com/repos/avafinger/nanopi-m4-ubuntu-base-minimal/releases | grep -oP '"browser_download_url": "\K(.*)(?=")' | grep v1.20)



  * Install

  You need at least 20 Mbytes free on /boot


		sudo dpkg - i linux-image-mainline-5.0_1.0-9.deb
		sudo shutdown -h now
		Reboot..


# Release v1.21 (Experimental)

  * Kernel 5.1-rc1 (linux-image && kernel headers)

  **Instructions:**

  * Download deb file:



		wget $(curl -s https://api.github.com/repos/avafinger/nanopi-m4-ubuntu-base-minimal/releases | grep -oP '"browser_download_url": "\K(.*)(?=")' | grep v1.21)



  * Install

  You need at least 20 Mbytes free on /boot


		sudo dpkg - i linux-image-mainline-5.1_1.0-10.deb
		sudo shutdown -h now
		Reboot..

  7z b

		7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
		p7zip Version 16.02 (locale=C.UTF-8,Utf16=on,HugeFiles=on,64 bits,6 CPUs LE)
		
		LE
		CPU Freq:  1938  1989  1989  1989  1989  1989  1989  1989  1989
		
		RAM size:    1989 MB,  # CPU hardware threads:   6
		RAM usage:   1323 MB,  # Benchmark threads:      6
		
		                       Compressing  |                  Decompressing
		Dict     Speed Usage    R/U Rating  |      Speed Usage    R/U Rating
		         KiB/s     %   MIPS   MIPS  |      KiB/s     %   MIPS   MIPS
		
		22:       3882   357   1058   3777  |      98473   528   1591   8398
		23:       4318   403   1092   4400  |     101357   532   1647   8770
		24:       5381   479   1207   5786  |      98415   527   1638   8638
		25:       4924   462   1216   5623  |      97324   530   1633   8661
		----------------------------------  | ------------------------------
		Avr:             425   1143   4896  |              530   1627   8617
		Tot:             477   1385   6757



  lsmod

		Module                  Size  Used by
		brcmfmac              225280  0
		rockchipdrm           118784  1
		brcmutil               16384  1 brcmfmac
		cfg80211              327680  1 brcmfmac
		analogix_dp            36864  1 rockchipdrm
		dw_hdmi                32768  1 rockchipdrm
		dw_mipi_dsi            20480  1 rockchipdrm
		drm_kms_helper        180224  4 dw_mipi_dsi,rockchipdrm,dw_hdmi,analogix_dp
		realtek                20480  1
		hci_uart               49152  0
		drm                   425984  6 drm_kms_helper,dw_mipi_dsi,rockchipdrm,dw_hdmi,analogix_dp
		btbcm                  16384  1 hci_uart
		bluetooth             335872  23 hci_uart,btbcm
		dwmac_rk               28672  0
		stmmac_platform        20480  1 dwmac_rk
		crct10dif_ce           16384  1
		stmmac                135168  2 stmmac_platform,dwmac_rk
		phy_rockchip_pcie      16384  0
		ecdh_generic           24576  2 bluetooth
		rfkill                 28672  4 bluetooth,cfg80211
		drm_panel_orientation_quirks    20480  1 drm
		rtc_rk808              16384  1
		pcie_rockchip_host     20480  0
		rockchip_saradc        16384  0
		rockchip_thermal       24576  0
		ip_tables              32768  0
		x_tables               36864  1 ip_tables
		ipv6                  393216  26


  Bootlog:

 	https://gist.github.com/avafinger/b87a07bf056c2d26b576f71e864ad30d


# Release v1.22 (Experimental)

  * Kernel 5.1-rc2 (linux-image && kernel headers)

  **Instructions:**

  * Download deb file:



		wget $(curl -s https://api.github.com/repos/avafinger/nanopi-m4-ubuntu-base-minimal/releases | grep -oP '"browser_download_url": "\K(.*)(?=")' | grep v1.22)



  * Install

  You need at least 20 Mbytes free on /boot


		sudo dpkg - i linux-image-mainline-5.1_1.0-10.deb
		sudo shutdown -h now
		Reboot..


* Note:
  Install this linux-image on OS **5.y** only and not on 4.4


# Mainline Kernel 5.1-rc6 - Release 1.23 (experimental)

  * Bootlog & modules


	https://gist.github.com/avafinger/12c7ba931eec5972c7cfb19af0fa326a



  * Kernel 5.1-rc6 (linux-image && kernel headers)

  **Instructions:**

  * Download deb file:



		wget $(curl -s https://api.github.com/repos/avafinger/nanopi-m4-ubuntu-base-minimal/releases | grep -oP '"browser_download_url": "\K(.*)(?=")' | grep v1.23)


  * Install

  You need at least 20 Mbytes free on /boot


		sudo dpkg - i linux-image-mainline-5.1_1.0-11.deb
		sudo shutdown -h now
		Reboot..


# Mainline Kernel 5.2.0

Mainline kernel 5.2 has been released, here is what you can expect:

  * DVFS works
  * BT works
  * Wifi (in progress - almost)
  * Gbps
  
Bootlog: https://gist.github.com/avafinger/97d7faea424e386219ea4193a787d3b5

DVFS
![DVFS](https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/raw/master/img/manline_5.2.png)



# Mainline Kernel 5.6.2

Mainline kernel 5.6.2 (status update) has some improvments:

  * DVFS works
  * BT works
  * Wifi works
  * Gbps
  * hdmi
  * hdmi-sound out works
  
i was surprised by some nice improvments on DVFS and Wifi and BT are working together.
The missing pieces are the rt5651 codec and HW decoding.

**7z b**

	ubuntu@nanopi-m4:~$ 7z b

	7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
	p7zip Version 16.02 (locale=C.UTF-8,Utf16=on,HugeFiles=on,64 bits,6 CPUs LE)

	LE
	CPU Freq: 64000000 - - - - - - - -

	RAM size:    1920 MB,  # CPU hardware threads:   6
	RAM usage:   1323 MB,  # Benchmark threads:      6

			       Compressing  |                  Decompressing
	Dict     Speed Usage    R/U Rating  |      Speed Usage    R/U Rating
		 KiB/s     %   MIPS   MIPS  |      KiB/s     %   MIPS   MIPS

	22:       5049   450   1092   4912  |      98605   505   1665   8409
	23:       5796   522   1131   5906  |      96652   506   1652   8363
	24:       5369   497   1161   5773  |      94737   504   1649   8315
	25:       5838   550   1212   6666  |      93054   507   1633   8281
	----------------------------------  | ------------------------------
	Avr:             505   1149   5814  |              506   1650   8342
	Tot:             505   1399   7078

  
Bootlog: https://gist.github.com/avafinger/eb14cc0d7fde87223e3c8fa7766ac238


# Build Mainline Kernel on NanoPi M4 (**on board**)

  Requirements:

  * 16 GB sd card minimum
  * Pre-built **Mainline OS Image (This is important!)**
  * Mainline Kernel from kernel.org to build


  Instructions:

  * login into NanoPi M4

  * create directory

		mkdir -p linux
		cd linux  

  * grab the latest kernel: https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/refs/tags

		wget https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/snapshot/linux-5.2.tar.gz
		tar -xvpzf linux-5.2.tar.gz
		cd linux-5.2

  * Build

		make  defconfig
		#make  menuconfig (if you want to add or change kernel modules)
		make  oldconfig
		make -j6 INSTALL_MOD_PATH=output Image 
		make -j6 INSTALL_MOD_PATH=output dtbs
		make -j6 INSTALL_MOD_PATH=output modules
		make -j6 INSTALL_MOD_PATH=output modules_install

  * Install

		export KV=$(strings ./arch/arm64/boot/Image |grep "Linux version"|awk '{print $3}')
		sudo cp -fv ./arch/arm64/boot/Image /boot/Image_${KV}
		sync
		sudo cp -vfr ./output/* /
		sync
		sudo cp -vf arch/arm64/boot/dts/rockchip/rk3399-nanopc-t4.dtb /boot/rk3399-nanopc-t4.dtb_${KV}
 		sudo cp -vf arch/arm64/boot/dts/rockchip/rk3399-nanopi-m4.dtb /boot/rk3399-nanopi-m4.dtb_${KV}
                sync


  * Make it current kernel

		cd /boot
		sudo ln -sf Image_${KV} Image
		sudo ln -sf rk3399-nanopc-t4.dtb_${KV} dtb
		sudo ln -sf rk3399-nanopi-m4.dtb_${KV} dtb
		cd ${KVD}
		sync

  * Reboot

		sudo shutdown -h now (remove power for 30 secs)
		**Boot** with your new kernel

# Building KODI 19

Instructions to build Kodi 19.0 ALPHA1

  * Upgrade to Kernel 4.4.177-rk3399 or use the latest Image i have provided (RAW Image)
  * Install all dependencies
  * Remove any Previous Installed Kodi.
  
KODI 19.0 ALPHA1
![Kodi 1](https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/raw/master/kodi_19.png)

KODI 19.0 ALPHA1 - mali
![Kodi 2](https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/raw/master/kodi_mali.png)

KODI 19.0 ALPHA1 - Web Inteerface Config
![Kodi 3](https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/raw/master/kodi_web.png)

KODI 19.0 ALPHA1 - system
![Kodi 4](https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/raw/master/kodi_system.png)


**Install dependencies if not already installed, add or change if desired:**

    sudo apt-get install autoconf automake autopoint gettext autotools-dev cmake curl default-jre gawk gcc g++ cpp gdc gperf     libasound2-dev libass-dev libavahi-client-dev libavahi-common-dev libbluetooth-dev libbluray-dev libbz2-dev libcdio-dev     libcec-dev libp8-platform-dev libcrossguid-dev libcurl4-openssl-dev libcwiid-dev libdbus-1-dev libegl1-mesa-dev libenca-     dev libflac-dev libfontconfig1-dev libfmt-dev libfreetype6-dev libfribidi-dev libfstrcmp-dev libgcrypt20-dev libgif-dev     libgles2-mesa-dev libglew-dev libglu1-mesa-dev libgnutls28-dev libgpg-error-dev libiso9660-dev libjpeg-dev liblcms2-dev     liblirc-dev libltdl-dev liblzo2-dev libmicrohttpd-dev libmysqlclient-dev libnfs-dev libogg-dev libomxil-bellagio-dev         libpcre3-dev libplist-dev libpng-dev libpulse-dev libsmbclient-dev libsqlite3-dev libssl-dev libtag1-dev libtiff5-dev       libtinyxml-dev libtool libudev-dev libva-dev libvdpau-dev libvorbis-dev libxkbcommon-dev libxmu-dev libxrandr-dev           libxslt1-dev libxt-dev netcat lsb-release nasm python-dev python-pil python-minimal rapidjson-dev swig unzip uuid-dev       yasm zip zlib1g-dev

**Build the Kodi on-board**
    
    mkdir -p kodi
    cd kodi
    mkdir -p kodi-build
    git clone https://github.com/xbmc/xbmc kodi
    cd kodi
    sudo make -C tools/depends/target/crossguid PREFIX=/usr
    sudo make -C tools/depends/target/flatbuffers PREFIX=/usr
    sudo make -C tools/depends/target/libfmt PREFIX=/usr
    cd ../kodi-build
    cmake ../kodi -DCMAKE_INSTALL_PREFIX=/usr/local -DCORE_PLATFORM_NAME=gbm -DGBM_RENDER_SYSTEM=gles
    cmake --build . -- VERBOSE=0 -j4
    sudo make install
    cd ../kodi
    sudo make -j4 -C tools/depends/target/binary-addons PREFIX=/usr/local
    
**Testing**

    kodi


**Pre-built Kodi 19 RK3399**

* Latest rockchip update

      https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/releases/tag/1.24

# Fix for memory leak and random crahes

Kernel 4.4.177 fix
https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/releases/tag/v1.25


# nanopi-m4-ubuntu-base-minimal 19.10 development

Deploying Ubuntu 19.10 Eoan Ermine (development branch)

	Welcome to Ubuntu Eoan Ermine (development branch) (GNU/Linux 5.3.0-rc5-rk3399 aarch64)

	 * Documentation:  https://help.ubuntu.com
	 * Management:     https://landscape.canonical.com
	 * Support:        https://ubuntu.com/advantage

	Last login: Wed Aug 21 23:13:19 2019
	ubuntu@nanopi-m4:~$ 


* Info

		DISTRIB_ID=Ubuntu
		DISTRIB_RELEASE=19.10
		DISTRIB_CODENAME=eoan
		DISTRIB_DESCRIPTION="Ubuntu Eoan Ermine (development branch)"


* memory usage kernel 4.4:

			      total        used        free      shared  buff/cache   available
		Mem:           1926          54        1782           8          90        1794
		Swap:             0           0           0

* memory usage kernel 5.3 (ssh):

			      total        used        free      shared  buff/cache   available
		Mem:           1985          78        1715           8         191        1826
		Swap:             0           0           0


* gcc dev tools

		gcc (Ubuntu 9.2.1-2ubuntu1) 9.2.1 20190819
		Copyright (C) 2019 Free Software Foundation, Inc.
		This is free software; see the source for copying conditions.  There is NO
		warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.


# Mainline Linux Kernel 5.3.0-rc7

Bootlog: https://gist.github.com/avafinger/84aa9fac1c810765ec84844cb0da94b6

* Flash Image to SD CARD

      https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/releases/tag/v1.27

**Compiled with gcc 9.2.1*

Bootlog: https://gist.github.com/avafinger/5d2e7586b4b10cb45a8a97f9d33d093b

# Mainline Linux Kernel 5.3.1

Bootlog: https://gist.github.com/avafinger/28d976dbe48bc92580efba3fffc37078

* Linux-image

      https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/releases/tag/v1.28


# Mainline Linux Kernel 5.4.0-rc4

  Bootlog: https://gist.github.com/avafinger/0d3d90ad478fb3457707b9652c9710ea

  * Linux-image

        https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/releases/tag/v1.29
      

   * 7z b
   
         7z b burning test
         
         alex@svn:~$ ssh ubuntu@192.168.254.100
         ubuntu@192.168.254.100's password: 
         Welcome to Ubuntu 19.10 (GNU/Linux 5.4.0-rc4 aarch64)
         
          * Documentation:  https://help.ubuntu.com
          * Management:     https://landscape.canonical.com
          * Support:        https://ubuntu.com/advantage
         
         Last login: Tue Oct 22 21:06:53 2019 from 192.168.254.253
         ubuntu@nanopi-m4:~$ 7z b
            
         7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
         p7zip Version 16.02 (locale=C.UTF-8,Utf16=on,HugeFiles=on,64 bits,6 CPUs LE)
         
         LE
         CPU Freq: - - - - - - - - -
         
         RAM size:    1986 MB,  # CPU hardware threads:   6
         RAM usage:   1323 MB,  # Benchmark threads:      6
         
                                Compressing  |                  Decompressing
         Dict     Speed Usage    R/U Rating  |      Speed Usage    R/U Rating
                  KiB/s     %   MIPS   MIPS  |      KiB/s     %   MIPS   MIPS
         
         22:       5165   471   1067   5025  |     103265   533   1652   8807
         23:       4807   447   1096   4898  |     100202   531   1633   8670
         24:       3885   373   1119   4178  |      99252   533   1633   8712
         25:       5253   498   1203   5998  |      94648   518   1626   8423
         ----------------------------------  | ------------------------------
         Avr:             447   1122   5025  |              529   1636   8653
         Tot:             488   1379   6839
         ubuntu@nanopi-m4:~$ 


![7z b stress](https://github.com/avafinger/nanopi-m4-ubuntu-base-minimal/raw/master/img/rk3399_htop.png)

# Mainline Bluetooth

  Mailine Bluetooth works out-of-the-box on 5.3.y and 5.4.y

  Here is how to play music with a Bluetooth speaker like JBL CHARGE3
  
  * Install Bluetooth stack
  
        sudo apt-get update
        sudo apt-get dist-upgrade
        sudo apt-get install dialog alsa-utils libasound2 alsa-base
        sudo apt-get install bluez bluez-tools libbluetooth-dev
        sudo apt-get install pulseaudio pulseaudio-utils pavucontrol pulseaudio-module-bluetooth


  * Find the BT

        ubuntu@nanopi-m4:~$ hciconfig -a
        hci0:	Type: Primary  Bus: UART
	    BD Address: CC:4B:73:23:D4:33  ACL MTU: 1021:8  SCO MTU: 64:1
	    UP RUNNING PSCAN 
	    RX bytes:3640 acl:0 sco:0 events:418 errors:0
	    TX bytes:64284 acl:0 sco:0 commands:418 errors:0
	    Features: 0xbf 0xfe 0xcf 0xfe 0xdb 0xff 0x7b 0x87
	    Packet type: DM1 DM3 DM5 DH1 DH3 DH5 HV1 HV2 HV3 
	    Link policy: RSWITCH SNIFF 
	    Link mode: SLAVE ACCEPT 
	    Name: 'nanopi-m4'
	    Class: 0x0c0000
	    Service Classes: Rendering, Capturing
	    Device Class: Miscellaneous, 
	    HCI Version: 4.1 (0x7)  Revision: 0x210a
	    LMP Version: 4.1 (0x7)  Subversion: 0x230f
	    Manufacturer: Broadcom Corporation (15)
	    
  * Configure ALSA	    

        cat /etc/asound.conf
        pcm.!default {
            type plug
            slave {
                pcm "hw:1,0"
            }
        }
        		
        ctl.!default {
           type hw
           card 1
        } 


  * Check for Pulse (must be running)

        ubuntu@nanopi-m4:~$ rfkill list all
        0: hci0: Bluetooth
	    Soft blocked: no
	    Hard blocked: no

        ubuntu@nanopi-m4:~$ ps -e|grep pulse
        603 ?        00:00:00 pulseaudio

    if Pulse is not running, install and run:
  
         pulseaudio --start
       
  
  * Find, pair and connect with CHARGE3       

        sudo bluetoothctl
        power on
        agent on
        scan on
        scan off
        trust 8E:06:78:D2:E1:3C
        pair 8E:06:78:D2:E1:3C
        connect 8E:06:78:D2:E1:3C
        exit

  
  * Play music
  
        sudo apt-get install sox libsox-fmt-all
        play music.mp3

    
    I played this: https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3
    
        play SoundHelix-Song-1.mp3 
        
        SoundHelix-Song-1.mp3:
        
        File Size: 8.95M     Bit Rate: 192k
          Encoding: MPEG audio    Info: 2009
          Channels: 2 @ 16-bit   
        Samplerate: 44100Hz      
        Replaygain: off         Artist: SoundHelix
        Duration: 00:06:12.73  
        
        In:9.39% 00:00:35.02 [00:05:37.71] Out:1.54M [!=====|=====!] Hd:0.1 Clip:0 
    
    
# Build instructions

  * Pre-requisites

    
        sudo apt-get install build-essential git bison flex bc device-tree-compiler dh-make bzr-builddeb p7zip-full
        sudo apt-get install libssl-dev rsync wget

  * Build 

    Get your kernel or use the linus kernel (stable kernel 5.3.1 on **Ubuntu 19.10**):

        mkdir -p linux
        cd linux/
        wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.3.1.tar.xz
        tar -xf linux-5.3.1.tar.xz
        cd linux-5.3.1/

    Build:

        export KVD=$PWD
        make  distclean
        rm -rf ./output/*
        make  mrproper
        make  defconfig
        make  menuconfig # enable,diable,add,remove driver(s) or configuration
        make  oldconfig
        make -j6 INSTALL_MOD_PATH=output Image 
        make -j6 INSTALL_MOD_PATH=output dtbs
        make -j6 INSTALL_MOD_PATH=output modules
        make -j6 INSTALL_MOD_PATH=output modules_install
        export KV=$(strings ./arch/arm64/boot/Image |grep "Linux version"|awk '{print $3}')
        make INSTALL_HDR_PATH=output/usr/src/linux-headers-${KV} headers_install

    Install:

        sudo cp -vfr ./output/usr/* /usr/
        sudo cp -vfr ./output/lib/* /usr/lib
        sync
        sudo cp -vf arch/arm64/boot/dts/rockchip/rk3399-nanopc-t4.dtb /boot/rk3399-nanopc-t4.dtb_${KV}
        sudo cp -vf arch/arm64/boot/dts/rockchip/rk3399-nanopi-m4.dtb /boot/rk3399-nanopi-m4.dtb_${KV}
        sync
        cd /boot
        sudo ln -sf Image_${KV} Image
        sudo ln -sf rk3399-nanopc-t4.dtb_${KV} dtb
        sudo ln -sf rk3399-nanopi-m4.dtb_${KV} dtb
        cd $KVD
        sync

    Reboot with:
 
        sudo shutdown -h now

    Remove power for 15 secs and power again!

    **PS: it takes about 45 min to complete, depends on your SD CARD and how you cool your board!!!**

You can also monitor the health of your board with htop 2.2.2 from here:

    https://github.com/avafinger/htop_2.2.2

# Fix Wifi on Mainline Kernels

Until recently i was able to use Wifi or Bluetooth but not both together. This has been fixed following some simple instructions.

I used the old way (the ugly way) to set the Wifi and Ethernet, editing the file **/etc/network/interfaces** instead of **netplan**, the recommended way which i found a bit hard to configure.

For some reason, the wifi works smooth with **power save off** in **2.4 GHz** and **5 GHz**, and now Bluetooth can work together.
Setting the **wireless-power off** in  **/etc/network/interfaces** does not work but using **iw** works:

	sudo apt-get update
	sudo apt-get install iw
	sudo iw dev wlan0 set power_save off

Now Wifi and Bluetooth work smooth.

Also for a better performance you can update the firmware from here (which is more up-to-date):

	https://people.linaro.org/~manivannan.sadhasivam/rock960_wifi/
	

You can add the power save command at boot time adding the command to **rc.local** file:

	#!/bin/bash
	iw dev wlan0 set power_save off
	exit 0

You might need to add the rc.local service if you have not done it yet before you edit the rc.local file above;

	sudo systemctl status rc-local
	sudo systemctl enable rc-local
	printf '%s\n' '#!/bin/bash' 'exit 0' | sudo tee -a /etc/rc.local
	sudo chmod +x /etc/rc.local
	sudo systemctl enable rc-local

Check for SSID(s):

	sudo iw dev wlan0 scan | egrep "signal:|SSID:" | sed -e "s/\tsignal: //" -e "s/\tSSID: //" | awk '{ORS = (NR % 2 == 0)? "\n" : " "; print}' | sort

Enjoy the maximum performance of both Wifi and BT.


# Credits

  * FriendlyElec (for the sample)
  * Amanda Finger (Expertise on Kodi and help building)
  * Armbian (technical informations)
