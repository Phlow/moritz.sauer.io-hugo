---
title               : 'Hugo Website Generator – Hilfreiche Code-Snippets'
date                : "2020-05-01T14:39:29+02:00"
schlagwort         :
    - hugo
    - webdesign
---
[Hugo]({{< ref "/schlagwort/hugo" >}}) ist ein [Static Website Generator](https://www.staticgen.com/), der zahlreiche meiner Websites baut – unter anderem [Phlow.de](https://phlow.de/) und [Moritz.Sauer.io](https://moritz.sauer.io/). An dieser Stelle sammele ich zahlreiche Bausteine für die Web-Entwicklung.

{{< toc >}}

Die Verwendung der Template-Sprache Go und auch die Hugo-Programmierung ist nicht ganz leicht. Ich stolper immer wieder über IF-Abfragen oder Schleifen mit `range`. Darum diese Sammlung…

## Die wichtigsten Kommandos für das Terminal

### Hugo Befehle

`hugo new site ORDNERNAME`
: Legt ein neues Hugo-Projekt an

`hugo new theme [name]`
: Legt ein fast leeres neues Theme an

`hugo server`
: Startet den Hugo-Live-Server für die Entwicklung

`hugo server --watch --port 4000 --baseURL "" --disableFastRender`
: Startet den Hugo-Live-Server auf Port 4000 und baut dank `--disableFastRender` bei der Änderungen von Dateien komplett alles neu.

`hugo config`
: Listet alle gesetzten Konfigurationsparameter auf

`hugo -t themename`
: Startet Hugo mit dem Theme _themename_

In der Dokumentation findest Du die Übersicht 
[Aller Befehle der Hugo CLI](https://gohugo.io/getting-started/usage/).

### Hugo aktualisieren, upgraden, updaten…

Um Hugo mit [homebrew](https://phlow.de/magazin/terminal/homebrew/) zu aktualisieren, gibst Du folgendes ein. Dabei aktualisierst Du zuerst homebrew mit

~~~
brew update
~~~

Und nimmst anschließend das Upgrade für Hugo vor.

~~~
brew upgrade hugo
~~~


## Struktur eines Hugo-Projektes

    .
    ├── archetypes
    ├── assets
    ├── config
    ├── content
    ├── data
    ├── layouts
    ├── static
    └── themes

archetypes
: Vorlagen für neue Beiträge, die Du mit `hugo new` kreieren kannst.

assets
: Beinhaltet Dateien, die Hugo verarbeiten soll, z.B. *.scss*, *.postcss*,…

config
: Ort für die Konfigurationsdatei(en)

content
: Ordner für alle Inhalte.

data
: Hugo verarbeitet auf Wunsch Daten, die in Webseiten eingebunden werden sollen.

layouts
: Vorlagen für Deine Webseiten.

static
: In diesen Ordner gehören Bilder, Javascripte, Fonts, Mediendateien,…

## Hugo Standard-Variablen

- {{ .Summary }}
- {{ .Content }}
- {{ .Title }}
- {{ .RelPermalink }}
- {{ .Permalink }}
- .Params.param-name

### Eigene Variablen erstellen

{{ $myVar := value }} // assigns value to $myVar
{{ $myVar }} // prints $myVar

### Globale Variablen erstellen

in your config.toml or theme.toml
[params]
myvariable = "testing 123"

[params.general]
mysubvariable = "more tests"
in your theme file.
{{ .Site.Params.myvariable }}
{{ .Site.Params.general.mysubvariable }}

## if-Abfragen mit Hugo

Bei meiner [Webdesign]({{< ref "/schlagwort/webdesign" >}})-Arbeit mit dem [Website Generator Hugo]({{< ref "/schlagwort/hugo" >}}) stolpere ich immer wieder über die Konstruktion von _if_- oder _where_-Abfragen. Hier zahlreiche funktionierende Beispiele…

### Wenn _in .Section_, dann…

~~~
{{ if (eq .Section "pages") }}
<!-- wenn in Section pages -->
{{ end }}
~~~

### Wenn Parameter 1 _oder_ 2 vorhanden ist, dann…

~~~
{{ if or .Title .Content }}
<!-- Ausgabe wenn in Section pages -->
{{ end }}
~~~

### Wenn Wert _nicht_ existiert, dann…

~~~
{{ if (not (isset .Params "some_variable")) }}
{{ end }}
~~~

### Wenn in Kategorie X, dann…

~~~
{{ if eq .Page.Params.Categories "seminare" }}
<!-- Ausgabe wenn in Kategorie seminare -->
{{ end }}
~~~

### Wenn Schlagwort, dann bitte nur das erste ausgeben

~~~
{{ if isset .Params "schlagwort" }}
{{ $tag := (index ( .Params.schlagwort ) 0) }}
 <a href="{{ "/schlagwort/" | relLangURL }}{{ $tag | urlize }}/">{{ $tag }}</a>
{{ end }}
~~~

## Range – Schleifen mit Hugo

Mit `range` baut man klassische For-Schleifen. `range` bietet zahlreiche Möglichkeiten Beiträge sortiert und gezielt auszugeben. Leider ist die Syntax nicht ganz einfach. Darum hier eine Sammlung an Beispielen.

### Eine Section _mit_ Index-Seite ausgeben

~~~
{{ range where .Site.Pages "Section" "blog" }}
  <li><a href="{{.Permalink}}">{{.Title}}</a></li>
{{ end }}
~~~

### Eine Section _ohne_ Index-Seite ausgeben

~~~
{{ range where .Site.RegularPages "Section" "blog" }}
  <li><a href="{{.Permalink}}">{{.Title}}</a></li>
{{ end }}
~~~

### Ausgabe steuern nach Schlagworten

~~~
{{ range .Site.Taxonomies.tags.webdesign }}
  <li><a href="{{.Permalink}}">{{.Title}}</a></li>
{{ end }}
~~~

### Range und Data

~~~
{{ range (index .Site.Data (.Get "data")) }}
{{ end }}
~~~

### Sortieren mit `sort`

~~~
{{ range sort .Pages "File.TranslationBaseName" }}
    {{ .Title }}
{{ end }}
~~~

### Umgekehrte Sortierung mit `reverse`

~~~
{{ range .Pages.ByTitle.Reverse }}
{{ end }}
~~~

### Paginator – Weiterblättern alle X Seiten

~~~
{{ range (.Paginator 5).Pages }}
{{ end }}
~~~

### Zeige eine Liste an Tags an

~~~
{{ range $name, $taxonomy := .Site.Taxonomies.tags }}
  <a href="/schlagwort/{{ $name | urlize }}">{{ $name }}</a>
{{ end }}
~~~

### Führe eine Schleife X-Mal aus

Du kannst `seq` mit `range`und `after` kombinieren, um eine bestimmte Anzahl von X Elementen zu erhalten.

~~~
{{ range after 1 (seq 20)}}
{{ end }}
~~~

### `first` – Zeige die letzten drei Beiträge

~~~
{{ range first 3 .Site.Pages }}
  <div>
    <h5><a href="{{ .Permalink }}">{{ .Title }}</a></h5>
    <time class="timeago" datetime='{{ .Date.Format "2006-01-02T15:04:05-07:00" }}'>{{ .Date }}</time>
  </div>
{{ end }}
~~~

### Zeige Beiträge zu einem bestimmten Tag

So zeigen Sie eine Liste der Beiträge für ein bestimmtes Tag an. In diesem Fall habe ich ein Tag mit dem Namen »featured«.

~~~
{{ range .Site.Taxonomies.tags.featured }}
    <h5><a href="{{ .Page.Permalink }}">{{ .Page.Title }}</a></h5>
    <time class="timeago" datetime='{{ .Page.Date.Format "2006-01-02T15:04:05-07:00" }}'>{{ .Page.Date }}</time>
{{ end }}
~~~

### `after` – Zeige Beiträge erst nach den ersten X (offset)

Sie können _first_ und _after_ kombinieren, um eine kompliziertere Abfrage zu erstellen. Das folgende Beispiel zeigt 3 vorgestellte Beiträge an, nachdem der Erste übersprungen wurde. Außerdem soll ein _featured_image_, das im Content-Markdown in der Titelzeile stand angezeigt werden.

~~~
{{ range after 1 (first 3 .Site.Taxonomies.tags.featured) }}
  <div>
    {{ with .Page.Params.featured_image }}<img src="{{ . }}">{{ end }}
    <h5><a href="{{ .Page.Permalink }}">{{ .Page.Title }}</a></h5>
  </div>
{{ end }}
~~~

Wenn Sie sich innerhalb einer Schleife befinden, müssen Sie $ am Anfang von .params hinzufügen, um auf den Wert zuzugreifen. [Siehe dazu ›](http://stackoverflow.com/questions/16734503/access-out-of-loop-value-inside-golang-templates-loop)

~~~
{{ with .Params.some_variable }}{{ with $.Params.some_other_variable }}{{ . }}{{ end }}{{ . }}{{ end }}
~~~

### Nach Parameter (hier: Kategorien) gruppieren

~~~
{{ range .Pages.GroupByParam "chapter" }}
<ul class="toc-list">
    {{ $counter := 0 }}
    {{ range sort .Pages "File.TranslationBaseName" }}
      {{ if eq $counter 0 }}<h2>{{ .Params.Categories }}</h2>{{ end }}
      <li>
        <a href="{{ .Permalink }}">{{ .Title }}</a>
      </li>
      {{ $counter = add $counter 1 }}
    {{ end }}
</ul>
{{ end }}
~~~

### Sortieren mit `range` nach Metadaten

#### ByWeight

~~~
{{ range .Pages.ByWeight }}
{{ end }}
~~~

#### ByTitle

~~~
{{ range .Pages.ByTitle }}
{{ end }}
~~~

#### ByLength

~~~
{{ range .Pages.ByLength }}
{{ end }}
~~~

#### ByDate

~~~
{{ range .Pages.ByDate }}
{{ end }}
~~~

#### ByPublishedDate

~~~
{{ range .Pages.ByPublishedDate }}
{{ end }}
~~~

#### ByExirationDate

~~~
{{ range .Pages.ByExirationDate }}
{{ end }}
~~~

#### ByLastmod

~~~
{{ range .Pages.ByLastmod }}
{{ end }}
~~~

#### ByTitle

~~~
{{  range .Pages.ByTitle }}
{{ end }}
~~~

#### ByLinkTitle

~~~
{{ range .Pages.ByLinkTitle }}
{{ end }}
~~~

#### ByParam

~~~
{{ range (.Pages.ByParam "parametername") }}
{{ end }}
~~~

Verschachtele Parameter

~~~
{{ range (.Pages.ByParam "author.last_name") }}
{{ end }}
~~~

## Hugo Shortcodes

Damit Markdown in Shortcodes nach HTML konvertiert wird, muss der Shortcode `%` nutzen.

**HINWEIS: Da diese Website mit Hugo gebaut wird, musste ich das folgende Beispiel anpassen. Am Anfang steht ein `{{` und _Leerzeichen_ und dann erst das `%`. Das Leerzeichen muss gelöscht werden!**
~~~
{{ % mein_shortcode %}}
**Fett** oder _kursiv_, so wie Du es magst.
{{ % /mein_shortcode %}}
~~~

~~~
{{ < param testparam >}}
{{ < param "my.nested.param" >}}
{{ < instagram BWNjjyYFxVx >}}
{{ < highlight html >}}
   <h1 id="title">{{ .Title }}</h1>
    {{ range .Pages }}
        {{ .Render "summary"}}
    {{ end }}
{{ < /highlight >}}
{{ < youtube w7Ft2ymGmfc >}}
~~~

