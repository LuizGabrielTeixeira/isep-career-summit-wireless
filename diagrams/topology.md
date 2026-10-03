# Topology

```mermaid
flowchart TB
    Internet[Internet]
    Router[Upstream Router<br/>Gateway / DHCP / Internet]
    Switch[Cisco Catalyst 2960 SI PoE<br/>Layer 2]
    Host[PC Host]
    WLC[Cisco Virtual WLC]

    subgraph Wireless["Wireless Infrastructure"]
        AP1[Cisco AIR-CAP2602E<br/>AP1]
        AP2[Cisco AIR-CAP2602E<br/>AP2]
        AP3[Cisco AIR-CAP2602E<br/>AP3]
    end

    Clients[Wireless Clients]

    Internet --> Router
    Router --> Switch

    Switch -->|Fa0/4| Host
    Host --> WLC

    Switch -->|Fa0/1 + PoE| AP1
    Switch -->|Fa0/2 + PoE| AP2
    Switch -->|Fa0/3 + PoE| AP3

    AP1 -. CAPWAP / DTLS .-> WLC
    AP2 -. CAPWAP / DTLS .-> WLC
    AP3 -. CAPWAP / DTLS .-> WLC

    AP1 --> Clients
    AP2 --> Clients
    AP3 --> Clients
```

## Switching View

```mermaid
flowchart LR
    SW[Catalyst 2960]
    A1[Fa0/1 - AP1]
    A2[Fa0/2 - AP2]
    A3[Fa0/3 - AP3]
    W[Fa0/4 - WLC Host]
    U[Gi0/1 - Upstream]
    B[Unused Ports<br/>VLAN 99 + shutdown]

    SW --> A1
    SW --> A2
    SW --> A3
    SW --> W
    SW --> U
    SW --> B
```

## Addressing Concept

```text
Client DHCP pool
        |
        | dynamic client addressing
        v

upper addresses reserved for infrastructure:

.251  switch management
.252  WLC host
.253  virtual WLC
.254  gateway
```
