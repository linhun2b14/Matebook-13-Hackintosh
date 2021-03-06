# Huawei Matebook 13 Hackintosh Mojave LAST UPDATE 2019/08/04
## I've spent the majority of my spare time on this project, so if you want to support my works consider to make a donation(info at the end of the guide). 

**[Youtube video](https://www.youtube.com/watch?v=bGCNpHCqUcA).** 

**In the next release**
No time to work on it until summer.
Hoping that in this month, some dev finish intel wifi card porting porting, so the project can reach the next level.
- Catalina??
- Wifi card support??


**Changelog**
* **2019/08/04**
- With SSDT-USB patch the system now have right usb injection(better battery life)
- To get a better battery life use "One command CPU Friend"(end of the guide)

* **2019/07/28**
- Fixed audio, headphone jack(Can select in setting between internal speaker and headphones)


* **2019/07/27**
- Fixed brightness shortcut
- Fixed brithtness selector
- Fixed panic at boot with "OSI to XOSI" rename
- Seems fixed audio sommetimes don't work(if happen, you tell me)
- Updated clover to the v2.5k_r5018

* **2019/07/19**
 - Fixed boot problems

* **2019/07/17**
 - Fixed Touchpad
 - Fixed Sensors
 - Fixed Battery detection
 - Polish here and there

* **2019/07/15**
 - Initial release

## I'm not responsible for damage, termonuclear war or pregnant wife. Sorry for my bad english, i've done my best 
This guide is designed for Huawei Matebook 13.
After some night spent on it, almost all works(except WiFi).
In the next days I will try to mod bios to read broadcom WiFi card


nb. Many thanks to tonymac forum



**Whats work**
* Graphics accelaration
* Battery stats 
* trackpad
* sensors 
* audio
* almost all exept thing listed in "bugs"

**Bugs:**
* Bluetooth and Wifi wont working (nb: wifi card is replaceble but whitelisted in bios, so we need a mod one to read a non intel wifi card) Bluetooth work only on hot boot from linux or windows
* Camera(maybe not compatible with osx) will try
* Some problems with audio id layouts(config.plist > device > properties), 28 make headphone working(crappy sound) and broke mic, 13 make mic working, but not headphones(i use usb c headphones, or esternal sound card to use 3,5 jack)

**What you need:**
* A working mac(hackinosh or vmware virtual machine are good too)
* Usb hub for the installation(connected on the usb port of huawei original adaptator. If you have a usb type c otg connector you can use it to turn usb c port to usb a)
* Usb drive(al least 8GB)


**Raccomandations:**
* Format SSD to Mac  Mac OS Extended (Journaled)
* Use left usb port or will get errors during installation
* Use a usb hub during installation or a OTG usb C adaptator to use usb c port as usb
* During installation may occur that pc shut down after clover selection for the first two attempt
* Versions with Samsung PM981 NVMe need ssd to be replaced
* Versions with Western Digital nvme work out of the box 

**Installation**
* Download Osx from the appstore with a existing mac/hackintosh or with a vmware virtual machine(google is your friend)
* Format a usb drive, Mac OS(Journaled) with gpt partition scheme and rename it in "osx" (at least 8GB)
* Build the usb installer with this command:
> sudo "/Applications/Install macOS Mojave.app/Contents/Resources/createinstallmedia" --volume  /Volumes/osx --nointeraction 

osx is the name of the usb drive, so if you use different name you have to change it in the path of the command
* Install Clover [Download Clover v2.5k r5018](https://sourceforge.net/projects/cloverefiboot/files/Installer/Clover_v2.5k_r5018.zip/download)
* Choose Usb drive as destination and click on the "Ad hoc" button,
select "Clover for UEFI booting only" and continue the installation.
* After Clover installation by default EFI partition of usb drive should be mounted, if not, you should mount it manually using this command 
> sudo diskutil mount disk2s1

'disk2s1' may change according to your partition scheme. To know which is the partition you need to mount(EFI of usb drive), use this other command

>diskutil list

Once you have access of your usb drive EFi partition, copy the content of **CloverInstallation.zip** in each corrisponding folder of your EFI/CLOVER partiton(delete the previus content)
* Now the installation should go on with no problems(If your screen turn off after Clover selection) just do another 2/3 attempts(system will reboot during installation, select the mac os HDD from clover selection in bootloader). Remember to format your drive Mac OS(Journaled) in disk utility before installation, or the process will fail.

**Post Installation**
* After boot, install same clover used in the installation, but this time on HDD
* Extract **CloverPost.zip** from my repository and copy the content in each EFI/Clover like you did for the installation process, but this time on the HDD
* Extract the **Kext.zip** in the desktop and type this commands to install kext in Library/Extensions

> cd Desktop/kexts 

> sudo cp -R *.kext /Library/Extensions/ 

Now we need to rebuild kernel cache, so launch this other command

> sudo kextcache -i /

* Disable hibernation by launching this command one at time
> sudo pmset -a hibernatemode 0 

> sudo rm /var/vm/sleepimage 

> sudo mkdir /var/vm/sleepimage 

> sudo pmset -a standby 0 

> sudo pmset -a autopoweroff 0 

* Reboot and enjoy your Hackintosh(Some thing maybe wont work perfect, this is a continuos work in progress, so read carefully before complain"


**Optimizations**
* If some apps has problem starting, try add this bootflags 
> shikigva=32

> shiki-id=Mac-7BA5B2D9E42DDD94

* Remove red badge(1) of setting icon on the dock when updates are available

>defaults write com.apple.systempreferences AttentionPrefBundleIDs 0

>killall Dock


*To get better battery life, you can use cpu friend kext 
run this command 
> bash -c "$(curl -fsSL https://raw.githubusercontent.com/stevezhengshiqi/one-key-cpufriend/master/one-key-cpufriend.sh)"
You have to choose in terminal what configuration use, i've choosed 800mhz and maximum power saving. I will generate 2 kext on the desktop that you have to install in "/Library/Extensions" folder.
Thanks to [Stevezhengshiqi OneKey CPU Friend](https://github.com/stevezhengshiqi/one-key-cpufriend).



I'm working on this project to get almost fully functional hackintosh build on this laptop
if you want to help me or join in project you can write me an email: edoardo001ct@gmail.com

_**If you want to buy me a beer please click here:**_
**[Buy me a beer](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=2NMM7HN9SJRVE&source=url
).** 

