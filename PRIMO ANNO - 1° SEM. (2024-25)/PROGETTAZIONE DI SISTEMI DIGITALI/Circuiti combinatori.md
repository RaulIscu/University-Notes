## Cos'è un circuito combinatorio?

Un **circuito combinatorio** è un circuito in cui **gli output dipendono esclusivamente dagli input attuali** (esso, dunque, non "ricorda" gli input precedenti a quelli attuali, infatti **un circuito combinatorio è privo di memoria**). Dunque, gli output vengono ottenuti "combinando" e manipolando i valori presi in input. Un esempio basilare di circuito combinatorio può essere una qualsiasi [[Porte logiche#Cos'è una porta logica?|porta logica]]. La specifica di funzione di un circuito combinatorio esprime gli output in funzione degli input. La specifica di tempo, invece, risulterà in un intervallo di tempo delimitato dal minimo e dal massimo delay tra rilevamento degli input e restituzione degli output.

Per costruire un circuito combinatorio, è importante seguire le regole della **composizione combinatoria**. Le principali direttive da tenere a mente sono le seguenti:
- ogni elemento di un circuito combinatorio dev'essere anch'esso combinatorio;
- ogni nodo di un circuito combinatorio o trasporta un input nel circuito o è connesso a esattamente un output di un elemento del circuito;
- un circuito combinatorio non può contenere cicli, e ogni percorso possibile all'interno del circuito può passare per un nodo del circuito al massimo una volta.

Graficamente, un circuito combinatorio viene rappresentato con il rettangolo tipico del circuito generico, e racchiusa al suo interno la dicitura "***CL***" (che sta per "combinational logic"), come nel seguente esempio:

![[combinationalcircuit.png]]

A volte, per semplificare la rappresentazione di un circuito combinatorio, si riassumono più input o più output in una sola linea, attraversata da uno slash (`/`) e dotata di un numero che indica l'ammontare di segnali racchiusi nella linea stessa; questo tipo di rappresentazione viene definito "**bus**". Ad esempio, un circuito con un bus a 3 segnali in input e uno a 2 segnali in output può essere rappresentato nel modo seguente:

![[combinationalcircuit_bus.png]]

Se il numero di segnali non è rilevante, o se risulta ovvio per qualche motivo, l'indicatore dello stesso può essere omesso.
___
## Specifica di funzione di un circuito combinatorio

La specifica di funzione di un circuito combinatorio può essere espressa con una **tavola di verità** o con un'**[[Algebra booleana#Cos'è un'equazione booleana?|equazione booleana]]**. Prima, però, per capire al meglio come ottenere la seconda dalla prima, è utile conoscere il significato di due termini, ossia "mintermine" e "maxtermine":
- un prodotto che coinvolge tutti gli input di un determinato circuito viene detto "**mintermine**" (***minterm***) di quel circuito;
- una somma che coinvolge tutti gli input di un determinato circuito viene detto "**maxtermine**" (***maxterm***) di quel circuito.

A partire da una tavola di verità, ci sono principalmente due modi di arrivare a un'equazione booleana che descriva il funzionamento di un circuito combinatorio, a seconda della forma di tale equazione e di come ci si arrivi:
- la forma "***sum of products***" (o **SOP**);
- la forma "***product of sums***" (o **POS**).

La forma **SOP** consiste nello scrivere l'equazione booleana relativa a un circuito combinatorio **sommando tutti i mintermini** (quindi, i prodotti) del circuito stesso per cui l'output risulta essere **`True`**. La forma **POS**, invece, consiste nello scrivere l'equazione booleana relativa a un circuito combinatorio **moltiplicando tutti i maxtermini** (quindi, le somme) per cui l'output risulta essere **`False`**.

Alternativamente, la forma SOP può essere scritta utilizzando la notazione $\Sigma$, che prende in argomento i mintermini da considerare, oppure gli indici delle righe della tavola di verità corrispondenti a tali mintermini; ad esempio:
$$F(A, B) = \Sigma(m₁, m₃)$$
$$F(A, B) = \Sigma(1, 3)$$
La forma POS, inoltre, può essere scritta utilizzando la notazione $\Pi$, che prende in argomento i maxtermini da considerare, oppure gli indici delle righe della tavola di verità corrispondenti a tali maxtermini; ad esempio:
$$F(A, B) = \Pi(M₀, M₂)$$
$$F(A, B) = \Pi(0, 2)$$

[PASSAGGIO DA SOP A POS E DA POS A SOP]
___
## Mappe di Karnaugh

Le **mappe di Karnaugh** (o "**K-map**"), ideate nel 1953 dall'ingegnere Maurice Karnaugh, rappresentano un metodo veloce per **semplificare un'equazione booleana** di un circuito digitale **in maniera grafica**. Analizziamo subito un esempio concreto, per comprendere al meglio il funzionamento di una mappa di Karnaugh. Supponiamo di avere la tavola di verità di un circuito a 3 input:

![[kmap_example_truth.png]]

Ora, per impostare la K-map relativa a tale tavola di verità, si crea una tabella che presenterà sulla riga superiore i possibili valori degli input $A$ e $B$ (essendo gli input considerati 2, i possibili valori saranno 4), e sulla colonna di sinistra i possibili valori dell'input $C$ (essendo l'input considerato 1, i possibili valori saranno 2). A questo punto, nella tabella risultante, si inserirà in ogni casella il valore di output corrispondente agli input relativi a tale casella; facendo ciò, si avrà che ogni casella della K-map corrisponderà a una riga della tavola di verità, e dunque a un **mintermine** del circuito considerato. Di seguito, la K-map relativa alla tavola di verità dell'esempio, prima scritta in forma classica, poi evidenziando i mintermini corrispondenti:

![[kmap_example.png]]

Nella costruzione di una K-map, è importante ricordare di inserire i valori di input in un ordine particolare, definito "**gray code**", secondo cui essi vanno inseriti in modo che **tra valori adiacenti cambi una sola cifra**; ciò porta a variazioni rispetto al classico ordine binario, ma risulterà utile in seguito. Facendo ciò, infatti, ogni casella, o mintermine, presente nella K-map differisce da una casella adiacente ad essa di una sola variabile: dunque, caselle adiacenti condividono tutti i loro literals tranne uno, che appare nella sua *true form* in una casella e con il suo complemento nell'altra. Un'altra proprietà interessante delle K-map è che sono **circolari**, nel senso che, ad esempio, le ultime caselle a destra sono considerate adiacenti alle ultime a sinistra (infatti, anch'esse variano di un solo literal).

A questo punto, si può notare immediatamente che solo due dei mintermini saranno presenti nell'equazione booleana del circuito, ossia quelli indicati da un $1$ nella K-map. Si potrebbe, dunque, semplificare l'equazione algebricamente, oppure graficamente lavorando proprio sulla K-map. Per fare ciò, basterà:
- raggruppare gli $1$ in caselle adiacenti;
- per ogni raggruppamento, segnare l'implicante corrispondente ad esso (l'implicante relativo al raggruppamento più grande verrà definito "implicante primo");
- se all'interno di un raggruppamento è presente una variabile insieme al suo complemento, escludere tale variabile dall'implicante.

Nell'esempio, si cerchieranno gli 1 nelle caselle a sinistra, ottenendo:

![[kmap_example_1.png]]

Essendo inclusi nel raggruppamento sia $C$ che il suo complemento, la variabile $C$ verrà esclusa dall'implicante risultante, che sarà dato dunque solo dai complementi delle variabili $A$ e $B$. Si è ottenuta, così, l'equazione booleana semplificata che si sarebbe ottenuta lavorando algebricamente sulla tavola di verità.

In generale, per lavorare al meglio anche su mappe e circuiti più complessi, è utile stabilire alcune **linee guida**, tra cui:
- usare il **minor numero di raggruppamenti possibile**, e fare in modo che **ogni raggruppamento sia il più grande possibile**;
- tutte le caselle di un raggruppamento possono contenere solo $1$;
- ogni raggruppamento deve contenere **$2^n$ caselle** ($1$, $2$, $4$, $8$, ecc. ecc.);
- **una casella può essere compresa in più raggruppamenti** se fare ciò consente di avere meno raggruppamenti totali.

Ovviamente, l'approccio analizzato finora, dove si raggruppano tutte le caselle per cui l'output è $1$, si utilizza per ricavare una [[Circuiti combinatori#Specifica di funzione di un circuito combinatorio|forma SOP]] dalla K-map. È possibile, tuttavia, trovare anche la relativa [[Circuiti combinatori#Specifica di funzione di un circuito combinatorio|forma POS]]: per fare ciò, basterà semplicemente raggruppare le caselle contenenti $0$ invece di quelle contenenti $1$, e rispettare analogamente le altre linee guida; è fondamentale, però tenere a mente che **se si ricava una forma POS, i literals inseriti andranno negati**.

All'interno di una mappa di Karnaugh, e dunque anche all'interno di una tavola di verità, si possono trovare anche dei *[[Circuiti combinatori#Circuiti combinatori con più output|don't care]]* tra gli output, nei casi in cui tale output è irrilevante per qualche motivo o quando la combinazione di input che porterebbe a tale output non può verificarsi. Trovare dei *don't care* in una K-map, in realtà, può risultare notevolmente comodo, in quanto, all'occorrenza, essi possono essere considerati sia come $0$ che come $1$, consentendo una maggiore semplificazione logica.
___
## PLA

In generale, un diagramma che rappresenti graficamente la funzionalità di un circuito digitale, mostrandone i vari elementi e i collegamenti che sussistono tra di essi, viene definito "**diagramma schematico**".

Potenzialmente, un diagramma schematico può essere disegnato come si desidera, ma per comodità si sono stabilite convenzionalmente delle **regole di base** che ogni diagramma schematico dovrebbe seguire. Le principali sono:
- i segnali di **input** si trovano nella **parte sinistra** (o **superiore**) del diagramma;
- i segnali di **output** si trovano nella **parte destra** (o **inferiore**) del diagramma;
- se possibile, le **porte logiche** dovrebbero confluire una nell'altra **da sinistra verso destra**;
- è preferibile rappresentare **nodi "dritti"** rispetto a nodi che presentano molteplici angoli o spigoli;
- i cavi si collegano sempre tra di loro in un **incrocio a T**;
- se due cavi si incrociano formando una **croce**, essi saranno collegati solo se vi sarà un **punto** al centro di quest'ultima, altrimenti non vi sarà collegamento.

Una qualsiasi [[Algebra booleana#Cos'è un'equazione booleana?|equazione booleana]], se posta in **[[Circuiti combinatori#Specifica di funzione di un circuito combinatorio|forma SOP]]**, può essere disegnata sistematicamente senza problemi con un diagramma schematico che segue le regole appena stabilite. Per farlo, converrà prima di tutto rappresentare varie colonne per gli input (con annesse le relative porte *NOT*, in modo da avere anche i complementi degli input se necessari); poi, si avranno varie righe di porte *AND*, una per ognuno dei mintermini; infine, per l'output, si dovrà inserire una porta *OR* in cui confluiranno i mintermini relativi a tale output. Un esempio di diagramma disegnato così è il seguente:

![[pla_example.png]]

Un diagramma disegnato in questo stile, seguendo queste convenzioni, viene chiamato ***PLA***, o "***programmable logic array***".
___
## Circuiti combinatori con più output

Ovviamente, un circuito combinatorio può avere **molteplici output**, ognuno dei quali è definito da una diversa funzione booleana degli *input*. Nonostante ciò, risulta spesso conveniente definire tutti gli output in **una singola tavola di verità**.

Un esempio di circuito combinatorio a più output è il cosiddetto "**circuito di priorità**", un circuito in cui vi è, in parole povere, una gerarchia di importanza tra i vari input e dal quale, in base ad essa, risulta sempre un unico dei output dai vari possibili. Per visualizzare meglio questo meccanismo, possiamo immaginare un'università in cui il rettore, il presidente di un dipartimento, un professore di tale dipartimento e uno studente richiedano di utilizzare una determinata aula. Tra di essi, naturalmente, ci sarà una differenza di priorità, che va a decrescere andando da rettore a studente: dunque, ad esempio, la richiesta del rettore vincerà su tutte le altre, mentre quella dello studente vincerà solo se nessun'altro avrà richiesto l'aula nello stesso giorno.

Immaginiamo, ora, di esprimere questo concetto con un circuito di priorità. Associamo a ciascun personaggio un *output*:
- $Y_{3}$ rappresenterà la vittoria del rettore;
- $Y_{2}$ rappresenterà la vittoria del presidente di dipartimento;
- $Y_{1}$ rappresenterà la vittoria del professore;
- $Y_{0}$ rappresenterà la vittoria dello studente.

Analogamente a come sono configurati gli output, associamo anche i vari input $A_{3}$, $A_{2}$, $A_{1}$ e $A_{0}$. Notiamo, ora, alcune cose: $Y_{3}$ risulterà `True` ogni volta che $A_{3}$ sarà `True`(ossia, il rettore otterrà l'aula ogni volta che la richiederà, essendo il più importante dei quattro); $Y_{2}$ risulterà `True` ogni volta che $A_{2}$ sarà `True` e $A_{3}$ sarà `False` (ossia, il presidente di dipartimento otterrà l'aula ogni volta che la richiederà, a patto che non lo faccia il rettore); e così via. Una **tavola di verità** che descrive il funzionamento di tale circuito può essere la seguente:

![[prioritycirc_example_truth.png]]

Se volessimo, invece, rappresentare il circuito con una **[[Circuiti combinatori#PLA|PLA]]**, si otterrebbe:

![[prioritycirc_example_pla.png]]

Dall'analisi di questo circuito, si osserva che se determinati input sono attivi, per gli output è irrilevante lo stato degli altri input. Gli input irrilevanti per un determinato output, dunque, non importano, e vengono perciò definiti "***don't care***". I *don't care* si indicano in una tavola di verità con una $X$. Questo concetto permette spesso di semplificare notevolmente la tavola di verità di un circuito; ad esempio, quella del circuito appena analizzato diventa:

![[prioritycirc_example_dontcare.png]]
___
## Valori illegali e impedenze

Seppur l'[[Algebra booleana|algebra booleana]] sia limitata a due soli valori possibili ($0$ e $1$), nel concreto all'interno di un circuito possono presentarsi anche "**valori illegali**" o "**impedenze**", indicati rispettivamente con **$X$** (da non confondere con i *[[Circuiti combinatori#Circuiti combinatori con più output|don't care]]* delle tavole di verità) e $Z$.

Il simbolo $X$ indica che un particolare nodo di un circuito presenta un valore "**illegale**" o "**ignoto**"; ciò avviene, comunemente, se si collega un nodo a uno $0$ e a un $1$ allo stesso tempo. Una situazione del genere viene definita "**contention**", e viene ovviamente considerata come un errore da evitare, in quanto porta a un'incertezza sul voltaggio del nodo considerato ed, eventualmente, anche a surriscaldamenti o danneggiamenti del circuito stesso. A volte, il simbolo $X$ può essere utilizzato dai simulatori di circuiti anche per denotare una variabile non inizializzata, in modo da far risaltare meglio il problema.

Il simbolo $Z$, invece, indica che un particolare nodo di un circuito non presenta né un valore $1$ né un valore $0$; in questa situazione, si dice che il nodo è ad "**alta impedenza**" o è "***floating***". Un nodo ad alta impedenza potrebbe contenere uno $0$, un $1$, o qualsiasi altro voltaggio nell'intervallo delimitato da questi ultimi, e la presenza di questa situazione non rappresenta sempre un errore, a patto che qualche altro elemento del circuito riassegni il nodo a un valore valido quando esso sarà rilevante nella funzionalità del circuito stesso. Comunemente, una situazione di alta impedenza avviene se non si collega un determinato voltaggio a un input del circuito: fare ciò porterà quest'ultimo a comportarsi in maniera imprevedibile. Un componente in cui il valore di alta impedenza assume importanza è il [[Circuiti combinatori#Tristate buffer|tristate buffer]].
___
## Componenti combinatorie

Oltre alle **[[Porte logiche|porte logiche]]**, ci sono anche altre componenti "**notevoli**" nella progettazione di circuiti combinatori, molto utili per riassumere comportamenti complessi e nella costruzione di circuiti più grandi, combinatori o sequenziali che siano. Le principali sono:
- il **tristate buffer**;
- il **multiplexer**;
- il **decoder**.
___
#### Tristate buffer

Il **tristate buffer** è un componente combinatorio che presenta tre possibili output diversi: $1$, $0$ e $Z$. Tale componente, nel concreto, è dotato di un input $A$, un output $Y$ e di un cosiddetto valore di "**enable**" $E$: quando il valore di enable è $1$, il tristate buffer si comporta come un normalissimo **buffer**, restituendo quindi come output lo stesso valore ricevuto in input; invece, quando il valore di enable è $0$, il tristate buffer emetterà un **output ad alta impedenza**. La rappresentazione grafica di questo componente, e la sua tavola di verità, è la seguente:

![[tristate_buffer.png]]

In particolare, quello mostrato in figura è un tristate buffer che presenta un ***active high enable***, e dunque è attivo quando il valore di enable è $1$, come stabilito in precedenza. Vi è una variazione di questo componente, ossia il tristate buffer con un ***active low enable***, che è attivo quando il valore di enable è $0$:

![[tristate_buffer_low.png]]
___
#### Multiplexer

Un **multiplexer** (detto anche semplicemente **mux**) è un componente combinatorio il cui scopo è quello di scegliere un output tra diversi possibili input, in base a un valore di "**select**", chiamato anche "**segnale di controllo**". La forma più basilare di multiplexer è il cosiddetto "**$2:1$ multiplexer**", che presenta due input ($D_{0}$ e $D_{1}$), un valore di select ($S$) e un valore di output ($Y$). Di seguito, la rappresentazione grafica di un $2:1$ multiplexer generico e la sua tavola di verità:

![[mux.png]]

Come si può notare dalla tavola di verità, quando il valore $S$ è uguale a $0$, l'output corrisponderà all'input $D_{0}$, mentre quando $S$ sarà uguale a $1$, l'output corrisponderà all'input $D_{1}$. Un $2:1$ multiplexer può essere costruito con un circuito in [[Circuiti combinatori#Specifica di funzione di un circuito combinatorio|forma SOP]], o anche utilizzando dei [[Circuiti combinatori#Tristate buffer|tristate buffer]], come si può vedere di seguito:

![[mux_sop.png]]
![[mux_tristate.png]]

Esistono anche multiplexer più grandi, che presentano dunque un maggior numero di input. Ad esempio, un **$4:1$ multiplexer** presenta 4 input ($D_{0}$, $D_{1}$, $D_{2}$ e $D_{3}$), due valori di select ($S_{0}$ e $S_{1}$) e un valore di output ($Y$). Di seguito, la rappresentazione grafica di un $4:1$ multiplexer generico:

![[mux4.png]]

Oltre a essere costruibile mediante circuiti in forma SOP o contenenti tristate buffer, un multiplexer con più di due input come il $4:1$ multiplexer può essere costruito anche utilizzando **molteplici $2:1$ multiplexer**:

![[mux4_with_mux2.png]]

Si incontreranno, probabilmente, anche multiplexer più complessi, come l'$8:1$ multiplexer, il $16:1$ multiplexer e così via. In generale, sarà utile ricordare che un mux potrà avere $2^n$ input e un numero di valori select pari a $n$.
___
#### Decoder

Un **decoder** è un componente combinatorio il cui scopo è quello di scegliere esattamente un output tra diversi possibili output, in base alla combinazione di input che riceve; per questa esclusività degli output, essi vengono definiti "***one-hot***", in quanto solo uno di loro è "attivo" in qualsiasi momento. In generale, un decoder può avere un numero $n$ di input e un numero $2^n$ di output.

Una delle forme più basilari e comuni di decoder è il **$2:4$ decoder**, che presenta due input ($A_{0}$ e $A_{1}$) e 4 output ($Y_{0}$, $Y_{1}$, $Y_{2}$ e $Y_{3}$). Di seguito, la rappresentazione grafica di un $2:4$ decoder generico e la sua tavola di verità:

![[decoder.png]]

Similmente ai [[Circuiti combinatori#Multiplexer|multiplexer]], anche i decoder possono essere costruiti mediante un circuito in [[Circuiti combinatori#Specifica di funzione di un circuito combinatorio|forma SOP]], o meglio utilizzando delle porte *AND*. Generalmente, per un $n:2^n$ decoder, saranno necessarie $2^n$ porte *AND* con $n$ *input*, con ogni porta che riceverà la *true form* o il complemento di ciascun input presente; si può notare, dunque, che **ogni output in un decoder rappresenta un singolo mintermine degli input**. Graficamente, un $2:4$ decoder equivale al seguente circuito:

![[decoder_and.png]]
___