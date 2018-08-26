# CODESYS V3 Library for Monarco HAT

![Alt text](http://pigeoncomputers.com/wp-content/uploads/2017/08/Codesys_Logo_250px.png "CODESYS")
![Alt text](https://www.monarco.io/wp-content/uploads/2017/01/monarco_dinrail.jpg "Monarco HAT")

The Monarco HAT is a robust industrial graded HAT, perfectly suited for home automation projects. 
Tt wil protect your Raspebrry Pi from being fried by overvoltage or short circuiting and provide enough IO points to do some small projects with it. For example some IOT project, small home-automation or industrial projects in combination with MQTT telemetry protocol and much more ... 

A CODESYS V3 library was missing, so I wrote it to fill the gap after studying the C & Java Node-JS code examples and documentation provided by Monarco. Though tested thoroughly, it will probably still contain bugs =( 
If you spot a bug, share it so we can fix it.

As the CODESYS runtime for Raspbery Pi also contains a very good responsive HTML5 compatible webinterface (via a built in webserver in CODESYS itself), no extra software like OpenHAB or Domoticz is neccesary. But offcourse you can connect to these platforms if needed. For the record, I am not connected with Monarco or CODESYS in any way.

# V2.0.0.1 library info
- Implemented as CODESYS 3 IO device-driver;
   - 100% Open source,
   - 100% Pure IEC 61131-3 code (ST),
- No function block calls in your software necessary, just write code, attach variable to an I/O channel, ready! 
- Breaks compatibility with earlier FB version but improves highly on ease of use,
   - 4 Di,
   - 4 Do,
   - 2 Ai,
   - 2 Ao,
   - Hardware Watchdog,
   - Control Byte (experimental).
- Stable, but work in progress ...

# Missing in action
At this moment, some things are still missing, however all functionality are allready implemented (supported) in the core driver, but not yet routed as parameters;
- Not yet routed to parameters are;
   - RS485 configuration, 
   - DO channels PWM configuration,
   - DI channels Counter configuration.

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
- Latest Monarco IO Hat library for CODESYS package

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

# Enable NTP sync
Now manually configure and enable NTP service;

    sudo nano etc/ntp.config
    
    Add server pool.ntp.org (other server entries can be commented out)
    Uncomment line restrict 192.168.1.0 mask 255.255.255.0 nomodify notrap (you may need to change IP to your network base)
    
Now save and Quit nano again. Now you can enable NTP service;

      sudo systemctl enable ntpd.service

And then start it;

      sudo systemctl start ntpd.service

And check configuration;

      sudo ntpq -p

Now you can use the HAT, RS-485 and the Real-Time Clock from within a CODESYS IEC application. 
Access the RS485 UART via a comlib of you own flavour (like CAA SerialCOM library)

# Run CODESYS Project
Open the provided example project file,

Check/Set SPI master parameters:

    Mode 0,
    SPI bits 8,
    Speed(Hz) 1000000 (=1MHz) => can be set up to 4 MHz, slower speeds avoid chance on crc errors

# Compile, download and run => enjoy!
