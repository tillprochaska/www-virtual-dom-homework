# Performance-Implikationen von DOM-Manipulationen {#sec:dom-performance}

Während der deklarative Ansatz eine deutlich bessere Developer Experience bieten und mit einer geringeren Fehleranfälligkeit aufwarten kann, so entsteht bei einer banalen Umsetzung die Gefahr von Performance-Einschränkungen.

[@Lst:todo-list] zeigt eine einfache deklarative Implementierung einer Todo-Liste. Mithilfe der Methoden `addTodo` und `completeTodo` können Aufgaben zur Todo-Liste hinzugefügt bzw. als erledigt markiert werden. Zwar wird bei Ausführung im Browser das erwartete Ergebnis gerendert. Jedoch ersetzen sowohl `addTodo` als auch `completeTodo` bei jedem Aufruf die gesamte Todo-Liste, obwohl lediglich ein neues Element angefügt bzw. nur das `class`-Attribut eines existierenden Elements hätte geändert werden müssen.

```{#lst:todo-list .js caption="Einfache deklarative Umsetzung einer Todo-Liste"}
const render = todos => {
    const listItems = todos.map(item => `
        <li class="${ item.isDone && 'is-done'}">
            ${ item.text }
        </li>
    `);

    return `<ul>${ listItems.join('') }</ul>`;
};

const updateDOM = () => document.body.innerHTML = render(todos);

const addTodo = (text, isDone = false) => {
    todos.push({ text, isDone });
    updateDOM();
};

const completeTodo = index => {
    todos[index].isDone = true;
    updateDOM();
};

let todos = [];
updateDOM();
```

Mithilfe eines einfachen Benchmarking-Test kann nachvollzogen werden, dass dies Auswirkungen auf die Performance hat, z. B. in Hinblick auf die Zeit, die das Aktualisieren des Views in Anspruch nimmt.  Im Test-Szenario werden jeweils 25 Aufgaben zu einer Todo-Liste hinzugefügt und anschließend als erledigt markiert. Verglichen wird die in [@lst:todo-list] gezeigte Implementierung sowie eine vergleichbare Implementierung, die explizite, granulare DOM-Manipulationen vornimmt. Die Implementierung aus [@lst:todo-list] ist dabei bis zu 95 Prozent langsamer[^benchmark].

Um zu verstehen, warum unnötige DOM-Manipulationen wie im Beispiel ein Problem darstellen, ist es wichtig, den Rendering-Prozess eines Browser zu verstehen. Aus dem Webseiten-Quelltext erstellt der Browser neben dem DOM noch eine weitere Baumstruktur, das sogenannte CSS-Object-Model, kurz CSSOM. Während das DOM die Struktur des HTML-Dokuments repräsentiert, liefert das CSSOM Informationen zur visuellen Darstellung der einzelnen HTML-Elemente, basierend auf ausgelieferten Cascading Stylesheets.

1. DOM und CSSOM werden zusammen zu einen sogenannten Render-Tree kombiniert. Dieser enthält die zu rendernden Knoten und deren jeweilige Gestaltungsvorgaben.

2. Zwar enthält der Render-Tree Informationen zur Gestaltung der einzelnen Elemente. In der Regel enthält er aber keine Informationen über die konkrete Position eines Elements auf dem Bildschirm. Im Beispiel aus [@lst:html-snippet] verfügt der Browser lediglich über die Information, dass zunächst die Überschrift, anschließend eine Liste dargestellt werden soll. Die Dimensionen und die Position sind also nur implizit gegeben. Im *Layouting* genannten Prozess bestimmt der Browser die konkreten Dimensionen und Positionen der HTML-Elemente.

3. Während des *Paintings* werden die einzelnen Knoten des Render-Trees durchlaufen und als tatsächliche Pixel auf dem Bildschirm angezeigt.

Ergeben sich Änderungen am DOM oder CSSOM, wird der Browser möglichst wenige Operationen durchführen, um die Anzeige im Browser anzupassen. Wird beispielsweise lediglich die Textfarbe eines Elements angepasst, so reicht es aus, den Painting-Prozess für dieses eine Element neu auszuführen. Wird hingegen ein Element in der Mitte des HTML-Dokuments entfernt oder hinzugefügt, so müssen die Position und Größe aller nachfolgenden Elemente neu berechnet werden [@mozrenderpath19].

Wird in [@lst:todo-list] z. B. eine Aufgabe als erledigt markiert, wird die gesamte Todo-Liste durch eine neue ersetzt. In der Folge muss das Layouting und Painting für alle Listenelemente und für alle nachfolgenden Elemente neu ausgeführt werden.

Bei einer vergleichbaren Umsetzung mittels expliziter, granularer DOM-Manipulationen würde lediglich das `class`-Attribut eines einzelnen Listenelements aktualisiert. Sofern hierdurch die Dimensionen und die Positionierung des Listenelements nicht verändert wird, muss der Browser lediglich für dieses Element den Painting-Prozess neu durchlaufen. Es sind also deutlich weniger Operationen notwendig, um die Anzeige auf dem Bildschirm zu aktualisieren.

[^benchmark]: Der vollständige Test-Case sowie Testergebnisse sind unter <https://jsperf.com/performance-decl-expl-dom-manipulation> einzusehen. Der Test wurde in Chrome 73.0.3683 unter macOS 10.12.6 durchgeführt.
