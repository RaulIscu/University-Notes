In questo capitolo, si approfondirà un aspetto trattato in parte nel [[SO1_03 - Processi#Come vengono programmati i processi nella CPU?|capitolo precedente]]: lo **scheduling dei processi all'interno della CPU**. In particolare, partiremo con un'introduzione generale, soffermandoci sulle definizioni e i concetti di base, e passeremo in seguito a vari algoritmi e concetti più avanzati applicabili a tale argomento.

## Introduzione allo scheduling

Sappiamo bene che pressoché qualsiasi programma alterna, in qualche modo, fasi incentrate sulla **computazione nella CPU** a fasi che dipendono dall'**I/O**. Assumendo di avere un sistema in grado di eseguire un solo processo alla volta, il tempo passato ad attendere un dato o un evento di I/O è sostanzialmente sprecato, dato che è un lasso di tempo in cui la CPU non lavora e non contribuisce all'esecuzione del [[SO1_03 - Processi|processo]]. Questa rappresenta una delle problematiche principali a cui deve provvedere lo **scheduling**: l'obiettivo, dunque, è sostanzialmente **ottimizzare l'esecuzione dei processi, massimizzando la produttività della CPU e garantendo un'equità di esecuzione tra i vari processi**.

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

Come si può immaginare, il non-preemptive scheduling è un approccio ormai antiquato e che presenta vari limiti, mentre il preemptive scheduling è diventato lo standard per gli OS moderni. Ciononostante, l'implementazione del preemptive scheduling può presentare delle **problematiche**: ad esempio, potrebbe causare comportamenti imprevisti se avviene durante l'esecuzione di una system call, oppure contestualmente a [[SO1_03 - Processi#Come comunicano i processi tra di loro?|processi cooperanti]]. Per ovviare a questi problemi, possiamo implementare soluzioni come fare in modo che **lo scheduling attenda il completamento o il blocco di una system call** prima di attivarsi (benché funzionante, tale soluzione può interferire con eventuali sistemi real-time, dove naturalmente ritardare lo scheduling porterebbe a un ritardo anche nella reattività del sistema).

Nel momento in cui lo scheduler ha scelto il processo da inviare alla CPU, entra in gioco il "**dispatcher**", ossia il modulo che concretamente si occupa di **dare il controllo della CPU a tale processo**. Tra le sue mansioni, dunque, troviamo quella di eseguire il [[SO1_03 - Processi#Come vengono programmati i processi nella CPU?|context switch]], di effettuare la transizione alla modalità utente, e di saltare alla posizione opportuna del programma da far eseguire alla CPU. Per sua natura, **il dispatcher viene eseguito con ogni context switch**, e avendo già stabilito che quest'ultimo rappresenta un'operazione relativamente costosa a livello di tempo e di trasferimento di dati, è cruciale che il dispatcher sia il più veloce possibile, diminuendo la cosiddetta "**dispatcher latency**".

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
- **Priority Scheduling**;
- **Multilevel Queue** (**MQ**);
- **Multilevel Feedback Queue** (**MFQ**);
- **Lottery Scheduling**.

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

Come si può facilmente intuire, l'efficienza di questo algoritmo dipende fortemente dal **quanto di tempo** utilizzato: dei quanti di tempo troppo lunghi portano l'algoritmo quasi a degenerare in un FCFS, dato che i processi termineranno quasi sicuramente la loro esecuzione prima dello scadere del quanto; al tempo stesso, dei quanti di tempo troppo corti implicano un maggior numero di [[SO1_03 - Processi#Come vengono programmati i processi nella CPU?|context switch]], e di conseguenza a un throughput minore. Si dovrà dunque mantenere un **equilibrio**, facendo in modo che **il ritardo dovuto a un context switch sia relativamente piccolo rispetto al quanto di tempo** (ad esempio, spesso un quanto di tempo si aggira tra i $10$ e i $100$ millisecondi in contesti in cui un context switch occupa tra i $0.01$ e i $0.1$ millisecondi).

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
___
##### Priority Scheduling

Gli algoritmi di **Priority Scheduling** consistono, alla base, nell'**assegnare una certa priorità ai vari processi da eseguire**, in modo che lo scheduler mandi in esecuzione i processi nel loro ordine di priorità (dal più importante al meno importante). Si tratta, in realtà, più di una categoria generale di algoritmi che di un algoritmo ben preciso: ad esempio, l'[[SO1_04 - Scheduling della CPU#Shortest Job First|SJF]] è un algoritmo di Priority Scheduling, dove concretamente tale priorità è data dalla durata degli slanci di CPU.

In pratica, le priorità dei processi sono solitamente implementate utilizzando **valori interi compresi in un determinato intervallo**, e spesso valori piccoli corrispondono a priorità alte, con il valore $0$ che corrisponde alla priorità massima. Le priorità dei processi possono essere determinate **internamente** o **esternamente**:
- le priorità determinate internamente sono assegnate dall'OS utilizzando vari criteri, come la durata media di uno slancio di CPU, il rapporto tra slanci di CPU e slanci di I/O, l'ammontare di utilizzo delle risorse di sistema, ecc. ecc.;
- le priorità determinate esternamente sono assegnate dagli utenti, in base all'importanza effettiva del processo.

Inoltre, abbiamo già visto che **gli algoritmi di Priority Scheduling possono essere sia non-preemptive** (come l'SFJ) **che preemptive** (come l'SRTF).

Come tutti gli algoritmi visti e che vedremo, anche gli algoritmi di Priority Scheduling presentano dei **limiti**: ad esempio, una problematica ricorrente è quella della "**starvation**" di determinati processi, che avviene nell'eventualità in cui un processo di bassa priorità non viene mai eseguito a causa del continuo prevaricare di altri processi con priorità più alta; una soluzione parziale a questo problema può essere l'**invecchiamento** di un processo, ossia l'aumento graduale della sua priorità in proporzione al tempo che ha passato in attesa di essere eseguito (ciò garantisce che il processo venga selezionato dallo scheduler in tempi più ragionevoli).
___
##### Multilevel Queue

L'algoritmo **Multilevel Queue**, spesso abbreviato in **MLQ**, può essere riassunto fondamentalmente nell'**utilizzare diverse code distinte, ciascuna destinata a una categoria di processo**. In questo contesto, **ognuna di queste code implementa indipendentemente qualsiasi algoritmo di scheduling sia più consono per la relativa categoria**, e oltre allo scheduling interno alle singole code deve avvenire anche uno **scheduling tra le varie code**. Per quest'ultima caratteristica, due degli approcci più comuni sono:
- mantenere un **ordine di priorità**, assegnando dunque priorità basse o alte alle code stesse, e facendo in modo che nessun processo di una coda con bassa priorità possa essere eseguito finché tutte le code con priorità più alta hanno terminato di eseguire i loro processi;
- adottare un approccio simile al **[[SO1_04 - Scheduling della CPU#Round Robin|Round Robin]]**, in cui ogni coda riceve a turno un certo periodo di tempo per eseguire i propri processi (i periodi di tempo possono variare nella loro durata).

Un esempio di implementazione dell'MLQ può essere il seguente gruppo di code:

![[mlq_esempio.png]]
___
##### Multilevel Feedback Queue

L'algoritmo **Multilevel Feedback Queue**, spesso abbreviato in **MLFQ**, è **molto simile all'[[SO1_04 - Scheduling della CPU#Multilevel Queue|MLQ]]** visto nel paragrafo precedente, con la differenza che, in questo caso, **i processi possono spostarsi da una coda a un'altra**. Ciò può tornare utile in vari contesti, come quando:
- le caratteristiche di un processo passano dall'essere più legate alla CPU rispetto che all'I/O, o viceversa;
- un processo che ha atteso per un lungo periodo di tempo potrebbe essere spostato in una coda con priorità maggiore per favorire la sua esecuzione.

Per garantire una buona efficienza e una certa uniformità di esecuzione tra processi vincolati alla CPU e all'I/O, l'MFLQ implementa il seguente meccanismo:
1. un processo parte sempre, inizialmente, dalla coda con priorità maggiore;
2. se il quanto di tempo destinato al processo in questione termina, il processo viene spostato in una coda di un livello di priorità più bassa;
3. invece, se il quanto di tempo non viene sorpassato (ad esempio, se avviene un context switch a causa di una richiesta di I/O effettuata dal processo stesso), il processo viene spostato in una coda di un livello di priorità più alta (se possibile).

In questo modo, quello che succederà è che **la priorità dei processi vincolati alla CPU tenderà a diminuire**, mentre **i processi vincolati all'I/O tenderanno a rimanere a livelli alti di priorità**.

Sebbene l'MLFQ risulti essere **uno degli algoritmi più flessibili e versatili** visti finora, è anche **il più complesso da implementare**. Si deve pensare, infatti, a un numero sostanzioso di parametri nella progettazione di un sistema MLFQ, ad esempio al **numero di code** da implementare, all'**algoritmo di scheduling utilizzato per ogni coda**, a **come spostare i processi da una coda all'altra**, o in certi casi a **come determinare la coda iniziale di un processo**.

Vediamo un esempio concreto di **applicazione dell'algoritmo MLFQ**. Supponiamo di avere i seguenti tre processi da eseguire:

| Ordine di arrivo | Processo | Slancio di CPU (in unità di tempo) |
| ---------------- | -------- | ---------------------------------- |
| 1                | A        | 30                                 |
| 2                | B        | 20                                 |
| 3                | C        | 10                                 |

Si suppone che nessuno dei processi considerati presenti uno slancio di I/O, che il context switch abbia durata trascurabile, e che si vogliono utilizzare $3$ code con un sistema di priorità tra di esse. A questo punto, indicheremo con:
$$\text{PROCESSO}^{\text{tempoDiEsecuzione}}_{\text{tempoTotalePassato}}$$
il processo $\text{PROCESSO}$ che è stato eseguito per $\text{tempoDiEsecuzione}$ unità di tempo dopo $\text{tempoTotalePassato}$ unità di tempo (ad esempio, $A^{2}_{7}$ indica che il processo $A$ è stato eseguito per $2$ unità di tempo dopo $7$ unità di tempo totali). Ora, impostiamo le 3 code: esse verranno nominate $1$, $2$ e $3$, e come accennato in precedenza più piccolo sarà il numero della coda e più priorità avrà quest'ultima; inoltre, vogliamo assegnare quanti di tempo di durata crescente al decrescere della priorità, dunque considereremo un quanto di $1$ unità di tempo per la coda $1$, $2$ unità di tempo per la coda $2$ e $4$ unità di tempo per la coda $3$. Applicando l'algoritmo, si avrà una situazione del genere:

![[mlfq_esempio.png]]

Proviamo con un altro approccio: supponiamo stavolta di voler utilizzare solo due code, e consideriamo che il processo $C$ alterni la sua esecuzione tra $1$ unità di tempo di slancio di CPU e $1$ unità di tempo di slancio di I/O. Si può verificare che, in questo caso, l'andamento dell'esecuzione assume il seguente aspetto:

![[mlfq_esempio1.png]]

Per certi versi, l'MLFQ cerca di rifarsi al **comportamento ottimale** dell'[[SO1_04 - Scheduling della CPU#Shortest Job First|SJF]] **relativamente al waiting time medio**, e fa così dando per natura più importanza ai processi "corti", che concretamente corrisponderanno spesso a quelli vincolati all'I/O. Tuttavia, così come l'SJF, anche l'MLFQ rischia di essere **poco equo**, a differenza di altri algoritmi come l'[[SO1_04 - Scheduling della CPU#Round Robin|RR]].
___
##### Lottery Scheduling

Il **Lottery Scheduling** è un algoritmo di scheduling diverso da tutti gli altri visti finora, principalmente per una differenza sostanziale: mentre tutti gli altri algoritmi implementavano uno scheduler deterministico, con scelte chiare e priorità ben definite, uno scheduler che implementa il Lottery Scheduling è quasi uno **scheduler "casuale"**. Vediamo perché.

L'idea alla base dell'algoritmo di Lottery Scheduling è quella di **dare a ogni processo un certo numero di "biglietti della lotteria"**, e di **scegliere un "biglietto vincente" ogni quanto di tempo**: in questo modo, l'ordine di esecuzione dei processi sarà determinato dalla distribuzione originale dei biglietti, e per la legge dei grandi numeri ciò dovrebbe **favorire l'equità di esecuzione** tra i vari processi. Va precisato, comunque, che **i biglietti non sono distribuiti proprio in maniera casuale**: infatti, rifacendosi per certi versi all'[[SO1_04 - Scheduling della CPU#Shortest Job First|SJF]], l'algoritmo di Lottery Scheduling impone di assegnare **più biglietti a processi di durata minore**, e viceversa **meno biglietti a processi di durata maggiore**, facendo comunque attenzione ad assegnare almeno un biglietto a ogni processo in modo da evitare la [[SO1_04 - Scheduling della CPU#Priority Scheduling|starvation]] di un processo.

Vediamo un esempio concreto di **applicazione dell'algoritmo di Lottery Scheduling**. Supponiamo, per adesso, di distinguere puramente tra "processi corti" e "processi lunghi", senza entrare troppo nei dettagli; in questo contesto, consideriamo un'implementazione dell'algoritmo che assegna $10$ biglietti a ciascun processo corto e $1$ biglietto a ciascun processo lungo. Possiamo, dunque, ipotizzare vari rapporti tra processi lunghi e corti, e stilare una tabella per verificare quanta probabilità avrà ciascun processo di essere scelto in un quanto di tempo generico:

| Processi corti / Processi lunghi | Prob. di esecuzione per ogni processo corto | Prob. di esecuzione per ogni processo lungo |
| -------------------------------- | ------------------------------------------- | ------------------------------------------- |
| 1/1                              | 91% cca.                                    | 9% cca.                                     |
| 0/2                              |                                             | 50%                                         |
| 2/0                              | 50%                                         |                                             |
| 10/1                             | 9.9% cca.                                   | 0.99% cca.                                  |
| 1/10                             | 50%                                         | 5%                                          |

Come possiamo osservare, se abbiamo precisamente un processo corto e un processo lungo, il primo avrà una probabilità molto maggiore di essere scelto dallo scheduler dato che dispone di più biglietti; anche nel caso in cui si ha un solo processo corto e $10$ processi lunghi, il processo corto disporrà della metà dei biglietti totali, e avrà dunque una probabilità del $50\%$ di essere eseguito per primo; gli stessi principi possono essere osservati anche negli altri esempi.
___
##### Riassunto dei vari algoritmi

Avendo trattato molti degli algoritmi di scheduling principali, in quest'ultimo paragrafo cerchiamo di **ricapitolare le caratteristiche principali di ciascun algoritmo**:
- l'algoritmo First Come First Serve, o **FCFS**, è un algoritmo di **non-preemptive scheduling**, e rappresenta un'opzione **molto semplice** ma anche **poco equa** e con **grande varianza nel waiting time dei processi**;
- l'algoritmo Round Robin, o **RR**, è un algoritmo di **preemptive scheduling**, **molto più equo** e **più o meno efficiente**, ma che può portare a un **waiting time medio maggiore**;
- l'algoritmo Shortest Job First, o **SJF**, è un algoritmo che, in base alla variazione, può funzionare **sia come non-preemptive scheduling che come preemptive scheduling**, è generalmente **non equo** e presenta la possibilità di **starvation di un processo**, ma è **ottimale in termini di waiting time medio**;
- gli algoritmi **MLQ** e **MLFQ** rappresentano una sorta di **perfezionamento dell'SJF**, partendo dagli stessi principi e aggiungendo delle sovrastrutture per rendere il tutto più "flessibile";
- l'algoritmo Lottery Scheduling è un algoritmo **relativamente equo** e con un **waiting time medio moderato**, ma per natura è anche **poco prevedibile**.
___