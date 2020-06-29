---
layout              : post
subtitle            : Linux Tipp
title               : "Google Fonts & Microsoft-Schriften für Linux installieren"
image:
    title           : /img/schreibt/linux-schriften-installieren.jpg
    caption         : Raphael Schaller raphaelphoto.ch
comments            : true
schlagwort          : linux
date                : 2017-03-10
---
Die Installation von Schriften bei [Linux]({{< ref "/schlagwort/linux/" >}}) ist wunderbar unkompliziert. Ein paar Befehle in das Terminal kopiert und schon stehen die Standardschriften von Microsoft und sämtliche Google Fonts zur Verfügung. Eine Kurzanleitung für die schnelle Installation von ca. 900 professionellen Schriften.
<!--more-->

Bei der Installation von Schriften spielt das Terminal seine Mächtigkeit aus: Es lädt Schriften herunter, entpackt die Archive und verschiebt die Schriften an die richtige Stelle. Das nenne ich Komfort.

**Hinweis:** Ganz am Ende gibt es ein Skript, um alle hier vorgestellten Fonts in einem Aufwasch zu installieren.

## Alle Google Fonts in einem Rutsch per Skript installieren

Eines meiner – wenn nicht das – Lieblingsprojekt von Google ist [Google Fonts](https://fonts.google.com/), dass professionelle Open Source-Schriften zur Verfügung stellt. Zur Zeit sind es 818 Schriftfamilien. Wobei mehrere Schriften gleich mit mehreren Schriftschnitten daherkommen. Dank der offenen Lizenzbedingungen stehen [alle Schriften auf GitHub](https://github.com/google/fonts) in Form eines [Schriften-ZIP](https://github.com/google/fonts/archive/master.zip) zur Verfügung.

Mit dem kleinen aber feinen Skript, dass ich unter [»Automatically Install All The Google Web Fonts In Ubuntu Using A Script«](http://www.webupd8.org/2011/01/automatically-install-all-google-web.html) gefunden habe, lädt man sich per Terminal alle Schriften herunter und installiert sie in einem Durchgang. Genial.

~~~
cd && wget https://raw.githubusercontent.com/hotice/webupd8/master/install-google-fonts
chmod +x install-google-fonts
./install-google-fonts
~~~

## Microsoft-Schriften wie Georgia, Times New Roman installieren

Grundlegende Schriften von Microsoft, wie die wunderbare Georgia bietet Microsoft unentgeltlich an. Um die Schriften zu installieren, musst Du nur den Lizenzbedingungen zustimmen. Dazu aktiviert man mittels Tab zur Schaltfläche _OK_ und drückt die Eingabetaste. Nach Aktivierung der Schaltfläche _Ja_, bestätigt man noch einmal per Tabulator-Taste, dass man EULA akzeptiert. Dazu drückst Du noch einmal die Eingabetaste. Hier der Befehl.

~~~
sudo apt-get install ttf-mscorefonts-installer
~~~

## Noch mehr Schriften für Linux

Zwei wunderbare Serifenschriften solltest Du Dir noch anschauen: **Linux Libertine** und **EB Garamond**.

~~~
sudo apt-get install ttf-linux-libertine
sudo apt-get install fonts-ebgaramond fonts-ebgaramond-extra
~~~

## Und jetzt alle Schriften auf einmal

1. Öffne Dein Terminal.
2. Wechsle auf Deinen Schreibtisch.
3. Schnappe Dir mit wget das Installationsskript: `wget https://gist.githubusercontent.com/Phlow/94ebb77a6b6cc6dccd3451436be43096/raw/2fee13d632dec696483d42f84c734e37fe17577a/schrifteninstallieren.sh`
4. Gebe dem Skript Ausführungsrechte `chmod +x schrifteninstallieren.sh`.
5. Starte das Skript mit `./schrifteninstallieren.sh`.
6. Genieße die Magie und bestätige gegen Ende die EULA von Microsoft.
7. Lösche auf Deinem Schreibtisch die ZIP-Datei und das Skript.

~~~
#!/bin/bash
# Google Fonts
cd && wget https://raw.githubusercontent.com/hotice/webupd8/master/install-google-fonts
chmod +x install-google-fonts
./install-google-fonts
# Linux Libertine und EB Garamond
sudo apt-get install ttf-linux-libertine
sudo apt-get install fonts-ebgaramond fonts-ebgaramond-extra
sudo apt-get install ttf-mscorefonts-installer
~~~
