# Monarco-HAT-library-for-CODESYS-V3
![Alt text](https://pbs.twimg.com/profile_images/735481953491800064/_BwVygX7.jpg "Monarco Logo")
![Alt text](http://files.linuxgizmos.com/rex_monarcohat1.jpg "Monarco HAT")
![Alt text](https://tienda.opiron.com/107-home_default/curso-de-codesys.jpg "CODESYS")


CODESYS V3 Library for Monarco IO HAT


I am not connected with Monarco.io or CODESYS in any way. I simply wrote this library out of hobbyism and for fun (self education) because I love the industrial rubustness of this HAT. It's an industrial graded Hat ideally suited for Home, IOT or small industrial projects.

The Monarco HAT was lacking a proper CODESYS V3 library, so I decided to write it myself to fill in this gap.
So, using C & Java Node-JS code examples and documentation from Monarco and after lots of reading and coding, this is end-result. I intend to expand on the Device driver with frequent updates. I decided that it maybe of use for other people, Therefore, I released it under the "Unlicense" agreement. It may still contain bugs (not too much I hope!). If you spot a bug, tell me. Feel free to contribute!

# Information about older and current release;
https://github.com/Aliazzzz/Monarco-HAT-library-for-CODESYS-V3/blob/master/VERSIONS.md


![Alt text](https://github.com/Aliazzzz/Monarco-HAT-library-for-CODESYS-V3/blob/master/Monarco/2.0.0.0/pics/Monarco_HAT%20Information2018-02-11_172304.png "v2.0.0.0 driver info")


# The main components are;
- .package file (CODESYS installer) which contains all below mentioned files in a user friendly installer, together with the "unlicense" agreement;
- .devdesc.xml,
- .Library,
- Example.project file.


# Prerequisitories;
- A Raspberry pi with the Monarco HAT,
- CODESYS IDE with Raspberry Pi .package installed,
- CODESYS runtime component installed on pi (Demo or licensed).


# Hardware installation;
- To use the HAT hardware, RS-485 and the Realtime Clock under CODESYS, please follow these steps.
- RTC requires no Linux side config apart from the overlay;

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


# Software installation;
1) Either install the .package via CODESYS Package Manager (or double click it), or 
2) Install the loose components via the Library / Device Repository, both found under Tools menu option in CODESYS IDE.
3) ENJOY!
