# Was ist das Document Object Model? {#sec:dom}

Wer Webseiten und Webanwendungen entwickelt, kommt um die Hypertext Markup Language, kurz HTML, nicht herum. HTML ist eine Auszeichnugssprache, um Inhalte zu strukturieren. [@Lst:html-snippet] zeigt einen Auszug des HTML-Dokuments, das die aktuelle HTML-Spezifikation beschreibt. Durch die sogenannten HTML-Tags können semantische und hierarchische Informationen hinzugefügt werden. Jeweils ein öffnender und ein schließender HTML-Tag umklammern ein HTML-Element. Beispielsweise drückt der `<header>`-Tag aus, dass das Element zum Dokumentenkopf gehört, `<h1>` und `<h2>` kennzeichnen Überschriften der ersten bzw. zweiten Hierarchieebene.

```{#lst:html-snippet .html caption="Vereinfachter Auszug des HTML-Quelltextes der Spezifikation des HTML5-Standards."}
<header>
    <h1 id="title">HTML 5.3</h1>
    <h2 id="subtitle">
        Editor’s Draft,
        <time datetime="2018-10-18">18 October 2018</time>
    </h2>
</header>

<h2 id="abstract">Abstract</h2>
<p>This specification defines the 5th major version, third minor
revision of the core language of the World Wide Web: the Hypertext
Markup Language (HTML). …</p>
```

Das Document Object Model, kurz DOM, ist eine Repräsentation eines HTML- oder XML-Dokuments. Es dient als Schnittstelle, um auf Elemente des Dokuments zuzugreifen oder es zu verändern. Das DOM stellt ein Dokument als Baum dar, wobei die einzelnen Elemente Knoten dieses Baumes sind.

Der wohl bekannteste Anwendungsfall dürfte die Javascript-Implementation des DOMs sein. JavaScript ist eine Programmiersprache, die im Browser ausgeführt werden kann. Während allein mit HTML lediglich statische Dokumente in einem Browser dargestellt werden können, so erlaubt es JavaScript beispielsweise, in Folge einer Nutzerinteraktion das DOM zu verändern. Damit bildet es den Grundstein interaktiver Webseiten und Webanwendungen. Einige Möglichkeiten, mittels JavaScript auf ein HTML-Dokument zuzugreifen oder es zu verändern sind in [@lst:js-dom] dargestellt.

```{#lst:js-dom .js caption="Beispielhafte Zugriffe auf und Manipulationen an ein HTML-Dokument mithilfe der JavaScript-DOM-API"}
let titleNode = document.querySelector(".title");
console.log(titleNode.textContent); // "HTML 5.3"

titleNode.textContent = "HTML Specification";
console.log(titleNode.textContent); // "HTML Specification"

let subtitleNode = document.querySelector(".subtitle");
let textNode = subtitleNode.children[0];
let timeNode = subtitle.children[1];

console.log(textNode.textContent); // "Editor’s Draft, "
console.log(timeNode.getAttribute("time")); // "2018-10-18"

timeNode.setAttribute("time", "2019-01-01");
console.log(timeNode.getAttribute("time")); // "2019-01-01"
```
