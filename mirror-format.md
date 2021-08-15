# Formatting for HTTP/HTTPS Mirror for netbooting

Set the URL of the mirror on line 15 of `menus/menu.ipxe`. It defaults to the root of the server that loaded the iPXE menu.

Can either be an subdomain, as in `boot.example.org`, or a path, such as `files.example.org/pxeboot`.

Please note that some files may be copyrighted, such as RHEL or Windows.



All Live Images expect a `vmlinuz`, an `initrd`, and a `squashfs` filesystem.

All Linux Installers expect at least a `vmlinuz` and an `initrd`. 

Specific documentation can be found below.

# **Path requirements for every file:**
In a somewhat tree style breakdown, with `menus/` being the root.
```
boot.cfg # Set mirror_url according to above
menu.ipxe # DO NOT TOUCH

tools/
    lspci.ipxe # DO NOT TOUCH
    pciids.ipxe # DO NOT TOUCH
    netinfo.ipxe # DO NOT TOUCH
    dban.ipxe # Needs DBAN.BZI in $mirror_url/DBAN.BZI, can change path by editing line 3.
    memtest.ipxe # single version, path $mirror_url/memtest/
    clonezilla.ipxe # single version, path $mirror_url/clonezilla/

live/
    debian.ipxe # Uses version names, path $mirror_url/debian/live/$version_name/ EX: buster

    fedora.ipxe # Uses version numbers and DEs, path $mirror_url/fedora/live/$version_number$DE_in_lowercase/ EX: 33gnome, 34kde
    
    kali.ipxe # One version, uses 'latest', path $mirror_url/kali/live/latest/

    popos.ipxe # Uses version number without dots, path $mirror_url/popos/live/$version_number/ EX: 20.04 LTS -> 2004, 21.04 -> 2104

install/
    alpine.ipxe # Uses version numbers prefixed by 'v', path $mirror_url/alpine/$version/ EX: 3.14 LTS -> v3.14

    debian.ipxe # Uses version names, path $mirror_url/debian/$version_name/ EX: buster

    kali.ipxe # Uses a single version name, latest, path $mirror_url/kali/latest/

    fedora.ipxe # Uses version numbers, path $mirror_url/fedora/$version_number/ EX: 33, 34

    rhel.ipxe # Uses version numbers, path $mirror_url/rhel/$version_number/ EX: 7, 8

    ubuntu.ipxe # Uses version numbers without dots and the type, path $mirror_url/ubuntu/$version_number-$version_type/ EX: 20.04 LTS Server-> 2004-server, 21.04 Desktop -> 2104-desktop

    windows.ipxe # Uses version 'numbers', path $mirror_url/win/$version/ EX: Windows 10 -> W10, Server 2019 -> S2019
```

# **Specific documentation on required files:**

## **`tools/dban.ipxe`:** 
`DBAN.BZI` can be found by downloading the latest version of DBAN in ISO format from https://dban.org/, mounting the ISO, and extracting the `dban.bzi` file.

