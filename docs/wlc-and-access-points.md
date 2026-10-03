# WLC and Access Points

## Access Points

The deployment used three:

```text
Cisco AIR-CAP2602E-E-K9
```

The APs were operating with a lightweight image:

```text
AP3G2-K9W8-M
```

This meant the APs relied on the Wireless LAN Controller rather than being configured as autonomous access points.

## CAPWAP

CAPWAP provided the control relationship between APs and the WLC.

Main ports:

| UDP Port | Purpose |
|---:|---|
| 5246 | CAPWAP control |
| 5247 | CAPWAP data |

The expected join flow was:

```text
AP powers on
    |
receives IP by DHCP
    |
discovers / is pointed to WLC
    |
CAPWAP session
    |
DTLS establishment
    |
AP joins controller
    |
WLC pushes configuration
    |
AP advertises SSID
```

## Controller Discovery

Where automatic discovery was insufficient, the APs were explicitly pointed to the virtual controller.

Conceptually:

```text
capwap ap primary-base <WLC-NAME> <WLC-IP>
```

Older command syntax was retained as a fallback for compatibility with the AP platform.

## WLC

The Cisco Virtual Wireless Controller ran on a PC connected to the same Layer 2 event network as the APs.

The WLC centralized:

- AP management;
- SSID creation;
- WPA2-PSK security;
- radio control;
- client visibility;
- CAPWAP termination.

## Wireless Design

The final event design used:

- one event SSID;
- WPA2-PSK;
- DHCP from the upstream router;
- WLC management on the event LAN;
- AP mode: Local;
- no VLAN tagging between switch and WLC in the simplified final design.

## Operational Checks

Useful AP checks included:

```text
show version
show ip interface brief
show capwap client config
show capwap client state
show logging
show crypto pki certificates
```

Useful WLC checks included:

```text
show ap summary
show client summary
show wlan summary
show country
show sysinfo
show ap join stats summary all
```
