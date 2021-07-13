## Created VM of linux/ARM64 using qemu on below environment

Host OS version:Name="Ubuntu linux"

Version="14.4"

Architecture:x86_64

Ram:8 GB


## How do we install QEMU and install an OS on QEMU?

<h5> Step - 1- Install qemu-system-aarch64 & QEMU_EFI.fd </h5>

<p> apt-get install qemu-system-arm </p>

<p> QEMU_EFI.fd (download link:http://releases.linaro.org/components/kernel/uefi-linaro/16.02/release/qemu64/) </p>

<h5> Step - 2- Download the image you want to boot. <br> For our example we use an Ubuntu installer.</h5>

What I use here is the ubuntu 16.04 server version of the arm64 architecture-

<p> wget https://old-releases.ubuntu.com/releases/16.04.3/ubuntu-16.04.3-server-amd64.iso</p>


<h5> Step - 3- Create a virtual hard disk</h5>

<p> qemu-img create ubuntu16.04-arm64.img 16G </p>


<h5> Step - 4- Start QEMU with the installer.</h5>

<p> qemu-system-aarch64 -m 2048 -cpu cortex-a57 -smp 2 -M virt -bios QEMU_EFI.fd -nographic -drive if=none,file=ubuntu-16.04.3-server-arm64.iso,id=cdrom,media=cdrom -device virtio-scsi-device -device scsi-cd,drive=cdrom -drive if=none,file=ubuntu16.04-arm64.img,id=hd0 -device virtio-blk-device,drive=hd0 </p>


<h5> Step - 5- Follow the instructions to install Ubuntu to the ubuntu-image.img file.<br> Then restart QEMU without the installer image with the following command.</h5>

<p> qemu-system-aarch64 -m 2048 -cpu cortex-a57 -smp 2 -M virt -bios QEMU_EFI.fd -nographic -drive if=none,file=ubuntu16.04-arm64.img,id=hd0 -device virtio-blk-device,drive=hd0 </p>

## What problem did I face?
  
  I faced gcc package installation problem.
  

## What did you understand about that?
   
   I understand that for gcc package instalation no reqirement for internet.

## How did i solve it?
 
 With the help of these commands i solved the gcc instalation problem.
 
 apt-get -f install
 
 apt install gcc

**Source Link  ===>**https://www.programmersought.com/article/81835534690/
