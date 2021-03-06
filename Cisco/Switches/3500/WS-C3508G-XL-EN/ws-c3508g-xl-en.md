# WS-C3508G-XL-EN

Website Deprecated

### Required tools:
- TFTP Server
- Console cable and USB to Serial connector
- Screwdrivers
- Testing GBIC
- Testing Fiber SFP
- SC to LC Fiber

### Inventory:

[Cisco 3500 Switch Kit](Cisco_3500_kit.md)

## I. Physical

### External

Examine the outside of the switch and the bezel. If the top of the switch is scratched, remove and send to paint.  

Look for the following:

- Deep scratches

- Dents

- Bent ports

- GBIC slot damage

- Serial stickers on rear of switch

- Missing screws (The screw pattern for 3500 switches is as follows:)
	- Left side: (3 total) 1 screw in front, middle, and back along the bottom
	- Right side: (3 total) 1 screw in front, middle, and back along the bottom
	- Back: (5 total) 1 small screw in each hole

### Internal

**Note: Always hold fans in place while blowing air through them.**

Remove top and examine the inside of the switch. Clean thoroughly with compressed air. When the top is back on, clean top, bezel, and underside of switch with number 

Look for the following:

- Dirt or dust

- Leaking, bent, or otherwise defective components

- Rust

- Pay particular attention to all fans
	
## II. Functional

**Firmware: c3500xl-c3h2s-mz.120-5.WC17.bin**

1. Set the device up at a workstation.  Telnet into `10.0.0.201` port `701X` where `X` is the number of the workstation.

1. Power the switch on and monitor the terminal. Wait until the switch displays `Press RETURN to get started`.

1. Press Return. If asked to enter the initial configuration dialog, respond with no. The switch will display a prompt ending in `>`.

1. Enter `enable` and press Return. The prompt should change to `# `.

1. Enter `show post` and make sure all POST tests passed.

1. Enter the following:

	`configure terminal`

	`no spanning-tree`

	`interface vlan 1`

	`ip address 10.0.0.1 255.255.255.0`

	`no shutdown`

	`end`

1. Enter `format flash:`. The switch will prompt you to confirm the action. Press Return and wait several moments until the format is complete.

1. Insert a GBIC into slot 1 and connect it to a 1G fiber SFP in the testing network.

1. Enter `copy tftp flash`. The source IP address should be entered as `10.0.0.45`. The source filename should be pasted in. Press Return for all other prompts and wait for the switch to download the new image.

1. Enter `show flash` to confirm the firmware copied correctly.

1. After the download is complete, enter `erase startup-config` followed by `reload`. The switch will ask to confirm the reload. If asked to save the running configuration, answer with no.

1.  Monitor the switch while booting.  The switch should pass all POST tests and eventually display `Press RETURN to get started`.

1. Press Return. If asked to enter the initial configuration dialog, respond with no. The switch will display a prompt ending in `>`.

1. Enter `enable` and press Return. The prompt should change to `# `.

1. Repeat configuration for all ports to get the switch ready for port testing.  Use the following commands:

	`configure terminal`

	`no spanning-tree`

	`interface vlan 1`

	`ip address 10.0.0.1 255.255.255.0`

	`no shutdown`

	`end`

1. Plug the testing GBIC into slot 1, and the SC to LC fiber into that GBIC.

1. Set up a second switch with a normal SFP slot and insert a Network Craze 1G Fiber SFP in for testing.  Configure that switchport as access and turn portfast on.

1. Ping between the switches using `ping 10.0.0.3` from the `switch# ` menu of the original switch.

1. Ping ports 11 and 12 using the standard method `ping -t -l 1200 10.0.0.1` in Windows or `ping -a -t 1200 10.0.0.1` on a Mac.

1. After all ports are tested, enter `erase startup-config` and confirm the action when prompted.  Enter `reload`.  Unplug any ethernet cables used for testing.  When the switch reboots, capture a `show tech-support` using the console log.  

1. Enter `erase startup-config` and `reload` one last time.  The switch can be unplugged when it starts to reboot. 
## III. Packing

1. Do a final cleaning of fingerprints and apply inventory and Network Craze stickers upon certification that the switch is fully complete. Include the correct kit as well.

	- Inventory stickers go as far to the upper left corner of the bottom of the switch as possible, (accounting for screws, indents, etc.) in the same orientation as the rest of the stickers.  Network Craze stickers go directly below inventory stickers aligned with the left edge of the inventory sticker.
	
1. Seal switch in anti-static bag to be packed for shipping.
