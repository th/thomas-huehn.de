---
title: Lebenslauf mit currvita
date: 2008-02-02
tags: [LaTeX]
aliases: [/artikel/currvita/]
description: Es existieren mehrere LaTeX-Pakete, um Lebensläufe zu erstellen. Ich habe mich für currvita entschieden.
---
Es existieren mehrere LaTeX-Pakete, um Lebensläufe zu erstellen. Ich habe mich für [currvita](http://www.ctan.org/tex-archive/macros/latex/contrib/currvita/) entschieden.

Ich verfasse einen knappen, fiktiven Lebenslauf für [Summer Glau](http://www.summerglau.co.uk/), eine amerikanische Schauspielerin, die ich in der Fernsehserie „Firefly“ und dem dazugehörigen Film „Serenity“ sehr schätze.

## Allgemeines

Wer solch ein LaTeX-Paket nutzt, sollte sich im Klaren darüber sein, daß er ohne tiefgehende LaTeX-Kenntnisse das Aussehen nicht radikal ändern kann. Schon kleinere Änderungen können schwierig sein. Ich empfehle daher dringend, das Endresultat anzuschauen. Wem es überhaupt nicht gefällt, der sollte sich nach einer anderen Lösung umsehen.

## Präambel

Als Standardklasse verwende ich üblicherweise „scrartcl“ aus den KOMA-Script-Paket: \documentclass{scrartcl}

Nun noch das übliche zu Textkodierung und Sprache: \usepackage[utf8]{inputenc} sowie \usepackage[german]{babel}

currvita selbst muß natürlich ebenfalls geladen werden: \usepackage{currvita}

Und ich möchte ein Portraitfoto in den Lebenslauf einfügen, also benötige ich noch Pakete zur Einbindung von Grafiken: \usepackage{graphicx} und \usepackage{picins}
Wozu das Paket picins notwendig ist, erläutere ich gleich noch.

## Foto einbinden

Das Einbinden eines Fotos ist an und für sich natürlich nicht schwer, jedoch soll es ja an sinnvoller Position eingebunden und vom folgenden Text umflossen werden.

Hier kommt nur das Paket „picins“ ins Spiel. Mittels „parpic“ kann man eben dies erreichen.

\parpic[r][r]{\includegraphics[height=6cm,keepaspectratio]{summerglau2.jpg}} reicht jedoch leider nicht. Zum einen ragt der Text ins Bild hinein, zum anderen befindet sich das Foto für viele Zwecke zu weit links. Es wird strikt in den Satzspiegel eingepaßt, obwohl es ruhig ein ganzes Stück in den rechten Rand hineinragen dürfte (so wie man auch ein Foto von Hand aufkleben würde).

Daher muß das Foto noch nach rechts verschoben werden:
\parpic(4.37cm,6cm)(2.5cm,6cm)[r][r]{\includegraphics[height=6cm,keepaspectratio]{summerglau2.jpg}}

Das erste Längenpaar gibt die Abmessungen des Fotos an, man kann es leider offenbar nicht weglassen oder leer lassen. Das zweite Längenpaar verschiebt das Foto um 2,5 cm nach rechts und 6 cm nach unten. Nach unten deshalb, weil es ansonsten um die Bildhöhe nach oben geschoben wird. Warum ist mir völlig unklar. Ich empfehle, mit den Parametern einfach ein wenig zu spielen, bis es gut aussieht.

## Lebenslauf-Umgebung

Die einzelnen Abschnitte stehen innerhalb einer Lebenslauf-Umgebung:

\begin{cv}{Lebenslauf} bis \end{cv}

## Abschnitte des Lebenslaufs

Der Lebenslauf besteht nun aus mehreren Abschnitten. Klassische Abschnitte wären „Zur Person“, „Schule und Ausbildung“ oder auch „Fremdsprachen“.

Eingeleitet wird solch ein Abschnitt durch \begin{cvlist}{Angestrebte Rolle}, worauf dann am Ende natürlich ein \end{cvlist} folgt.

Eine beliebige Zahl solcher Abschnitte steht hintereinander innerhalb der Lebenslauf-Umgebung.

## Einträge in den Abschnitten

Ein Eintrag erfolgt mittels \item{ledig, ohne Kinder}, wobei auch eine weitere Form mit optionalem Parameter existiert, der dann üblicherweise Zeiträume angibt und in einer eigenen Spalte gesetzt wird:
\item[2002–2003]{\textbf{Firefly:} Hauptrolle (River Tam)}

Hier ist das jetzt nur eine Jahreszahl, in „echten“ Lebensläufen im deutschsprachigen Raum ist es üblich, dort einen Zeitabschnitt der Form „MM/JJJJ–MM/JJJJ“ anzugeben. Davon geht currvita auch standardmäßig aus, um den richtigen Abstand zu ermitteln.

## Der fertige Lebenslauf

Die TeX-Datei zum Lebenslauf ist damit vollständig.

Nun ruft man pdflatex auf (pdflatex summerglau) und erhält eine PDF-Datei mit [diesem Ergebnis](https://bear-images.sfo2.cdn.digitaloceanspaces.com/th/summerglau.pdf).

Impressum Hauptseite