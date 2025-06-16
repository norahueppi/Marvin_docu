# **This is the Marvin Documentation**  
**Nora Hüppi**  
**EN22a**  
**BüP**  
   
# Inhaltsverzeichnich
1. Einleitung
2. Analyse
3. Berechnungen
4. Realisierung
5. Bauelemente
6. Testing
7. Schwierigkeiten im Code
8. Arbeitsjournal
9. Anhang
10. Zeitplan und Anforderungen

# Einleitung
Im Rahmen meines berufsübergreifenden Projekts (BüP) habe ich mich erneut dazu entschieden, eine ikonische Szene aus *Per Anhalter durch die Galaxis* (*The Hitchhiker’s Guide to the Galaxy*) von Douglas Adams nachzubilden: die stöhnende Tür. Diese Szene ist ein Paradebeispiel für den einzigartigen Humor und die satirische Überzeichnung technischer Entwicklungen in Adams’ Werk. Mein Ziel ist es, diesen skurrilen Moment durch ein selbstentwickeltes interaktives System technisch und atmosphärisch erlebbar zu machen.

*Per Anhalter durch die Galaxis* ist weit mehr als ein Klassiker der Science-Fiction – es ist eine ironisch überzeichnete Auseinandersetzung mit übertriebener Technologisierung, Bürokratie und der Absurdität des Alltags. Die stöhnende Tür steht dabei symbolisch für überautomatisierte Systeme, die Funktionen erfüllen, die eigentlich niemand braucht – und gerade dadurch für Lacher sorgen. Genau diesen absurden Charme möchte ich mit meinem Projekt aufgreifen und technisch umsetzen.

Im Vergleich zu meinem früheren Projektansatz, bei dem ich auf ein ESP32-Audio-Kit zurückgriff, habe ich mich diesmal für eine vollständige Eigenentwicklung aller Hardwarekomponenten entschieden. Das System basiert auf einer 4,2-Volt-Li-Ion-Batterie, deren Spannung durch einen speziell ausgewählten Low-Dropout-Linearregler (LDO) auf die erforderlichen Betriebsspannungen angepasst wird. Ich habe sämtliche Schaltungen – von der Audioausgabe über den Verstärker bis hin zu SD-Karten-, Lade- und Stromversorgungsmodulen – selbst entworfen, gezeichnet und gefertigt.

Der Mikrocontroller ESP32 wird in diesem Projekt nicht mit der Arduino-Umgebung, sondern direkt mit dem ESP-IDF Framework programmiert. Die gesamte Softwarestruktur basiert auf FreeRTOS, was eine saubere, multitaskingfähige und zeitkritisch gesteuerte Architektur erlaubt. Die Audiodateien werden von einer SD-Karte gelesen, dekodiert und über einen von mir eingebundenen Audio-Codec sowie einen Verstärker abgespielt. Der TOF-Sensor erkennt Personenbewegungen in Türnähe und triggert die Soundausgabe mit einem charakteristischen Seufzen oder Stöhnen – die Geräusche wurden individuell aufgenommen, teils von mir, teils von Kollegen, um eine möglichst abwechslungsreiche und unterhaltsame Wirkung zu erzielen.

Dieses Projekt ist nicht nur eine Hommage an Douglas Adams' Werk, sondern auch eine persönliche Herausforderung und ein Lernfeld. Es vereint Hardwareentwicklung, Embedded-Programmierung, Audiosignalverarbeitung und kreative Gestaltung. Die Arbeit daran ermöglicht mir, mein technisches Wissen zu vertiefen und gleichzeitig meine Begeisterung für Science-Fiction und Satire in ein funktionales und unterhaltsames Produkt zu überführen. So wird aus einer literarischen Idee ein reales, interaktives Erlebnis mit einem Augenzwinkern – ganz im Sinne von *Per Anhalter durch die Galaxis*.  

# Analyse
## Überlegungen
Für die Realisierung des Projekts habe ich mir einige überlegungen gemacht.
- **Wie spare ich am besten Strom ohne den Sleep mode des ESP zu benutzen da es zu lange dauert in wieder zu wecken**
    - *Ich und mein Lehrmeister haben und darüber unterhalten und sind au den entschluss gekommen das es besser ist wenn ich das Projekt nicht mit ArduinoIDE sondern mit einer ESP IDF programmiere und FreeRTOS lernen werden.*
