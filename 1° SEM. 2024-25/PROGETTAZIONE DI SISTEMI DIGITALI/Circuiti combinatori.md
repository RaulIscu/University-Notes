Un **circuito combinatorio** è un circuito in cui gli *output* dipendono esclusivamente dagli *input* attuali (esso non "ricorda" gli *input* precedenti a quelli attuali, infatti un circuito combinatorio è privo di memoria). Dunque, gli *output* vengono ottenuti "combinando" e manipolando i valori presi in *input*. Un esempio basilare di circuito combinatorio può essere una qualsiasi [[Porte logiche|porta logica]].

La specifica di funzione di un circuito combinatorio esprime gli *output* in funzione degli *input*. La specifica di tempo, invece, risulterà in un intervallo di tempo delimitato dal minimo e dal massimo *delay* tra rilevamento degli *input* e restituzione degli *output*.
___
Per costruire un circuito combinatorio, è importante seguire le regole della **composizione combinatoria**. Le principali direttive da tenere a mente sono le seguenti:
- ogni elemento di un circuito combinatorio dev'essere anch'esso combinatorio;
- ogni nodo di un circuito combinatorio o trasporta un *input* nel circuito o è connesso a esattamente un *output* di un elemento del circuito;
- un circuito combinatorio non può contenere cicli, e ogni percorso possibile all'interno del circuito può passare per un nodo del circuito al massimo una volta.
___
Graficamente, un circuito combinatorio viene rappresentato con il rettangolo tipico del circuito generico, e racchiusa al suo interno la dicitura "***CL***" (che sta per "*combinational logic*"), come nel seguente esempio:

![[combinationalcircuit.png]]

A volte, per semplificare la rappresentazione di un circuito combinatorio, si riassumono più *input* o più *output* in una sola linea, attraversata da uno *slash* (`/`) e dotata di un numero che indica l'ammontare di segnali racchiusi nella linea stessa; questo tipo di rappresentazione viene definito "***bus***". Ad esempio, un circuito con un *bus* a 3 segnali in *input* e uno a 2 segnali in *output* può essere rappresentato nel modo seguente:

![[combinationalcircuit_bus.png]]

Se il numero di segnali non è rilevante, o se risulta ovvio per qualche motivo, l'indicatore dello stesso può essere omesso.
___
La specifica di funzione di un circuito combinatorio può essere espressa con una tavola di verità o con un'equazione booleana; analizziamo, in particolare, quest'ultimo metodo.

Un'**equazione booleana** viene espressa mediante variabili binarie, che possono dunque essere `True` o `False` (1 o 0). Per poter approfondire al meglio questo tipo di equazione, è opportuno innanzitutto imparare alcuni termini specifici:
- una variabile priva di negazioni si trova nella sua "forma vera" (***true form***);
- il "**complemento**" di una variabile è il suo inverso;
- una variabile (o il suo complemento) viene definita anche come un "***literal***";
- l'*AND* di uno o più *literals* viene anche detto "**prodotto**" o "**implicante**";
- l'*OR* di uno o più *literals* viene anche detto "**somma**";
- un prodotto che coinvolge tutti gli *input* di un determinato circuito viene detto "**mintermine**" (***minterm***) di quel circuito;
- una somma che coinvolge tutti gli *input* di un determinato circuito viene detto "**maxtermine**" (***maxterm***) di quel circuito.

Avendo stabilito questo glossario, risulta ora cruciale stabilire una **gerarchia** dei vari operatori di un'equazione booleana. In una qualsiasi equazione booleana, l'ordine di precedenza dei tre operatori fondamentali è:
1. NOT
2. AND
3. OR

A partire da una tavola di verità, ci sono principalmente due modi di arrivare a un'equazione booleana che descriva il funzionamento di un circuito combinatorio, a seconda della forma di tale equazione e di come ci si arriva:
- la forma "***sum of products***" (o **SOP**);
- la forma "***product of sums***" (o **POS**).

La forma **SOP** consiste nello scrivere l'equazione booleana relativa a un circuito combinatorio sommando tutti i mintermini (quindi, i prodotti) del circuito stesso per cui l'*output* risulta essere `True`. La forma **POS**, invece, consiste nello scrivere l'equazione booleana relativa a un circuito combinatorio moltiplicando tutti i maxtermini (quindi, le somme) per cui l'*output* risulta essere `False`. Nel fare ciò, è importante ricordare che, in una tavola di verità, a ogni riga viene associato un mintermine che sia `True` per quella riga e un maxtermine che sia `False` per quella riga.

Alternativamente, la forma SOP può essere scritta utilizzando la notazione Σ, che prende in argomento i mintermini da considerare o gli indici delle righe della tavola di verità corrispondenti a tali mintermini; ad esempio:
$$F(A, B) = Σ(m₁, m₃)$$
$$F(A, B) = Σ(1, 3)$$
La forma POS, inoltre, può essere scritta utilizzando la notazione Π, che prende in argomento i maxtermini da considerare o gli indici delle righe della tavola di verità corrispondenti a tali maxtermini; ad esempio:
$$F(A, B) = Π(M₀, M₂)$$
$$F(A, B) = Π(0, 2)$$
___
Ovviamente, un circuito combinatorio può avere **molteplici *output***, ognuno dei quali è definito da una diversa funzione booleana degli *input*. Nonostante ciò, risulta spesso conveniente definire tutti gli *output* in una singola tavola di verità.

