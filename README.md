# Sugar Live Build
## Introduction

Welcome to Sugar Live Build! This project contains the config files to make a complete bootable image containing Sugar, the toolkits, and the demonstration activities. It:

- can be booted from hard drive, flash drive, and optical media, automatically starting Sugar without persistence,

- can be installed as a virtual machine, with persistence and password protection,

- contains all build dependencies, configured source trees (git clones in /usr/src), and binaries (make install) for Sugar modules and the demonstration activity set.

**If you're looking for a pre-compiled ISO file please refer to [Downloads](http://people.sugarlabs.org/~quozl/sugar-live-build-20171009/).**


## Configuration with Debian Live Build to make a Sugar Live Build ISO 
1. Install Debian Live Build. (You may also refer to the their [docs](https://debian-live.alioth.debian.org/live-manual/stable/manual/html/live-manual.en.html#107) for the installation process.)

    `sudo apt-get install live-build`

2. Build using Debian Live Build.
    
    `sudo lb build`
    
    This will take some time to process, at the end you will have a file ending with `.hybrid.iso` which is your iso bootable file.
