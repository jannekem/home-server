# CentOS 7 installation
Here we'll install CentOS 7 Linux to a virtual machine on the ESXi host.

## Download CentOS 7 minimal
Go to [https://www.centos.org/download/] and download the Minimal ISO image.

Log in to the ESXi Web Client by going to the server management IP address on your browser and transfer the .iso file to the server datastore.

## Create VM
Click "Create/Register VM".

Select "Create new virtual machine" and click Next.

Give the VM a name, for example "Nextcloud". Select compatibility "ESXi 6.5 virtual machine", Guest OS family "Linux" and Guest OS version "CentOS 7 (64-bit)" and click next.

Select the storage where you want to store the virtual machine files.

On the Customize settings tab allocate the resources to the VM, here are some possible values:

- CPU: 2
- Memory: 6 GB
- Hard disk 1: Thin provision, 40 GB
- Hard disk data: Thin provision, 1.5 TB
- Hard disk backup: Thin provision, 2 TB

Click Next, verify that the settings are correct and click Finish.

## Installation
Click the newly created VM and click "Power on". The VM should boot from the CentOS .iso image. Select to install CentOS.

Select the installation language.

Under System select the installation destination 

Reboot when prompted.

## Connect to the VM
When the VM has rebooted use your newly created credentials to log in and type command
```
ip addr
```
This will print out the network configuration. The output can be something like this:
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN qlen 1
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: ens192: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP qlen 1000
    link/ether 00:0c:29:5f:fd:7f brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.90/24 brd 192.168.1.255 scope global dynamic ens192
       valid_lft 85879sec preferred_lft 85879sec
    inet6 fe80::885f:a458:1f7:e126/64 scope link 
       valid_lft forever preferred_lft forever
```
The first entry is the local loopback interface and the second one is the actual outside connection. Check the ip address next to `inet` and remember it, in this case it is `192.168.1.90`.

The online console is not very pleasant to work with so let's close it and connect to the server through SSH. On Windows you can download PuTTY [http://www.putty.org/] and on Mac or Linux you can use the terminal app and type `ssh 192.168.1.90` (replace the ip address with the one from your server). Accept the certificate and type in your newly created credentials. If you can't connect make sure that you are connected to the same network as the server.

## Configure the server
Now that you can log in to the server let's make the required configurations.

