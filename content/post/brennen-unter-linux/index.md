---
title: Brennen unter Linux
date: 2008-02-02
tags: [Linux, Softwarelizenzen, Open Source]
description: CDs und DVDs unter Linux brennen
---
## Einleitung

Es gibt immer etwas zu brennen: Seien es die neuesten Live-CDs exotischer Betriebssysteme, die man unbedingt einmal ausprobieren möchte, seien es die Aufnahmen der Lieblings-Fernsehserie oder was auch immer. Das Brennen von CDs und DVDs ist eine Standardtätigkeit.

## Frontend oder Backend?

Unter Linux gibt es eine Reihe von kommandozeilengesteuerten Programmen, die CDs und DVDs (sowie mittlerweile auch Blu-ray- oder HD-DVD-Scheiben) beschreiben können. Die meisten Anwender werden aber sicherlich ein grafisches Programm zur komfortablen Auswahl der Brenntätigkeit bevorzugen. Diese Programme gibt es zuhauf, sie heißen beispielsweise k3b oder gnomebaker. Sie können allerdings nicht selbst brennen, sondern steuern die zugrundeliegenden Programme. Um diese zugrundeliegenden Programme soll es hier gehen, also diejenigen, die die verfügbaren Möglichkeiten bestimmen. Ein grafisches Frontend kann man leicht wechseln, ohne daß die Brennqualität leidet.

Diese Arbeitsteilung in „mächtiges Kommandozeilenprogramm hier, bequemes grafisches Tool dort“ ist unter Linux der Regelfall, zumindest soweit es die freie Software angeht. Im folgenden wird jedoch auch ein Programm „aus einem Guß“ besprochen werden, das die Brennfunktionalität und die grafische Bedienung untrennbar miteinander verknüpft hat.

Ich habe all diese Programme in der Vergangenheit bereits verwendet, mir nun aber anläßlich einer Neuinstallation Gedanken dazu gemacht, welche Programme geeignet sein mögen. Natürlich mit klarem Fokus auf „für mich geeignet“.

## Die Kandidaten

### cdrtools (cdrecord)

Die cdrtools, zu denen das Programm cdrecord gehört, sind sozusagen das Urgestein der Szene. Jörg Schilling hat sich über viele Jahre hinweg mit dem Thema Brennen unter unixoiden Systemen (mit Präferenz auf Sun Solaris) befaßt, die cdrtools waren lange Zeit die einzig ernstzunehmende Programmsuite zum Brennen von CDs.

Sie sind leider etwas komplizierter zu kompilieren, wobei „kompliziert“ sich hier lediglich darauf bezieht, daß ein Schilling-eigenes Build-System verwendet wird, das man zuvor noch beschaffen muß. Die eigentliche Kompilation sollte keine Schwierigkeiten bereiten.

Die cdrtools sind mit Augenmerk auf Portabilität geschrieben. Man kann also erwarten, sie auf so ziemlich allem übersetzt zu bekommen und benutzen zu können, was nach Unix aussieht.

