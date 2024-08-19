# Patch for Dirty COW (CVE-2016-5195)

The following are step-by-step instructions for patching the Dirty COW vulnerability.

## 1. Install Tools for Building and Managing Kernel Packages

If not already installed, use the following commands:

$ sudo apt update
$ sudo apt install build-essential dpkg-dev

## 2. Create a Directory to Extract and Modify the Kernel Source


$ mkdir ~/kernel_patch
$ cd ~/kernel_patch

## 3. Download the Kernel Source and Patch Files
Run the following commands to download the necessary files (links are provided in the appendix):

$ wget https://launchpad.net/ubuntu/+archive/primary/+sourcefiles/linux/3.13.0-100.147/linux_3.13.0.orig.tar.gz --no-check-certificate
$ wget https://launchpad.net/ubuntu/+archive/primary/+sourcefiles/linux/3.13.0-100.147/linux_3.13.0-100.147.diff.gz --no-check-certificate
$ wget https://launchpad.net/ubuntu/+archive/primary/+sourcefiles/linux/3.13.0-100.147/linux_3.13.0-100.147.dsc --no-check-certificate

## 4. Extract the Kernel Source Code
Once the downloads are complete, extract the kernel source:

$ dpkg-source -x linux_3.13.0-100.147.dsc
$ cd linux-3.13.0


## 5. Apply the Patch
Apply the patch contained in the .diff.gz file:

$ gunzip -c ../linux_3.13.0-100.147.diff.gz | patch -p1


## 6. Use the Default Configuration or Customize It
Copy the current kernel configuration and update it:

$ cp /boot/config-$(uname -r) .config
$ make oldconfig
Note: This will prompt you for new configuration options. Press Enter to accept the default values. This process might take some time.


## 7. Compile Only the Modules
To compile the kernel modules, use the following command:

$ make -j$(nproc) modules


## 8. Install the Modules
After compilation, install the modules:

$ sudo make modules_install


## 9. Reboot the System
Reboot the system to apply the changes and boot into the new kernel:

$ sudo reboot
