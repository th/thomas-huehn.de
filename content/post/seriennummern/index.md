---
title: "Seriennummern"
description: Idee zur Kodierung und Darstellung von Seriennummern
date: 2015-09-01
tags: ['Idee']
---
## Motivation

Seriennummern sind herkömmlicherweise längere Zeichenketten, ursprünglich reine Ziffernketten, zuweilen aber auch alphanumerische Zeichenketten. Eine strikte Folge sukzessiv um 1 inkrementierter Nummern ist dabei meistens gar nicht erforderlich (und oft auch nicht in aller Strenge durchgehalten).

Sie kommen an verschiedenen Stellen vor, an denen einzelne Exemplare einer Fertigungsserie eindeutig gekennzeichnet werden müssen, da sie identifizierbar und unterscheidbar sein sollen.

Dies betrifft zunächst physische Produkte. Bei nicht-physischen Produkten wie Software handelt es sich bei der umgangssprachlich zuweilen auch als „Seriennummer“ bezeichneten Zeichenketten meistens um einen Lizenzkey, der anderen Zwcken dient (auf die diese Prinzipien aber weitgehend ebenso anwendbar wären).

Wo die Seriennummern lediglich automatisiert ausgelesen und verwaltet werden, ist das Zahlenformat natürlich günstig.

Für den menschlichen Benutzer sind solche Seriennummern jedoch ausgesprochen unhandlich zu verwenden. Sie sind schwer zu merken und auch ein Vertippen oder falsches Erinnern kann der Mensch in der Regel nicht direkt selbst erkennen (sondern erst eine nachgeschaltete rechnergestützte Plausibilisierung deckt Fehler auf, sofern redundante Information wie eine Prüfziffer enthalten sein sollte). Seriennummern sind auch schwer einem Kollegen mündlich zu übermitteln oder zu reproduzieren (schriftlich oder anderweitig).

Seriennummern könnten jedoch auch so gestaltet werden, daß sie diese Nachteile vermeiden oder zumindest stark verringern. Dazu kann auf natürliche Sprache zurückgegriffen werden.

## Grundidee

Anstelle einer Seriennummer „736273932“ wird eine Wortfolge der Art „rot Hemd Biene“ als Seriennummer verwendet. Die Wörter der Wortfolge entstammen dabei einem festen und eindeutig festgelegten Wörterbuch.

Der Anwender des Geräts kann sich die Wortfolge bedeutend leichter merken und diese leichter reproduzieren als er dies bei einer Ziffernfolge könnte. Zudem entdeckt er geringfügige Fehler leicht („Wetteer“) und korrigiert diese selbständig.

Dabei ist ein großes Wörterbuch vorteilhaft, weil die Anzahl der Wörter als Basis der Potenzierung die Anzahl der möglichen Wortfolgen einer beschränkten Länge bestimmt.

## Ausführungsvarianten

### Wortlängen

Dabei ist es natürlich sinnvoll, die Wörter im Wörterbuch so zu wählen, daß sie möglichst kurz sind. Das beschleunigt das manuelle Eintippen durch den Benutzer und spart Platz beim eventuellen Gehäuseaufdruck.

### Unterscheidbarkeit

Die Wörter können so gewählt werden, daß sie sich möglichst deutlich unterscheiden. So sollten „rot“ und „tot“ eher nicht beide im Wörterbuch aufgeführt sein.

Eine mögliche unerwünschte Ähnlichkeit kann sowohl in der Aussprache auftreten („malen“/„mahlen“), als auch in der Schreibweise („rot“/„tot“) oder der Grammatik („bin“/„ist“).

### Bedeutungstragende Wörter

Vorteilhaft sollte auch sein, anstelle von abstrakten Konzepten („Frieden“, „eßbar“) konkrete, bedeutungstragende Wörter zu verwenden, die Gegenstände der physischen Umwelt bezeichnen.

So könnten „Vogel“ oder „Baum“ geeignet sein.

#### Bilder

Wenn man solche Beschreibungen konkreter Gegenstände gewählt hat, dann können diese nicht nur textuell als Wort, sondern auch als (gegebenenfalls vereinfachte) Abbildung des jeweiligen Gegenstands dargestellt werden (sowohl in Konfigurationsprogrammen als auch beim im Gehäusedruck).

Die Eingabe durch den Benutzer muß dann natürlich sinnvollerweise als beschreibendes Wort erfolgen.

Ein weiterer Vorteil könnte darin liegen, daß der Benutzer die Seriennummer nicht stumpf abschreibt, sondern von bildlicher Form in textuelle Form übertragen muß, wodurch ein Mindestmaß an intellektueller Anwesenheit und Beteiligung notwendig ist. Durch gesteigerte Aufmerksamkeit könnte er bei wichtigen Dingen (Safety) möglicherweise leichter Fehler vermeiden.

