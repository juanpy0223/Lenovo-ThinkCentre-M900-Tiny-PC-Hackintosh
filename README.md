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

From Windows:

I followed [Dortania's OpenCore Guide](https://dortania.github.io/)
 and did Port Mapping from Windows https://www.reddit.com/r/hackintosh/comments/ta1ef4/guide_easy_usb_mapping_with_usbtoolbox_on_windows/?utm_medium=android_app&utm_source=share 

please add your own PLATFORM INFO, with https://github.com/corpnewt/GenSMBIOS... Im using iMac17,1 SMBIOS. 

After Installing Catalina:

Last I followed [OC Little Translated by 5T33Z0](https://github.com/5T33Z0/OC-Little-Translated)


# My Specs:

- Model Make: Lenovo Thinkcentre M900 Tiny PC

- CPU/GPU: Intel i7-6700t/Intel HD Graphics 530 (2 DisplayPort + 1 VGA port) only 2 display ports work on macOS.

- DRAM: 20GB (16GB+4GB) 2133Mhz DDR4 So-Dimm

- Storage: 1TB Crucial P5 2280 (nvme slot) (MacOS-Catalina, Big Sur and Windows 10 64bit 21H2)... 
I used this guide to install win10 (https://www.youtube.com/watch?v=ztxHRGdX0Sw&t=3s)

- Connections: I219-LM Intel Ethernet - no wifi

- 6x (2 Front+4 Rear) USB 3.1 Gen1 (one front AlawysOn)

- I replaced the original heatsink and fan cooler with the ID-Cooling SE-214-xt (now idle temp is 30c and full load 50c)... 
followed this guide https://hackaday.com/2022/03/13/minipc-surgery-makes-it-50-cooler/ 

![IMG_20220723_184451](https://user-images.githubusercontent.com/74636450/180625287-2f2fdefe-3229-4fc6-9710-48e455dea7ed.jpg)
![IMG_20220722_214346](https://user-images.githubusercontent.com/74636450/180625300-567f6312-f886-42ba-a08c-b04dd04a3306.jpg)


# What works on MacOS:


- Graphics Full Aceleration, (Plug.aml, Lilu.kext, VirtualSMC.kext, WhateverGreen.kext,SSDT-MEM2.aml)

- A type USB USB Port Map kext - (USB Port Map kext + SSDT-USBX-.aml-for USB power)

- Power Management (SSDT-PLUG.aml, CPUFriend+CPUFriendDataProvider kexts)

- Conexion LAN (IntelMausi.kext)

- Audio: Monitor Speakers via DisplayPort and LineOut to Headphones ¨Front Jack¨ (AppleAlc.kext alcid13 + HPET.aml + IRQ and IPIC Conflict patch)


# There are other patches for making macOS believe that os running on a real iMac, like DMAC, MCHC, MEM2, PCMR, and so on.


# Note: I will dedicate some time to trying to fix sleep issue (display not working after sleep)


# This is a WORK IN PROGRESS, please let me know any problem you may have, or any suggestions.




I hope this information helps.... if you have the same model...
