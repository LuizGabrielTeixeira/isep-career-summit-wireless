# Validation

Validation was performed at multiple layers rather than relying on a single connectivity test.

## Switching

### Interface State

```text
show interfaces status
```

Expected active links:

```text
Fa0/1  AP1
Fa0/2  AP2
Fa0/3  AP3
Fa0/4  WLC host
Gi0/1  upstream
```

### VLANs

```text
show vlan brief
```

Used to confirm active access ports in the event VLAN and inactive ports in the blackhole VLAN.

### MAC Learning

```text
show mac address-table dynamic
```

MAC addresses for APs and the WLC host were observed on the expected ports.

### CDP

```text
show cdp neighbors
show cdp neighbors detail
```

The Aironet devices appeared as Cisco AP neighbors.

## PoE

```text
show power inline
```

Observed values:

```text
Available: 124.0 W
Used:       46.2 W
Remaining:  77.8 W
```

Each AP used approximately:

```text
15.4 W
```

This confirmed adequate PoE budget for the three access points.

## Management Connectivity

The switch management SVI was observed up/up during testing.

APs received management addresses through DHCP.

## AP-to-WLC Connectivity

The APs were tested for IP reachability to the WLC before controller association troubleshooting.

This was important because it separated:

- network reachability;
- CAPWAP/DTLS association.

## Internet Connectivity

Internet reachability was also tested from the network.

Observed ping result:

```text
Success rate is 100 percent
```

## WLC Validation

Controller-side checks included:

```text
show ap summary
show client summary
show wlan summary
show ap join stats summary all
```

These commands were used to inspect AP association, WLAN state and connected wireless clients.
