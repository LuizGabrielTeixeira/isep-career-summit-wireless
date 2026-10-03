# Switching

## VLANs

Two VLANs were used on the Catalyst switch.

| VLAN | Name | Purpose |
|---:|---|---|
| 111 | SUMMIT | Operational event network |
| 99 | BLACKHOLE | Unused ports |

## Active Ports

| Port | Role | Mode |
|---|---|---|
| Fa0/1 | AP1 | Access VLAN 111 |
| Fa0/2 | AP2 | Access VLAN 111 |
| Fa0/3 | AP3 | Access VLAN 111 |
| Fa0/4 | WLC host | Access VLAN 111 |
| Gi0/1 | Upstream router/network | Access VLAN 111 |

## Edge Protection

The AP and WLC-host access ports used:

- `spanning-tree portfast`
- `spanning-tree bpduguard enable`

This reduced normal edge-port convergence delay while protecting the access layer from unexpected BPDUs.

## Unused Ports

Unused interfaces were:

- moved to VLAN 99;
- administratively shut down.

This reduced accidental connectivity and unnecessary exposure during the event.

## Management

The switch used a management SVI on the operational VLAN.

During testing DHCP was used. The final addressing plan reserved `.251` for switch management with `.254` as the default gateway.

## Management Surface

The switch HTTP and HTTPS services were disabled.

## Verification Commands

Typical verification included:

```text
show interfaces status
show vlan brief
show ip interface brief
show power inline
show mac address-table dynamic
show cdp neighbors
show cdp neighbors detail
```

These commands were used to verify link state, VLAN placement, management status, AP discovery and PoE delivery.
