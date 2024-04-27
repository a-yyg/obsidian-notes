#draft 
[`systemd`](https://en.wikipedia.org/wiki/Systemd) is a system and service manager.
It provides the following three general functions:
- A system and service manager
- A software platform
- The glue between applications and the kernel

```d2
title: Boot Sequence {
	shape: text
	near: top-center
	style: {
		font-size: 55
	}
}
direction: right

p1: {
	label: ""
	direction: right
	Turn On Power -> Boot BIOS/UEFI -> Load Bootloader -> _.p2.Load Kernel
}
p2: {
	label: ""
	ex: {
		label: ""
		Execute Processes {
			style.fill: transparent
			style.stroke: transparent
			systemd startup
		}
	}
	Login <- ex <- Load Kernel
}
```

Read up on [this](https://qiita.com/ryonryon1802/items/987b886a4ba75f4a0145) to complete this page.