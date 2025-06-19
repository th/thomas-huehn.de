---
title: Backup für DokuWiki mit Tarsnap
description: Wiem an ein DokuWiki backupt
date: 2019-02-07
lastmod: 2019-10-09
tags:
  - Software
  - Wiki
aliases:
  - /2019/02/backup-dokuwiki-tarsnap/
---
Mein [DokuWiki](/einstellungen-dokuwiki/) wird jede Nacht durch dieses Skript gebackuppt, wobei Verzeichnisse ausgeschlossen sind, die sich permanent ändern:

```bash
#!/bin/sh
/home/username/tarsnap/inst/bin/tarsnap -c \
        -f username-$(date +%Y-%m-%d_%H-%M-%S) \
        --exclude cache \
        --exclude index \
        --exclude locks \
        --exclude tmp \
        /var/www/virtual/username/html/data \
        /var/www/virtual/username/html/conf
```

Und dann von crontab aus aufrufen.