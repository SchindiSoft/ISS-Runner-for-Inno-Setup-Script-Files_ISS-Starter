# ISS-Runner-Starter-fuer-InnoSetup-Files
Seit der neuen InnnoSetup Version 7 x64 hab ich mehrere Versionen auf der Festplatte - dieses Tool erlaubt eine Auswahl des Compilers...

1. Vorbereitung in der Inno Setup Datei (.iss)

Fügen Sie ganz oben in Ihren .iss-Dateien eine eindeutige Zeile hinzu, die die bevorzugte Version definiert:

; --- Compiler Konfiguration ---

#define PreferredVersion "6"

[Setup]
AppName=Mein Programm

AppVersion=1.0
...

Kompilierte ISS-Runner.exe z.B.: ins neue "C:\Program Files\Inno Setup 7" kopieren

1. Machen Sie im Windows Explorer einen Rechtsklick auf eine beliebige .iss-Datei.
2. Wählen Sie Öffnen mit -> Andere App auswählen.
3. Aktivieren Sie unbedingt das Häkchen bei „Immer diese App zum Öffnen von .iss-Dateien verwenden“.
4. Scrollen Sie ganz nach unten und klicken Sie auf „Andere App auf diesem PC suchen“.
5. Wählen Sie im Dateibrowser Ihre ISS-Runner.exe aus


Code:

#include <Array.au3>
#include <String.au3>

; Pfade zu den Compilern (Bitte an Ihre tatsächlichen Pfade anpassen!)
Global Const $INNO_V5 = "C:\Program Files (x86)\Inno Setup 5\Compil32.exe"
Global Const $INNO_V6 = "C:\Program Files (x86)\Inno Setup 6\Compil32.exe"
Global Const $INNO_V7 = "C:\Program Files\Inno Setup 7\ISIDE.exe"

; Prüfen, ob eine Datei übergeben wurde (per Doppelklick oder Drag&Drop)
If $CmdLine[0] = 0 Then
    MsgBox(16, "Fehler", "Bitte öffnen Sie eine .iss-Datei mit diesem Programm.")
    Exit
EndIf

Global $issDatei = $CmdLine[1]


; --- AUTOMATISCHE ERKENNUNG (Optional) ---
; Wir lesen die Datei ein und prüfen, ob ein bestimmtes Merkmal existiert
Global $fileContent = FileRead($issDatei)

; 1. Nach der spezifischen #define-Direktive suchen
Local $versionMatch = _StringBetween($fileContent, '#define PreferredVersion "', '"')


If IsArray($versionMatch) Then
    Local $preferred = $versionMatch[0]
    ConsoleWrite("-> Bevorzugte Version aus Datei ausgelesen: Inno Setup " & $preferred & @CRLF)

    ; Compiler basierend auf dem ausgelesenen Wert zuweisen
    Select
        Case $preferred = "5"
            $chosenCompiler = $INNO_V5
        Case $preferred = "6"
            $chosenCompiler = $INNO_V6
        Case $preferred = "7"
            $chosenCompiler = $INNO_V7
		Case Else
           ; $chosenCompiler = $inno6Path ; Standard-Fallback, falls eine unbekannte Zahl eingetragen wurde
	EndSelect

; 3. Compiler ausführen
If FileExists($chosenCompiler) Then
    ConsoleWrite("-> Starte Kompilierung mit: " & $chosenCompiler & @CRLF)
    Run('"' & $chosenCompiler & '" "' & $issDatei & '"', "", @SW_SHOW)
Else
    MsgBox(16, "Fehler", "Der ausgewählte Inno Setup Compiler wurde nicht gefunden unter:" & @CRLF & $chosenCompiler)
EndIf
Exit


Else
;obsolet i create a GUI with Buttons...
    ; 2. Fallback: Wenn kein #define gefunden wurde, Standardwert nutzen
  ;  $chosenCompiler = $inno6Path
  ;  ConsoleWrite("-> Keine Direktive gefunden. Verwende Standard-Compiler (Inno Setup 6)." & @CRLF)
EndIf



#include <FontConstants.au3>
#include <ButtonConstants.au3>
#include <GUIConstantsEx.au3>

; --- MANUELLES AUSWAHLMENÜ (Falls automatische Erkennung nicht greift) ---
; Erstellt ein kleines, sauberes Fenster zur Auswahl
Global $gui = GUICreate("Inno Setup Version wählen", 600, 200, -1, -1, 0x00080000) ; Ohne Minimieren/Maximieren

    Local $sFont = "Comic Sans MS"
    GUISetFont(14, $FW_NORMAL, $sFont)

GUICtrlCreateLabel("Mit welchem Compiler soll die Datei geöffnet werden?", 20, 15, 600, 50)
	GUISetFont(7, $FW_NORMAL, $sFont)

GUICtrlCreateLabel("default = Inno Setup 6 = Enter, Abbruch = ESC or Alt F4 or x", 20, 40, 600, 10)

    GUISetFont(14, $FW_NORMAL, $sFont)

Global $btnV5 = GUICtrlCreateButton("Inno Setup 5", 20, 60, 120, 30)
Global $btnV6 = GUICtrlCreateButton("Inno Setup 6", 160, 60, 120, 30);;, $BS_DEFPUSHBUTTON)


Global $btnV7 = GUICtrlCreateButton("Inno Setup 7", 300, 60, 120, 30)

GUICtrlSetState($btnV6, $GUI_FOCUS)

GUISetState(@SW_SHOW)


While 1
    Switch GUIGetMsg()
        Case -3 ; Schließen-Button (X)
            Exit
        Case $btnV5
            $PID=Run('"' & $INNO_V5 & '" "' & $issDatei & '"')
			if @error <> 0 Then
				    MsgBox(16, "Fehler", "Programm ""Inno Setup 5"" ist nicht installiert...")
			EndIf
            Exit
        Case $btnV6
            Run('"' & $INNO_V6 & '" "' & $issDatei & '"')
			if @error <> 0 Then
				    MsgBox(16, "Fehler", "Programm ""Inno Setup 6"" ist nicht installiert...")
			EndIf
			Exit

        Case $btnV7
            Run('"' & $INNO_V7 & '" "' & $issDatei & '"')
			if @error <> 0 Then
				    MsgBox(16, "Fehler", "Programm ""Inno Setup 7"" ist nicht installiert...")
			EndIf
			Exit

	EndSwitch
WEnd
