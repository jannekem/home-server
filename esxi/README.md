# ESXi installation
Here we will go through the phases to install VMware ESXi hypervisor on your server.

## Download and licensing
Go to the VMware site and obtain a free license key for the VMware vSphere Hypervisor 6 (you will need to register for a free account):
[https://my.vmware.com/group/vmware/evalcenter?p=free-esxi6]

Register for the free trial to download a newer version of ESXi
[https://my.vmware.com/group/vmware/evalcenter?p=vsphere-6#tab_download]

## Preparation
After downloading the .iso file you will need to create a bootable USB stick with the ESXi image. 

### Windows
If you are on Windows you can download Rufus [https://rufus.akeo.ie/] which is a fast and handy tool for creating bootable USB sticks. It doesn't need any installation, just download and run the executable. Select your USB stick from the dropdown menu and add the .iso file by clicking the disk drive icon next to the "Create bootable disk using" checkbox. Press start and wait for the process to finish.

### Mac OS/Linux
On Mac or Linux you can use for example Etcher [https://etcher.io/] or UNetbootin [https://unetbootin.github.io/] to create the installation drive.

## Installation
Attach a monitor and keyboard to your server or log in to the remote management interface if your server has one.

Plug the newly created installation USB drive to the server machine and power on. The server should boot to the ESXi installer. If the installation screen doesn't come up check that USB is highest on the boot order in BIOS. Some server machines have an additional USB port inside that you can use.

The installer will load everything in memory so you can choose the same USB stick as the destination for the installation. Follow the instructions on the installer and create the root password.

## Settings
Log in to the management console and set the management network settings. On your own machine connected to the same network go to the configured management IP address on your browser to access the vSphere Web Client. Give the root account credentials and you should be able to manage the host.

