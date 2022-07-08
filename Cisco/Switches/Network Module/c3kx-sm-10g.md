# C3KX-SM-10G

[Online Support Site](support website)

[Data Sheet](Docs\data sheet)

### Required tools:

- Cisco 3750-X series Switch

### Inventory:

- No kit or accessories are needed for this item.

## I. Physical

- Examine the module for physical damage.
	
## II. Functional

1. Power on the test switch and wait for it to boot.

1. Insert the module into the network module slot of the test switch.

1. Configure the switch for testing with the following commands:

	`configure terminal`

	`interface gigabitEthernet 1/1/2`

	`spanning-tree portfast	`

	`interface gigabitEthernet 1/1/4`

	`spanning-tree portfast	`
	
	`interface vlan 1`

	`ip address 10.0.0.1 255.255.255.0`

	`no shutdown`

	`end`

1. Ping each port from a command prompt **(cmd.exe in Windows)** with <1500 bytes.  Use the command `ping -t -l 1200 10.0.0.1` in Windows.

1. Remove the module from the network module slot.

## III. Packing

1. Do a final cleaning of fingerprints and apply inventory and Network Craze stickers upon certification that the module is fully complete.

1. Seal the module in an anti-static bag to be packed for shipping.