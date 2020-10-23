# Sugar Live Build
## Introduction

Sugar Live Build is a complete bootable image containing Debian Linux,
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

## How to rebuild

Rebuilding Sugar Live Build is not necessary if you just want to use it.  You only need to rebuild if you plan to release a new image for others.

1. Install Debian 10 Buster;

2. Clone this repository;
```bash
git clone https://github.com/sugarlabs/sugar-live-build.git
```

2.5. (optional) Work around a bug in metacity-1.30 which causes the Journal
to open raised on startup, obscuring the Activities page
(or you can press F3 when it does this)
```bash
src=https://snapshot.debian.org/archive/debian/20190910T220103Z/pool/main/m/metacity
dir=src/config/packages.chroot
arch=$(dpkg --print-architecture)
wget -P $dir \
    $src/metacity_3.34.0-1_$arch.deb \
    $src/libmetacity1_3.34.0-1_$arch.deb
    $src/metacity-common_3.34.0-1_all.deb \
```

3. Run the `build` script.
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
