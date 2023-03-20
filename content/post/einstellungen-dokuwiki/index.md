---
title: "Einstellungen für eine neue DokuWiki-Installation"
description: Konfiguration fürs DokuWiki
date: 2018-08-12
lastmod: 2019-01-01
tags: ['Software']
---
DokuWiki ist ein sehr feines, no-nonsense Wikisystem. Es bietet viele Features, sieht okay aus und braucht keine Datenbank (was das [Backup]({{< relref "backup-dokuwiki-tarsnap" >}}) trivial macht).

Allerdings gefallen mir die Werkseinstellungen nicht sonderlich. Daher dokumentiere ich hier, was ich bei einer frischen Installation ändern möchte.

|Einstellung|Wert|
|---|---|
|showuseras|username|
|useheading|1|
|relnofollow|false|
|indexdelay|60|
|mailguard|none|
|sitemap|1|
|rss_type|RSS 2.0|
|rss_linkto|the current page|
|rss_content|Full HTML page content|
|rss_media|pages|
|userewrite|.htaccess|
|useslash|true|
|sepchar|–|

Und natürlich nicht vergessen, im Webserver die Rewrites zu konfigurieren!
