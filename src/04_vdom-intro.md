# Was ist ein virtueller DOM? {#sec:vdom-intro}

Während die deklarative Entwicklung von User Interfaces also zu einer deutlich besseren User Experience führen kann, so sind in der Regel deutlich umfangreichere DOM-Manipulationen als eigentlich notwendig die Folge. Wie in [@sec:dom-performance] erläutert, sind diese DOM-Manipulationen extrem rechenintensiv.

Virtuelle DOMs sind ein Ansatz, deklarative UI-Entwicklung zu ermöglichen, gleichzeitig das DOM aber auf optimale Weise anzupassen. Optimal bedeutet, so wenige DOM-Manipulationen wie nötig vorzunehmen. 

Irrtümlicherweise wird oft angenommen[^vdom-fast], der Einsatz virtueller DOMs sei performanter als direkte DOM-Manipulationen. Klar ist aber: Es müssen immer noch DOM-Manipulationen vorgenommen werden. Der Einsatz eines virtuellen DOMs kann also niemals effizienter sein als die explizite, granulare DOM-Manipulation. Er ermöglicht es jedoch, die deklarative UI-Entwicklung mit einer akzeptablen Rendering-Performance zu verbinden.

Anstatt wie in [@lst:todo-list] nach jeder Datenänderung den bestehenden HTML-Quelltext vollständig durch den neuen zu ersetzen, werden virtuelle DOMs als Zwischenrepräsentation genutzt. Ein vDOM ähnelt in vielerlei Hinsicht einem echten DOM. Es ist jedoch auf die für das Rendering relevanten Informationen reduziert. In der Regel handelt es sich um ein einfaches Objekt, das HTML-Tag und -Attribute sowie eine Liste mit Kind-Elementen enthält. Jedes Kind-Element ist wiederum ein vDOM. Operationen auf dem vDOM sind dadurch besonders effizient. Ein beispielhaftes vDOM ist in [@lst:todo-vdom] dargestellt.

```{#lst:todo-vdom .js caption="Virtuelles DOM für eine Todo-Liste"}
{
    tag: 'ul',
    attributes: { class: 'todo-list' }
    children: [
        {
            tag: 'li',
            attributes: { class: 'is-done' },
            textContent: 'Milch kaufen',
        },
        {
            tag: 'li',
            textContent: 'Steuererklärung abgeben',
        },
    ],
}
```

## Renderingzyklus

![Renderingzyklus](resources/04_vdom-lifecycle.pdf){#fig:vdom-lifecycle}

1. Initial wird aus den gegeben Daten ein virtuelles DOM-Objekt erstellt. 

2. Aus dem vDOM werden rekursiv echte DOM-Knoten erstellt. Bis zu diesem Schritt entstehen noch keine relevanten Vorteile durch die Nutzung eines virtuellen DOMs.

3. Das ändert sich, sobald sich die Daten ändern – und in der Folge ein Rerendering notwendig wird.

4. Es wird erneut ein vDOM-Objekt erstellt – dieses Mal auf Basis der geänderten Daten.

5. Anstatt das neue vDOM-Objekt wie in Schritt 2 direkt zu rendern, wird mithilfe eines sogenannten *Diffing-Algorithmus* eine minimale Menge an Änderungen bestimmt, um den alten Baum in einen neuen zu transformieren.

6. Es werden die zuvor bestimmten minimalen Änderungen durchgeführt. Das DOM entspricht jetzt dem neuen vDOM, ohne dass unnötige DOM-Operationen auszuführen. Die Schritte 3 bis 6 können beliebig oft wiederholt werden.

[^vdom-fast]: Die Google-Suche liefert zum Beispiel für die Suchbegriffe »virtual dom fast« Einträge auf den QA-Webseiten Quora und Stackoverflow: »Why is React's virtual DOM so much faster than the real DOM?« und »How is React's Virtual DOM faster than DOM?«.
