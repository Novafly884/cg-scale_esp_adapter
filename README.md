# CG-Scale ESP adapter v1.1
Breakout-Board zum Bau einer Schwerpunktwaage (CG-Scale) auf Basis der @nightflyer88 Firmware für zwei bis drei Wägezellen. Das Board dient dazu, sich die Einzelverdrahtung der ganzen Komponenten zu sparen und alle wesentlichen Anschlüsse steckbar zu haben. 

Link Firmware: https://github.com/nightflyer88/CG_scale

Link RC-Network: https://www.rc-network.de/threads/schwerpunkt-waage-mit-arduino.674777/page-79

# Dokumentation zur Platine
## Layout & Bauteile

![image](https://github.com/user-attachments/assets/77431425-05dd-41d7-a129-67d73d9bcfd7)

| ID | Wert |	Rastermaß |	Beschreibung | Verwendung |
| :--- | :--- | :--- | :--- | :--- |
| MCU | - | - | NodeMCU (ESP8266, ESP-12E) | - |
| R1 | 20 kOhm |	10 mm |	1%, Metallschicht-Widerstand | Optional |
| R1 | 10 kOhm |	10 mm |	1%, Metallschicht-Widerstand | Optional |
| C1 | 220 µF |	2,54 mm |	Kondensator, gepolt (Elko), 16 Volt | Optional |
| C2 | 100 nF |	2,54 mm |	Kondensator | Optional |
| DISP; LC1-LC3 | - |	2,54 mm |	4-pol. *JST XH2.54* | - |

Die Widerstände R1 & R2 bilden einen Spannungsteiler, um die Versorgungsspannung durch den Controller messen und anzeigen zu können. Wird diese Funktionalität nicht benötigt, können die Teile unbestückt bleiben und die Funktion in der Fimware deatkviert werden. 

C1 & C2 dienen zur Spannungsstabilisierung bzw. Filterung von Peaks auf der Versorgungsspannung. Da normalerweise die Platine aus einem Akku versorgt wird, benötigt es die Kondensatoren nicht. Bei einem Betrieb an einem Steckernetzteil ist die Bestückung allerdings zu empfehlen. 

Die Anschlüsse für das Display (DISP) und die Wägezellen (LCx) können mit allen Stecksystemen mit einem Rastermaß von 2,54mm ausgeführt werden. Persönlich verwende ich gerne die JST XH-Stecksysteme, da diese auch vom Bauraum her recht klein sind. Ein direktes Anlöten der Leitungen zu den HX711-Messwandlern ist selbstverständlich auch möglich. 

## Maße / Bohrabstände
- Platinengröße: 73 x 46 mm.
- Raster der Befestigungsbohrungen: 63 x 36 mm (Bohrungsdurchmesser = 2,8 mm).
  Der Isolationsbereich an den Befestigungen hat einen Durchmesser von ~5,9 mm.

![image](https://github.com/user-attachments/assets/f6eaf787-4cdb-4ef3-9480-ff2b8eb48f7b)

## Anschlussbelegung der Wägezellen-Messwandler (HX711)
Das nachfolgende Bild zeigt den Anschluss der HX711-Messwandler (ROTE Version) und einem 128X64 OLED-Displays mit "SH1106"-Chipsatz. Je nach Ausführung des Displays müssen die entsprechenden Anschlüsse "SDA", "SCL", "VCC" und "GND" gedreht werden (Beschriftungen auf der Displayplatine beachten!).

*Sollte trotz korrekter Verkabelung euer Display nichts anzeigen, bitte einmal den Controllertyp in der "U8g2lib.h" in eurem Code kontrollieren! ;)*

![image](https://github.com/user-attachments/assets/5317d233-8525-46ec-a215-0faa998a5e6c)


## Spannungsversorgung / Anschluss für Schalter
Die Controllerplatine (Node MCU) wird mit max. 9 Vdc versorgt. Hierzu eignen sich 2-zellige LiIon- oder LiPo-Packs bzw. eine 9V Blockbatterie. Theoretisch kann der auf der Platine befindliche Spannungsregler mit max. 15 Vdc gespeist werden - hierzu ist aber die Installation eines Kühlkörpers auf dem Chip notwendig!

"SW" dient zum Anschluss eines Power-Schalters, um die Waage ein- und ausschalten zu können. Wird kein Schalter verwendet, muss an dieser Stelle eine Drahtbrück bzw. in Jumper gesetzt werden. 

![image](https://github.com/user-attachments/assets/a2651875-af12-4ebc-90f6-0bc36a3a85fd)



