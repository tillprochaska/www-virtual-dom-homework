# Evolution der Frontend-Entwicklung {#sec:frontend-dev}

Innerhalb der letzten 15 Jahre wurden mit der zunehmenden Verlagerung von Anwendungen in den Browser unterschiedlichste JavaScript-Bibliotheken und -Frameworks zur Unterstützung der Entwicklung von Web-Anwendungen entwickelt.

In den frühen 2000er-Jahren wurden Web-Anwendungen im Regelfall serverseitig entwickelt, d. h. sowohl Business-Logik als auch das Rendering der Anwendung wurde in einer serverseitigen Programmiersprache implementiert. Damit NutzerInnen interaktive Funktionalitäten nutzen konnten, war in der Regel ein Request an den Server notwendig, der die Auslieferung einer komplett neu gerenderten Seite an den Browser zur Folge hatte. Javascript diente zu dieser Zeit lediglich der vereinzelten Ergänzung der serverseitig gerenderten Anwendung. Typische Beispiele hierfür sind z. B. Dropdowns, Date-Picker oder Slideshows.

Viele Browser-Funktionalitäten waren in dieser Zeit entweder noch nicht standardisiert oder von Browser-Engines nicht standardgetreu implementiert. Dies führte zur Entstehung von Bibliotheken wie Prototype[^prototype] und jQuery[^jquery]. Ihr primärer Zweck lag in der Vereinheitlichung und vereinfachten Verwendung von Browserfunktionalitäten wie z. B. Event-Listening, asynchrone Netzwerkanfragen (AJAX) oder DOM-Manipulationen.

Ende der 2000er-Jahre entstanden vermehrt aufwändige, stark interaktive Webanwendungen. Beispielhaft hierfür seien Facebook und GMail genannt. Um eine bessere User-Experience zu erlauben, setzten die EntwicklerInnen solcher Anwendungen vermehrt auf clientseitige Programmierung. Auf einmal mussten mittels Javascript komplexe Datenstrukturen gerendert und Nutzerinteraktionen behandelt werden.

Hierbei stellte nicht nur vom Standard abweichende JavaScript-Implementationen eine Herausforderung dar. Die Komplexität dieser Anwendung erforderte auch eine bessere Sturkturierung der Codebasis, als sie bisher üblich waren. Im Jahr 2010 wurden mit Backbone.js[^backbone] und Knockout[^knockout] zwei Frameworks veröffentlicht, die sich dieses Problems annahmen – und deshalb großer Popularität erfreuten. Mit Knockout erlaubte ein Framework zum ersten Mal die deklarative Programmierung von User-Interfaces.

Der Ansatz deklarativer UI-Entwicklung hat sich spätestens mit der zunehmenden Popularität von Frontend-Frameworks wie React[^react] und Vue.js[^vuejs] durchgesetzt. Dieser Ansatz trennt das zugrundeliegende Datenmodell von der View-Schicht. Anstatt auf Nutzerinteraktionen mit expliziten DOM-Manipulationen zu reagieren, wird lediglich eine Aktualisierung des Datenmodells ausgelöst. Die Synchronisation der View-Schicht mit dem Datenmodells übernimmt das Framework.

[^prototype]: Prototype; erste Version veröffentlicht in 2005; Webseite: <http://prototypejs.org/>
[^jquery]: jQuery; erste Version veröffentlicht in 2006; Webseite: <https://jquery.org/>
[^backbone]: Backbone; erste Version veröffentlicht in 2010; Webseite: <https://backbonejs.org/>
[^knockout]: Knockout; erste Version veröffentlicht in 2010; Webseite: <https://knockoutjs.com/>
[^react]: React; erste Version veröffentlicht in XXXX; Webseite: <https://reactjs.org>
[^vuejs]: Vue.js; erste Version veröffentlicht in XXXX; Webseite: <https://vuejs.org>
