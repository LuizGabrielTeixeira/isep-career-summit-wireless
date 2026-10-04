# Lessons Learned

## Keep the temporary design simple

The Catalyst 2960 was used strictly as a Layer 2 access switch.

Gateway, DHCP and Internet access remained on the upstream router. This reduced the number of moving parts for a temporary event network.

## Lightweight APs depend on the controller

The AIR-CAP2602E APs did not require autonomous SSID configuration.

Their main local requirements were:

- receive an IP address;
- reach the WLC;
- complete CAPWAP/DTLS association.

## Ping is necessary but not sufficient

IP reachability between an AP and WLC did not guarantee a successful join.

CAPWAP and DTLS introduced additional control-plane dependencies.

## Legacy certificates can become operational issues

The older APs had expired MIC certificates.

The certificate problem only became visible after basic network connectivity had already been confirmed.

## Virtualization mode matters

The virtual WLC needed direct participation in the physical event LAN.

Bridged networking was therefore an infrastructure requirement, not just a VM preference.

## Physical validation matters

Commands such as:

```text
show power inline
show mac address-table dynamic
show cdp neighbors
```

were useful because they validated physical and Layer 2 behavior before troubleshooting higher-layer wireless problems.

## RF channel planning matters

Distributing the neighboring APs across 2.4 GHz channels 1, 6 and 11 reduced avoidable channel overlap in this deployment.
