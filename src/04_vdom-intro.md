# Wirkung und Aufbau eines virtuellen DOMs {#sec:vdom-intro}

Während die deklarative Entwicklung von User Interfaces also zu einer deutlich besseren User Experience führen kann, so sind in der Regel deutlich umfangreichere DOM-Manipulationen als eigentlich notwendig die Folge. Wie in [@sec:dom-performance] erläutert, sind diese DOM-Manipulationen extrem rechenintensiv.

Virtuelle DOMs sind ein Ansatz, deklarative UI-Entwicklung zu ermöglichen, gleichzeitig das DOM aber auf optimale Weise anzupassen. Optimal bedeutet, so wenige DOM-Manipulationen wie nötig vorzunehmen. 

Irrtümlicherweise wird oft angenommen, der Einsatz virtueller DOMs sei performanter als direkte DOM-Manipulationen. Klar ist aber: Es müssen immer noch DOM-Manipulationen vorgenommen werden. Der Einsatz eines virtuellen DOMs kann also niemals effizienter sein als die explizite, granulare DOM-Manipulation. Er ermöglicht es jedoch, die deklarative UI-Entwicklung mit einer akzeptablen Rendering-Performance zu verbinden.
