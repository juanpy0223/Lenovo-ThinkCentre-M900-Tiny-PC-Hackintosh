# Lenovo-ThinkCentre-M900-Tiny-PC-Hackintosh

# Lenovo Thinkcentre M900 Tiny PC OpenCore 0.7.8

 

Tested to clean Install Sierra, Catalina, Big Sur, and Monterey.

Sierra:
![m900tiny sierra 10 12 6](https://user-images.githubusercontent.com/74636450/181305352-69758405-f766-45f1-9ee1-d86e106ebb25.png)

Catalina:
![00 m900tinycatalina](https://user-images.githubusercontent.com/74636450/180625322-7ae9e0b4-417d-449e-a2ec-f17248c5d5e6.png)

Big Sur:
![01 m900tinybigsur2](https://user-images.githubusercontent.com/74636450/180625420-b50c4ef7-e666-4592-85dc-3fc29d6b20ee.png)

Monterey:
![01 m900tinymonterey 2](https://user-images.githubusercontent.com/74636450/180625421-6e476b95-a6d4-4b6a-b095-0a5a4e715df6.png)



# Guides and sources:

- Please add your own PLATFORM INFO, with https://github.com/corpnewt/GenSMBIOS... Im using iMac17,1 SMBIOS. 

# From Windows:

I followed [Dortania's OpenCore Guide](https://dortania.github.io/)
 and did Port Mapping from Windows https://www.reddit.com/r/hackintosh/comments/ta1ef4/guide_easy_usb_mapping_with_usbtoolbox_on_windows/?utm_medium=android_app&utm_source=share 

# After Installing Catalina: (for Catalina and olver versions, Port Mapping is not a must), so its perfect, for doing post-install process...

- Followed Dortania Post-Install - https://dortania.github.io/OpenCore-Post-Install/

- Last I followed [OC Little Translated by 5T33Z0](https://github.com/5T33Z0/OC-Little-Translated)


# My Specs:

- Model Make: Lenovo Thinkcentre M900 Tiny PC

- Bios Version: FWKTBFA

- CPU/GPU: Intel i7-6700t/Intel HD Graphics 530 (2 DisplayPort + 1 VGA port) only 2 display ports work on macOS.

- DRAM: 20GB (16GB+4GB) 2133Mhz DDR4 So-Dimm

- Storage: 1TB Crucial P5 2280 (nvme slot) (MacOS-Catalina, Big Sur and Windows 10 64bit 21H2)... 

I used this guide to install win10 (https://www.youtube.com/watch?v=ztxHRGdX0Sw&t=3s)

- Connections: I219-LM Intel Ethernet - Wifi BCM94360ng Fenvi

- 6x (2 Front+4 Rear) USB 3.1 Gen1 (one front AlawysOn)

- I replaced the original heatsink and fan cooler with the ID-Cooling SE-214-xt (now idle temp is 30c and full load 50c)... 
followed this guide https://hackaday.com/2022/03/13/minipc-surgery-makes-it-50-cooler/ 

![IMG_20220729_124101](https://user-images.githubusercontent.com/74636450/181805961-205c3e1d-2103-4231-8079-558d8e1e3f89.jpg)

![IMG_20220729_124110](https://user-images.githubusercontent.com/74636450/181806073-6989820d-7fc6-4a4d-b015-cceb123fac7a.jpg)


# What works on MacOS:


- Graphics Full Aceleration, (Plug.aml, Lilu.kext, VirtualSMC.kext, WhateverGreen.kext,SSDT-MEM2.aml)

- Type A USB Ports - (USB Port Map kext + SSDT-USBX-.aml-for USB power)

- Power Management (SSDT-PLUG.aml, EC.aml and CPUFriend+CPUFriendDataProvider kexts)

- Conexion - LAN (IntelMausi.kext) ; Wifi+Bluetooth no kext required, only mapped BT usb port as internal (255)

- Audio: Monitor Speakers via DisplayPort and LineOut to Headphones ¨Front Jack¨ (AppleAlc.kext+HPET.aml+IRQ and IPIC Conflict patch) - now Also Internal Speaker working with alcid=20


# There are other patches for making macOS believe that os running on a real iMac, like DMAC, MCHC, MEM2, PCMR, and so on.


# Note: I will dedicate some time to trying to fix sleep issue (display not working after sleep)...

# Progress: I went deep into Whatevergreen.kext patching, So I figured out how to send sleep command, ONLY TO IGPU, and make the M900 to go into HALF-SLEEP state, to avoid the tiny pc to get stuck on BLANK MODE
Instead of typing a lot, I will show you My Config on a few pictures... Remember this tiny pc has mobile hardware, so I treated it as a MacMini not a iMac; the LSPCON and hda-gfx=onboard-1 patches, make MacOS believe its a mobile IGPU not a Desktop IGPU
so, when you go to sleep and later press a key or move the mouse, basically the system believes you a CLOSING and/or OPENING the "Laptop".

![00DEVICEPROPERTIES](https://user-images.githubusercontent.com/74636450/181666524-5afc44bc-bddc-411e-a4d5-0bc75f35e26f.png)

![01KEXTS](https://user-images.githubusercontent.com/74636450/181666527-f5951e4d-2df3-4f53-8ca1-bee4b3d78b51.png)

![02BOOT-ARGS](https://user-images.githubusercontent.com/74636450/181666534-a63a1115-1834-4aad-8e52-6f5334ed3e81.png)

![03DORTANIA FIX SLEEP](https://user-images.githubusercontent.com/74636450/181666540-fc3606db-43f1-499d-9d87-05111e72a2b7.png)

-- if you check whatevergreen patching methods, the board controller (0x1912) supports 3 video output ports (2 DP + 1 Dummy which can be HDMI or VGA depending on adapter)... If you change the dummy port definition from Dummy to DP, SLEEP and WAKE happens really fast 2-3 seconds.
Exampl: From Dummy "10 00 00 00" to Display Port "00 04 00 00".

# This way you avoid getting stuck on BLANK SCREEN and Only Fan and CPU are still running, reducing power consumption.



# Lenovo ThinkCentre M900 Tiny Pc CFG lock (MSR 0xE2) fix:

All the following models with BIOS Update - Intel B150 for ThinkCentre M700 Tiny, ThinkCentre M800, M900, M900x Tiny

Bios Version: FWKTBFA (fwjtbfusa) - 05 Jul 2022

This guide will work, only if your Lenovo ThinkCentre tiny pc has this bios version, if not, you will have to update. (It is included on Windows 10 updates), or you can download it from official site.
https://support.lenovo.com/pt/en/downloads/DS105487

# Method: 
- I followed Dortania Post-Install Guide on the topic, with a little variation...

https://dortania.github.io/OpenCore-Post-Install/misc/msr-lock.html#what-is-cfg-lock

The guide helped me find the CFG Lock value for my bios, but no matter how much I searched, I could not find CpuSetup value anywhere, so I knew the Modified GRUB Shell commands, had to be different.

- I first tried the suggested: setup_var_cv CpuSetup 0x197 0x01 0x00, with no luck.

- I tried this: setup_var 0x197 0x00, and it worked. (0x197 is the value for this bios version)
"CFG lock, VarStoreInfo (VarOffset/VarName): 0x197, VarStore: 0x1, QuestionId: 0x87D , Size: 1, Min: 0x0, Max 0x1, Step: 0x0"

- You have to disable Kernel -> Quirks -> AppleCpuPmCfgLock and Kernel -> Quirks -> AppleXcpmCfgLock, on your Config.plist

Now the system has full access to your CPU MSR 0xe2, to controll it and perform better.



# This is a WORK IN PROGRESS, please let me know any problem you may have, or any suggestions.



I hope this information helps.... if you have the same model...
