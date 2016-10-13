# node-red-contrib-usbhid

A node-hid (USB HID device access library) wrapper for nodered

Credit goes to node-hid. 

You can look up either git to find information on setup, Prerequisites and Platforms to get the node working:
https://github.com/node-hid/node-hid


### Prerequisites:

* [Node.js](https://nodejs.org/) v0.8 - v4.x+
* Mac OS X 10.8, Linux (kernel 2.6+), and Windows XP+
* libudev-dev, libusb-1.0-0-dev (if Linux, see Compile below)
* [git](https://git-scm.com/)

node-hid uses node-pre-gyp to store pre-built binary bundles, so usually no compiler is needed to install.

Platforms we pre-build binaries for:
- Mac OS X x64: v0.10, v0.12, v4.2.x
- Windows x64 & x86: v0.10, v0.12, v4.2.x
- Linux Debian/Ubuntu x64: v4.2.x
- Raspberry Pi arm: v4.2.x

## How to Use

### HID ( USB ) read/write access for non root users ( in my case for user pi on an raspberry pi 2 running nodered )

The Pd-extended [hid] object allows you to access Human Interface Devices such as mice, keyboards, and joysticks. However, in most Linux distributions, these devices are setup to where they cannot be read/written directly by Pd unless you run it as root.

Running a non-system process as root is considered a security risk, so an alternative is to change the permissions of the input devices so that pd can read/write them.

```
sudo mkdir -p /etc/udev/rules.d
sudo nano /etc/udev/rules.d/85-pure-data.rules
```
Now add the following rules to /etc/udev/rules.d/85-pure-data.rules:

```
SUBSYSTEM=="usb", GROUP="input", MODE="777"
```

Then create an "input" group and add yourself to it:

```
sudo groupadd -f input
sudo gpasswd -a YOURUSERNAME input
```
Reboot your machine for the rules to take effect.
Your nodejs / nodered has now FULL ACCESS !! to you usb devides. Feel free to adjust the permissions to fit your needs.

