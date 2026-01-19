In questo capitolo, si approfondirà un aspetto trattato in parte nel [[SO1_03 - I processi#Come vengono programmati i processi nella CPU?|capitolo precedente]]: lo **scheduling dei processi all'interno della CPU**. In particolare, partiremo con un'introduzione generale, soffermandoci sulle definizioni e i concetti di base, e passeremo in seguito a vari algoritmi e concetti più avanzati applicabili a tale argomento.

## Introduzione allo scheduling

Sappiamo bene che pressoché qualsiasi programma alterna, in qualche modo, fasi incentrate sulla **computazione nella CPU** a fasi che dipendono dall'**I/O**. Assumendo di avere un sistema in grado di eseguire un solo processo alla volta, il tempo passato ad attendere un dato o un evento di I/O è sostanzialmente sprecato, dato che è un lasso di tempo in cui la CPU non lavora e non contribuisce all'esecuzione del [[SO1_03 - I processi|processo]]. Questa rappresenta una delle problematiche principali a cui deve provvedere lo **scheduling**: l'obiettivo, dunque, è sostanzialmente **ottimizzare l'esecuzione dei processi, massimizzando la produttività della CPU e garantendo un'equità di esecuzione tra i vari processi**.

Come abbiamo già anticipato, tutti i processi gestiti dall'OS risiedono in esattamente una delle varie **process state queues**; inoltre, possiamo affermare che tutti i processi si alternano tra **due stati possibili** in un ciclo continuo:
- uno "**slancio di CPU**";
- uno "**slancio di I/O**".

Il primo dei due corrisponde alla fase dell'esecuzione incentrata sui calcoli e sulle operazioni svolte grazie alla CPU, mentre il secondo corrisponde alla fase dell'esecuzione dedicata all'attesa del trasferimento di dati in invio o in ricezione. Nella maggioranza dei casi, **gli slanci di CPU hanno una durata breve**, mentre **gli slanci di I/O portano ad attese prolungate**.

L'obiettivo di uno **scheduler**, dunque, è quello innanzitutto di **assegnare un nuovo processo da eseguire alla CPU non appena questa diventa inattiva**: quando ciò accade, lo scheduler va a prendere un processo dalla process state queue relativa allo stato `ready`, dunque un processo che è pronto per essere eseguito, e attiva la sua esecuzione all'interno della CPU, rimuovendo quello che la occupava in precedenza. L'algoritmo con cui lo scheduler sceglie il processo da mandare in esecuzione non si basa necessariamente su una coda di tipo FIFO (First In, First Out), ma dipende dall'implementazione specifica e dall'obiettivo con maggiore priorità.

In generale, **lo scheduling della CPU si attiva quando si verifica una delle seguenti 4 condizioni**:
1. quando un processo passa **dallo stato `running` allo stato `waiting`**, ad esempio in attesa di una risposta I/O o dell'esecuzione di una system call;
2. quando un processo passa **dallo stato `running` allo stato `ready`**, ad esempio in risposta a un interrupt;
3. quando un processo passa **dallo stato `waiting` allo stato `ready`**, ad esempio in seguito al completamento di una richiesta di I/O o al termine di una chiamata `wait()`;
4. quando un processo viene **creato** o **terminato**.

In particolare, nel primo e nell'ultimo caso generalmente lo scheduler è **forzato a scambiare il processo attualmente considerato con uno nuovo**, mentre nel secondo e nel terzo caso, in base al contesto, esso può **scegliere di eseguire un nuovo processo o di continuare con quello attuale**. In base a quale dei due approcci viene scelto, si distingue tra due tipi diversi di scheduling:
- il "**non-preemptive scheduling**", ossia lo scheduling che avviene solo quando non si ha altra scelta, come nelle condizioni $1$ e $4$ (in questo tipo di sistema, una volta che un processo inizia la sua esecuzione nella CPU esso non potrà essere sospeso dallo scheduler, a meno che il processo stesso non sospenda da solo la sua esecuzione o la termini);
- il "**preemptive scheduling**", ossia lo scheduling che avviene non solo quando non si ha altra scelta, ma anche in condizioni come la $2$ e la $3$ (in questo tipo di sistema, lo scheduler ha il pieno controllo sui processi che vengono eseguiti nella CPU).

Come si può immaginare, il non-preemptive scheduling è un approccio ormai antiquato e che presenta vari limiti, mentre il preemptive scheduling è diventato lo standard per gli OS moderni. Ciononostante, l'implementazione del preemptive scheduling può presentare delle **problematiche**: ad esempio, potrebbe causare comportamenti imprevisti se avviene durante l'esecuzione di una system call, oppure contestualmente a [[SO1_03 - I processi#Come comunicano i processi tra di loro?|processi cooperanti]]. Per ovviare a questi problemi, possiamo implementare soluzioni come fare in modo che **lo scheduling attenda il completamento o il blocco di una system call** prima di attivarsi (benché funzionante, tale soluzione può interferire con eventuali sistemi real-time, dove naturalmente ritardare lo scheduling porterebbe a un ritardo anche nella reattività del sistema).

Nel momento in cui lo scheduler ha scelto il processo da inviare alla CPU, entra in gioco il "**dispatcher**", ossia il modulo che concretamente si occupa di **dare il controllo della CPU a tale processo**. Tra le sue mansioni, dunque, troviamo quella di eseguire il [[SO1_03 - I processi#Come vengono programmati i processi nella CPU?|context switch]], di effettuare la transizione alla modalità utente, e di saltare alla posizione opportuna del programma da far eseguire alla CPU. Per sua natura, **il dispatcher viene eseguito con ogni context switch**, e avendo già stabilito che quest'ultimo rappresenta un'operazione relativamente costosa a livello di tempo e di trasferimento di dati, è cruciale che il dispatcher sia il più veloce possibile, diminuendo la cosiddetta "**dispatcher latency**".

Parlando di **tempistiche**, prima di continuare soffermiamoci su alcune **definizioni utili** per comprendere i vari intervalli di tempo a cui si deve prestare attenzione quando si tratta lo scheduling:
- l'**arrival time** ($T_{arrival}$) consiste nel momento in cui un processo entra nella coda `ready`;
- il **completion time** ($T_{completion}$) consiste nel momento in cui un processo completa la sua esecuzione;
- il **burst time** ($T_{burst}$) consiste nel tempo richiesto da un processo per l'esecuzione nella CPU;
- il **turnaround time** ($T_{turnaround}=T_{completion}-T_{arrival}$) consiste nel tempo trascorso tra l'arrivo di un processo nella coda `ready` e il completamento della sua esecuzione;
- il **waiting time** ($T_{waiting}=T_{turnaround}-T_{burst}$) consiste nel tempo dell'esecuzione di un processo non dedicato alla computazione nella CPU.

A questo punto, avendo chiaro un quadro generale di come funziona lo scheduling nella CPU, possiamo cominciare a pensare agli **algoritmi di scheduling**, e ai vari fattori da considerare nella scelta di questi ultimi. In generale, per valutare la "qualità" di un algoritmo di scheduling sarà opportuno considerare i seguenti criteri:
- **utilizzo della CPU**, ossia sostanzialmente l'ammontare di tempo in cui la CPU sta svolgendo una qualche operazione (idealmente, si vorrebbe tenere la CPU occupata il $100\%$ del tempo, in modo da non sprecare nemmeno un ciclo di clock, ma realisticamente l'occupazione della CPU si aggira solitamente tra il $40\%$ e il $90\%$);
- **throughput**, ossia il numero di processi completati in un'unità di tempo;
- **turnaround time**, ossia, come visto in precedenza, il tempo richiesto per completare un processo;
- **waiting time**, ossia, come visto in precedenza, il tempo dell'esecuzione di un processo non dedicato alla computazione nella CPU, e dunque trascorso nella coda `ready` (non va confuso con lo stato `waiting`);
- **response time**, ossia il tempo che trascorre tra l'emissione di un comando e l'inizio della risposta a tale comando (si considera soprattutto contestualmente a processi fortemente interattivi).

Di questi fattori, un buon algoritmo di scheduling deve cercare di **massimizzare il più possibile l'utilizzo della CPU e il throughput**, cercando al tempo stesso di **minimizzare il turnaround time, il waiting time e il response time**. In altre parole, vogliamo ottenere il massimo della produttività e dell'occupazione della CPU mantenendo, contemporaneamente, delle tempistiche e dei ritardi ragionevoli. 

Idealmente, sarebbe perfetto avere un algoritmo che riesca a soddisfare tutte queste aspettative al meglio, ma realisticamente ciò è impossibile, e si dovrà sempre sacrificare qualche aspetto in favore di un altro. Dunque, solitamente, **la scelta di un algoritmo di scheduling si basa sull'obiettivo specifico del sistema considerato**. Ad esempio, in un **sistema interattivo**, si potrebbe preferire una **minimizzazione del response time medio** (in modo da fornire all'utente un output il prima possibile), del **response time massimo** e della **varianza del response time** (in genere, un utente è più propenso ad utilizzare un sistema costante e prevedibile, anche se un po' più lento, piuttosto che uno imprevedibile e con tempi molto vari). Invece, in un **sistema a batch**, si preferisce una **massimizzazione del throughput** e una **minimizzazione del waiting time**.
___
## Algoritmi di scheduling

In questo paragrafo, andremo ad approfondire vari **algoritmi di scheduling**, analizzando funzionamento, strutture dati utilizzate e contesti favorevoli in cui utilizzare ciascuno di essi. In particolare, ci concentreremo sui seguenti algoritmi:
- **First Come First Serve** (**FCFS**);
- **Round Robin** (**RR**);
- **Shortest Job First** (**SJF**);
- **Priority Scheduling** (**PS**);
- **Multilevel Queue** (**MQ**);
- **Multilevel Feedback Queue** (**MFQ**).

##### First Come First Serve

L'algoritmo **First Come First Serve**, spesso abbreviato in **FCFS**, è in realtà abbastanza semplice. Si basa su una **coda di tipo FIFO** (**First In First Out**), ossia una coda dove **il primo elemento ad essere aggiunto sarà anche il primo ad essere eventualmente rimosso**. 

Per comprendere meglio, si può pensare a tale coda come a una coda di clienti alla cassa di un supermercato: i primi della fila saranno i primi a pagare, e i clienti procederanno nell'ordine in cui sono arrivati alla cassa. Contestualizzando allo scheduling di processi nella CPU, **lo scheduler andrà ad eseguire i processi in ordine di "arrivo" fino al loro completamento**; perciò, esso entrerà in gioco solo quando il processo corrente sospenderà autonomamente la propria esecuzione o quando quest'ultima terminerà. Avendo chiarito quest'ultima proprietà, capiamo che **l'algoritmo FCFS è un algoritmo di [[SO1_04 - Scheduling della CPU#Introduzione allo scheduling|non-preemptive scheduling]]**. 

Vediamo un esempio concreto di **applicazione dell'algoritmo FCFS**. Supponiamo di avere i seguenti tre processi da eseguire:

| Ordine di arrivo | Processo | Slancio di CPU (in unità di tempo) |
| ---------------- | -------- | ---------------------------------- |
| 1                | A        | 5                                  |
| 2                | B        | 2                                  |
| 3                | C        | 3                                  |

Si suppone, per semplicità, che questi processi non presentino alcuno slancio di I/O. Ora, seguendo il ragionamento dell'algoritmo considerato, i 3 processi verranno creati (e, dunque, entreranno nella coda `new`) nell'ordine dato dalla colonna $\text{Ordine di arrivo}$, ossia $A-B-C$; analogamente, verranno poi spostati nella coda `ready` sempre nello stesso ordine. Infine, lo scheduler li trasmetterà alla CPU mantenendo ancora lo stesso ordine: avvierà l'esecuzione di $A$, e attenderà il termine della sua esecuzione per avviare quella di $B$, e lo stesso avverrà con $C$. Dunque, su un'ipotetica linea temporale, al termine dell'esecuzione dei 3 processi si avrà una situazione del genere:

![[fcfs_esempio.png]]

Possiamo farci un'idea del **waiting time medio** di ogni processo, ossia del tempo speso in media da uno dei processi considerati nella coda `ready`. Dato un numero $N$ di processi, indichiamo con $T^{arrival}_{i}$ l'arrival time dell'$i$-esimo processo, con $T^{completion}_{i}$ il completion time dell'$i$-esimo processo, con $T^{burst}_{i}$ il burst time dell'$i$-esimo processo, e con $T^{turnaround}_{i}=T^{completion}_{i}-T^{arrival}_{i}$ il turnaround time dell'$i$-esimo processo. A questo punto, per ottenere il waiting time medio $\overline{T}^{waiting}$ si dovrà eseguire la seguente operazione:
$$\overline{T}^{waiting}=\frac{\sum_{i\,=\,1}^{N}(T^{turnaround}_{i}-T^{burst}_{i})}{N}$$
Specifichiamo, per chiarezza, che a meno di altre indicazioni assumeremo, in generale, che $T^{arrival}_{i}=0$ per ogni processo considerato, dunque sostanzialmente che tutti i processi "arrivino" nello stesso momento.

Applicando questa formula all'esempio appena visto, troviamo che il waiting time medio per i processi considerati è pari a $\frac{0+5+7}{3}=4$ unità di tempo. Questo valore, tuttavia, varia in base all'ordine con cui inseriamo i processi nella coda: vediamo, ad esempio, cosa succede nel caso in cui l'ordine di arrivo è $B-C-A$, e dunque in una situazione del genere:

| Ordine di arrivo | Processo | Slancio di CPU (in unità di tempo) |
| ---------------- | -------- | ---------------------------------- |
| 1                | B        | 2                                  |
| 2                | C        | 3                                  |
| 3                | A        | 5                                  |

In questo caso, la linea temporale assume questa forma:

![[fcfs_esempio1.png]]

Seppur il tempo necessario per il completamento dei 3 processi rimane invariato, il waiting time medio va in realtà a diminuire: infatti, stavolta troviamo che $\overline{T}^{waiting}=\frac{0+2+5}{3}\approx 2.3$ unità di tempo. Questo avviene perché, in generale, per ridurre il waiting time medio conviene eseguire prima i processi dall'esecuzione più corta.

Ora, consideriamo ancora lo stesso esempio, tornando però all'ordine iniziale ($A-B-C$), e supponendo stavolta che $A$, oltre alle $5$ unità di tempo dedicate allo slancio di CPU, debba anche eseguire uno **slancio di I/O**. In questo caso, assumendo che lo slancio di I/O sia necessario dopo $2$ unità di tempo dello slancio di CPU, la linea temporale si presenta così:

![[fcfs_esempio2.png]]

Notiamo alcune caratteristiche interessanti. Innanzitutto, notiamo che dopo $2$ unità di tempo, l'esecuzione di $A$ è stata fermata dallo scheduler in corrispondenza della richiesta di I/O effettuata dal processo, e si è dunque avviata l'esecuzione di $B$, tuttavia essendo questo un algoritmo di non-preemptive scheduling la richiesta di I/O potrebbe aver ottenuto risposta anche prima del termine dell'esecuzione di $B$, ma ciò non avrebbe potuto influenzare l'ordine di esecuzione. Dopo la seconda unità di tempo, dunque, a livello di code quello che è successo è che:
- $A$ è stato spostato nella coda `waiting`;
- $B$ è stato spostato dalla coda `ready` alla coda `running`, ossia è stato eseguito;
- $C$ è rimasto nella coda `ready`.

A questo punto, dopo l'esecuzione di $B$, notiamo che è $A$ a tornare in esecuzione. Ci si potrebbe chiedere perché non sia stato scelto $C$, la cui esecuzione non è ancora nemmeno cominciata: la risposta sta proprio nella natura dell'algoritmo FCFS, che considera solo ed esclusivamente l'ordine di arrivo iniziale nella coda `ready`. Dunque, essendo i processi arrivati in tale coda nell'ordine $A-B-C$, il processo $A$ avrà sempre e comunque la priorità sul processo $C$.

In questo scenario, abbiamo che $\overline{T}^{waiting}=\frac{2+2+7}{3}\approx 3.7$ unità di tempo. In realtà tale calcolo non è esattamente preciso, dato che dovremmo rimuovere dal waiting time di $A$ il tempo trascorso tra l'invio della richiesta di I/O e l'arrivo della risposta.

Avendo capito come funziona l'algoritmo FCFS, vediamo i **pro** e i **contro**:
- il **pro** principale dell'algoritmo è sicuramente la sua **semplicità**, sia a livello di implementazione che di funzionamento;
- i **contro** dell'algoritmo sono l'**alta varianza del waiting time medio**, che può variare ingentemente in base all'ordine di arrivo dei processi, e il cosiddetto "**convoy effect**", ossia il fatto che processi esclusivamente vincolati alla CPU faranno sempre aspettare processi vincolati all'I/O, anche se le richieste inviate da quest'ultimi hanno già ricevuto risposta.
___
##### Round Robin

L'algoritmo **Round Robin**, spesso abbreviato in **RR**, è relativamente **simile all'[[SO1_04 - Scheduling della CPU#First Come First Serve|FCFS]]**, con la differenza che **gli slanci di CPU sono eseguiti entro determinati quanti di tempo**. Dunque, quando un processo viene assegnato alla CPU, viene avviato un timer, e se l'esecuzione del processo termina prima che scada il quanto di tempo, allora verrà regolarmente scambiato con il primo processo della coda `ready` come avviene nell'FCFS, mentre se l'esecuzione non è ancora terminata il processo in questione viene spostato all'ultimo posto della coda `ready`, mentre il processo al primo posto della stessa viene eseguito.

Si nota, in base a questa proprietà, che lo scheduler ha il pieno controllo su quale processo viene eseguito in un qualsiasi momento, e dunque **l'algoritmo RR è un algoritmo di [[SO1_04 - Scheduling della CPU#Introduzione allo scheduling|preemptive scheduling]]**.

Il nome dell'algoritmo deriva dal fatto che possiamo vedere la coda `ready` come un cerchio: lo scheduler assegnerà un "turno" di esecuzione a ogni processo in ordine, e una volta terminati i processi ricomincerà da capo nello stesso ordine. Si tratta di un algoritmo che favorisce **maggiore equità**, distribuendo in modo più uniforme l'esecuzione dei processi che gestisce; al tempo stesso, però, **il waiting time medio può risultare maggiore** rispetto ad altri algoritmi di scheduling.

Come si può facilmente intuire, l'efficienza di questo algoritmo dipende fortemente dal **quanto di tempo** utilizzato: dei quanti di tempo troppo lunghi portano l'algoritmo quasi a degenerare in un FCFS, dato che i processi termineranno quasi sicuramente la loro esecuzione prima dello scadere del quanto; al tempo stesso, dei quanti di tempo troppo corti implicano un maggior numero di [[SO1_03 - I processi#Come vengono programmati i processi nella CPU?|context switch]], e di conseguenza a un throughput minore. Si dovrà dunque mantenere un **equilibrio**, facendo in modo che **il ritardo dovuto a un context switch sia relativamente piccolo rispetto al quanto di tempo** (ad esempio, spesso un quanto di tempo si aggira tra i $10$ e i $100$ millisecondi in contesti in cui un context switch occupa tra i $0.01$ e i $0.1$ millisecondi).

Vediamo un esempio concreto di **applicazione dell'algoritmo RR**. Supponiamo di avere i seguenti tre processi da eseguire:

| Ordine di arrivo | Processo | Slancio di CPU (in unità di tempo) |
| ---------------- | -------- | ---------------------------------- |
| 1                | A        | 5                                  |
| 2                | B        | 2                                  |
| 3                | C        | 3                                  |

Si suppone che nessuno dei 3 processi presenti uno slancio di I/O, e che un quanto di tempo sia pari a $2$ unità di tempo, mentre la lunghezza di un context switch è trascurabile. Per adesso l'esecuzione dell'algoritmo è esattamente identica a quella dell'FCFS: i 3 processi arrivano nella coda `ready` nell'ordine $A-B-C$, e lo scheduler sceglie come primo processo da eseguire $A$. A questo punto, però, dopo $2$ unità di tempo, ossia trascorso un quanto, lo scheduler sposta $A$ dalla CPU all'ultimo posto della coda `ready`, e avvia l'esecuzione del processo $B$; dopo un altro quanto, invece, $B$ avrà terminato la propria esecuzione, dunque parte l'esecuzione di $C$ senza ulteriori spostamenti; arrivati alla fine del terzo quanto, $C$ viene spostato al termine della coda `ready`, e ricomincia l'esecuzione di $A$; infine, dopo il quarto quanto, ritorna in esecuzione $C$, ma dopo una singola unità di tempo la sua esecuzione termina, e dunque la restante unità di tempo del quanto viene impiegata per terminare anche l'esecuzione di $A$. Seguendo questi passaggi, la linea temporale dell'esecuzione dei processi assume la seguente forma:

![[rr_esempio.png]]

Per quanto riguarda il waiting time medio, esso è pari a $\frac{5+2+6}{3}\approx 4.3$ unità di tempo, un valore relativamente alto come anticipato.

Consideriamo un altro esempio, stavolta con $5$ processi con slanci di CPU da $100$ unità di tempo ciascuno, e considerando un quanto di tempo pari a $1$ unità e un context switch di durata trascurabile. La tabella seguente mostra un confronto tra FCFS e RR nella gestione di questa situazione:

![[rr_fcfs_confronto.png]]

Dalla tabella, in realtà, sembra che l'algoritmo FCFS vinca su tutti i fronti contro l'RR. Tuttavia, un occhio attento noterà che **seppur la media del turnaround time e del waiting time sia più bassa con l'FCFS, lo stesso non si può dire della varianza** degli stessi: mentre per l'FCFS essi oscillano tra le $100$ e le $500$ unità di tempo, con l'RR si trovano tutti a distanza di poche unità di tempo uno dall'altro. Questo aspetto è fondamentale se ci si inquadra nel contesto di un sistema moderno, in cui meccanismi come lo [[SO1_01 - Introduzione#Multiprogrammazione|pseudo-parallelismo]] sono importantissimi, e dunque non è da sottovalutare. 

Del resto, questa apparente inefficienza dell'RR non si trova in qualsiasi caso. Ad esempio, nella seguente tabella:

![[rr_fcfs_confronto1.png]]

considerando gli stessi valori per quanto di tempo e context switch, l'efficienza dell'algoritmo RR è perfettamente identica a quella dell'FCFS, pur mantenendo mediamente una varianza minore.
___
##### Shortest Job First

L'algoritmo **Shortest Job First**, spesso abbreviato in **SJF**, si basa su un'idea molto semplice: **hanno priorità maggiore i processi che richiedono un ammontare di lavoro** (per "ammontare di lavoro" si intende la durata dello slancio di CPU) **previsto minore prima del prossimo slancio di I/O o della loro terminazione**.

Vediamo un esempio concreto di **applicazione dell'algoritmo SJF**. Supponiamo di avere i seguenti 4 processi da eseguire:

| Ordine di arrivo | Processo | Slancio di CPU (in unità di tempo) |
| ---------------- | -------- | ---------------------------------- |
| 1                | A        | 6                                  |
| 2                | B        | 8                                  |
| 3                | C        | 7                                  |
| 4                | D        | 3                                  |

Seguendo questa logica, lo scheduler sceglierà prima di eseguire il processo $D$, poi il processo $A$, poi $C$ e infine $B$. In questo modo, la linea temporale relativa all'esecuzione di questi processi sarà la seguente:

![[sjf_esempio.png]]

con un waiting time medio pari a $\frac{0+3+9+16}{4}=7$ unità di tempo. Si noti che lo scheduler non interviene fino al termine dell'esecuzione del processo, o finché il processo stesso non sospende la propria esecuzione: dunque, l'**algoritmo SJF è un algoritmo di [[SO1_04 - Scheduling della CPU#Introduzione allo scheduling|non-preemptive scheduling]]**.

Avendo capito come funziona l'algoritmo SJF, vediamo i **pro** e i **contro**:
- il **pro** principale dell'algoritmo è il **waiting time medio ottimale**;
- i **contro** dell'algoritmo sono la **quasi impossibilità di conoscere la durata del prossimo slancio di CPU** di un processo, così come il fatto che **processi vincolati all'I/O saranno tendenzialmente preferiti a quelli vincolati alla CPU**, dato che per natura dispongono di slanci di CPU minori.

Come appena accennato, un contro dell'algoritmo è rappresentato dalla difficoltà nel conoscere la durata del prossimo slancio di CPU di un processo: infatti, per definizione, l'algoritmo prioritizza i processi "più brevi", ma in questo confronto considera solo lo slancio di CPU precedente alla terminazione o al prossimo slancio di I/O, e ciò porta a volte a risultati inaccurati. Si vuole trovare, perciò, un modo per **stimare la durata del prossimo slancio di CPU di un processo**. 

Un metodo semplice, veloce e relativamente accurato è il cosiddetto "**exponential smoothing**". 

> Indicata con $x_{t}$ la durata effettiva del $t$-esimo slancio di CPU, e con $s_{t\,+\,1}$ la durata prevista per il $(t+1)$-esimo slancio di CPU, e considerato un valore $\alpha\in\mathbb{R}$ con $0\leq \alpha\leq 1$, facciamo valere le seguenti uguaglianze:
> $$\begin{align} &s_{1}=x_{0}\\ &s_{t\,+\,1}=\alpha x_{t}+(1-\alpha)s_{t} \end{align}$$

Dunque, in parole povere, con l'exponential smoothing si fa corrispondere la durata prevista del prossimo slancio di CPU con la **media ponderata tra la durata effettiva dello slancio precedente e la previsione precedente**. Il coefficiente che determina a quale dei due fattori si darà più peso nel calcolo della media è proprio $\alpha$:
- se $\alpha=0$, si ha che $s_{t\,+\,1}=s_{t}$, ossia che la previsione per lo slancio successivo sarà perfettamente identica alla previsione precedente (le durate effettive osservate verranno completamente ignorate, e sostanzialmente si assumerà una durata costante per ogni slancio);
- se $\alpha=1$, si ha che $s_{t\,+\,1}=x_{t}$, ossia che la previsione per lo slancio successivo sarà perfettamente identica alla durata osservata nello slancio di CPU precedente (la "cronologia" delle durate verrà completamente ignorata).

Generalmente, per mantenere un buon equilibrio tra i due fattori, si assume che $\alpha=0.5$.

In precedenza abbiamo specificato che SJF è un algoritmo di non-preemptive scheduling. Tuttavia, è possibile utilizzare una sua variante, ossia l'algoritmo **Shortest Remaining Time First**, o **SRTF**, che è invece un **algoritmo di preemptive scheduling**. Con questo algoritmo, **ogni volta che un nuovo processo entra nella coda `ready`, se la durata stimata per il suo prossimo slancio di CPU è minore della durata rimasta per lo slancio del processo attualmente in esecuzione, quest'ultimo viene sostituito con il primo**. Vediamo subito un esempio per capire meglio come funziona l'algoritmo, supponendo di avere i seguenti processi:

| Processo | Arrival time | Slancio di CPU (in unità di tempo) |
| -------- | ------------ | ---------------------------------- |
| A        | 0            | 8                                  |
| B        | 1            | 4                                  |
| C        | 2            | 9                                  |
| D        | 3            | 5                                  |

Naturalmente, all'inizio c'è solo $A$ nella coda `ready`, dunque lo scheduler avvia subito la sua esecuzione; tuttavia, dopo un'unità di tempo, entra nella coda il processo $B$, e risulta che la durata del suo slancio di CPU è minore di quella rimasta dello slancio di $A$, dunque lo scheduler sostituisce $A$ con $B$; nelle prossime unità di tempo entreranno nella coda `ready` anche $C$ e $D$, ma nessuno dei due processi sarà più "corto" di $B$, e dunque le successive $4$ unità di tempo saranno interamente dedicate all'esecuzione di $B$, fino al suo termine; una volta terminato $B$, il processo con meno slancio di CPU rimasto è $D$, dunque è lui ad essere eseguito, e dato che non arrivano altri processi nel mentre la sua esecuzione proseguirà fino al termine; lo stesso varrà per $A$ e, in seguito, per $C$. Complessivamente, la linea temporale di questo esempio sarà la seguente:

![[srtf_esempio.png]]

con un waiting time medio pari a $\frac{(17-0-8)\,+\,(5-1-4)\,+\,(26-2-9)\,+\,(10-3-5)}{4}=\frac{26}{4}=6.5$ unità di tempo. Notiamo che, **se non si presentano nuovi processi da eseguire, l'algoritmo SRTF si comporta in modo esattamente analogo all'SJF**.

[06, slide 118]
___
##### Priority Scheduling

[06, slide 122 - 126 - 129]
___
##### Multilevel Queue


___
##### Multilevel Feedback Queue


___