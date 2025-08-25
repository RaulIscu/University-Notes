## Cos'è un circuito sequenziale?

Un **circuito sequenziale** è un circuito in cui **gli output dipendono sia dagli input attuali che da quelli precedenti** (esso, dunque, "ricorda" gli input precedenti a quelli attuali, infatti **un circuito sequenziale è dotato di memoria**).

In un circuito sequenziale potrebbero essere ricordati degli input precisi, oppure essi potrebbero essere condensati in un'informazione riassuntiva chiamata lo "**stato**" del sistema. Lo stato di un circuito è, solitamente, rappresentato da una determinata quantità di bit chiamati "**variabili di stato**", che contengono le informazioni relative al funzionamento passato del circuito necessarie per definire il funzionamento futuro dello stesso.
___
## Elemento bistabile

Il componente fondamentale di un circuito dotato di memoria, e dunque di un circuito sequenziale, è un cosiddetto "**elemento bistabile**", ossia un elemento che presenta **due stati stabili e distinti**. Un esempio basilare di un elemento del genere è il seguente:

![[bistable_example.png]]

Come si può notare immediatamente, questo piccolo circuito è costituito da due porte *NOT*, collegate in un loop; possiamo affermare che le due porte in questione sono "**cross-coupled**", in quanto l'output di una è l'input dell'altra e viceversa. Il circuito non presenta input convenzionali, tuttavia tecnicamente presenta due output, ossia $Q$ e il suo complemento. Possiamo visualizzare meglio questa proprietà in un'implementazione equivalente:

![[bistable_example1.png]]

Essendo un circuito ciclico, $Q$ dipenderà dal suo complemento e viceversa. Cerchiamo, dunque, di analizzare il circuito in base a due casistiche, $Q = 0$ e $Q = 1$:
- se $Q = 0$, la porta $I2$ riceverà in input $Q$ e ritornerà $\bar{Q}$, ossia $1$, che verrà ricevuto a sua volta come input da $I1$, che ritornerà $Q$, ossia $0$;
- se $Q = 1$, la porta $I2$ riceverà in input $Q$ e ritornerà $\bar{Q}$, ossia $0$, che verrà ricevuto a sua volta come input da $I1$, che ritornerà $Q$, ossia $1$.

Si noti che entrambe le casistiche hanno un **risultato finale compatibile con le condizioni stabilite inizialmente**: ciò vuol dire che entrambi i casi sono "**stabili**"; inoltre, essendoci due stati stabili per il circuito, si può affermare che esso sia effettivamente **bistabile**.

In generale, un elemento con $N$ stati stabili può "conservare" un numero di bit di informazione pari a $\log_{2}N$. Dunque, un elemento bistabile come quello appena analizzato conserva un bit di informazione, che in questo caso corrisponde all'output $Q$: infatti, conoscere il valore della variabile $Q$ ci consente di sapere tutto il necessario sul passato funzionamento del circuito per predire e conoscere accuratamente il suo funzionamento futuro. Questo perché, se sappiamo che $Q = 0$, vorrà dire che anche in futuro $Q$ rimarrà sempre $0$, e lo stesso vale se $Q = 1$. Anche $\bar{Q}$ è una variabile di stato accettabile, ma la sua considerazione insieme a $Q$ non aggiungerà informazioni ulteriori, dunque sceglierne una rende l'altra trascurabile.

