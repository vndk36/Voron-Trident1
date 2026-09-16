# Voron trident Setup guide

Fresh install of the OS using Pi imager.

Right now installed Bookworm Lite 64 bits OS

Hardware wise the setup is a Voron trident printer, BTT Manta M5P board with a PI CM4 lite, CAN toolhead board BTT EBB 36 v1.2 directly wired on the Manta can port, Cartographer V3, BTT tft 50 screen.

## Update of the OS

From this, update and upgrade all the OS to get a fresh install
```
sudo apt-get update
sudo apt-get upgrade
```

## Screen and USB hub on Manta M5P board

The screen will not be visible at first on the Manta M5P board, you will need to enable it first.
Also you need to add a line to enable the USB hub.
On Trixie, it's done by editing the config.txt file in the bin/firmware/config.txt.
```
sudo nano /boot/firmware/config.txt
```
Edit it and add at the end:

```
dtoverlay=dwc2,dr_mode=host
dtoverlay=vc4-kms-dsi-7inch 
```

## Kiauh

```
sudo apt-get update && sudo apt-get install git -y
cd ~ && git clone https://github.com/dw-0/kiauh.git
./kiauh/kiauh.sh
```

This will let install:
- Klipper
- Moonraker
- Fluidd
- Klipper screen
- Extension / Autotune TMC
  
## CAn bus
Then do all of this as well to get the CAN BUS to work:

https://canbus.esoterical.online/Getting_Started.html

Summary of the command to preform to get Can working again on a previously working setup
```
sudo systemctl enable systemd-networkd
sudo systemctl start systemd-networkd
systemctl | grep systemd-networkd
sudo systemctl disable systemd-networkd-wait-online.service
echo -e 'SUBSYSTEM=="net", ACTION=="change|add", KERNEL=="can*"  ATTR{tx_queue_len}="128"' | sudo tee /etc/udev/rules.d/10-can.rules > /dev/null
cat /etc/udev/rules.d/10-can.rules
echo -e "[Match]\nName=can*\n\n[CAN]\nBitRate=1M\n\n[Link]\nRequiredForOnline=no" | sudo tee /etc/systemd/network/25-can.network > /dev/null
cat /etc/systemd/network/25-can.network
sudo reboot now
```

## Katapult
```
git clone https://github.com/Arksine/katapult
cd katapult
make menuconfig
make
```

## Cartographer
Then, install cartographer code:
```
curl -s -L https://raw.githubusercontent.com/Cartographer3D/cartographer3d-plugin/refs/heads/main/scripts/install.sh | bash -s -- --klipper ~/klipper --klippy-env ~/klippy-env
```

## Shaktune
And finally install shaketune to be able to perform some input shaper graphs:
```
wget -O - https://raw.githubusercontent.com/Frix-x/klippain-shaketune/main/install.sh | bash
```


## Moonraker config
Add this to the Monraker config file, this to have cartographer and autotuneTMC in the updatable files:
```
[update_manager cartographer_plugin]
type: python
channel: stable
virtualenv: ~/klippy-env
project_name: cartographer3d-plugin
is_system_service: False
managed_services: klipper
info_tags: desc=Cartographer Plugin
```


# BTT M5P
Commands specific to the M5P board with a CM4

Enable the screen on the correct port:

sudo wget https://datasheets.raspberrypi.com/cmio/dt-blob-disp1-cam1.bin -O /boot/firmware/dt-blob.bin

Then edit the config.txt in the SD card root part







