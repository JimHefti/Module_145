# Packet Tracer – MAC- und IP-Adressen identifizieren

## Zielsetzung

- **Teil 1:** PDU-Daten im lokalen Netzwerk erfassen  
- **Teil 2:** PDU-Daten bei Kommunikation über Netzwerke hinweg erfassen  
- **Teil 3:** Reflexionsfragen beantworten

---

## Teil 1: Lokale Netzwerkkommunikation – PDU-Informationen

### Ping von 172.16.31.5 → 172.16.31.2

| Gerät       | Ziel-MAC       | Quell-MAC      | Quell-IP     | Ziel-IP      |
|------------|----------------|----------------|--------------|--------------|
| 172.16.31.5 | 000C:85CC:1DA7 | 00D0:D311:C788 | 172.16.31.5  | 172.16.31.2  |
| Switch1     | 000C:85CC:1DA7 | 00D0:D311:C788 | 172.16.31.5  | 172.16.31.2  |
| 172.16.31.2 | 00D0:D311:C788 | 000C:85CC:1DA7 | 172.16.31.2  | 172.16.31.5  |

### Ping von 172.16.31.3 → 172.16.31.2

| Gerät       | Ziel-MAC       | Quell-MAC      | Quell-IP     | Ziel-IP      |
|------------|----------------|----------------|--------------|--------------|
| 172.16.31.3 | 000C:85CC:1DA7 | 00D0:588C:2401 | 172.16.31.3  | 172.16.31.2  |
| Switch1     | 000C:85CC:1DA7 | 00D0:588C:2401 | 172.16.31.3  | 172.16.31.2  |
| 172.16.31.2 | 00D0:588C:2401 | 000C:85CC:1DA7 | 172.16.31.2  | 172.16.31.3  |

### Ping von 172.16.31.5 → 172.16.31.4

| Gerät       | Ziel-MAC       | Quell-MAC      | Quell-IP     | Ziel-IP      |
|------------|----------------|----------------|--------------|--------------|
| 172.16.31.5 | 00D0:234C:1FA1 | 00D0:D311:C788 | 172.16.31.5  | 172.16.31.4  |
| Switch1     | 00D0:234C:1FA1 | 00D0:D311:C788 | 172.16.31.5  | 172.16.31.4  |
| 172.16.31.4 | 00D0:D311:C788 | 00D0:234C:1FA1 | 172.16.31.4  | 172.16.31.5  |

---

## Teil 2: Kommunikation über Netzwerke hinweg – PDU-Informationen

### Ping von 172.16.31.5 → 10.10.10.2

| Gerät         | Ziel-MAC       | Quell-MAC      | Quell-IP     | Ziel-IP      |
|---------------|----------------|----------------|--------------|--------------|
| 172.16.31.5    | 00D0:BA8E:741A | 00D0:D311:C788 | 172.16.31.5  | 10.10.10.2   |
| Switch1        | 00D0:BA8E:741A | 00D0:D311:C788 | 172.16.31.5  | 10.10.10.2   |
| Router         | 0060:2F84:4AB6 | 00D0:BA8E:741A | 172.16.31.5  | 10.10.10.2   |
| Switch0        | 0060:2F84:4AB6 | 00D0:588C:2401 | 172.16.31.5  | 10.10.10.2   |
| Access Point   | 0060:2F84:4AB6 | 00D0:588C:2401 | 172.16.31.5  | 10.10.10.2   |
| 10.10.10.2     | 00D0:588C:2401 | 0060:2F84:4AB6 | 10.10.10.2   | 172.16.31.5  |

---

## Teil 3: Reflexionsfragen – Antworten

1. **Wurden unterschiedliche Kabel oder Medien verwendet?**  
   Ja, sowohl Kupferkabel (Ethernet) als auch drahtlose Verbindungen kamen zum Einsatz.

2. **Beeinflussen die Kabel die PDU-Struktur?**  
   Nein, die PDU bleibt gleich, nur das Übertragungsmedium ändert sich.

3. **Hat der Hub Informationen verloren?**  
   Nein, aber er leitet sie an alle angeschlossenen Ports weiter.

4. **Wie geht der Hub mit MAC- und IP-Adressen um?**  
   Er verarbeitet diese nicht, sondern sendet alles an alle Ports.

5. **Hat der Access Point aktiv mit den Daten gearbeitet?**  
   Ja, er leitete sie basierend auf der MAC-Adresse gezielt weiter.

6. **Ging beim Funkverkehr eine MAC- oder IP-Adresse verloren?**  
   Nein, alle Adressen blieben erhalten.

7. **Auf welcher OSI-Schicht arbeiten Hub und Access Point maximal?**  
   - Hub: Schicht 1 (Physikalisch)  
   - Access Point: Schicht 2 (Sicherung)

8. **Haben Hub oder Access Point PDUs dupliziert, die abgelehnt wurden?**  
   Nein, es wurde nichts weitergeleitet, was mit „rotem X“ markiert war.

9. **Welche MAC-Adresse steht im PDU-Detail zuerst?**  
   Die Zieladresse erscheint vor der Quelladresse.

10. **Warum erscheint zuerst die Zieladresse?**  
    Damit das Frame korrekt zugestellt werden kann.

11. **Gab es ein Muster bei den MAC-Adressen?**  
    Ja, Geräte desselben Typs hatten ähnliche Adress-Präfixe.

12. **Haben Switches abgelehnte PDUs dupliziert?**  
    Nein, sie arbeiten MAC-basiert und leiten gezielt weiter.

13. **Wo ändern sich die MAC-Adressen im Netzwerkpfad zwischen 172er und 10er-Netz?**  
    Beim Übergang über den Router.

14. **Welche Geräte hatten MAC-Adressen mit 00D0:BA?**  
    Eine Router-Schnittstelle, die mit dem 172.16.31.x-Netz verbunden ist.

15. **Wer hatte die restlichen MAC-Adressen?**  
    PCs, Router, Switches und Access Points.

16. **Haben sich die IP-Adressen der Pakete auf dem Weg verändert?**  
    Nein, sie bleiben durchgehend gleich.

17. **Tauschen sich Quell- und Ziel-IP beim Ping-Antwortpaket?**  
    Ja, Quelle wird Ziel und umgekehrt.

18. **Gab es ein Schema bei den IPs?**  
    Ja: 172.16.31.x für interne Geräte, 10.10.10.x für externe.

19. **Warum braucht ein Router verschiedene IP-Netze an seinen Ports?**  
    Damit er unterschiedliche Subnetze verbinden und weiterleiten kann.

20. **Was wäre bei IPv6 anders?**  
    - Adressen wären länger  
    - Trennung durch Doppelpunkte  
    - ARP wird durch NDP ersetzt
