# Kiauh

``sudo apt-get update && sudo apt-get install git -y
cd ~ && git clone https://github.com/dw-0/kiauh.git
./kiauh/kiauh.sh``

# Katapult

git clone https://github.com/Arksine/katapult
cd katapult
make menuconfig
make

# Cartographer

cd ~
git clone https://github.com/Cartographer3D/cartographer-klipper.git
./cartographer-klipper/install.sh

## moonraker

[update_manager cartographer]
type: git_repo
path: ~/cartographer-klipper
channel: stable
origin: https://github.com/Cartographer3D/cartographer-klipper.git
is_system_service: False
managed_services: klipper
info_tags:
  desc=Cartographer Probe

#  Autotune TMC

wget -O - https://raw.githubusercontent.com/andrewmcgr/klipper_tmc_autotune/main/install.sh | bash

## moonraker
[update_manager klipper_tmc_autotune]
type: git_repo
channel: dev
path: ~/klipper_tmc_autotune
origin: https://github.com/andrewmcgr/klipper_tmc_autotune.git
managed_services: klipper
primary_branch: main
install_script: install.sh


# Shaktune

wget -O - https://raw.githubusercontent.com/Frix-x/klippain-shaketune/main/install.sh | bash

# Crownest

cd ~
git clone https://github.com/mainsail-crew/crowsnest.git
cd ~/crowsnest
sudo make install

## moonraker

[update_manager crowsnest]
type: git_repo
path: ~/crowsnest
origin: https://github.com/mainsail-crew/crowsnest.git
install_script: tools/pkglist.sh