## **`tools/memtest.ipxe`:**
Needs `memdisk` and `memtest.iso`. `memtest.iso` can be found by downloading the latest ISO from https://memtest.org/, and renaming the ISO to `memtest.iso`
`memdisk` can be found by downloading `syslinux` version 5.10, found [here](https://www.kernel.org/pub/linux/utils/boot/syslinux/syslinux-5.10.zip). `memdisk` will be found in the `memdisk/` directory within the archive.

Place both files in the base of the designated mirror path.

## **`tools/clonezilla.ipxe`:**
Needs `filesystem.squashfs`, `initrd.img`, and `vmlinuz`. All of these can be found by downloading the latest ZIP from https://clonezilla.org.

All files will be found within the `live/` directory within the archive. 

Place all files in the base of the designated mirror path.

# **Live Images:**

## **`live/debian.ipxe`:** 
Needs `filesystem.squashfs`, `initrd.img`, and `vmlinuz`. All of these can be found by downloading the latest LIVE-ISO from https://debian.org, mounting the ISO.

All files will be found within the `live/` directory within the ISO. `initrd.img` and `vmlinuz` may be suffixed by the kernel version. 

Place all files in the base of the designated mirror path.

## **`live/fedora.ipxe`:** 
Needs `squashfs.img`, `initrd.img`, and `vmlinuz`. All of these can be found by downloading the DVD-ISO from https://getfedora.org, mounting the ISO. 

The `initrd.img` and `vmlinuz` files can be found in the path `images/pxeboot` within the ISO, and `squashfs.img` can be found within the `LiveOS/` directory. 

Place all files in the base of the designated mirror path.

## **`live/kali.ipxe`:** 
Needs `filesystem.squashfs`, `initrd.img`, and `vmlinuz`. All of these can be found by downloading the latest Live Boot ISO from https://kali.org. 

All files can be found in the `live/` directory. `initrd.img` and `vmlinuz` may have copies suffixed by the kernel version. 

Place all files in the base of the designated mirror path. 

## **`live/popos.ipxe`:** 
Needs `filesystem.squashfs`, `initrd`, and `vmlinuz`. `filesystem.squashfs` can be found in an ISO downloaded from https://pop.system76.com/, in the `casper/` directory. 

However, both `initrd` and `vmlinuz` will have to be acquired from the `netboot.xyz` repositories. Download `initrd` and `vmlinuz` from [here](https://github.com/netbootxyz/ubuntu-squash/releases/tag/5-66b7e861). 

Place all files in the base of the designated mirror path.

# **Installers:**

## **`install/alpine.ipxe`:** 
Needs `modloop-lts`, `initramfs-lts`, and `vmlinuz-lts`. 
All of these can be found by downloading the netboot build from https://alpinelinux.org. 

Place all files in the base of the designated mirror path.

## **`install/debian.ipxe`:** 
Needs `initrd.gz` and `linux`. These can both be found at [this place in the Debian repos](https://deb.debian.org/debian/dists/buster/main/installer-amd64/current/images/netboot/debian-installer/amd64/) for buster. 
Place both files in the base of the designated mirror path.

## **`install/kali.ipxe`:**
Needs `initrd.gz` and `linux`. These can both be found in [This archive](http://http.kali.org/kali/dists/kali-rolling/main/installer-amd64/current/images/netboot/netboot.tar.gz), and in the folder structure `debian-installer/amd64` within the archive.
Place both files in the base of the designated mirror path.

## **`install/esxi.ipxe`:**
Needs the ISOs from VMware's website. Also needs `memdisk` which can be found in the same place as for memtest86+. Place all files in the base of the mirror path.

## **`install/fedora.ipxe`:** 
Needs `vmlinuz`, `initrd.img`, and `install.img`. All of these can be found by downloading the Fedora Server netinst image(don't worry, it can do Workstation too!), and mounting the ISO. 

`vmlinuz` and `initrd.img` will be in the `images/pxeboot/` directory, and `install.img` will be in the `images/` directory. 

Place `vmlinuz` and `initrd.img` in the base of the designated mirror path, and place `install.img` inside of an `images` directory.

## **`install/rhel.ipxe`:** 
Needs `vmlinuz`, `initrd.img`, and `install.img`. I will not cover how to get access to RHEL ISOs, but you will want to download the sub 1G `boot.iso`. 

Mount this ISO, and inside the `images/pxeboot/` directory you will find `vmlinuz` and `initrd.img`. `install.img` will be found in the `images/` directory. 

Place `vmlinuz` and `initrd.img` in the base of the designated mirror path, and place `install.img` inside of an `images` directory.

## **`install/ubuntu.ipxe`:** 
Needs `initrd`, `vmlinuz`, and a copy of the live ISO for the version you want. 

Download the Live ISO, and mount it. Inside the `casper/` directory you will find the `initrd` and `vmlinuz` files. Make a copy of the ISO and rename it `ubuntu.iso`. 

Copy `initd`, `vmlinuz`, and `ubuntu.iso` to the base of the designated mirror path.

## **`install/windows.ipxe`:** 
You will need `wimboot` to be able to boot Windows. `wimboot` can be found [here](https://github.com/ipxe/wimboot/releases/latest/download/wimboot), and will need to be placed at the base of the designated mirror path. 

For each version of Windows you want, EX; Server 2019 and Windows 10, make a folder inline with the naming scheme in the base of the designated mirror path. `Server 2019 -> S2019 | Windows 10 -> W10`.

I will not cover where to acquire Windows or Windows Server ISOs, this assumes you have them.

Mount the ISO for the wanted version, and copy all contents of the ISO into the directory for the version.