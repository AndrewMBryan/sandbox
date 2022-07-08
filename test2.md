# ISR 4331 Router

[Online Support Site]()

[Online Firmware Download]()

[Data Sheet]()

### Required tools:

- Testing SFP

### Inventory:

[ISR 4431 Router Kit](isr_4351_kit.md)

## I. Physical

 

### External

Examine the outside of the router and the faceplate. If the top of the router is scratched, remove and send to paint.  

Look for the following:

- Bent corners
- Deep scratches
- Dents
- Bent ports
- Missing screws
- SFP slot damage
- Serial stickers on rear of router

### Internal

**Note: Always hold fans in place while blowing air through them.**

Remove top and examine the inside of the router. Clean thoroughly with compressed air. When the top is back on, clean top, faceplate, and underside of router with number 

Look for the following:

- Dirt or dust
- Leaking, bent, or otherwise defective components
- Rust
- Pay particular attention to all fans
	
## II. Functional

**Firmware: isr4300-universalk9.17.03.05.SPA.bin** *Note: If version is at 3.x, upgrade to 16.6.7 first, then upgrade to this version*

**ROMMON: isr4200_4300_rommon_1612_2r_SPA.pkg**

**Firmware_Step: isr4300-universalk9.16.06.07.SPA.bin** => *Use this version for disaster recovery*

1. Set the device up at a workstation.  Telnet into `10.0.0.201` port `701X` where `X` is the number of the workstation.

1. Power the router on and monitor the terminal. Wait until the router displays `Press RETURN to get started`.

1. Press Return. If asked to enter the initial configuration dialog, respond with no. The router will display a prompt ending in `>`.

	### BEGIN PASSWORD RECOVERY STEPS ###

	*If the device boots with a password, it needs to be removed. Follow the below instructions to remove:*

	1. Turn the device off, either by unplugging said device or turning it off with the switch, then either plug it in or turn it back on.
 
	1. Hold down `CTRL` and continuously hit `C`. You should eventually see `rommon 1>`

		*If this does not work, hold down `ALT` and continuously hit `B`.*

		1. If this method is used, enter `confreg 0x140`, then `reset`.

	1. From here, enter `unset BOOT`

	1. Next, enter `confreg 0x2142`.

	1. Enter `boot`.

	1. Wait for the device to boot fully.

	### END PASSWORD RECOVERY STEPS ###

1. Enter `enable` and press Return. The prompt should change to `# `.

1. Before proceeding further, enter `show license feature`. You should see `yes` under "Enabled" listed for ipbasek9.

1. Enter `show version` to check the amount of RAM in the device. It should have at least 4GB (4096MB). If it doesn't, it will have to be updated first.

1. Using the output from the previous command, look at the `Configuration register` area. If it is anything other than 0x2102, enter the following to change it:

	1. `configure terminal`

	1. `config-register 0x2102`

	1. `end`

	1. `write`

	1. `reload`

1. After the router reloads, enter `enable` to enter Enable mode, then enter the following:

	`show ip interface brief` => *If no IP address shows up, continue these steps*

	`configure terminal`

	`interface GigabitEthernet 0/0/0`

	`ip address 172.16.0.xx 255.255.255.0` (xx is the number the bench corresponds to)

	`no shutdown`

	`end`

1. Enter `format bootflash:`. The router will prompt you to confirm the action. Press Return and wait several moments until the format is complete.

1. Enter `show platform` or `show rom-monitor r0` to check ROMMON versions.  If necessary, copy ROMMON upgrade file for upgrading.

1. Enter:

	`copy ftp://ftpuser:ftp123!@172.16.0.45/firmware/isr4300-universalk9.17.03.05.SPA.bin bootflash:`

1. Enter `dir bootflash:` to confirm the files copied correctly.

1. Enter `erase startup-config`. Then, enter the following to set the boot variable:

	`configure terminal`

	`boot system bootflash:isr4300-universalk9.17.03.05.SPA.bin`

	`exit`

	`write`

	`reload`

1. Wait for reboot.  When asked to enter the initial configuration dialog, respond with no. Press Return when prompted.  The router will display a prompt ending in `>`.

1. Enter `enable` and press Return. The prompt should change to `# `.

1. Enter the following to test the first port:

	`configure terminal`

	`interface GigabitEthernet 0/0/0`

	`ip address 172.16.0.10 255.255.255.0`

	`no shutdown`

1. Ping the first port from a command prompt **(cmd.exe in Windows)** with <1500 bytes.  Use the command `ping -t -l 1200 172.16.0.10` in Windows.

1. Switch to the SFP slot for the first port, then enter `media-type sfp` to ping test it.

1. Enter the following to test the next port:

    `no ip address`

	`interface GigabitEthernet 0/0/1`

    `ip address 172.16.0.10 255.255.255.0`

    `no shutdown`

1. Ping the second port from a command prompt **(cmd.exe in Windows)** with <1500 bytes.  Use the command `ping -t -l 1200 172.16.0.10` in Windows.

1. Switch to the SFP slot for the second port, then enter `media-type sfp` to ping test it.

1. Enter the following to test the next port:

    `no ip address`

    `interface GigabitEthernet 0/0/2`

    `ip address 172.16.0.10 255.255.255.0`

    `no shutdown`

1. Ping the third port from a command prompt **(cmd.exe in Windows)** with <1500 bytes.  Use the command `ping -t -l 1200 172.16.0.10` in Windows.

1. Switch to the SFP slot for the third port, then enter `media-type sfp` to ping test it.

1. Enter the following to test the next port:

    `no ip address`

	`interface GigabitEthernet 0/0/3`

	`ip address 172.16.0.10 255.255.255.0`

	`no shutdown`

1. Ping the fourth port from a command prompt **(cmd.exe in Windows)** with <1500 bytes.  Use the command `ping -t -l 1200 172.16.0.10` in Windows.

1. Switch to the SFP slot for the fourth port, then enter `media-type sfp` to ping test it.

1. After all ports are tested, enter `erase startup-configuration`.

1. Check licensing information before reloading by entering `show license usage`. securityk9 should show here.

1. Enter `reload`.

1. When the router reloads, enter `show inventory` to get the serial number, then enter `show tech-support | redirect flash:(Serial Number).txt`.

1. Repeat the above process to configure the first port for copying the show tech-support output to the tftp server.

1. Enter `copy bootflash: ftp://ftpuser:ftp123!@172.16.0.45/diag/`, and input the correct file name and ip address when prompted.  Delete the text file from flash after copying using `delete bootflash:(filename)`.  

1. Enter `erase startup-config`, then `reload`. The router can be turned off when it starts to reboot.

## III. Packing

1. Do a final cleaning of fingerprints and apply inventory and Network Craze stickers upon certification that the router is fully complete. Include the correct kit as listed above.

	- Inventory stickers go as far to the upper left corner of the bottom of the router as possible, (accounting for screws, indents, etc.) in the same orientation as the rest of the stickers.  Network Craze stickers go directly below inventory stickers aligned with the left edge of the inventory sticker.
	
1. Seal router in anti-static bag to be packed for shipping.
