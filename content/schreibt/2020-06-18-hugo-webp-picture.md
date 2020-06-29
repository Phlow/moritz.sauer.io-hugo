---
title               : "Hugo: Markdown Render Hooks + webp = Noch schnellere Websites"
date                : 2020-06-18T15:25:03+02:00
schlagwort          :
    - webdesign
    - hugo
---
Mit Hugo Markdown Render Hooks generiert man aus einfachem Markdown inviduelles HTML. Das ermöglicht den Einsatz von webp-Bildern plus `<picture>`.

Meine Websites [Phlow.de](https://phlow.de/) und [moritz.sauer.io](https://moritz.sauer.io/) baue ich mit [Hugo]({{< ref "/schlagwort/hugo" >}}). Die Beiträge verfasse ich in Markdown und seit Längerem wollte ich die Website beschleunigen, indem ich [webp-Bilder](https://web.dev/serve-images-webp/) nutze. Und dafür gibt es jetzt eine einfache Lösung.

{{< toc >}}

Das [webp-Format](https://developers.google.com/speed/webp) verkleinert Bilder in der Dateigröße besser als JPG. Subjektiv sehen die Bilder aber gleich scharf aus. **Das Problem für die Verwendung von webp**: nicht alle Browser unterstützen das Format.

Das Problem löst man leicht mit HTML, denn dafür steht das [`<picture>`-Tag](https://developer.mozilla.org/de/docs/Web/HTML/Element/picture) zur Verfügung. Dieses erlaubt den Einsatz von Bildern für verschiedene Bildschirmgrößen **und** lässt den Einsatz von Dateiformaten zu bzw. überlässt dem Browser die Wahl. Das sieht dann so aus:

~~~
<picture>
  <source type="image/webp" srcset="bild.webp">
  <source type="image/jpeg" srcset="bild.jpg">
  <img src="bild.jpg" alt="" />
</picture>
~~~

Während Safari weiterhin das _jpg_-Bildformat bevorzugt, nutzen Chrome und Firefox die _webp_-Variante.

## webp-Bilder aus JPG und PNG-Bildern generieren

_webp_-Bilder generiert man einfach über das [Mac Terminal](https://phlow.de/magazin/terminal/). Damit das auf meinem Mac funktioniert, habe ich mit _homebrew_ einfach das Werkzeug installiert:

~~~
brew install webp
~~~

Anschließend öffne ich den Ordner mit den Bildern im Terminal und zwei Schleifen für _jpg_- und _png_-Bilder konvertieren mir sämtliche Bilder im Ordner:

~~~
for i in *.jpg; do cwebp -q 90 $i -o "${i%.*}.webp"; done
for i in *.png; do cwebp -q 90 $i -o "${i%.*}.webp"; done
~~~

## Vergleich komprimierter Bilder mit jpg, guetzli-jpg und webp

Das folgende Beispiel illustriert, wie die Bilder mit den Maßen 1600 × 1067 schrumpfen. Exemplarisch habe ich [ein Bild von Unsplash](https://unsplash.com/photos/6u0xv4j6WKI) runtergeladen und auf die Pixelmaße 1600 × 1067 verkleinert. Dann habe ich das Bild mit dem JPG-Komprimierer [guetzli](https://github.com/google/guetzli/) verkleinert und dann noch mit _webp_. Die Ergebnisse kannst Du über die folgenden Links öffnen und vergleichen.

* Original mit 288.482 Byte [webp-hugo-test-1600x1067.jpg](/img/schreibt/webp-hugo-test-1600x1067.jpg)
* guetzli-JPG 189.502 Byte [webp-hugo-test-1600x1067-guetzli.jpg](/img/schreibt/webp-hugo-test-1600x1067-guetzli.jpg)
* webp mit 118.800 Byte[webp-hugo-test-1600x1067.webp](/img/schreibt/webp-hugo-test-1600x1067.webp)

### Original JPG-Bild

<img src="/img/schreibt/webp-hugo-test-1600x1067.jpg" alt="">

### JPG mit guetzli Qualität 85 optimiert

<img src="/img/schreibt/webp-hugo-test-1600x1067-guetzli.jpg" alt="">

### Bild mit webp und Qualität 80 optimiert

**Hinweis:** Wenn Du ältere Browser nutzt oder Safari (Stand 2020-06-18), dann wird Dir das Bild nicht angezeigt.

<img src="/img/schreibt/webp-hugo-test-1600x1067.webp" alt="">


## Hugo Markdown Render Hooks übernehmen die Arbeit

Beiträge schreibt man in Hugo in Markdown. Die Syntax für ein Bild mit Markdown lautet schlicht:

~~~
![Bildtitel](bild.jpg)
~~~

Das Problem ist: _Und wie entsteht daraus das `<picture>`-Tag?_

Dafür habe ich heute in den Hugo-News eine für mich neue Funktion entdeckt: die [Markdown Render Hooks](https://gohugo.io/getting-started/configuration-markup#markdown-render-hooks). Über diese _hooks_ verändert man die Ausgabe der  Markdown-Befehle. Anstelle eines normalen HTML-Bildbefehls realisiert man komplexeres HTML.

Mit einem _hook_ erstellt man zuerst ein Rendering-Template, dass der Markdown-Parser Goldmark benutzt, wenn er z.B. ein Bild entdeckt. Diese Rendering-Templates legt man z.B. so ab:

<pre><code>
.
├── _default
│   ├── <mark>_markup</mark>
│   │   └── <mark>render-image.html</mark>
│   ├── baseof.html
│   ├── blog_frontpage.html
...
</code></pre>

## `substr` ersetzt die _jpg_-Endung mit _wepb_

In meinem Fall sieht der Code von _render-image.html_ so aus:

~~~
<picture>
  <source type="image/webp" srcset="{{ substr .Destination 0 -4 | safeURL }}.webp">
  <source type="image/jpeg" srcset="{{ .Destination | safeURL }}">
  <img src="{{ .Destination | safeURL }}" alt="{{ .Text }}" {{ with .Title}} title="{{ . }}"{{ end }} />
</picture>
~~~

Der kleine Trick ist in `substr` versteckt. Mit der [substr-Funktion](https://gohugo.io/functions/substr/) manipuliert man einen String. In diesem Fall schnappt sich `substr` den von Goldmark übergebenen Link, löscht die letzten drei Zeichen – hier _jpg_ – und hängt anschließend das _wepb_ dran.

Das feine an der ganzen Affäre: Beiträge schreibt man einfach, setzt ein Bild ein und Hugo übernimmt den Rest. Natürlich darf man nicht vergessen die _webp_-Bilder zu generieren.





