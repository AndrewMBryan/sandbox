# Cisco 7936 Conference Phone

## I. Physical

## II. Functional

- Connect the phone to a TFTP server with DHCP enabled. DHCP option 150 must be set to the address of the TFTP server. The file `cmterm-7936-sccp.3-3-21.bin` must be in the TFTP root.
- Power on the phone and press the `Menu` key when the phone begins to configure IP. Select the `Admin Settings` option and enter the password `**# `.
- Select the option `Reset to Defaults` and confirm the reset. The phone will reboot, acquire DHCP, and download the new firmware.
- The phone will reboot again after the firmware download. Disconnect the phone and connect it to an Ethernet port with access to the **Cisco CM** system.
- The phone will now boot up and eventually register with the system.
- Test all phone keys for proper function. Additionally, make a test call to another phone to verify function of the microphones, speaker, and mute key.
- Press the `Menu` key. Select the `Admin Settings` option and enter the password `**# `. Select the option `Reset to Defaults` and confirm the reset.
- The phone may now be cleaned and packed for shipping.