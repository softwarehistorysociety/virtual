# "Dell UNIX Lives Again! | Fun with virtualization"

*07-06-2021 07:06* 

> (please note that this is a guest post from Antoni Sawicki)
*(please note that this is a guest post from Antoni Sawicki)*

Dell UNIX is so ultra rare among rare Unix species that it doesn’t even have a Wikipedia entry. I have been hunting this elusive but important piece of computer history for well over 15 years now. Fortunately thanks to Charles H. Sauer and his [excellent blog post](http://technologists.com/notes/2008/01/10/a-brief-history-of-dell-unix/) I was finally able to lay my hands on disk and tape images and the restoration process begun.

[![](https://virtuallyfun.com/wordpress/wp-content/uploads/2012/03/1992DellSVR42-300x196.jpg "1992DellSVR42")](https://virtuallyfun.com/wordpress/wp-content/uploads/2012/03/1992DellSVR42.jpeg)

The install tape

The system can be installed from either a tape or network server (presumably NFS). Unfortunately no virtualization software can emulate a tape drive. Hopes for a network install are even slimmer since the required network support floppy disk has been lost and chances of suitable Ethernet driver working in Bochs or Qemu are equal to that of finding the lost floppy disk.

I have decided to try a hard disk image from a readily pre-installed system. The original Dell 486 workstation had a 1GB SCSI hard disk. Unfortunately neither Dell UNIX supports LBA mode nor Qemu/Bochs support the Adaptec 154x controller required by the OS.

As all normal install options have been exhausted, the only option left was to use a second hard disk image as source of cpio archive files. Booting from the two install floppies and attaching two disk images was a snap. The next step was to inject the tape “file” in to a right place on the disk, so it can be read by cpio command. A hard disk in Dell UNIX is pretty much unusable without a valid SysV partition and VTOC. Fortunately *dellsetup* command does it all for you. Once VTOC was put in place I’ve attached the transfer disk image as a loopback device in my host OS. In couple of iterations I was able to aim the host os *dd if=file1 of=/dev/loop0 bs=512 seek=offset* at the right place, which you work out using *prtvtoc /dev/rdsk/1s0* command. Then *cpio -ict < /dev/dsk/1s1* was able to list contents of the emulated tape… with errors…

In my infinite wisdom, for some unknown reason I’ve assumed that LBA addressing is required above 540MB. So to be on a safe side I have made the hard disk images 512 MB. What a mistake it was! I have lost several hours trying to figure out cpio header errors coming from the disk… By pure coincidence, while the tape archive was installing (with errors) I was researching for this very blog article and found that LBA starts at 504 MB… Recreating the hard disk images just few MB smaller took all tape and prior boot problems away!

Once the cpio archive was extracted I have made few final touches taken from the original tape install script. After a reboot Dell UNIX booted perfectly. You can experience this by using the firstboot image file. The final part of installation was injecting the second tape file containing System V PKG file to the transfer disk image and running *pkgadd -d /dev/dsk/1s1*. This is what’s included on allsoft.img.

[![](https://virtuallyfun.com/wordpress/wp-content/uploads/2012/03/dellunix.png "dellunix")](https://virtuallyfun.com/wordpress/wp-content/uploads/2012/03/dellunix.png)

Dell Unix at First Boot

Some final notes on running the OS:

-   To enable mouse to work:
    -   Qemu just add “*\-chardev msmouse,id=msmouse -device isa-serial,chardev=msmouse*” to the launch arguments.
    -   Bochs add to the config file:  
        *mouse: type=serial, enabled=1*   
        *com1: enabled=1, mode=mouse*  
        then you have to kill *mousemgr* process and prevent from starting by deleting */etc/rc2.d/S25mse*  
        then edit /usr/lib/X11/Xconfig:  
        *disable Xqueue*   
        *enable Microsoft Mouse*
-   To enable keyboard to work correctly in VirtualBOX start with Num Lock OFF.
-   You can use qemu-img utility to [convert the image](https://virtuallyfun.com/?p=436) to VMware vmdk to use in VirtualBox.
-   To run X window type startx

[![](https://virtuallyfun.com/wordpress/wp-content/uploads/2012/03/dellunix-x11.png "dellunix-x11")](https://virtuallyfun.com/wordpress/wp-content/uploads/2012/03/dellunix-x11.png)

X11 and all its glory

-   To attach it to internet use SLIP as there is no working Ethernet driver.  Contrary to most UNIXen of the time, the command is not *slattach*, but rather *slipattach*.  Thankfully it does work the same way.  I have found that running Dell Unix with VirtualBOX, along with Windows NT 4.0 I was able to connect into the Dell Unix VM, and get network access.  Just set the two VM’s up for a named pipe (\\\\.\\pipe\\dellunix) and make one of them a server, and start that VM 1st.  The steps to prepare Windows NT have been [outlined before](https://virtuallyfun.com/?p=216).

[![](https://virtuallyfun.com/wordpress/wp-content/uploads/2012/03/SLIP-into-dell-UNIX.png "SLIP into dell UNIX")](https://virtuallyfun.com/wordpress/wp-content/uploads/2012/03/SLIP-into-dell-UNIX.png)

Telnet via SLIP

Legal disclaimer: Dell UNIX is a commercial software and should not be distributed without manufacturers permission. However as the operating system has been dead for 20 years and with a long tradition from Unix Heritage Society and Bitsavers I’m publishing this in good faith under [abandonware](https://virtuallyfun.com/?p=1692) category. If Dell or any other copyright holder wishes this software removed, please let me know.

Attached are:

-   firstboot image
-   all (pkg) software installed
-   setup instructions if you wish to install from scratch.

Download:

-   [Bochs / QEMU Image](http://tenox.pdp-11.ru/dellunix/dellunix-bochs-qemu.7z) ([vpsland mirror](https://vpsland.superglobalmegacorp.com/install/DELLUnix/dellunix-bochs-qemu.7z))
-   [VirtualBox / OVA](http://tenox.pdp-11.ru/dellunix/DellUnix.ova)

You may also be interested in my post about a sister System V operating system – [Interactive UNIX](https://virtuallyfun.com/?p=197):

**Update**: Dell Unix now [runs on 86Box](https://virtuallyfun.com/wordpress/2020/12/01/dell-unix-on-86box/) with higher resolution and proper networking.
***

==**4821**== Words

- **[Dell UNIX Lives Again! | Fun with virtualization](https://virtuallyfun.com/wordpress/2012/03/20/dell-unix-lives-again/)**
