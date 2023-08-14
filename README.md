# dopinder-debian

Build script to build a Debian 12 image for the Walmart onn 4k UHD box (android codename dopinder), as well as all dependencies. This includes the following:

- Mainline Linux Kernel - [linux-6.5-rc6](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/tag/?h=v6.5-rc6)
- Mainline U-Boot - [v2023.10-rc2](https://github.com/u-boot/u-boot/tree/v2023.10-rc2)

Note that there are patches/modifications applied to the kernel and u-boot. The changes made can be seen in the `./patches` and `./overlay` directories. Also, a `./downloads` directory is generated to store a copy of the toolchain during the first build.

## Supported Boards
Currently images for the following devices are generated:
* Walmart onn 4K UHD Box

## Requirements

- The following packages below are required to use this build script. Note that this repo uses a Dockerfile to handle most of the heavy lifting, but some system requirements still exist.

`docker-ce losetup wget sudo make qemu-user-static`

Note that without qemu-user-static, debootstrap will fail!

## Usage
- Just run `make`.
- Completed builds output to `./output`
- To cleanup and clear all builds, run `make clean`

Other helpful commands:

- Have a build fail and have stale mounts? `make mountclean`
- Want to delete the download cache and do a 100% fresh build? `make distclean`

## Flashing
- Take your completed image from `./output` and extract it with gunzip
- Flash directly to a USB drive
  - `dd if=./debian-*.img of=/dev/mmcblk0 bs=2M conv=fdatasync`
- Plug it into your onn 4K UHD using an OTG cable, and hold the reset button while plugging in power.
- For future boots, you just need the USB drive plugged in during poweron. There is no more need to hold the reset button.

## To Do
* You tell me. Bug reports and PRs welcome!

## Notes
- This is a pet project that can change rapidly. Production use is not advised. Please only proceed if you know what you are doing!
