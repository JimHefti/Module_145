## Was ist ein Vlan?
Statt für jedes neue Netzwerk eigene Hardware (z. B. Switches) zu verwenden, ermöglichen VLANs (Virtual LANs) die Aufteilung eines physischen Netzwerks in mehrere virtuelle, voneinander getrennte Netzwerke. Diese laufen auf derselben Hardware, sind jedoch logisch getrennt. Dadurch spart man Kosten, verbessert die Sicherheitsstruktur und kann Zugriffe effizienter steuern.

## Warum Vlan?
VLANs ermöglichen eine strikte Trennung von Netzwerken auf Layer 2, verhindern unerwünschte Datenübertragung (z. B. Broadcasts) und steigern so die Sicherheit. Sie bieten Flexibilität, da Geräte unabhängig vom Standort logisch gruppiert werden können. VLANs erleichtern die Priorisierung von Diensten wie VoIP und helfen, die Komplexität großer Netzwerke durch Segmentierung zu reduzieren. Sicherheitsrelevante Systeme lassen sich gezielt abschotten. Für die Kommunikation zwischen VLANs werden Router bzw. Layer-3-Switches eingesetzt, die zusätzliche Sicherheitsfunktionen wie Firewalls ermöglichen.

## Wie funktioniert ein VLAN?
Die Zuordnung der Teilnetzwerke auf dem Switch (oder den Switches) kann auf zwei Arten erfolgen, als Portbasierte VLANs (Untagged) der als Tagged VLANs.


## Portbasierte VLANs

Mit portbasierten VLANs unterteilen Sie einen einzelnen physischen Switch einfach auf mehrere logische Switches (VLANs). Dabei wird jedem Port ein VLAN zugewiesen.

