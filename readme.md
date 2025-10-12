## Problem

When booting linux OS sometimes my mouse or other bluetooth devices would not connect. As my Mouseis bluetooth only, it let me solve this problem only via keyboard.

## Solution

Going into bluetoothctl and entering scan on, did not work and stated

 ```
[bluetooth]# scan on
[bluetooth]# SetDiscoveryFilter failed: org.bluez.Error.NotReady
[bluetooth]# Failed to start discovery: org.bluez.Error.NotReady
```

Checking rfkill list showed that some are blocked

```
rfkill list
0: hci0: Bluetooth
	Soft blocked: yes
	Hard blocked: no
1: phy0: Wireless LAN
	Soft blocked: no
	Hard blocked: no
```

hci0 is the standard name for the first host controller interface (HCI) device, which is the name the Linux kernel uses for a Bluetooth adapter. unblocking it made my system automatically connect to my bluetooth devices. 

```
rfkill unblock all
```
