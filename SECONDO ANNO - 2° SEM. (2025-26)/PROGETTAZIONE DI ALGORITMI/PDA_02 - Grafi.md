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

Formalizzando il problema in questo modo, risulta evidente una condizione necessaria per l'esistenza di una tale passeggiata: **un nodo che non è né l'inizio né la fine della passeggiata deve avere grado pari**, dato che naturalmente se si entra in uno di questi nodi si deve anche uscire da quest'ultimo; tale condizione non è rispettata dal grafo che abbiamo ottenuto, dato che tutti i nodi hanno grado dispari, e dunque si è dimostrato che non è possibile effettuare una passeggiata che rispetti le condizioni iniziali.

Generalizzando il problema dei 7 ponti di Konigsberg, ci si sta sostanzialmente chiedendo **se esiste una sequenza di nodi adiacenti che attraversa tutti gli archi del grafo senza mai passare due volte per lo stesso arco**. In generale, una sequenza di nodi adiacenti è detta "**cammino**", e di conseguenza il cammino descritto da questo problema generalizzato è detto "**cammino euleriano**". In particolare, se un cammino inizia e finisce nello stesso nodo viene chiamato "**circuito**", o "**ciclo**"; se, invece, un cammino o un ciclo non passano mai due volte per lo stesso nodo, essi vengono chiamati "**cammino semplice**" o "**ciclo semplice**".

Se esistono cammini o circuiti euleriani in un grafo, esistono algoritmi efficienti per trovarli. Lo stesso, però, non si può dire per un problema apparentemente molto simile: se volessimo trovare un **cammino che passa per tutti i nodi senza mai passare due volte per uno stesso nodo**? Questo problema fu proposto nella metà dell'800 dal matematico William Rohan Hamilton, e venne inizialmente posto in relazione al grafo dei vertici e spigoli del dodecaedro, un grafo del genere:

![[grafi_esempio_hamilton.png]]

Hamilton chiedeva se fosse possibile, partendo da un vertice (un nodo del grafo), toccare tutti i vertici una e una sola volta spostandosi unicamente lungo gli spigoli del dodecaedro (gli archi del grafo). Nell'immagine appena inserita, in azzurro è evidenziata una delle possibili soluzioni al problema, che casualmente è anche un ciclo. In generale, il problema proposto da Hamilton prende il nome di "**cammino hamiltoniano**" o di "**ciclo hamiltoniano**".

Insomma, è chiaro che i grafi hanno una grande varietà di casi di utilizzo, e in particolare nell'**informatica**: possono essere utilizzati per **modellare reti di computer**, per **visualizzare organizzazioni di dati**, **formalizzare flussi di computazione**, ecc. ecc. Ad esempio, in un sistema operativo, si può utilizzare un grafo per rappresentare il flusso di esecuzione di più processi e il modo in cui essi accedono a un certo numero di risorse (si tratta dei "Resource Allocation Graph" visti a Sistemi Operativi 1). Oltre all'informatica, i grafi sono molto utili in ambiti come l'economia, la fisica, la chimica, o anche la linguistica e la sociologia.
___
##### Rappresentazioni dei grafi

Naturalmente, la rappresentazione visiva che abbiamo visto finora dei grafi non può essere direttamente memorizzata all'interno di un computer. È evidente, dunque, la necessità di individuare altri **modi di rappresentare un grafo in memoria**. Vedremo principalmente due metodi, che sono tendenzialmente quelli più usati:
- la **matrice di adiacenza**;
- la **lista di adiacenza**.

La **matrice di adiacenza** è una matrice $n\times n$, dove $n$ è il numero di nodi del grafo. Si tratta sostanzialmente di una **matrice di valori booleani** che formalizza la presenza o meno di archi tra tutte le possibili coppie di nodi del grafo: infatti, indicando con $M$ tale matrice, abbiamo che $M[u][v]=true$ se l'arco $(u,\,v)$ o $\{u,\,v\}$ appartiene all'insieme $E$ degli archi del grafo, e che $M[u][v]=false$ altrimenti. Chiaramente, **se il grafo è non diretto, la matrice di adiacenza $M$ è una matrice simmetrica** (ossia, $M[u][v]=M[v][u]$).

La matrice di adiacenza risulta **molto efficiente se il massimo interesse è sapere se due nodi sono collegati o meno da un arco**, ma in generale è in realtà **abbastanza dispendiosa in termini di memoria**, richiedendo uno spazio in $O(n^{2})$ indipendentemente dal numero di archi (banalmente, ciò fa capire anche che se si lavora con un grafo sparso, cioè con relativamente pochi archi, la matrice di adiacenza spreca molta memoria); inoltre, sempre **avendo un grafo sparso, scandire tutti gli adiacenti di un dato nodo diventa un'operazione molto costosa**, dato che scorrere un'intera riga o colonna della matrice richiede un tempo in $O(n)$, e va fatto anche se il grado del nodo è molto minore di $n$.

