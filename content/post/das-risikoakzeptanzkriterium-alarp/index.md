---
title: Das Risikoakzeptanzkriterium ALARP
description: Ein gängiges Maß zur Risikoreduktion
date: 2020-09-10
tags:
  - Safety
aliases:
  - /2020/09/das-risikoakzeptanzkriterium-alarp/
---
ALARP steht für “as low as reasonably practicable” und ist ein verbreitetes Risikoakzeptanzkriterium. Infolge verschiedentlicher Standardisierung im Automatisierungs-, Prozeß- und Automobilbereich (IEC 61508 als Basisnorm, darauf aufbauend IEC 61511 oder angelehnt ISO 26262) ist ALARP heutzutage das verbreitetste – wenn nicht in der Praxis gar das einzige – Risikoakzeptanzkriterium.

Im Strahlenschutzbereich kennt man ALARP auch, dort aber unter dem Akronym ALARA: “as low as reasonable achievable”. Inhaltlich sind ALARP und ALARA jedoch identisch.

ALARP stammt aus England und ist unter einem weiteren Akronym – SFAIRP (“so far as is reasonably practicable”) – im dortigen Arbeitsschutzgesetz verankert. Entwickelt wurde das Prinzip aufgrund eines Gerichtsprozesses, in dem es um die Haftung nach einem Grubenunglück im Bergbau ging. Das Gericht entwickelte Grundsätze, um den Fall bewerten zu können, und das Parlament hat diese dann später aufgegriffen:

> Reasonably practicable is a narrower term than “physically possible” and implies that a computation must be made […] in which the quantum of risk is placed in one scale and the sacrifice involved in the measures necessary for averting the risk (whether in time, trouble or money) is placed in the other.\
 —Court of Appeals, Edwards v. National Coal Board, 1949

Normalerweise wird in jeder Erklärung von ALARP nun das Karottendiagramm gezeigt. Ich verstehe nicht warum, denn weder Farbe noch Form (die beide an eine Karotte erinnern) stellen irgendeine Information dar. Ich begnüge mich mit ein paar kurzen Absätzen, die ALARP ebenfalls vollständig beschreiben.

## Unacceptable region

Die inakzeptable Region ist schnell erklärt: wenn das technische System nach allen ergriffenen Maßnahmen noch immer ein Risiko aufweist, das von der Gesellschaft als inakzeptabel hoch betrachtet wird, dann darf das System so nicht gebaut werden.

Was bedeuten „inakzeptabel“ und „für die Gesellschaft“? Das ist absichtlich so schwammig formuliert. Intuitiv bedeutet es, wenn man einem vernünftigen Menschen das System erläutert und er entsetzt ist, dann ist es inakzeptabel. Praktisch heißt es, daß man mit seiner Benannten Stelle, die ein Zertifikat ausstellen soll, das Thema diskutiert.

Noch praktischer heißt es aber: Common practices und Stand der Technik beachten. Die meisten von uns bauen keine revolutionären Systeme. Wenn ich eine hydraulische Presse baue, dann weiß ich, daß bereits hydraulische Pressen auf dem Markt sind, es also möglich sein muß. Und wenn ich im großen und ganzen dieselben Maßnahmen in der Entwicklung ergreife, werde ich auch vergleichbar gut sein.

Dieser inakzeptable Bereich spielt in der Praxis keine Rolle. Niemand baut Systeme, die Gefahr laufen, dort hinein zu fallen. Solche System mögen in einem allerersten Brainstorming auf den Tisch kommen, werden dann aber schnell „entschärft“ oder fallengelassen.

*Ein System im inakzeptablen Bereich muß eine weitere Risikominderung erfahren, oder es wird eben nicht existieren.*

## Tolerable region

Der tolerierbare Bereich (auch ALARP-Bereich) erfordert eine ständige Abwägung im Einzelfall: man darf sich nicht darauf ausruhen, den tolerierbaren Bereich erreicht zu haben und weitere Risikominderungen weglassen, aber man muß auch keine Risikominderung um jeden Preis betreiben.

Der tolerierbare Bereich ist eben kein Zielbereich, und sobald ich drin bin, habe ich gewonnen. Er ist der Bereich, wo ich weitere Maßnahmen zur Risikominderung ergreifen soll, aber solche Maßnahmen auch im Einzelfall ablehen darf, weil ihr Aufwand oder ihre Kosten in keinem Verhältnis zur Risikominderung stehen.

*Das ist der Bereich, in dem man sich in einer normalen Entwicklung befindet.* Hier fordert die Benannte Stelle immer weitere Maßnahmen (aus Sicht des entwickelnden Unternehmens bis zum Stillstand des Projekts), läßt sich aber überzeugen, wenn man aufzeigen kann, daß die ergriffenen Maßnahmen wirksam sind und man alles getan hat, was vernünftig ist.

## Broadly acceptable region

In dieser Region ist das Risiko bereits so weit gemindert, daß jede weitere Diskussion als Zeitverschwendung betrachtet wird. Man könnte noch weitere Maßnahmen ergreifen, diese wären auch nicht übertrieben aufwendig und teuer.

Aber das verbliebene Restrisiko ist bereits so niedrig, daß man nicht weiter darüber nachdenken muß. Die gefährdete Person könnte ja auch von einem Blitz getroffen werden, während sie gleichzeitig von einem Auto überfahren wird.

In diese Region kommt man natürlich ebenfalls so gut wie nie. Sie stellt aber klar, daß irgendwo einmal ein Ende der Risikominderung vertretbar ist.

Ab welchem Wert für das Restrisiko gilt das? Wiederum gibt es keine konkrete Zahl. Wie immer entscheidet zunächst der Entwickler, dann die Benannte Stelle und zuletzt das Gericht.

## Eigenschaften von ALARP

ALARP ist ein subjektives Maß. Unterschiedliche Personen können vertretbar zu unterschiedlichen Bewertungen kommen.

Die Anforderungen an technische Systeme „wachsen mit“, wenn die gesellschaftliche Einstellung sich ändert, beispielsweise weil kürzlich ein aufsehenerregender Unfall in diesem Bereich durch die Presse ging.

Ebenso wachsen die Anforderungen mit, wenn der Stand der Technik sich ändert. Heute sind wir sicherlich an einem Punkt, an dem der Einsatz statischer Analysewerkzeuge für Programmcode üblich ist, also sollte man sie auch einsetzen. Vor dreißig Jahren sah das noch anders aus.

All dies bedeutet aber auch, daß ALARP einem wenig Anleitung und Halt gibt, man steht mit der Bewertung doch ziemlich alleine da.

Ein Vorteil ist sicherlich, daß kein Referenzsystem notwendig ist, ALARP kann auch für völlig neuartige Systeme angewendet werden.

Menschenleben werden durch ALARP jedoch indirekt pekuniär bewertet, denn man könnte mit mehr Kosten und Aufwand immer noch das Risiko mindern, der ALARP-Bereich sagt einem jedoch, daß auch irgendwann Schluß sein darf. Dieses Aufwiegen von Leben gegen Geld ist nicht allgemein akzeptiert.