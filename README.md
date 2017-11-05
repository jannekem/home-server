# Home server setup
## Description
This project contains information on how to create your own home server for backing up your data and more. The repository is in a tutorial format and different phases of the server setup have been split to their own folders.

The instructions are meant to be easy to follow, enhancement pull requests are welcome!

## Requirements
First of all you will need some sort of server machine. This can be an old salvaged PC or a specifically built server machine. If you want to buy a new server you could take a look at the HP ProLiant MicroServer lineup.

Minimum requirements:
- Dual Core CPU
- 4 GB RAM
- 2 separate hard drives

Recommended:
- 8 GB RAM

Here we assume that you have at least two separate hard drives available so that you can have some redundancy if either one of those goes bad. The Western Digital Red hard drives are a great option as they are meant for constant use in NAS environments.

You will also need a 4 GB or larger USB stick that can be left on the server.

If your server doesn't have a remote management system (iLO, RMM2, DRAC, etc.) you will also need a monitor and a keyboard for the initial installation.

## Overview
1. [Install ESXi](/esxi/README.md)
2. [Install CentOS 7](/centos7/README.md)
3. Install Docker and docker-compose
4. Install Nextcloud
