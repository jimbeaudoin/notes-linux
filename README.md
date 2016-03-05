notes-linux
===========

### Environment Variables
```
# Globals
/etc/environment

# By Profile
~/.profile
```

### Create a swap
```
sudo /bin/dd if=/dev/zero of=/var/swap.1 bs=1M count=1024
sudo /sbin/mkswap /var/swap.1
sudo /sbin/swapon /var/swap.1

# Edit /etc/fstab and add the following at the bottom to make the swap available at reboot:
/var/swap.1 swap swap defaults 0 0
```

#### Stop Intel Wireless Led Blink
```sh
sudo vim /etc/modprobe.d/wlan-blink.conf
  options iwlwifi led_mode=1
```

#### Debian Graphic Card Utility
```sh
sudo apt-get install mesa-utils
```

#### Add User to sudo Group
```sh
usermod -a -G sudo <username>
```

#### Create Random Binary Files
```sh
# 1KB
time dd if=/dev/urandom of=1KB bs=1 count=1024
# 1MB
time dd if=/dev/urandom of=1MB bs=1 count=1048576
# 25MB
time dd if=/dev/urandom of=25MB bs=1 count=26214400
# 50 MB
time dd if=/dev/urandom of=50MB bs=1 count=52428800
# 100 MB
time dd if=/dev/urandom of=100MB bs=1 count=104857600
# 150MB
time dd if=/dev/urandom of=150MB bs=1 count=157286400
# 200MB
time dd if=/dev/urandom of=200MB bs=1 count=209715200
# 250MB
time dd if=/dev/urandom of=250MB bs=1 count=262144000
# 300MB
time dd if=/dev/urandom of=300MB bs=1 count=314572800
# 400MB
time dd if=/dev/urandom of=400MB bs=1 count=419430400
# 500MB
time dd if=/dev/urandom of=500MB bs=1 count=524288000
# 600MB
time dd if=/dev/urandom of=600MB bs=1 count=629145600
# 700MB
time dd if=/dev/urandom of=700MB bs=1 count=734003200
# 800MB
time dd if=/dev/urandom of=800MB bs=1 count=838860800
# 900MB
time dd if=/dev/urandom of=900MB bs=1 count=943718400
# 1000MB
time dd if=/dev/urandom of=1000MB bs=1 count=1048576000
```


#### Show Dependencies
```sh
aptitude show nginx
```

#### File Checksum
```sh
shasum -a 256 nginx-1.6.2.tar.gz
b5608c2959d3e7ad09b20fc8f9e5bd4bc87b3bc8ba5936a513c04ed8f1391a18  nginx-1.6.2.tar.gz
```

#### General
```sh
# Show CPU Info
cat /proc/cpuinfo
# Tail a file
tail -f <file_name>
```
#### Generate Certificate
```sh
# Generate a web certificate & CSR
openssl req -new -newkey rsa:2048 -nodes -keyout server.key -out server.csr

# Generate self signed certificate
openssl req -x509 -sha256 -newkey rsa:4096 -keyout server.key -out server.crt -nodes -days 36500

# Generate a DH for nginx (Take some times)
openssl dhparam -out dhparam.pem 4096

# Private key and SSL certificate in unencrypted PEM format.
openssl rsa -in privateKey.key -text > private.pem
openssl x509 -inform PEM -in www_mydomain_com.crt > public.pem

# Check Certificate
openssl s_client -showcerts -connect yourapp.com:443

# Generate an RSA keypair with a 4096 bit private key
openssl genrsa -aes256 -out private_key.pem 4096

# Extracting the public key from an RSA keypair
openssl rsa -pubout -in private_key.pem -out public_key.pem

# Lets Encrypt
./letsencrypt-auto certonly --standalone -d example.com -d www.example.com --rsa-key-size 4096
```

#### Show syslog
```sh
tail -f /var/log/messages
```

#### Format USB Drive
``` sh
fdisk /dev/sdd
o
w
fdisk /dev/sdd
n
sudo cryptsetup luksFormat /dev/sdd1
YES
cryptsetup luksOpen /dev/sdd1 LUKS001
mkfs.vfat /dev/mapper/LUKS001 -n LUKS001
cryptsetup luksClose LUKS001
```

#### Remove a user from a group
```sh
sudo deluser user group
```

#### Show Kernel Version
```sh
uname -r
```

#### Set Locale
```sh
sudo dpkg-reconfigure locales
```

#### Show OS Version
```sh
lsb_release -a #=> Show OS Version
cat /proc/version
cat /etc/issue
cat /etc/os-release
```

#### Shutdown VPS
```sh
sudo shutdown -h now
```

#### Generate SSH Key
```sh
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

#### Make Symbolic Link
```sh
ln -s /path/to/file /path/to/symlink
```

#### Search Package
```sh
# Debian
sudo apt-cache search <package_name>

# Red Hat
sudo yum search <package_name>
```

#### Install Package
```sh
# Install
sudo dpkg -i package.deb
# Check
dpkg -l | grep 'tcl'
# Remove
dpkg -r tcl8.4
``` 

#### Show Package Information
```sh
sudo yum info <package_name>
sudo yum --enablerepo=epel info <package_name>
```

#### Execute a Command at Boot
```sh
# Debian
/etc/rc.local #=> Put your cmd in this file
```

#### Show Running Processes
```sh
ps auxf
```

#### Show Groups
```sh
# Red Hat
sudo yum grouplist
```

#### Change Hostname
```sh
sudo vi /etc/sysconfig/network
  HOSTNAME=<new_hostname>
  
