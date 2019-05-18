# Was ist das Document Object Model? {#sec:dom}

Wer Webseiten und Webanwendungen entwickelt, kommt um die Hypertext Markup Language, kurz HTML, nicht herum. HTML ist eine Auszeichnugssprache, um Inhalte zu strukturieren. Diesen können durch sogenannte HTML-Tags semantische und hierarchische Informationen hinzugefügt werden [@htmlspec17].

[@Lst:html-snippet] zeigt einen Auszug eines HTML-Dokuments, das eine einfache Todo-Liste beschreibt. Jeweils ein öffnender und ein schließender HTML-Tag umklammern ein HTML-Element. Ein `<h1>`-Tag kennzeichnet eine Überschrift der ersten Hierarchieebenen (engl. *heading 1*). Der `<ul>`-Tag drückt aus, dass es sich um eine ungeordnete Liste (engl. *unordered list*) handelt. Die Liste enthält mehrere `<li>`-Elemente, die einzelnen Listenelemente (engl. *list items*).

```{#lst:html-snippet .html caption="Auszug eines HTML-Dokuments zur Darstellung einer einfachen Todo-Liste"}
<h1>Meine Aufgaben</h1>
<ul>
  <li class="is-done">Vortrag vorbereiten</li>
  <li class="is-done">Vortrag halten</li>
  <li>Paper fertigstellen</li>
</ul>
```

Das Document Object Model, kurz DOM, ist eine Repräsentation eines HTML-Dokuments[^dom-xml]. Es dient als Schnittstelle, um auf Elemente des Dokuments zuzugreifen oder es zu verändern. Das DOM stellt ein Dokument als Baum dar, wobei die einzelnen HTML-Elemente Knoten dieses Baumes sind [@domspec04, »What is the Document Object Model?«].

Der wohl bekannteste Anwendungsfall dürfte die Javascript-Implementation des DOMs sein. JavaScript ist eine Programmiersprache, die im Browser ausgeführt werden kann. Während mit HTML allein lediglich statische Dokumente in einem Browser dargestellt werden können, so erlaubt es JavaScript beispielsweise, in Folge einer Nutzerinteraktion das DOM – und damit die Darstellung im Browser – zu verändern. Damit bildet es den Grundstein interaktiver Webseiten und Webanwendungen. Einige Möglichkeiten, mittels JavaScript auf ein HTML-Dokument zuzugreifen oder es zu verändern sind in [@lst:js-dom] dargestellt.

```{#lst:js-dom .js caption="Beispielhafte Zugriffe auf und Manipulationen an ein HTML-Dokument mithilfe der JavaScript-DOM-API"}
let titleNode = document.querySelector('h1');
console.log(titleNode.textContent); // => "Meine Aufgaben"

let listNode = document.querySelector('ul');
console.log(listNode.children); // => [HTMLLIElement, HTMLLIElement, …]

let itemNode = listNode.children[2];
itemNode.classList.add('is-done');
console.log(itemNode.textContent); // => 'Paper fertigstellen'
console.log(itemNode.classList); // => ['is-done']
```

[^dom-xml]: Tatsächlich können auch generische XML-Dokumente oder z. B. SVG-Grafiken durch ein DOM repräsentiert werden.
