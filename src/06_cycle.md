# Renderingzyklus
Als Renderingzyklus wird im Folgenden die Gesamtheit aller Schritte bezeichnet, die notwendig ist, um für gegebene Daten das entsprechende View im Browser zu rendern und bei Datenänderungen zu aktualisieren. Einen Überblick über die einzelnen Schritte des Zyklus bietet [@fig:vdom-cycle] [@aderinokun18]:

![Renderingzyklus](resources/05_vdom-cycle.pdf){#fig:vdom-cycle}

1. Initial wird aus den gegeben Daten ein virtuelles DOM-Objekt erstellt. 

2. Aus dem vDOM werden rekursiv echte DOM-Knoten erstellt (siehe [@sec:rendering]). Bis zu diesem Schritt entstehen noch keine relevanten Vorteile durch die Nutzung eines virtuellen DOMs.

3. Wirkung zeigt der Umweg über die Zwischenrepräsentation erst, sobald sich die Daten ändern – und in der Folge ein Rerendering notwendig wird.

4. Es wird erneut ein vDOM-Objekt erstellt – dieses Mal auf Basis der geänderten Daten.

5. Anstatt das neue vDOM-Objekt wie in Schritt 2 direkt zu rendern, wird mithilfe eines sogenannten *Diffing-Algorithmus* eine möglichst minimale Menge an Änderungen bestimmt, um den alten Baum in einen neuen zu transformieren (siehe [@sec:diffing]).

6. Es werden die zuvor bestimmten minimalen Änderungen durchgeführt. Das DOM entspricht jetzt dem neuen vDOM, ohne dass unnötige DOM-Operationen auszuführen. Dieser Vorgang wird auch *Patching* genannt (siehe [@sec:patching]). Die Schritte 3 bis 6 können beliebig oft wiederholt werden.

## Rendering {#sec:rendering}

## Diffing {#sec:diffing}

## Patching {#sec:patching}

[^vdom-fast]: Die Google-Suche liefert zum Beispiel für die Suchbegriffe »virtual dom fast« Einträge auf den QA-Webseiten Quora und Stackoverflow: »Why is React's virtual DOM so much faster than the real DOM?« und »How is React's Virtual DOM faster than DOM?«.
