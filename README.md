# Sugar Live Build
## Introduction

Sugar Live Build is a complete bootable image containing Debian,
Sugar, the Sugar toolkits, and the demonstration activities.

- it can be booted from hard drive, flash drive, and optical media,
automatically starting Sugar without persistence;

- it can be installed as a virtual machine, with persistence and
password protection,

- it contains all build dependencies, configured source trees (git
clones in `/usr/src`), and binaries (`make install`) for Sugar modules
and the demonstration activity set.

For a pre-built ISO-9660 file see
[Downloads](http://people.sugarlabs.org/~quozl/sugar-live-build/).

## How to install

Sugar Live Build can be booted and operate as-is.  Sometimes it is
installed on disk for persistence, password protection, and for use as
a development target system.

Boot from the ISO file, and as soon as the system shows
the boot menu, be sure to select "Install".

This will start installation of Debian.

You will be asked a series of questions, such as language, location,
and keyboard.  Additional components will be loaded.  Then further
questions; host name, domain name, new root password, new user
account, and clock time zone.

There are other questions, but these are normal Debian questions, so
the best way to answer them is to understand the question by reading
the Debian documentation.

Eventually the system will be installed.

When the system is rebooted, log in with the new user account, and
Sugar will be started.

## How to rebuild

Rebuilding Sugar Live Build is not necessary if you just want to use it.  You only need to rebuild if you plan to release a new image for others.

1. Install Debian 10 Buster;

2. Clone this repository;
```bash
git clone https://github.com/sugarlabs/sugar-live-build.git
```

3. (optional) Work around a bug in Metacity 3.30 which causes the Journal
to open raised on startup, obscuring the Home View
(or you can press F3 when it does this)
```bash
src=http://dev.laptop.org/~quozl/metacity-3.38-backport-debian-buster/
dir=src/config/packages.chroot
arch=$(dpkg --print-architecture)
wget -P $dir \
    $src/metacity_3.38.0-2_$arch.deb \
    $src/libmetacity3_3.38.0-2_$arch.deb \
    $src/metacity-common_3.38.0-2_all.deb
```

4. Run the `build` script.
```bash
./build
```

When this is finished, look for a new file ending with `.hybrid.iso`,
which is a bootable ISO-9660 file.

## How to add activities

1. Open the `build` script with a text editor,

2. Look for the section that clones activities,

2. Clone each activity;

    `clone https://github.com/username/repository.git ActivityName.activity`

Above is a template.  Use the URL of the repository.  Replace
`ActivityName` with the bundle name. Use `.activity` as the directory
suffix.

Then rebuild.

## Debian Live Build

Debian Live Build has
[documentation](https://live-team.pages.debian.net/live-manual/html/live-manual/index.en.html)
for more details.

## Caching

A cache of packages is maintained by *Live Build*, so that repeated builds will avoid downloading what has already been downloaded.  The cache is about 1.4 GB after our build of Debian Buster.

However, the cache is distribution version specific.  For development of multiple distribution versions, you may use an instance of the *approx* package.  This may be on a different system, or the same system as *Live Build*.

This is optional.

How to set up *Live Build* and *approx* together:

* install the *approx* package:

~~~
		sudo apt install approx
~~~

* edit the *approx* configuration file:

~~~
		sudo editor /etc/approx/approx.conf
~~~

* add entries for Debian:

~~~
		debian          http://ftp.debian.org/debian
		security        http://security.debian.org/
~~~

* edit your `build` file to switch to using approx,

~~~
		lb config \
		    --mirror-bootstrap http://approx:9999/debian \
		    --mirror-chroot-security http://approx:9999/security \
~~~

* clear the *Live Build* disk cache,

~~~
		sudo rm -rf cache
~~~

* run *Live Build* again.

---
