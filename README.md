**Application**

[Arch Linux](https://www.archlinux.org/)

**Description**

Arch Linux is an independently developed, i686/x86-64 general purpose GNU/Linux distribution versatile enough to suit any role. Development focuses on simplicity, minimalism, and code elegance.

**Build notes**

Arch Linux image built "from scratch" using shim and ducktape (https://github.com/dock0/ducktape) to bootstrap. This image has been stripped down to reduce size and is ready to be used to build upon as a base, see binhex/arch-base for example.

**Instructions:**

1. [Build a 32 bit Arch Linux chroot](https://wiki.archlinux.org/index.php/Building_32-bit_packages_on_a_64-bit_system)
2. Log into the chroot with `archnspawn <CHROOT_DIR>/root bash`
3. Pack up the chroot into a tarball via the method described in the 2nd link ([Arch Linux from scratch](https://github.com/binhex/arch-scratch). 
4. Clear the pacman package cache to clean some space out with `paccache -r` (typically 6+ GB).
5. Create the tarball inside the chroot (size expected: 300 MB).

        mkdir -p /ext && tar -cvpjf /ext/root.tar.bz2 --exclude=/ext --exclude=/etc/hosts --exclude=/etc/hostname --exclude=/etc/resolv.conf --exclude=/sys --one-file-system /

6. Install `openssh` in the chroot
7. Transfer the tarball was via scp back to the original host with `scp /ext/root.tar.bz2 user@host:/home/user`
8. Build using the dockerfile with your host computer, located at ([Arch Linux from scratch](https://github.com/binhex/arch-scratch). Docker does not install (even though I've read you can with a good deal of hassle) on a 32 bit host

        docker build -f /path/to/a/Dockerfile .

9. Optional: remove openssh from the chroot to clean up
___
If you appreciate my work, then please consider buying me a beer  :D

[![PayPal donation](https://www.paypal.com/en_US/i/btn/btn_donate_SM.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=MM5E27UX6AUU4)

[Support Forum](http://lime-technology.com/forum/index.php?topic=45811.0)