Un esempio di circuito combinatorio a più *output* è il cosiddetto "circuito di priorità", un circuito in cui vi è, in parole povere, una gerarchia di importanza tra i vari *input* e dal quale, in base ad essa, risulta sempre un unico dei *output* dai vari possibili. Per visualizzare meglio questo meccanismo, possiamo immaginare un'università in cui il rettore, il presidente di un dipartimento, un professore di tale dipartimento e uno studente richiedono di utilizzare una determinata aula. Tra di essi, naturalmente, ci sarà una differenza di priorità, che va a decrescere andando da rettore a studente: dunque, ad esempio, la richiesta del rettore vincerà su tutte le altre, mentre quella dello studente vincerà solo se nessun'altro avrà richiesto l'aula nello stesso giorno.

Immaginiamo, ora, di esprimere questo concetto con un circuito di priorità. Associamo a ciascun personaggio un *output*:
- *Y₃* rappresenterà la vittoria del rettore;
- *Y₂* rappresenterà la vittoria del presidente di dipartimento;
- *Y₁* rappresenterà la vittoria del professore;
- *Y₀* rappresenterà la vittoria dello studente.

Analogamente a come sono configurati gli *output*, associamo anche i vari *input* *A₃*, *A₂*, *A₁* e *A₀*. Notiamo, ora, alcune cose: *Y₃* risulterà `True` ogni volta che *A₃* sarà `True`(ossia, il rettore otterrà l'aula ogni volta che la richiederà, essendo il più importante dei quattro); *Y₂* risulterà `True` ogni volta che *A₂* sarà `True` e *A₃* sarà `False` (ossia, il presidente di dipartimento otterrà l'aula ogni volta che la richiederà, a patto che non lo faccia il rettore); e così via. Una tavola di verità che descrive il funzionamento di tale circuito può essere la seguente:

![[prioritycirc_example_truth.png]]
Se volessimo, invece, rappresentare il circuito con una [[PLA]], si otterrebbe:

![[prioritycirc_example_pla.png]]

Dall'analisi di questo circuito, si osserva che se determinati *input* sono attivi, per gli *output* è irrilevante lo stato degli altri *input*. Gli *input* irrilevanti per un determinato *output*, dunque, non importano, e vengono perciò definiti "***don't care***". I *don't care* si indicano in una tavola di verità con una *X*. Questo concetto permette spesso di semplificare notevolmente la tavola di verità di un circuito; ad esempio, quella del circuito appena analizzato diventa:

![[prioritycirc_example_dontcare.png]]
___
I circuiti logici in forma SOP operano nella cosiddetta "logica a due livelli", in quanto i vari *literals* sono connessi a un primo livello di porte *AND* e a un secondo livello di porte *OR*. Spesso, tuttavia, un circuito viene costruito utilizzando più di questi due livelli, in quanto fare ciò consentirebbe di utilizzare meno componenti; se un circuito possiede più di due "livelli", esso opera nella **logica combinatoria multilivello**.

Un caso semplice in cui risulta immediata la convenienza della logica multilivello è la porta *XOR* a 3 *input*. Volendo rappresentare il funzionamento di una porta *XOR* con la logica a due livelli, si otterrebbe un circuito del genere:

![[xor3_twolevel.png]]

Invece, se si volesse trascendere la logica a due livelli, si potrebbe rappresentare il funzionamento di tale circuito semplicemente con due porte *XOR* a due *input*, disposte nella maniera seguente:

![[xor3_multilevel.png]]

Volendo esagerare l'esempio appena analizzato, la convenienza risulta ancora più evidente: ad esempio, una porta *XOR* a 8 *input* necessiterebbe di 128 porte *AND* a 8 *input* e di una porta *OR* a 128 *input* per essere schematizzata con la logica a due livelli; invece, molto più convenientemente, si potrebbero utilizzare tre livelli di porte *XOR* a 2 *input*, per un totale di 7 porte.

In generale, scegliere la migliore implementazione multilivello di una determinata funzione logica non è sempre immediato, e il significato stesso di "migliore" potrebbe variare in base al contesto.
___
Seppur l'algebra booleana sia limitata a due soli valori possibili (0 e 1), nel concreto all'interno di un circuito possono presentarsi anche "**valori illegali**" o "**impedenze**", indicati rispettivamente con **X** (da non confondere con i *don't care* delle tavole di verità) e **Z**.

Il simbolo X indica che un particolare nodo di un circuito presenta un valore "illegale" o "ignoto"; ciò avviene, comunemente, se si collega un nodo a uno 0 e a un 1 allo stesso tempo. Una situazione del genere viene definita "***contention***", e viene ovviamente considerata come un errore da evitare, in quanto porta a un'incertezza sul voltaggio del nodo considerato e può anche portare a surriscaldamenti o danneggiamenti del circuito stesso. A volte, il simbolo X può essere utilizzato dai simulatori di circuiti per denotare una variabile non inizializzata, in modo da far risaltare meglio il problema.

Il simbolo Z, invece, indica che un particolare nodo di un circuito non presenta né un valore 1 né un valore 0; in questa situazione, si dice che il nodo è ad "**alta impedenza**" o è "***floating***". Un nodo ad alta impedenza potrebbe contenere uno 0 , un 1, o qualsiasi altro voltaggio nell'intervallo delimitato da questi ultimi, e la presenza di questa situazione non rappresenta sempre un errore, a patto che qualche altro elemento del circuito riassegni il nodo a un valore valido quando esso sarà rilevante nella funzionalità del circuito. Comunemente, una situazione di alta impedenza avviene se non si collega un determinato voltaggio a un *input* del circuito: fare ciò porterà quest'ultimo a comportarsi in maniera imprevedibile. Un componente in cui il valore di alta impedenza assume importanza è il *[[Tristate buffer|tristate buffer]]*.