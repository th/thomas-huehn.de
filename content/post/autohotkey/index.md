---
title: "AutoHotKey"
description: Beispielkonfiguration für AutoHotKey
date: 2018-08-12
lastmod: 2019-12-08
tags: ['Software']
vgwort: 'e7d9c592266b45338aced08633046d2c'
---
Ich verwende schon seit langem [AutoHotKey](https://www.autohotkey.com/), um wiederkehrende Aufgaben zu automatisieren oder Ärgernisse zu umschiffen.

Sowohl bei der Arbeit, als auch privat, wobei die Skripte sich nur in kleinen Teilen unterscheiden. Mein privates Skript sieht derzeit wie folgt aus und wird beim Windows-Start automatisch geladen.

Hauptsächlich habe ich Tastatur-Hotkeys definiert, beispielsweise um ein typographische Anführungszeichen im Deutschen und Englischen eingeben zu können, oder auch einen Halbgeviertstrich.

Aber auch ein wenig Windowmanagement ist dabei: ein Fenster zu zwingen, oberhalb von anderen Fenstern zu bleiben, ist oft sehr hilfreich.

Und dann sind noch reine Textersetzungen dabei. Zum Beispiel kann ich „DATUM“ eingeben und diese Zeichen werden direkt durch das aktuelle Datum ersetzt.

```
#NoEnv          ; Recommended for performance and compatibility
                ; with future AutoHotkey releases.
; #Warn         ; Enable warnings to assist with detecting common errors.
SendMode Input  ; Recommended for new scripts
                ; due to its superior speed and reliability.
SetWorkingDir %A_ScriptDir%  ; Ensures a consistent starting directory.

#SingleInstance force

;AltGr 3 ist öffnendes, AltGr 4 ist schließendes Anführungszeichen
<^>!1::Send ‚
<^>!2::Send ‘
<^>!3::Send „
<^>!4::Send “
<^>!5::Send “
<^>!6::Send ”
<^>!+5::Send ‘
<^>!+6::Send ’

;AltGr - ist Halbgeviertstrich
<^>!-::Send –

<^>!.::Send …

<^>!SPACE:: 

<^>!a::Send ä
<^>!o::Send ö
<^>!u::Send ü
<^>!s::Send ß
<^>!+a::Send A
<^>!+o::Send Ö
<^>!+u::Send Ü

;für Plain TeX
<^>!ä::Send \"a
<^>!ö::Send \"o
<^>!ü::Send \"u

;für Pollen
<^>!l::Send ◊

;CapsLock fungiert als weitere Ctrl-Taste
Capslock::Ctrl

<^>!t::Winset, Alwaysontop, TOGGLE, A

<^>!+Q::ExitApp

:co:ZEIT::
FormatTime, zeit, , HH:mm
zeit := zeit . " Uhr "
Send %zeit%
return

:co:DATUM::
FormatTime, datum, , yyyy-MM-dd
Send %datum% `
return

; Unicode-Zeichen
<^>!#::
InputBox,u,Unicode-Zeichen,Codepunkt (Hex),Bitte geben Sie den Codepunkt ein.,,,,,,,
if not ErrorLevel
{
u := "U+" . u
  Send {%u%}
}
return
```
