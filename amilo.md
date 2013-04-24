---
layout: default
title: Amilo A7645
aliases: ['/web/7/index.html', '/web/amilo.html']
sitemap: {priority: 0.2, changes: monthly}
---
## Hardware

<table>
  <tr>
    <td>AMD Turion MT-28 1.6 Ghz </td>
    <td> Works </td>
    <td> had to manually load powernow-k8 module</td>  
  </tr>
  <tr>
    <td>15 inch TFT Display, 1024x768 pixels </td>
    <td> Works </td>
    <td> selected generic flat panel 1024x768</td>
  </tr>
  <tr>
    <td>SIS M760 integrated video card </td>
    <td> Works </td>
    <td> selected &quot;sis&quot; driver in XFree86 config</td>
  </tr>
  <tr>
    <td>2x512 MB </td>
    <td> Works </td>
    <td> -</td>
  </tr>
  <tr>
    <td>60 GB IDE hard disk </td>
    <td> Works </td>
    <td> -</td>
  </tr>
  <tr>
    <td>Firewire/IEEE1394 </td>
    <td> Not tried </td>
    <td> detected by kernel, probably works</td>
  </tr>
  <tr>
    <td>Integrated Network Card </td>
    <td> Works </td>
    <td> -</td>
  </tr>
  <tr>
    <td><a href="#modem">Internal 56k Modem</a> </td>
    <td> Works </td>
    <td> using ALSA + Intel 8x0 driver + slmodemd</td>
  </tr>
  <tr>
    <td>DVD writer </td>
    <td> Works </td>
    <td> -</td>
  </tr>
  <tr>
    <td><a href="#wireless">Internal WLAN</a> </td>
    <td> Works </td>
    <td> -</td>
  </tr>
  <tr>
    <td>Battery </td>
    <td> Works </td>
    <td> added ec_burst=1 to kernel parameters</td>
  </tr>
  <tr>
    <td><a href="#touchpad">Touchpad</a> </td>
    <td> In progress </td>
    <td> some remaining problems</td>
  </tr>
  <tr>
    <td><a href="#power">Power management</a> </td>
    <td> In progress </td>
    <td> mostly works</td>
  </tr>
</table>

## Software

<p>Debian GNU/Linux 3.1 &quot;Sarge&quot; for AMD64 upgraded to 4.0 &quot;Etch&quot;</p>
<p>Installed an i386 chroot as per instructions in <a href="https://alioth.debian.org/docman/view.php/30192/21/debian-amd64-howto.html#id271960">The Debian GNU/Linux AMD64 HOW-TO</a>. Using self-compiled 2.6.27 kernel.</p>

## Modem <a name="modem" />

<p>I downloaded the <a href="http://www.xs4all.nl/~pjl/slmodemd/slmodemd-2.9.9e_pre1_alsa-4.FC4.LC.x86_64.rpm ">binary packages for x86_64/Fedora Core 4</a> and converted them to DEB format using Alien.</p>
<p>Debian correctly identifies the soundcard and loads the snd-intel8x0 and snd-intel8x0m drivers and the ac97 codecs.</p>
<p>To use the modem I need to run slmodemd --country=ITALY --alsa --daemon and change pppd config to use /dev/ttySL0 (wvdial does this automatically).</p>

## Touchpad <a name="touchpad" />

<p>For Debian the driver is packaged as xfree86-driver-synaptics; installation instructions are under /usr/share/doc/xfree86-driver-synaptics/. As an alternative, you can <a href="http://web.telia.com/~u89404340/touchpad/files/">download the sources for the Synaptics driver</a>; it is then necessary to modify XF86Config/xorg.conf <a href="http://web.telia.com/~u89404340/touchpad/xorg.conf">as demonstrated here</a>.</p>

## Power management <a name="power" /> 

<p>Suspend to disk (S4) works using the stock 2.6.15 kernel. There seem not to be any problems.</p>

<p>Suspend to RAM (S3) works after adding acpi_sleep=s3_bios,s3_mode to the kernel boot parameters. The notebook only wakes up when pressing the power button hence I had to substitute the poweroff.sh script included with acpid as packaged by Debian.</p>
<p>My /usr/bin/suspend.ram script (to be run as root):</p>
<pre>
#!/bin/sh

touch /var/run/suspend.ram
echo -n mem > /sys/power/state
</pre>
<p>My /etc/acpi/powerbtn.sh script:</p>
<pre>
#!/bin/sh

if test -e /var/run/suspend.ram; then
    ( /bin/sleep 5; /bin/rm -rf /var/run/suspend.ram ) &amp;
else
    /sbin/shutdown -h now "Power button pressed"
endif 
</pre>
<p>Standby (S1) works with 2.6.16/2.6.17 kernels. Sometimes the notebook enters standby when the lid is closed even if attached to AC (happened with 2.6.12, seems to be fixed in 2.6.15).</p>
<p>DPMS turns off the display but fails to turn off the backlight hence the screen becomes completely white (and I suspect there is near-zero power saving).</p>

## Wireless <a name="wireless"/>

<p>Works using  kernel 2.6.15.5, ndiswrapper 1.10, <a href="ftp://ftp.support.acer-euro.com/notebook/aspire_3020_5020/driver/winxp64bit/">64 bit Windows drivers for ACER Aspire</a>.</p>
<p>Not tried with a 32 bit OS but it should work. It did not work with older kernels/ndiswrapper versions.</p>
