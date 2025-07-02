# Cisco Packet Tracer: Configure Trunks
tzt.

---

##  Addressing Table

| PC  | IP Address     | VLAN | Switch | Port   |
|-----|----------------|------|--------|--------|
| PC1 | 172.17.10.21   | 10   | S2     | F0/11  |
| PC2 | 172.17.20.22   | 20   | S2     | F0/18  |
| PC3 | 172.17.30.23   | 30   | S2     | F0/6   |
| PC4 | 172.17.10.24   | 10   | S3     | F0/11  |
| PC5 | 172.17.20.25   | 20   | S3     | F0/18  |
| PC6 | 172.17.30.26   | 30   | S3     | F0/6   |

---

## PART 1: VERIFY VLANs

### Step 1a – VLANs auf S1 anzeigen

```bash
show vlan brief
```

---

### Step 1b – VLANs auf S2 und S3 anzeigen

```bash
show vlan brief
```

---

### Step 2 – Ping-Tests (vor Trunk-Konfiguration)

```bash
ping 172.17.10.24
ping 172.17.20.25
ping 172.17.30.26
```
 Ergebnis: Pings schlagen fehl → VLAN-Traffic kann Switch-Grenzen nicht überschreiten (noch kein Trunk).

---

## PART 2: CONFIGURE TRUNKS

### Step 1 – Trunks auf S1 konfigurieren (Native VLAN 99)

```bash
interface range g0/1 - 2
switchport mode trunk
switchport trunk native vlan 99
```

---

### Step 2 – Trunk-Status prüfen auf S2 und S3

```bash
show interface trunk
```

---

### Step 3 – Native VLAN auf S2 und S3 korrigieren

#### S2 (Port G0/1):

```bash
interface g0/1
switchport mode trunk
switchport trunk native vlan 99
```

#### S3 (Port G0/2):

```bash
interface g0/2
switchport mode trunk
switchport trunk native vlan 99
```

---

### Step 4a – Native VLAN prüfen (S2/S3)

```bash
show interface g0/1 switchport
show interface g0/2 switchport
```

---

### Step 4b – VLANs prüfen

```bash
show vlan brief
```

---

## Verständnisfragen

### Warum funktioniert der Ping trotz Native VLAN Mismatch?

Weil VLAN-getaggte Frames korrekt übermittelt werden. Der Native VLAN wird nur für **untagged Frames** verwendet.

---

### Welche VLANs dürfen über den Trunk?

 Alle VLANs (1–4094), aber **aktiv sind nur die VLANs**, die auch auf dem Switch existieren (z. B. 10, 20, 30).

---

### ❓ Warum ist Port G0/1 auf S2 nicht mehr in VLAN 1?

Weil der Port jetzt im **Trunk-Modus** ist und nicht mehr Teil eines einzelnen VLANs ist. Trunk-Ports erscheinen nicht mehr in der VLAN-Tabelle.




