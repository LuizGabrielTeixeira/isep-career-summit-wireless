# Troubleshooting

## 1. APs Could Reach the WLC but Would Not Join

### Symptom

Layer 3 connectivity worked:

```text
AP -> WLC ping: successful
```

but the APs did not complete controller association.

The logs showed DTLS certificate failure.

### Investigation

The failure pattern separated the problem into two layers:

```text
IP reachability      OK
CAPWAP initiation    observed
DTLS negotiation     FAILED
AP join              FAILED
```

The AP MIC certificate was found to be expired. CAPWAP initiation was observed, but DTLS negotiation did not complete, so the APs had not successfully joined the WLC.

### Resolution

The WLC was configured to ignore MIC certificate expiry for the legacy APs.

Conceptually:

```text
config ap cert-expiry-ignore mic enable
save config
```

After this change, the APs could progress through the join process.

### Lesson

The key distinction was that successful IP reachability did not imply a completed CAPWAP/DTLS association or successful AP join.

---

## 2. AP Could Not Discover the Controller

### Symptom

The AP reported that it could not discover a WLC.

### Resolution

The AP was manually pointed to the controller using the WLC name and management address.

This removed ambiguity from automatic controller discovery during deployment.

---

## 3. AP Received an Address From the Wrong Network

### Symptom

An AP obtained an address from an unexpected subnet.

### Investigation

The unexpected DHCP lease indicated that traffic was reaching an unintended network path.

Potential sources considered during troubleshooting included:

- virtualization NAT;
- host-only networking;
- virtual host interfaces;
- Internet-sharing services;
- parallel DHCP services.

### Resolution

The WLC virtual machine was connected using bridged networking so that the APs and controller shared the intended physical LAN.

### Lesson

Virtualization networking mode is part of the network design. NAT or host-only networking can prevent lightweight APs from reaching the intended controller even when the VM itself appears functional.