- **Benutze ich den gleichen Print oder Designe ich mir eine eigenen?**
    - *Da war ich entwas verunsichert ob ich dann alles unter einen Hut kriege wenn ich noch mein PCB selber mache, habe mich allerdings trotzdem dafür entschieden.*
- **Wie ermögliche ich einen Standby Modus ohne den Sleep Mode des ESP32?**
    - *Ich habe mir eine Darlington Schaltung designed die ich mit einem GPIO Pin ansteuern kann. Duch diese Schaltung kann ich dann im Code den GPIO auf HIGH oder LOW setzten je nach dem ob ich die Spannung brauche oder nicht.*
  
## Theorie
Das Ziel meines Projekts(was das selbe ist wie im letzten Semester) ist es, ein interaktives System zu entwickeln, bei dem eine Audiodatei abgespielt wird, sobald eine Person von einem TOF-Sensor erkannt wird, die durch eine Tür geht. Der zentrale Bestandteil des Systems ist ein selbst entwickeltes Audiomodul, das auf einem ESP32-Mikrocontroller basiert. Anders als im letzten Semester verwende ich kein fertiges Audio-Kit mehr, sondern habe die gesamte Schaltung, inklusive des Audio-Codecs, selbst entworfen und aufgebaut. Diese Schaltung ermöglicht die Verarbeitung der Audiodateien sowie deren Wiedergabe über einen angeschlossenen Lautsprecher.
  
Die Audiodatei selbst werde ich aus dem letzten Projekt verwenden die ich mit einem Aufnahmegerät erstellen. Um die ikonische "Moaning Door" aus The Hitchhiker’s Guide to the Galaxy möglichst authentisch nachzubilden, da habe ich Kolleginnen und Kollegen im Betrieb gebeten, ein entsprechendes Seufzen beizusteuern.
  
Die Stromversorgung erfolgt über eine 4,2-Volt-Batterie. Da sowohl der TOF-Sensor als auch der Mikrocontroller mit 3,3 Volt betrieben werden, kommt ein Low-Dropout-Linearregler (LDO) zum Einsatz, der die Spannung entsprechend reduziert. Zwar wäre ein Schaltregler hinsichtlich Energieeffizienz und Batterielaufzeit die bessere Wahl gewesen – insbesondere bei mobilen, batteriebetriebenen Systemen –, dennoch habe ich mich aus Gründen der Einfachheit und besseren Integrierbarkeit für einen LDO entschieden.
  
Um das System benutzerfreundlich zu gestalten und die eingeschränkte Energieeffizienz auszugleichen, habe ich zusätzlich eine Ladefunktion über eine USB-C-Schnittstelle implementiert. Dadurch lässt sich die Batterie direkt im Gerät wieder aufladen, ohne sie ausbauen zu müssen.
  
# Berechnungen
  
  
# Realisierung
## Funktionen
### SPI (Serial Peripheral Interface)
**SPI** ist ein schnelles, synchrones Kommunikationsprotokoll für die Verbindung zwischen einem Master und mehreren Slaves. Es wird oft für Sensoren, Displays, Speicher und Audio-Chips verwendet.
  
**Hauptmerkmale:**  
- **Schnelle, synchrone Vollduplex-Übertragung**  
- **Flexible Datenbreite**, keine festen Datenrahmen  
- **Einfaches Protokoll** ohne Adressierung  
  
**Signale:**  
- **MOSI** (Master Out, Slave In)  
- **MISO** (Master In, Slave Out)  
- **SCLK** (Takt vom Master)  
- **SS/CS** (Slave-Auswahl)  
  
**Vorteile:**  
- Sehr **hohe Datenrate**  
- **Vollduplex** möglich  
- **Einfach zu implementieren**  
  
**Nachteile:**  
- **Viele Leitungen** nötig bei mehreren Slaves  
- Keine **Fehlerprüfung** oder Adressierung  
- Nur **kurze Distanzen** zuverlässig  
  
**Typische Anwendungen:**
Sensoren, Speicherchips, Audio-Codecs, Displays
  
  
### I2S (Inter-IC Sound)
**I2S** ist ein serielles Protokoll speziell für digitale **Audiodaten**. Es verbindet z. B. Mikrocontroller mit DACs, ADCs oder Audio-Codecs.

