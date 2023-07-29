---
title: "Caching-Tutorial für Webautoren und Webmaster"
description: Deutsche Übersetzung von Mark Nottinghams Caching-Tutorial
date: 2010-02-26
lastmod: 2014-12-07
tags: ['Übersetzung', 'Web', 'Caching']
---
**Anmerkung des Übersetzers:** Dies ist das [Caching Tutorial for Web Authors and Webmasters](https://www.mnot.net/cache_docs/) von [Mark Nottingham](https://www.mnot.net/personal/), übersetzt ins Deutsche von [Thomas Hühn](https://www.thomas-huehn.de/).

Dieses Dokument hat informativen (d.h. nicht-normativen) Charakter. Obwohl es technischer Natur ist, versucht es, die beinhalteten Konzepte verständlich und auf realistische Situationen anwendbar zu machen. Daher sind einige Aspekte der Thematik im Sinne einer klaren Erläuterung vereinfacht oder weggelassen. Wenn Sie sich für die Einzelheiten des Gebietes interessieren, durchstöbern Sie bitte die [Verweise und weitere Informationen](#verweise-und-weitere-informationen) am Ende.

## Was ist ein Web-Cache? Warum benutzen die Leute welche?

Ein Web-Cache sitzt zwischen einem oder mehreren Webservern (auch Origin-Server genannt) und einem oder vielen Clients. Er sieht Anfragen vorbeikommen und speichert dabei Kopien der Antworten – wie HTML-Seiten, Bilder und Dateien (zusammen auch Repräsentationen genannt) – für sich selbst ab. Dann kann er bei einer anderen Anfrage nach derselben URL die Antwort nutzen, die er bereits hat, anstatt den Origin-Server erneut danach zu fragen.

Es gibt zwei Hauptgründe, weshalb Web-Caches genutzt werden:

* **Um Latenzen zu verringern** – Weil die Anfrage vom Cache statt vom Origin-Server befriedigt wird (und der Cache sich näher am Client befindet), dauert es weniger lange, die Repräsentation zu holen und anzuzeigen. Dadurch wirkt es so, als ob das Web schneller reagiert.

* **Um Netzwerkverkehr zu verringern** – Weil Repräsentationen wiederverwendet werden, verringert sich die Bandbreite, die ein Client nutzt. Das spart Geld, wenn der Client für Netzwerkverkehr bezahlt und hält die Bandbreitenanforderungen niedriger und handhabbarer.

## Arten von Web-Caches

### Browser-Caches

Wenn Sie den Einstellungsdialog eines modernen Webbrowsers (wie Internet Explorer, Safari oder Mozilla) erkunden, finden Sie wahrscheinlich eine Einstellung für „Cache“. Mit dieser Einstellung können Sie einen Teil der Computerfestplatte zur Seite nehmen, um darin Repräsentationen zu speichern, die Sie bereits gesehen haben. Nur für sich selbst. Der Browser-Cache arbeitet nach ziemlich einfachen Regeln. Er stellt sicher, daß die Repräsentationen „fresh“ sind, üblicherweise einmal pro Sitzung (also einmal pro Aufruf des Webbrowsers).

<aside>
Anmerkung des Übersetzers: Ich verzichte darauf, „fresh“ als „frisch“ und „freshness“ als „Frische“ zu übersetzen, ebenso wie ich weiter oben bereits „Origin“ stehengelassen habe. Diese Begriffe gehören zum HTTP-Jargon, sind recht einfach, so daß die meisten Leser die deutsche Übersetzung kennen dürften, und eine Übersetzung würde nur zu Verwirrung führen, sobald Sie – geschätzter Leser – in englischsprachigen Quellen nach weiteren Informationen suchen.
</aside>

Dieser Cache ist besonders nützlich, wenn Benutzer auf den „Zurück“-Button oder auf einen Link zu einer Seite klicken, die sie gerade eben angesehen haben. Und wenn Sie dieselben Bilder zur Navigation auf der gesamten Webpräsenz nutzen, werden sie fast sofort aus den Browsercaches geliefert.

### Proxy-Caches

Web-Proxy-Caches arbeiten nach demselben Prinzip, aber in einem viel größeren Rahmen. Proxies bedienen hunderte oder tausende von Benutzern auf dieselbe Art; große Unternehmen und Internetprovider richten sie oft auf ihren Firewalls oder als eigenständige Server ein (auch intermediaries genannt).

Weil Proxy-Caches weder zum Client, noch zum Origin-Server gehören, sondern sich stattdessen draußen im weiten Netz befinden, müssen Anfragen irgendwie zu ihnen gelenkt werden. Eine Möglichkeit, das zu tun, besteht darin, dem Webbrowser über die Proxyeinstellungen von Hand zu sagen, welchen Proxy er benutzen soll; eine andere Möglichkeit ist die des Abfangens. Abfangende Proxies lassen Webanfragen vom zugrundeliegenden Netzwerk zu sich umleiten, so daß Clients nicht für sie konfiguriert werden müssen. Sie müssen nicht einmal von ihnen wissen.

Proxy-Caches sind eine Form von gemeinsamen Caches; anstatt nur von einer Person benutzt zu werden, haben sie üblicherweise eine große Anzahl von Nutzern, und deswegen sind sie sehr gut darin, Latenzen und Netzwerkverkehr zu reduzieren. Denn beliebte Repräsentationen werden mehrfach wiederverwendet.

### Gateway-Caches

Auch als *reverse proxy caches* oder *surrogate caches* bekannt, sind Gateway-Caches ebenfalls intermediaries, doch werden sie üblicherweise nicht von Netzwerkadministratoren eingerichtet, um Bandbreite zu sparen, sondern von Webmastern selbst, um ihre Seite besser skalierbar, zuverlässiger und schneller zu machen.

Anfragen können mehrfach durch Gateway-Caches geleitet werden, doch wird üblicherweise eine Art von Lastverteiler genutzt, um einen oder mehrere von ihnen für die Clients wie Origin-Server aussehen zu lassen.

Content delivery networks (CDNs) verteilen Gateway-Caches über das ganze Internet (oder einen Teil davon) und verkaufen Caching an interessierte Webseiten. [Speedera](http://www.speedera.com/) und [Akamai](http://www.akamai.com/) sind Beispiele für CDNs.

Dieses Tutorial konzentriert sich hauptsächlich auf Browser- und Proxy-Caches, obwohl einige der Informationen auch für diejenigen geeignet sind, die sich auch für Gateway-Caches interessieren.

## Sind Web-Caches nicht etwas Schlechtes? Warum sollte ich ihnen behilflich sein?

Web-Caching ist eine der am meisten mißverstandenen Techniken im Internet. Besonders Webmaster fürchten, die Kontrolle über ihre Webpräsenz zu verlieren, denn ein Proxy-Cache kann Benutzer vor ihnen „verstecken“, wodurch es schwierig wird festzustellen, wer die Webpräsenz nutzt.

Leider können Sie selbst in Abwesenheit von Web-Caches nicht sicher sein, daß sie ein genaues Bild bekommen können, wie Benutzer ihre Webpräsenz sehen. Dafür gibt es im Internet zu viele Variablen. Wenn das für Sie ein echtes Problem ist, dann wird dieses Tutorial Ihnen zeigen, wie Sie die Statistiken bekommen, die sie brauchen, ohne Ihre Webpräsenz cache-unfreundlich zu machen.

Eine weitere Befürchtung ist, daß Caches Inhalte ausliefern, die veraltet, oder stale, sind. Dieses Tutorial kann ihnen jedoch zeigen, wie Sie Ihren Server so konfigurieren, daß Sie steuern, wie Inhalte gecachet werden.

Auf der anderen Seite können Caches dabei helfen, daß Ihre Webpräsenz schneller lädt, sowie Last auf dem Server und auf der Internetanbindung einsparen, wenn Sie Ihre Webpräsenz gut planen. Der Unterschied kann dramatisch sein; eine Webpräsenz, die schwer zu cachen ist, mag mehrere Sekunden zum Laden brauchen, während eine, die die Vorteile des Cachings ausnutzt, im Vergleich dazu sofort da zu sein scheint. Die Benutzer werden eine schnell-ladende Webpräsenz zu schätzen wissen und diese öfter besuchen.

Sehen Sie es so: viele große Internetunternehmen geben Millionen von Dollar dafür aus, rund um die Welt Server einzurichten, die ihre Inhalte replizieren, damit diese für ihre Benutzer so schnell wie möglich zu erreichen sind. Caches tun dasselbe für Sie, und sie sind sogar noch näher am Endbenutzer. Und das beste an alldem: Sie müssen dafür nichts bezahlen.

Es ist einfach so, daß Proxy- und Browsercaches genutzt werden, ob Sie es nun mögen oder nicht. Wenn Sie Ihre Webpräsenz nicht so konfigurieren, daß sie richtig gecachet wird, wird sie unter Verwendung der Defaulteinstellungen gecachet, für die sich der Cacheadministrator entschieden hat.

<aside>
CDNs (content delivery networks) sind eine interessante Entwicklung, weil deren Gateway-Caches im Gegensatz zu vielen Proxy-Caches auf die Interessen der Webpräsenz, die gecachet wird, abgestimmt sind, so daß diese Probleme nicht zu sehen sind. Doch selbst wenn Sie ein CDN nutzen, müssen Sie daran denken, daß es „weiter hinten im Netz“ Proxy- und Browsercaches geben wird.
</aside>

## Wie Web-Caches arbeiten

Alle Caches haben eine Sammlung von Regeln, die sie benutzen, um zu bestimmen, wann sie eine Repräsentation aus dem Cache ausliefern, falls sie verfügbar ist. Einige dieser Regeln sind in den Protokollen (HTTP 1.0 und 1.1) festgelegt, andere werden vom Administrator des Cache bestimmt (entweder der Benutzer des Browser-Cache oder der Proxy-Administrator).

Allgemein gesprochen sind dies die gebräuchlichsten Regeln, die befolgt werden (keine Sorge, falls Sie nicht alle Einzelheiten verstehen, sie werden weiter unten erklärt):

1. Wenn die Header der Antwort dem Cache sagen, daß er sie nicht aufheben soll, wird er es nicht tun.
    
2. Wenn die Anfrage paßwortgeschützt oder verschlüsselt war (zum Beispiel durch HTTPS), wird sie nicht gecachet.
    
3. Repräsentationen, die *fresh* sind, werden direkt aus dem Cache ausgeliefert, ohne den Origin-Server zu fragen. Eine gecachete Repräsentation wird als *fresh* betrachtet (das bedeutet, sie kann zum Client geschickt werden, ohne den Origin-Server zu fragen), wenn:

   * sie eine Ablaufzeit oder einen anderen Header besitzt, der die Haltbarkeitszeit bestimmt, und sie noch innerhalb der Haltbarkeitszeit ist, oder
        
   * der Cache die Repräsentation kürzlich gesehen hat und sie vor relativ langer Zeit das letzte Mal geändert worden ist.
   
4. Wenn eine Repräsentation abgelaufen ist (stale), wird der Origin-Server gebeten, diese zu validieren, also dem Cache mitzuteilen, ob dessen Kopie noch immer brauchbar ist.

5. Unter bestimmten Voraussetzungen – beispielsweise wenn er eine Netzwerkverbindung verloren hat – kann ein Cache abgelaufene Antworten ausliefern, ohne den Origin-Server zu fragen.

Wenn es keinen Validator (einen ETag- oder Last-Modified-Header) bei einer Antwort gibt, **und** sie keine ausdrückliche Freshness-Information enthält, wird die Antwort in der Regel – allerdings nicht immer – als uncachebar betrachtet.

Freshness und Validierung sind zusammen die wichtigsten Arten, auf die ein Cache mit Inhalten arbeitet. Eine Repräsentation, die fresh ist, wird sofort aus dem Cache verfügbar sein, wohingegen eine validierte Repräsentation verhindert, daß die gesamte Repräsentation wiederum geschickt werden muß, wenn sie sich nicht geändert hat.

## Wie man Caches steuert (und wie man es nicht tut)

Es gibt mehrere Werkzeuge, die Webdesigner und Webmaster nutzen können, um einzustellen, wie Caches ihre Webpräsenzen behandeln. Es mag erfordern, daß Sie sich Ihre Hände ein wenig mit der Serverkonfiguration schmutzig machen, aber die Ergebnisse sind es wert. Für Einzelheiten zur Benutzung dieser Werkzeuge mit Ihrem Server, lesen Sie bitte die [Implementierungshinweise](#implementierungshinweise-fuer-webserver) weiter unten.

### HTML-Meta-Tags und HTTP-Header

HTML-Autoren können in den `<HEAD>`-Abschnitt ihres Dokuments Tags einfügen, die dessen Eigenschaften beschreiben. Diese Meta-Tags werden häufig im Glauben benutzt daß sie ein Dokument als uncachebar oder als nach einer bestimmten Zeit ablaufend markieren können.

Meta-Tags sind einfach zu verwenden, aber sie sind nicht besonders effektiv. Das liegt daran, daß sie nur von einigen Browser-Caches beachtet werden (die tatsächlich den HTML-Code lesen), nicht aber von Proxy-Caches (die fast niemals das HTML im Dokument lesen). Auch wenn es verlockend ist, ein `Pragma: no-cache` als Meta-Tag in eine Webseite einzufügen, läßt es diese nicht unbedingt fresh bleiben.

Auf der anderen Seite geben echte HTTP-Header Ihnen eine Menge Kontrolle darüber, wie sowohl Browsercaches als auch Proxies Ihre Repräsentationen behandeln. Sie sind im HTML nicht sichtbar und werden üblicherweise vom Webserver automatisch erzeugt. Jedoch können Sie sie bis zu einem gewissen Grad steuern, in Abhängigkeit vom Server, den Sie nutzen. In den folgenden Abschnitten werden Sie erfahren, welche HTTP-Header interessant sind und wie Sie diese auf Ihre Webpräsenz anwenden können.

HTTP-Header werden vom Server vor dem HTML-Code gesendet, und sie werden nur vom Browser und allen Zwischencaches gesehen. Typische HTTP-1.1-Antwortheader könnten so aussehen:

```
HTTP/1.1 200 OK
Date: Fri, 30 Oct 1998 13:19:41 GMT
Server: Apache/1.3.3 (Unix)
Cache-Control: max-age=3600, must-revalidate
Expires: Fri, 30 Oct 1998 14:19:41 GMT
Last-Modified: Mon, 29 Jun 1998 02:28:12 GMT
ETag: "3e86-410-3596fbbc"
Content-Length: 1040
Content-Type: text/html
```

Der HTML-Code würde nun durch eine Leerzeile getrennt auf diese Header folgen. Lesen Sie bitte die [Implementierungshinweise](#implementierungshinweise-fuer-webserver), um zu erfahren, wie Sie diese HTTP-Header setzen können.

### Pragma-HTTP-Header (und warum diese nicht funktionieren)

Viele Leute glauben, daß eine Repräsentation uncachebar gemacht wird, wenn sie ihr einen `Pragma: no-cache`-HTTP-Header zuordnen. Das ist nicht unbedingt richtig; die HTTP-Spezifikation gibt keinerlei Richtlinien zu Pragma-Antwort-Headern vor, stattdessen werden Pragma-Anforderungs-Header besprochen (die Header, die ein Browser an den Server sendet). Auch wenn einige wenige Caches diesen Header beachten mögen, wird die Mehrzahl es nicht tun und der Header hat keine Wirkung. Nutzen Sie stattdessen die folgenden Header.

### Freshness über den Expires-HTTP-Header steuern

Der `Expires`-HTTP-Header ist ein grundlegendes Mittel, um Caches zu steuern; er sagt allen Caches, wie lange die zugeordnete Repräsentation *fresh* ist. Nach Ablauf dieser Zeit fragen Caches stets beim Origin-Server nach, ob sich das Dokument geändert hat. `Expires`-Header werden von praktisch jedem Cache unterstützt.

Die meisten Webserver erlauben Ihnen, `Expires`-Antwort-Header auf verschiedene Weisen zu setzen. Üblicherweise erlauben sie, eine absolute Zeit bis zum Ablaufen zu setzen, eine Zeit zu setzen, die auf der letzten Zeit basiert, zu der der Client die Repräsentation geholt hat (last *access time*), oder eine Zeit zu setzen, die auf der letzten Zeit basiert, zu der das Dokument auf Ihrem Server verändert worden ist (last *modification time*).

`Expires`-Header sind besonders gut dafür geeignet, statische Bilder (wie Navigationsleisten und Buttons) cachebar zu machen. Weil diese sich nicht viel verändern, können Sie extrem lange Ablaufzeiten für sie festlegen, wodurch Ihre Webpräsenz Ihren Benutzern viel schneller zu reagieren scheint. Auch sind sie nützlich, um das Caching einer Seite zu steuern, die sich häufig ändert. Im Beispiel einer Nachrichtenseite, die Sie einmal am Tag um sechs Uhr früh aktualisieren, können Sie die Repräsentation zu diesem Zeitpunkt ablaufen lassen, so daß die Caches wissen, wann sie eine neue Ausgabe holen müssen, ohne daß die Benutzer den “Neu laden”-Button anklicken müssen.

Der **einzig** gültige Wert in einem `Expires`-Header ist eine HTTP-Zeitangabe; alles andere wird höchstwahrscheinlich als “in der Vergangenheit” interpretiert, so daß die Repräsentation uncachebar ist. Denken Sie auch daran, daß die Zeit in einer HTTP-Zeitangabe nach Greenwich Mean Time (GMT) angegeben wird, nicht nach der lokalen Zeit.

Ein Beispiel:

```
Expires: Fri, 30 Oct 1998 14:19:41 GMT
```

Obwohl der `Expires`-Header nützlich ist, unterliegt er einigen Einschränkungen. Zunächst einmal müssen die Uhren des Webservers und des Caches synchronisiert sein, da Zeitangaben betroffen sind; wenn beide unterschiedliche Vorstellung von der aktuellen Uhrzeit haben, wird das beabsichtigte Ergebnis nicht erreicht werden und die Caches betrachten möglicherweise veraltete Inhalte als *fresh*.

Ein weiteres Problem mit `Expires` ist, daß man leicht vergißt, daß Sie einen Inhalt zu einer bestimmten Zeit ablaufen lassen. Wenn Sie die `Expires`-Zeit nicht aktualisieren, bevor sie abläuft, wird jede einzelne Anforderung wieder Ihren Webserver treffen und damit Last und Latenz erhöhen.

<aside>
Es ist wichtig sicherzustellen, daß die Uhr Ihres Webserver richtig geht, wenn Sie den `Expires`-Header verwenden. Eine Möglichkeit, das zu tun, ist, das Network Time Protocol zu verwenden; sprechen Sie mit Ihrem örtlichen Systemadministrator, um mehr zu erfahren.
</aside>

### Cache-Control-HTTP-Header

HTTP 1.1 führte eine neue Klasse von Headern ein, die `Cache-Control`-Antwort-Header, um Webautoren mehr Kontrolle über ihren Inhalt zu geben und um die Beschränkungen von `Expire` anzugehen.

Nützliche `Cache-Control`-Antwort-Header beinhalten:

`max-age=[seconds]`
: Bestimmt die maximale Zeitdauer, während der eine Repräsentation als fresh betrachtet wird. Ähnlich zu Expires gibt diese Anweisung die Zeit relativ zum Zeitpunkt der Anfrage an, nicht absolut. `[seconds]` ist die Anzahl der Sekunden vom Anfragezeitpunkt an, für die Sie die Repräsentation fresh haben möchten.

`s-maxage=[seconds]`
: ähnlich wie max-age, nur daß es sich ausschließlich auf gemeinsame Caches (zum Beispiel Proxies) bezieht.

`public`
: Markiert paßwortgeschützte Antworten als cachebar; normalerweise sind Antworten automatisch `private`, wenn HTTP-Authentifizierung verlangt wird.

`private`
: Erlaubt Caches, die nur für einen einzelnen Benutzer gelten, die Antwort zu speichern, gemeinsame Caches (z.B. von Proxys) dürfen dies nicht.

`no-cache`
: Zwingt Caches, die Anfrage jedesmal zur Validierung an den Origin-Server weiterzuleiten, bevor sie gecachete Kopien herausgeben. Dies ist nützlich, um sicherzustellen, daß ein Passwortschutz beachtet wird (im Zusammenspiel mit `public`), oder um strikte Freshness zu gewährleisten, ohne all die Vorteile des Cachings aufzugeben.

`no-store`
: Weist Caches an, unter keinen Umständen eine Kopie der Repräsentation zu halten.

`must-revalidate`
: Sagt Caches, daß sie jegliche Freshness-Information beachten müssen, die Sie ihnen zu einer Repräsentation geben. HTTP erlaubt Caches unter besonderen Umständen, abgelaufene Repräsentationen auszuliefern; durch Angabe dieses Headers teilen Sie dem Cache mit, daß Sie von ihm erwarten, daß er ihre Regeln strikt einhält.

`proxy-revalidate`
: Ähnlich wie `must-revalidate`, außer daß es sich nur an Proxy-Caches wendet.

  Zum Beispiel:

 `Cache-Control: max-age=3600, must-revalidate`

Wenn sowohl `Cache-Control` als auch `Expires` vorhanden sind, hat `Cache-Control` Vorrang. Wenn Sie vorhaben, die `Cache-Control`-Header einzusetzen, sollten Sie einen Blick in die hervorragende Dokumentation in HTTP 1.1 werfen, siehe [Verweise und weitere Informationen](#verweise-und-weitere-informationen).

### Validatoren und Validierung

In [Wie Web-Caches arbeiten](#wie-web-caches-arbeiten) hatten wir gesagt, daß Server und Caches die Validierung nutzen, um sich mitzuteilen, wenn eine Repräsentation verändert worden ist. Dadurch vermeiden Caches, daß die gesamte Repräsentation heruntergeladen werden muß, wenn sie zwar bereits eine Kopie lokal vorhalten, sich aber nicht sicher sind, ob diese noch fresh ist.

Validatoren sind sehr wichtig; wenn keiner vorhanden ist und auch keine Freshness-Informationen (`Expires` oder `Cache-Control`) verfügbar sind, speichern Caches eine Repräsentation überhaupt nicht.

Der am häufigsten verwendete Validator ist die Zeit, zu der das Dokument sich zuletzt geändert hat, was durch den `Last-Modified`-Header mitgeteilt wird. Wenn ein Cache eine Repräsentation gespeichert hat, die einen `Last-Modified`-Header beinhaltet, kann er diesen nutzen, um den Server zu fragen, ob sich die Repräsentation seit dem letzten Zeitpunkt, zu dem er sie gesehen hat, geändert hat. Dazu stellt er eine `If-Modified-Since`-Anfrage.

HTTP 1.1 hat eine neue Art von Validator eingeführt, das ETag. ETags sind eindeutige Bezeichner, die vom Server erzeugt und jedesmal geändert werden, wenn die Repräsentation sich ändert. Weil der Server kontrolliert, wie das ETag erzeugt wird, können Caches sich sicher sein, daß die Repräsentation wirklich dieselbe ist, wenn sie eine `If-None-Match`-Anfrage stellen und das ETag übereinstimmt.

Nahezu alle Caches nutzen `Last-Modified`-Zeiten, um festzustellen, ob eine Repräsentation fresh ist; ETag-Validierung wird ebenfalls immer üblicher.

Die meisten modernen Webserver erzeugen sowohl `ETag`-, als auch `Last-Modified`-Header als Validatoren für statische Inhalte (zum Beispiel Dateien) automatisch; Sie müssen dazu nichts tun. Die Server wissen jedoch nicht genug über dynamische Inhalte (wie CGI, ASP oder Datenbankinhalte), um dafür Validatoren generieren zu können; siehe [Cachebewußte Skripte schreiben](#cachebewusste-skripte-schreiben).

## Tipps zum Bau einer cachebewußten Seite

Neben Freshness-Informationen und Validierung gibt es eine Reihe weiterer Dinge, die Sie tun können, um Ihre Webpräsenz cache-freundlicher zu gestalten.

* **Benutzen Sie URLs auf konsistente Art und Weise** – dies ist die Goldene Regel des Cachings. Wenn Sie denselben Inhalt auf verschiedenen Seiten ausliefern, zu verschiedenen Benutzern oder von verschiedenen Webpräsenzen, sollte er dieselbe URL verwenden. Dies ist die einfachste und effektivste Art, Ihre Seite cache-freundlich zu gestalten. Wenn Sie beispielsweise einmal /index.html als einen Verweis in Ihrem HTML nutzen, nutzen Sie ihn immer genau so.

* **Benutzen Sie eine gemeinsame Bibliothek von Bildern** und anderen Elementen und verweisen Sie von verschiedenen Orten aus darauf.

* **Lassen Sie Bilder und Seiten, die sich nicht häufig verändern, von Caches speichern,** indem Sie einen `Cache-Control: max-age`-Header mit einem großen Wert setzen.

* **Sorgen Sie dafür, daß Caches regelmäßig aktualisierte Seiten erkennen,** indem Sie eine angemessene max-age oder Ablaufzeit angeben.

* **Wenn sich eine Ressource ändert (insbesondere eine herunterladbare Datei), ändern Sie ihren Namen.** Auf diese Art können Sie die Ressource weit in der Zukunft ablaufen lassen und dennoch garantieren, daß die richtige Version ausgeliefert wird; die Seite, die dorthin verlinkt, ist die einzige, die eine kurze Ablaufzeit benötigt.

* **Ändern Sie Dateien nicht unnötigerweise.** Wenn Sie es doch tun, wird alles eine fälschlich junge Last-Modified-Zeitangabe haben. Wenn Sie zum Beispiel Ihre Webpräsenz aktualisieren, kopieren Sie nicht die gesamte Webpräsenz, sondern nur die Dateien, die Sie verändert haben.

* **Benutzen Sie Cookies nur da, wo es notwendig ist** – Cookies sind schwierig zu cachen und in den meisten Situationen auch unnötig. Wenn Sie ein Cookie benutzen müssen, beschränken Sie die Nutzung auf dynamische Seiten.

* **Minimieren Sie die Nutzung von SSL** – denn verschlüsselte Seiten werden von gemeinsamen Caches nicht gespeichert, nutzen Sie sie nur, wenn sie müssen, und nutzen Sie Bilder auf SSL-Seiten nur sparsam.

* **Prüfen Sie ihre Seiten mit [REDbot](https://redbot.org/)** – er kann Ihnen helfen, viele der Konzepte aus diesem Tutorial anzuwenden.

## Cachebewußte Skripte schreiben

Standardmäßig liefern die meisten Skripte keinen Validator (einen `Last-Modified-If`– oder `ETag`-Antwort-Header) zurück. Während manche Skripte wirklich dynamisch sind (das bedeutet, daß sie unterschiedliche Antworten auf jede Anfrage liefern), können viele Skripte (wie Suchmaschinen und datenbankbasierte Webpräsenzen) einen Vorteil daraus ziehen, cache-freundlich zu sein.

Allgemein gesagt sollte ein Skript cachebar sein, wenn es eine Ausgabe erzeugt, die bei derselben Anforderung zu einem späteren Zeitpunkt (sei es Minuten oder Tage später) reproduzierbar ist. Wenn der Inhalt des Skripts nur davon abhängt, was in der URL steht, ist es cachebar; wenn die Ausgabe von einem Cookie, Passwortschutz oder anderen externen Kriterien abhängt, ist es das vermutlich nicht.

* Die beste Art ein Skript cache-freundlich zu gestalten (und dabei eine höhere Leistung zu erzielen) ist, den Inhalt immer dann in eine einfache Datei zu herauszuschreiben, wenn er sich ändert. Der Webserver kann diese Datei dann wie jede andere Webseite behandeln und Validatoren erzeugen sowie benutzen, was Ihr Leben vereinfacht. Denken Sie daran, nur Dateien zu schreiben, die sich verändert haben, so daß die `Last-Modified`-Zeitangaben erhalten bleiben.

* Eine andere Möglichkeit, ein Skript auf eine beschränkte Weise cachebar zu machen, ist, einen zeitbezogenen Header so weit in die Zukunkt wie praktikabel zu setzen. Obwohl dies mit `Expires` erreicht werden kann, ist es wahrscheinlich einfacher, `Cache-Control: max-age` zu verwenden, was die Anfrage für eine bestimmte Zeit nach der Anfrage fresh hält.

* Wenn Sie das nicht tun können, müssen Sie dem Skript beibringen, einen Validator zu erzeugen, und dann auf `If-Modified-Since`– und/oder auch `If-None-Match-Anfragen` antworten. Dies kann durch Parsen der HTTP-Header und anschließendes Antworten mit `304 Not Modified` erreicht werden, wenn es angebracht ist. Leider ist dies keine triviale Aufgabe.

Einige weitere Tipps:

* **Benutzen sie kein POST,** außer es ist angebracht. Antworten auf die POST-Methode werden von den meisten Caches nicht gespeichert; wenn Sie Informationen im Pfad- oder Query-Teil der URL (via GET) mitschicken, können Caches diese Information für zukünftige Anfragen aufheben.

* **Nehmen Sie keine nutzerspezifische Information in die URL auf,** es sei denn, der erzeugte Inhalt ist völlig einmalig für diesen Benutzer.

* **Verlassen Sie sich nicht darauf, daß alle Anfragen eines Benutzers vom selben Rechner kommen,** denn Caches arbeiten oft zusammen.

* **Erzeugen Sie Content-Length-Antwort-Header**. Das ist leicht und erlaubt, daß die Antwort Ihres Skripts in einer *persistenten Verbindung* übertragen wird. Das erlaubt es Clients, mehrere Repräsentationen über eine TCP/IP-Verbindung anzufordern, statt für jede Anfrage eine eigene Verbindung aufmachen zu müssen. Es wird ihre Webpräsenz viel schneller erscheinen lassen.

Siehe auch die [Implementierungshinweise](#implementierungshinweise-fuer-webserver) für spezifischere Informationen.

## Häufig gestellte Fragen

### Welche sind die wichtigsten Dinge, die cachebar gemacht werden sollten?

Eine gute Strategie besteht darin, herauszufinden, welches die beliebtesten und größten Repräsentationen sind (besonders Bilder) und mit ihnen zu beginnen.

### Wie kann ich meine Seiten durch Caches so schnell wie möglich machen?

Die am besten cachebaren Repräsentationen sind die, die eine lange Haltbarkeitszeit gesetzt haben. Validierung hilft die Zeit zu verringern, die es dauert, bis man eine Repräsentation sieht, aber der Cache muß noch immer zum Origin-Server Verbindung aufnehmen, um zu sehen, ob sie fresh ist. Wenn der Cache bereits weiß, daß sie fresh ist, wird sie sofort ausgeliefert.

### Ich verstehe, daß Caching eine gute Sache ist, aber ich brauche Statistiken, wie viele Leute meine Seite besuchen!

Wenn Sie jedes Mal mitbekommen wollen, wenn auf eine Seite zugegriffen wird, wählen Sie ein kleines Element der Seite (oder die Seite selbst) und machen Sie sie uncachebar, indem Sie die passenden Header vergeben. Beispielsweise könnten Sie von jeder Seite aus auf ein transparentes Ein-Pixel-Bild verlinken. Der Referer Header enthält dann die Information, von welcher Seite aus das Bild aufgerufen worden ist.

Seien Sie sich im Klaren darüber, daß Sie nicht einmal dadurch wirklich genaue Statistiken über Ihre Benutzer erhalten, und es ist unfreundlich zum Internet und zu Ihren Benutzern; es erzeugt unnötigen Netzwerkverkehr und zwingt die Leute, auf das Herunterladen dieses ungecacheten Elements zu warten. Für weitere Informationen zum Thema siehe „On Interpreting Access Statistics“ in den [Verweisen](#verweise-und-weitere-informationen).

### Wie kann ich die HTTP-Header einer Repräsentation ansehen?

Viele Webbrowser zeigen die Expires- und Last-Modified-Header in einer „Seiteninformation“ oder einer ähnlichen Benutzerschnittstelle an. Falls diese verfügbar ist, bekommen Sie ein Menü von der Seite und etwaiger verknüpfter Repräsentationen (wie Bilder), samt derer Einzelheiten.

Um die vollen Header einer Repräsentation anzuschauen, können Sie sich mit einem Telnet-Client manuell zum Webserver verbinden.

Um dies zu tun, müssen Sie möglicherweise die Portnummer (standardmäßig 80) in ein gesondertes Feld eintragen oder sie müssen sich möglicherweise zu `www.example.com:80` oder zu `www.example.com 80` (beachten Sie das Leerzeichen) verbinden. Schauen Sie im Handbuch Ihres Telnet-Clients nach.

Sobald Sie eine Verbindung zu der Seite geöffnet haben, tippen Sie folgende Anfrage ein:

```
GET /foo.html HTTP/1.1 [return]
Host: www.example.com [return][return]
```

Drücken Sie die Enter-Taste an jeder Stelle, an der Sie `[return]` sehen; stellen Sie sicher, daß Sie sie am Ende zweimal drücken. Dies wird erst die Header und dann die volle Repräsentation anzeigen. Um nur die Header zu sehen, ersetzen Sie `GET` durch `HEAD`.

### Meine Seiten sind paßwortgeschützt; wie gehen Proxy-Caches mit ihnen um?

Standardmäßig werden durch HTTP-Authentifizierung geschützte Seiten als privat betrachtet und von gemeinsamen Caches nicht gespeichert. Jedoch können Sie authentifizierte Seiten durch einen `Cache-Control: public`-Header öffentlich machen; Caches, die HTTP 1.1 unterstützen, werden dann zulassen, daß diese Seiten gecachet werden.

Wenn Sie solche Seiten cachebar, dabei aber noch immer für jeden Benutzer authentifiziert machen wollen, kombinieren Sie die `Cache-Control: public`– und `no-cache`-Header. Das sagt dem Cache, daß er die Authentifizierungsinformationen des neuen Clients an den Origin-Server schicken muß, bevor er die Repräsentation aus dem Cache freigibt. Es sieht dann folgendermaßen aus:

```
Cache-Control: public, no-cache
```

Ob man es nun so tut oder nicht, es ist am besten, die Benutzung von Authentifizierung zu minimieren. Wenn beispielsweise Ihre Bilder nicht schutzbedürftig sind, legen Sie sie in ein gesondertes Verzeichnis und konfigurieren Sie Ihren Server so, daß er dafür keine Authentifizierung erzwingt. So sind diese Bilder cachebar.

### Sollte ich mir über die Sicherheit Sorgen machen, wenn die Leute über einen Cache auf meine Webpräsenz zugreifen?

SSL-verschlüsselte Seiten werden von Proxy-Caches nicht gecachet (oder entschlüsselt), also müssen Sie sich darum keine Sorgen machen. Weil Caches Nicht-SSL-Anfragen und -URLs speichern, die durch sie abgerufen werden,wäre es jedoch vorstellbar, daß ein skrupelloser Administrator Informationen über die Benutzer sammeln könnte, besonders in der URL.

Tatsächlich könnte jeder Administrator im Netzwerk zwischen Ihrem Server und Ihren Nutzern diese Art von Informationen sammeln. Ein besonderes Problem besteht dann, wenn CGI-Skripte Benutzernamen und Paßwörter in die URL selbst packen, dadurch wird es für andere leicht, deren Benutzerkonto herauszufinden und zu nutzen.

Wenn Sie sich allgemein der Probleme bewußt sind, die es im Bereich Websicherheit gibt, dann sollten Sie keine Überraschungen durch Proxy-Caches erleben.

### Ich suche nach einer integrierten Web-Veröffentlichungs-Lösung. Welche sind cachebewußt?

Das ist unterschiedlich. Grundsätzlich gesprochen ist es um so schwieriger zu cachen, je komplexer die Lösung ist. Die schlimmsten Lösungen sind diejenigen, die alle Inhalte dynamisch generieren, aber keine Validatoren bereitstellen. Diese sind möglicherweise gar nicht cachebar. Sprechen Sie mit technischen Ansprechpartnern des Herstellers, und lesen Sie die Implementierungshinweise weiter unten.

### Meine Bilder laufen in einem Monat ab, aber ich muß sie jetzt in den Caches verändern!

Der Expires-Header kann nicht umgangen werden; solange dem Cache (ob Browser oder Proxy) nicht der Speicher ausgeht und er die Repräsentationen löschen muß, wird die gecachete Kopie bis dahin genutzt werden.

Die erfolgversprechendste Lösung besteht darin, jegliche Links zu ihnen zu ändern. Auf diese Weise werden völlig neue Repräsentationen neu vom Origin-Server geladen werden. Denken Sie daran, daß die Seite, die auf eine Repräsentation verweist, ebenfalls gecachet wird. Deshalb ist es am besten, statische Bilder und ähnliche Repräsentationen sehr gut cachebar zu machen, und die HTML-Seiten, die zu ihnen verweisen, hingegen an der kurzen Leine zu halten.

Wenn Sie eine Repräsentation von einem bestimmten Cache neu laden möchten, können Sie entweder ein neues Laden erzwingen, wenn Sie den Cache nutzen (Firefox setzt einen `Pragma: no-cache`-Anforderungs-Header, wenn Sie Shift gedrückt halten, während Sie „Aktuelle Seite neu laden“ anklicken). Oder Sie können den Cache-Administrator bitten, die Repräsentation über seine Administrationsschnittstelle zu entfernen.

### Ich betreibe einen Webhosting-Dienst. Wie kann ich meine Nutzer cache-freundliche Seiten veröffentlichen lassen?

Wenn Sie Apache benutzen, denken Sie darüber nach, .htaccess-Dateien verwenden zu lassen und angemessene Dokumentation bereitzustellen.

Andernfalls können Sie auf jedem virtuellen Server vorbestimmte Bereiche für verschiedene Caching-Eigenschaften definieren. Zum Beispiel könnten Sie ein Verzeichnis /cache-1m, das nach dem Zugriff einen Monat lang gecachet wird, und einen /no-cache-Bereich anlegen, der mit Headern ausgeliefert wird, die Caches anweisen, keine Repräsentationen daraus zu speichern.

Was auch immer Sie tun können, am besten ist es, wenn Sie als erstes mit Ihren größten Kunden am Caching arbeiten. Die meisten Einsparungen (an Bandbreite und Last auf Ihren Servern) werden von Webpräsenzen mit vielen Zugriffen stammen.

### Ich habe meine Seiten als cachebar markiert, aber mein Webbrowser holt sie bei jeder Anforderung neu. Wie zwinge ich den Cache, Repräsentationen daraus zu speichern?

Von Caches wird nicht verlangt, daß sie eine Repräsentation speichern und wiederverwenden, von ihnen wird lediglich verlangt, daß sie sie unter bestimmten Bedingungen nicht speichern oder verwenden. Alle Caches fällen Entscheidungen, welche Repräsentationen sie speichern, anhand derer Größe, Art (z.B. Bild gegenüber HTML), oder wieviel Speicherplatz ihnen noch für lokale Kopien zur Verfügung steht. Ihre Repräsentationen werden möglicherweise nicht als aufhebenswert betrachtet, verglichen mit beliebteren oder größeren Repräsentationen.

Einige Caches erlauben ihren Administratoren zu priorisieren, welche Arten von Repräsentationen gespeichert werden, und manche erlauben es, daß Repräsentationen im Cache „festgenagelt“ werden, so daß sie immer verfügbar sind.

## Implementierungshinweise für Webserver

### Apache HTTP Server

[Apache](https://www.apache.org/) verwendet optionale Module, um Header einzufügen. Das betrifft auch `Expires` und `Cache-Control`. Beide Module sind in der Distribution ab Version 1.2 enthalten.

Die Module müssen in Apache selbst hineingebaut werden; obwohl sie in der Distribution enthalten sind, sind sie standardmäßig nicht eingeschaltet. Um herauszufinden, ob die Module in Ihrem Server eingeschaltet sind, suchen Sie die ausführbare Datei httpd und führen Sie `httpd -l` aus. Dadurch sollte eine Liste der verfügbaren Module angezeigt werden (beachten Sie, daß nur einkompilierte Module angezeigt werden, um auch dynamisch geladene Module anzuzeigen, geben Sie `httpd -M` ein). Die Module, um die es geht, sind expires_module und headers_module.

Wenn sie nicht verfügbar sind und Sie administrative Rechte haben, können Sie Apache neu kompilieren und dabei diese Module einbinden. Dies kann entweder dadurch getan werden, daß die entsprechenden Zeilen in der Konfigurationsdatei einkommentiert werden, or indem man configure (1.3 oder neuer) die Argumente `--enable-module=expires` und `--enable-module=headers` mitgibt. Ziehen Sie die Datei INSTALL zu Rate, die Sie in der Apache-Distribution finden.

Sobald Sie einen Apache mit den entsprechenden Modulen haben, können Sie mod_expires verwenden, um anzugeben, wann Repräsentationen ablaufen sollen. Die können Sie entweder in .htaccess-Dateien oder in der access.conf des Servers tun. Sie können das Ablaufen entweder auf dem Zugriffszeitpunkt oder dem Zeitpunkt der letzten Änderung basieren lassen, und es auf einen Dateityp anwenden oder als Standard einstellen. Lesen Sie die [Dokumentation des Moduls](https://www.apache.org/docs/mod/mod_expires.html) für weitere Informationen und sprechen Sie bei Problemen mit Ihrem örtlichen Apache-Guru.

Um `Cache-Control`-Header anzuwenden, müssen Sie das mod_headers-Modul verwenden, das Ihnen erlaubt, beliebige HTTP-Header für eine Ressource anzugeben. Schauen Sie auch in die [mod_headers-Dokumentation](https://www.apache.org/docs/mod/mod_headers.html).

Hier ist eine Beispiel-.htaccess-Datei, die den Gebrauch einiger Header vorführt.

.htaccess-Dateien erlauben es Webautoren, Kommandos zu verwenden, die normalerweise nur in Konfigurationsdateien auftreten. Diese beeinflussen die Inhalte des Verzeichnisses, in denen sie sich befinden, sowie dessen Unterverzeichnisse. Sprechen Sie mit Ihrem Server-Administrator, um herauszufinden, ob sie aktiviert sind.

```
#### mod_expires aktivieren
ExpiresActive On
####  .gif's laufen einen Monat nach dem letzten Zugriff ab
ExpiresByType image/gif A2592000
#### Alles andere läuft einen Tag nach der letzten Änderung ab
#### (hier wird die alternative Syntax verwendet)
ExpiresDefault "modification plus 1 day"
#### Einen Cache-Control-Header auf index.html anwenden
<Files index.html>
Header append Cache-Control "public, must-revalidate"
</Files>
```

Beachten Sie, daß mod_expires automatisch einen passenden `Cache-Control: max-age`-Header berechnet und einfügt.

Die Konfiguration von Apache 2 ähnelt sehr der von Apache 1.3, lesen Sie die 2.2er Dokumentation zu [mod_expires](https://httpd.apache.org/docs/2.2/mod/mod_expires.html) und [mod_headers](https://httpd.apache.org/docs/2.2/mod/mod_headers.html) für weitere Informationen.

### Microsoft IIS

[Microsofts](https://www.microsoft.com/) Internet Information Server macht es sehr leicht, Header auf einigermaßen flexible Art zu setzen. Beachten Sie, daß dies nur in Version 4 des Servers möglich ist, die nur unter Windows NT Server läuft.

Um Header für einen Bereich einer Webpräsenz zu festzulegen, wählen Sie diesen Bereich in “Administration Tools” und öffnen Sie dessen Eigenschaften. Nachdem Sie das Tab „HTTP Headers“ angewählt haben, sollten Sie zwei interessante Bereiche sehen: „Enable Content Expiration“ und „Custom HTTP headers“. Der erste sollte selbsterklärend sein, und der zweite kann genutzt werden, um Cache-Control-Header anzuwenden.

Lesen Sie den ASP-Abschnitt weiter unten, um Informationen zu erhalten, wie Sie Header in den Active Server Pages setzen können. Es ist auch möglich, Header aus ISAPI -Modulen heraus zu setzen; schauen Sie für Details ins MSDN.

### Netscape/iPlanet Enterprise Server

In der Version 3.6 bietet der Enterprise Server keine offensichtliche Möglichkeit, Expires-Header zu setzen. Er hat jedoch Funktionalität aus HTTP 1.1 seit Version 3.0 unterstützt. Das bedeutet, daß HTTP-1.1-Caches (Proxy und Browser) die Cache-Control-Einstellungen, die Sie vornehmen, ausnutzen können.

Um Cache-Control-Header zu nutzen, wählen Sie „Content Management | Cache Control Directives“ im Administrations-Server. Dann wählen Sie das Verzeichnis, in dem Sie die Header setzen wollen, indem Sie den „Resource Picker“ verwenden. Nachdem Sie die Header gesetzt haben, klicken Sie „OK“. Für weitere Informationen schauen Sie ins Handbuch des NES.

## Implementierungshinweise für serverseitiges Skripten

Weil der Augenmerk beim serverseitigen Skripten auf dynamischen Inhalten liegt, führt es nicht zu besonders cachebaren Seiten, selbst wenn der Inhalt gecachet werden könnte. Wenn sich Ihr Inhalt häufig ändert, aber nicht bei jedem Seitenbesuch, ziehen Sie in Betracht, einen `Cache-Control: max-age`-Header zu setzen; die meisten Benutzer greifen auf Seiten in relativ kurzer Zeit erneut zu. Beispielsweise müssen Benutzer, wenn sie auf den „Zurück“-Button klicken und keine Validatoren oder Freshness-Information verfügbar sind, warten, bis die Seite vom Server erneut heruntergeladen worden ist, um sie sehen zu können.

<aside>
Denken Sie daran, daß es möglicherweise einfacher ist, HTTP-Header mittels des Webservers zu setzen, als dies in der Skriptsprache zu tun. Versuchen Sie beides.
</aside>

### CGI

CGI-Skripte sind eine der beliebtesten Arten, Inhalte zu erzeugen. Sie können HTTP-Antwort-Header leicht anhängen, indem Sie sie hinzufügen, bevor Sie den Body senden. Die meisten CGI-Implementierungen verlangen das bereits für den Content-Type-Header von Ihnen. Ein Beispiel in Perl:

``` perl
#!/usr/bin/perl
print "Content-type: text/html\n";
print "Expires: Thu, 29 Oct 1998 17:04:19 GMT\n";
print "\n";
#### Der Body-Inhalt folgt...
```

Weil dies alles reiner Text ist, können Sie die Expires- und andere Zeit-bezogene Header leicht mit eingebauten Funktionen erzeugen. Es ist sogar noch einfacher, wenn sie `Cache-Control: max-age` verwenden.

```
print "Cache-Control: max-age=600\n";
```

Dies sorgt dafür, daß das Skript für zehn Minuten nach der Anforderung gecachet werden kann, so daß der Benutzer die Anforderung nicht erneut schickt, wenn er den “Zurück”-Button anklickt.

Die CGI-Spezifikation macht Anforderungs-Header, die der Client sendet, auch in der Umgebung des Skripts verfügbar; jeder Header hat dabei seinem Namen „HTTP_“ vorangestellt. Wenn ein Client eine `If-Modified-Since`-Anforderung stellt, wird dies also folgendermaßen auftauchen:

```
HTTP_IF_MODIFIED_SINCE = Fri, 30 Oct 1998 14:19:41 GMT
```

Beachten Sie auch die [cgi_buffer-Bibliothek](https://github.com/nigelhorne/CGI-Buffer), die sich für Perl- und Python-CGI-Skripte mit einem einzeiligen Include automatisch um ETag-Generierung und -Validation, `Content-Length`-Erzeugung und gzip-Inhaltskodierung kümmert. Die Python-Version kann auch benutzt werden, um damit beliebige CGI-Skripte zu wrappen.

### Server Side Includes

SSI (oft mit der Dateierweiterung .shtml benutzt) sind eine der ersten Arten gewesen, auf die Webautoren in die Lage versetzt wurden, dynamische Inhalte in Seiten einzufügen. Indem sie besondere Tags in den Seiten benutzten, war eine beschränkte Art von Skripting in HTML möglich.

Die meisten SSI-Implementierungen setzen keine Validatoren und sind damit nicht cachebar. Die Implementierung des Apache erlaubt Benutzern jedoch festzulegen, welche SSI-Dateien gecachet werden können, indem sie die Gruppen-Ausführungsrechte der entsprechenden Dateien setzen und die Anweisung `XbitHack full` verwenden. Für weitere Informationen lesen Sie bitte die [mod_include-Dokumentation](https://httpd.apache.org/docs/current/mod/mod_include.html).

### PHP

PHP ist eine serverseitige Skriptsprache wie SSI, mit der Skripte im HTML-Code einer Webseite eingebettet werden können, nur mit viel mehr Möglichkeiten. PHP kann als CGI-Skript auf jedem beliebigen Webserver (Unix oder Windows) oder als Apache-Modul verwendet werden.

Standardmäßig wird Repräsentationen, die von PHP verarbeitet worden sind, keine Validatoren zugeordnet, weshalb sie uncachebar sind. Entwickler können jedoch HTTP-Header mittels der `Header()`-Funktion setzen.

Zum Beispiel lassen sich so ein Cache-Control-Header und ein Expires-Header, der drei Tage in die Zukunft verweist, erzeugen:

``` php
<?php
Header("Cache-Control: must-revalidate");
$offset = 60 * 60 * 24 * 3;
$ExpStr = "Expires: " . gmdate("D, d M Y H:i:s", time() + $offset) . " GMT";
Header($ExpStr);
?>
```

Denken Sie daran, daß die Funktion `Header()` vor aller anderen Ausgabe kommen **muß.**

Wie Sie sehen können, müssen Sie die HTTP-Zeitangabe für einen Expires-Header von Hand erzeugen; PHP bietet Ihnen keine Funktion dafür an (auch wenn neuere Versionen es erleichtert haben, lesen Sie die [Dokumentation zu PHPs date](https://www.php.net/manual/de/function.date.php)). Natürlich ist es leicht, einen `Cache-Control: max-age`-Header zu setzen, was in den meisten Situationen genausogut ist.

Für weitere Informationen lesen Sie bitte den [Handbucheintrag zu header](https://www.php.net/manual/de/function.header.php).

Schauen Sie sich auch die [cgi_buffer-Bibliothek](https://github.com/nigelhorne/CGI-Buffer) an, die ETag-Generierung und -Validation, `Content-Length`-Erzeugung und gzip-Inhaltskodierung für PHP-Skripte mit einem einzeiligen Include erledigt.

### Cold Fusion

[Cold Fusion](https://www.adobe.com/products/coldfusion-family.html) von Macromedia ist ein kommerzielles, serverseitiges Skriptsystem mit Unterstützung mehrerer Webserver für Windows, Linux und verschiedenen Linux-Arten.

Cold Fusion macht das Setzen beliebiger HTTP-Header durch das `CFHEADER`-Tag relativ leicht. Leider führt ihr Beispiel zum Setzen eines Expires-Headers, wie unten zu sehen, etwas in die Irre.

```
<CFHEADER NAME="Expires" VALUE="#Now()#">
```

Es funktioniert nicht so, wie Sie meinen könnten, da die Zeitangabe (in diesem Fall: wann die Anforderung gestellt wurde) nicht in eine in HTTP gültige Zeitangabe umgewandelt wird; stattdessen wird sie als eine Repräsentation von Cold Fusions Datums/Zeit-Objekt ausgegeben. Die meisten Clients werden einen solchen Wert entweder ignorieren oder ihn zu einem Standardwert wie den 1. Januar 1970 umwandeln.

Cold Fusion bietet jedoch auch eine Funktion zur Datumsformatierung an, die die Aufgabe erledigt: `GetHTTPTimeString`. In Kombination mit `DateAdd` ist es leicht, Expires-Zeitangaben zu setzen. Hier setzen wir einen Header, der angibt, daß Repräsentationen der Seite in einem Monat ablaufen sollen:

```
<cfheader name="Expires" value="#GetHttpTimeString(DateAdd('m', 1, Now()))#">
```

Sie können auch das `CFHEADER`-Tag verwenden, um `Cache-Control: max-age` und andere Header zu setzen.

Denken Sie daran, daß Webserver-Header in einigen Installationsarten von Cold Fusion (so wie CGI) durchgeschleift werden; prüfen Sie Ihre Installation, ob Sie das ausnutzen können, indem Sie Header im Server setzen, statt in Cold Fusion.

### ASP und ASP.NET

Active Server Pages, in IIS eingebaut und auch für andere Webserver verfügbar, erlauben Ihnen ebenfalls, HTTP-Header zu setzen. Beispielsweise können Sie die Eigenschaften des Response-Objekts nutzen, um eine Ablaufzeit zu setzen

```
<% Response.Expires=1440 %>
```

und so die Anzahl der Minuten von der Anforderung an festzulegen, nach der die Repräsentation veraltet.

`Cache-Control`-Header können folgendermaßen gesetzt werden:

```
<% Response.CacheControl="public" %>
```

In ASP.NET ist `Response.Expires` veraltet, die richtige Art, cachebezogene Header zu setzen, geht mit `Response.Cache`:

```
Response.Cache.SetExpires ( DateTime.Now.AddMinutes ( 60 ) ) ;
Response.Cache.SetCacheability ( HttpCacheability.Public ) ;
```

Wenn Sie HTTP-Header aus ASP heraus setzen, stellen Sie sicher, daß Sie entweder die Response-Methodenaufrufe vor jegliche HTML-Generierung stellen, oder daß Sie `Response.Buffer` nutzen, um die Ausgabe zu puffern. Beachten Sie auch, daß einige Versionen des IIS einen `Cache-Control: private`-Header für ASPs standardmäßig setzen, und diese ASPs public deklariert werden müssen, um von gemeinsamen Caches gecachet werden zu können.

Schauen Sie für weitere Informationen in die [MSDN-Dokumentation](https://docs.microsoft.com/de-de/aspnet/core/?view=aspnetcore-6.0).

## Verweise und weitere Informationen

* [HTTP-1.1-Spezifikation](http://www.ietf.org/rfc/rfc2616.txt)

  Die HTTP-1.1-Spezifikation enthält viele Erweiterungen, um Seiten cachebar zu machen und ist die authoritative Anleitung, um das Protokoll zu implementieren. Schauen Sie in die Abschnitte 13, 14.9, 14.21 sowie 14.25.

* [Web-Caching.com](http://www.web-caching.com/)

  Eine hervorragende Einführung in Caching-Konzepte, mit Verweisen auf andere Online-Ressourcen.

* [On Interpreting Access Statistics](http://www.goldmark.org/netrants/webstats/)
  
  Jeff Goldbergs informative Tirade, warum Sie sich nicht auf Zugriffsstatitiken und Besucherzähler verlassen sollten.

* [REDbot](https://redbot.org/)
  
  Untersucht HTTP-Ressourcen, um festzustellen, wie sie mit Webcaches interagieren und allgemein, wie gut sie das Protokoll nutzen.

* [cgi_buffer-Bibliothek](https://github.com/nigelhorne/CGI-Buffer)

  Einzeiliger Include in Perl-CGI, Python-CGI und PHP-Skripten, der `ETag`-Erzeugung und -Validation, `Content-Length`-Generierung und gzip-Inhaltskodierung automatisch handhabt — auf korrekte Art. Die Python-Version kann auch als Wrapper um beliebige CGI-Skripte verwendet werden.

## Über dieses Dokument

Dieses Dokument unterliegt dem gemeinsamen Urheberrecht von Mark Nottingham <mnot@pobox.com> (© 1998-2013) für den Inhalt und Thomas Hühn <mail@thomas.huehn.de> (© 2010-2014) für die deutsche Übersetzung. Dieses Werk ist unter einer Creative-Commons-Lizenz, der [Creative Commons Attribution-Noncommercial-No Derivative Works 3.0 Unported License](https://creativecommons.org/licenses/by-nc-nd/3.0/), lizenziert.

Wenn Sie dieses Dokument spiegeln, senden Sie bitte eine E-Mail an Thomas Hühn <mail@thomas.huehn.de>, so daß Sie über Aktualisierungen unterrichtet werden können.

Alle Markenzeichen darin sind von ihren jeweiligen Inhabern geschützt.

Auch wenn der Autor glaubt, daß die Inhalte zum Zeitpunkt der Veröffentlichung akkurat sind, wird keine Haftung für sie, ihre Anwendung oder jegliche Folgen daraus übernommen. Falls Sie irgendwelche Falschdarstellungen, Fehler oder andere Notwendigkeiten für eine Klärung finden, kontaktieren Sie den Autor bitte umgehend.

Die jüngste Fassung dieses Dokuments kann stets unter https://www.thomas-huehn.de/2010/02/caching-tutorial/ abgerufen werden.

Das englische Original finden Sie unter http://www.mnot.net/cache_docs/.

Übersetzungen in weitere Sprachen sind für das [Chinesische](https://www.chedong.com/tech/cache_docs.html), das [Tschechische](https://www.jakpsatweb.cz/clanky/caching-tutorial-czech-translation.html) sowie das das [Französische](https://www.mnot.net/cache_docs/index.fr.html) verfügbar.
