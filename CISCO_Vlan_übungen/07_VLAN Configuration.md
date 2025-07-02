#  VLAN-Konfiguration in Cisco Packet Tracer

##  Netzwerkübersicht

In diesem Projekt wurden 6 PCs in 3 VLANs aufgeteilt:

| Gerät | IP-Adresse       | VLAN | Switch |
|-------|------------------|------|--------|
| PC1   | 172.17.10.21     | 10   | S2     |
| PC2   | 172.17.20.22     | 20   | S2     |
| PC3   | 172.17.30.23     | 30   | S2     |
| PC4   | 172.17.10.24     | 10   | S3     |
| PC5   | 172.17.20.25     | 20   | S3     |
| PC6   | 172.17.30.26     | 30   | S3     |



---

## ⚙️ Schritt 1: VLANs auf allen Switches erstellen

```bash
enable
configure terminal

vlan 10
name Faculty/Staff

vlan 20
name Students

vlan 30
name Guest(Default)

vlan 99
name Management&Native

vlan 150
name VOICE

````

## Switch Access-Ports auf Switch S2 konfigurieren

```` bash
enable
configure terminal

interface fastethernet 0/11
switchport mode access
switchport access vlan 10

interface fastethernet 0/18
switchport mode access
switchport access vlan 20

interface fastethernet 0/6
switchport mode access
switchport access vlan 30

`````


## Schritt 3: Access-Ports auf Switch S3 konfigurieren

````Bash
enable
configure terminal

interface fastethernet 0/11
switchport mode access
switchport access vlan 10

interface fastethernet 0/18
switchport mode access
switchport access vlan 20

interface fastethernet 0/6
switchport mode access
switchport access vlan 30

````
## Schritt 4: VOICE VLAN auf S3 F0/11 konfigurieren

````bash
enable
configure terminal

interface fastethernet 0/11
switchport voice vlan 150

`````

## Schritt 5 Lösung: Trunk-Ports zwischen den Switches konfigurieren

### Auf Switch S1 (Verbindung zu S2 und S3)
````bash

enable
configure terminal

interface gigabitEthernet 0/1
switchport mode trunk

interface gigabitEthernet 0/2
switchport mode trunk

`````

### Auf Switch S2 (Verbindung zu S1)
```bash
enable
configure terminal

interface gigabitEthernet 0/1
switchport mode trunk

````

### Auf Switch S3 (Verbindung zu S1)
```bash
enable
configure terminal

interface gigabitEthernet 0/2
switchport mode trunk

```