**Hauptmerkmale:**  
- **Spezialisiert auf Audioübertragung**  
- Unterstützt **Stereo** (links/rechts getrennt)  
- Hohe **Audioauflösung** (16–32 Bit)  

**Signale:**  
- **BCLK** (Bit Clock)  
- **WS** (Word Select: links/rechts)  
- **SD** (Serielle Datenleitung)  
- Optional: **MCLK** (Master Clock)  

**Vorteile:**  
- **Präzise Synchronisation**
- ***Hohe Audioqualität***
- Ideal für **Stereo-Anwendungen**
  
**Nachteile:**
- **Nur für Audio** geeignet
- **Hoher Taktbedarf**, kurze Distanzen
- Weniger universell als SPI/I²C
  
**Typische Anwendungen:**
Audio-Codecs, DACs, digitale Lautsprecher, MEMS-Mikrofone
  
  
### I²C (Inter-Integrated Circuit)
**I²C** ist ein weit verbreitetes serielles Busprotokoll mit **nur zwei Leitungen**, ideal für einfache Kommunikation zwischen ICs.

**Hauptmerkmale:**  
- **Master-Slave-Architektur**  
- Unterstützt **Multi-Master**  
- Geräte werden über **Adressen** angesprochen  

**Signale:**  
- **SDA** (Serielle Datenleitung)  
- **SCL** (Taktleitung)  
- Beide Leitungen sind **Open-Drain** mit Pull-Ups  

**Vorteile:**  
- **Nur zwei Leitungen**, einfache Verdrahtung  
- **Viele Slaves** anschließbar  
- **ACK/NACK-Mechanismus** für Fehlerkontrolle  

**Nachteile:**
- **Langsamer** als SPI
- **Begrenzte Reichweite**
- **Externe Pull-Ups** notwendig

**Typische Anwendungen:**  
Sensoren, Displays, EEPROMs, Eingabegeräte  

## KiCad

## VS Code

# Bauelemente
  
## TMF8820 – Time-of-Flight (TOF) Distanzsensor
Der **TMF8820** von AMS ist ein präziser **Time-of-Flight-Sensor**, der Distanzen misst, indem er die Zeit berechnet, die Licht benötigt, um von einem Objekt reflektiert und vom Sensor wieder empfangen zu werden. Die Lichtquelle ist eine integrierte **VCSEL-Laserdiode**, die für hohe Genauigkeit sorgt.
  
- **Messbereich:** bis zu **4 Meter** (abhängig von Oberfläche & Lichtbedingungen)
- **Multi-Zonen-Erfassung:** 9 Zonen im **3×3-Muster**, um Richtungen und mehrere Objekte zu erkennen
- **Kommunikation:** über **I²C-Schnittstelle**, einfache Anbindung an Mikrocontroller
- Versorgungsspannung: 2,8 V – 3,3 V, ideal für ESP32
- **Vorteile:** hohe Präzision, geringe Latenz, energieeffizienter Betrieb
- **Typische Anwendungen:** Gestensteuerung, Personen-/Bewegungserkennung, Raumüberwachung, Robotik
  
  
## ESP32 – Selbst entwickelte Audio-Schaltung mit I2S
Statt eines vorgefertigten Audio-Kits wurde eine eigene Audioplatine mit dem **ESP32** als zentralem Mikrocontroller entwickelt. Der ESP32 ist ein **leistungsstarker Dual-Core-Mikrocontroller**, der sich durch seine **I2S-Schnittstelle** besonders gut für Audioprojekte eignet.
  
- CPU: Xtensa LX6 Dual-Core, **bis 240 MHz**
- **Kommunikation: Wi-Fi, Bluetooth (Classic + BLE), SPI, I2C, UART, PWM, I2S**
- **Audio:** Übertragung digitaler Audiodaten via I2S an externen Codec (z. B. ES8388)
- **Speicher:** typ. 4–16 MB Flash + SD-Kartenunterstützung
- **Software:** Arduino IDE, ESP-IDF, ESP Audio Framework
- **Besonderheiten:** flexible Schnittstellen, hohe Rechenleistung, ideal für interaktive Systeme
- **Typische Anwendungen:** Wiedergabe von Soundeffekten, Sprachsteuerung, Streaming, Smart Home-Audio
  
  
## TP4056 – Linearer 1-Zellen Li-Ion Ladecontroller
Der **TP4056** ist ein **kostengünstiger Ladechip**, der speziell für das Laden von **einzelnen Lithium-Ionen-Zellen (4,2 V)** entwickelt wurde. Er verwendet ein **CC/CV-Verfahren** und regelt den gesamten Ladeprozess automatisch.

