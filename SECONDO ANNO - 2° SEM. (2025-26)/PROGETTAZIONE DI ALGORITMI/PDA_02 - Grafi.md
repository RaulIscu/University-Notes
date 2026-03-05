## Cos'è un grafo?

> Un **grafo** è una coppia $(V,\, E)$, dove $V$ è un **insieme di vertici**, o **nodi**, ed $E$ è un insieme di **archi**, definiti come collegamento tra coppie di vertici.

In altri termini, possiamo vedere un grafo come una **collezione di elementi con una relazione binaria tra di essi**, dove i vertici rappresentano tali elementi e gli archi le relazioni binarie che sussistono tra coppie di vertici $(u,\,v)$. Le relazioni tra i vari nodi possono essere **simmetriche** (ad esempio le relazioni di amicizia tra due persone, ossia in cui entrambe le parti hanno il medesimo ruolo) o **asimmetriche** (ad esempio i link tra pagine Web, ossia in cui le due parti hanno ruoli diversi).

Come detto, le relazioni che sussistono tra due nodi sono chiamate "archi". Se la relazione tra due nodi $u$ e $v$ è simmetrica, allora l'arco è detto "**non diretto**" e denotato con $\{u,\,v\}$; al contrario, se la relazione tra due nodi $u$ e $v$ è asimmetrica, allora l'arco è detto "**diretto**", o anche "**orientato**", e denotato con $(u,\,v)$, dove il verso dell'arco va dal nodo $u$ al nodo $v$. Di conseguenza, un **grafo che presenta solamente archi non diretti** viene detto "**grafo non diretto**", mentre un **grafo che presenta solamente archi diretti** viene detto "**grafo diretto**".

All'interno di un grafo, due nodi $u$ e $v$ collegati da un arco si dicono **adiacenti** o **direttamente connessi**; l'arco che collega i due nodi si dice "**incidente**" in $u$ e in $v$, e il numero degli archi incidenti in un nodo $u$ è detto **grado** di $u$. In particolare, se ci si trova in un grafo diretto (dunque, se tutti gli archi del grafo sono orientati), distinguiamo tra "**grado uscente**" di $u$, ossia il numero di archi uscenti dal nodo $u$, e "**grado entrante**" di $u$, ossia il numero di archi entranti nel nodo $u$.

##### Applicazioni dei grafi

I grafi sono utili per formalizzare una varietà di situazioni. Uno degli esempi più iconici è il **problema dei 7 ponti di Konigsberg**: in tale cittadina, si trova una disposizione di 7 ponti equivalente alla seguente:

![[grafi_esempio_konigsberg.png]]

e ci si chiede se è possibile effettuare una passeggiata che attraversi tutti e 7 i ponti passando una sola volta su ciascuno di essi. Per rispondere a questa domanda, nel 1735 il matematico Leonhard Euler pose di fatto le basi per la nascita della teoria dei grafi: la figura precedente può infatti essere rappresentata con un grafo, che dispone di 4 nodi (le varie "zone" collegate dai ponti) e di 7 archi (i ponti stessi):

![[grafi_esempio_konigsberg1.png]]



[APPUNTI: 01, pag. 2 - 3]
___
##### Rappresentazioni dei grafi

[APPUNTI: 01, pag. 3 - 4]
___
##### Connettività

[APPUNTI: 01, pag. 4 - 5]
___