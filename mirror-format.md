# Formatting for http/https Mirror for netbooting

Set the URL of the mirror in `menus/boot.cfg`.

Can either be an subdomain, as in `boot.example.org`, or a path, such as `files.example.org/pxeboot`.

Please note that some files may be copyrighted, such as RHEL or Windows.



All Live Images expect a `vmlinuz`, an `initrd`, and a `squashfs` filesytem.

All Linux Installers expect at least a `vmlinuz` and an `initrd`. 

Specific documentation can be found below.

## **Path requirements for every file:**
In a somewhat tree style breakdown, with `menus/` being the root.
```
boot.cfg # Set mirror_url according to above
menu.ipxe # DO NOT TOUCH

tools/
    lspci.ipxe # DO NOT TOUCH
    pciids.ipxe # DO NOT TOUCH
    netinfo.ipxe # DO NOT TOUCH
    dban.ipxe # Needs DBAN.BZI in $mirror_url/DBAN.BZI, can change path by editing line 3.

live/
    debian.ipxe # Uses version names, path $mirror_url/debian/live/$version_name/ EX: buster

    fedora.ipxe # Uses version numbers and DEs, path $mirror_url/fedora/live/$version_number$DE_in_lowercase/ EX: 33gnome, 34kde
    
    kali.ipxe # One version, uses 'latest', path $mirror_url/kali/live/latest/

    popos.ipxe # Uses version number without dots, path $mirror_url/popos/live/$version_number/ EX: 20.04 LTS -> 2004, 21.04 -> 2104

install/
    alpine.ipxe # Uses version numbers prefixed by 'v', path $mirror_url/alpine/$version/ EX: 3.14 LTS -> v3.14

    debian.ipxe # Uses version names, path $mirror_url/debian/$version_name/ EX: buster

    fedora.ipxe # Uses version numbers, path $mirror_url/fedora/$version_number/ EX: 33, 34

    rhel.ipxe # Uses version numbers, path $mirror_url/rhel/$version_number/ EX: 7, 8

    ubuntu.ipxe # Uses version numbers without dots, path $mirror_url/ubuntu/$version_number/ EX: 20.04 LTS -> 2004, 21.04 -> 2104

    windows.ipxe # Uses version 'numbers', path $mirror_url/win/$version/ EX: Windows 10 -> W10, Server 2019 -> S2019
```

## **Specific documentation on required files:**

**`tools/dban.ipxe`:** `DBAN.BZI` can be found by downloading the latest version of DBAN in ISO format from https://dban.org/, mounting the ISO, and extracting the `dban.bzi` file.

**`live/debian.ipxe`:** Needs `filesystem.squashfs`, `initrd.img`, and `vmlinuz`. All of these can be found by downloading the latest LIVE-ISO from https://debian.org, mounting the ISO, and extracting those files from the `live/` directory within the ISO. `initrd.img` and `vmlinuz` may be suffixed by the kernel version.

**`live/fedora.ipxe`:** Needs `squashfs.img`, `initrd.img`, and `vmlinuz`. All of these can be found by downloading the DVD-ISO from https://getfedora.org, mounting the ISO. The `initrd.img` and `vmlinuz` files can be found in the path `images/pxeboot` within the ISO, and `squashfs.img` can be found within the `LiveOS/` directory.

**`live/kali.ipxe`:** Needs `filesystem.squashfs`, `initrd.img`, and `vmlinuz`. All of these can be found by downloading the latest Live Boot ISO from https://kali.org. All files can be found in the `live/` directory. `initrd.img` and `vmlinuz` may have copies suffixed by the kernel version.

**`live/popos.ipxe`:** Needs `filesystem.squashfs`, `initrd`, and `vmlinuz`. `filesystem.squashfs` can be found in an ISO downloaded from https://pop.system76.com/, in the `casper/` directory. However, both `initrd` and `vmlinuz` will have to be aquired from the netboot.xyz repositories. Download `initrd` and `vmlinuz` from https://github.com/netbootxyz/ubuntu-squash/releases/tag/5-66b7e861.

**`install/alpine.ipxe`:** Needs `modloop-lts`, `initramfs-lts`, and `vmlinuz-lts`. All of these can be found by downloading the netboot build from https://alpinelinux.org.

**`install/debian.ipxe`:** 