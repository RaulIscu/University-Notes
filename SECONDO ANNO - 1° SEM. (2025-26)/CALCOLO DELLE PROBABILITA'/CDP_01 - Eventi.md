## Cos'è un evento?

In questo corso, si approfondirà il **calcolo delle probabilità**, una branca della matematica che, come suggerisce il nome, studia la probabilità che avvenga un determinato "**evento**". La definizione di "evento" è particolarmente generica e permissiva: sostanzialmente, possiamo considerare come tale un **qualcosa che ha una certa probabilità di avvenire**, un possibile risultato di un'azione.

Pensiamo, ad esempio, di osservare il lancio di due dadi, e di indicare con $X_{1}$ il punteggio ottenuto dal primo dado e con $X_{2}$ quello ottenuto dal secondo. Eseguendo questo "esperimento", si potranno ottenere diversi risultati, come ad esempio:
- $A$, in cui il punteggio del primo dado è minore o uguale al punteggio del secondo ($X_{1} \le X_{2}$);
- $B$, in cui la somma dei punteggi ottenuti è pari ($X_{1} + X_{2} \text{\, è pari}$);
- $C$, in cui il punteggio ottenuto dal primo dado è strettamente maggiore di 3 ($X_{1} > 3$);
- $D$, in cui il punteggio ottenuto dal primo dado è 2 e il punteggio ottenuto dal secondo è 5 ($X_{1} = 2,\, X_{2} = 5$).

Ciascuna di queste situazioni è un singolo **evento**: dunque, possiamo vedere un evento anche come una **proposizione logica**, che risulta essere vera se l'evento si verifica e falsa se l'evento non si verifica.

Per il momento, possiamo indicare con il simbolo $\mathcal{E}$ la "**famiglia**" dei possibili eventi distinti in un esperimento del genere. Come è facile notare, la famiglia costituita dagli eventi elencati poco fa è una **famiglia finita**; analogamente, per ora ci si limiterà a trattare esempi con famiglie di eventi finite, ma è possibile anche avere un esperimento che generi una famiglia non finita.
___
## Eventi dal punto di vista logico e insiemistico

Avendo definito un evento anche come proposizione logica, risulta naturale introdurre all'interno di una famiglia di eventi anche le **operazioni logiche**, in particolare:
- la **somma logica**, detta anche **OR** e indicata con il simbolo $\lor$;
- il **prodotto logico**, detto anche **AND** e indicato con il simbolo $\land$;
- la **negazione**, detta anche **NOT** e indicata con il simbolo $\lnot$.