- **Ladespannung:** fest auf **4,2 V**
- **Ladestrom:** programmierbar bis 1 A (über Widerstand)
- **Betriebsspannung: 4,0–8,0 V** (z. B. über USB oder 5 V-Netzteil)
- **Zusatzfunktionen:**
    - automatische Wiederaufladung
    - Temperaturschutz (via NTC)
    - Status-LED-Ausgänge (CHRG/STDY)
    - Trickle Charge bei Tiefentladung
- **Stromverbrauch im Standby:** nur **55 µA**, bei Inaktivität sogar **<2 µA**
- **Einsatzgebiet:** ideal für USB-Ladefunktionen in **batteriebetriebenen Geräten**
  
  
## DW01A – Schutz-IC für Li-Ion Akkus
Der **DW01A** schützt Einzelzellen vor kritischen Betriebszuständen wie **Überladung**, **Tiefentladung** oder **Überstrom** und wird typischerweise direkt im Akku-Pack oder Ladegerät eingesetzt.

- **Überladeschutz:** Aktiv bei **4,3 V ±50 mV**, Entsperrung bei 4,1 V
- **Tiefentladeschutz:** Aktiv bei **2,5 V**, Rückkehr bei 2,9 V
- **Überstromschutz:** Aktiv bei **~150 mV** Spannungsabfall
- **Verzögerungszeiten:** intern erzeugt, kein externer Kondensator nötig
- **Stromaufnahme:** extrem gering, typ. **3 µA**, ideal für Dauerbetrieb
- **Bauform:** kompakter **SOT-23-6**, einfache Integration
- **Einsatzbereich:** Lithium-Akkus in tragbaren Geräten (z.B. Ladeelektronik, Akkupacks) 
  
  
## ES8388 – Audio-Codec mit DAC, ADC & Verstärker

Der **ES8388** ist ein **hochwertiger Audio-Codec**, der sowohl **digitale zu analoge (DAC)** als auch a**naloge zu digitale Signale (ADC)** verarbeitet. Er enthält **Mikrofonverstärker, Kopfhörerausgänge, digitale Effekte** und lässt sich über **I2C oder SPI** konfigurieren.

- **Audioauflösung:** 24-Bit bei **8 – 96 kHz Samplingrate**
- **DAC & ADC:**
    - *DAC*: 96 dB Dynamikumfang, -83 dB THD+N
    - *ADC:* 95 dB Dynamikumfang, -85 dB THD+N
- **Audiofunktionen:**
    - Bass/Treble
    - Stereo-Enhancement
    - Lautstärke-Regelung
    - Rauschunterdrückung
- **Schnittstellen:** I2S, Left-Justified, PCM, DSP Mode
- **Versorgungsspannung: 1,8 V bis 3,3 V**
- **Leistungsaufnahme: 7 mW Playback, 16 mW bei Wiedergabe + Aufnahme**
- **Typische Anwendungen:** MP3-Player, Bluetooth-Audio, Mikrocontroller-Audio, Sprachsteuerung
  
  
# Testing
## Funktionale Anforderungen
|Nr.| Beschreibung | erwartete Reaktion | Ergebnis | Status |  
|----|-------------------------|-------------------------|-------------------------|------------|
|


## Nicht-Funktionale Anforderungen
|Nr.| Beschreibung | erwartete Reaktion | Ergebnis | Status |  
|----|-------------------------|-------------------------|-------------------------|------------|

# Schwierigkeiten im Code

# Arbeitsjournal
## KW8

## KW9

## KW10

## KW11

## KW12

## KW13

## KW14

## KW15

## KW16

## KW17

## KW18

## KW19

## KW20

## KW21

## KW22

## KW23

## KW24

## KW25

# Anhang

# Zeitplan und Anforderungen