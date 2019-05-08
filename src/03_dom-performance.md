# Performance-Implikationen von DOM-Manipulationen

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

Mithilfe eines einfachen Benchmarking-Test kann nachvollzogen werden, dass dies auch Auswirkungen auf die Performance hat. Im Test-Szenario werden jeweils 25 Aufgaben zu einer Todo-Liste hinzugefügt und anschließend als erledigt markiert. Verglichen wird die in [@lst:todo-list] gezeigte Implementierung sowie eine vergleichbare Implementierung, die explizite, granulare DOM-Manipulationen vornimmt. Die Implementierung aus [@lst:todo-list] ist dabei bis zu 95 Prozent langsamer[^benchmark].

Um zu verstehen, warum unnötige DOM-Manipulationen wie diese ein Problem darstellen, ist es wichtig, den Rendering-Prozess eines Browser zu verstehen.

[^benchmark]: Der vollständige Test-Case sowie Testergebnisse sind unter <https://jsperf.com/performance-decl-expl-dom-manipulation> einzusehen. Der Test wurde in Chrome 73.0.3683 unter macOS 10.12.6 durchgeführt.