![image](https://github.com/user-attachments/assets/922a86e7-cd70-49f9-aa88-015cf3a1c6bf)

Im folgenden Beispiel teilen wir einen physischen 8-Port Switch (Switch A) auf zwei logische Switches auf:
| Switch-Port | VLAN ID     | Angeschlossenes Gerät |
|-------------|-------------|------------------------|
| 1           | 1 (grün)    | PC A-1                 |
| 2           |             | PC A-2                 |
| 3           |             | -                      |
| 4           |             | -                      |
| 5           | 2 (orange)  | PC A-5                 |
| 6           |             | PC A-6                 |
| 7           |             | -                      |
| 8           |             |                        |

Obwohl alle PCs an einem physischen Switch angeschlossen sind, können aufgrund der VLAN Konfiguration nur folgende PCs jeweils miteinander kommunizieren:

PC A-1 mit PC A-2
PC A-5 mit PC A-6

Nehmen wir an, dass im Nachbarraum ebenfalls vier PCs stehen. Nun sollen PC B-1 und PC B-2 mit PC A-1 und PC A-2 im ersten Raum kommunizieren können. Ebenfalls soll die Kommunikation zwischen PC B-5 und PC B-6 aus Raum 2 mit PC A-5 und PC A-6 im Raum 1 möglich sein.
Im Raum 2 haben wir wieder einen Switch:

| Switch-Port | VLAN ID     | Angeschlossenes Gerät |
|-------------|-------------|------------------------|
| 1           | 1 (grün)    | PC B-1                 |
| 2           |             | PC B-2                 |
| 3           |             | -                      |
| 4           |             | -                      |
| 5           | 2 (orange)  | PC B-5                 |
| 6           |             | PC B-6                 |
| 7           |             | -                      |
| 8           |             | -                      |

Damit die beiden VLANs hier verbunden werden können, benötigen wir bei portbasierten VLANs zwei Kabel, je eines für die entsprechenden VLANs:

von Switch A Port 4 zu Switch B Port 4 (für das VLAN 1)
von Switch A Port 8 zu Switch B Port 8 (für das VLAN 2)

![image](https://github.com/user-attachments/assets/1dd10017-2a72-46c8-8848-f3860c26aab2)

Portbasiertes VLAN mit zwei Switches.

## Tagged VLANs
Bei Tagged VLANs können mehrere VLANs über einen einzelnen Switch-Port genutzt werden. Die einzelnen Ethernet Frames bekommen dabei ein Tag hinzugefügt, in dem die VLAN-ID vermerkt ist, zu dessen VLAN das Frame gehört.
Wenn im gezeigten Beispiel beide (!) Switches tagged VLANs beherrschen, kann damit die gegenseitige Verbindung mit einem einzelnen Kabel erfolgen. Diese eine Verbindung mit den tagged VLANs wird Trunk genannt:

![image](https://github.com/user-attachments/assets/e19628a2-d5a5-4e43-9182-f83961d3922c)

In der Norm IEEE 802.1q ist definiert, wie die Tags in das Ethernet-Frame
eingefügt werden.
Zusatzinfo: Die Ports werden zwischen Access-Ports und Trunk-Ports unterschieden.
Das Access-Port dient dazu, ein Gerät mit dem Switch zu verbinden, über diese Port wird nur ein zugewiesenes VLAN geführt.
Ein Trunk-Port, ist in der Lage, mehrere VLANS zu transportieren, z.B. zwischen Switches oder zu einem Gerät, das mehrere VLANs bedient wie z.B. Server oder WLAN-APs.

## Aufbau Ethernet Frame
Der VLAN Tag kommt in einem Ethernet Frame nach den MAC Adressen. Es enthält u.a. die VLAN-ID, die das Frame dem VLAN zuordnen:

![image](https://github.com/user-attachments/assets/f0519123-ac1d-464f-9425-a25762f33fbb)

Bei tagged VLANs nach IEEE 802.1q werden die Pakete vom Endgerät (z. B. Tagging-fähigem Server oder Access-Point) versehen. Wenn das einspeisende Gerät selber kein tagging kennt, kann das der Switch für das Gerät übernehmen.
Zu diesem Zweck wird dem Port eine PVID (Port VLAN ID) zugewiesen. Jedes untagged Frame das an diesem Port eingeht, wird mit dem entsprechenden VLAN-Tag (PVID) versehen und wird damit zu einem tagged Frame.
Achtung: Ein Frame mit Tags wird i.d.R. von einem Gerät, dass Tags nicht kennt als ungültig betrachtet und verworfen.

## VLAN und Routing
VLANs arbeiten auf Layer 2 und sind damit von der IP-Adressierung grundsätzlich nicht betroffen, aber…

![image](https://github.com/user-attachments/assets/fd81f074-aa96-4aff-9560-72c32194f104)

VLANs führen zu einer kompletten Trennung auf Layer 2. Das heisst aber auch, dass zwischen den VLANs kein Datenverkehr möglich ist. Wenn doch zwischen den VLANs Datenverkehr nötig ist, muss auf Layer 3 geroutet werden. Damit das aber geht ist es zwingend nötig, dass jedes VLAN ein eigenes (Sub) IP-Netz bildet. Diese IP-Netze werden dann über Router verbunden. Damit die Router die getagten Frames unterscheiden können (z.B. auf einem Trunk), müssen diese Router tagging verstehen. Diese Geräte werden allgemein als Layer 3 Switches oder Routing Switches bezeichnet.

## Verständnisfragen
Beantworten Sie die nachfolgenden Fragen im Forms (Einzelaufgabe):
Den Link erhalten Sie von der Lehrperson.

Auf welchem ISO-OSI-Layer arbeitet ein normaler Switch? A: Auf Layer 2

Kann ich mehrere Subnetze über einen normalen, nicht VLAN-fähigen Switch
führen? A: Nein, nicht sinnvoll. Kein VLAN = keine Trennung.

Nennen Sie Gründe, ein physikalisches LAN in virtuelle Netze aufzuteilen
Darf ein VLAN Netzwerk als «Sicher» eingestuft werden? A: Nein. VLANs trennen logisch, bieten aber keinen echten Schutz. Sicherheit
Broadcast-Reduktion, Netztrennung, Flexibilität und Kosteneffizienz.

Was versteht man unter «Portbasiertem VLAN»? A: Jeder Port fest einem VLAN zugeordnet.

Was versteht man unter «Tagged VLAN»? A: VLAN-Info wird im Frame mitgesendet (802.1Q). Für Trunk-Links
