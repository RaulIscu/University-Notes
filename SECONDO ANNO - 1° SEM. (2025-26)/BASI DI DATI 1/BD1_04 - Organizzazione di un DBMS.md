Finora, ci siamo concentrati sulle varie caratteristiche del [[BD1_01 - Modello relazionale#Cos'è il modello relazionale?|modello relazionale]], sui vincoli che possiamo porre al suo interno, e su come creare dei database strutturati correttamente. All'inizio del corso, abbiamo accennato al fatto che i database vengono generalmente gestiti attraverso dei **DBMS**, o **Database Management System**, ma **cos'è concretamente un DBMS**?

Un DBMS completo e ben strutturato è, in realtà, un connubio di **più parti che lavorano in sincrono**, e che si occupano di varie mansioni, tra cui:
- un **gestore di memoria**;
- un **processore di query relazionali**;
- un **gestore delle comunicazioni con il client**;
- un **gestore dei processi**;
- vari **strumenti di utilità**.

Momentaneamente, andremo a focalizzarci soprattutto sul funzionamento della prima delle componenti elencate, ossia quella che viene anche definita "**strato fisico**".

## Strato fisico

Nello strato fisico si trovano tutti quegli strumenti e componenti che si occupano della **gestione della memoria** concreta, dunque dei dati contenuti nel database (qui troviamo il gestore di memoria, vari buffer, metodi di accesso, ecc. ecc.). Possiamo schematizzare la struttura di questo blocco del DBMS nel modo seguente:

![[stratofisico_struttura.png]]

Per approfondire il funzionamento e la struttura dello strato fisico, partiamo dalla base, cioè dall'**hardware di memoria**, utilizzato per conservare i dati. Quando si parla di memoria, un concetto fondamentale da conoscere è quello di "**gerarchia delle memorie**", ossia della struttura gerarchica in cui tipicamente si distribuiscono i vari livelli di memoria contenuti in un computer. Nell'ipotetica piramide formata da quest'ultimi:
- la **cima** è composta da **memorie più veloci**, ma anche **costose** e **piccole**;
- il **fondo** è composto da **memorie più lente**, ma anche **meno costose** e **più grandi**.

Le memorie più veloci vanno a comporre quella che possiamo definire "**memoria primaria**", o anche "**memoria volatile**", e in ordine crescente di grandezza qui troviamo tipicamente i **registri della CPU**, le **cache** (piccole memorie direttamente collegate alla CPU, che operano quasi alla sua stessa velocità), la **memoria principale** (chip di RAM, più lenti della cache ma anche molto più capienti, che fungono da ponte tra le memorie a disco e la CPU). Quelle più lente, invece, compongono la cosiddetta "**memoria secondaria**", o anche "**memoria persistente**", e qui troviamo tipicamente **HDD** (Hard Disk Drive), **SSD** (Solid State Drive) o altre memorie fisiche ad alta capienza. Ricontestualizzando il tutto nell'ambito di un database, la memoria primaria sarà destinata a contenere **buffer del database** e **codice da eseguire relativo ad applicazioni e altre componenti del DBMS**, mentre la memoria secondaria conterrà **i file del database**.

##### Hard Disk Drives

Facciamo un approfondimento sugli **Hard Disk Drives**, o **HDD** in breve. Si tratta di dispositivi di memoria direttamente accessibili, o di **DASD** in breve, e per contenere i dati sfruttano dei **dischi circolari coperti da particelle magnetiche**, che sono **fissati su un perno che ruota**, quando l'HDD viene utilizzato, **a una velocità costante**; per leggere e scrivere dati su questi dischi, nell'HDD sono presenti anche delle **testine posizionate all'apice di alcuni bracci**, che all'occorrenza vengono messe a contatto con i dischi. A loro volta, i bracci sono fissati a un cosiddetto **attuatore**, che permette di muoverli avanti o indietro per accedere a parti diverse di memoria. È possibile schematizzare la struttura appena descritta nel modo seguente:

![[hdd_struttura.png]]

Ma **quanto tempo ci vuole per leggere o scrivere dei dati con un HDD**? Seguendo la struttura che abbiamo visto, deduciamo che la lettura o scrittura di qualsiasi dato implica innanzitutto il **corretto posizionamento dell'attuatore**, in modo da allineare le testine con la traccia desiderata del disco, e il tempo utilizzato per ottenere ciò viene detto "**seek time**"; a questo punto, si dovrà aspettare che **il settore desiderato del disco ruoti fino ad arrivare sotto la testina**, e questo ulteriore ritardo viene invece denominato "**rotation delay**"; inoltre, c'è anche da considerare un "**transfer time**", che dipende dalla **grandezza del blocco di memoria considerato**, dalla **densità delle particelle magnetiche** che ricoprono i dischi e dalla **velocità di rotazione dei dischi**. Tutti i tempi citati finora contribuiscono al cosiddetto "**service time**", che costituisce dunque il tempo di "risposta" di un HDD quando si vuole leggere o scrivere qualcosa, ma il tempo di risposta effettivo (il "**response time**"), è in realtà dato dalla somma tra il service time e il "**queueing time**", ossia il ritardo dovuto allo scheduling delle varie operazioni che il calcolatore dovrà svolgere.

Considerando la sequenza di operazioni svolte dall'HDD, possiamo stimare approssimativamente con delle formule matematiche il **tempo necessario per leggere o scrivere blocchi di memoria**; per fare ciò, distinguiamo però tra due tipi di accessi, ossia:
- **RBA**, o **Random Block Access**;
- **SBA**, o **Sequential Block Access**.

La principale differenza tra i due sta nella diversa posizione delle testine, e dunque nel seek time: infatti, un RBA è un accesso a un blocco generico di memoria dove si assume che le testine debbano effettivamente spostarsi per raggiungerlo, e dunque tiene conto del seek time; al contrario, un SBA è un accesso sequenziale a blocchi di memoria contigui, dunque si assume che le testine siano già posizionate sulla traccia giusta e perciò il seek time non viene più considerato.

Indichiamo il tempo necessario per un RBA con $T_{RBA}$, e quello necessario per un SBA con $T_{SBA}$, e questi due valori potranno essere ottenuti con le seguenti formule:
$$T_{RBA}=\text{seek time}+\frac{ROT}{2}+\frac{BS}{TR}\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,T_{SBA}=\frac{ROT}{2}+\frac{BS}{TR}$$
dove con $ROT$ si intende il **tempo di rotazione** di un disco, con $BS$ la **grandezza del blocco di memoria** e con $TR$ il "**transfer rate**", ossia l'ammontare di memoria trasferito per unità di tempo.
___
##### Da concetti logici a blocchi di dati fisici

Naturalmente, lavorando con [[BD1_04 - Organizzazione di un DBMS#Hard Disk Drives|HDD]] o, in generale, con qualsiasi dispositivo di memoria, l'obiettivo è di **organizzare i dati e l'hardware in modo da minimizzare il più possibile qualsiasi ritardo nella lettura o scrittura**, e per quanto riguarda i dispositivi di memoria analizzati nel paragrafo precedente queste minimizzazioni possono essere effettuate soprattutto sul **seek time** e, parzialmente, sul **rotation delay**; oltre a ciò, si desidera anche **minimizzare il numero di RBA**, dato che naturalmente impiegano più tempo ad essere effettuati rispetto agli SBA.

Per poter pensare a queste problematiche, un creatore di basi di dati fisiche deve pensare ai modi più ottimali per **trasformare concetti e modelli logici di dato in strutture dati fisiche**, in modo da ottenere il miglior bilancio possibile tra una **lettura e scrittura efficiente** in termini di tempo e un **utilizzo intelligente dello spazio di memoria**. Per questo obiettivo, un'organizzazione adiacente al [[BD1_01 - Modello relazionale|modello relazionale]] su cui ci siamo soffermati finora nel corso risulta molto utile. Per capire come questi concetti possano essere collegati, vediamo la seguente tabella, dove ogni colonna rappresenta uno dei "passaggi" di questa trasformazione, e ciascuna riga un certo tipo di dato:

| Modello astratto                       | Modello logico-relazionale          | Modello fisico                                                      |
| -------------------------------------- | ----------------------------------- | ------------------------------------------------------------------- |
| Attributo e tipo di attributo          | Valore (cella) e nome della colonna | Dato (bit o caratteri rappresentanti un determinato valore)         |
| Singola entità                         | Riga o tupla                        | Collezione di dati, che rappresenta tutti gli attributi dell'entità |
| Insieme delle entità dello stesso tipo | Tabella o relazione                 | File o blocco di dati                                               |
| Insieme di tipi di entità              | Insieme di tabelle o relazioni      | Database                                                            |

A livello fisico, come anticipato dalla tabella, **un database consiste in un insieme di file**; ogni file, a sua volta, può essere visto come una **collezione di "pagine" di dimensione fissa**; ogni pagina, al suo interno, conterrà **diverse entità**, ciascuna corrispondente a una [[BD1_01 - Modello relazionale#Domini, tuple e relazioni|tupla]] per intenderci; infine, ciascuna tupla sarà composta da **un certo numero di campi**, di dimensione fissa o variabile, che rappresentano gli [[BD1_01 - Modello relazionale#Attributi|attributi]] della tupla.
___
## File

È chiaro, dunque, che il fulcro di un database sono i **file**, che costituiscono la sovrastruttura principale in cui sono organizzati i dati contenuti al suo interno.

Ma **come sono organizzati internamente i file**? Ci sono varie modalità alternative per distribuire i dati all'interno di un file, e di conseguenza in base ad esse ci sono diversi **tipi di file**, tra cui:
- **heap file**;
- **sequential file**;
- **random file**;
- **indexed sequential file**.

Analizziamo ciascuna di queste strutture più nel dettaglio. 

##### Heap file

Si tratta di un'**organizzazione basilare e comune**, dove **nuove entità sono aggiunte al termine del file**, e dove **non è presente una relazione tra attributi dell'entità e la loro posizione in memoria**. Evidentemente, basandoci su queste caratteristiche, l'unico modo per trovare un'entità ben precisa all'interno di un heap file è la **ricerca lineare**, ossia scorrere ciascuna delle entità del file una dopo l'altra finché non verrà trovata quella che corrisponde alla chiave di ricerca; quest'ultima, del resto, diventa ancora più inefficiente nel momento in cui tale chiave non è univoca all'interno del file, dato che ciò richiede che tutto il file venga interrogato in modo da assicurarsi di trovare tutte le entità al suo interno che corrispondono alla chiave di ricerca. Data la natura del file, per un file con $NBLK$ blocchi si dovranno controllare una media di $\frac{NBLK}{2}$ entità per trovare quella desiderata.
___
##### Sequential file

Pur rimanendo molto semplice, è un passo avanti rispetto all'[[BD1_04 - Organizzazione di un DBMS#Heap file|heap file]]: in questo caso, **le entità vengono memorizzate in ordine crescente o decrescente rispetto alla loro chiave di ricerca**. Si tratta di un piccolo cambiamento, ma che permette di aumentare l'efficienza in vari contesti: innanzitutto, supponendo che si vogliano recuperare **più entità contigue in ordine**, la struttura del sequential file permetterebbe di **effettuare una ricerca lineare esclusivamente con degli [[BD1_04 - Organizzazione di un DBMS#Hard Disk Drives|SBA]]**, che sappiamo essere più efficienti degli RBA; al tempo stesso, pur rimanendo la ricerca lineare una scelta possibile, per trovare una determinata entità sarà possibile effettuare una **ricerca binaria**, che porterà inevitabilmente a un'esecuzione di un numero molto minore di accessi, in media $\log_{2}NBLK$ (ciononostante, precisiamo che gli accessi in questione sarebbero prevalentemente degli RBA, dato che l'algoritmo di ricerca binaria prevede di spostarsi da un punto all'altro dell'insieme di entità).

Per comprendere quanto quest'ultimo approccio risulti essere più efficiente, vediamo un esempio: supponiamo di avere un sequential file contenente $NR=30\,000$ entità, dove una singola entità avrà dimensione $RS=100$ byte, e con la dimensione di un singolo blocco di memoria pari a $BS=2048$ byte; possiamo ottenere il numero $BF$ di entità contenute in un blocco dividendo la dimensione di un blocco di memoria per la dimensione di un'entità ($BF=\frac{BS}{RS}=\frac{2048}{100}\approx 20$), e in seguito il numero $NBLK$ di blocchi del file dividendo il numero di entità per il valore appena trovato ($NBLK=\frac{NR}{BF}=\frac{30\,000}{20}=1500$). A questo punto, possiamo stimare il numero di accessi a blocchi di memoria che ci si aspetta debbano essere eseguiti per trovare un'entità generica all'interno del file. Come abbiamo detto, la ricerca lineare necessita in media $\frac{NBLK}{2}$ accessi e, in un sequential file, sarebbero tutti accessi a blocchi di memoria contigui, dunque ci si aspettano: $$\frac{1500}{2}\text{ SBA} = 750 \text{ SBA}$$Se utilizzassimo, invece, la ricerca binaria, allora impiegheremmo in media:
$$\log_{2}1500\text{ RBA}\approx 11\text{ RBA}$$

Tuttavia, il sequential file è **meno efficiente** dell'heap file su un aspetto, ossia l'**aggiornamento dei dati contenuti al suo interno**: per ovviare a questa inefficienza, spesso si preferisce aggiungere, rimuovere o modificare entità in gruppi.
___
##### Random file

Stavolta, troviamo un'organizzazione che si basa sull'**hashing**: in questa struttura, **si assegna a un'entità una posizione in memoria in base alla sua chiave di ricerca**. Ciò implica una diretta relazione tra chiave di ricerca di un'entità e la sua posizione fisica, che permette di **trovare un'entità specifica con uno o pochi accessi**. 

Come è facile dedurre, l'hashing non può garantire che tutte le chiavi siano mappate a indirizzi diversi di memoria, di conseguenza ci sono quelle che vengono chiamate "**bucket addresses**", ossia indirizzi che indicano blocchi di memoria destinati a contenere più entità. È, dunque, perfettamente possibile che **più entità vengano mappate allo stesso indirizzo**: le entità che sono contenute nella stessa bucket address vengono dette "**sinonimi**". Nel caso in cui si cerca di inserire più sinonimi di quanti la bucket address sia capace di contenere, si ha un "**overflow**", e ciò comporta la necessità di accessi aggiuntivi per ottenere eventuali entità in overflow; generalmente, per evitare il più possibile quest'evenienza, **un algoritmo di hashing dovrebbe cercare di distribuire le chiavi di ricerca nel modo più uniforme possibile** tra le varie bucket addresses.

Possono essere utilizzati svariati **algoritmi di hashing** per assegnare un indirizzo di memoria a una determinata chiave di ricerca, più o meno complessi. Uno dei più semplici e comuni è il seguente:
$$\text{address(key)}=\text{key mod M}$$
dove per $\text{mod}$ si intende l'operazione di "modulo", ossia il resto della divisione tra i due operandi (in questo caso, $\text{key}$ e $\text{M}$), mentre $\text{M}$ è, tendenzialmente, un numero primo, pari o leggermente più grande del numero di indirizzi disponibili. 

L'**efficienza di un algoritmo di hashing** si misura in base al **numero previsto di [[BD1_04 - Organizzazione di un DBMS#Hard Disk Drives|RBA]] e di [[BD1_04 - Organizzazione di un DBMS#Hard Disk Drives|SBA]]**: ad esempio, per l'algoritmo di hashing che abbiamo appena visto, ottenere un'entità che non si trova in overflow dovrebbe richiedere $1$ RBA per entrare nella bucket address prevista, e in seguito $1$ o più SBA per ottenere l'entità cercata. Per quanto riguarda il numero di accessi aggiuntivi richiesti per accedere ad entità in overflow, ciò dipende dalla percentuale media di entità in overflow e dalla tecnica di gestione degli stessi.

Ma **come capire quante bucket addresses conviene avere?** Per ottenere il numero $NB$ di bucket addresses necessarie per contenere un certo numero $NR$ di entità, è possibile utilizzare la seguente formula:
$$NB=\frac{NR}{BS\times LF}$$
dove $BS$ è la **dimensione del bucket**, mentre $LF$ rappresenta il cosiddetto "**loading factor**". Nel decidere il valore di $BS$, è importante tenere a mente che una dimensione maggiore del bucket porta a una minore possibilità di overflow, ma anche a un ulteriore lavoro necessario per ottenere le entità non in overflow: è dunque importante optare per un valore che bilancia questi due fattori. Per quanto riguarda $LF$, esso indica all'incirca quanto si vuole riempire ciascun bucket in media, ed è solitamente impostato con un valore tra $0.7$ e $0.9$.

Come abbiamo detto, ci sono diversi **modi per gestire un overflow**. Uno dei più basilari è il cosiddetto "**open addressing**": sostanzialmente, nel momento in cui un bucket va in overflow, l'entità che ha causato l'overflow viene memorizzata nel primo spazio libero trovato dopo il bucket in questione. In questo modo, per ottenere un'eventuale entità in overflow, saranno necessari $1$ RBA e tanti SBA quanti serviranno per arrivare al blocco dove è stata memorizzata l'entità.
___
##### Indexed sequential file

Mentre l'organizzazione di un [[BD1_04 - Organizzazione di un DBMS#Random file|random file]] risulta essere particolarmente efficiente per ottenere singole entità in base alla loro chiave di ricerca, e quella del [[BD1_04 - Organizzazione di un DBMS#Sequential file|sequential file]] per ottenere più entità in ordine, la struttura dell'**indexed sequential file** risulta essere una sorta di via di mezzo tra le due, combinando l'organizzazione sequenziale del secondo con l'utilizzo di uno o più "**indici**", similmente alle bucket addresses del primo.

Un indexed sequential file è diviso in **intervalli**, detti anche "**partizioni**", e ciascuna partizione è indicata da un **indice** contenente la **chiave di ricerca della prima entità della partizione** e un **puntatore alla posizione fisica di tale entità**. In particolare, quest'ultimo può essere:
- un **puntatore a un blocco**, dunque all'indirizzo di memoria di tale blocco;
- un **puntatore all'entità**, dunque una combinazione dell'indirizzo del blocco e di un ID, oppure di un valore di offset all'interno del blocco.

Le posizioni fisiche effettive, dunque il luogo dove sono conservate le entità, è concretamente un sequential file, ordinato in base alla chiave di ricerca.

A seconda di **quanti indici si vogliono utilizzare**, si può avere un'organizzazione di tipo "**dense index**", dove si ha un indice per ogni valore possibile della chiave di ricerca, o di tipo "**sparse index**", dove si ha un indice solo per alcuni dei valori possibili, e dunque dove ogni indice si riferisce in realtà a un gruppo di entità. Anche qui, entrambe le strategie hanno i loro pro e contro: infatti, **il dense index è generalmente più veloce**, ma **occupa anche più memoria ed è più complesso da mantenere**, e viceversa per lo sparse index.

[21 - slide 34/37]
___
## Alberi

Gli **alberi** rappresentano una delle strutture dati più importanti e versatili nel mondo dell'informatica. Ma cosa sono concretamente?

A livello base, **un albero è un insieme di "nodi"**, che **derivano uno dall'altro** in modo simile a come un albero cresce dalle sue radici (con l'eccezione che, mentre un albero reale cresce dal basso verso l'alto, gli alberi dell'informatica tendenzialmente si sviluppano dall'alto verso il basso). Nel nostro caso, abbiamo **un nodo "radice"**, che sarà il punto di partenza dell'albero; **ogni nodo** dello stesso, ad eccezione della radice, **ha esattamente un nodo "genitore"** e **può avere nessuno, uno o più nodi "figli"**. Dei nodi che hanno lo stesso genitore sono detti anche "**fratelli**", e tutti i figli, figli di figli, e così via di un nodo sono i suoi "**discendenti**". Come abbiamo detto, un nodo può anche non avere figli: **un nodo privo di figli è detto "foglia" dell'albero**. Infine, per chiudere questo elenco di vocabolario relativo agli alberi, **un albero costituito da un nodo che non è radice e da tutti i suoi discendenti** è detto un "**sotto-albero**".

I nodi di un albero sono distribuiti in più **livelli**, che rappresentano la distanza dei loro nodi dalla radice. Un albero dove **tutte le foglie si trovano sullo stesso livello** si dice "**bilanciato**", mentre un albero che non ha questa caratteristica è di conseguenza "**non bilanciato**".

Gli alberi possono essere utilizzati, nel nostro contesto, per fornire:
- una **rappresentazione concreta di una gerarchia**, come ad esempio una gerarchia di impiegati di un'azienda;
- una **struttura fisica di indici**, che può essere utilizzata (ad esempio in un [[BD1_04 - Organizzazione di un DBMS#Indexed sequential file|indexed sequential file]]) per velocizzare la ricerca e l'ottenimento delle entità.

##### Implementazione di un albero

Ci si chiede, a questo punto, **come possiamo implementare concretamente un albero** in modo da utilizzarlo come struttura dati?

Un modo semplice ma comunque efficace è la **contiguità dei nodi in memoria**: in una sequenza che va **dall'alto verso il basso** e **da sinistra verso destra**, si memorizza prima la radice, poi il primo figlio della radice, poi se quest'ultimo ha a sua volta figli si passa al primo figlio dello stesso, e così via. Dunque, **se un nodo non ha più figli, si passa al suo prossimo fratello da sinistra a destra**, e **se un nodo non ha più fratelli, si passa al prossimo fratello del suo genitore**. Ogni nodo contiene, oltre a un certo dato, anche il **livello dove si trova**. Vediamo un esempio di questo tipo di implementazione:

![[albero_implementazione_esempio.png]]

Le lettere rappresentano le ipotetiche chiavi di ricerca delle entità rappresentate dai nodi, mentre i numeri rappresentano il livello occupato dal nodo in questione nell'albero. Questo tipo di implementazione può essere navigato solo ed esclusivamente in modo **sequenziale**, nell'ordine esposto nello schema.

È possibile implementare un albero anche in un altro modo, un po' più complesso: le **linked lists**. In questo caso, alla contiguità fisica propria dell'approccio precedente si aggiungono anche dei **puntatori**: in particolare, **ogni nodo avrà un puntatore al suo prossimo fratello**, se esiste. In questo modo, sarà possibile navigare l'albero sia nell'**ordine genitore-figlio** (considerando i nodi nell'ordine in cui compaiono in memoria) sia nell'**ordine fratello-fratello** (considerando i puntatori contenuti nei nodi). In questo tipo di implementazione, viene spesso aggiunto a ogni nodo anche un **bit di controllo** che indica se il nodo in questione è una foglia (`0`) o no (`1`). Vediamo un esempio di questo tipo di implementazione:

![[albero_implementazione_esempio1.png]]
___
##### Alberi di ricerca binari e non

Un **albero binario di ricerca** è, sostanzialmente, un albero dove **ogni nodo ha al massimo due figli**. Dunque, contestualizzando, ogni nodo contiene una **chiave di ricerca** e **un massimo di due puntatori a nodi figli**; entrambi questi ipotetici figli potranno essere visti come radici di **due sottoalberi**, uno contenente esclusivamente **chiavi di ricerca minori di quella contenuta nel nodo originale** e l'altro contenente esclusivamente **chiavi di ricerca maggiori**.

Come si può intuire, questa struttura favorisce notevolmente l'**efficienza nella ricerca di entità specifiche** sfruttando la **ricerca binaria**: infatti, a ogni iterazione di tale algoritmo, andremmo attivamente a saltare circa metà dei nodi a nostra disposizione. Vediamo più nel dettaglio come funzionerebbe la ricerca binaria su un albero del genere: supponiamo di avere un albero binario di ricerca contenente nodi con varie chiavi di ricerca $K_{i}$, e di voler cercare il nodo con chiave $K_{\mu}$; il primo nodo che andiamo a controllare è la radice dell'albero, e a questo punto possono verificarsi tre scenari:
- se $K_{i}=K_{\mu}$, allora abbiamo trovato il nodo che cercavamo;
- se $K_{i}>K_{\mu}$, allora seguiamo il puntatore per il sottoalbero sinistro, ossia quello contenente le chiavi di ricerca minori di $K_{i}$;
- se $K_{i}<K_{\mu}$, allora seguiamo il puntatore per il sottoalbero destro, ossia quello contenente le chiavi di ricerca maggiori di $K_{i}$.

Applicando questi passaggi ricorsivamente sugli eventuali sottoalberi, si troverà il nodo cercato. Vediamo, ad esempio, l'applicazione di questo algoritmo nel seguente albero, ipotizzando di star cercando il nodo con chiave $K_{\mu}=24$:

![[alberobinario_esempio.png]]

Possiamo generalizzare i concetti esposti finora introducendo i cosiddetti "**alberi $m$-ari di ricerca**", dove ogni nodo ha al massimo $m$ figli. In questo tipo di struttura, ogni nodo assume una forma del genere:

![[alberom-ario_strutturanodo.png]]

dove $P_{0},\,P_{1},\,\dots,\,P_{n}$ sono **puntatori ai figli del nodo**, mentre $K_{0},\,K_{1},\,\dots,\,K_{n-1}$ sono le **chiavi di ricerca contenute nel nodo**. Le chiavi sono sempre contenute in **ordine crescente**, e valgono le seguenti proprietà:
- un singolo nodo contiene $n$ chiavi e $n+1$ puntatori, con $n+1\leq m$;
- tutte le chiavi contenute nel sotto-albero indicato dal puntatore $P_{i}$ sono minori di $K_{i}$;
- tutte le chiavi contenute nel sotto-albero indicato dal puntatore $P_{i+1}$ sono maggiori di $K_{i}$.

Come possiamo notare, dunque, in un albero $m$-ario **un singolo nodo può contenere più chiavi di ricerca**, in particolare può contenere **tra $1$ e $m-1$ chiavi**; al tempo stesso, il **numero di figli** può variare **tra $0$ e $i+1$**, dove $i$ è il numero di chiavi contenute nel nodo. In questo contesto, dunque, $m$ rappresenta un **limite superiore al numero di chiavi che un nodo può contenere**. Un esempio concreto di albero $m$-ario può essere il seguente:

![[alberom-ario_esempio.png]]

Gli alberi $m$-ari tornano molto utili anche nel contesto degli **[[BD1_04 - Organizzazione di un DBMS#Indexed sequential file|indexed sequential file]]**: è possibile, infatti, costruire tale struttura come un albero $m$-ario i cui nodi, oltre a chiavi e puntatori ai figli, contengono anche dei puntatori $P_{r}$ alle entità effettive (convenzionalmente, questi puntatori ad entità vengono inseriti dopo ogni chiave). Di seguito, una schematizzazione di questo utilizzo:

![[alberom-ario_indice.png]]

Nonostante la loro grande versatilità, gli alberi $m$-ari presentano un grande **limite**: **non abbiamo controllo su come vengano inserite le chiavi al loro interno**. Ad esempio, considerando un ipotetico albero $10$-ario, dunque in cui ogni nodo contiene al massimo $9$ chiavi, inizialmente vuoto, e volendo inserire al suo interno le chiavi $10$, $20$ e $30$, potrebbe benissimo crearsi una situazione del genere:

![[alberom-ario_inserimentoerrato_esempio.png]]

Come si può facilmente dedurre, un assetto del genere risulterebbe profondamente inefficace, e in generale con $m$ chiavi potremmo finire ad avere un albero di altezza $m$, con un costo di navigazione simile a quello della ricerca binaria. L'approccio migliore sarebbe **cercare di riempire prima il primo nodo**, e poi passare a eventuali figli in seguito. Per venire incontro a questa esigenza, si introducono i **[[BD1_04 - Organizzazione di un DBMS#$B$-trees|B-trees]]**, che verranno approfonditi nel prossimo paragrafo.
___
##### $B$-trees

Un **$B$-tree di ordine $m$** è definito come un **[[BD1_04 - Organizzazione di un DBMS#Alberi di ricerca binari e non|albero di ricerca]] $m$-ario "auto-bilanciato"**, che rispetta le seguenti proprietà:
1. ogni nodo ha **al massimo $m$ figli**;
2. ogni nodo, eccetto la radice e le foglie, ha **almeno $\frac{m}{2}$ figli**;
3. **la radice ha almeno due figli**;
4. **tutte le foglie sono sullo stesso livello**;
5. la creazione dell'albero avviene "al contrario".

La seconda proprietà, in particolare, provvede direttamente alla problematica sollevata alla fine del paragrafo precedente, dato che in un $B$-tree si dovrà necessariamente riempire un nodo almeno fino a metà prima di creare nuovi figli, e così facendo si controlla l'altezza dell'albero.

I $B$-tree, dunque, risultano essere un ottimo **indice strutturato ad albero**, dove **ogni nodo rappresenta un blocco del disco** e dove **i nodi sono mantenuti tra mezzi pieni e pieni**, in modo da favorire una distribuzione uniforme. Ogni nodo conterrà:
- un insieme di **chiavi di ricerca**;
- un insieme di **puntatori ai figli del nodo**;
- un insieme di **puntatori a entità o a gruppi di entità**, corrispondenti alle chiavi di ricerca.

Si precisa che, naturalmente, le entità effettive non fanno in alcun modo parte del $B$-tree, e sono conservate separatamente.

Per comprendere meglio il funzionamento dei $B$-tree, vediamo un esempio. Supponiamo di avere un $B$-tree di ordine $4$ inizialmente vuoto, e di voler inserire al suo interno le chiavi $10$, $20$, $40$ e $50$. Un singolo nodo può contenere al massimo $m-1$ chiavi, dunque non abbiamo problemi nell'aggiungere $10$, $20$ e $40$, ma arrivati a $50$ finiamo lo spazio, trovandoci nella seguente situazione:

![[btree_esempio.png]]

È a questo punto che possiamo "dividere" il nodo e creare dei figli. Dunque, generiamo due figli e dividiamo le chiavi tra di essi, nel modo seguente:

![[btree_esempio1.png]]

Supponiamo, a questo punto, di voler aggiungere altre chiavi, come $60$, $70$ e $80$. Come abbiamo detto, il $B$-tree cresce dalle foglie, dunque andiamo innanzitutto ad aggiungere $60$ al figlio di destra, essendo $60$ maggiore di $40$; facciamo lo stesso per $70$ senza intoppi, ma notiamo che quando dobbiamo aggiungere $80$, e ci troviamo dunque in questa situazione:

![[btree_esempio2.png]]

incappiamo di nuovo nello stesso problema. Perciò, andiamo nuovamente a dividere il nodo in questione, e dato che l'albero deve crescere verso l'alto quello che andiamo a fare è spostare $70$ nel genitore e creare un nuovo figlio dove inseriamo la chiave $80$, nel modo seguente:

![[btree_esempio3.png]]

Ancora, supponiamo di voler aggiungere anche le chiavi $30$ e $35$. La chiave $30$ è minore di $40$, dunque possiamo inserirla nel primo dei figli senza problemi. Tuttavia, lo stesso non si può dire per la chiave $35$, che dovrebbe andare nello stesso nodo ma che non ha spazio libero per farlo: occorrerà dividere nuovamente il nodo, trasferendo $30$ al nodo superiore e creando un nuovo figlio dove inserire $35$, nel modo seguente:

![[btree_esempio4.png]]

A questo punto, notiamo che abbiamo riempito completamente il nodo al livello superiore, sia di figli che di chiavi. Ciò andrà a complicare le cose se vogliamo continuare ad aggiungere chiavi: ad esempio, se volessimo inserire le chiavi $5$ e $15$, non avremmo problemi a inserire $5$ nel primo dei figli, ma avremo problemi nell'inserire $15$, che dovrebbe essere inserito sempre nello stesso nodo di $5$. Dunque, a partire da questa situazione:

![[btree_esempio5.png]]

per aggiungere $15$ dovremo andare a dividere sia il primo figlio che il genitore. Quello che facciamo, dunque, è dividere il genitore creando un nodo a un livello superiore contenente solo la chiave $40$ e avente due figli, il primo contenente $15$ e $30$ e il secondo $70$; di conseguenza, andiamo a ricollegare gli ultimi due figli della serie al secondo nodo del livello intermedio, e poi a dividere il primo nodo del livello inferiore in due nodi, il primo contenente $5$ e $10$ e il secondo contenente $20$; i nodi del livello inferiore contenenti $5$ e $10$, $20$ e $35$ verranno ricollegati al nodo contenente $15$ e $30$, portandoci ad avere una struttura del genere:

![[btree_esempio6.png]]

Vediamo un altro esempio, stavolta con un $B$-tree di ordine $5$, ossia in cui ciascun nodo può contenere al massimo $4$ chiavi. Stavolta, non partiamo da un albero vuoto, ma cominciamo la nostra analisi dalla situazione seguente:

![[btree_esempio7.png]]

 Notiamo subito che, per adesso, il $B$-tree rispetta le proprietà necessarie (la radice ha un numero di figli compreso tra $2$ ed $m$, tutte le foglie sono sullo stesso livello, ecc. ecc.); inoltre, per chiarezza, specifichiamo che i quadratini nello schema rappresentano i puntatori ai figli dei rispettivi nodi, che in una situazione del genere sono in realtà dei puntatori `NULL`. Supponiamo di voler aggiungere $10$ all'albero: tale operazione può essere fatta senza problemi, essendoci ancora spazio nel primo figlio della radice, portando alla seguente situazione:

![[btree_esempio8.png]]

Se volessimo aggiungere anche $11$, però, notiamo che finiamo lo spazio nel primo figlio della radice, dunque sarà necessario dividere il nodo in questione. Andiamo dunque a spostare $8$ (è il valore centrale dei 5, dunque quello che favorirà la maggiore uniformità di riempimento tra i nodi) nella radice, e a dividere il primo figlio della stessa in due nodi, il primo contenente le chiavi minori di $8$ (ossia $2$ e $3$) e il secondo contenente le chiavi maggiori (ossia $10$ e $11$):

![[btree_esempio9.png]]

Finora, in entrambi gli esempi, abbiamo sempre visto cosa succede quando si vogliono aggiungere dei valori ai nostri $B$-tree; ma come facciamo invece a rimuoverli? Supponiamo, ad esempio, di voler rimuovere dall'albero appena ottenuto la chiave $8$, situata nella radice: si potrebbe pensare di spostare nella radice una delle chiavi contenute in uno dei primi due figli, per preservare la struttura esistente; tuttavia, ciò porterebbe il figlio in questione ad avere troppi pochi figli (rimuovendo una chiave, si rimuoverebbe anche un figlio, e sappiamo che i nodi interni devono avere tra $\frac{m}{2}$ e $m$ figli). Perciò, l'unica soluzione possibile è fondere i primi due figli della radice, e semplicemente rimuovere $8$ da quest'ultima:

![[btree_esempio10.png]]

Ora, vogliamo rimuovere anche $13$ dal $B$-tree. Semplicemente rimuovere $13$ dal suo nodo senza ulteriori aggiustamenti porterebbe il nodo in questione ad avere troppi pochi figli, dunque quello che possiamo fare è una serie di spostamenti di chiavi tra i tre nodi dell'albero: dopo aver rimosso $13$ dal secondo figlio, spostiamo $12$ dalla radice al secondo figlio, e di conseguenza spostiamo $11$ dal primo figlio alla radice. In questo modo, finiamo in una situazione del genere:

![[btree_esempio11.png]]

E se volessimo rimuovere anche $11$? In questo caso, per preservare la radice mantenendo, al tempo stesso, il numero minimo di chiavi negli altri nodi, possiamo eliminare $11$ dalla radice e rimpiazzarlo spostandoci $10$ dal primo figlio:

![[btree_esempio12.png]]



[21 - slide 81/95]
___
##### $B^{+}$-trees

[21 - slide 96/99]
___