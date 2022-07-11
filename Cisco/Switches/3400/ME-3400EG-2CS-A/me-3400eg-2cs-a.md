# Cisco ME-3400EG-2CS-A Switch

### Required tools:
- TFTP Server
- Console cable and USB to Serial connector
- Screwdrivers
- Cisco Compatible SFP

### Inventory:

## I. Physical

 

### External
- Examine the outside of the switch and the bezel. If the top of the switch is scratched, remove and send to paint.  
Look for the following:
	- Deep scratches
	- Dents
	- Bent ports
	- Missing screws 
	- SFP slot damage
	- Serial stickers on back of switch

### Internal

- Remove top and examine the inside of the switch. Clean thoroughly with compressed air. When the top is back on, clean top, bezel, and underside of switch with number 1. Look for the following:
	- Dirt or dust
	- Leaking, bent, or otherwise defective components
	- Rust
	
## II. Functional

**Firmware: me340x-metroaccessk9-mz.122-60.EZ6.bin**

1. Set the device up at a workstation.  Telnet into `10.0.0.201` port `701X` where `X` is the number of the workstation. Connect the TFTP server to the switch via the `MGMT 10/100` port.

1. Power the switch on and monitor the terminal. The switch should pass all POST tests and eventually display `Press RETURN to get started`.

1. Press Return. If asked to enter the initial configuration dialog, respond with no. The switch will display a prompt ending in `>`.

1. Enter `enable` and press Return. The prompt should change to `# `.

1. Enter:

	`configure terminal`

	`interface FastEthernet 0`

	`ip address 10.0.0.1 255.255.255.0`

	`no shutdown`

	`end`

1. Enter `format flash:`. The switch will prompt you to confirm the action. Press Return and wait several moments until the format is complete.

1. Enter `copy tftp flash`. The source IP address should be entered as `10.0.0.45`. The source filename should be pasted in. Press Return for all other prompts and wait for the switch to download the new image.

1. Enter `show flash` to confirm the firmware copied correctly.

1. After the download is complete, enter `erase startup-config` followed by `reload`. The switch will ask to confirm the reload. If asked to save the running configuration, answer with no.

1. The switch should pass all POST tests and eventually display `Press RETURN to get started`.

1. Press Return. If asked to enter the initial configuration dialog, respond with no. The switch will display a prompt ending in `>`.

1. Enter `enable` and press Return. The prompt should change to `# `.

1. Enter:
 
	`configure terminal`

	`interface vlan 1`

	`ip address 10.0.0.1 255.255.255.0`

	`no shutdown`

	`interface range gigabitEthernet 0/1 -2`

	`media-type rj45`

	`no shutdown`

	`interface range gigabitEthernet 0/3 -4`

	`no shutdown`

1. Ping each port with 64 bytes. Use a Network Craze test SFP to ping SFP slots 3 and 4. SFP slots 1 and 2 do not accept any RJ45 SFP.

1. After all ports are tested, enter `erase startup-config` and confirm the action when prompted. Enter `reload`. Unplug any ethernet cables used for testing. When the switch reboots, capture a `show tech-support | redirect flash:(Serial Number).txt`.  

1. Enter `copy flash tftp`, and input the correct file name and ip address when prompted. Delete the text file from flash after copying using `delete flash:(filename)`.  

1. Enter `erase startup-config` and `reload` one last time. The switch can be unplugged when it starts to reboot. 

## III. Packing

1. Do a final cleaning of fingerprints and apply inventory and Network Craze stickers upon certification that the switch is fully complete. Include the correct kit.

	- Inventory stickers go as far to the upper left corner of the bottom of the switch as possible, (accounting for screws, indents, etc.) in the same orientation as the rest of the stickers. Network Craze stickers go directly below inventory stickers aligned with the left edge of the inventory sticker.

1. Seal switch in anti-static bag to be packed for shipping.