Dunque, siano $E_{1}$ ed $E_{2}$ due eventi della famiglia di eventi $\mathcal{E}$, si ha che la somma logica $E_{1} \lor E_{2}$ corrisponde all'evento:
$$\{\text{si è verificato almeno uno dei due eventi }E_{1}\text{ ed }E_{2}\}$$
Invece, il prodotto logico $E_{1}\land E_{2}$ corrisponde all'evento:
$$\{\text{si sono verificati entrambi gli eventi }E_{1}\text{ ed }E_{2}\}$$
Infine, la negazione $\lnot E_{1}$ corrisponde all'evento:
$$\{\text{non si è verificato l'evento }E_{1}\}$$
##### Eventi elementari e composti

> Un evento $E\in\mathcal{E}$ si dice "**composto**" se esistono almeno due eventi $E_{1},\,E_{2}\in\mathcal{E}$ tali per cui:
> $$E = E_{1}\lor E_{2}\,\,\,\,\,\,\,\,\,\,\text{con }E\neq E_{1},\,E\neq E_{2}$$
> Qualsiasi evento non sia composto viene detto "**semplice**", o "**elementare**".

Ad esempio, supponendo di lanciare un dado a sei facce, l'evento $E=\{X_{1}>3\}$ è un evento composto, dato che in tale esperimento gli eventi elementari sono:
$$\{X_{1}=1\}, \{X_{1}=2\},\,\dots,\,\{X_{1}=6\}$$
e l'evento $E$ può essere riscritto come:
$$E=\{X_{1}>3\}=\{X_{1}=4\}\lor\{X_{1}=5\}\lor\{X_{1}=6\}$$
Supponendo, in un altro esempio, di lanciare due dadi a sei facce, si ottiene stavolta che gli eventi elementari sono tutti gli eventi del tipo:
$$\{X_{1}=n,\,X_{2}=m\}\,\,\,\,\,\,\,\,\,\,\text{con n} = 1,\,2,\,\dots,\,6\text{ \,e\, m}=1,\,2,\,\dots,\,6$$
ossia eventi in cui entrambi i dadi assumono un valore ben preciso; in questo contesto, invece, un evento $E$ del tipo $\{X_{1}=n\}$ risulta essere un evento composto, dato che può essere riscritto come:
$$E=\{X_{1}=n\}=\bigvee_{k\,=\,1}^{6}\,\{X_{1}=n,\,X_{2}=k\}$$
> L'insieme $\Omega = \{\omega_{1},\,\omega_{2},\,\dots,\,\omega_{k}\}$, che contiene tutti gli eventi elementari di un esperimento, viene detto "**spazio campione**" per tale esperimento.

Avendo uno spazio campione $\Omega$, indichiamo con il simbolo $\mathcal{P}(\Omega)$ la "**famiglia delle parti**" di $\Omega$, ossia la famiglia di **tutti i possibili sottoinsiemi** di $\Omega$, e per ogni $E\in \mathcal{P}(\Omega)$ si indica con il simbolo $|\,E\,|$ la "**cardinalità**" di $E$, ossia il numero di elementi contenuti al suo interno.
___
##### Da operazioni logiche a operazioni insiemistiche

Per definizione, gli elementi di uno spazio campione $\Omega$ sono gli eventi elementari di un esperimento. Notiamo, a questo punto, che esiste una **corrispondenza biunivoca tra i sottoinsiemi di $\Omega$ e gli eventi composti**: infatti, è possibile associare a ciascun evento composto il sottoinsieme di $\Omega$ che contiene gli eventi elementari che lo compongono; viceversa, è possibile associare a ciascun sottoinsieme di $\Omega$ l'evento composto definito dalla somma logica dei suoi elementi.

Ad un qualsiasi evento elementare $\omega_{i} \in \Omega$, facciamo corrispondere l'insieme $\{\omega_{i}\}\in\mathcal{P}(\Omega)$ (si ricorda che un insieme contenente un unico elemento viene definito "**singoletto**" o "**singleton**"); più in generale, dato un evento $E\in\mathcal{E}$, possiamo indicare con **$\mathcal{H}(E)$** il **corrispondente sottoinsieme di $\Omega$** ottenuto mediante la stessa operazione.

Ci si rende facilmente conto che, nella corrispondenza univoca appena definita, **le operazioni logiche $\lor$, $\land$ e $\lnot$ definite su $\mathcal{E}$ corrispondono rispettivamente alle operazioni insiemistiche $\cup$, $\cap$ e $\complement$ definite su $\mathcal{P}(\Omega)$**. Infatti, si possono affermare le seguenti uguaglianze:
$$\begin{align} &\mathcal{H}(E_{1}\lor E_{2}) = \mathcal{H}(E_{1})\cup\mathcal{H}(E_{2})\\&\mathcal{H}(E_{1}\land E_{2}) = \mathcal{H}(E_{1})\cap\mathcal{H}(E_{2})\\&\mathcal{H}(\lnot E) = \complement(\mathcal{H}(E)) \end{align}$$
Dunque, per semplicità, da questo momento in poi ci si riferirà in maniera univoca a eventi e a sottoinsiemi di $\Omega$, si tralasceranno i simboli $\mathcal{E}$,  $\lor$, $\land$, $\lnot$ e $\mathcal{H}(E)$ e si continuerà la trattazione utilizzando solamente le nozioni relative ai sottoinsiemi di $\Omega$ e alle operazioni tra sottoinsiemi.

Ciononostante, rimane importante e conveniente avere ben presente il "**significato logico**" di tali nozioni, e a tal proposito possiamo attribuire un'**interpretazione di tipo logico a varie nozioni di tipo insiemistico**, come le seguenti:
- dire che "**$A\subseteq B$**" equivale a dire che **ogni evento elementare che verifica $A$ verifica anche $B$**, ossia che il verificarsi di $A$ implica il verificarsi di $B$, e dunque possiamo interpretare tale relazione dal punto di vista logico come "**$\text{A implica B}$**";
- dire che "**$\Omega\text{ è un evento vero, qualunque evento elementare si verifichi}$**", in quanto esso contiene tutti gli eventi elementari che possono verificarsi, può essere interpretato dal punto di vista logico affermando che "**$\Omega \text{ è un evento certo}$**";
- dire che "**$\text{l'insieme vuoto } \emptyset \text{ è un evento che non è mai verificato}$**", in quanto esso non contiene alcun evento elementare possibile, può essere interpretato dal punto di vista logico affermando che "$\emptyset \text{ è un evento impossibile}$";
- dire che "**$A\cup B=\Omega$**" equivale a dire che **l'evento costituito dal verificarsi di almeno uno dei due eventi $A$ e $B$ coincide con l'evento certo $\Omega$**, e dunque possiamo interpretare tale relazione dal punto di vista logico come "**$A$ e $B$ sono eventi esaustivi**", ossia eventi tali per cui **è certo che si verifichi almeno uno dei due**;
- dire che "**$A\cap B=\emptyset$**" equivale a dire che **l'evento costituito dal verificarsi di entrambi gli eventi $A$ e $B$ coincide con l'evento impossibile $\emptyset$**, e dunque possiamo interpretare tale relazione dal punto di vista logico come "**$A$ e $B$ sono eventi incompatibili**", ossia eventi tali per cui **è certo che si verifichi al più uno dei due**.
_____
##### Partizione dell'evento certo

> Data una collezione di sottoinsiemi $\mathcal{H}=\{H_{1},\,H_{2},\,\dots,\,H_{m}\}$ dello spazio campione $\Omega$, tale collezione costituisce una "**partizione di $\Omega$**" se e solo se **gli insiemi $H_{1},\,H_{2},\,\dots,\,H_{m}$ sono disgiunti** (non hanno elementi comuni) **a due a due** e se **la loro unione coincide con $\Omega$**, ossia vale che:
> $$H_{l_{1}}\cap H_{l_{2}}=\emptyset\,\,\,\text{per }l_{1}\neq l_{2}\,\,\,\,\,\bigwedge\,\,\,\,\,\bigcup_{l\,=\,1}^{m}H_{l}=\Omega$$
> Gli insiemi $H_{l}$ vengono anche detti **elementi** della partizione $\mathcal{H}$.

Interpretando $H_{1},\,H_{2},\,\dots,\,H_{m}$ come eventi, si può dire che due eventi appartenenti a una partizione $\mathcal{H}$ sono **a due a due incompatibili** (dunque, è impossibile che se ne verifichino due contemporaneamente) **ed esaustivi** (dunque, è certo che se ne verifichi almeno uno). In altre parole, **è certo che si verifichi uno e uno soltanto degli eventi $H_{1},\,H_{2},\,\dots,\,H_{m}$**.

Per comprendere meglio questo concetto, vediamo un esempio. Supponiamo di avere 4 palline numerate da $1$ a $4$ in una teca, e di volerle estrarre una alla volta da quest'ultima senza reinserirle al suo interno: tutti i possibili ordini di estrazione si possono ottenere con le varie permutazioni della sequenza $\{1, 2, 3, 4\}$, e vanno a comporre lo spazio campione $\Omega$. A questo punto, possiamo definire la famiglia $\mathcal{H} = \{H_{1},\,H_{2},\,H_{3},\,H_{4}\}$, dove abbiamo che:
$$\begin{align} &H_{1}=\{\text{Il primo numero estratto è l'1}\}\\&H_{2}=\{\text{Il primo numero estratto è il 2}\}\\&H_{3}=\{\text{Il primo numero estratto è il 3}\}\\&H_{4}=\{\text{Il primo numero estratto è il 4}\} \end{align}$$
Ciascuno di questi 4 insiemi rappresenta un [[CDP_01 - Eventi#Eventi elementari e composti|evento composto]], ciascuno definito dall'unione di 6 eventi; si ha, inoltre, che la famiglia $\mathcal{H}$ rappresenta a tutti gli effetti una partizione di $\Omega$, in quanto gli elementi della partizione ($H_{1},\,H_{2},\,H_{3}$ e $H_{4}$) sono esaustivi, ossia la loro unione coincide con $\Omega$, e sono incompatibili a due a due.
___
## Proprietà relative alle operazioni insiemistiche

Avendo introdotto l'[[CDP_01 - Eventi#Da operazioni logiche a operazioni insiemistiche|interpretazione insiemistica degli eventi]], per semplificare le operazioni relative agli stessi ricordiamo in questo capitolo alcune **proprietà** per le principali operazioni insiemistiche.

La prima proprietà che riportiamo è la **proprietà distributiva dell'unione rispetto all'intersezione**, che afferma che l'intersezione tra un insieme e un'unione di altri due insiemi equivale all'unione tra le intersezioni del primo con gli altri due insiemi presi singolarmente, o formalmente che:
$$(A\cup B)\cap C\,=\,(A\cap C)\cup(B\cap C)$$
In seguito, vediamo la **proprietà distributiva dell'intersezione rispetto all'unione**, che afferma pressoché la stessa cosa ma con gli operatori invertiti:
$$(A\cap B)\cup C\,=\,(A\cup C)\cap(B\cup C)$$
Infine, vediamo la **legge di De Morgan**, che afferma che il complementare dell'intersezione tra due insiemi equivale all'unione tra i complementari degli stessi due insiemi, o formalmente che:
$$\complement(A\cap B)=\complement(A)\cup\complement(B)\,\,\,\,\,\text{che equivale a dire che}\,\,\,\,\,A\cap B=\complement(\complement(A)\cup\complement(B))$$
Per brevità, possiamo scrivere $\overline{A}$ al posto di $\complement(A)$, e riscrivere quindi l'enunciato precedente nel modo seguente:
$$\overline{A\cap B}=\overline{A}\cup\overline{B}\,\,\,\,\,\text{che equivale a dire che}\,\,\,\,\,A\cap B=\overline{(\overline{A}\cup\overline{B})}$$
Le proprietà appena esposte si estendono per induzione a famiglie finite di $l$ insiemi (ma valgono anche per famiglie infinite):
$$\begin{align} &(\bigcup_{i\,\subset\,l}A_{i}) \cap C\,\,=\,\,\bigcup_{i\,\subset\,l} (A_{i}\cap C)\\&(\bigcap_{i\,\subset\,l}A_{i})\cup C\,\,=\,\,\bigcap_{i\,\subset\,l}(A_{i}\cup C)\\&\overline{(\bigcap_{i\,\subset\,l}A_{i})}=\bigcup_{i\,\subset\,l}\overline{A_{i}} \end{align}$$
[esercizi: pag. 14/16]
___

