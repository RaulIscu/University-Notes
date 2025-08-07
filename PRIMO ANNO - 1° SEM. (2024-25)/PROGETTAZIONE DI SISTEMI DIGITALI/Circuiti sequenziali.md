## Cos'è un circuito sequenziale

Un **circuito sequenziale** è un circuito in cui gli *output* dipendono sia dagli *input* attuali che da quelli precedenti (esso, dunque, "ricorda" gli *input* precedenti a quelli attuali, infatti un circuito sequenziale è dotato di memoria).

In un circuito sequenziale potrebbero essere ricordati degli *input* precisi, oppure essi potrebbero essere condensati in un'informazione riassuntiva chiamata lo "**stato**" del sistema. Lo stato di un circuito è, solitamente, rappresentato da una determinata quantità di bit chiamati "**variabili di stato**", che contengono le informazioni relative al funzionamento passato del circuito necessarie per definire il funzionamento futuro dello stesso.
___
Il componente fondamentale di un circuito dotato di memoria, e dunque di un circuito sequenziale, è un "**elemento bistabile**", ossia un elemento che presenta due stati stabili e distinti. Un esempio basilare di un elemento del genere è il seguente:

![[bistable_example.png]]

Come si può notare immediatamente, questo piccolo circuito è costituito da due porte *NOT*, collegate in un *loop*; possiamo affermare che le due porte in questione sono "***cross-coupled***", in quanto l'*output* di una è l'*input* dell'altra e viceversa. Il circuito non presenta *input*, tuttavia tecnicamente presenta due *output*, ossia Q e il suo complemento. Possiamo visualizzare meglio questa proprietà in un'implementazione equivalente:

![[bistable_example1.png]]

Essendo un circuito ciclico, Q dipenderà dal suo complemento e viceversa. Cerchiamo, dunque, di analizzare il circuito in base a due casistiche, Q = 0 e Q = 1:
- se Q = 0, la porta I2 riceverà in *input* Q e ritornerà Q', ossia 1, che verrà ricevuto a sua volta come *input* da I1, che ritornerà Q, ossia 0;
- se Q = 1, la porta I2 riceverà in *input* Q e ritornerà Q', ossia 0, che verrà ricevuto a sua volta come *input* da I1, che ritornerà Q, ossia 1.

Si noti che entrambe le casistiche hanno un risultato finale che coincide con le condizioni stabilite inizialmente: ciò vuol dire che entrambi i casi sono "**stabili**"; inoltre, essendoci due stati stabili per il circuito, si può affermare che esso sia effettivamente bistabile.

In generale, un elemento con *N* stati stabili può "conservare" un numero di bit di informazione pari a log₂*N*. Dunque, un elemento bistabile come quello appena analizzato conserva un bit di informazione, che in questo caso corrisponde all'*output* Q: infatti, conoscere il valore della variabile Q ci consente di sapere tutto il necessario sul passato funzionamento del circuito per predire e conoscere accuratamente il suo funzionamento futuro. Questo perché, se sappiamo che Q = 0, vorrà dire che anche in futuro Q rimarrà sempre 0, e lo stesso vale se Q = 1. Anche Q' è una variabile di stato accettabile, ma la sua considerazione insieme a Q non aggiungerà informazioni ulteriori, dunque sceglierne una rende l'altra trascurabile.
___
Circuiti sequenziali come quello appena analizzato, seppur utili per conservare un bit di informazione, non sono molto pratici, in quanto non presentano *input*, e dunque non possono essere effettivamente controllati. Altri componenti, invece, consentono questo controllo proprio disponendo di *input* manipolabili: i più comuni e diffusi sono i *[[Latch|latch]]* e i *[[Flip-flop|flip-flop]]*.
___
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