### Sprachabhängigkeit und Lokalisierung

Eine sprachliche Darstellung einer Seriennumer ist natürlich zwangsläufig sprachgebunden.

Wenn der Benutzer aufgefordert ist, eine Seriennummer vom Gerät selbst zu reproduzieren, beispielsweise, indem er sie in ein Konfigurationsprogramm eintippt, um sicherzustellen, daß er das richtige Gerät konfiguriert, dann kann sich eine bildliche Darstellung wie oben beschrieben anbieten.

Denn wenn die Darstellung anhand solcher Bilder und Zeichnungen erfolgt, dann kann beispielsweise das Bild eines Baums angezeigt werden, das Konfigurationsprogramm kann jedoch „tree“, „Baum“ und „träd“ allesamt als gültige Benutzereingabe akzeptieren, oder je nach Spracheinstellung auch nur das passende Wort.

Selbstverständlich kann auch für sonstige Zwecke eine „Übersetzung“ der Wortfolge in andere Sprachen nicht nur die Benutzerfreundlichkeit verbessern, sondern auch deshalb vorteilhaft sein, weil die Muttersprache stets zuverlässiger beherrscht wird als Fremdsprachen.

### Klassenbildung

Auch kann eine Kategorisierung oder Klassenbildung der Geräte ausgedrückt werden, indem eigene Teilwörterbücher pro Klasse verwendet werden. So könnten Safety-Geräte beispielsweise stets mit einem Tier anfangen, Nicht-Safety-Geräte jedoch mit einer Pflanze.

### Positionale Einschränkung

Die Wörter des Wörterbuchs können mit Einschränkungen bezüglich ihres Auftretens in der Wortfolge annotiert sein. So könnte festgelegt werden, daß die Wortfolgen stets von der Form „Adjektiv Substantiv“ sind. Oder daß bestimmte Teile des Wörterbuchs nur am Anfang, andere nur am Ende stehen.

### Grammatikalität

Neben den hier aufgeführten Beispielen sind auch weitere denkbar. Entscheidend ist, möglichst nahe an einen grammatischen Satz heranzukommen.

#### Satzstruktur

Das Merken solcher Wortfolgen wird bedeutend erleichtert, wenn die Wortfolge einen Satz bildet und sich an die allgemeinen syntaktischen Regeln der Sprache hält. So könnten im Deutschen „Subjekt Verb“ oder „Subjekt Verb Objekt“ als Regeln beachtet werden.

Statt „rot Hemd Biene“ im Beispiel weiter oben wäre also „Biene trägt rotes Hemd“ oder ähnliches besser.

#### Kasuskongruenz

Auch weitere grammatikalische Regeln können beachtet werden. „rot Hemd“ ist aufgrund fehlender Kasuskongruenz bei weitem ungünstiger als „rotes Hemd“. Grammatische Sätze sind besser zu merken als ungrammatische. Denn letztere laufen stets Gefahr, vom Menschen unbewußt korrigiert zu werden.

Dabei können „rote“ und „rotes“ als zwei unterschiedliche Wörter betrachtet werden, die sich sinnvollerweise (der Unterscheidung ähnlicher Wörter wegen) jedoch in zueinander disjunkten Teilwörterbüchern befinden (nämlich jeweils mit ihren zugehörigen Substantiven).

Oder man betrachtet beide Wörter als morphologische Varianten des Wortstamms „rot“, der zur Ein- und Ausgabe passend dekliniert wird, aber logisch nur einen einzigen Eintrag im Wörterbuch belegt.

### Kodierung für Benutzerzwecke

Die Seriennummer muß nicht zwingend umgestellt werden, man kann auch eine konventionelle Seriennummer durch eine bijektive Abbildung auf eine Wortfolge abbilden. Der Anwender sieht in seinen Konfigurationstools und Protokollen dann stets die Wortfolge, intern maßgeblich bleibt jedoch die konventionelle Seriennummer.

Die Abbildung muß nicht zwingend bijektiv sein. Injektivität reicht aus und kann vorteilhaft sein: so beispielsweise im Beispiel der Sprachunabhängigkeit bildlicher Darstellungen.

## Kompatibilität mit bestehendem Umfeld

Bestehende DV-Systeme oder organisatorische Prozesse, die Ziffernfolgen als Seriennummern erwarten, können befriedigt werden, indem eine solche Abbildung von Wortfolgen auf Ziffernfolgen (oder umgekehrt) angewendet wird.

Am einfachsten wäre wohl, Zifferngruppen auf jeweils ein Wort abzubilden, aber auch andere Schemata sind denkbar.

Welche Repräsentation „die echte“ ist, muß zumindest solange nicht diskutiert werden, wie die genutzte Abbildung bijektiv ist, weil dann kein Unterschied feststellbar ist.

## Linguistischer Hintergrund