# You can apply the new hostname without reboot
sudo hostname <new_hostname>
```

#### Add EPEL Repos
```sh
curl -O http://dl.fedoraproject.org/pub/epel/beta/7/x86_64/epel-release-7-0.2.noarch.rpm
sudo rpm -ivh epel-release-7-0.2.noarch.rpm
yum --enablerepo=epel info zabbix
yum --enablerepo=epel install zabbix
```

#### Show login history of users
```sh
sudo last
```

#### Show who is logged in
```sh
sudo who
```

#### Find out when was the system last rebooted
```sh
sudo last reboot
```

#### See when did someone last log in to the system
```sh
sudo lastlog
```

#### Get HTTP Server Headers
```sh
curl -I http://example.com
```

#### Show Established Connections
```sh
netstat -an | grep ESTABLISHED
netstat -natp
```

#### Show Listening Ports (udp/tcp)
```sh
netstat -nlutp
```

#### AWS (Amazon Web Services)
```sh
sudo -s #=> Become root
```

#### Video Card Informations
```sh
lspci | grep VGA #=> Identify your hardware (even if not configured at all)
find /dev -group video #=> Check if the correct kernel driver is loaded
glxinfo | grep -i vendor #=> Check if the correct X driver is loaded
```

#### Terminal Softwares
```sh
apt-get install w3m #=> Terminal Web Browser
```

#### How to mount a remote directory over ssh on Linux
```sh
sudo apt-get install sshfs
sudo usermod -a -G fuse <user_name>
sshfs my_user@remote_host:/path/to/directory <local_mount_point>

#To unmount a ssh-mounted directory:
fusermount -u <local_mount_point>

# If you would like to automatically mount over ssh upon boot, set up passwordless ssh login, and append the following in /etc/fstab.
sudo vi /etc/fstab
sshfs#my_user@remote_host:/path/to/directory <local_mount_point> fuse user 0 0
```

#### Kernel Upgrade (official)
```sh
# Show available kernel images
apt-cache search linux-image

# Install kernel
sudo apt-get install linux-image-x.x.x-xx
```

#### Kernel Upgrade (backports)
```sh
# Add Debian backports source
sudo vim /etc/apt/sources.list
  deb http://http.debian.net/debian wheezy-backports main
  
sudo apt-get -t wheezy-backports install linux-image-amd64
```
  
#### ISO to USB Stick
```sh
# Get USB Stick place
sudo ls -l /dev/disk/by-id/*usb*
cd ~/downloads
sudo dd if=<isofile> of=/dev/sdb bs=4M; sync
# 
```

#### To classified
```sh
head .bash_history #=> Show last commands
```
#### From a web site (I do not remember where. Sry!)... for video card driver

You can download the driver for your video card for Ubuntu 64bit from here. Assuming that you are using Ubuntu 64bit now. If you installed Ubuntu 32 bit, there is 331 version of the same driver for Ubuntu 32bit. Save your driver somewhere where you can easily access it, like your user home directory or inside a newly created nvidia directory in your user home directory.

To be able to install your nvidia driver you have to remove your previous video driver with this code in a terminal window:
```
sudo apt-get remove nvidia*
```
After you finish with this one, you should also blacklist the nouveau driver by editing this file:
```
sudo gedit /etc/modprobe.d/blacklist-nouveau.conf
```
…and add these lines at the end:
```
    blacklist nouveau
    blacklist lbm-nouveau
    options nouveau modeset=0
    alias nouveau off
    alias lbm-nouveau off
```
If, by any chance, there is no blacklist-nouveau.conf present in /etc/modprobe.d/, you can save your file as blacklist-nouveau.conf when prompted.

And you can also disable the Kernel Nouveau by typing these lines in a terminal window:
```
    echo options nouveau modeset=0 | sudo tee -a /etc/modprobe.d/nouveau-kms.conf
```
and after that
```
    sudo update-initramfs -u
```
Now you can reboot your computer, and when you get to the login prompt, press Ctrl+Alt+F1 to exit to the terminal console. Login with your username and password.

Go to the directory where you saved your nvidia driver using the command cd in the terminal console. Eg. cd nvidia considering that you are already in your user home directory after you login. You can use command dir to be able to see your exact driver's name.

To stop your display manager or the X server, you can type in the console this code:
```
   sudo stop lightdm   or

   sudo lightdm stop
```
If you are not using lightdm as your default display manager (DM), replace lightdm with your default display manager, which can be either kdm or gdm or whatever your display manager is.

You should get a message in the terminal console saying --> lightdm stopped/waiting
```
Install Linux Headers using

  sudo apt-get install linux-headers-generic
And now you can finally install the nvidia driver using a code similar to this one:

  sudo sh NVIDIA-Linux-x86_64.....run    (for Ubuntu 64bit)  
or

  sudo sh NVIDIA-Linux-x86.....run    (for Ubuntu 32bit)
If you don't type the exact name of the driver, you'll get this message: NVIDIA-Linux... could not be found and you should type again the code for installing the driver.

Nvidia installer automatically installs the driver, and at the end it will ask you whether you want to save your new X configuration. Press Yes. After reboot and getting to your desktop and changing your NVIDIA settings as you please you should open a terminal window and type in this code:

  sudo nvidia-xconfig
to save your new nvidia configuration in /etc/X11/xorg.conf.
```
It can happen that after reboot your system shows a black screen or enters the low graphics mode. To fix this you should exit again to the console terminal, login with your username and password, and use the code provided above sudo nvidia-xconfig and also make use of the following tutorial. It is meant to fix the greeter assuming that they haven't fixed this bug in Ubuntu 14.04.

--
<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons Licence" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/80x15.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">notes-linux</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="http://jim-beaudoin.com" property="cc:attributionName" rel="cc:attributionURL">Jimmy Beaudoin</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.