Die cdrtools sind im wesentlichen als Alpha-Version [von der Webseite des Autors](http://cdrecord.berlios.de/old/private/cdrecord.html) zu bekommen. Eine als stabil deklarierte Veröffentlichung hat es seit Urzeiten nicht gegeben, der Autor fordert Benutzer dazu auf, die sogenannten „Alpha-Versionen“ zu verwenden.

Einige verbreitete Linux-Distributionen liefern die cdrtools nicht mehr aus. Siehe dazu den Abschnitt über die [Streitigkeiten](#streit-um-cdrtools-cdrkit).

### cdrkit (wodim)

cdrkit ist ein vom [Debian-Projekt](http://www.debian.org/) gestarteter Fork (eine Abspaltung) einer älteren Version der cdrtools. Dieser Fork wird jedoch nicht nur von Debian, sondern auch von anderen großen Linux-Distributionen anstelle der cdrtools verbreitet. Die einzelnen Programme wurden dabei umbenannt, so wurde zum Beispiel aus „cdrecord“ „wodim“.

Die Weiterentwicklung und Fehlerbehebung erfolgt dabei selbstredend nicht durch Jörg Schilling, sondern durch verschiedene andere Entwickler.

Es gibt glaubhafte Berichte, wonach mit cdrkit Probleme aufgetaucht sind, die durch Ersetzen von cdrkit durch die cdrtools sofort gelöst waren. In den weitaus meisten Fällen funktioniert cdrkit aber zur Zufriedenheit der Anwender (es ist ja auch die Standard-Brennsuite einer Reihe großer Distributionen), auch wenn Jörg Schilling Aussagen in öffentlichen Foren wie „Bei mir funktioniert wodim“ damit kontert, daß derjenige, der das gerade geschrieben hat, offensichtlich ein Lügner sei, schließlich sei wodim „kaputt“. Laut Jörg Schilling kann wodim/cdrkit also niemals auf irgendeinem Rechner funktioniert haben. Die Realität sieht allerdings doch deutlich anders aus.

Die Entwickler des Forks [begründen ihren Schritt auch selbst](http://debburn.alioth.debian.org/FORK), Jörg Schilling [hat darauf geantwort](http://cdrecord.berlios.de/old/private/linux-dist.html).

#### Der Streit um cdrtools/cdrkit

Die Abspaltung des cdrkit von den cdrtools erfolgte nach Jahren intensiven und teilweise sehr bösartig geführten Streits zwischen Jörg Schilling und den Debian-Entwicklern, die die Debian-Pakete zu den cdrtools betreut haben, sowie mit Teilen des restlichen Debian-Projekts. Jörg nutzt auch heute noch jede Gelegenheit, Debian schlechtzumachen, ja, er beleidigt und beschimpft sogar einen der Debian-Entwickler in öffentlichen Foren in dessen Abwesenheit.

Debian wurde es irgendwann zu dumm und startete diesen Fork. Dabei haben sie das Schilling-eigene Buildsystem ersetzt, zuvorderst, weil weite Teile der Debian-Entwickler Lizenzprobleme sehen. Diese Lizenzprobleme werden von Jörg Schilling bestritten. Als außenstehender Nicht-Lizenz-Spezialist ist es sehr schwierig zu einem qualifizierten Schluß zu kommen, jedoch sollte nicht unerwähnt bleiben, daß Jörg Schillings Position ebenfalls weite Unterstützung findet.

wodim erlaubt im Gegensatz zu cdrecord, den Brenner mittels der /dev/hdc-Schreibweise anzusprechen, was Jörg Schilling strikt ablehnt und wohl niemals einbauen wird. cdrecord verlangt die Angabe dreier Zahlen in einer 0,1,0-Schreibweise. Auch hier sind die tatsächlichen Hintergründe schwer zu durchschauen, wenn man sich mit Kernel-Interna nicht auskennt, auch hier finden beide Lager Unterstützung. Im allgemeinen bevorzugen Anwender natürlich erstere Schreibweise, das sagt aber nun einmal wenig über technische Meriten beider Varianten. Außerdem muß wodim im Gegensatz zu cdrecord nicht als Superuser root ausgeführt werden.

Jörg Schilling bezichtigt cdrkit verschiedener Dinge: Zum einen enthalte cdrkit nicht nur eine ganze Reihe von Fehlern, diese Fehler seien darüberhinaus teilweise niemals in den Original-cdrtools enthalten und teilweise alte Fehler der cdrtools, die im Original längst behoben worden seien.

Zum anderen beschuldigt er cdrkit, in den zugehörigen man pages würde behauptet, das Original werde nicht mehr weiterentwickelt. Wer diese man pages einmal durchliest, findet jedoch nichts derartiges. Jörg Schilling weigert sich beständig zu erläutern, wo er seine Behauptung herauslesen will. Vermutlich meint er diese Stelle:

> This application is a spinoff from the original program cdrecord delivered in the cdrtools package [1] created by Joerg Schilling, who deserves the most credits for its success. However, he is not involved into the development of this spinoff and therefore he shall not be made responsible for any problem caused by it. Do not refer to this applica‐ tion as cdrecord, do not try to get support for wodim by contacting the original authors. 

Selbstverständlich sagt sie nichts derartiges, sondern nur, daß Jörg Schilling nicht an der Fortentwicklung des Spin-Offs beteiligt ist, was zweifelsohne stimmt.

### dvd+rw-tools (growisofs)

Ich habe growisofs schon häufig genutzt, da mein k3b (ein bekanntes grafisches Frontend) es in seinen Defaulteinstellungen zum Brennen von DVDs verwendet hat. Ich muß allerdings zugeben, daß ich nicht viel von diesem Programm weiß und es daher hier möglicherweise doch unverdient unter den Tisch fällt.

growisofs benötigt allerdings auch die cdrtools oder cdrkit, beziehungsweise das Programm mkisofs aus diesen.

Es ist, wie der Name schon andeutet, allerdings nur ein DVD-Brennprogramm und kann keine CDs brennen.

### Nero Linux

Nero ist seit vielen Jahren von Windows her bekannt, wo es das bekannteste Brennprogramm ist, das oft auch Brennern direkt beigelegt wird. Der Hersteller hat seit einiger Zeit auch eine Linux-Version im Programm.

Dies ist das erwähnte Programm „aus einem Guß“. Es kann offenbar ausschließlich über die grafische Oberfläche bedient werden, eine Steuerungmöglichkeit per Kommandozeile ist mir nicht bekannt.

## Meine Meinung zu den Kandidaten
### cdrecord
#### Rechtliches

Jörg Schilling streitet gerne und viel um die CDDL, deren Verhältnis zur GPL (die Verfasserin der CDDL habe natürlich keine Ahnung von „ihrer“ Lizenz, die Free Software Foundation habe keine Ahnung von der GPL, Debian verstehe die Debian-Free-Software-Guidelines nicht, etc. ad nauseam), so daß die Frage erlaubt ist, ob man sich aufgrund wilder Lizenzinterpretationen nicht unnötig rechtlichen Risiken aussetzt. Selbst wenn man einen Prozeß gewänne, hätte man zunächst einmal große Mühen und Kosten gehabt.

Viel interessanter: Es gab im Jahre 2004 schon einmal eine cdrtools-Version, die niemand verbreiten durfte, auch wenn sie vorgeblich unter GPL stand. Die Details sind [hier](http://lwn.net/Articles/97655/) und [hier](http://weblogs.mozillazine.org/gerv/archives/006193.html) zu finden.

Der Höhepunkt ist aber, daß [er der Meinung zu sein scheint](http://groups.google.com/group/de.comp.os.unix.linux.misc/msg/36c553bfda789f3e), daß er fremden Code nehmen und in seine Programme einbinden dürfe, ohne den Autor um Erlaubnis zu fragen. Er dürfe dann auch selbst die Lizenz wählen. Und zwar gelte dies im Rahmen einer sogenannten „Kleinsturheberschaft“ und aufgrund eines ominösen „EU-Urheberrechtsgesetzes“. Ein solches Gesetz existiert zwar nicht und das deutsche [UrhG](http://bundesrecht.juris.de/urhg/index.html) sieht nichts derartiges vor, aber das hält ihn nicht davon ab, solche Behauptungen aufzustellen. Und man halte sich fest: eine solche „Kleinsturheberschaft“ sei gegeben, solange der Umfang des fremden Codes nicht mehr als fünf bis zehn Prozent des gesamten Codes ausmache. Das ist doch recht ordentlich. Man nehme 10 Prozent von SAP R/3, stricke neunzig Prozent Code drumrum und verkaufe das dann. Was SAP dazu wohl sagen würde…

#### Menschliches

Wie bereits erwähnt neigt Jörg Schilling zu Beleidigungen der schlimmsten Art. Das hat keinen Einfluß auf die Software an sich, aber natürlich auf die Bereitschaft und die Fähigkeit anderer, mit ihm zusammenzuarbeiten. Insbesondere die Linux-Kernelentwickler wären da eine interessante Gruppe, wenn man als Linux-Anwender Wert auf Brennfunktionalität unter Linux legt. Und es ist natürlich ein völlig legitimer Grund, auch seine Software abzulehnen.

#### Praktisches

Es ist bei heutigen Distributionen häufig aufwendiger, die cdrtools zu beschaffen, da man erst das Schilling-Buildsystem holen und installieren und anschließend noch die cdrtools aus dem Quellcode kompilieren muß.

Zudem führt Jörg Schilling auch seit Jahren einen Privatkrieg mit einer ganzen Reihe von Linux-Kernel-Entwicklern, insbesondere Linus Torvalds, und ist auch sonst stets ganz vorne dabei, wenn es darum geht, Linux schlechtzumachen. Ob man davon ausgehen kann, daß die cdrtools auch in Zukunft auf Änderungen im Linux-Kernel angepaßt werden? Schon bei der Anpassung an Kernel 2.6 war Jörg Schilling alles andere als begeistert. Ebenso haßt er offensichtlich das Debian-Projekt und verachtet SUSE. Möchte man sich als Anwender dieser oder davon abgeleiteter Distributionen darauf verlassen, daß er nicht einmal eine schärfere Form von linuxcheck() einbaut?

### cdrkit
#### Praktisches

cdrkit hat auf meinem Rechner stets funktioniert. Dennoch ist es schade, daß der Erfahrungsschatz und das Wissen von Jörg Schilling dort nicht weiter einfließen wird. Auch existieren offenbar wirklich Fehler, die im Original nicht auftreten. Und die Codebasis ist deutlich älter, cdrkit basiert auf einem vergleichsweise alten cdrtools (nämlich der letzten GPL-Version vor dem Wechsel zu CDDL).

### dvd+rw-tools
#### Praktisches

Es ist schade, daß die dvd+rw-tools keine CDs beschreiben können. Dann hätte ich mich große Überlegungen vermutlich einfach sparen können und diese verwendet. Sonderlich exotische Anforderungen habe ich ohnehin nicht. Aber so muß ich mich ohnehin noch zwischen den übrigen Kandidaten entscheiden.

### Nero Linux
#### Finanzielles

Nero Linux 3 kostet 20 Euro. Das ist natürlich sehr viel mehr als die anderen Kandidaten kosten (allesamt kostenlos), allerdings auch nicht wirklich viel Geld.

#### Praktisches

Die langjährige Erfahrung des Entwicklerunternehmens und die (vermutete) große Bereitschaft der Gerätehersteller, behilflich zu sein, spricht mindestens ebensosehr für Nero wie vergleichbare Überlegungen für die cdrtools sprechen.

Die Software wird allerdings in Binärform ausgeliefert. Man kann sie also nicht selbst kompilieren, was beispielsweise zum Problem werden könnte, wenn neue Bibliotheksversionen im System installiert sind und die nicht mehr verfügbar sowie die neuen inkompatibel sind.

Nero gibt an, daß sie mit Ubuntu 5.10 lauffähig sei. Aktuell ist aber die Nachfolgerversion Ubuntu 7.04, die auch auf meinem Rechner läuft. Glücklicherweise funktioniert es. Aber wie erwähnt, Updates des Systems könnten einmal zum Problem werden.

Außerdem kann man natürlich nicht mehr zwischen vielen verschiedenen grafischen Frontends wählen, sondern ist auf die Nero-GUI festgelegt. Sie erinnert stark an die Windows-Version, Umsteiger sollten es also leicht haben. Nachdem auch Linux-Frontends sich häufig an Nero angelehnt haben, sollte es aber auch für alle anderen kein größeres Problem sein, abgesehen von der fehlenden Möglichkeit, beispielsweise zu Zwecken des Scripting auf die Benutzeroberfläche zu verzichten und sich auf die Kommandozeile zu beschränken.

## Mein Rat

Ich empfehle, zunächst das Programm zu versuchen, das als Standardbrennprogramm bei der eigenen Linux-Distribution mitgeliefert wird. Wenn es zu Problemen kommt und cdrkit verwendet wurde, kann es sich lohnen, die cdrtools zu kompilieren und zu versuchen. Aber ansonsten sehe ich aus reiner Anwendersicht wenige Gründe, eines unbedingt deintallieren und das andere installieren zu wollen (das Benennungsschema mag ein schwaches Argument für cdrkit sein, die Erfahrung von Jörg Schilling ein recht starkes Argument für die cdrtools, aber „works for me“ ist meiner Ansicht nach für den Anwender ein völlig akzeptabler Standpunkt.

Die dvd+rw-tools können leider keine CDs brennen, sind aber in der Bedienung einfacher, dafür aber wohl auch etwas weniger mächtig als cdrtools/cdrkit. Wenn man aber CDs brennen möchte, muß man sich für diesen Teil ja noch immer zwischen den anderen Kandidaten entscheiden.

Nero kostet derzeit 20 Euro und ist Closed Source. Es kann nicht per Kommandozeile gesteuert und so geskriptet werden. Muß man eben abwägen, ob einem dies wichtig ist.

## Meine Entscheidung

Ich habe Nero Linux 3 gekauft.

Jörg Schilling ist sicherlich äußerst kompetent, aber ich ziehe Nero seiner Software vor. Die Mitarbeiter von Nero (vormals Ahead) haben mich noch nie übelst beschimpft und beleidigt, Jörg Schilling hat dies wiederholt getan.

Ich halte Jörg Schilling für deutlich kompetenter als die cdrkit-Entwickler. Das meine ich nicht derogativ in Bezug auf die cdrkit-Entwickler, aber die jahrelange Erfahrung mit Brennen unter mehreren Betriebssystemen zeichnet Jörg Schilling aus.

Nero hat ebenfalls extrem viel Erfahrung mit Brennsoftware und Brennhardware, schließlich sind sie unter Windows Marktführer. Jörg Schilling mag eine große Sammlung von Brennern besitzen und „geheime Kommandos“ herausgefunden haben, Nero kriegt mit Sicherheit eine einwandfreie Unterstützung der Hersteller. Schließlich können sie damit rechnen, daß Zeitschriftentests häufig unter Verwendung von Nero durchgeführt werden.

Hinzu kommen rechtliche Unsicherheiten. Wer der Meinung ist, daß er legal fremden Code in seine Programme einbauen und diesen dann unter ihm genehme Lizenzen stellen darf, ohne daß der Urheber des fremden Codes ein Mitspracherecht habe, der ist niemand, dessen Code ich unbedingt nutzen möchte. Wobei nutzen fast noch unkritisch ist, verbreiten würde richtig spaßig.

Also Nero Linux 3 und nicht cdrecord oder cdrkit. Die 20 Euro leiste ich mir gerne, wenn ich dafür ein Stück Software bekomme, das alles kann, was ich benötige.

In gewisser Weise sind das für mich spannende Überlegungen gewesen: Ich weiß nun, daß es tatsächlich Closed-Source-Software gibt, die ich nicht einfach verwende, weil es einfacher ist oder weil sie mehr kann als vergleichbare Open-Source- oder Freie Software. Nein, es gibt auch Open-Source-Software, der ich im Gegensatz zum Closed-Source-Pendant einfach nicht vertraue. 