Auch wenn Chomskys Vorstellung einer Universalgrammatik und eines ‘language acquisition device’ ausgesprochen strittig sind, so dürfte doch offensichtlich sein, daß der Mensch sich darauf spezialisiert hat, Sprachäußerungen zu verarbeiten, sich zu merken und zu reproduzieren. Wesentliche Teile der „Ausbildung“ in den ersten Lebensjahren sind darauf ausgerichtet.

Auch daß der Umgang mit der eigenen Muttersprache leichter fällt als mit einer Fremdsprache dürfte klar sein.

Interessanterweise gibt es auch physiologische Evidenz für diese groben Regeln.

<aside>
Ich kann dafür leider keine zitierfähige Quelle angeben, das entstammt einer Äußerung meines Phonologieprofessors im Studium.
</aside>

So kann das Gehirn auf Sprachlaute (beliebiger Sprachen) schneller reagieren als auf andere Schallquellen und Geräusche.

<aside>
Eine Studie, an der ich als Versuchsperson teilgenommen habe: <cite>Silvia Lipski, Neurosci Lett. 2007 Mar 19, “A Magnetoencephalographic study on auditory processing of native and nonnative fricative contrasts in Polish and German listeners.”</cite>
</aside>

Auch die Muttersprache wird favorisiert: Sprachlaute aus der eigenen Muttersprache werden in anderen Hirnarealen verarbeitet als Sprachlaute anderer Sprachen.

Bezüglich der Unterscheidbarkeit von Wörtern muß besonders auf Homonyme geachtet werden. Homophone („Wende“/„Wände“) sind dabei ziemlich problematisch, besonders bei verbaler Übermittlung (beispielsweise beim Zurufen der Seriennummer an einen Kollegen). Homographe („modern“, „übersetzen“) sind dagegen eher unschädlich.

## Prior art

Das Grundprinzip, Zeichenketten in leichter merkbare Darstellungen zu überführen, ist natürlich schon alt. Einige Beispiele fallen mir dazu ein, sind jedoch jeweils anders gelagert.

### Paßwortgeneratoren

Paßwortgeneratoren wie [apg](http://www.adel.nursat.kz/apg/) bieten oft eine Option, aussprechbare Paßwörter zu erzeugen. Dabei werden jedoch keine echten Wörter generiert, sondern lediglich Silben, die den phonotaktischen Regeln westlicher Sprachen (primär natürlich Englisch) in großen und ganzen entsprechen.

### Diceware

[Diceware](http://world.std.com/~reinhold/diceware.html) ist eine Wortliste (ursprünglich Englisch, aber auch auf andere Sprachen „portiert“), durch die sichere Paßphrasen ausgewählt werden können. Der Benutzer würfelt mit fünf Würfeln und liest die zum gewürfelten Ergebnis passende Paßphrase ab, indem jedes Würfelergebnis (also eine Ziffernfolge mit fünf Ziffer von 1 bis 6) auf ein kurzes Wort abgebildet wird.

Das Diceware-Wörterbuch ist recht umfangreich (7776 Wörter), allerdings sind diese Wörter oftmals eher ungebräuchlich, Abkürzungen oder gar sinnlose Zeichenketten (die aber einigermaßen gut zu merken sind).

### S/Key

[S/Key](http://tools.ietf.org/html/rfc1760) oder „Lamport’s Scheme“ ist ein Verfahren, sich mittels Einmalpaßwörtern an einem Rechner zu authentisieren. Der Benutzer muß dabei eine 64-Bit-Zahl eingeben. Aus Gründen der Benutzerfreundlichkeit wird ihm jedoch stattdessen eine Paßphrase abverlangt, die mittels eines Wörterbuchs mit 2048 kurzen Wörtern aus dieser Zahl gebildet wurde.

Linguistische Beweggründe zur Auswahl der Wörter sind dabei zumindest nicht öffentlich dokumentiert, auch sind solche nicht direkt ersichtlich.

### PGPfone

[PGPfone](http://www.pgpi.org/products/pgpfone/) war ein kommerzielles Programm zum verschlüsselten Telefonieren. Dabei mußten die Gesprächspartner den jeweiligen Fingerabdruck ihrer öffentlichen Schlüssel austauschen.

Da dies eben über ein Telefonat funktionieren können sollte, wurde der Fingerabdruck auf eine Phrase abgebildet, die dann gesprochen werden konnte.

Dabei wurden recht ausführliche Betrachtungen phonetischer und phonologischer Natur angestellt, die im [Benutzerhandbuch](http://philzimmermann.com/docs/pgpfone10b7.pdf) kurz, in [zwei](http://www.mathcs.duq.edu/~juola/papers.d/icslp96.pdf) [weiteren](http://cds.cern.ch/record/405181) Papers jedoch ausführlicher beschrieben sind.
