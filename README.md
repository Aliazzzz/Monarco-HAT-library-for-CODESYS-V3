# Monarco-HAT-library-for-CODESYS
CODESYS 3 Library for Monarco HAT

The Monarco HAT was lacking a CODESYS library, so I decided to write it myself.

I am not connected with Monarco in any way, I simply wrote this library out of hobbyism and for fun. 
I decided that maybe of use for other people. Therefore, I released it under the "Unlicense" agreement.


The main library components are;
- MonarcoHAT.devdesc.xml,
- .library file,
- example .project file

Also included in the release;
- .package file (CODESYS installer) which contains all above files in a user friendly installer, together with the "unlicense" agreement.


Prerequisitories;
- A Raspberry pi with the Monarco HAT,
- CODESYS IDE with Raspberry Pi .package installed,
- CODESYS runtime component installed on pi (Demo or licensed),


Hardware Installation;
To use the HAT hardware, RS-485 and the Realtime Clock under CODESYS, please follow these steps.
RTC requires no Linux side config apart from the overlay;

1) On your Raspberry Pi, switch to root user: sudo -s
2) Disable Linux console on UART: sed 's/ console=serial0,[0-9]\+//' -i /boot/cmdline.txt
3) Run the following command to get device-tree overlay definition for the RS-485 on the Monarco HAT: wget www.monarco.io/download/monarco-fix-4-9.dtbo
4) Copy it to /boot/overlays: sudo cp monarco-fix-4-9.dtbo /boot/overlays
5) Afterwards add dtoverlay=monarco-fix-4-9 line to the /boot/config.txt file: echo dtoverlay=monarco-fix-4-9 >> /boot/config.txt
6) Reboot your Raspberry Pi: reboot
7) After reboot, check the output of the following command: ls -l /dev/serial0
8) The response should read "/dev/serial0 -> ttyAMA0"
9) Again, switch to root user: sudo -s  cd etc/
10) Then: nano CODESYSControl.cfg
11) Add the following lines: [SysCom] Linux.Devicefile=/dev/ttyAMA
12) Then reboot your Raspberry Pi again: reboot
13) After reboot: Now you can use the HAT, RS-485 and the Real-Time Clock from within a CODESYS IEC application. Access the RS485 UART via a comlib of you own flavour (like CAA SerialCOM library).
14) Follow the Software Installation steps;


Software Installation;
1) Either install the .package via CODESYS Package Manager (or double click it), or 
2) Install the loose components via the Library / Device Repository, both found under Tools menu option in CODESYS IDE.
3) ENJOY!
