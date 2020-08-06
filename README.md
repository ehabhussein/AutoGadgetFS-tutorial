![](https://github.com/ehabhussein/AutoGadgetFS/raw/master/screenshots/agfslogos.png)

<iframe width="500" height="315" src="https://www.youtube.com/embed/VY10xFifA50" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

[![PayPal Donations](https://img.shields.io/static/v1?logo=Donate&label=Donate&message=To%20support%20the%20development%20of%20AGFS&color=blue)](https://www.paypal.me/autogadgetfs)

<a name="autogadgetfs-tutorial"/>

## Table of contents: (Under development)
1. [What is AutoGadgetFS ✔️](https://agfs.io/){:target="_blank"}
1. [Learn about USB ✔️](https://www.beyondlogic.org/usbnutshell/usb1.shtml){:target="_blank"}
1. [How to install Autogadgetfs ✔️](https://agfs.io/#Installation){:target="_blank"}
1. [AutoGadgetFS settings file ✔️](#agfssettings)
1. [Importing agfs and selecting your device(Configuration, Interface, Alternate Settings, Endpoints)✔️](#selecting-your-device)
1. [Create a new project ✔️](#newp)
1. [Emulating the selected device ✔️](#Emulating-the-selected-device)
1. [Starting the router on the Pi Zero ✔️](#Starting-the-router-on-the-Pi-Zero)
1. [Starting and stopping Man in the middle ✔️](#Mitm)
1. [Removing a running gadget on the Pi Zero ✔️](#rgadget)
1. [Starting and stopping the device sniffer ❌](#devsniff)
1. [Fuzzing device and host](#Fuzzing)
	- [Fuzzing the device](#Devfuzz)
		1. [Random fuzzer ✔️](#Device-random-fuzzer)
		1. [Smart Fuzzer ❌](#Device-smart-fuzz)
		1. [Describe fuzzer ✔️](#Describe-fuzzer)
		1. [Send packet to device ❌](#senddev)
	- [Fuzzing the host ✔️](#Hostfuzz)
		1. [Random fuzzer ✔️](#Host-random-fuzzer)
		1. [Smart Fuzzer ✔️](#Host-smart-fuzzer)
		1. [Gadget fuzzer ✔️](#Host-gadget-fuzzer)
		1. [Send packet to host ✔️](#sendhst)
		1. [Fuzzing with code coverage ❌](#codecov)
1. [Device control transfer enumerator ✔️](#Control-Transfer-Enumerator)
1. [Monitor device interfaces for changes ✔️](#monint)
1. [Clearing rabbitMQ Queues✔️](#qclear)
1. [Releasing the device back to the system ✔️](#release)
1. [Parse, search , show and replay usblyzer capture ❌](#usblyzer)
1. [Reset the device ✔️](#reset)
1. [Show device information](#devinfo)
1. [Help ✔️](#Help)
	- [Summary of methods ✔️](#All-methods)
	- [Help for a method ✔️](#Method-help)
1. [Supported by ✔️](#Support)
1. [Slack channel ✔️](#Slack)
1. [Buy me a coffee ☕️ ✔️](#Donate)
1. [Contact me ✔️](#Contact)
15. [Want to contribute ? ✔️](#Cont)

---

<a name="agfssettings"/>

### AutoGadgetFS settings file

* Basic settings needed for agfs to work found in the file `agfsSettings.json` set them accordingly to your setup:

```json
{
	"RabbitMQ-IP":"127.0.0.1",
	"PiZeroIP":"192.168.1.57",
	"PiZeroSSHPort":22,
	"PiZeroUser":"pi",
	"PiZeroPass":"raspberry"
}
```

- [Go Back](#autogadgetfs-tutorial)

---

<a name="selecting-your-device"/>

### Importing agfs and selecting your device (Configuration, Interface, Alternate Settings, Endpoints)

```python

In [1]: import libagfs                                                         

In [2]: agfs = libagfs.agfs()                                                                                                                                                                    
***************************************
AutoGadgetFS: USB testing made easy
***************************************
Enter IP address of the rabbitmq server: 127.0.0.1

In [3]: agfs.newProject()
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
     bInterfaceSubClass :    0x01
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

	Interface number: 0,Alternate Setting: 0

		Endpoint Address: 0x81

		Endpoint Address: 0x2

	Interface number: 1,Alternate Setting: 0

		Endpoint Address: 0x83

		Endpoint Address: 0x4

Do you want to reset the device? [y/n]: n
which Configuration would you like to use: 1
Checking if device supports DFU mode based on USB DFU R1.1

********************************

This Device isnt in DFU mode

********************************

Do you want to claim all device interfaces: [y/n] y
[+] Claiming interface 0
	[-]Successfully claimed interface 0
[+] Claiming interface 1
	[-]Successfully claimed interface 1
[+] Claiming interface 2
	[-]Successfully claimed interface 2
Checking HID report retrieval
Hid report [0]: 05010906a101050719e029e71500250175019508810295017508810195057501050819012905910295017503910195067508150025650507190029658100090375089508b102c0
	decoded: .........à.ç....u.......u.....u...........u.....u....e.....e....u.....À
Hid report [1]: 06d0f10901a1010920150026ff007508954081020921150026ff00750895409102c0
	decoded: .Ðñ.........ÿ.u..........ÿ.u.....À

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

<a name="newp"/>

### Create a new project

```python
In [20]: agfs.newProject()                                                                                                                                                                       
[-] Releasing the Interface
Releasing interfaces :
1
[-] Attaching the kernel driver
Releasing interface: 0
Releasing interface: 1
[-] Device released!
Give your project a name?!: 
```
    
- [Go Back](#autogadgetfs-tutorial)

---

<a name="Emulating-the-selected-device"/>

### Emulating the selected device

```python3

In [4]: agfs.setupGadgetFS()                                                                                                                                                                     
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

<a name="Starting-the-router-on-the-Pi-Zero"/>

### Starting the router on the Pi Zero

* Once you have called agfs.setupGadgetFS() and the gadget is running . Now you can start the router on the raspberry pi side.

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

<a name="Mitm"/>

### Starting and stopping Man in the middle

* Starting MITM Device side: ( You can select any EndpointIN on the active configuration)

```python
In [12]: agfs.startMITM(epin=0x81,epout=0x2,devsave=1,hostsave=1)
# devsave and hostsave will write all the MITM communication of the device and host to files inside the binariesdb/ folder 
```


![devmitm1](https://github.com/ehabhussein/AutoGadgetFS-tutorial/raw/master/agfstutscreens/devmitm11.png)
    

* Starting MITM host side:

```bash
pi@agfs:~ $ sudo bash
root@agfs:/home/pi# python3 router.py -l64 -ip 192.168.1.3
```

![devmitm2](https://github.com/ehabhussein/AutoGadgetFS-tutorial/raw/master/agfstutscreens/devmitm2H.png)


* Stopping MITM Device side:
	
	```python
		In [18]: agfs.stopMITM()                                   
	**********************************
	Thread Terminated Successfully
	**********************************
	**************************************
	Sniffing has stopped successfully!
	**************************************
	Stream connection lost: IndexError('pop from an empty deque')
	***************************************
	MITM Proxy has now been terminated!
	***************************************

	In [19]: 
	```

* Stopping MITM Raspberry pi side:
	
	```bash
	Keep pressing Ctrl-C anytime to clean up and exit!
	```

- [Go Back](#autogadgetfs-tutorial)

---

<a name="rgadget"/>

### Removing a running gadget on the Pi Zero

```python3
In [6]: agfs.removeGadget()  
```

- [Go Back](#autogadgetfs-tutorial)

---

<a name="Fuzzing"/>

### Fuzzing device and host

<a name="Devfuzz"/>

#### Fuzzing the device
<a name="Device-random-fuzzer"/>

  * Random fuzzer:
  ```python3
  In [22:] agfs.devrandfuzz(epin=0x81,epout=0x2)
  ```
![](https://github.com/ehabhussein/AutoGadgetFS-tutorial/raw/master/agfstutscreens/devrandfuzz.png)

- [Go Back](#autogadgetfs-tutorial)

<a name="Describe-fuzzer"/>

  * Describe fuzzer
  
  ```python3
  In [19:] agfs.describeFuzz(epin=0x81,epout=0x2,packet="f3e01ec..SNIP..259d293d",howmany=10)
  ```
  ![](https://github.com/ehabhussein/AutoGadgetFS-tutorial/raw/master/agfstutscreens/describefuzz.png)

- [Go Back](#autogadgetfs-tutorial)

---

<a name="Hostfuzz"/>

### Fuzzing the host

<a name="Host-random-fuzzer"/>

### Host random fuzzer

```python3

In [12]: agfs.help("hstrandfuzz")                                                                                                                                                                
****
[+]Help for hstrandfuzz Method:
[-]Signature: hstrandfuzz(self, howmany=None, size=None, min=None, max=None, timeout=0.5, mybyte=None)


[+]hstrandfuzz Help:
this method allows you to create fixed or random size packets created using urandom and send them to the host queue
:param howmany: how many packets to be sent to the device`
:param size: fixed size packet lengthsize = 10 to generate a length 10 packet
:param min minimum size value to generate a packet
:param max maximum size value to generate a packet
:param timeout: timeOUT !
:param mybyte: if you want to fuzz with a specific byte 'AA'
:return: None
****

In [13]: agfs.hstrandfuzz(howmany=100,size=64,timeout=0) 

```

- [Go Back](#autogadgetfs-tutorial)

---

<a name="Host-smart-fuzzer"/>

### Host Smart Fuzzer

* After you have done a MITM between the device and the host, the communication has been saved in the `binariesdb/` folder you can use either the host or device communication to generate packets.

```python3

In [41]: agfs.help("SmartFuzz")                                                                                                                                                                  
****
[+]Help for SmartFuzz Method:
[-]Signature: SmartFuzz(self, engine=None, samples=10, direction=None, filename=None)


[+]SmartFuzz Help:
This method is generates packets based on what it has learned from a sniff from either the host or the device
:param engine: choice between smart, random
    random: [truly random based on charset , length , chars found]
    smart: [based on input , weight & positions]
:param samples: number of samples to be generated
:param direction: 'hst' or 'dev'
:param filename: 'filename to learn from'
:return: None
****

In [42]: !head -n5 binariesdb/dfg-Nuvoton-1046-20764-1595061045.257177-device.bin                                                                                                             
0308010000000100000000000000ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff000006b0ab2c
04185900000001000000160000000100000088000000ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff000006b0ab2c
06185900000001000000160000000100000088000000ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff000006b0ab2c
07080100000001000000160000000100000088000000ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff000006b0ab2c
0114fd1a000009200100100000009e01820100b20000ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff000006b0ab2c

In [43]: agfs.SmartFuzz(engine="random",samples=100,filename='binariesdb/dfg-Nuvoton-1046-20764-1595061045.257177-device.bin',direction='hst')
```

<details>

```python3
[+]General Statistics
Full charset                : !"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_`abcdefghijklmnopqrstuvwxyz{|}~
Discarded charset           : !"#$%&'()*+,-./:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_`ghijklmnopqrstuvwxyz{|}~
Final charset               : 0123456789abcdef
Word Length                 : 128
Lower Case index usage      : 92%
Lower Case index locations  : [1, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, 100, 101, 102, 103, 104, 105, 106, 107, 108, 109, 110, 111, 112, 113, 114, 115, 122, 124, 125, 127]
Upper Case index usage      : 0%
Upper Case index locations  : []
Digit index usage           : 96%
Digit index locations       : [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, 100, 101, 102, 103, 104, 105, 106, 107, 108, 109, 110, 111, 112, 113, 114, 115, 116, 117, 118, 119, 120, 121, 123, 126]
NonAN index usage           : 0%
NonAN index locations       : []
Counter statistics          : Uppercase: 0 , Lowercase: 217240, Digits:385384 , NonAlphaNumeric:0
All char Frequencies        : 
character:3 found:22297 times
character:8 found:27540 times
character:0 found:174030 times
character:2 found:40654 times
character:5 found:9022 times
character:4 found:23961 times
character:1 found:32497 times
character:7 found:17345 times
character:b found:19418 times
character:9 found:14464 times
character:d found:12904 times
character:f found:140847 times
character:a found:15099 times
character:e found:12454 times
character:c found:16518 times
character:6 found:23574 times
```
</details>

```python3
************************
generated:99 Packets
************************
***********************
Ended Successfully!
***********************

In [44]: agfs.edap.packets                                                                                                                                          
```

<details>
```python3
Out[44]: 
['3a3cd3f2100661b9bff40f436464db4b1a9d003c10a357481a998149f12a9174e2701e81dabd8c4c3a01ab84e8d6d579b508562cf267e7cf5730000006b0ab2c',
 '42081d4fea4927c06d4144dd5c07ce239e59e01de3d323fcdd0b4f41679d51bd954707a2b0b1b75cec9b66f8dfbd9d719fc00fc9c595347efc62000006b0ab2c',
 '4a301f2c24cb8c2e08d53454490d75f7a2be5332dae4402167dd45877735c974b6f157c701e7dc01012a68df585af7c6100f02f87ffa3267558e000006b0ab2c',
 '342071341a76d245c3649a5c1eedb03f9b958d2400a5173f5bd0280ba5570ac22905958d4f6b26a343b0df13efed425130e05693a2e217a1f3e2000006b0ab2c',
 '7f08d53245e3c79ddb2b1adc505f7bfa8560d200cd59b6ff2db2f9b9349d46b927392c3b0adbc88b273c51f07f2c3e3018e21c497b8f80440100000006b0ab2c',
 '74085d7ac549c79b74f85376ddea9cad8380babe40225ea8710832287ac76757269fe9ccd89ef36c5170170619fd5c0039d2dd49894a31e46c30000006b0ab2c',
 '6f28041b3f3efaca767cea1356cc09388422df4c5fabc3fee7242b757881abba227197c90d5854bbb0dec25b0309b0facfc7c599a8b81828b51a000006b0ab2c',
 '6130cb70ecb6256062653ebf4c7aa8f6d8e72c610d1edb0926c0cda7486835751492e49fa4ea25034736bb1a746364f3ce863efba9a4e8d6d9fc000006b0ab2c',
 '3704b4098b5b6853a2d4d55bc72a52882fc843bbd2558520aefad080dd84f3713825ac1545b9b3279a2c1dc1edccf676ed8570b7ae8fb6cc38bd000006b0ab2c',
 '67086e55d6233cf87058004a670f6439cfbf0438950b061db10ce6ac4673685a3ac1a5b9d7ef5451ba48241605ac6db6da6a37f46570d9d9c583000006b0ab2c',
 '5d18c49cc6fa3fdfc1905301883c04c8ea6c770d1029c380529510d89e2406d21b567dd774d37ca0b72c8dfa4716043629b5d3ba6156c27bfacf000006b0ab2c',
 '1c1c36c5d2612a33bb2c7b4b094cbb4ee75067d61859c97d6fefc3570f6d5c255c7586b6360d39672f5b33489d07d4428905a164d118928da0b5000006b0ab2c',
 '320c2faf3ec660261295ada57f1495cd57f9d887957191344f100977fa2f720c455b88784976aff61c629f09c110748eee70ec51cb486da3f924000006b0ab2c',
 '6200fb148e557cef808569361735a1cd8e6387baa76f9d4e7abb139d5eac51536e9e1587ad183ab1e28c9f519d55682b84be9bfe38f5c461cdcb000006b0ab2c',
 '7c18d5a65db1ca1854b21f90810fbf54c869a1a584bc9d945a98bdca8a7cf2267505a5cdb9cef57a01fb4138a6852628f8cd376dfec4f308f5d5000006b0ab2c',
 '6108e28ee56e02c782fcafef6a0f4fb8295e93b7c2e67a088dfab4901fd886a7aec23b6259899aa74ad509a0cf3a5b483187d8cada6b5ef4744c000006b0ab2c',
 '4f1cae583604188f1b99e18980f40e797f1ad6651dbd5b93e347f4d38faa3bfd5947cc67edd30e32468d45bb692d83a99bc2934609fbba3dfad9000006b0ab2c',
 '0c3ccc2b2d8322c8d0b8a3c9268aced86c5294d83a541e0acadf786302f763b42e91f904b473dcd6ea34d5d2fee0f170ddea3a7851bb453b2273000006b0ab2c',
 '452c266b280d63ce77cae2db122e2fabc7440f470544ea15f031d080eeada3834180bc517332f518814eeb0d0a0a79aecd33763528b54b92b5bc000006b0ab2c',
 '2334243bfb1c8cda6045167c6f50e91e74071eb60fad57e23724860f8b2273ff1e9abb7d5fada1ba8820a149cab49117cb116454a1ffe1c961c8000006b0ab2c',
 '3f38ee382c80049f609c0d1ee4f29e2653460b4b375868b806b2b8cc770ac9121bef73ca983c56c9791b6869ed989f44d626f810e3eb2ea6816b000006b0ab2c',
 '261c3762b3fd0ffd244179a4a58acc39186fa10c175ae1f49881b05c58dc25ad04520f669ecd4b1d56d496922f7239a23d99641c1c9dacbc2841000006b0ab2c',
```
</details>

- [Go Back](#autogadgetfs-tutorial)

---

<a name="Host-gadget-fuzzer"/>

### Gadget fuzzer

```python3

In [11] agfs.help("startGadgetFuzzer")                                                                                                                                                          
****
[+]Help for startGadgetFuzzer Method:
[-]Signature: startGadgetFuzzer(self, vid=None, pid=None, dclass=None, serial='AutoGadgetFS', manufacturer=None, product=None, samples=100, min=0, max=10)


[+]startGadgetFuzzer Help:
This method creates random gadgets to run on the Pi
:param vid: vendor ID
:param pid: product ID
:param dclass: device class
:param serial: serial number
:param manufacturer: manufacturer name
:param product: product name
:param samples: number of gadgets to create and run
:param min: minimum bytes to add to the HID report
:param max: maximum bytes to add to the HID report
:return: None
****

In [12]: agfs.startGadgetFuzzer(vid=50475,pid=1133,serial="AutoGadgetFS",samples=20) 

```

![](https://github.com/ehabhussein/AutoGadgetFS-tutorial/raw/master/agfstutscreens/GadgetFuzzer.png)


- [Go Back](#autogadgetfs-tutorial)

---

<a name="sendhst"/>

### Send packet to host

```python3

In [52]: agfs.help("startQueuewrite")                                                                                                                                                            
****
[+]Help for startQueuewrite Method:
[-]Signature: startQueuewrite(self)


[+]startQueuewrite Help:
initiates a connection to the queue to communicate with the host
****

In [53]: agfs.help("hostwrite")                                                                                                                                                                  
****
[+]Help for hostwrite Method:
[-]Signature: hostwrite(self, payload, isfuzz=0)


[+]hostwrite Help:
This method writes packets to the host either targeting a software or a driver in control of the device
use this when you want to send payloads to a device driver on the host.

:param payload: the message to be sent to the host example: "0102AAFFCC"
:param isfuzz: is the payload coming from the fuzzer ?

****

In [54]: agfs.help("stopQueuewrite")                                                                                                                                                             
****
[+]Help for stopQueuewrite Method:
[-]Signature: stopQueuewrite(self)


[+]stopQueuewrite Help:
stop the thread incharge of communicating with the host machine
****


In [55]: agfs.startQueuewrite()                                                                                                                                                                  
In [56]: agfs.hostwrite("AAAA")                                                                                                                                                          
In [56]: agfs.hostwrite("BBBB")  

In [57]: agfs.stopQueuewrite()  

```


- [Go Back](#autogadgetfs-tutorial)

---

<a name="Control-Transfer-Enumerator"/>

### Device control transfer enumerator

```python3
In [3]: agfs.help("devEnumCtrltrnsf")                                                                                                                                                            
****
[+]Help for devEnumCtrltrnsf Method:
[-]Signature: devEnumCtrltrnsf(self, fuzz='fast')


[+]devEnumCtrltrnsf Help:
This method enumerates all possible combinations of a control transfer request
:param fuzz: "fast" fuzzer (bmRequest is fuzzed against 0x81 and 0xc0 and the other parameters are limited to one byte
             "full" fuzzing (bmRequest is range(0xff) , wValue is range(0xffff) , wIndex is range(0xffff) . USE WITH CARE !!
:return: None

In [4]: agfs.devEnumCtrltrnsf()

**************************************************
Control Transfer requests enumeration started!
**************************************************
**************************
Now at bmRequest[0xa1]
**************************
|-Control transfer found--------------------------------------------------------------------------------
|	  Request:
|		Sent: bmRequest=0xa1, bRequest=0x0,wValue=0x0 , wIndex=0x1,data_length=0xff
|		    |____Received: b'\x00\x84MFG:Cano'...[SNIP]
|	  Decoded:
|		 Response: ..MFG.Canon.CMD.BJRaster3.IVEC.MDL.G2010.series.CLS.PRINTER.DES.Canon.G2010.series.VER.1.040.STA.10.PSE.KMFK02913.CID.CA.BJR520.IJP.
|__________________________________________________________________________________________[*]
|-Control transfer found--------------------------------------------------------------------------------
|	  Request:
|		Sent: bmRequest=0xa1, bRequest=0x0,wValue=0x1 , wIndex=0x1,data_length=0xff
|		    |____Received: b'\x00\x84MFG:Cano'...[SNIP]
|	  Decoded:
|		 Response: ..MFG.Canon.CMD.BJRaster3.IVEC.MDL.G2010.series.CLS.PRINTER.DES.Canon.G2010.series.VER.1.040.STA.10.PSE.KMFK02913.CID.CA.BJR520.IJP.
|__________________________________________________________________________________________[*]
|-Control transfer found--------------------------------------------------------------------------------
|	  Request:
|		Sent: bmRequest=0xa1, bRequest=0x0,wValue=0x2 , wIndex=0x1,data_length=0xff
|		    |____Received: b'\x00\x84MFG:Cano'...[SNIP]
|	  Decoded:
|		 Response: ..MFG.Canon.CMD.BJRaster3.IVEC.MDL.G2010.series.CLS.PRINTER.DES.Canon.G2010.series.VER.1.040.STA.10.PSE.KMFK02913.CID.CA.BJR520.IJP.
|__________________________________________________________________________________________[*]
...SNIP
```

- [Go Back](#autogadgetfs-tutorial)

---

<a name="monint"/>

### Monitor device interfaces for changes

```python3
In [6]: agfs.help("startMonInterfaceChng")                                                                                                                                                       
****
[+]Help for startMonInterfaceChng Method:
[-]Signature: startMonInterfaceChng(self)


[+]startMonInterfaceChng Help:
This method Allows you to monitor a device every 10 seconds in case it suddenly changes its interface configuration.
Like when switching and Android phone from MTP to PTP . you'll get a notification so you can check
your interfaces and adapt to that change using changeintf() method
****

In [7]: agfs.startMonInterfaceChng() 
```

- [Go Back](#autogadgetfs-tutorial)

---

<a name="qclear"/>

### Clearing rabbitMQ Queues

```python3
In [7]: agfs.help("clearqueues")                                                                                                                                                                 
****
[+]Help for clearqueues Method:
[-]Signature: clearqueues(self)


[+]clearqueues Help:
this method clears all the queues on the rabbitMQ queues that are set up
****

In [8]: agfs.clearqueues() 
```

- [Go Back](#autogadgetfs-tutorial)

---

<a name="release"/>

### Releasing the device back to the system

```python3
In [8]: agfs.help("releasedev")                                                                                                                                                                  
****
[+]Help for releasedev Method:
[-]Signature: releasedev(self)


[+]releasedev Help:
releases the device and re-attaches the kernel driver
****

In [9]: agfs.releasedev()                                                                                                                                                                        
Releasing interfaces :
	2
[-] Attaching the kernel driver
Releasing interface: 2
[-] Device released!

```

- [Go Back](#autogadgetfs-tutorial)

---

<a name="reset"/>

### Reset the device

```python3
In [9]: agfs.device.reset()

```

- [Go Back](#autogadgetfs-tutorial)

---

<a name="Help"/>

### Help

### All methods

```python3

In [63]: agfs.help("")

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

In [65]: agfs.help("startMITMusbWifi",source=True)

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

<img src="https://pbs.twimg.com/profile_images/1039931315766870016/ahOvevDU_400x400.jpg" width="166" height="166"> ![JetBrains](https://github.com/ehabhussein/AutoGadgetFS/raw/master/screenshots/JetBrains.png) ![PyUSB](https://github.com/ehabhussein/AutoGadgetFS/raw/master/screenshots/pyusb.png)

- [Go Back](#autogadgetfs-tutorial)

---

<a name="Slack"/>

### Join Slack:

Visit [AutogadgetFS Slack Channel](https://join.slack.com/t/autogadgetfs/shared_invite/zt-emgcv3ol-unG_axHmSQlk~5GcBddhlQ){:target="_blank"}


- [Go Back](#autogadgetfs-tutorial)

---

<a name="Donate"/>

### Buy me a coffee to support the development of this project

[![PayPal Donations](https://img.shields.io/static/v1?logo=Donate&label=Donate&message=To%20support%20the%20development%20of%20AGFS&color=blue)](https://www.paypal.me/autogadgetfs){:target="_blank"}

- [Go Back](#autogadgetfs-tutorial)

---

<a name="Contact"/>

### Contact me:

### 📧: <rd@agfs.io>

### 🐦 : [https://twitter.com/0xRaindrop](https://twitter.com/0xRaindrop){:target="_blank"}

- [Go Back](#autogadgetfs-tutorial)

---

<a name="Cont"/>

### Contribute:

We're looking for developers to make this tool great! send me an 📧: <rd@agfs.io> if you feel you'd like to be a part of this.

- [Go Back](#autogadgetfs-tutorial)
