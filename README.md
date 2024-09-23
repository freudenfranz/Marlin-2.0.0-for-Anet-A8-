# Marlin 3D Printer Firmware for AnetA8
 Ready to Flash AnetA8 Firmware open in PlatformIo and Select Sanguino as Board and Flash

## Display

As Display is selected: ZONESTAR_LCD

 For changing to a 128x64 pixel Display with Rorary Encoder change in the Configuration.h:

 - line 1900  #define REPRAP_DISCOUNT_FULL_GRAPHIC_SMART_CONTROLLER
 - line 1813 //#define ZONESTAR_LCD

## Temporary Settings - PLEASE CHANEG
- Temporarily reduced X_BED_SIZE and Y_BED_SIZE to 200 since my probe (sensor) is to far on the right
- Added Babystepping and set BABYSTEP_MULTIPLICATOR_Z to 10

## Language

The Display Language is set to German to change this go to line 1607 and change

#define LCD_LANGUAGE de

with one of this
 *   en, an, bg, ca, cz, da, de, el, el_gr, es, eu, fi, fr, gl, hr, it, jp_kana,
 *   ko_KR, nl, pl, pt, pt_br, ru, sk, tr, uk, vi, zh_CN, zh_TW, test

## SD-Card Support

To safe storage space sd-card support was disabled:
- line 1647: //#define SDSUPPORT

## LEVELING AND Z-ENDSTOP-Probe
These settings are due to the usage of a inductive proximity sensor as z-endstop
probe (ROKO SN04-N).

Therefore the 'Probe Type' is set to
- line 869: #define FIX_MOUNTED_PROBE instead of
- line 862: #define PROBE_MANUALLY

The sensor offset to the nozzle is set to:
- line 937: #define NOZZLE_TO_PROBE_OFFSET { 21, 55, -1 }

The auto bed leveling stategy is set to
- line 1180: #define AUTO_BED_LEVELING_BILINEAR

"Z Safe Homing" is set to avoid homing with a Z probe outside the bed area:
-line 1344: #define Z_SAFE_HOMING

In order to disable software endstops for setting the z-offset
this option is enabled:
- line 1105: #define SOFT_ENDSTOPS_MENU_ITEM

[1188] #define RESTORE_LEVELING_AFTER_G28
Normalerweise wird das Bed Leveling nach G28 Auto Home ausgeschaltet. Man muss deshalb im Slicer M501 (Load all saved settings from EEPROM) und M420 S1 (Bed Leveling State: Enable) in den Start-GCode jeder Druckdatei eintragen um es vor jedem Druck wieder zu aktivieren.
(Ungetestet:) Bed Leveling ist nach jedem Einschalten des Druckers standardmäßig deaktiviert. Falls das nur am Auto Home beim Start liegt würde dieser Eintrag helfen.

Optional: [1372] #define GRID_MAX_POINTS_X 3
Anzahl der Messpunkte für die x-Achse. Ich würde 5 vorschlagen. In der Zeile darunter wird der gleiche Wert für die y-Achse gesetzt.

Optional: [1372] #define GRID_MAX_POINTS_X 3
Anzahl der Messpunkte für die x-Achse. Ich würde 5 vorschlagen. In der Zeile darunter wird der gleiche Wert für die y-Achse gesetzt.

Optional: [1441] #define LEVEL_BED_CORNERS
Schaltet einen zusätzlichen Menüpunkt frei, mit dem nacheinander die Ecken des Druckbettes angefahren werden können, um das Druckbett vor dem Bed Leveling einfacher von Hand einstellen zu können.

Since my printer constantly triggered a thermal runaway protection stop,
 I increased the THERMAL_PROTECTION_HYSTERESIS to 20 deg Celsius in [..]_adv.h:
- line 141: #define THERMAL_PROTECTION_HYSTERESIS 20

## Hilfreiche Link

