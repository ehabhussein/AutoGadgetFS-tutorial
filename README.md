![](https://github.com/ehabhussein/AutoGadgetFS/raw/master/screenshots/agfslogos.png)

<a name="autogadgetfs-tutorial"/>

## Table of contents: (Under development)
1. [What is AutoGadgetFS](https://agfs.io/){:target="_blank"}
1. [How to install Autogadgetfs](https://agfs.io/#Installation){:target="_blank"}
1. [Importing agfs and selecting your device (Configuration, Interface, Alternate Settings, Endpoints)](#selecting-your-device)
1. [Create a new project](#newp)
1. [Emulating the selected device](#Emulating-the-selected-device)
1. [Starting the router on the Pi Zero](#Starting-the-router-on-the-Pi-Zero)
1. [Starting and stopping Man in the middle](#Mitm)
1. [Starting and stopping the device sniffer](#devsniff)
1. [Fuzzing device and host](#Fuzzing)
	- [Fuzzing the device](#Devfuzz)
		1. [Random fuzzer](#Device-random-fuzzer)
		1. [Sequential Fuzzer](#Device-sequential-fuzzer)
		1. [Smart Fuzzer](#Device-smart-fuzz)
		1. [Describe fuzzer](#Describe-fuzzer)
		1. [Send packet to device](#senddev)
	- [Fuzzing the host](#Hostfuzz)
		1. [Random fuzzer](#Host-random-fuzzer)
		1. [Smart Fuzzer](#Host-smart-fuzzer)
		1. [Gadget fuzzer](#Host-gadget-fuzzer)
		1. [Send packet to host](#sendhst)
		1. [Fuzzing with code coverage](#codecov)
1. [Developing your custom fuzzer](#cusfuzz)
1. [Device control transfer enumerator](#Control-Transfer-Enumerator)
1. [Removing a running gadget on the Pi Zero](#rgadget)
1. [Monitor device interfaces for changes](#monint)
1. [Change to another Configuration, Interface, Alternate Settings, Endpoints on the device](#chgint)
1. [Pull firmware from device that is in DFU mode](#dfu)
1. [Clearing rabbitMQ Queues](#qclear)
1. [Releasing the device back to the system](#release)
1. [Parse, search , show and replay usblyzer capture](#usblyzer)
1. [Reset the device](#reset)
1. [Show device information](#devinfo)
1. [AGFS directory structure](#struct)
1. [Help](#Help)
	- [Summary of methods](#All-methods)
	- [Help for a method](#Method-help)
1. [Supported by](#Support)
1. [Slack channel](#Slack)
1. [Buy me a coffee ☕️](#Donate)
1. [Contact me](#Contact)

---

### Selecting your device (Configuration, Interface, Alternate Settings, Endpoints)

```python

In [1]: import libagfs                                                         

In [2]: x = libagfs.agfs()                                                                                                                                                                    
***************************************
AutoGadgetFS: USB testing made easy
***************************************
Enter IP address of the rabbitmq server: 127.0.0.1

In [3]: x.findSelect()
```
<details>
	
```python
Give your project a name?!: Nuc220DevKit
0 : Realtek:33107:3034
1 : Generic:1041:3034
2 : Linux 5.6.0-kali1-amd64 xhci-hcd:3:7531
3 : Linux 5.6.0-kali1-amd64 xhci-hcd:2:7531
4 : VIA Labs, Inc.:2071:8457
5 : Linux 5.6.0-kali1-amd64 xhci-hcd:3:7531
6 : None:257:6720
7 : Generic:21521:3034
8 : None:57506:1161
9 : CN09357GLOG008CLA8P2A01:26403:3141
10 : SINO WEALTH:4102:9610
11 : Nuvoton:20764:1046
12 : VIA Technologies Inc.         :258:8457
13 : Logitech:50475:1133
14 : VIA Labs, Inc.:10263:8457
15 : Linux 5.6.0-kali1-amd64 xhci-hcd:2:7531
---> Select a device: 11
DEVICE ID 0416:511c on Bus 001 Address 047 =================
 bLength                :   0x12 (18 bytes)
 bDescriptorType        :    0x1 Device
 bcdUSB                 :  0x110 USB 1.1
 bDeviceClass           :    0x0 Specified at interface
 bDeviceSubClass        :    0x0
 bDeviceProtocol        :    0x0
 bMaxPacketSize0        :   0x40 (64 bytes)
 idVendor               : 0x0416
 idProduct              : 0x511c
 bcdDevice              :  0x100 Device 1.0
 iManufacturer          :    0x1 Nuvoton
 iProduct               :    0x2 Nu-Link
 iSerialNumber          :    0x0 
 bNumConfigurations     :    0x1
  CONFIGURATION 1: 100 mA ==================================
   bLength              :    0x9 (9 bytes)
   bDescriptorType      :    0x2 Configuration
   wTotalLength         :   0x40 (64 bytes)
   bNumInterfaces       :    0x2
   bConfigurationValue  :    0x1
   iConfiguration       :    0x0 
   bmAttributes         :   0x80 Bus Powered
   bMaxPower            :   0x32 (100 mA)
    INTERFACE 0: Human Interface Device ====================
     bLength            :    0x9 (9 bytes)
     bDescriptorType    :    0x4 Interface
     bInterfaceNumber   :    0x0
     bAlternateSetting  :    0x0
     bNumEndpoints      :    0x2
     bInterfaceClass    :    0x3 Human Interface Device
     bInterfaceSubClass :    0x0
     bInterfaceProtocol :    0x0
     iInterface         :    0x0 
      ENDPOINT 0x81: Interrupt IN ==========================
       bLength          :    0x7 (7 bytes)
       bDescriptorType  :    0x5 Endpoint
       bEndpointAddress :   0x81 IN
       bmAttributes     :    0x3 Interrupt
       wMaxPacketSize   :   0x40 (64 bytes)
       bInterval        :    0x1
      ENDPOINT 0x2: Interrupt OUT ==========================
       bLength          :    0x7 (7 bytes)
       bDescriptorType  :    0x5 Endpoint
       bEndpointAddress :    0x2 OUT
       bmAttributes     :    0x3 Interrupt
       wMaxPacketSize   :   0x40 (64 bytes)
       bInterval        :    0x1
    INTERFACE 1: CDC Data ==================================
     bLength            :    0x9 (9 bytes)
     bDescriptorType    :    0x4 Interface
     bInterfaceNumber   :    0x1
     bAlternateSetting  :    0x0
     bNumEndpoints      :    0x2
     bInterfaceClass    :    0xa CDC Data
     bInterfaceSubClass :    0x0
     bInterfaceProtocol :    0x0
     iInterface         :    0x0 
      ENDPOINT 0x83: Bulk IN ===============================
       bLength          :    0x7 (7 bytes)
       bDescriptorType  :    0x5 Endpoint
       bEndpointAddress :   0x83 IN
       bmAttributes     :    0x2 Bulk
       wMaxPacketSize   :   0x40 (64 bytes)
       bInterval        :    0x0
      ENDPOINT 0x4: Bulk OUT ===============================
       bLength          :    0x7 (7 bytes)
       bDescriptorType  :    0x5 Endpoint
       bEndpointAddress :    0x4 OUT
       bmAttributes     :    0x2 Bulk
       wMaxPacketSize   :   0x40 (64 bytes)
       bInterval        :    0x0
        
do you want to detach the device from it's current system driver: [y/n] y
Disabling Interfaces on configuration: 1
Disabling interfaces :
	2
Disabled interface: 0
[-] Kernel driver detached
Configuration Value: 1

​	Interface number: 0,Alternate Setting: 0

​		Endpoint Address: 0x81

​		Endpoint Address: 0x2

​	Interface number: 1,Alternate Setting: 0

​		Endpoint Address: 0x83

​		Endpoint Address: 0x4

Do you want to reset the device? [y/n]: n
which Configuration would you like to use: 1
which Interface would you like to use: 0
which Alternate setting would you like to use: 0
which Endpoint IN would you like to use: 0x81
which Endpoint OUT would you like to use: 0x2
Checking if device supports DFU mode based on USB DFU R1.1

********************************

This Device isnt in DFU mode

********************************

Do you want to claim the device interface: [y/n] y
Checking HID report retrieval

b'05010900a101150026ff0019002900750895408102190029009102c0'
.........ÿ.....u...........À
Do you want to save this device's information?[y/n]y
setting up: Nuvoton
Creating backup of device

- Done: Device settings copied to file.

In [4]:

```
</details> 

- [Go Back](#autogadgetfs-tutorial)

---

### Emulating the selected device

```python3

In [4]: x.setupGadgetFS()                                                                                                                                                                     
setting up: Nuvoton
Aquiring info about the device for Gadetfs

are you going to configure this gadget to work with windows [y/n] ?y
0 ]  b'05010900a101150026ff0019002900750895408102190029009102c0'
Which report would you like to use? 0
Do you want to push the gadget to the Pi zero ?[y/n] y
Enter the ip address of the Pi zero: 192.168.1.57
Enter the port of the Pi zero: 22
Enter the username: pi
Password: 
Connecting...
Sending...
Done!
Do you want to run the gadget? [y/n]y
********************************
Gadget should now be running
********************************

In [5]:  

```

- [Go Back](#autogadgetfs-tutorial)

---

### Starting the router on the Pi Zero

```bash

root@pi:/home/pi# python3 router.py -h
usage: router.py [-h] -ip IPADDRESS -l PKTLEN [-s HSTONLY]

optional arguments:
  -h, --help     show this help message and exit
  -ip IPADDRESS  ip address of RabbitMQ
  -l PKTLEN      packet length. Check bMaxPacketsize0 on your device
  -s HSTONLY     Just to receive packets to the host

```

<details>
	
```bash

root@pi:/home/pi# python3 router.py -l64 -ip 192.168.1.3

```

</details>

- [Go Back](#autogadgetfs-tutorial)

---

### Help

### All methods

```python3

In [63]: x.help("")

```

<details>

```python

Currently supported methods:
________________________________________________________________________________
Method               ||-->Description
________________________________________________________________________________
MITMproxy            ||-->This method creates a connection to the RabbitMQ and listen on received messages on the todev queue
________________________________________________________________________________
MITMproxyRQueues     ||-->This method reads from the queue todev and sends the request to the device its self.
________________________________________________________________________________
SmartFuzz            ||-->This method is generates packets based on what it has learned from a sniff from either the host or the device
________________________________________________________________________________
chgIntrfs            ||-->This method allows you to change and select another interface
________________________________________________________________________________
clearqueues          ||-->this method clears all the queues on the rabbitMQ queues that are set up
________________________________________________________________________________
clonedev             ||-->This method does not need any parameters it only saves a backup of the device incase you need to share it or use it later.
________________________________________________________________________________
createctrltrsnfDB    ||-->creates a SQLite database containing values that were enumerated from control transfer enumeration
________________________________________________________________________________
createdb             ||-->create the sqlite table and columns from usblyzer captures
________________________________________________________________________________
decodePacketAscii    ||-->This method decodes packet bytes back to Ascii
________________________________________________________________________________
describeFuzz         ||-->This method allows you to describe a packet and select which bytes will be fuzzed
________________________________________________________________________________
devDfuDump           ||-->This method allows you to pull firmware from a device in DFU mode
________________________________________________________________________________
devEnumCtrltrnsf     ||-->This method enumerates all possible combinations of a control transfer request
________________________________________________________________________________
devReset             ||-->This method Resets the device
________________________________________________________________________________
devWrite             ||-->To use this with a method you would write make sure to run the startSniffReadThread(self,endpoint=None, pts=None, queue=None,channel=None)
________________________________________________________________________________
devctrltrnsf         ||-->This method allows you to send ctrl transfer requests to the target device
________________________________________________________________________________
deviceInfo           ||-->gets the complete info only for any usb connected to the host
________________________________________________________________________________
deviceInterfaces     ||-->get all interfaces and endpoints on the device
________________________________________________________________________________
devrandfuzz          ||-->this method allows you to create fixed or random size packets created using urandom
________________________________________________________________________________
devseqfuzz           ||-->This method allows you to create sequential incremented packets and send them to the device
________________________________________________________________________________
findSelect           ||-->This method enumerates all USB devices connected and allows you to select it as a target device as well as its endpoints
________________________________________________________________________________
help                 ||-->AutogadgetFS Help method
________________________________________________________________________________
hostwrite            ||-->This method writes packets to the host either targeting a software or a driver in control of the device
________________________________________________________________________________
hstrandfuzz          ||-->this method allows you to create fixed or random size packets created using urandom and send them to the host queue
________________________________________________________________________________
monInterfaceChng     ||-->Method in charge of monitoring interfaces for changes this is called from def startMonInterfaceChng(self)
________________________________________________________________________________
newProject           ||-->creates a new project name if you were testing something else
________________________________________________________________________________
releasedev           ||-->releases the device and re-attaches the kernel driver
________________________________________________________________________________
removeGadget         ||-->This method removes the gadget from the raspberryPI
________________________________________________________________________________
replaymsgs           ||-->This method searches the USBLyzer parsed database and give you the option replay a message or all messages from host to device
________________________________________________________________________________
searchmsgs           ||-->This method allows you to search and select all messages for a pattern which were saved from a USBlyzer database creation
________________________________________________________________________________
setupGadgetFS        ||-->setup variables for gadgetFS : Linux Only, on Raspberry Pi Zero best option
________________________________________________________________________________
showMessage          ||-->shows messages if error or warn or info
________________________________________________________________________________
sniffdevice          ||-->read the communication between the device to hosts
________________________________________________________________________________
startMITMusbWifi     ||-->Starts a thread to monitor the USB target Device
________________________________________________________________________________
startMonInterfaceChng||-->This method Allows you to monitor a device every 10 seconds in case it suddenly changes its interface configuration.
________________________________________________________________________________
startQueuewrite      ||-->initiates a connection to the queue to communicate with the host
________________________________________________________________________________
startSniffReadThread ||-->This is a thread to continuously read the replies from the device and dependent on what you pass to the method either pts or queue
________________________________________________________________________________
stopMITMusbWifi      ||-->Stops the man in the middle thread between the host and the device
________________________________________________________________________________
stopMonInterfaceChang||-->Stops the interface monitor thread
________________________________________________________________________________
stopQueuewrite       ||-->stop the thread incharge of communicating with the host machine
________________________________________________________________________________
stopSniffing         ||-->Kills the sniffing thread strted by startSniffReadThread()
________________________________________________________________________________
usblyzerparse        ||-->This method will parse your xml exported from usblyzer and then import them into a database
________________________________________________________________________________


```

</details>

- [Go Back](#autogadgetfs-tutorial)


---


### Help for a method

```python3

In [65]: x.help("startMITMusbWifi",source=True)

```

<details>
		
```python

****
[+]Help for startMITMusbWifi Method:
[-]Signature: startMITMusbWifi(self, endpoint=None, savefile=None, genpkts=0)


[+]startMITMusbWifi Help:
Starts a thread to monitor the USB target Device
:param endpoint: the OUT endpoint of the device most probably self.epout which is from the device to the PC
:param savefile: if you would like the packets from the host to be saved to a binary file
:param: genpkts: save packets from device to file
:return: None

[+]Source code of method startMITMusbWifi:
    def startMITMusbWifi(self,endpoint=None,savefile=None,genpkts=0):
        """ Starts a thread to monitor the USB target Device
        :param endpoint: the OUT endpoint of the device most probably self.epout which is from the device to the PC
        :param savefile: if you would like the packets from the host to be saved to a binary file
        :param: genpkts: save packets from device to file
        :return: None
        """
        if savefile:
            self.savefile = 1
        self.killthread = 0
        self.nlpthresh = 0
        self.startMITMProxyThread = threading.Thread(target=self.MITMproxy, args=(endpoint,savefile,genpkts,))
        self.startMITMProxyThread.start()

****

```

</details>

- [Go Back](#autogadgetfs-tutorial)

---

<a name="Support"/>

### Supported by:

<img src="https://scontent.faly3-2.fna.fbcdn.net/v/t1.0-9/fr/cp0/e15/q65/44079817_10157132509822841_8000883082938810368_n.jpg?_nc_cat=111&_nc_sid=dd9801&efg=eyJpIjoidCJ9&_nc_oc=AQmV77vp4H7E5CLwRCvKIPBIb9mRcD6LUSD48vYLH-cjd5wwxVvv5p-S8CwHBBYQr9I&_nc_ht=scontent.faly3-2.fna&_nc_tp=14&oh=d1653eaad921c8faf36beecbf242dcf8&oe=5F02FEF9" width="166" height="166"> ![JetBrains](https://github.com/ehabhussein/AutoGadgetFS/raw/master/screenshots/JetBrains.png) ![PyUSB](https://github.com/ehabhussein/AutoGadgetFS/raw/master/screenshots/pyusb.png) <img src="https://dslv9ilpbe7p1.cloudfront.net/TkfZukgA9X8SQdqJjdmdCA_store_logo_image.png" width="166" height="166"> 

- [Go Back](#autogadgetfs-tutorial)

---

<a name="Slack"/>

### Join Slack:

Visit [AutogadgetFS Slack Channel](https://join.slack.com/t/autogadgetfs/shared_invite/zt-emgcv3ol-unG_axHmSQlk~5GcBddhlQ){:target="_blank"}


- [Go Back](#autogadgetfs-tutorial)

---

<a name="Donate"/>

### Buy me a coffee to support the development of this project

[![Paypal Donations](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.me/autogadgetfs){:target="_blank"}

- [Go Back](#autogadgetfs-tutorial)

---

<a name="Contact"/>

### Contact me:

### 📧: <rd@agfs.io>

### 🐦 : [https://twitter.com/0xRaindrop](https://twitter.com/0xRaindrop){:target="_blank"}

- [Go Back](#autogadgetfs-tutorial)
