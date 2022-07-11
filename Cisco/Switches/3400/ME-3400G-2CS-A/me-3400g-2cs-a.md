# Cisco ME-3400G-2CS-A Switch

[Online Support Site](http://www.cisco.com/c/en/us/support/switches/me-3400g-2cs-a-switch/model.html)

[Online Firmware Download](https://software.cisco.com/download/release.html?mdfid=280779757&softwareid=280805680&os=&release=12.2.60-EZ8&relind=AVAILABLE&rellifecycle=&reltype=latest&i=!pp)

[Datasheet](Docs\product_data_sheet0900aecd8034fef3.pdf)

### Required tools:
- TFTP Server
- Console cable and USB to Serial connector
- Screwdrivers
- Cisco Compatible SFP

### Switch Inventory:

[Cisco 3400 Switch Kit](cisco_3400_kit.md)

## I. Physical

 

### External

Examine the outside of the switch and the bezel. If the top of the switch is scratched, remove and send to paint.  

Look for the following:

- Deep scratches

- Dents

- Bent ports

- Missing screws 

- SFP slot damage

- Serial stickers on back of switch

### Internal

**Note: Always hold fans in place while blowing air through them.**

Remove top and examine the inside of the switch. Clean thoroughly with compressed air. When the top is back on, clean top, bezel, and underside of switch with number 1.

Look for the following:

- Dirt or dust

- Leaking, bent, or otherwise defective components

- Rust

- Pay attention to all fans
	
## II. Functional

**Firmware: me340x-metroaccessk9-mz.122-60.EZ10.bin**

1. Set the device up at a workstation.  Telnet into `10.0.0.201` port `701X` where `X` is the number of the workstation.

1. Power the switch on and monitor the terminal. The switch should pass all POST tests and eventually display `Press RETURN to get started`.

1. Press Return. If asked to enter the initial configuration dialog, respond with no. The switch will display a prompt ending in `>`.

1. Enter the following:

	`enable`

	`configure terminal`

	`interface vlan 1`

	`ip address 10.0.0.1 255.255.255.0`

	`no shut`

	`interface GigabitEthernet 0/1`

	`media rj45`

	`switchport`

	`switchport mode access`

	`switchport access vlan 1`

	`no shutdown`

	`end`

	`format flash:`

1. Press Return and wait several moments until the format is complete.

1. Enter `copy ftp://user@10.0.0.45/me340x-metroaccessk9-mz.122-60.EZ10.bin flash:` to load the software.

1. Enter `show flash` to confirm the firmware copied correctly.

1. After the download is complete, enter `erase startup-config` followed by `reload`. The switch will ask to confirm the reload. If asked to save the running configuration, answer with no.

1. When console displays `*** The system will autoboot in 5 seconds ***
Send break character to prevent autobooting.`, press Alt + B or use your console to send a break.  The prompt should show up as `switch:`.

1. Enter `set` to see boot variables.  Enter the command `set BOOT flash:/me340x-metroaccessk9-mz.122-60.EZ10.bin`.  Enter `set` again afterwards to make sure it is now correctly defined.  Enter `reset` when finished.

1. The switch should pass all POST tests and eventually display `Press RETURN to get started`.

1. Press Return. If asked to enter the initial configuration dialog, respond with no. The switch will display a prompt ending in `>`.

1. Enter the following:

	`enable` 

	`configure terminal`

	`interface vlan 1`

	`ip address 10.0.0.1 255.255.255.0`

	`no shutdown`

	`interface range gigabitEthernet 0/1 - 2`

	`media-type rj45`

	`switchport`

	`switchport mode access`

	`switchport access vlan 1`

	`no shutdown`

	`interface range gigabitEthernet 0/3 - 4`

	`switchport`

	`switchport mode access`

	`switchport access vlan 1`

	`no shutdown`

	`end`

1. Ping each port from a command prompt **(cmd.exe in Windows)** with <1500 bytes.  Use the command `ping -t -l 1200 10.0.0.1` in Windows.

1. Test the Port 1-2 SFPs last by entering:

	`configure terminal`

	`interface range gigabitEthernet 0/1 - 2`

	`media-type sfp`

	`shutdown`

	`no shutdown`

	`end`

1. After all ports are tested, enter `erase startup-config` and confirm the action when prompted.  Enter `reload`.  Unplug any ethernet cables used for testing.  When the switch reboots, capture a `show tech-support | redirect flash:(Serial Number).txt`.  

1. Repeat the configuration for port 0/4 to upload the text file to the tftp server.

1. Enter `copy flash tftp`, and input the correct file name and ip address when prompted.  Delete the text file from flash after copying using `delete flash:(filename)`.  

1. Enter `erase startup-config` and `reload` one last time.  The switch can be unplugged when it starts to reboot. 

## III. Packing

1. Do a final cleaning of fingerprints and apply inventory and Network Craze stickers upon certification that the switch is fully complete. Include the correct kit [Cisco 3400 Switch Kit](cisco_3400_kit.md).

	- Inventory stickers go as far to the upper left corner of the bottom of the switch as possible, (accounting for screws, indents, etc.) in the same orientation as the rest of the stickers.  Network Craze stickers go directly below inventory stickers aligned with the left edge of the inventory sticker.

1. Seal switch in anti-static bag to be packed for shipping.