- [Autolevel for the A8 Anet 3D Printer](https://3dprint.wiki/reprap/anet/a8/improvement/autobedleveling)

## Weitere Anmerkungen

Nach dem Flashen der Firmware wie üblich einen Reset durchführen und alte Werte im EEPROM löschen.

Im Slicer unter Start-GCode für jede Druckdatei eintragen:
M501 // Load all saved settings from EEPROM
M420 S1 // Bed Leveling State: Enable

Eine genaue Anleitung zum Bed Leveling per Kommandozeile oder Druckermenü gibt es hier (Unter Manual Probing, Click for Details). Dabei ist es nicht so wichtig wie dick das Papier ist oder wie hoch die Kraft - solange es an allen Punkte gleich ist.

Nach dem Bed Leveling nicht vergessen die Messdaten im EEPROM zu speichern (Menüpunkt oder M500)

Anschliessend muss man einmal die Höhe der Düse über dem Druckbett während der ersten Schicht einstellen (z-Offset, der Vorgang wird First Layer Calibration genannt). Dafür gibt es einen Menüpunkt mit dem man beim laufenden Druck die Höhe verändern kann (z-Babystepping). Das erfordert etwas Übung, es ist aber sehr wichtig das gut zu machen. Der gedruckte Strang darf nicht zu platt und nicht zu rund sein, sonst gibt es trotzdem Haftungsprobleme.

## Links

[![Build Status](https://travis-ci.org/MarlinFirmware/Marlin.svg?branch=2.0.x)](https://travis-ci.org/MarlinFirmware/Marlin)
![GitHub](https://img.shields.io/github/license/marlinfirmware/marlin.svg)
![GitHub contributors](https://img.shields.io/github/contributors/marlinfirmware/marlin.svg)
![GitHub Release Date](https://img.shields.io/github/release-date/marlinfirmware/marlin.svg)

<img align="right" width=175 src="buildroot/share/pixmaps/logo/marlin-250.png" />

Additional documentation can be found at the [Marlin Home Page](http://marlinfw.org/).
Please let us know if Marlin misbehaves in any way. Volunteers are standing by!

## Marlin 2.0

Marlin 2.0 takes this popular RepRap firmware to the next level by adding support for much faster 32-bit and ARM-based boards while improving support for 8-bit AVR boards. Read about Marlin's decision to use a "Hardware Abstraction Layer" below.

Download earlier versions of Marlin on the [Releases page](https://github.com/MarlinFirmware/Marlin/releases).

## Building Marlin 2.0

To build Marlin 2.0 you'll need [Arduino IDE 1.8.8 or newer](https://www.arduino.cc/en/main/software) or [PlatformIO](http://docs.platformio.org/en/latest/ide.html#platformio-ide). Detailed build and install instructions are posted at:

  - [Installing Marlin (Arduino)](http://marlinfw.org/docs/basics/install_arduino.html)
  - [Installing Marlin (VSCode)](http://marlinfw.org/docs/basics/install_platformio_vscode.html).

### Supported Platforms

  Platform|MCU|Example Boards
  --------|---|-------
  [Arduino AVR](https://www.arduino.cc/)|ATmega|RAMPS, Melzi, RAMBo
  [Teensy++ 2.0](http://www.microchip.com/wwwproducts/en/AT90USB1286)|AT90USB1286|Printrboard
  [Arduino Due](https://www.arduino.cc/en/Guide/ArduinoDue)|SAM3X8E|RAMPS-FD, RADDS, RAMPS4DUE
  [LPC1768](http://www.nxp.com/products/microcontrollers-and-processors/arm-based-processors-and-mcus/lpc-cortex-m-mcus/lpc1700-cortex-m3/512kb-flash-64kb-sram-ethernet-usb-lqfp100-package:LPC1768FBD100)|ARM® Cortex-M3|MKS SBASE, Re-ARM, Selena Compact
  [LPC1769](https://www.nxp.com/products/processors-and-microcontrollers/arm-microcontrollers/general-purpose-mcus/lpc1700-cortex-m3/512kb-flash-64kb-sram-ethernet-usb-lqfp100-package:LPC1769FBD100)|ARM® Cortex-M3|Smoothieboard, Azteeg X5 mini, TH3D EZBoard
  [STM32F103](https://www.st.com/en/microcontrollers-microprocessors/stm32f103.html)|ARM® Cortex-M3|Malyan M200, GTM32 Pro, MKS Robin, BTT SKR Mini
  [STM32F401](https://www.st.com/en/microcontrollers-microprocessors/stm32f401.html)|ARM® Cortex-M4|ARMED, Rumba32, SKR Pro, Lerdge, FYSETC S6
  [STM32F7x6](https://www.st.com/en/microcontrollers-microprocessors/stm32f7x6.html)|ARM® Cortex-M4|The Borg, RemRam V1
  [SAMD51P20A](https://www.adafruit.com/product/4064)|ARM® Cortex-M4|Adafruit Grand Central M4
  [Teensy 3.5](https://www.pjrc.com/store/teensy35.html)|ARM® Cortex-M4|
  [Teensy 3.6](https://www.pjrc.com/store/teensy36.html)|ARM® Cortex-M4|

## Submitting Changes

- Submit **Bug Fixes** as Pull Requests to the ([bugfix-2.0.x](https://github.com/MarlinFirmware/Marlin/tree/bugfix-2.0.x)) branch.
- Submit **New Features** to the ([dev-2.0.x](https://github.com/MarlinFirmware/Marlin/tree/dev-2.0.x)) branch.
- Follow the [Coding Standards](http://marlinfw.org/docs/development/coding_standards.html) to gain points with the maintainers.
- Please submit your questions and concerns to the [Issue Queue](https://github.com/MarlinFirmware/Marlin/issues).

## Marlin Support

For best results getting help with configuration and troubleshooting, please use the following resources:

- [Marlin Documentation](http://marlinfw.org) - Official Marlin documentation
- [Marlin Discord](https://discord.gg/n5NJ59y) - Discuss issues with Marlin users and developers
- Facebook Group ["Marlin Firmware"](https://www.facebook.com/groups/1049718498464482/)
- RepRap.org [Marlin Forum](http://forums.reprap.org/list.php?415)
- [Tom's 3D Forums](https://discuss.toms3d.org/)
- Facebook Group ["Marlin Firmware for 3D Printers"](https://www.facebook.com/groups/3Dtechtalk/)
- [Marlin Configuration](https://www.youtube.com/results?search_query=marlin+configuration) on YouTube

## Credits

The current Marlin dev team consists of:

 - Scott Lahteine [[@thinkyhead](https://github.com/thinkyhead)] - USA &nbsp; [Donate](http://www.thinkyhead.com/donate-to-marlin) / Flattr: [![Flattr Scott](http://api.flattr.com/button/flattr-badge-large.png)](https://flattr.com/submit/auto?user_id=thinkyhead&url=https://github.com/MarlinFirmware/Marlin&title=Marlin&language=&tags=github&category=software)
 - Roxanne Neufeld [[@Roxy-3D](https://github.com/Roxy-3D)] - USA
 - Chris Pepper [[@p3p](https://github.com/p3p)] - UK
 - Bob Kuhn [[@Bob-the-Kuhn](https://github.com/Bob-the-Kuhn)] - USA
 - João Brazio [[@jbrazio](https://github.com/jbrazio)] - Portugal
 - Erik van der Zalm [[@ErikZalm](https://github.com/ErikZalm)] - Netherlands &nbsp; [![Flattr Erik](http://api.flattr.com/button/flattr-badge-large.png)](https://flattr.com/submit/auto?user_id=ErikZalm&url=https://github.com/MarlinFirmware/Marlin&title=Marlin&language=&tags=github&category=software)

## License

Marlin is published under the [GPL license](/LICENSE) because we believe in open development. The GPL comes with both rights and obligations. Whether you use Marlin firmware as the driver for your open or closed-source product, you must keep Marlin open, and you must provide your compatible Marlin source code to end users upon request. The most straightforward way to comply with the Marlin license is to make a fork of Marlin on Github, perform your modifications, and direct users to your modified fork.

While we can't prevent the use of this code in products (3D printers, CNC, etc.) that are closed source or crippled by a patent, we would prefer that you choose another firmware or, better yet, make your own.
