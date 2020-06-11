---
title               : 'Hugo – Range-Schleifen'
date                : "2020-05-01T14:39:29+02:00"
tags                :
    - hugo
    - webdesign
---
Bei meiner [Webdesign]({{< ref "/tags/webdesign" >}})-Arbeit mit dem [Website Generator Hugo]({{< ref "/tags/hugo" >}}) stolpere ich immer wieder über die Syntax von _range_-Schleifen. Hier eine Liste verschiedener Varianten, um Beiträge auszugeben.

{{< toc >}}

## Eine Section _mit_ Index-Seite ausgeben

~~~
{{ range where .Site.Pages "Section" "blog" }}
  <li><a href="{{.Permalink}}">{{.Title}}</a></li>
{{ end }}
~~~

## Eine Section _ohne_ Index-Seite ausgeben

~~~
{{ range where .Site.RegularPages "Section" "blog" }}
  <li><a href="{{.Permalink}}">{{.Title}}</a></li>
{{ end }}
~~~

## Ausgabe steuern nach Schlagworten

~~~
{{ range .Site.Taxonomies.tags.webdesign }}
  <li><a href="{{.Permalink}}">{{.Title}}</a></li>
{{ end }}
~~~

## Range und Data
~~~
{{ range (index .Site.Data (.Get "data")) }}
{{ end }}
~~~



