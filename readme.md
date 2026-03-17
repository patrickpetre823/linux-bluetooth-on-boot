## Problem

When booting Linux, my mouse and other Bluetooth devices would sometimes not connect automatically. Since my mouse is Bluetooth-only, I could only resolve this issue via keyboard.

## Solution

Going into `bluetoothctl` and running `scan on` did not work and returned the following error:
```
[bluetooth]# scan on
[bluetooth]# SetDiscoveryFilter failed: org.bluez.Error.NotReady
[bluetooth]# Failed to start discovery: org.bluez.Error.NotReady
```

Checking `rfkill list` revealed that the Bluetooth adapter was soft blocked:
```
rfkill list
0: hci0: Bluetooth
    Soft blocked: yes
    Hard blocked: no
1: phy0: Wireless LAN
    Soft blocked: no
    Hard blocked: no
```

`hci0` is the standard name for the first Host Controller Interface (HCI) device, which is the name the Linux kernel uses for a Bluetooth adapter. Unblocking it caused the system to automatically reconnect to all Bluetooth devices:
```bash
rfkill unblock all
```

## Alternative Solution

In some cases a simple `bluetoothtcl power on` is all it takes.
