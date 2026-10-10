# ISS-Runner (Starter) for Inno Setup-Files
Seit dem neuen Inno Setup 7 habe ich ja mehrere Versionen (7 = neue x64 = 64 Bit Version und ältere 5 u. 6 sind x86 = 32 Bit Versionen) auf der Festplatte...

Mein Autoit Tool erlaubt nun eine einfache Auswahl des Compilers beim Öffnen einer ISS-Datei. Ich erstelle gerne kleine Tools mit der Autoit Skriptsprache...

1. Optional: Vorbereitung in der Inno Setup Datei (.iss)

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

2. Die ISS-Runner.au3 Datei mit (einem natürlich vorher installiertem) Autoit3 kompilieren...
Eine von mir erstellte und mit UPX komprimierte, und von mir selbstsignierte EXE Datei, ist auch im Anhang...
Ich verwende Autoit Freeware-Skriptsprache gerne mal wieder um schnell kleine praktische Tools zu erstellen...

Kompilierte ISS-Runner.exe z.B.: ins neue "C:\Program Files\Inno Setup 7" Verzeichnis kopieren...

3. ISS Datei mit ISS-Runner.exe verknüpfen:

3.1. Machen Sie im Windows Explorer einen Rechtsklick auf eine beliebige .iss-Datei.
3.2. Wählen Sie Öffnen mit -> Andere App auswählen.
3.3. Aktivieren Sie unbedingt das Häkchen bei „Immer diese App zum Öffnen von .iss-Dateien verwenden“.
3.4. Scrollen Sie ganz nach unten und klicken Sie auf „Andere App auf diesem PC suchen“.
3.5. Wählen Sie im Dateibrowser Ihre ISS-Runner.exe aus

Hinweis:
Falls die Version vom Programm nicht ermittelt werden kann, so wird ein Fenster mit den entsprechenden Schaltflächen geöffnet,
und es kann eine manuelle Auswahl erfolgen (default bei Enter = Inno Setup 6...

<img width="600" height="199" alt="image" src="https://github.com/user-attachments/assets/6b1b33d6-34d3-4601-9531-2fa349016fc0" />



Code:

siehe angefügte ISS-Runner.au3
