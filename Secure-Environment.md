<div style="text-align: justify">

# Creating Secure Environment

## Ubuntu 18.04 LTS

### Introduction

If you choose to follow this tutorial make sure you backed up all your data, because you might permanently lose it or damage your hardware while performing some of the steps. Please note that even by following this tutorial you can't be guaranteed absolute safety and should perform your own due diligence.


### Prerequisites



*   Laptop or PC with 64-bit processor, 4GB RAM and Ubuntu, Windows or macOS
*   Pendrive with at least 4GB flash memory where you will burn portable Ubuntu "Live CD"
*   Pendrive with at least 64GB flash memory (USB 3.1) were you will instal full Ubuntu OS


### Steps To Complete



*   Downloading and burning fresh new Ubuntu 18.04 LTS "Live CD" image into 4GB pendrive
*   Booting Ubuntu installer from the 4GB flash pendrive
*   Installing Ubuntu OS into 64GB pendrive and encrypting it

_NOTE: It's recommended that you use a pendrive with at least "up to" 200MB/s read and 150MB/s write speed compatible with USB 3.1 standard. It's essential to use high quality hardware as installing operating system will wear off flash memory and it's usability / user experience will be capped by how fast your flash drive can be._


## Burning Ubuntu 18.04 LTS "Live CD"

To ensure your security it's required that you complete one of the 4 following steps (depending on which operating system you have) so that your seed words are never accessed from the operating system that you are using for everyday tasks, which could contain tracking or malicious software and compromise your seed phrases o other plaintext secrets.

First insert your 4GB flash drive to the USB port and follow one of the 3 tutorials below to create a bootable "Live CD" USB stick that will allow us later to create full Ubuntu installation on your 64GB flash drive.

* If you are using Windows follow **[Create a bootable USB stick on Windows](https://tutorials.ubuntu.com/tutorial/tutorial-create-a-usb-stick-on-windows#0)** 

* If you are using Ubuntu follow **[Create a bootable USB stick on Ubuntu](https://tutorials.ubuntu.com/tutorial/tutorial-create-a-usb-stick-on-ubuntu#0)** 

* If you are using macOS follow **[Create a bootable USB stick on macOS](https://tutorials.ubuntu.com/tutorial/tutorial-create-a-usb-stick-on-macos#0)** 

 Another option (not recommended for security sake) is to use [UNetbootin](https://unetbootin.github.io/) to automatically download and install for you Ubuntu 18.04 "Live CD" ito your 4GB flash memory. Note that if you use this option and you already run ubuntu you might have issues with seeing blank window after starting unetbootin, in such case run following command after installation or downloading binaries: 


```
sudo QT_X11_NO_MITSHM=1 unetbootin
```


After creating a "Live CD" **I highly recommend to physically remove all your hard drives from your PC or laptop before you proceed!** If you can't do it I advise against following this tutorial as sometimes ubuntu installation wizard can override EFI or Boot partition even if you explicitly select advanced options and define that you only want to use partition on your usb stick for "Device for boot loader installation". I repeat, that <span style="text-decoration:underline;">not removing all your hard drives prior to full installation if Ubuntu on your 64GB flash drive might irreversibly corrupt your boot loader</span> regardless of the options you choose (in the installation wizard), to the point where even using [boot-repair](https://help.ubuntu.com/community/Boot-Repair) tool will not help you fix the issue.



## Installing Ubuntu 18.04 LTS

Now after burning of the "Live CD" is complete you need to enter Boot Menu, to do this you have to **restart or turn on and off again** your PC/laptop and and press **F12** during the initial startup screen (NOTE: that key might differ depending on your bios and motherboard manufacturer). Depending on the BIOS manufacturer, a menu may appear. Navigate using arrow keys, select **Flash Drive** (your 4GB flash drive to boot from) and press enter. 

_NOTE: If by mistake you enter BIOS you can also change boot priority by navigating to BOOT tab to give a USB device highest boot sequence priority over the hard drive and then save and restart your machine._ _In some cases you might have to enable option in your BIOS to allow booting from USB devices before you can complete previous step. In such case you might have to refer to your motherboard manufacturer instructions in order to enable this option. (It might for example require setting "Secure Boot Control" to Disabled or switch to "Boot" and set "Launch CSM" to Enabled.)_

Once "console like" looking GNU GRUB bootloader appears Plug your 64GB pendrive and select "Try Ubuntu without installing" (default option that is selected automatically) and you will be then greeted with operational Ubuntu desktop and "Install Ubuntu 18.04.X LTS" icon.

Double-click on the "Install Ubuntu 18.04.X LTS" icon and follow all default options during installation wizard, it's recommended to use "Encrypt the Ubuntu Installation" option but it might not work on all PC's and laptops after installation completes and you might have to try again without. If you took my advice to hearth **to remove all your hard drives** from your machine then you can select "Erase disk and install Ubuntu" option and do not have to worry that you will lose your data. If you didn't you can try to use "Something else" option during installation type step of the wizard and [follow this tutorial](https://linuxhint.com/run-ubuntu-18-04-from-usb-stick/), but I highly **advise against** as it's **not** guaranteed to work and can corrupt your boot partition in irrecoverable way.

After installation is complete you can remove your 4GB "Live CD" flash drive, reboot your machine and press **F12** during the initial startup screen to enter Boot Menu. This time select your 64GB flash drive with full ubuntu installation to boot from. After logging in **you are ready to safely** install any tools, wallets or extract your secrets.



## Foreword

If you have chosen to follow this tutorial to access your private keys and are installing third party software even from trusted sources make sure that for each "wallet" you install or access you create a separate "Secure Environment". If you do not follow this advice you might end up installing malicious software and increase a risk of exposing your secrets.
</div>


