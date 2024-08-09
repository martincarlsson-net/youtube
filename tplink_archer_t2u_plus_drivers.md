## How to install Archer T2U Plus driver on Raspberry Pi Os 32 bit
### Create dir for drivers
mkdir ~/git && cd ~/git

### Clone driver repo
git clone https://github.com/morrownr/8821au-20210708.git

### Install
cd rtl8812au && sudo make dkms_install

### Check driver status
dkms status

Output should show something like:
 - rtl8821au/5.12.5.2, 6.6.31+rpt-rpi-v7, armv7l: installed

### Check wirless interface wlan1
iwconfig