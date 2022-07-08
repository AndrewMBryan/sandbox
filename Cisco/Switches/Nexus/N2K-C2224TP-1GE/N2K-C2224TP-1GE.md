# N2K-C2224TF-1GE

[Online Support Site](http://www.cisco.com/c/en/us/support/switches/nexus-2224tp-ge-fabric-extender/model.html)

[Data Sheet](Docs\Data_Sheet_C78-437758.pdf)

### Required tools:

- Nexus 7000 Test Chassis
- Nexus 7000 Supervisor
- Console cable and USB to Serial connector
- Nexus 10G SFP Line Card
- 2 x SFP-10G-SR or FET-10G

### Inventory:

2 x Power Supplies

## I. Physical

Examine the switch. Look for the following:

- Deep scratches
- Dents
- Problems with bezel
- Bent ports or connectors
- Missing screws
- Dirt or dust
- Leaking, bent, or otherwise defective components
- Rust
	
## II. Functional

1. Insert supervisor and power on Nexus 7000 test chassis.  Insert 10G line card into slot 1.

1. Configure the following on the supervisor:

	`configure terminal`

	`install feature-set fex`

	`feature-set fex`

	`feature interface-vlan`

	`system auto-upgrade epld`

	`fex 101`

	`type N2224TP`

	`exit`

	`interface vlan 1`

	`ip address 10.0.0.1 255.255.255.0`

	`no shutdown`

	`interface port-channel 101`

	`switchport`

	`switchport mode fex-fabric`

	`fex associate 101`

	`no shutdown`

	`exit`

	`interface Ethernet 1/1`

	`channel-group 101 force`

	`no shutdown`

	`end`

1. Plug the SFPs into both port 1 of the 10G line card and any of the SFP ports on the fabric extender switch.  Connect the SFPs with testing fiber and power on the switch.

1. When the switch has booted, a console message should indicate that FEX 101 is online.  Enter `show fex` to ensure status is online.

1. Enter the following:

	`install all kickstart bootflash:n7000-s1-kickstart.6.2.14.bin system bootflash:n7000-s1-dk9.6.2.14.bin parallel`

1. Confirm the software install and wait for all console messages to indicate the process is complete.

1. Enter the following:

	`install all epld bootflash:n7000-s1-epld.6.2.14.img parallel`

1. Confirm the EPLD upgrade and wait for all console messages to indicate the process is complete.

1. Enter the following:

	`configure terminal`

	`interface Ethernet101/1/1 - 24`

	`switchport`

	`switchport mode access`

	`switchport access vlan 1`

	`spanning-tree port type edge`

	`no shutdown`

1. Ping each port from a command prompt **(cmd.exe in Windows)** with <1500 bytes.  Use the command `ping -t -l 1200 10.0.0.1` in Windows.

1. Capture the output of `show fex detail` to a file "<Serial number>-diags.txt" using your console.  The switch can be unplugged.

## III. Packing

1. Do a final cleaning of fingerprints and apply inventory and Network Craze stickers upon certification that the switch is fully complete.

	- Invetory sticker goes on the top of the switch above the Cisco sticker.  Network Craze sticker aligns to the left and top of the smaller stickers on the right side of the Cisco sticker.

1. Seal the switch in a static bag for boxing.