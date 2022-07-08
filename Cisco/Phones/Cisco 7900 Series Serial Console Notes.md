# Cisco 7900 Series Serial Console Notes

- This cable allows the viewing of log messages and console interaction on Cisco 7900 series phones:
	- Pins are numbered right to left as viewed from the top of the plug with the cable end facing toward you.
	- RJ11 pin 1 -> N/C
	- RJ11 pin 2 -> RJ45 pin 3
	- RJ11 pin 3 -> RJ45 pin 4
	- RJ11 pin 4 -> RJ45 pin 6
- The cable connects to the RJ11 AUX or RS232 port on the phone and terminates in an RJ45 plug. This plug should be coupled to a Cisco rollover cable for proper usage.
- Depending on the model of phone connected to, different communication settings and features are used:
	- The Cisco 79x0 series uses 9600 8N1 and outputs no debug messages by default. There is a console session available after the phone finishes booting where debug messages and settings may be viewed. This console session is accessed with a password of "cisco".
	- The Cisco 79x1 series uses 9600 8N1 and outputs all debug messages by default. There is no console session available.
	- The Cisco 79x2 series uses 115200 7N1 and outputs all debug messages by default. There is no console available.