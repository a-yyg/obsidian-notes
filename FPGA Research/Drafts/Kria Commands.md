#draft
## `dtc` - [[Device Tree]] Compiler
### Man Page
```
DTC(1)                                           General Commands Manual                                           DTC(1)

NAME
       dtc - Device Tree Compiler

SYNOPSIS
       /usr/bin/dtc [options] <input file>

DESCRIPTION
       Device  Tree  Compiler,  dtc,  takes as input a device-tree in a given format and outputs a device-tree in another
       format for booting kernels on embedded systems.  Typically, the input format is "dts",  a  human  readable  source
       format, and creates a "dtb", or binary format as output.
```
### Usage: Obtaining the Device Tree
```sh
sudo dtc /sys/firmware/fdt 2> /dev/null > system.dts
```
### Usage: Generating a `dtb` from a `dts`
```sh
dtc -I dts -O dtb system.dts -o system.dtb
```
# [[systemd]]
## `multi-user.target`
This is necessary for using [SmartCam](https://github.com/Xilinx/smartcam). #why

```sh
sudo systemctl set-default multi-user.target
```
## `graphical.target`

```sh
sudo systemctl set-default graphical.target
```
