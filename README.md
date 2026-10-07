# ISS-Runner-Starter-fuer-InnoSetup-Files
Seit der neuen InnnoSetup Version 7 (=64Bit - x64 Version) habe ich mehrere Versionen auf der Festplatte - dieses Tool erlaubt eine Auswahl des Compilers...

1. Vorbereitung in der Inno Setup Datei (.iss)

Fügen Sie ganz oben in Ihren .iss-Dateien eine eindeutige Zeile hinzu, die die bevorzugte Version definiert:

; --- Compiler Konfiguration ---

#define PreferredVersion "6"

[Setup]
AppName=Mein Programm

AppVersion=1.0
...
.
.
.
.

Die ISS-Runner.au3 Datei mit (einem natürlich vorher installiertem) Autoit3 kompilieren...
Kompilierte ISS-Runner.exe z.B.: ins neue "C:\Program Files\Inno Setup 7" kopieren

1. Machen Sie im Windows Explorer einen Rechtsklick auf eine beliebige .iss-Datei.
2. Wählen Sie Öffnen mit -> Andere App auswählen.
3. Aktivieren Sie unbedingt das Häkchen bei „Immer diese App zum Öffnen von .iss-Dateien verwenden“.
4. Scrollen Sie ganz nach unten und klicken Sie auf „Andere App auf diesem PC suchen“.
5. Wählen Sie im Dateibrowser Ihre ISS-Runner.exe aus

Falls die Version im Script nicht ermittelt werden kann, so wird ein Fenster mit den entsprechenden Schaltflächen geöffnet,
und es kann eine manuelle Auswahl erfolgen (default bei Enter = Inno Setup 6...

<img width="600" height="199" alt="image" src="https://github.com/user-attachments/assets/6b1b33d6-34d3-4601-9531-2fa349016fc0" />



Code:

siehe angefügte ISS-Runner.au3
