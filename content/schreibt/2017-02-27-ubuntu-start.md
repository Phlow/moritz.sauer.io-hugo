---
date                : 2017-02-27
subtitle            : 'Linux Experimente'
title               : 'Erfahrungsbericht Ubuntu'
image:
    title: /img/schreibt/ubuntu-logo.png
schlagwort          : linux
---
Megakonzerne wie Apple sind mir unsympathisch und werden immer unsympathischer. Ich nutze seit Jahren mein erstes und solide arbeitendes Macbook Pro. Ich bin mit diesem Computer sehr zufrieden, bis auf die lächerlichen zwei USB-Schnittstellen. Aber während Apple sich weigert in Europa Steuern und hinterzogenes Geld zu bezahlen, Apple neuere Computer immer weniger für Professionelle produziert, die erst mit zig Kabeladaptern funktionieren, habe ich immer mehr das Gefühl, dass man den Konzern boykottieren sollte. Ist da [Linux]({{< ref "/schlagwort/linux/" >}}) bzw. Ubuntu eine Alternative? Ein Erfahrungsbericht meiner ersten Schritte.
<!--more-->

Nachdem sich Ubuntu ohne Probleme über einen USB-Stick auf meinem alten Lenovo T60 selbst installiert hat, habe ich zum ersten einmal Amazon aus der Seitenleiste gelöscht. Ich bin immer noch überrascht, wie nahtlos die Installation vor sich ging. Auch die Verschlüsselung des Computers per Ubuntu ist super einfach und die Installationsroutine war einwandfrei. Eine wichtige Erfahrung, wie ich finde…

Jetzt geht es an die Anpassung der Maschine an meine Bedürfnisse…

## Atom: Ein vernünftiger moderner Texteditor

{{< img src="/img/schreibt/atom_screenshot.png" alt="Atom: Ein vernünftiger moderner Texteditor" >}}

Als nächstes habe ich mir dann erst einmal einen vernünftigen Texteditor heruntergeladen: [Atom.io](https://atom.io). Installiert habe ich Atom auf meiner alten 32 Bit-Maschine mit drei Befehlen, die ich in das Terminal kopiert habe, das ich mit STRG+ALT+t geöffnet habe. Die [drei Befehle für die Installation](https://medium.com/how-to-install/how-to-install-atom-editor-in-ubuntu-14-04-1c761af5e2ba#.ym5bdky8c) habe ich nach ein wenig googlen gefunden habe.

Zuerst musste ich leider wieder erst googlen, um herauszufinden, dass ich Befehle nur über STRG+Umschalt+C und STRG+Umschalt+V in das Terminal kopieren kann. Erste kleine Nervigkeiten.

~~~
sudo add-apt-repository ppa:webupd8team/atom
sudo apt-get update
sudo apt-get install atom
~~~

## Lieblingsschrift fürs Coden installieren

Typografie ist mir sehr wichtig. Darum habe ich mir für das Terminal und Atom anschließend erst einmal die liebgewonne [Inconsolata-Schrift](https://fonts.google.com/specimen/Inconsolata) heruntergeladen. Es ist meine Lieblings Monospace-Schrift für die Programmierung. Und Schriften installiert man, wie 

## Little fluffy Cloud – Dropbox & Google Drive

Viele Dokumente speichere ich in der Cloud ab. iCloud auf meinem Mac finde ich total nervig und es fühlt sich immer wieder unfertig an. Darum nutze ich seit Jahren einen kostenlosen Mix aus Dropbox und Google Drive. Die Cloud hilft schon enorm bei der Koordination und dem Teilen von Dateien. Nebenbei sichert Sie auch die Daten, was nicht schlecht ist.

Was ich erstaunlich schlecht fand – auch wenn ich es verstanden habe – war die [Anleitung auf der Dropbox-Website](https://www.dropbox.com/de/install-linux). Ein normaler Anwender wüsste glaube ich nicht, was ein _Daemon_ ist, und so richtig habe ich den Mix aus Terminaleingabe und Download auch nicht verstanden. Erfolgreich war die Installation scheinbar trotzdem, denn gerade synchronisiert sich der Dropbox-Ordner.

Erstaunlich ist dahingegen, dass Google Drive keine Anwendung selbst anbietet. Es gibt zwar einen Weg, aber der ist mir jetzt erst einmal zu kompliziert. Dann muss ich eben über Firefox an die Daten ran.

## Daten und Ordner verschlüsseln mit Cryptomator

Cryptomator ist mir sehr ans Herz gewachsen. Es funktioniert auf meinem Mac hervorragend, ist einfach zu bedienen und verschlüsselt Ordner ordentlich. So ermöglicht Cryptomator z.B. Daten auf Dropbox zu lagern, die verschlüsselt sind. So nutzt man die Cloud und trotzdem kommt niemand an die Daten heran, da man Sie vorher verschlüsselt. Will ich die Daten öffnen, muss ich zuerst Cryptomator starten und den _Tresor_ öffnen.

~~~
sudo add-apt-repository ppa:sebastian-stenzel/cryptomator
sudo apt-get update
sudo apt-get install cryptomator
~~~

Nach den obigen Befehlen ist Cryptomator installiert und funktioniert einwandfrei.

## Was ich als nächstes brauche…

Ich liebe Tastaturkürzel, ein Programm die Texteingabe überwacht und aus Kürzeln wie _vgm_ _Viele Grüße, Moritz_ macht und einen Zwischenspeichermanager, der mir mehr erlaubt mehr als nur das letzte gemerkte Objekt, Textschnipsel, etc. zu kopieren bzw. einzusetzen.

Das spare ich mir aber jetzt erst einmal für den nächsten Schritt auf…

Teil meiner kleinen [Linux Serie]({{< ref "/schlagwort/linux/" >}}).
