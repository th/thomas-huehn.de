---
title: Vom Gatter zum Computer
description: Der Aufbau einer kompletten Hardware- und Softwarehierarchie zu Lehrzwecken
date: 2020-11-30
tags:
  - Hardware
aliases:
  - /2020/11/vom-gatter-zum-computer/
---
Das Verständnis dafür, wie ein Computer im Kern funktioniert, ist kein Allgemeinwissen.

Zwar glaubt jeder, irgendwie zu wissen, was passiert: in Programmiersprachen werden Programme geschrieben. Da gibt es Funktionen und Anweisungen und Schleifen, und all diese Konstrukte sagen dem Computer, was er tun soll. Und dann gibt es Millionen bis zu Abermilliarden Transistoren, die man zusammengenommen „Prozessor“ nennt, und der führt das Programm dann aus.

Doch wie? Begriffe wie „Compiler“ oder „Betriebssystem“ mögen auch noch als Begriff bekannt sein, aber wie das genau funktioniert? Zumindest die Teilnehmer der üblichen Talkshows wissen es wohl nicht. Und trauen sich im Zweifel auch nicht daran, denn das ist ja ein unüberschaubares Fachgebiet, auf dem nur der Informatiker und der Ingenieur sich auskennt. Wobei auch unter diesen viele ins Schwitzen kämen, müßten sie es mal eben erläutern.

Hier setzt [„nand2tetris“](https://www.nand2tetris.org/) an, ein Online-Kurs von zwei israelischen Informatikprofessoren. Der Kurs läßt – wie auch ihr inhaltsgleiches Buch „The Elements of Computing Systems“ – den Teilnehmer bei einfachen Logikgattern wie UND sowie ODER beginnen, und steigt mit ihm dann über kombinatorische und sequentielle Schaltungen die Hardwarehierarchie hinauf, bis der Teilnehmer einen einfachen Computer entworfen hat.

Dieser ist natürlich nicht real, niemand muß löten können. Die Gatter und daraus zusammengefügten Schaltungen werden in einem downloadbaren Java-Programm simuliert. Dennoch findet sich hier alles in vereinfachter Form: der Teilnehmer verwendet eine simple Hardwarebeschreibungssprache und simuliert dann die Schaltung in einem ebenso einfachen Simulator. Wenige Knöpfe, Reduzierung aufs wesentliche. Alles fein.

Bis hierhin muß der Teilnehmer sozusagen keine Vorkenntnisse haben, ab hier muß er programmieren können. In einer beliebigen Programmiersprache. Auch der allereinfachsten, es kann auch BASIC sein. Es geht nur um einfache Textein- und -ausgaben auf der Konsole.

Im zweiten Teil des Kurses und des Buches setzt der Teilnehmer dann darauf auf und steigt die Softwarehierarchie hinauf. Zunächst steht ein Assembler auf dem Programm, denn in Maschinensprache zu programmieren ist lästig.

Anschließend entwirft er eine virtuelle Maschine, die Anwenderprogramme ausführen kann, und implementiert diese in Assemblersprache.

Dann entwirft er eine Hochsprache, die ein wenig wie Java aussieht, aber sehr abgespeckt und simpel ist. Und natürlich einen Compiler dafür. Themen wie Lexer und Parser werden natürlich im Kurs und im Buch erklärt.

Und wie überall im Kurs: die Themen werden so minimal angeschnitten, daß eine sinnvolle, praktische Verwertung möglich wird, nicht mehr. Das ist eben die Leistung des Buches! Über Syntaxanalyse allein kann man viele Semester studieren. Aber für diese ganz einfache Sprache reicht das bißchen aus (die natürlich so vorentworfen ist, daß sie mit allereinfachsten Analysemethoden handzuhaben ist – die Autoren lenken den Teilnehmer ja schon sehr deutlich auf den vorgegebenen Weg).

Zuguterletzt entwirft und implementiert der Teilnehmer noch ein einfaches Betriebssystem. Auch hier darf man keine hochtrabenden Vorstellungen haben, es sind ein paar einfache Routinen, die erstens praktisch sind, um eigene kleine Programmierprojekte auf „seinem Computer“ umzusetzen, und die zweitens einen Eindruck geben, welche Themenbereiche ein Betriebssystem abdecken kann.

Ich kann den Kurs nur jedem ans Herz legen, besonders auch Leuten in meiner Position: im Prinzip habe ich nichts neues gelernt, ich wußte das alles schon. Im Prinzip halt. Implementiert habe ich einen Compiler aber noch nie. Viel zu kompliziert…

Nein, ist es nicht! Und es macht richtig Spaß!

Den Onlinekurs finde ich als Format etwas langatmig, stundenlang Videos anzugucken ist nicht so meins, daher bevorzuge ich deutlich das Buch. Inhaltlich sind beide jedoch identisch, und der Kurs ist kostenlos im Internet zu belegen.