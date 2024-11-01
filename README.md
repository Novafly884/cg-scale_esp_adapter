# CG-Scale ESP adapter v1.1
Breakout-Board zum Bau einer Schwerpunktwaage (CG-Scale) auf Basis der @nightflyer88 Firmware für zwei bis drei Wägezellen. Das Board dient dazu, sich die Einzelverdrahtung der ganzen Komponenten zu sparen und alle wesentlichen Anschlüsse steckbar zu haben. 

Link Firmware: https://github.com/nightflyer88/CG_scale

Link RC-Network: https://www.rc-network.de/threads/schwerpunkt-waage-mit-arduino.674777/page-79

# Dokumentation zur Platine
## Begriffe
+ PCB = Die Adapterplatine selbst in der angegebenen Version 
+ MCU = Node MCU (ESP8266 ESP-12E): Controller-Platine mit Wifi-Modul, welche auf die PCB gelötet wird
+ LC = Load cell = Wägezelle
+ Messwandler = HX711 Wägezellen-Messwandlerplatine zwischen Wägezelle und MCU 
+ I2C = I²C-Datenbus (Zweidraht) für die Ansteuerung des Displays

## Layout & Bauteilübersicht

![image](https://github.com/user-attachments/assets/77431425-05dd-41d7-a129-67d73d9bcfd7)

| ID | Wert |	Rastermaß |	Beschreibung | Verwendung |
| :--- | :--- | :--- | :--- | :--- |
| MCU | - | - | NodeMCU (ESP8266, ESP-12E) | - |
| R1 | 20 kOhm |	10 mm |	1%, Metallschicht-Widerstand | Optional |
| R2 | 10 kOhm |	10 mm |	1%, Metallschicht-Widerstand | Optional |
| C1 | 220 µF |	2,54 mm |	Kondensator, gepolt (Elko), 16 Volt | Optional |
| C2 | 100 nF |	2,54 mm |	Kondensator | Optional |
| DISP; LC1-LC3 | - |	2,54 mm |	4-pol. *JST XH2.54* | - |

Die Widerstände R1 & R2 bilden einen Spannungsteiler, um die Versorgungsspannung durch den Controller messen und anzeigen zu können. Wird diese Funktionalität nicht benötigt, können die Teile unbestückt bleiben und die Funktion in der Fimware deatkviert werden.  
*Wichtig: Sollte die PCB mit >9 Vdc versorgt werden, ist unbedingt das Datenblatt zum Node MCU (ESP8266 ESP-12E) zu beachten und es muss das Widerstandsverhältnis angepasst werden, da die MCU nur max. 3,3V am analogen Eingang messen kann!!*

C1 & C2 dienen zur Spannungsstabilisierung bzw. Filterung von Peaks auf der Versorgungsspannung. Im Normalfall wird die PCB aus einem Akkupack versorgt - hier benötigt es die Kondensatoren nicht. Bei einem Betrieb an einem Steckernetzteil ist die Bestückung allerdings zu empfehlen. 

Die Anschlüsse für das Display (DISP) und die Wägezellen (LCx) können mit allen 2,54mm-Stecksystemen (Rastermaß) ausgeführt werden. Beispiele dafür wären übliche Stiftleisten oder die JST XH-Stecksysteme, da diese auch vom Bauraum her recht klein sind. Ein direktes Anlöten der Leitungen zu den HX711-Messwandlern ist selbstverständlich möglich, wobei dann der Komfort der steckbaren Lösung "verloren" geht. 

## Maße / Bohrabstände
- Platinengröße: 73 x 46 x 1,6mm.
- Raster der Befestigungsbohrungen: 63 x 36 mm (Bohrungsdurchmesser = 2,8 mm).
  Der Isolationsbereich an den Befestigungen hat einen Durchmesser von ~5,9 mm.

![image](https://github.com/user-attachments/assets/f6eaf787-4cdb-4ef3-9480-ff2b8eb48f7b)

## Anschlussbelegung Messwandler & Display
Die Messwandler und das Display werden entsprechend der Beschriftungen auf der Platine angeschlossen. 
Die unteren Beschriftungen weisen Bezeichner auf, die auch auf euren Bauteilen zu finden sein sollten. Da diese bei den Messwandlerplatinen durchaus unterschiedlich sein können, gilt folgende Zuordnung: 
+ DAT = Cx (Daten)
+ CLK = Tx (Takt)

Weiterhin findet sich oberhalb der Anschlussplätze die Angabe der Pin-Nummern an der MCU (D3, D4, Dx...) für die erleichterte Konfiguration der entsprechenden Eingangs- und Ausgangs-Pins in der Software.

*Quick-Tipp: Sollte trotz korrekter Verkabelung euer Display nichts anzeigen, bitte einmal den Controllertyp in der "U8g2lib.h" in eurem Code kontrollieren! ;)*

![image](https://github.com/user-attachments/assets/83db5273-0933-493e-a880-8c954c3fe511)


## Spannungsversorgung / Anschluss für Schalter
Die MCU wird mit max. 9 Vdc versorgt - Hierzu eignen sich 2-zellige LiIon- oder LiPo-Packs bzw. eine 9V Blockbatterie. 

"SW" dient zum Anschluss eines (optionalen) Schalters, um die Waage ein- und ausschalten zu können. Wird kein Schalter verwendet, ist an dieser Stelle eine Drahtbrück bzw. in Jumper zu setzen. 

![image](https://github.com/user-attachments/assets/a2651875-af12-4ebc-90f6-0bc36a3a85fd)



