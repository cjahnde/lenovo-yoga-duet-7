# Lenovo Yoga Duet 7 13ITL6

|    |     |
| -- | --- |
| **Machine Type Model** | [82MA0071GE](https://pcsupport.lenovo.com/ar/en/products/laptops-and-netbooks/yoga-series/yoga-duet-7-13itl6/82ma/82ma0071ge) (Yoga Duet 7-13ITL6) |

## Ubuntu 22.04 - Issues

### No sound with speakers

Check, if `snd_hda_intel` is used:

```shell
lsmod | grep snd_hda_intel
```

If yes, then run the following command ([source](https://askubuntu.com/a/1406739)):

```shell
echo "options snd-hda-intel model=generic" | sudo tee -a /etc/modprobe.d/alsa-base.conf
```

#### Links

* [**ArchLinux Wiki:** Lenovo ThinkPad X1 Yoga](https://wiki.archlinux.org/title/Lenovo_ThinkPad_X1_Yoga_(Gen_3)#Manual_method)
* [**Lenovo Forum 2021:** Yoga 7i 14ITL5 and 15ITL5 - ALC287 no sound with speaker & S3 ACPI mode not available - Linux Ubuntu](https://forums.lenovo.com/t5/Lenovo-Yoga-Series-Notebooks/Yoga-7i-14ITL5-and-15ITL5-ALC287-no-sound-with-speaker-S3-ACPI-mode-not-available-Linux-Ubuntu/m-p/5077334?page=1#5323234)
* [**BBS ArchLinux 2021:** thinkbook no audio](https://bbs.archlinux.org/viewtopic.php?id=266180)
* [**GitHub:** linux-realtek-alc287](https://github.com/thiagotei/linux-realtek-alc287)

### Build-in Cameras not working

Both cameras are not recognized by the system:

* Front camera: OV5678 (?)
* Rear camera: GC5035 (?)

```shell
# list usb devices (should also list webcams)
lsusb

# using Video4Linux 
sudo apt install v4l-utils
v4l2-ctl --list-devices
```

Use additional driver:

* Intel integrated Image Processing Unit 6 (IPU6) driver from intel-ipu6-dkms

```shell
sudo apt install linux-modules-ipu6-oem-24.04
```

Ubuntu 24.04 is bundled with Kernel 6.8. To install the 6.12 as follows (as described [here](https://9to5linux.com/how-to-install-linux-kernel-6-12-lts-on-ubuntu-24-04-lts-and-ubuntu-24-10))

```shell
sudo add-apt-repository ppa:cappelikan/ppa
sudo apt update && sudo apt full-upgrade
sudo apt install -y mainline
```

Research:

* [**ArchLinux:** Lenovo ThinkPad X1 Yoga (Gen 3)](https://wiki.archlinux.org/title/Lenovo_ThinkPad_X1_Yoga_(Gen_3))
* [**tudor codes:** How to Fix Lenovo Camera on Linux Ubuntu (Sep 2021)](https://www.tudorcodes.com/blog/how-to-fix-lenovo-camera-on-linux-ubuntu/)
* [**Lenovo Forum:** Camera not working](https://forums.lenovo.com/t5/Ubuntu/Camera-not-working/m-p/5172434?page=5)
* [Camera Sensor Front Driver for LENOVO - Yoga Duet 7 13ITL6 (82MA) working on Microsoft Windows 11](https://www.driveridentifier.com/scan/camera-sensor-front-driver/download/911780516/EBF2B82D950C4EC5B8B6E42D38782313/ACPI%5COVTI5678)
* [**Ubuntu Wiki:** IntelMIPICamera](https://wiki.ubuntu.com/IntelMIPICamera#Test_the_Intel_MIPI_camera)
* [**9to5Linux:** How to Install Linux Kernel 6.12 LTS on Ubuntu 24.04 LTS and Ubuntu 24.10](https://9to5linux.com/how-to-install-linux-kernel-6-12-lts-on-ubuntu-24-04-lts-and-ubuntu-24-10)
* [**reddit.com:** ipu6 webcams in ubuntu](https://www.reddit.com/r/DellXPS/comments/1cfu7ih/ipu6_webcams_in_ubuntu/)
* [**reddit.com:** Intel Progress On The IPU6 Linux Driver To Enable Web Camera Support With Newer Laptops](https://www.reddit.com/r/linux/comments/1360meg/intel_progress_on_the_ipu6_linux_driver_to_enable/)
* [**github.com:** intel / ipu6-drivers](https://github.com/intel/ipu6-drivers)
* [**launchpad.net:** "OEM Solutions Group" team](https://launchpad.net/~oem-solutions-group/+archive/ubuntu/intel-ipu6)
* [**Linux Community:** Schwierige Inbetriebnahme: MIPI-Kameras unter Linux](https://www.linux-community.de/ausgaben/linuxuser/2023/04/schwierige-inbetriebnahme-mipi-kameras-unter-linux/)
* [**Ubuntu Handbook:** Install Linux Kernel (6.12 Updated) in Ubuntu 24.04, 22.04, 20.04](https://ubuntuhandbook.org/index.php/2023/08/install-latest-kernel-new-repository/)
