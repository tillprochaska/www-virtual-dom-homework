# Was ist ein virtuelles DOM? {#sec:vdom-intro}

Wie in [@sec:dom-performance] erläutert, sind DOM-Manipulationen häufig extrem rechenintensiv. Virtuelle DOMs sind ein Ansatz, deklarative UI-Entwicklung zu ermöglichen, gleichzeitig das DOM aber auf möglichst optimale Weise anzupassen. Optimal bedeutet, so wenige DOM-Manipulationen wie nötig vorzunehmen[^diff-algo].

Irrtümlicherweise wird oft angenommen[^vdom-fast], der Einsatz virtueller DOMs sei performanter als die direkte Manipulation des DOMs. Klar ist aber: Virtuelle DOMs dienen lediglich als eine Zwischenrepräsentation, an deren Ende immer noch ganz normale DOM-Manipulationen stehen. Der Einsatz eines virtuellen DOMs kann also niemals effizienter sein als die explizite, granulare DOM-Manipulation. Er ermöglicht es jedoch, die deklarative UI-Entwicklung mit einer akzeptablen Rendering-Performance in Einklang zu bringen.

Anstatt wie in [@lst:todo-list] nach jeder Datenänderung den bestehenden HTML-Quelltext vollständig durch den neuen zu ersetzen, werden virtuelle DOMs als Zwischenrepräsentation genutzt. Ein vDOM ähnelt in vielerlei Hinsicht einem echten DOM. Es ist jedoch auf die für das Rendering relevanten Informationen reduziert. In der Regel handelt es sich um ein einfaches Objekt, das HTML-Tag und -Attribute sowie eine Liste mit Kind-Elementen enthält. Jedes Kind-Element ist wiederum ein vDOM. Operationen auf dem vDOM sind dadurch besonders effizient [@aderinokun18; @reactrecon, Kapitel »Reconciliation«].

Ein beispielhaftes vDOM-Objekt ist in [@lst:todo-vdom] dargestellt. In der Regel stellen Frameworks und Bibliotheken eine Hilfsfunktion zum Erstellen von vDOMs bereit, deren Signatur meist der in [@lst:h-sig] dargestellten ähnelt.

```{#lst:todo-vdom .js caption="Virtuelles DOM für eine Todo-Liste. Ein Knoten ist jeweils durch ein dreielementiges (Tag, Attribute, Kindknoten) Array (bzw. im Falle eines Textknotens als String) dargestellt."}
{
    ['ul', { class: 'todo-list' }, [
        ['li', { class: 'is-done' }, ['Vortrag vorbereiten']],
        ['li', { class: 'is-done' }, ['Vortrag halten']],
        ['li', {}, ['Paper fertigstellen']],
    ],
}
```

```{#lst:h-sig .js caption="Signatur einer Funktion zum Erstellen eines vDOM-Knotens"}
Object createElement(String tag, Object attributes, Array children)
```

[^diff-algo]: In der Praxis wird unter Umständen darauf verzichtet, tatsächlich die minimale Menge an Änderungen zu bestimmen, da hierfür eine hohe Anzahl an Vergleichen notwendig ist (vgl. auch @reactrecon, Kapitel »Reconciliation«).