Un'alternativa alla matrice di adiacenza è la **lista di adiacenza**, che consiste sostanzialmente in una lista dei nodi del grafo, e a ciascun nodo $u$ viene abbinata una lista dei suoi adiacenti. Ad esempio, un grafo relativo alle amicizie tra un gruppo di persone può essere rappresentato tramite la seguente lista di adiacenza:

```
Luisa -> Rik, Fabio
Marco -> Anna
Luca -> Rik, Fabio, Angelo, Anna
Ugo -> Anna
Rik -> Luisa, Luca
Fabio -> Luisa, Luca, Maria
Anna -> Luca, Marco, Ugo, Angelo, Maria
Angelo -> Luca, Anna
Maria -> Anna, Fabio
```

Il **costo in termini di memoria** è in $O(n+m)$, dove $n$ è il numero di nodi del grafo e $m$ è il numero di archi; è chiaro, dunque, che (almeno per grafi sparsi) una lista di adiacenza è preferibile a una matrice di adiacenza. Inoltre, anche se non permette di capire se un arco esiste o meno in tempo costante ($O(1)$) come nella matrice, la lista di adiacenza permette di **scandire l'intera lista degli adiacenti di un nodo $u$ in tempo $O(d)$**, dove $d$ è il grado di $u$. Per queste ragioni, generalmente le liste di adiacenza sono di gran lunga più utilizzate rispetto alle matrici di adiacenza.
___
##### Connettività

Una delle proprietà fondamentali della struttura di un grafo è la "**connettività**".

Due nodi $u$ e $v$ si dicono "**connessi**" se **esiste un cammino che li connette**. Di solito, tale relazione di connessione è pensata in modo simmetrico (ovviamente, ciò accade nei [[PDA_02 - Grafi#Cos'è un grafo?|grafi non diretti]], in cui se esiste un cammino da $u$ a $v$ esso equivale al cammino "rovesciato" da $v$ a $u$). Un grafo non diretto è detto **connesso** se, comunque presi due nodi $u$ e $v$, esiste un cammino che li connette.

Per grafi diretti il discorso è un po' più complesso, dato che l'esistenza di un cammino orientato da $u$ a $v$ non implica l'esistenza del cammino orientato opposto. Per questo, nel caso dei grafi diretti, si dice che un grafo è "**fortemente connesso**" se per ogni coppia di nodi $u$ e $v$ esiste sia un cammino orientato da $u$ a $v$ che un cammino orientato da $v$ a $u$.

Nel caso in cui un grafo non sia connesso, lo si può vedere come **partizionato in sottoparti connesse**: dunque, in un grafo non diretto $G$, una "**componente connessa**" è un sotto-grafo di $G$ che è connesso e che non è estendibile senza distruggere la connessione. In altre parole, **se un grafo non diretto $G$ non è connesso, allora è sicuramente partizionato in due o più componenti connesse**, e non sono presenti archi che collegano nodi appartenenti a componenti connesse differenti. Considerando il concetto di connessione forte, si può fare una considerazione simile per i grafi diretti: in un grafo diretto $G$, una "**componente fortemente connessa**" è un sotto-grafo di $G$ che è fortemente connesso e che non è estendibile senza distruggere la connessione forte. In altre parole, **se un grafo diretto $G$ non è fortemente connesso, allora è sicuramente partizionato in due o più componenti fortemente connesse**, e gli archi tra queste non possono formare cicli, cioè non esistono cicli che contengono nodi appartenenti a componenti differenti. Ad esempio, nel grafo seguente ci sono 6 componenti fortemente connesse, evidenziate dai diversi colori dei nodi:

![[grafi_esempio.png]]
___
## Visita di un grafo

Per "**visita di un grafo**" si intende una procedura che, **partendo da un nodo $u$, visita tutti i nodi e gli archi raggiungibili da $u$**, e dunque che a ogni nuovo passo visita nuovi nodi o archi solamente se direttamente connessi a nodi o archi già visitati. Per intenderci, un nodo o arco si dice **"raggiungibile" da $u$** se esiste un cammino che arriva da $u$ al nodo o arco considerato.

Ovviamente, ci sono tantissimi modi per effettuare una visita di un grafo; tuttavia, due procedure in particolare sono specialmente importanti, sia per la loro semplicità che per le loro proprietà. Le due procedure in questione sono:
- la **Depth First Search**, o **DFS** in breve;
- la **Breadth First Search**, o **BFS** in breve.

##### La DFS

La **DFS** è una procedura simile a quella che si potrebbe seguire, intuitivamente, per esplorare un labirinto: 

[APPUNTI: 02, pag. 2]
___
##### La BFS


___