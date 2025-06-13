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
Vielen Dank für die ausführlichen Informationen – sie zeigen, wie sehr du dich weiterentwickelt hast. Für dein aktuelles Projekt wäre es sinnvoll, den ursprünglichen Einleitungstext zu übernehmen, aber an den entscheidenden Stellen zu überarbeiten und deine neuen, deutlich fortgeschritteneren technischen Ansätze hervorzuheben.

Hier ist ein überarbeiteter und professionell formulierter **Einleitungstext für dein neues BüP-Projekt**, der sowohl den kulturellen Hintergrund als auch die technische Tiefe deines Projekts berücksichtigt:

---

### Einleitung

Im Rahmen meines berufsübergreifenden Projekts (BüP) habe ich mich erneut dazu entschieden, eine ikonische Szene aus *Per Anhalter durch die Galaxis* (*The Hitchhiker’s Guide to the Galaxy*) von Douglas Adams nachzubilden: die stöhnende Tür. Diese Szene ist ein Paradebeispiel für den einzigartigen Humor und die satirische Überzeichnung technischer Entwicklungen in Adams’ Werk. Mein Ziel ist es, diesen skurrilen Moment durch ein selbstentwickeltes interaktives System technisch und atmosphärisch erlebbar zu machen.

*Per Anhalter durch die Galaxis* ist weit mehr als ein Klassiker der Science-Fiction – es ist eine ironisch überzeichnete Auseinandersetzung mit übertriebener Technologisierung, Bürokratie und der Absurdität des Alltags. Die stöhnende Tür steht dabei symbolisch für überautomatisierte Systeme, die Funktionen erfüllen, die eigentlich niemand braucht – und gerade dadurch für Lacher sorgen. Genau diesen absurden Charme möchte ich mit meinem Projekt aufgreifen und technisch umsetzen.

Im Vergleich zu meinem früheren Projektansatz, bei dem ich auf ein ESP32-Audio-Kit zurückgriff, habe ich mich diesmal für eine vollständige Eigenentwicklung aller Hardwarekomponenten entschieden. Das System basiert auf einer 4,2-Volt-Li-Ion-Batterie, deren Spannung durch einen speziell ausgewählten Low-Dropout-Linearregler (LDO) auf die erforderlichen Betriebsspannungen angepasst wird. Ich habe sämtliche Schaltungen – von der Audioausgabe über den Verstärker bis hin zu SD-Karten-, Lade- und Stromversorgungsmodulen – selbst entworfen, gezeichnet und gefertigt.

Der Mikrocontroller ESP32 wird in diesem Projekt nicht mit der Arduino-Umgebung, sondern direkt mit dem ESP-IDF Framework programmiert. Die gesamte Softwarestruktur basiert auf FreeRTOS, was eine saubere, multitaskingfähige und zeitkritisch gesteuerte Architektur erlaubt. Die Audiodateien werden von einer SD-Karte gelesen, dekodiert und über einen von mir eingebundenen Audio-Codec sowie einen Verstärker abgespielt. Der TOF-Sensor erkennt Personenbewegungen in Türnähe und triggert die Soundausgabe mit einem charakteristischen Seufzen oder Stöhnen – die Geräusche wurden individuell aufgenommen, teils von mir, teils von Kollegen, um eine möglichst abwechslungsreiche und unterhaltsame Wirkung zu erzielen.

Dieses Projekt ist nicht nur eine Hommage an Douglas Adams' Werk, sondern auch eine persönliche Herausforderung und ein Lernfeld. Es vereint Hardwareentwicklung, Embedded-Programmierung, Audiosignalverarbeitung und kreative Gestaltung. Die Arbeit daran ermöglicht mir, mein technisches Wissen zu vertiefen und gleichzeitig meine Begeisterung für Science-Fiction und Satire in ein funktionales und unterhaltsames Produkt zu überführen. So wird aus einer literarischen Idee ein reales, interaktives Erlebnis mit einem Augenzwinkern – ganz im Sinne von *Per Anhalter durch die Galaxis*.


# Analyse

# Berechnungen

# Realisierung

# Bauelemente

# Testing

# Schwierigkeiten im Code

# Arbeitsjournal

# Anhang

# Zeitplan und Anforderungen