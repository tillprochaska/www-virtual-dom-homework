# Evolution der Frontend-Entwicklung {#sec:frontend-dev}

Innerhalb der letzten 15 Jahre wurden mit der zunehmenden Verlagerung von Anwendungen in den Browser unterschiedlichste JavaScript-Bibliotheken und -Frameworks zur Unterstützung der Entwicklung von Web-Anwendungen entwickelt.

## Einfaches Scripting {#sec:simple-scripting}
In den frühen 2000er-Jahren wurden Web-Anwendungen im Regelfall serverseitig entwickelt, d. h. sowohl Business-Logik als auch das Rendering der Anwendung wurde in einer serverseitigen Programmiersprache implementiert. Damit NutzerInnen interaktive Funktionalitäten nutzen konnten, war in der Regel ein Request an den Server notwendig, der die Auslieferung einer komplett neu gerenderten Seite an den Browser zur Folge hatte. Javascript diente zu dieser Zeit lediglich der vereinzelten Ergänzung der serverseitig gerenderten Anwendung. Typische Beispiele hierfür sind z. B. Dropdowns, Date-Picker oder Slideshows.

Viele Browser-Funktionalitäten waren in dieser Zeit entweder noch nicht standardisiert oder von Browser-Engines nicht standardgetreu implementiert. Dies führte zur Entstehung von Bibliotheken wie Prototype[^prototype] und jQuery[^jquery]. Ihr primärer Zweck lag in der Vereinheitlichung und vereinfachten Verwendung von Browserfunktionalitäten wie z. B. Event-Listening, asynchrone Netzwerkanfragen (AJAX) oder DOM-Manipulationen.

```{#lst:jquery-expl .js caption="Implementierung eines Dropdowns mit jQuery"}
$('.dropdown').click(function(event) {
    e.preventDefault();
    $(this).parent('.dropdown').find('.dropdown-list').toggle();
});
```
```{#lst:vanilla-js-expl .js caption="Implementierung eines Dropdowns ohne Javascript-Library"}
var buttons = document.getElementsByClassName('dropdown-button');
for(var i = 0; i < buttons.length; i++) {
  buttons[i].onclick = function(event) {
    var dropdown = this.parentNode;
    var list = dropdown.getElementsByClassname('dropdown-list')[0];
    var isVisible = list.style.display === 'block';
    list.style.display = isVisible ? 'none' : 'block';
  };
}
```

Das beiden Codebeispiele [-@lst:jquery-expl; -@lst:vanilla-js-expl] zeigen dabei auf, wie stark die Nutzung einer Javascript-Bibliothek die Implementierung selbst simpler Funktionalität – in diesem Fall das Ein- und Ausblenden der Einträge eines Dropdown-Menüs – vereinfachen konnten. (Sofern z. B. auch eine Unterstützung des Internet Explorer 7 oder 8 gefordert gewesen wäre, wäre die Implementierung in der Praxis noch komplexer geworden.)

Aus beiden Codebeispielen wird der vorherrschende imperative Programmierstil deutlich: nach einem Mausklick wird das Dropdown-Element explizit manipuliert, indem eine Klasse entweder hinzugefügt oder entfernt wird.

## Komplexe Javascript-Anwendungen mit Data-Modeling und -Bindings
Ende der 2000er-Jahre entstanden vermehrt aufwändige, stark interaktive Webanwendungen. Beispielhaft hierfür seien Facebook und GMail genannt. Um eine bessere User-Experience zu erlauben, setzten die EntwicklerInnen solcher Anwendungen vermehrt auf clientseitige Programmierung. Auf einmal mussten mittels Javascript komplexe Datenstrukturen gerendert und Nutzerinteraktionen behandelt werden.

Die Komplexität dieser Anwendung erforderte eine bessere Sturkturierung der Codebasis, als sie bisher üblich waren. Im Jahr 2010 wurden mit Backbone.js[^backbone] und Knockout[^knockout] zwei Frameworks veröffentlicht, die sich dieses Problems annahmen – und deshalb großer Popularität erfreuten. Mit Knockout erlaubte ein Framework zum ersten Mal die deklarative Programmierung von User-Interfaces.

```{#lst:knockout-expl-html .html caption="HTML-Code für ein Dropdown-Menü mit Knockout"}
<div class="dropdown">
    <button class="dropdown-button" data-bind="click: toggle">
      Click me
    </button>
    
    <ul class="dropdown-list" data-bind="visible: isOpen">
      <li>Item 1</li>
      <li>Item 2</li>
    </ul>
</div>
```

```{#lst:knockout-expl-js .js caption="Javascript-Code für ein Dropdown-Menü mit Knockout"}
var DropdownViewModel = function() {
    this.isOpen = ko.observable(false);
 
    this.toggle = function() {
        this.isOpen(!this.isOpen());
    };
};
 
ko.applyBindings(new DropdownViewModel());
```

Wie das Dropdown-Beispiel aus [@sec:simple-scripting] in Knockout implementiert werden kann, ist in [@lst:knockout-expl-html, @lst:knockout-expl-js] dargestellt. Anstelle das DOM direkt zu manipulieren, wird lediglich der Zustand des sogenannte View-Model aktualisiert. Das Framework nimmt dann die Aktualisierung des DOMs vor. Die derartige Strukturierung des Frontend-Codes und die Kapselung des Zustands verringert Konflikte zwischen verschiedenen Bestandteilen einer Anwendung und ermöglicht die einfache Wiederverwendbarkeit.

## Single-Page-Applications & deklarative View-Libraries
Das Konzept des virtuellen DOMs ist – obwohl es grundsätzlich unabhängig von ihnen ist – eng mit der Popularität dieser Frameworks verbunden.

[^prototype]: Prototype; erste Version veröffentlicht in 2005; Webseite: <http://prototypejs.org/>
[^jquery]: jQuery; erste Version veröffentlicht in 2006; Webseite: <https://jquery.org/>
[^backbone]: Backbone; erste Version veröffentlicht in 2010; Webseite: <https://backbonejs.org/>
[^knockout]: Knockout; erste Version veröffentlicht in 2010; Webseite: <https://knockoutjs.com/>
