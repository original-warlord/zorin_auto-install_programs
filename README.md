# zorin_auto-install_programs
This bash script is a down and dirty version of an initial setup for Zorin18 OS.

All code used is below in this README. I used something similar to setup my daughter's computer quickly.

Once the aut-install downloads and you copy it to the desktop, open a terminal cd to the desktop and use the "./" command to run it.

Go to the Zorin emblem and search for Terminal
Open Terminal and click in the Terminal

Type the following command after your username@computername:~$ cd Desktop

then hit enter

Type the ls command and hit enter
then type the following command 
./zorin_auto-install_programs_all

then hit enter and it will run.

When it reboots, you can right click any of the following by right-clicking and 
selecting "Run as Program" :
Personal_wiki - a downloadable offline wiki for basic computer stuff
web_zorin_auto-install_programs - opens the web to the Github that contains the code that ran

The following has to be run with the ./ command in Terminal :
zorin_auto-install_programs-direct-download - wget downloadable version


# CODE : 

#!/usr/bin/env bash

# Update, Upgrade, and autoremove for main system before installs.
echo "Starting Update, Upgrade, and autoremove current applications.."
sleep 1
sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y

# Starting install of applications
echo "Starting install of programs."
sleep 1
sudo apt install bat gnucash vlc wireshark chromium-browser snapd audacity kdenlive pavucontrol bluefish kleopatra emacs kate sox terminator bmon htop gparted gimp nmap ufw qemu-kvm virt-manager wget libvirt-clients libvirt-daemon-system bridge-utils libguestfs-tools genisoimage openssh-server openssh-client -y


# Adding the user account to libvirtd and libvirtd-qemu to build and use Virtual Machines
echo "Adding user account to libvirtd and libvirtd-qemu to build and use Virtual Machines"
sleep 1
sudo adduser $USER libvirt && sudo adduser $USER libvirt-qemu && sudo adduser $USER kvm
sudo systemctl enable --now libvirtd
sudo systemctl start libvirtd


sleep 3

# Create the Personal_Wiki download bash script and link to Personal_wiki
echo "Setting up PERSONAL_WIKI"
echo -e '#!/usr/bin/env bash \nbrave-browser "https://drive.google.com/drive/folders/1KqoVLiCxCREzTJULhuXgtHQEnP4IogBq?usp=sharing"' > /home/$USER/Desktop/Personal_wiki && chmod +x /home/$USER/Desktop/Personal_wiki

# Create the Zorin Auto-install download bash script and link to Github page
echo -e '#!/usr/bin/env bash \nbrave-browser "https://github.com/original-warlord/zorin_auto-install_programs.git"' > /home/$USER/Desktop/web_zorin_auto-install_programs && chmod +x /home/$USER/Desktop/web_zorin_auto-install_programs
echo -e '#!/usr/bin/env bash \nwget https://github.com/original-warlord/zorin_auto-install_programs/archive/refs/heads/main.zip' > /home/$USER/Desktop/zorin_auto-install_programs-direct-download && chmod +x /home/$USER/Desktop/zorin_auto-install_programs-direct-download
echo -e 'mv main.zip Zorin_auto-install_programs.tgz && mv Zorin_auto-install_programs.tgz /home/$USER/Desktop/ && cd /home/$USER/Desktop && tar -zxvf Zorin_auto-install_programs.tgz && rm Zorin_auto-install_programs.tgz' >> /home/$USER/Desktop/zorin_auto-install_programs-direct-download

# Reboot to impliment changes
sudo reboot -h now

# Self Destruct
rm -- "$0"





