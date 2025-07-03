# Inter-VLAN Routing Challenge – 100% Lösung

Diese Anleitung beschreibt die vollständige Konfiguration für ein funktionierendes Inter-VLAN-Routing-Szenario mit statischem Routing zum Servernetzwerk. Geeignet für Cisco Packet Tracer.

---

## Part 1: Switch S1 konfigurieren

### VLANs erstellen & benennen
```bash
enable
configure terminal

vlan 10
name Faculty/Staff
vlan 20
name Students
vlan 30
name Guest(Default)
vlan 88
name Native
vlan 99
name Management
```

### Ports VLANs zuweisen (Access Mode)
```bash
interface range f0/11 - 17
switchport mode access
switchport access vlan 10

interface range f0/18 - 24
switchport mode access
switchport access vlan 20

interface range f0/6 - 10
switchport mode access
switchport access vlan 30
```

### Trunk konfigurieren (Gi0/1)
```bash
interface g0/1
switchport mode trunk
switchport trunk native vlan 88
```

### Management-IP (VLAN 99)
```bash
interface vlan 99
ip address 172.17.99.10 255.255.255.0
no shutdown

ip default-gateway 172.17.99.1
```

### Unbenutzte Ports deaktivieren
```bash
interface range f0/1 - 5
shutdown

interface range f0/25 - 48
shutdown

interface g0/2
shutdown
```

### Konfiguration speichern
```bash
end
write memory
```

---

## Part 2: Router R1 konfigurieren (Router-on-a-Stick)

### Verbindung zum HQ (G0/0)
```bash
interface g0/0
ip address 172.17.25.2 255.255.255.252
no shutdown
```

### Subinterfaces für VLANs
```bash
interface g0/1.10
encapsulation dot1Q 10
ip address 172.17.10.1 255.255.255.0

interface g0/1.20
encapsulation dot1Q 20
ip address 172.17.20.1 255.255.255.0

interface g0/1.30
encapsulation dot1Q 30
ip address 172.17.30.1 255.255.255.0

interface g0/1.99
encapsulation dot1Q 99
ip address 172.17.99.1 255.255.255.0

interface g0/1.88
encapsulation dot1Q 88 native
ip address 172.17.88.1 255.255.255.0
```

### Trunk-Interface aktivieren
```bash
interface g0/1
no shutdown
```

### Konfiguration speichern
```bash
end
write memory
```

---

## Part 3: IP-Konfiguration für PCs & Server

In Packet Tracer: PC > Desktop > IP Configuration

| Gerät | IP-Adresse       | Subnetmaske       | Gateway         |
|--------|------------------|-------------------|-----------------|
| PC1    | 172.17.10.21     | 255.255.255.0     | 172.17.10.1     |
| PC2    | 172.17.20.22     | 255.255.255.0     | 172.17.20.1     |
| PC3    | 172.17.30.23     | 255.255.255.0     | 172.17.30.1     |
| Server | 172.17.50.254    | 255.255.255.0     | 172.17.50.1     |

---

## Part 4: Statische Route zum Servernetz (auf R1)

```bash
ip route 172.17.50.0 255.255.255.0 172.17.25.1
```

---

## Part 5: Ping-Testplan zur Funktionsprüfung

Von jedem PC aus im Terminal (Command Prompt):
```bash
ping 172.17.10.1      ! Gateway PC1
ping 172.17.20.1      ! Gateway PC2
ping 172.17.30.1      ! Gateway PC3
ping 172.17.99.1      ! Gateway VLAN 99
ping 172.17.99.10     ! Switch S1 Management-IP
ping 172.17.50.254    ! Server im HQ
ping 172.17.25.2      ! R1 G0/0 Richtung HQ
ping 172.17.20.22     ! PC2 aus PC1
ping 172.17.30.23     ! PC3 aus PC2
```


