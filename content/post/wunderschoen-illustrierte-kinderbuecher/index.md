---
title: "Wunderschön illustrierte Kinderbücher"
date: 2019-08-12
lastmod: 2019-08-22
tags: ["Buch"]
aliases: ["/2019/08/wunderschoen-illustrierte-kinderbucher/"]
description: "Mein kleines Projekt zu Kinderbuchillustrationen"
---
2015 schrieb [DanBC](https://news.ycombinator.com/user?id=DanBC) [in Hacker News:](https://news.ycombinator.com/item?id=9848031)

> 2\) I buy many books for my child. Amazon is pretty hopeless at recommending books to me, even though I’ve seeded it with knowledge of the books I’ve bought. So I turn to human curation: the Kate Greenaway medal focuses on excellent illustration in books for children. That list is an excellent source for books. Then one or two degrees of separation (eg, other books the illustrator has worked on, or other books the author of the winning book has written) get you hundreds of excellent books. Someone scraping this list and using affiliate links could probably make a bit of passive income.

Ich bin endlich dazu gekommen, [etwas in der Art auf die Beine zu stellen](https://www.thomas-huehn.de/schoene-kinderbuecher/).

Dabei habe ich mit der englischen Kate-Greenaway-Medal und der Caldecott-Medal, dem amerikanischen Gegenstück, begonnen. Leider sind viele oder gar die meisten dieser Bücher nie ins Deutsche übersetzt worden.

Ebenso habe ich Preisträgerlisten einiger deutschsprachiger Preise durchforstet. Die Evangelische Kirche hat ein oder zwei Preise auf dem Gebiet der Kinder- und Jugendbuchliteratur, das Land Nordrhein-Westfalen hat einen weiteren.

Alles habe ich von Hand gemacht, und es hat viel länger gedauert, als ich erwartet hatte: Preislisten durchsehen, die Autoren- und Illustratoreninformationen sammeln, den Inhalt erfassen, HTML und CSS schreiben. Alles ohne Deep Learning und Neuronale Netze…

Was ist dabei gelernt habe:

* Menschen blockieren Werbung. *Auch ich* blockiere Werbung. Und da wundere ich mich, wieso die Amazon-Affiliate-Links nicht funktionieren. Bis ist an uBlock Origin dachte. Und dann an Privacy Badger. Und an meinen Pi-Hole.

  Ich habe das dann so gelöst, daß ich die Titelbilder heruntergeladen und selbst gehostet habe. Nach Amazons Vertragsbestimmungen darf ich höchstens 100 Bilder downloaden. Ich habe 66. Also nichts mit „hunderte Bücher“, wie DanBC schrieb.

  (Zunächst wollte ich das komplett werbefrei machen, zumal ich ohnehin kaum Einnahmen erwartete, aber all die Verleger anschreiben und um Nutzungsrechte für Titelbilder bitten? Nein danke, dann lieber die harschen Restriktionen von Amazon Partnernet, aber dafür auch Pauschalrechte.)

* Webdesign ist eine Katastrophe. Ich habe das Projekt als Ausrede genommen, ein wenig CSS Grid oder Flexbox zu lernen, bin mit beiden eine ganze Weile gescheitert und habe dann beide kombiniert. Und am Ende mußte ich eine Sonderbehandlung für den Internet Explorer 11 einführen, denn obwohl eigentlich alles laut Dokumentation mit Vendor-Präfixen funktionieren sollte, war das Layout komplett zerschossen und alles lag übereinander. Ich hatte wenig Lust, noch einen weiteren Abend mit IE11 zu verbringen.

* Selbst wenn es keine Katastrophe wäre, bin ich kein Designer. Ich wollte die Webseite aber etwas weniger nach dem „Hacker-News-Minimalismus-Klischee“ aussehen lassen. Es ist erstaunlich, wieviel man mit einem einfachen Boxschatten und abgerundeten Ecken erreichen kann!

* Bezüglich “affiliate links could probably make a bit of passive income” bezweifle ich, das ich auch nur den „einen Kaffee pro Tag“-Bereich erreichen werde. Es gibt unzählige Blogs und Webseiten, die Kinderbücher vorstellen.

  Vielleicht werfe ich mal zwanzig Euro in Richtung Google- oder Facebook-Werbung, weniger, weil ich mit großen Ergebnissen rechne, und mehr, weil mich die Seite der Internet-Werbenden interessiert. Damit hatte ich bislang noch keinerlei Berührungspunkte.

* Buchbeschreibungen sind schwer. Besonders wenn man das Buch nicht physisch vor sich liegen hat. Meine Beschreibungen sind kurz und sprühen nicht unbedingt vor Esprit, aber sie geben eine grobe Richtung an.

* Meine Datenschutzerklärung ist streng formaljuristisch wahrscheinlich noch immer nicht gut genug, obwohl sie wenigstens so geschrieben ist, daß ein Laie sie versteht. Wenn man Affiliate-Links auf eine Webseite streut, dann verspürt man einen gewissen Druck, diese rechtlichen Dinge richtig zu machen. Und ich mag das &lt;details&gt;-Tag in HTML, es ermöglicht das Aufklappen des langen Texts ohne jegliches Javascript.

DanBC fand meine Seite gut und schlug vor, daß ich sie als “Show HN” an Hacker News submitte. Allerdings sind dort nur Dinge zugelassen, die man im eigentlichen Sinne ausprobieren kann, und eine normale Submission macht wohl auch wenig Sinn, da nicht-englischsprachige Submissions dort keinerlei Stand haben.