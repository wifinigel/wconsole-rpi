# wconsole-rpi
Turn your rpi in to a wireless serial console cable

It can be annoying to have to sit in an equipment room to use the serial console port on an item of networking equipment. This project allows you to use an RPi to connect to your serial console cable via a wireless link while sat in the comfort of a nearby office, rather than sat with your laptop on the equipment room floor :) 

To provide a wireless console serial port, you will need:

 - An RPi 3B or later model
 - A (compatable) USB to serial cable connected to one of the RPi USB ports (e.g. Prolific Technology, Inc. PL2303 Serial Port)

Before attempting to use wconsole, you must install the followings packages on your RPi by performing the following steps:

1. Connect your RPI via the Ethernet port to a network with Internet access
2. SSH to the RPi and login
3. Execute the following commands:
    apt-get update
    apt-get install hostapd
    apt-get install isc-dhcp-server
    apt-get install ser2net
    
(Note that if you prefer to use the RPi desktop rather than SSH, it's fine to add the packages that way too)

Once the packages are installed, copy the supplied wconsole gzipped archive to the /etc directory of the RPI (e.g.using SFTP). Extract the files from the archive using the command:

```
 tar xvfz rconsole.tar.gz
```

Change to the newly created directory /etc/wconsole:

```
 cd /etc/wconsole
```

Run the installation script to configure hostapd, ser2net isc-dhcp-server files:

```
 sudo ./wconsole_switcher install
```

Flip the RPi in to wconsole mode:

```
 sudo ./wconsole_switcher on
```

At this point, the RPi will reboot. Following the reboot, an SSID of RCONSOLE will be available on channel 1. Join the SSID and use the default key: Password1.

Once you have joined the SSID, open a telnet session to 192.168.42.1:9600. This will provide access to the serial console cable plugged in to the USB port.

To switch out of rconsole mode, SSH to the RPi using network address 192.168.42.1 (while connected to the rconsole SSID) and run the command: 

```
 sudo /etc/wconsole/wconsole_switcher off
```

![WLANPi Menu](https://github.com/wifinigel/wconsole-rpi/blob/master/images/wconsole_rpi_demo.jpg)
