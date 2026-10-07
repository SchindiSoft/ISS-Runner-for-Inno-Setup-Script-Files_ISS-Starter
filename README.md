# ISS-Runner-Starter-fuer-InnoSetup-Files
Seit der neuen InnnoSetup Version 7 x64 hab ich mehrere Versionen auf der Festplatte - dieses Tool erlaubt eine Auswahl des Compilers...

1. Vorbereitung in der Inno Setup Datei (.iss)

Fügen Sie ganz oben in Ihren .iss-Dateien eine eindeutige Zeile hinzu, die die bevorzugte Version definiert:
pascal
; --- Compiler Konfiguration ---
#define PreferredVersion "6"

[Setup]
AppName=Mein Programm

AppVersion=1.0
...
