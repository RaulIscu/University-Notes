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
##### Visita di un grafo

Per "**visita di un grafo**" si intende una procedura che, **partendo da un nodo $u$, visita tutti i nodi e gli archi raggiungibili da $u$**, e dunque che a ogni nuovo passo visita nuovi nodi o archi solamente se direttamente connessi a nodi o archi già visitati. Per intenderci, un nodo o arco si dice **"raggiungibile" da $u$** se esiste un cammino che arriva da $u$ al nodo o arco considerato.

Ovviamente, ci sono tantissimi modi per effettuare una visita di un grafo; tuttavia, due procedure in particolare sono specialmente importanti, sia per la loro semplicità che per le loro proprietà. Le due procedure in questione sono:
- la **Depth First Search**, o **[[PDA_02 - Grafi#La DFS|DFS]]** in breve;
- la **Breadth First Search**, o **[[PDA_02 - Grafi#La BFS|BFS]]** in breve.
___
## La DFS

La **DFS** è una procedura di **[[PDA_02 - Grafi#Visita di un grafo|visita di un grafo]]** simile a quella che si potrebbe seguire, intuitivamente, per esplorare un labirinto: 
- **partendo dall'entrata del labirinto, avanzeremmo in uno dei corridoi** fino ad arrivare ad un bivio, e a quel punto **prenderemmo nuovamente uno dei corridoi disponibili**, e così via;
- dovremmo, però, stare anche attenti a non girare in tondo, e cercheremmo quindi anche di **non percorrere corridoi già attraversati in precedenza**; 
- oltre a ciò, sarebbe utile **ricordare anche quali corridoi ci hanno portato al punto in cui ci troviamo a partire dall'entrata**, dato che senza questa memoria tutti i bivi già visitati diventerebbero indistinguibili e non sapremmo quali potrebbero portare a corridoi inesplorati, introducendo il rischio di non esplorare l'intero labirinto.

Generalizzando il ragionamento appena esposto nel contesto dei [[PDA_02 - Grafi#Cos'è un grafo?|grafi]], quello che vogliamo fare è:
- **a partire da un nodo, avanzare nel grafo seguendo uno degli archi** uscenti dallo stesso;
- **ricordare quali nodi sono già stati visitati**;
- **ricordare il cammino dal nodo di partenza al nodo in cui ci troviamo**.

In particolare, per memorizzare quest'ultima informazione possiamo utilizzare una struttura dati particolare ma notevolmente efficace in questo contesto: la **pila**, o "**stack**". Si tratta di una struttura dati lineare e ordinata di tipo **LIFO**, ossia "**Last In, First Out**": ciò implica che **l'ultimo elemento ad essere inserito nello stack sarà il primo ad essere eventualmente rimosso**. Sullo stack, dunque, sono definite **due operazioni**:
- il "**push**", utilizzato per aggiungere un elemento nello stack;
- il "**pop**", utilizzato per rimuovere un elemento dallo stack.

Lo stack fa proprio al caso nostro dato che, **quando ci si troverà in un nodo in cui tutti gli archi incidenti sono già stati attraversati** (tornando all'esempio del labirinto, un bivio da cui partono tutti corridoi già esplorati), basterà tornare al nodo precedente del cammino, ossia **effettuare un'operazione di pop** sullo stack; invece, **quando si vorrà attraversare un arco per arrivare a un nuovo nodo** (avanzare in un corridoio non esplorato in precedenza), basterà aggiungere quest'ultimo al cammino, ossia **effettuare un'operazione di push** sullo stack.

Sulla base delle conclusioni effettuate finora, possiamo già fornire dello **pseudocodice** per un algoritmo di visita di un grafo di tipo DFS:

```
DFS(G: grafo, u: nodo di partenza):
	VIS <- insieme dei nodi visitati, inizialmente vuoto
	S <- stack del cammino, inizialmente vuoto
	
	S.push(u)
	VIS.add(u)
	
	while (S is not empty):
		v <- S.top()               # legge il nodo in cima allo stack
		if (esiste un adiacente w di v, con w non in VIS):
			VIS.add(w)
			S.push(w)              # aggiunge w in cima allo stack
		else:
			S.pop()                # rimuove il nodo in cima allo stack
	
	return VIS
```

Al termine della visita, e dunque dell'esecuzione dell'algoritmo, **`VIS` conterrà 
l'insieme dei nodi visitati**. 
##### Esempio di esecuzione dell'algoritmo DFS

Per capire meglio come funziona l'algoritmo, vediamo un esempio concreto. Di seguito, vediamo i vari passaggi della visita di un grafo (ogni passaggio rappresenta una nuova iterazione del ciclo `while`) partendo dal nodo `a`, in cui il nodo azzurro è quello appena letto dalla cima dello stack, gli archi rossi sono quelli che hanno portato a scoprire nuovi nodi, l'eventuale nuovo nodo visitato è blu, i nodi e gli archi già visitati sono bianchi. Nei seguenti passaggi: 

![[dfs_esempio.png]]

si visita inizialmente il nodo `a`, che viene quindi aggiunto allo stack `S` e all'insieme `VIS` dei nodi visitati; in seguito, nella prima iterazione del ciclo while, si legge proprio il nodo `a` e si sceglie un suo adiacente, in questo caso `b`, che verrà visitato e aggiunto a `S` e `VIS`; nella seconda iterazione, viene letto il nodo `b` dallo stack e si visita l'adiacente `g`. In seguito: 

![[dfs_esempio1.png]]

viene letto il nodo `g` e si visita l'unico suo adiacente non ancora visitato, ossia `c`; a questo punto, lo stack `S` conterrà in ordine i nodi $[a,\,b,\,g,\,c]$, e gli stessi nodi saranno contenuti anche all'interno di `VIS`. Passando alla quarta iterazione del ciclo `while`, viene letto il nodo `c`, e notiamo però che non troviamo adiacenti di `c` che non si trovino in `VIS`: allora `c` verrà rimosso dallo stack. Nell'iterazione seguente, lo stesso accadrà per il nodo `g`, e in seguito:

![[dfs_esempio2.png]]

toccherà la stessa sorte a `b`. Siamo tornati, a questo punto, al nodo di partenza `a`, e siamo obbligati a prendere una strada diversa da quella precedente: l'unico adiacente di `a` che non è stato già visitato infatti è `d`, che verrà quindi aggiunto allo stack `S` (ora, lo stack assume la forma $[a,\,d]$) e all'insieme `VIS`. Da `d`, viene scelto (in modo casuale) il nodo `e` come prossima visita, e in seguito:

![[dfs_esempio3.png]]

il nodo `h`, che si rivela essere, come il nodo `c` poco fa, un vicolo cieco. A questo punto, torniamo al nodo `e` e poi:

![[dfs_esempio4.png]]

scegliamo un'altra strada, stavolta visitando il nodo `i`; da qui, l'unico nodo adiacente e non già visitato è il nodo `f`, che tra l'altro è anche l'ultimo nodo rimasto da visitare nell'intero grafo. Dunque, negli ultimi passaggi:

![[dfs_esempio5.png]]
![[dfs_esempio6.png]]

andremo semplicemente a ripercorrere a ritroso i nodi contenuti in `S`, fino a tornare al nodo di partenza `a`. Infine, dato che abbiamo visitato tutti i nodi del grafo non avremo nodi da visitare partendo da `a` ma avremo svuotato lo stack `S`, l'esecuzione dell'algoritmo termina e viene ritornato `VIS`, che conterrà tutti i nodi del grafo.

Nel caso in cui il grafo sia [[PDA_02 - Grafi#Cos'è un grafo?|diretto]], l'algoritmo non cambierà di implementazione: l'unica differenza starà nel modo in cui verrà eseguito, dato che naturalmente **potrà avanzare lungo gli archi solamente seguendo la loro orientazione**.
___
##### Dimostrazione della correttezza dell'algoritmo DFS

Per poterci affidare all'[[PDA_02 - Grafi#La DFS|algoritmo]] mostrato poco fa, dobbiamo **dimostrare che esso, partendo da un nodo $u$, visiti sempre tutti i nodi raggiungibili da $u$**.

Per fare ciò, supponiamo per assurdo che esista un nodo $z$ raggiungibile da $u$, ma che la DFS non lo visiti. Siccome $z$ è raggiungibile da $u$ sappiamo per certo che esiste un cammino $u_{0},\,u_{1},\,u_{2},\,\dots,\,u_{k}$, dove $u_{0}=u$ e $u_{k}=z$. A questo punto, indichiamo come $u_{i}$ il primo nodo del cammino che non viene visitato dall'algoritmo (banalmente, si ha che $0< i\le k$): per definizione di $u_{i}$, sappiamo che il nodo $u_{i\,-\,1}$ è stato visitato per certo; ora, per natura dell'algoritmo DFS, prima che il nodo $u_{i\,-\,1}$ venga rimosso dallo stack devono essere stati visitati tutti i suoi adiacenti, ed essendo banalmente $u_{i}$ uno di essi, anch'esso dovrà essere stato visitato. Siamo arrivati, così, a una contraddizione della nostra ipotesi per assurdo: dunque, abbiamo dimostrato che **se un nodo $z$ è raggiungibile da $u$, allora la DFS lo visiterà**.

Quindi, se **il grafo non è diretto**, la DFS visita esattamente **tutti i nodi della [[PDA_02 - Grafi#Connettività|componente connessa]] del nodo di partenza**. Se **il grafo è diretto**, la DFS visita **tutti i nodi raggiungibili dal nodo di partenza tramite cammini orientati** che, in generale, sono un soprainsieme della componente fortemente connessa di $u$.
___
##### Efficienza della DFS

Ma **quanto è efficiente l'algoritmo della DFS?** Per valutare la complessità della DFS, dobbiamo precisare alcuni dettagli implementativi:
- per mantenere l'insieme dei nodi visitati, `VIS` può essere implementato come un **array di valori booleani**, con un valore per ogni nodo e con tutti i valori inizializzati a `false`, in modo che ogni volta che un nuovo nodo `w` viene visitato si ponga `VIS[w] = true` (tramite questa implementazione, **l'aggiornamento e il controllo relativo alla visita di un nodo hanno entrambi un costo costante**);
- lo stack `S` può essere facilmente implementato in modo che **tutte le operazioni `push`, `pop` e `top` abbiano costo costante**.

Dunque, riprendendo lo pseudocodice dell'algoritmo, possiamo cominciare ad associare a ciascuna istruzione il relativo costo computazionale:

```
DFS(G: grafo, u: nodo di partenza):
	VIS <- insieme dei nodi visitati, inizialmente vuoto
	S <- stack del cammino, inizialmente vuoto
	
	S.push(u)                                                  # Ө(1)
	VIS.add(u)                                                 # Ө(1)
	
	while (S is not empty):
		v <- S.top()                                           # Ө(1)
		if (esiste un adiacente w di v, con w non in VIS):     
			VIS.add(w)                                         # Ө(1)
			S.push(w)                                          # Ө(1)
		else:
			S.pop()                                            # Ө(1)
	
	return VIS                                                 # Ө(1)
```

Rimane, a questo punto, da chiarire il costo complessivo del ciclo `while`. Ad ogni iterazione del ciclo, possono verificarsi due scenari: o viene visitato un nuovo nodo, o viene estratto un nodo dallo stack. 

[APPUNTI: 02, pag. 5]
___
##### Versione ricorsiva della DFS

[APPUNTI: 02, pag. 5]
___
##### Albero di visita

[APPUNTI: 02, pag. 5 - 6]
___
##### Determinazione delle componenti connesse

[APPUNTI: 02, pag. 6]
___
## La BFS


___