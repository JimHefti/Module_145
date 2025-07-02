# VLAN und Trunking Konfiguration – Cisco Packet Tracer

## Part 1: VLANs konfigurieren

```bash
conf t
vlan 10
name Admin
vlan 20
name Accounts
vlan 30
name HR
vlan 40
name Voice
vlan 99
name Management
vlan 100
name Native
end
```

**Stichwort:** VLANs müssen auf allen drei Switches (SWA, SWB, SWC) eingerichtet werden.

---

## Part 2: Ports zu VLANs zuweisen

### SWB – Access Ports

```bash
interface fa0/1
 switchport mode access
 switchport access vlan 10


interface fa0/2
 switchport mode access
 switchport access vlan 20


interface fa0/3
 switchport mode access
 switchport access vlan 30

```

### SWC – Access Ports + Voice VLAN

```bash
interface fa0/1
 switchport mode access
 switchport access vlan 10
exit

interface fa0/2
 switchport mode access
 switchport access vlan 20
exit

interface fa0/3
 switchport mode access
 switchport access vlan 30
exit

interface fa0/4
 switchport mode access
 switchport access vlan 10
 switchport voice vlan 40
exit
```

**Stichwort:** Fa0/4 auf SWC nutzt VLAN 10 für Daten und VLAN 40 für Voice.

---

## Part 3: Statisches Trunking konfigurieren (SWA ↔ SWB)

### SWA – G0/1

```bash
interface g0/1
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport nonegotiate
 switchport trunk native vlan 100

```

### SWB – G0/1

```bash
interface g0/1
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport nonegotiate
 switchport trunk native vlan 100

```

**Stichwort:** Statische Trunks mit ausgeschaltetem DTP und gleichem Native VLAN (100).

---

## Part 4: Dynamisches Trunking konfigurieren (SWA ↔ SWC)

### SWA – G0/2

```bash
interface g0/2
 switchport trunk encapsulation dot1q
 switchport mode dynamic desirable
 switchport trunk native vlan 100

```

### SWC – G0/2 (falls Korrektur notwendig)

```bash
interface g0/2
 switchport trunk native vlan 100

```

**Stichwort:** SWA handelt Trunking mit SWC aus, das im Standard auf dynamic auto steht.

---

## Management-VLAN (SVI) konfigurieren

### SWA

```bash
interface vlan 99
 ip address 192.168.99.252 255.255.255.0
 no shutdown
```


### SWB

```bash
interface vlan 99
 ip address 192.168.99.253 255.255.255.0
 no shutdown

```

### SWC

```bash
interface vlan 99
 ip address 192.168.99.254 255.255.255.0
 no shutdown

```

**Stichwort:** Die Switches sollen sich **nicht gegenseitig pingen können**, da kein Routing aktiviert ist.
