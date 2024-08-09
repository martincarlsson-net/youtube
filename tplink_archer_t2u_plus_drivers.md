mkdir git && cd git
git clone https://github.com/morrownr/8821au-20210708.git
cd rtl8812au
sudo make dkms_install
dkms status
