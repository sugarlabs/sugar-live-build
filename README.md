# Sugar Live Build
## Introduction

Welcome to Sugar Live Build! This makes a complete bootable image containing Sugar, the toolkits, and the demonstration activities. It:

- can be booted from hard drive, flash drive, and optical media, automatically starting Sugar without persistence,

- can be installed as a virtual machine, with persistence and password protection,

- contains all build dependencies, configured source trees (git clones in /usr/src), and binaries (make install) for Sugar modules and the demonstration activity set.

If you're looking for a pre-built ISO file see [Downloads](http://people.sugarlabs.org/~quozl/sugar-live-build-20171009/).

## How to Build

- install Debian Stretch,

- clone this repository,

- run the `build` script.

This will take some time to process, and at the end you will have a file ending with `.hybrid.iso` which is your iso bootable file.

## Debian Live Build

Debian Live Build has [documentation](https://debian-live.alioth.debian.org/live-manual/stable/manual/html/live-manual.en.html#107) for more details.
