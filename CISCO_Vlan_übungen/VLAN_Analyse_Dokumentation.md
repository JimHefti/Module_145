
# VLAN Implementation – Analyse in Cisco Packet Tracer

## 🧾 Dokumentation: VLAN-Verhalten beobachten

---

## 🔷 Teil 1 – VLANs sind aktiv

### ✅ Ziel:
Beobachten, wie Broadcast-Traffic durch VLANs eingeschränkt wird.

---

### 🔹 Schritt 1: Ping von PC1 zu PC6 (VLAN10 → VLAN30)

**Was zu tun ist:**
1. In **Simulation Mode** wechseln
2. Auf **Add Simple PDU** klicken (Briefumschlag mit grünem Plus)
3. **PC1 anklicken**, dann **PC6**

**IP-Adressen:**
- PC1: `172.17.10.21` (VLAN 10)
- PC6: `172.17.30.26` (VLAN 30)

**Beobachtung / Ergebnis:**
- ❌ **Ping schlägt fehl**
- ARP-Request wird **nur innerhalb von VLAN 10** weitergeleitet
- PC6 empfängt ihn nicht → **keine ARP-Antwort → kein Ping**

---

### 🔹 Schritt 2: Ping von PC1 zu PC4 (VLAN10 → VLAN10)

**Was zu tun ist:**
1. Klicke auf **„New“** im Szenario-Menü
2. Add Simple PDU: **PC1 → PC4**

**IP-Adressen:**
- PC1: `172.17.10.21` (VLAN 10)
- PC4: `172.17.10.24` (VLAN 10)

**Beobachtung / Ergebnis:**
- ✅ **Ping erfolgreich**
- ARP-Request wird im VLAN 10 gebroadcastet
- PC4 antwortet → ICMP-Paket geht durch

---

## 🔷 Teil 2 – VLAN-Konfiguration entfernen

### ✅ Ziel:
Alle Switches zurücksetzen und das Verhalten **ohne VLANs** beobachten.

---

### 🔹 Schritt 1: Konfiguration löschen auf allen Switches

**Auf jedem Switch (S1, S2, S3):**

```
erase startup-config
delete flash:vlan.dat
reload
```

**Wichtig:**
- Bei „Save? [yes/no]“ → `no` eingeben
- Nach dem Boot erscheint `switch:`

**Dann eingeben:**

```
boot
```

- Sobald gefragt wird:
  „Would you like to enter the initial configuration dialog?“ → `no`

Dann:

```
Switch> enable
Switch#
```

---

### 🔹 Schritt 2: Ping von PC1 zu PC6 (ohne VLANs)

**Was zu tun ist:**
1. Wieder in den **Simulation Mode**
2. **Add Simple PDU:** PC1 → PC6

**IP-Adressen:**
- PC1: `172.17.10.21`
- PC6: `172.17.30.26`

**Beobachtung / Ergebnis:**
- ✅ **Ping funktioniert**
- ARP-Request wird **an alle Ports** weitergeleitet
- PC6 antwortet → Ping geht durch

---

## 🟢 Zusammenfassung: Ping-Ergebnisse

| Quelle     | Ziel       | VLANs aktiv? | Ergebnis         |
|------------|------------|--------------|------------------|
| PC1 → PC6  | Ja         | ❌ schlägt fehl |
| PC1 → PC4  | Ja         | ✅ funktioniert |
| PC1 → PC6  | Nein       | ✅ funktioniert |

---

## ❓ Reflection Questions – Antworten

1. **PC in VLAN 10 sendet Broadcast → Wer empfängt?**  
   ➤ Nur PCs im VLAN 10 (PC1, PC4, PC7)

2. **PC in VLAN 20 sendet Broadcast → Wer empfängt?**  
   ➤ Nur PCs in VLAN 20 (PC2, PC5, PC8)

3. **PC in VLAN 30 sendet Broadcast → Wer empfängt?**  
   ➤ Nur PCs in VLAN 30 (PC3, PC6, PC9)

4. **Frame von VLAN 10 → VLAN 30?**  
   ➤ Wird verworfen. VLANs sind logisch getrennt. Kein Routing → keine Verbindung.

5. **Collision Domains pro Port?**  
   ➤ Jeder Port ist eine eigene Collision Domain.

6. **Broadcast Domains pro VLAN?**  
   ➤ Jedes VLAN ist eine eigene Broadcast Domain.

---

## ✅ Fazit
VLANs verbessern die Netzwerkauslastung, da Broadcasts isoliert werden.  
Ohne VLANs steigt der Broadcast-Verkehr, da alle Geräte erreichbar sind – das reduziert die Performance bei großen Netzen.
