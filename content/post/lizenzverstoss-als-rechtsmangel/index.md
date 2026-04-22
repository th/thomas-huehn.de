---
title: "Lizenzverstoß als Rechtsmangel"
date: 2026-04-09T20:36:30+02:00
tags: 
  - Recht
  - Open Source
description: "Die Kanzlei JUN Legal testet gerade eine neue Theorie vor Gericht."
image: ""
aliases: []
draft: false
---
# Was ist geschehen?

Die Kanzlei von Rechtsanwalt Jun hat einen chinesischen Autohersteller (bzw. dessen deutschen Importeur) [verklagt,](https://jun.legal/2025/08/19/pressemitteilung-klage-gegen-mg-importeur-wegen-verletzung-von-open-source-bedingungen-eingereicht/) nachdem die Kanzlei ein Elektroauto geleast hatte, dann aber [keine Open-Source-Lizenzinformationen](https://www.thomas-huehn.com/what-i-heard-at-openchain-friends-2026/#open-source) finden konnte.

Ignorieren wir die prozessualen Nebenschauplätze (tritt die Leasingfirma als Streitgenosse bei?), so schien mir das zunächst dennoch eine relativ sinnlose PR-Veranstaltung zu sein. Ja, man arbeitet im Open-Source-Umfeld, man schreibt ein Buch zum Thema (Galetzka/Jun/Roßmann, Praxishandbuch Open Source), aber ist ein Streit mit einem von vielen Chinesen wirklich von belang oder ist das aktivistische Blindleistung?

Mittlerweile bin ich schlauer. Der ganze Fall dient nämlich dazu, eine Rechtstheorie zu testen und vor ein Gericht zu bringen.

# Was ist neu daran?

Traditionell herrscht die Auffassung vor, daß nur Urheber, also Inhaber von Urheberrechten, Lizenzverletzungen geltend machen können. Wenn ich Software schreibe und jemand meine (Open-Source-)Softwarelizenz verletzt, kann ich klagen. Wenn ich eine Software von jemandem erhalte, und deren Lizenz verletzt wurde, kann ich selbst jedoch nicht klagen.

Das ist aus Durchsetzungssicht unpraktisch. Denn es gibt [sehr viel mehr Nutzer](https://www.thomas-huehn.com/four-sources-of-open-source-compliance-risk/) als Urheber, und die Wahrscheinlichkeit, daß ein Urheber seine Rechte wahrnimmt, ist doch ziemlich gering, wie die Vergangenheit zeigt. [Viele Linux-Kernel-Entwickler](https://docs.kernel.org/process/kernel-enforcement-statement.html) beispielsweise scheuen juristische Auseinandersetzungen und versuchen lieber zu überzeugen. [Einzelne Ausnahmen](https://www.netfilter.org/files/2022-01-24-Beschluss_und_Vergleich.pdf) gibt es natürlich.

Nicht jeder ist jedoch mit diesem Vorgehen einverstanden, insbesondere die Software Freedom Conservancy in Amerika versucht immer wieder, Urheber aufzutun, die zu einer Klage geneigt sind, und unterstützt diese dann. Zuletzt hat sie jedoch etwas anderes versucht: sie klagte ohne Urheber. Die zugrundeliegende Rechtstheorie ist, daß der Nutzer der Software ein „Third-party beneficiary“ sei, dem eigene Rechte aus typischen Open-Source-Lizenzen zukomme. [Den Fall](https://sfconservancy.org/copyleft-compliance/vizio.html) haben sie zwar teilweise gewonnen, aber mit dieser Argumentation drangen sie dennoch nicht durch.

In Deutschland hatte ein privater Open-Source-Aktivist wegen Open-Source-Lizenzverstößen gegen AVM (den FRITZ!Box-Hersteller) geklagt. In [der Klageschrift](https://sfconservancy.org/static/docs/avm-Complaint_Klageschrift_DE.pdf) wird mit dem Vertrag zugunsten Dritter das deutsche Pendant zum „Third-party beneficiary“-Konzept am Rande angeführt, sich aber nicht wesentlich darauf gestützt.

Jun versucht nun etwas völlig anderes, um reinen Nutzern ohne Urheberschaft einen Hebel zur Lizenzdurchsetzung zu geben: er stützt sich auf Gewährleistungsrecht/Mängelhaftung. Die Open-Source-Lizenzverstöße seien ein Rechtsmangel. Hier ist nun ein originärer Anspruch des Nutzers, nicht des Urhebers (dieser hätte Ansprüche aus Urheberrecht). Und da eine Nacherfüllung/Nachbesserung kaum möglich sein wird (nicht nur aus Aufwandsgründen, sondern auch weil sich mittlerweile herausgestellt hat, da0 zueinander inkompatible Open-Source-Lizenzen vermischt wurden), bleibt der Rücktritt mit Erstattung des Kaufpreises.

Dies ist wohl auch die einzige Argumentation in der Klage, es gibt kein hilfsweise Vorbringen zum Vertrag zugunsten Dritter, da explizit die Rechtstheorie vor Gericht getestet werden soll, daß erstens bereits ein noch so kleiner Verstoß gegen Open-Source-Lizenzbedingungen ein Rechtsmangel sei, und zweitens dieser auch zwingend zu einem Anspruch auf Kaufpreiserstattung führt. Selbst die praxisferne Möglichkeit, daß ein Urheber den Autokäufer (statt den Hersteller) in Anspruch nehmen könnte, löse den Rechtsmangel bereits aus. Insofern ist es schon Aktivismus, aber rechtsfortbildender Aktivismus.

# Warum ist es wichtig?

Bei höherpreisigen Produkten wur einem Auto sei die Kaufpreiserstattung ein „ganz harter Hebel“. Solch ein Vorgehen lohnt sich nicht für Kopfhörer oder auch die oben erwähnte FRITZ!Box, weil der Hersteller dort nach einer juristischen Auseinandersetzung immer einen Rücktritt mit Kaufpreiserstattung akzeptieren wird. Wie viele Kunden werden sich schon melden? Aber ein Auto für viele zehntausend Euro? Das kann schmerzhaft werden, wenn es zumindest ein paar Kunden zurückgeben, zumal der Restwert nach Ende des juristischen Streits vermutlich nicht mehr sonderlich hoch sein wird.

# Was geschieht als nächstes?

Voraussichtlich wird der Fall am 19. Oktober 2026 vor der 42. Zivilkammer des Landgerichts München 1 verhandelt. Diese Kammer hatte bereits den Fall GEMA v. OpenAI verhandelt und dabei deutlich gemacht, daß sie auf florierende Geschäftsmodelle nicht unbedingt Rücksicht nimmt, sondern Urheberrechte ernst nimmt.