Circuiti sequenziali come quello appena analizzato, seppur utili per conservare un bit di informazione, non sono molto pratici, in quanto non presentano input, e dunque non possono essere effettivamente controllati. Altri componenti, invece, consentono questo controllo proprio disponendo di input manipolabili: i più comuni e diffusi sono i **[[Circuiti sequenziali#Latch|latch]]** e i **[[Circuiti sequenziali#Flip-flop|flip-flop]]**.
___
## Latch

In questa sezione, analizzeremo principalmente due tipi di ***latch***:
1. l'**SR latch**;
2. il **D latch**.
___
#### SR Latch

L'**SR latch** è composto da **due porte *NOR* cross-coupled**. Tale circuito presenta due input ($S$ e $R$, che stanno per "set" e "reset" e danno il nome al latch) e due output ($Q$ e il suo complemento $\bar{ Q}$). Graficamente, un esempio generico di SR latch è il seguente:

![[sr_latch.png]]

Per comprendere meglio il circuito, consideriamo le 4 casistiche possibili in base agli input $S$ e $R$:
- se $S = 0$ e $R = 1$, $N1$ riceve almeno un input `True`, quindi produce un output $Q = 0$ che viene preso in input da $N2$; quest'ultimo, ricevendo due input `False` produrrà un output $\bar{Q} = 1$;
- se $S = 1$ e $R = 0$, $N2$ riceve almeno un input `True`, quindi produce un output $\bar{Q} = 0$ che viene preso in input da $N1$; quest'ultimo, ricevendo due input `False` produrrà un output $Q = 1$;
- se $S = 1$ e $R = 1$, sia $N1$ che $N2$ ricevono almeno un input `True`, quindi entrambi gli output $Q$ e $\bar{Q}$ saranno uguali a $0$;
- se $S = 0$ e $R = 0$, ci troviamo apparentemente bloccati, in quanto sia $Q$ che $\bar{Q}$ rimangono incerti; tuttavia, sappiamo che l'output $Q$ deve risultare o $0$ o $1$, dunque possiamo ricavare il funzionamento del circuito distinguendo questi due sotto-casi:
	1. se $Q = 0$, $N2$ produrrà come output $\bar{Q} = 1$, che porterà $N1$ a restituire invece come output $Q = 0$, rispettando le condizioni iniziali;
	2. se $Q = 1$, $N2$ produrrà come output $\bar{Q} = 0$, che porterà $N1$ a restituire invece come output $Q = 1$, rispettando le condizioni iniziali.

I due sotto-casi del quarto e ultimo caso possono essere riassunti supponendo che $Q$ abbia un qualsiasi valore noto precedente a quello corrente. Possiamo chiamare questo valore $Q_{prev}$, ed esso rappresenterà semplicemente la variabile di stato del latch. Dunque, in "assenza" di input, ossia quando $S$ e $R$ sono uguali a $0$, il circuito ricorda il suo stato precedente, dato da $Q_{prev}$, e rimane in esso. Possiamo riassumere i casi analizzati in una tavola di verità, che ci aiuterà a spiegare meglio il funzionamento dell'SR latch:

![[sr_latch_truth.png]]

Ripensando al significato delle lettere $S$ e $R$, comprendiamo che "settare" un valore vuol dire renderlo `True`, mentre "resettarlo" vuol dire riportarlo a `False`. Sapendo ciò, notiamo che se $R = 1$ l'output $Q$ sarà uguale a $0$ (`False`), mentre se $S = 1$ e $R = 0$, l'output $Q$ sarà uguale a $1$ (`True`); il caso in cui entrambi gli input $S$ e $R$ sono uguali a $1$, in realtà, non ha concretamente senso, in quanto implica che il circuito in questione venga settato e resettato allo stesso tempo; se, invece, nessun input viene attivato, il latch ricorda il suo stato precedente, e si attiene ad esso.

Solitamente, un SR latch viene costruito con le porte *NOR* che abbiamo visto, ma esso può potenzialmente essere costruito in vari altri modi. In generale, qualsiasi circuito che rispetti la tavola di verità appena analizzata può essere definito SR latch, e graficamente rappresentato con il seguente simbolo:

![[sr_latch_symbol.png]]
___
#### D Latch

L'SR latch risulta non ottimale in molte situazioni, proprio per il fatto che il circuito si comporta in maniera anomala nel caso in cui sia $S$ che $R$ sono attivi; inoltre, ciascuno dei due input determina non solo quale sarà lo stato del circuito, ma anche quando questo andrà a cambiare, mentre solitamente è più comodo che queste due incognite vengano risolte separatamente. È per compensare a questi problemi che viene introdotto il "**D latch**", dove $D$ sta per "data". Anche questo circuito presenta due input, ossia $D$ (che controlla lo stato del latch) e $CLK$, che sta per "clock" (che controlla quando lo stato del latch va a cambiare). Graficamente, un generico D latch può essere implementato nel modo seguente:

![[d_latch.png]]

Per comprendere meglio il circuito, consideriamo le casistiche possibili in base agli input $D$ e $CLK$:
- se $CLK = 0$, allora $S = R = 0$ indipendentemente dal valore di $D$;
- se $CLK = 1$ e $D = 0$, allora $S = 0$ e $R = 1$;
- se $CLK = 1$ e $D = 1$, allora $S = 1$ e $R = 0$.

Possiamo riassumere i casi analizzati in una tavola di verità, che ci aiuterà a spiegare meglio il funzionamento del D latch:

![[d_latch_truth.png]]

Avendo i valori di $S$ e $R$, naturalmente, gli output $Q$ e $\bar{Q}$ verranno determinati in base alla tavola di verità dell'SR latch. Si nota, dunque, che se $CLK = 0$ si ha che $Q = Q_{prev}$ (il circuito, dunque, ricorderà il suo valore precedente); invece, se $CLK = 1$, allora si ha che $Q = D$. Mediante questo meccanismo, il D latch evita il caso anomalo dell'attivazione contemporanea di $S$ e $R$. Insomma, in un D latch, **l'input $CLK$ è quello che determina quando l'informazione** ($D$) **entra nel circuito**: per questo, quando $CLK = 1$, il circuito viene detto "**trasparente**", in quanto si comporta come un *[[Porte logiche#Porte logiche con un input *NOT* e *BUFFER*|BUFFER]]* e trasmette come output il valore di $D$; quando, invece, $CLK = 0$, il circuito viene detto "**opaco**", in quanto non lascia passare l'informazione $D$ e l'output mantiene il suo valore precedente.

In generale, qualsiasi circuito che rispetti la tavola di verità appena analizzata può essere definito D latch, e graficamente rappresentato con il seguente simbolo:

![[d_latch_symbol.png]]
___
## Flip-flop

In questa sezione, analizzeremo principalmente quattro tipi di **flip-flop** o di componenti derivate da essi:
1. il **D flip-flop**;
2. il **registro**;
3. l'**enabled flip-flop**;
4. il **resettable flip-flop**.
___
#### D Flip-Flop

Un **D flip-flop** consiste, sostanzialmente, in due [[Circuiti sequenziali#D Latch|D latch]], collegati in modo che l'output $Q$ del primo sia l'input $D$ del secondo, e controllati da $CLK$ complementari. I due latch utilizzati vengono chiamati rispettivamente $L1$ e $L2$, e il nodo che li collega viene generalmente indicato con $N1$. Graficamente, un D flip-flop viene rappresentato con il diagramma seguente:

![[d_flipflop.png]]

e può essere riassunto in maniera compatta con il simbolo seguente:

![[d_flipflop_symbol.png]]

Ancora, se l'output $\bar{Q}$ è trascurabile, la simbologia può essere ancora più condensata:

![[d_flipflop_symbolcondensed.png]]

In un D flip-flop, il latch $L1$ (ossia, generalmente, quello collegato all'input $D$) viene detto "**master**", mentre il latch $L2$ (ossia, generalmente, quello il cui input è collegato al nodo $N1$) viene detto "**slave**". Quando $CLK = 0$, il master è trasparente e lo slave è opaco: dunque, l'input $D$ viene propagato al nodo $N1$ attraverso il latch $L1$; quando $CLK = 1$, il master è opaco e lo slave è trasparente: dunque, il valore propagato al nodo $N1$ viene propagato all'output $Q$, mentre $N1$ "perde il collegamento" con l'input $D$. Questo meccanismo implica che il valore assunto da $D$ immediatamente prima del passaggio di $CLK$ da $0$ a $1$ viene trasmesso a $Q$ immediatamente dopo tale passaggio; invece, in qualsiasi altro momento, $Q$ mantiene il suo valore precedente. Si può riassumere il funzionamento appena spiegato affermando che **un D flip-flop trasmette $D$ a $Q$ durante il "rising edge" di $CLK$, e mantiene il suo stato precedente in qualsiasi altro momento**. 

Il **rising edge** di $CLK$, per comodità, viene spesso detto semplicemente "**clock edge**". Il D flip-flop in sé, inoltre, può essere chiamato anche "**master-slave flip-flop**", "**edge-triggered flip-flop**" o "**positive edge-triggered flip-flop**".
___
#### Registro

Un **registro** a $N$ bit consiste in un gruppo di $N$ flip-flop che condividono lo stesso segnale $CLK$, in modo tale che tutti i bit di output del registro vengano aggiornati sempre nello stesso momento. Di seguito, ad esempio, il diagramma di un registro a 4 bit:

![[register_example.png]]

Vediamo, inoltre, che tale rappresentazione può essere compattata nella seguente:

![[register_example_symbol.png]]
___
#### Enabled Flip-Flop

Un **enabled flip-flop** consiste nell'unione tra un classico D flip-flop e un nuovo input chiamato "enable" (o $EN$), che determina se l'informazione fornita dall'input $D$ viene o meno trasmessa attraverso il circuito durante il clock edge: dunque, quando $EN = 1$, l'enabled flip-flop si comporta come un normalissimo D flip-flop, mentre quando $EN = 0$, il circuito ignora completamente il valore di $CLK$ e mantiene il suo stato precedente. Un enabled flip-flop può essere implementato in vari modi, tra cui:

![[enabled_flipflop.png]]

È possibile riassumere una qualsiasi di queste implementazioni con il seguente simbolo:

![[enabled_flipflop_symbol.png]]

Potrebbe tornare utile precisare che, nella seconda possibile implementazione, si deve fare attenzione a non variare il valore di $EN$ nel momento in cui $CLK = 1$, in quanto fare ciò potrebbe causare un glitch. È saggio, generalmente, evitare di implementare logica che coinvolga il segnale $CLK$, in quanto potrebbe spesso portare a problematiche del genere e quasi sicuramente a errori di tempo.
___
#### Resettable Flip-Flop

Un **resettable flip-flop** è simile a un enabled flip-flop, nel senso che anch'esso aggiunge un nuovo input a un D flip-flop di partenza; in questo caso, però, l'input in questione è $RESET$, ed esso si trova a stretto contatto con $D$ piuttosto che con $CLK$. Infatti, quando $RESET = 0$, il circuito si comporta come un normalissimo D flip-flop; quando, invece, $RESET = 1$, il circuito ignora il valore di $D$ e l'output $Q$ viene forzato a $0$. Graficamente, un resettable flip-flop può essere implementato nel modo seguente:

![[resettable_flipflop.png]]

e condensato mediante la seguente simbologia:

![[resettable_flipflop_symbols.png]]

Circuiti del genere possono venire categorizzati in:
- **sincroni**, che possono essere resettati solo in concomitanza con il clock edge;
- **asincroni**, che si resettano non appena $RESET = 1$, indipendentemente dal valore di $CLK$.

In particolare, l'implementazione fornita prima mostra un resettable flip-flop sincrono.
___
## Circuiti astabili

In generale, un circuito sequenziale è composto da elementi non combinatori, e dunque il cui *output* non può sempre essere determinato a priori semplicemente analizzando l'*input* attuale. Ci sono, partendo da questa caratteristica, alcuni casi "estremi" di circuiti sequenziali, che si comportano in maniere anomale o imprevedibili; vediamo alcuni esempi.

Supponiamo di avere un circuito formato esclusivamente da tre porte *NOT* collegate in un ciclo chiuso, in modo che l'*output* dell'ultimo *NOT* diventi l'*input* del primo, nel modo seguente:

![[astable_circuit_example.png]]

Se ponessimo, inizialmente, *X = 0*, si avrebbe di conseguenza *Y = 1*, seguito da *Z = 0*, che porta così a *X = 1*; notiamo subito un'incongruenza con le nostre condizioni iniziali, che ci porta ad affermare che il circuito considerato non presenta stati stabili, e in quanto tale viene definito "**instabile**" o "**astabile**". In particolare, analizzando le forme d'onda relative a tale circuito (supponendo che ogni porta *NOT* ha un *propagation delay* di 1 ns), si nota che esso presenta un funzionamento ciclico e periodico. Infatti:

![[astable_circuit_examplewave.png]]

Un circuito del genere viene definito **oscillatore ad anello** (o ***ring oscillator***), e il suo periodo dipende dal *propagation delay* delle porte logiche coinvolte al suo interno; in questo caso, si può notare che ogni nodo del circuito oscilla tra i valori 0 e 1 con un periodo di 6 ns.

Ancora, supponiamo di avere un circuito simile, per molti versi, a un canonico *D latch* ma con delle variazioni:

![[racecondition_example.png]]

All'apparenza, un circuito del genere sembra essere un'implementazione più efficiente di un regolare *D latch*, in quanto vengono utilizzate meno porte logiche. Tuttavia, se si tengono in conto i possibili *delay*, si può incorrere in delle problematiche. Ad esempio, consideriamo una condizione iniziale in cui *CLK = D = 1*: in questo caso, il *latch* risulta essere trasparente, e trasmette quindi il valore di *D* a *Q*, portando *Q = 1*. Supponiamo, adesso, che *CLK* passi da 1 a 0: il circuito, se funzionasse come un *D latch*, dovrebbe ricordare il suo valore precedente e mantenere *Q = 1*; tuttavia, se consideriamo la porta *NOT* come avente un *delay* maggiore rispetto alle porte *AND* e all'*OR*, allora N1 e, conseguentemente, *Q* passerebbero a 0 prima ancora che *CLK' = 1*, e si arriverebbe quindi a un'anomalia rispetto al funzionamento previsto.

Si dice che un circuito con problematiche del genere presenta una ***race condition***; inoltre, esso rappresenta un esempio di circuito "**asincrono**". I circuiti asincroni in questo senso presentano spesso problemi simili, e il loro funzionamento è particolarmente influenzato dalle condizioni in cui si trovano (temperatura, voltaggio, ecc. ecc.) nonché dal modo in cui i suoi singoli elementi sono costruiti.
___
## Circuiti sequenziali sincroni e asincroni

I due esempi precedenti contenevano dei cosiddetti "**percorsi ciclici**", ossia percorsi in cui gli *output* di un circuito vengono trasmessi direttamente ai suoi *input* in maniera ciclica. Questa caratteristica risulta essere la principale differenza tra un circuito sequenziale e un [[Circuiti combinatori|circuito combinatorio]]: ricordiamo, infatti, che un circuito combinatorio non può contenere cicli al suo interno. In un circuito combinatorio, l'*output* darà sempre il risultato previsto entro un determinato *propagation delay*; in un circuito sequenziale, invece, ciò non è sempre garantito a causa della possibilità di problematiche simili a quelle mostrate negli esempi precedenti.

Per tentare di ovviare a questo difetto, si possono inserire, nella progettazione di un circuito, dei [[Flip-flop|registri]] che "interrompano" un determinato percorso ciclico. Facendo ciò, il circuito in questione diventa sostanzialmente un insieme di logica combinatoria e registri, che conservano lo stato del circuito stesso, stato che può così variare solo durante il *clock edge*. Per questo, affermiamo che lo stato è "**sincronizzato**" con il *CLK*. In questo modo, se la variazione di *CLK* avviene con un periodo sufficientemente lungo, i vari segnali del circuito (e, in particolare, coinvolti nei registri) avranno il tempo di assestarsi al valore desiderato, eliminando qualsiasi possibilità di *race condition*.

Dunque, sapendo che un circuito sequenziale dovrebbe avere un numero finito di stati stabili distinti, possiamo affermare che un **circuito sequenziale sincrono** presenterà sempre un *input* *CLK* che indicherà precisamente i tempi in cui le transizioni tra questi stati possono avvenire. Per indicare e distinguere questi stati, utilizziamo i termini "***current state***" per lo stato attuale del circuito e "***next state***" per lo stato che assumerà il circuito in corrispondenza del prossimo *clock edge*. La [[Circuiti|specifica di funzione]] di un circuito sequenziale sincrono dovrà dare informazioni sul *next state* e sul valore di ogni *output* per ogni possibile combinazione di *current state* e di *input*; la [[Circuiti|specifica di tempo]], infine, è definita da un intervallo di tempo che ha come estremo superiore ***t`pcq`***, ossia il tempo  massimo che intercorre tra l'aggiornamento di *CLK* e il raggiungimento da parte di *Q* del suo valore finale, e come estremo inferiore ***t`ccq`***, ossia il tempo minimo che intercorre tra l'aggiornamento di *CLK* e l'inizio dell'aggiornamento di *Q*. Questi due valori di tempo corrispondono ai valori ***t`pd`*** e ***t`cd`*** relativi ai [[Tempi (combinatori)|circuiti combinatori]], e oltre ad essi sono importanti anche ***t`setup`*** e ***t`hold`***, che indicano quando gli *input* devono rimanere stabili relativamente al *clock edge*.

In generale, un circuito sequenziale sincrono è tale se rispetta le seguenti condizioni:
- ogni elemento del circuito o è un registro o è un elemento combinatorio;
- almeno un elemento del circuito è un registro;
- tutti i registri ricevono in *input* il medesimo segnale *CLK*;
- ogni percorso ciclico contiene almeno un registro.

Intuitivamente, un circuito sequenziale che non rispetta queste condizioni non è sincrono, ma viene detto **asincrono**.

Un *flip-flop* è, di fatto, il più semplice dei circuiti sequenziali sincroni: presenta un *input* (*D*), un *CLK*, un *output* (*Q*, che include anche *Q'*) e due possibili stati (0 e 1). La specifica di funzione di un *flip-flop* mostra che il *next state* è dato da *D*, mentre il *current state* corrisponde a *Q*. Possiamo indicare *current state* e *next state* in maniera veloce come *S* e *S'*.

Un altro tipo comune di circuito sequenziale sincrono è la categoria delle "*finite state machines*", o "***[[FSM]]***".
___

