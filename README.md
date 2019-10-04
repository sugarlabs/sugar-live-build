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
[Downloads](http://people.sugarlabs.org/~quozl/sugar-live-build-20171009/).

## How to rebuild

1. Install Debian 10 Buster;

2. Clone this repository;
```bash
git clone https://github.com/sugarlabs/sugar-live-build.git
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
