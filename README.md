# Monarco-HAT-library-for-CODESYS-V3
![Alt text](https://www.codesys.com/typo3conf/ext/template87/Resources/Public/Images/CODESYS_logo_ds.svg "CODESYS")
![Alt text](https://www.monarco.io/wp-content/uploads/2017/01/monarco.png "Monarco HAT")


CODESYS V3 Library for Monarco HAT

A proper CODESYS V3 library was missing, so I wrote it to fill the gap.
Written after studying C & Java Node-JS code examples and documentation provided by Monarco.
Released under the "Unlicense" agreement, not connected with Monarco.io or CODESYS in any way. 
Though tested thoroughly, it will probably still contain bugs =( If you spot a bug, share it so we can fix it.
Written out of hobbyism and fun.

# Use Case
The Monarco HAT is a real robust industrial graded HAT perfectly suited for home automation projects, i.e. in combination with mqtt telemetry protocol, IOT projects, Industry 4.0, small industrial projects and much more ...

# V2.0.0.0 library info
- Implemented as CODESYS 3 IO device-driver;
   - 100% Open source,
   - 100% Pure IEC code (ST),
   - No function block calls in your software necessary, just write code, attach variable to an I/O channel, ready! 
   - Breaks compatibilty with earlier FB version but improves highly on ease of use,
   - Stable, but work in progress ...

# Previous versions info
https://github.com/Aliazzzz/Monarco-HAT-library-for-CODESYS-V3/blob/master/VERSIONS.md

# The main software components
- .package file (CODESYS package installer) which installs the necessary files in a user friendly manner;
   - Hardware device description file,
   - Software library file,
   - Example project file, 
   - A copy of the "unlicense" agreement...

# Hardware prerequisitories
- A Raspberry Pi,
- A Monarco HAT ...

# Software prerequisitories
- CODESYS V3 IDE available at https://store.codesys.com/codesys.html,
- CODESYS Raspberry Pi .package available at https://store.codesys.com/codesys-control-for-raspberry-pi-sl.html,
- Monarco IO Hat library for CODESYS V2.0.0.0 package found at https://github.com/Aliazzzz/Monarco-HAT-library-for-CODESYS-V3/tree/master/Monarco/2.0.0.0

# Hardware installation
Attach Monarco HAT to Raspberry Pi and power it up; 

    sudo cat /proc/device-tree/hat/vendor
    
should return "REX Controls" 

    sudo cat /proc/device-tree/hat/product

should return "Monarco HAT"

# Disable system console on UART

    sudo sed 's/ console=serial0,[0-9]\+//' -i /boot/cmdline.txt
    sudo reboot

# Install essential tools
    
    sudo apt update
    sudo apt install git

# Flash Monarco HAT EEPROM (to avoid manual installation of overlay)
sudo git clone https://github.com/monarco/monarco-hat-firmware-bin

    cd monarco-hat-firmware-bin
    ./monarco-eeprom.sh update

# Install CODESYS runtime component on pi (Demo or licensed)
Follow Codesys online help steps, its easy!

https://help.codesys.com/webapp/_rbp_install_runtime;product=CODESYS_Control_for_Raspberry_Pi_SL;version=3.5.12.0


# Monarco codesys package installation
Either install the Monarco codesys package via;
    Double-click the package or 
    via CODESYS IDE Package Manager or
    Install the loose components via the Library / Device Repository, found under Tools menu option in CODESYS IDE.

# Attach CODESYS to the RS485 UART
Switch to etc direcory and edit the CODESYSControl.cfg;

    cd etc/
    sudo nano CODESYSControl.cfg

Add the following lines;
    
    [SysCom] Linux.Devicefile=/dev/ttyAMA

Now save and Quit nano. 

Now you can use the HAT, RS-485 and the Real-Time Clock from within a CODESYS IEC application. 
Access the RS485 UART via a comlib of you own flavour (like CAA SerialCOM library)

# Run CODESYS Project
Open the provided example project file,

Check/Set SPI master parameters:

    Mode 0,
    SPI bits 8,
    Speed(Hz) 1000000 (=1MHz) => can be set up to 4 MHz, slower speeds avoid chance on crc errors


# Compile, download and run => enjoy!
