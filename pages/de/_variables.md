
# Variablen

Variablen sind die Essenz jeder Programmiersprache. Sie erlauben es, Werte wiederzuverwenden ohne sie jedesmal erneut kopieren zu müssen. Der wichtigste Punkt ist, dass sie es sehr einfach machen, einen Wert zu aktualisieren. Kein manuelles suchen und ersetzen mehr.

CSS ist jedoch lediglich eine große Kiste mit all unseren Schätzen. Anders als andere Sprachen, existiert in CSS kein echter Scope. Deshalb müssen wir beim Hinzufügen von Variablen das Risiko von Konflikten im Auge behalten.

Von daher ist mein Ratschlag, Variablen nur dann zu erzeugen, wenn es auch wirklich sinnvoll ist. Erstelle keine Variablen einfach weil du es kannst; es wird dich nicht weiter bringen. Eine neue Variable sollte nur bei folgenden Kriterien erstellt werden:

* der Wert wiederholt sich mindestens zweimal;
* der Wert wird vorraussichtlich mindestens einmal aktualisiert;
* alle Vorkommen des Werts sind an die Variable gebunden (d.h. nicht durch Zufall).

Grundsätzlich hat es keinen Sinn, eine Variable zu erstellen, die niemals aktualisiert oder nur ein einziges Mal verwendet wird.

## Scoping

Der Scope von Variablen in Sass hat sich über die Jahre verändert. Bis vor kurzem waren Deklarationen innerhalb von Regelsätzen und anderen Scopes standardmäßig lokal. Wenn es jedoch eine globale Variable mit demselben Namen gab, hat die lokale Variable die globale überschrieben. Seit Version 3.4 setzt Sass das Konzept von Scopes korrekt um und erzeugt stattdessen eine neue lokale Variable.

Die Dokumentation spricht von *Beschattung globaler Variablen*. Wenn eine Variable im inneren Scope (Selektor, Funktion, Mixin, …) deklariert wird, aber schon im globalen Scope existiert, dann sagt man, dass sie die globale Variable *beschattet*. Grundsätzlich überscheibt die lokale Variable die globale nur im lokalen Scope.

Folgendes Code-Snippet erklärt das Konzept der *Variablenbeschattung*:

{% include snippets/variables/01/index.html %}

## `!default` flag

Wenn eine Library, ein Framework, ein Gridsystem oder irgendwas anders in Sass verbreitet und von externen Entwicklern benutzt wird, sollten alle Konfigurationsvariablen als `!default` markiert werden, sodass sie auch überschrieben werden können.

{% include snippets/variables/02/index.html %}

Dadurch ist es einem Entwicker möglich, eine eigene `$baseline`-Variable *vor* dem Importieren deiner Library zu definieren, ohne dass sie überschrieben wird.

{% include snippets/variables/03/index.html %}

## `!global`-Flag

Das `!global`-Flag sollte nur benutzt werden, wenn eine globale Variable vom lokalen Scope überschrieben wird. Wenn eine Variable auf der Root-Ebene definiert wird, sollte das `!global`-Flag weggelassen werden.

{% include snippets/variables/04/index.html %}

## Mehrere Variablen oder Maps

Es hat Vorteile, Maps anstatt mehrerer einzelner Variablen zu verwenden. Der größte Vorteil ist die Fähigkeit, über eine Map zu iterieren, was mit einzelnen Variablen nicht möglich ist.

Ein weiterer Vorteil von Maps ist die Möglichkeit, eine kleine getter-Funktion zu schreiben, um eine freundlichere API bereitzustellen. Stell dir zum Beispiel folgenden Sass-Code vor:

{% include snippets/variables/05/index.html %}
