# Mainsail OS install
Fresh install of Mainsail OS 2.2.2

From this update, all the plugins and fix all the errors in the update tab of the mainsail plugin.

## Cartographer
Then, install cartographer code:
```
curl -s -L https://raw.githubusercontent.com/Cartographer3D/cartographer3d-plugin/refs/heads/main/scripts/install.sh | bash -s -- --klipper ~/klipper --klippy-env ~/klippy-env
```

##  Autotune TMC

Intalling Autotune TMC driver library:
```
wget -O - https://raw.githubusercontent.com/andrewmcgr/klipper_tmc_autotune/main/install.sh | bash
```

## Shaktune
And finally install shaketune to be able to perform some input shaper graphs:

```
wget -O - https://raw.githubusercontent.com/Frix-x/klippain-shaketune/main/install.sh | bash
```

## Kiauh

```
sudo apt-get update && sudo apt-get install git -y
cd ~ && git clone https://github.com/dw-0/kiauh.git
./kiauh/kiauh.sh
```
Then go through the menu to install Klipper screen with the default options.


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

[update_manager klipper_tmc_autotune]
type: git_repo
channel: dev
path: ~/klipper_tmc_autotune
origin: https://github.com/andrewmcgr/klipper_tmc_autotune.git
managed_services: klipper
primary_branch: main
install_script: install.sh

[update_manager KlipperScreen]
type: git_repo
path: ~/KlipperScreen
origin: https://github.com/KlipperScreen/KlipperScreen.git
virtualenv: ~/.KlipperScreen-env
requirements: scripts/KlipperScreen-requirements.txt
system_dependencies: scripts/system-dependencies.json
managed_services: KlipperScreen
```

## Katapult
```
git clone https://github.com/Arksine/katapult
cd katapult
make menuconfig
make
```

# BTT M5P
Commands specific to the M5P board with a CM4

Enable the screen on the correct port:

sudo wget https://datasheets.raspberrypi.com/cmio/dt-blob-disp1-cam1.bin -O /boot/firmware/dt-blob.bin

Then edit the config.txt in the SD card root part



# Old method or with a more rugulare debian os
# Cartographer
```
cd ~
git clone https://github.com/Cartographer3D/cartographer-klipper.git
./cartographer-klipper/install.sh
```
## moonraker
```
[update_manager cartographer]
type: git_repo
path: ~/cartographer-klipper
channel: stable
origin: https://github.com/Cartographer3D/cartographer-klipper.git
is_system_service: False
managed_services: klipper
info_tags:
  desc=Cartographer Probe
```
#  Autotune TMC
```
wget -O - https://raw.githubusercontent.com/andrewmcgr/klipper_tmc_autotune/main/install.sh | bash
```
## moonraker
```
[update_manager klipper_tmc_autotune]
type: git_repo
channel: dev
path: ~/klipper_tmc_autotune
origin: https://github.com/andrewmcgr/klipper_tmc_autotune.git
managed_services: klipper
primary_branch: main
install_script: install.sh
```

# Shaktune
```
wget -O - https://raw.githubusercontent.com/Frix-x/klippain-shaketune/main/install.sh | bash
```
# Crownest
```
cd ~
git clone https://github.com/mainsail-crew/crowsnest.git
cd ~/crowsnest
sudo make install
```
## moonraker
```
[update_manager crowsnest]
type: git_repo
path: ~/crowsnest
origin: https://github.com/mainsail-crew/crowsnest.git
install_script: tools/pkglist.sh
```
