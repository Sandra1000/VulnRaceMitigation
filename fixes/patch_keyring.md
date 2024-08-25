# Patch ForCVE-2015-1325 (Keyring Race Condition).
The following are step by step ways of patching the Keyring Vulnerability.

## 1.	Download the Original Tarball:
$ wget https://launchpad.net/ubuntu/+archive/primary/+sourcefiles/apport/2.14.1-0ubuntu3.11/apport_2.14.1.orig.tar.gz --no-check-certificate

$ wget https://launchpad.net/ubuntu/+archive/primary/+sourcefiles/apport/2.14.1-0ubuntu3.11/apport_2.14.1-0ubuntu3.11.diff.gz --no-check-certificate

$ wget https://launchpad.net/ubuntu/+archive/primary/+sourcefiles/apport/2.14.1-0ubuntu3.11/apport_2.14.1-0ubuntu3.11.dsc --no-check-certificate

# Steps to Apply the Patch
### 1.	Install Necessary Packages (if not already installed):

$ sudo apt update
$ sudo apt install build-essential dpkg-dev

### 2.	Create a Working Directory:
$ mkdir ~/keyring_patch
$ cd ~/keyring_patch

### 3.	Extract the Kernel Source:
$ dpkg-source -x apport_2.14.1-0ubuntu3.11.dsc
$ cd apport-2.14.1

### 4.	Apply the Patch:
$ gunzip -c ../apport_2.14.1-0ubuntu3.11.diff.gz | patch -p1


### 5.	Compile the Module:
$ make -j$(nproc) modules

### 6.	Install the Compiled Module:
$ sudo make modules_install

This process will allow you to apply the patch related to CVE-2015-1325 for the keyring using the apport package.
