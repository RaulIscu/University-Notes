Una delle mansioni più importanti di un OS all'interno di un calcolatore è una corretta **gestione della memoria**. Per ottenere ciò, l'OS deve puntare al compimento dei seguenti obiettivi:
- allocare correttamente memoria e risorse ai vari [[SO1_03 - Processi|processi]] e [[SO1_05 - Thread#Cos'è un thread?|thread]], **massimizzando l'utilizzo della memoria e il throughput del sistema**;
- garantire l'isolamento tra i vari processi, assicurando l'**indirizzabilità** e la **protezione tra processi**;
- fornire un'astrazione della memoria conveniente per l'utente, fornendo un'illusione di memoria illimitata tramite l'utilizzo di **memoria virtuale**.

Nei seguenti paragrafi, si approfondiranno i diversi modi in cui l'OS consegue questi obiettivi.

## Allocare memoria a processi e thread

##### Address binding

Partiamo dalle basi: quando un programmatore scrive un programma, e dunque del codice sorgente, **come fa il calcolatore ad eseguire tale programma?** Tipicamente, i programmi scritti da un utente fanno riferimento a dati e istruzioni specifici attraverso dei **nomi simbolici**, come `+`, `&&`, `count`, ecc. ecc.; per permettere l'esecuzione di un programma il cui codice contiene tali nomi, si dovrà:
1. **"tradurre" il codice sorgente in un file binario eseguibile**, che verrà conservato nella memoria a disco del calcolatore;
2. **caricare l'eseguibile nella memoria principale**, comunemente indicata come RAM.

Questi due passaggi fondamentali vengono eseguiti da diverse entità nel calcolatore: la traduzione da codice sorgente a file binario avviene grazie a **compilatori**, **assemblers** e **linkers** (nel caso di programmi scritti in linguaggi interpretati, la traduzione avviene invece quasi a runtime, ed è operata dall'interprete scelto); invece, il programma viene caricato in RAM dal **loader** dell'OS. 

Una volta ottenuto un eseguibile a partire da un programma, per poter **eseguire concretamente tale programma** la CPU dovrà ottenere ("**fetch**"), decodificare ("**decode**") ed eseguire ("**execute**") la serie di istruzioni contenuta al suo interno, e per fare ciò dovrà naturalmente accedere alla memoria. Inoltre, molte di queste istruzioni saranno istruzioni che richiederanno continue interazioni con la memoria, siano esse di **recupero** o di **scrittura di dati**, o anche entrambe in certi casi. Dato che per poter interagire con i chip della memoria si dovrà necessariamente far utilizzo di **indirizzi di memoria fisici**, sarà necessario **istanziare un qualche collegamento tra nomi simbolici contenuti nel programma e indirizzi fisici di memoria**. Ciò può avvenire attraverso la seguente scaletta:
1. **il nome simbolico**, ossia un riferimento simbolico alla memoria utilizzato all'interno del codice sorgente, **viene associato a un "indirizzo logico"**, ossia un indirizzo di memoria generato durante l'esecuzione del programma tramite la CPU;
2. **l'indirizzo logico viene poi convertito in un indirizzo fisico**, ossia un indirizzo di memoria effettivo, sul quale possono operare i chip della memoria e che conterrà il dato considerato.

Mentre il passaggio tra nome simbolico e indirizzo logico è relativamente semplice, quello tra indirizzo logico e indirizzo fisico, detto anche "**address binding**", non è così immediato. Innanzitutto, tale conversione può avvenire in $3$ momenti ben distinti:
- durante la **compilazione** del programma;
- durante il **caricamento** e l'**avvio** del programma;
- durante l'**esecuzione** del programma.

L'address binding che avviene **durante la compilazione** richiede che **si sappia l'indirizzo fisico di partenza del programma** considerato nella memoria. Se vale tale condizione, il compilatore potrà generare del cosiddetto "**codice assoluto**", e sostanzialmente **l'indirizzo fisico coinciderà con l'indirizzo logico**. Naturalmente, basandosi il tutto sull'indirizzo di memoria dove si trova il programma, se per qualche motivo esso cambia dopo la compilazione allora il programma dovrà essere ricompilato per assicurarne la corretta esecuzione.

L'address binding che avviene **durante il caricamento e l'avvio** avviene quando **non si è necessariamente a conoscenza**, durante la compilazione, **dell'indirizzo fisico di partenza del programma** considerato nella memoria. In questo caso, il compilatore genera del "**codice statico rilocalizzabile**", che si basa su indirizzi relativi all'ipotetico indirizzo di partenza $k$; sarà, in seguito, il loader dell'OS a determinare l'indirizzo fisico effettivo del programma (ossia $k$), e ad aggiustare gli indirizzi relativi generati dal compilatore in base a quest'ultimo (dunque, anche stavolta, **indirizzi logici e indirizzi fisici finiranno per coincidere**). Con questo approccio, se il programma dovesse per qualche motivo cambiare posizione in memoria dopo la compilazione, esso non dovrà necessariamente essere ricompilato, ma dovrà sicuramente essere riavviato dal loader.

L'address binding che avviene **durante l'esecuzione** avviene quando **è possibile che il programma venga spostato nella memoria principale durante l'esecuzione dello stesso**. In questo caso, il compilatore genera del "**codice dinamico rilocalizzabile**", che si basa su dei cosiddetti "**indirizzi virtuali**"; l'OS andrà poi ad associare volta per volta gli indirizzi virtuali a quelli fisici sfruttando una **Memory Management Unit**, o **MMU** in breve. Dunque, con questo approccio, **gli indirizzi logici** (o meglio, quelli virtuali) **non coincideranno con quelli fisici**. Quest'ultima soluzione è in realtà quella più flessibile e più frequentemente utilizzata nella maggior parte dei sistemi moderni.

Essendo gli indirizzi virtuali uno strumento così importante, è essenziale introdurre anche il concetto di **spazio di indirizzamento virtuale**, o **VAS** in breve, **di un processo**. Si assume, in generale, che il VAS di ogni processo abbia la medesima dimensione massima, che esso debba essere situato contiguamente nella memoria principale, e che la memoria principale debba essere molto più ampia della dimensione di un VAS.
___
##### Rilocazione di un processo

Quando si avvia l'esecuzione di un programma, sarà necessario **allocare il VAS di un processo all'interno della memoria principale**. Vediamo come avviene questa procedura.

Innanzitutto, dobbiamo fare delle premesse:
- si suppone sempre che **la parte di memoria occupata dall'OS si trovi all'inizio o alla fine della memoria**, e dunque occupi i più bassi o i più alti indirizzi di memoria;
- di conseguenza, si assume che qualsiasi indirizzo logico generato da un processo utente sia incluso nel range $[0,\,\text{memory\_size}-\text{os\_size}-1]$.

Tendenzialmente, quando un processo viene caricato nella memoria principale **il suo spazio di indirizzamento viene caricato in un segmento contiguo di memoria**. L'allocazione di uno spazio di memoria del genere a un processo, dunque sostanzialmente la traduzione degli indirizzi di memoria logici del programma in indirizzi fisici nella RAM, viene detta "**rilocazione**", e tale rilocazione può avvenire principalmente in due modi:
- **rilocazione statica**;
- **rilocazione dinamica**.

La **rilocazione statica** avviene al **caricamento del programma nella RAM**, in modo da poter essere eseguito. In parole povere, si ha un procedimento analogo all'[[SO1_07 - Gestione della memoria#Address binding|address binding]] in fase di caricamento che abbiamo visto nel paragrafo precedente: il loader "riscriverà" gli indirizzi logici del processo convertendoli in indirizzi fisici validi all'interno della RAM. Questo approccio presenta come **pregio** principale il **non avere bisogno di HW supplementare**, ma allo stesso tempo ha vari **difetti**: **non assicura una protezione dell'OS o di altri processi**; una volta caricato nella RAM, **il processo non potrà essere spostato nuovamente** dall'OS senza problemi; **non si assicura che lo spazio di indirizzamento del processo sia contiguo**.

Al contrario, la **rilocazione dinamica** è molto più all'avanguardia, seppur anche più complessa. Essa assicura la protezione degli spazi di memoria dedicati all'OS e ad altri processi, ma per essere implementata necessita di una componente di HW particolare, a cui abbiamo già accennato: la **Memory Management Unit**, o **MMU**. In questo caso, l'address binding effettivo avviene durante l'esecuzione del programma, con l'MMU che traduce dinamicamente i vari indirizzi logici (virtuali) in indirizzi fisici della RAM. Per fare ciò, l'MMU dispone di **almeno $2$ registri**:
- un registro **base**, contenente l'indirizzo fisico iniziale dello spazio di indirizzamento di un determinato processo;
- un registro **limite**, contenente la massima dimensione dello spazio di indirizzamento.

Questi registri vengono sfruttati nel modo seguente: quando un qualsiasi processo effettua una richiesta a un certo indirizzo del suo blocco di memoria, la MMU, sfruttando il suo registro limite, verificherà che tale indirizzo sia effettivamente contenuto nello spazio di indirizzamento del processo: se ciò si verifica, dunque se l'indirizzo richiesto è inferiore della dimensione massima dello spazio di indirizzamento, allora sfruttando il registro base la MMU sommerà l'indirizzo relativo richiesto a quello fisico contenuto in tale registro, ottenendo così l'indirizzo fisico effettivo del blocco di memoria richiesto dal processo; altrimenti, dunque se l'indirizzo richiesto eccede lo spazio di indirizzamento del processo, la MMU restituisce un errore.

I **pregi** della rilocazione dinamica sono principalmente la **protezione tra i vari spazi di indirizzamento**, il fatto che **l'OS potrà spostare i processi durante l'esecuzione più facilmente**, ma anche l'**implementazione facile ed efficiente a livello di HW**, tramite l'utilizzo della MMU che necessita pochissimi dati ed istruzioni per fornire il risultato desiderato. Allo stesso tempo, però, troviamo alcuni **limiti**: seppur semplice, **la presenza dell'MMU rallenta comunque ogni accesso alla memoria**; nonostante la possibilità dell'OS di spostare i processi, **si dovrà comunque cercare di allocare ogni VAS in blocchi di memoria contigui**; la dimensione dei processi e il numero degli stessi sono ancora limitati dalla dimensione della memoria fisica.  
___
##### Politiche di allocazione della memoria

Fino ad adesso, abbiamo assunto senza rifletterci troppo che **ogni processo viene allocato in uno spazio contiguo della memoria fisica**. Ma come possiamo assicurarci che ciò avvenga? Per garantire questa caratteristica, in base al sistema si possono scegliere diverse **politiche di allocazione della memoria**, dunque diversi modi del scegliere questi blocchi contigui di memoria.

In sistemi più semplici, ma anche abbastanza obsoleti, **la memoria principale disponibile per i processi utente viene divisa a priori in partizioni di dimensioni uguali**: dividendo la memoria principale in queste partizioni, ciascun processo potrà poi essere assegnato a una partizione. Si tratta però di un approccio abbastanza naif e anche un po' limitante, dato che mantenere questa divisione rigida della memoria restringe il numero di processi che si possono avere in esecuzione simultaneamente.

Un approccio alternativo, più dinamico e flessibile, consiste invece nel **far tenere traccia all'OS di eventuali segmenti liberi di memoria** ogni volta che dei processi entrano in esecuzione, la terminano, o semplicemente crescono nelle loro dimensioni. Vediamo un esempio di cosa si intende:

![[allocazione_memoria_esempio.png]]

Nella sequenza appena mostrata, vediamo che non appena il processo $B$ termina la sua esecuzione, e dunque libera un blocco di memoria principale, l'OS tiene traccia del "**buco**", ossia del blocco di memoria principale inutilizzato, che si è appena creato, e quando dovrà allocare della memoria per il processo $D$ saprà di poter sfruttare proprio tale buco, dunque inserirà lo spazio di indirizzamento di $D$ all'interno di tale blocco di memoria. Per poter fare ciò, l'OS conserva e aggiorna dinamicamente una lista di tutti i buchi presenti, e ogni volta che un processo deve essere caricato nella memoria principale, esso dovrà assegnargli un buco di dimensioni appropriate. È proprio nel gestire quest'ultima operazione che entrano in gioco le diverse **politiche di allocazione della memoria**.

La prima politica di allocazione della memoria che andremo a vedere è quella "**first-fit**". Seguendo questa politica, quello che viene fatto dall'OS è **scansionare linearmente la lista dei buchi finché non si trova un buco di dimensione sufficiente per ospitare il processo**; invece, eventuali ricerche successive potrebbero ripartire dall'inizio della lista oppure da dove è terminata la scorsa ricerca, in base all'implementazione particolare della politica. La **complessità** di questa ricerca è $O(n)$, dove $n$ è il numero di buchi. Volendo vedere un esempio concreto, ipotizziamo di avere la seguente lista di buchi:
- buco di $20$ byte
- buco di $400$ byte
- buco di $120$ byte

e supponiamo di avere un processo $X$ che ha bisogno di $100$ byte per essere caricato; l'OS, rispettando la politica first-fit, caricherà $X$ nei primi $100$ byte del buco di $400$ byte, dato che è il primo buco di dimensione sufficiente che viene incontrato nella lista. Ma cosa succederebbe se, dopo $X$, arrivasse un processo $Y$ che richiede $350$ byte di memoria? Seppur nel buco considerato in precedenza siano rimasti $300$ byte, essi non sono sufficienti per ospitare $Y$, dunque ora come ora non potremmo allocare uno spazio al processo $Y$. 

Un'altra alternativa, che potrebbe aiutarci in casi del genere, è la cosiddetta politica "**best-fit**". Seguendo questa politica, **l'OS allocherà al processo il buco più piccolo che è grande abbastanza per ospitare tale processo**; questo permetterà di preservare buchi di dimensioni ingenti per altri processi che potrebbero averne bisogno in seguito (come il processo $Y$ nell'esempio precedente), ma al tempo stesso porterà spesso allo spreco di porzioni piccole di memoria. La **complessità** di questa ricerca è sempre $O(n)$ normalmente, ma se la lista di buchi viene mantenuta ordinata dall'OS essa può diventare $O(\log n)$: questa complessità può essere raggiunta attraverso una **ricerca binaria su un albero di ricerca binario**.

Ritornando all'esempio precedente, stavolta il processo $X$ verrebbe assegnato al buco di $120$ byte, lasciando di conseguenza il buco da $400$ byte libero per l'eventualità di un arrivo successivo del processo $Y$.

C'è ancora un'altra alternativa, che può sembrare contro-intuitiva ma ha in realtà i suoi vantaggi: la politica "**worst-fit**". Seguendo questa politica, **l'OS allocherà al processo il buco di dimensione maggiore disponibile**; seppur può sembrare che ciò porti a problematiche simili a quelle viste nella prima iterazione dell'esempio, in realtà tendenzialmente la politica worst-fit aumenta la probabilità che le porzioni rimaste libere dei buchi, dopo l'allocazione di un processo, siano abbastanza grandi da poter essere utilizzate in seguito da altri processi. Ciononostante, varie simulazioni mostrano che best-fit e first-fit siano generalmente le opzioni migliori, e in particolare che la first-fit sia generalmente più veloce della best-fit.

Ma **cosa succede se non si trovano spazi contigui di memoria sufficientemente grandi per ospitare un processo?** Si verifica quella che viene definita "**frammentazione**", ossia la presenza di buchi di memoria troppo piccoli per ospitare singolarmente un processo, ma magari sufficienti se fossero combinati in un unico spazio di memoria. La frammentazione può presentarsi in due forme diverse:
- **frammentazione esterna**;
- **frammentazione interna**.

La **frammentazione esterna** si verifica in seguito a frequenti caricamenti e scaricamenti di processi, che portano alla creazione di molti buchi sparsi e di piccole dimensioni, e di conseguenza inutilizzabili singolarmente; in questo caso, in totale c'è abbastanza memoria libera per ospitare il processo, tuttavia tale memoria non è contigua ma divisa tra più buchi distinti. La **frammentazione interna**, invece, si verifica quando ad essere sprecata è della memoria interna a un singolo segmento allocato a un processo; ad esempio, può capitare che un processo occupi $8846$ byte e che ci sia un buco di $8848$ byte, di conseguenza sarò più conveniente allocare direttamente tutto il buco al processo piuttosto che tenere traccia di un buco di $2$ byte, che sicuramente non sarà utilizzabile; un altra situazione in cui avviene una frammentazione interna è l'allocazione di memoria attraverso partizioni.

Il problema della frammentazione esterna, in particolare, può essere risolto principalmente in due modi: la **compattazione totale** e la **compattazione parziale**. La prima consiste nel **rilocalizzare tutti i processi nella memoria principale in modo contiguo**, unendo così tutti i buchi di memoria presenti in precedenza in un unico buco di dimensioni maggiori. Un esempio di compattazione totale può essere il seguente, dove i processi $C$ e $D$ vengono compattati per lasciare spazio al processo $E$:

![[allocazione_memoria_esempio1.png]]

La seconda, invece, consiste nel **rilocalizzare solo i processi necessari affinché si crei un buco abbastanza grande da ospitare il processo considerato**. Un esempio di compattazione parziale può essere il seguente, dove solo il processo $D$ viene spostato per lasciare spazio al processo $E$:

![[allocazione_memoria_esempio2.png]]

Mentre **la compattazione totale elimina un numero maggiore di buchi,** e dunque lascia la memoria effettiva in una situazione più vantaggiosa, **la compattazione parziale risulta meno complessa e pesante a livello di lavoro da svolgere**, dato che tende a spostare meno processi della compattazione totale per ottenere lo scopo desiderato.
___
##### Swapping

Finora, abbiamo sempre dato per scontato che tutti i processi siano interamente caricati in memoria durante tutta la loro esecuzione. C'è da dire, però, che un processo deve necessariamente trovarsi nella memoria principale solo quando la CPU sta attivamente eseguendo sue istruzioni e accedendo a suoi dati; dunque, se un processo sospende la sua esecuzione per qualche motivo, esso non sarà obbligato a trovarsi nella memoria principale finché non tornerà ad essere eseguito. Per questo motivo, spesso avviene uno "**swapping**", con cui **il processo in questione viene spostato dalla memoria principale alla memoria a disco**, in modo da lasciare spazio ad altri processi che devono essere eseguiti.

Naturalmente, una volta che il processo torna ad essere disponibile per essere eseguito, l'OS dovrà procedere a **ricaricarlo nella memoria principale**: in base al tipo di [[SO1_07 - Gestione della memoria#Address binding|address binding]] utilizzato dal programma considerato, la modalità con cui avviene questo ricaricamento subisce una variazione:
- se l'address binding avviene **durante la compilazione** oppure **durante il caricamento**, allora per evitare problemi **il processo dovrebbe essere caricato nella stessa posizione in memoria assunta da esso prima dello swapping**;
- se l'address binding avviene **durante l'esecuzione**, allora **il processo può sostanzialmente essere caricato ovunque**, ed eventuali aggiustamenti saranno poi fatti dalla [[SO1_07 - Gestione della memoria#Address binding|MMU]].

Con lo swapping, la [[SO1_07 - Gestione della memoria#Politiche di allocazione della memoria|frammentazione]] può essere affrontata facilmente: basterebbe, infatti, **compattare** (totalmente o parzialmente) **prima dell'entrata via swapping di un processo nella memoria principale**. È anche vero, però, che lo swapping è un'**operazione molto lenta**, soprattutto a causa dell'interazione con la memoria a disco.
___
## Paging

Finora, abbiamo osservato alcuni **problemi ricorrenti nell'[[SO1_07 - Gestione della memoria#Allocare memoria a processi e thread|allocazione della memoria]]**:
- il dover allocare **spazi contigui di memoria** per i vari processi;
- l'evenienza della **[[SO1_07 - Gestione della memoria#Politiche di allocazione della memoria|frammentazione]]** quando ciò non è possibile;
- la **lentezza dello [[SO1_07 - Gestione della memoria#Swapping|swapping]]**.

Tutti questi problemi, e in particolare l'ultimo (lo swapping è una tecnica relativamente obsoleta, che ormai non viene quasi più utilizzata nei sistemi moderni), vengono risolti utilizzando il "**paging**".

Concretamente, il paging è una tecnica di gestione della memoria che prevede che **lo spazio di indirizzamento logico di un processo sia contiguo, ma che concretamente venga suddiviso in blocchi di memoria di dimensione fissa**, detti "**pagine**" e dando il nome alla tecnica. In questo modo, si risolve innanzitutto il problema dell'**allocazione di memoria contigua**, dato che non sarà più necessario allocare spazi contigui di memoria, dato che **le pagine possono essere mappate a "frame" fisici non contigui**; al tempo stesso, **avendo tutte le pagine una dimensione costante**, viene risolto anche il problema della **frammentazione esterna**, anche se quella interna potrebbe ancora accadere.

##### Da indirizzi virtuali a indirizzi fisici

Per poter utilizzare questa tecnica, l'OS dovrà occuparsi in modo efficiente della mappatura tra pagine logiche e frame di memoria fisici, e della traduzione in base ad essa degli indirizzi logici in indirizzi fisici: per fare ciò, si avrà bisogno di una "**page table**". Tramite questa page table, l'OS saprà dire con facilità in quale frame di memoria è conservata una determinata pagina, come nel seguente esempio:

![[paging_esempio.png]]

Gli **indirizzi virtuali**, in questo contesto, consistono concretamente di **due parti**:
- **`p`**, ossia il **numero della pagina** dove risiede tale indirizzo;
- **`offset`**, ossia l'**offset in byte** dell'indirizzo **rispetto all'inizio della pagina**.

Per **convertire un indirizzo virtuale in indirizzo fisico**, il valore `p` viene fatto corrispondere a un valore **`f`**, ossia al **numero di un frame fisico** di memoria, attraverso la page table, mentre il valore `offset` viene utilizzato così com'è, senza variazioni. Dunque, `f` e `offset` vanno a formare l'indirizzo fisico corrispondente all'indirizzo virtuale, seguendo il seguente flusso:

![[paging_davirtualeafisico.png]]

In realtà, il paging non è altro che una **forma avanzata di [[SO1_07 - Gestione della memoria#Rilocazione di un processo|rilocazione dinamica]]**: ogni indirizzo virtuale è vincolato, dalla page table, a un indirizzo fisico, e in questo contesto **la page table può essere vista come un insieme di registri base**, uno per ogni frame di memoria. Inoltre, **la traduzione degli indirizzi avviene concretamente nell'MMU**, e quindi si assicura la **protezione dei vari spazi di indirizzamento** in modo simile a come si faceva per la rilocazione dinamica con i registri limite.

Le **operazioni matematiche per tradurre un indirizzo virtuale in uno fisico** sono in realtà abbastanza semplici: per capirle al meglio, vediamole con un esempio. Supponiamo di avere $50$ byte di memoria fisica disponibili per i processi utente (sapendo ciò, sappiamo che un processo potrà generare solo indirizzi virtuali compresi nell'intervallo $[0,\,49]$), e di star utilizzando un sistema di paging in cui la dimensione di una page (e, dunque, anche di un frame fisico di memoria) è $S=10$ byte. Supponiamo, a questo punto, che un processo generi l'indirizzo virtuale $x=27$: otteniamo innanzitutto il numero di pagina `p`, e per fare ciò andremo a dividere l'indirizzo virtuale per la dimensione di una pagina, ossia
$$p=\frac{x}{s}=\frac{27}{10}=2$$
Ora, per ottenere l'`offset` basterà effettuare un'operazione di modulo (il resto di una divisione) tra gli stessi operandi:
$$\text{offset}=x \text{ mod }S=27\text{ mod }10 = 7$$
Così facendo, si è ottenuta una forma dell'indirizzo virtuale che sarà facilmente convertibile in indirizzo fisico sfruttando la page table.

**Il numero e la dimensione delle page e dei frame dipendono dall'architettura** del sistema su cui si sta lavorando, ma **tipicamente la dimensione di una page è una potenza di $2$**, spesso compresa tra $512$ byte (o $0.5\text{ KiB}$) e $8192$ byte (o $8\text{ KiB}$): ciò avviene perché l'utilizzo di potenze di $2$ rende la traduzione da indirizzo virtuale a fisico ancora più immediata, in modo che non necessiti neanche di eseguire le operazioni di divisione e modulo che abbiamo appena visto. Infatti, supponendo che l'indirizzo virtuale sia composto da $m$ bit, sappiamo che lo spazio di indirizzamento virtuale ha dimensione $2^{m}$, e dunque che gli indirizzi virtuali che il processo può generare si troveranno nell'intervallo $[0,\,2^{m}-1]$; allo stesso tempo, se assumiamo che la dimensione di una singola page sia pari a $2^{n}$ byte, con $n<m$, per ottenere **il numero di pagina** basterebbe estrarre **i primi $m-n$ bit dell'indirizzo virtuale** (si intende, i bit più a sinistra); di conseguenza **gli ultimi $n$ bit dell'indirizzo virtuale** (si intende, i bit più a destra), rappresenteranno l'**offset**.

Tendenzialmente, gli indirizzi virtuali sono composti **da $32$ o da $64$ bit**, portando lo spazio di indirizzamento virtuale ad avere dimensioni comprese tra $2^{32}$ (o $4\text{ GiB}$) e $2^{64}$ byte (o $16\text{ EiB}$).

##### Esempio n°1

Supponiamo di avere una memoria virtuale e una memoria fisica entrambe di dimensione $M=1024\text{ byte}$ (o $1\text{ KiB}$). Essendo $1024=2^{10}$, sappiamo che se consideriamo un indirizzamento al byte ci serviranno indirizzi da $10$ bit per poter coprire tutta la memoria. Ora, assumendo si utilizzare un sistema di paging con la dimensione di una page pari a $S=16\text{ byte}$, per sapere quante entry avrà la page table (dunque, quante page si avranno in totale), basterà dividere la dimensione della memoria per la dimensione di una page, ottenendo $T=\frac{M}{S}=\frac{1024}{16}=64$ pages. Poi, vogliamo sapere quali bit dell'indirizzo virtuale corrispondono a `p` e quali a `offset`: sappiamo che un indirizzo virtuale è lungo $10$ bit, e al tempo stesso che una page ha dimensione $S=16=2^{4}$, di conseguenza si utilizzeranno i $4$ bit più a destra per l'`offset` e i $10-4=6$ bit più a sinistra per `p`. Avendo queste informazioni, e assumendo di disporre della seguente page table:

| Page | Frame |
| ---- | ----- |
| 0    | 12    |
| 1    | 5     |
| 2    | 37    |
| 3    | 0     |
| ...  | ...   |
| 63   | 29    |

vogliamo tradurre l'indirizzo virtuale $x=42$ in un indirizzo fisico. Per fare ciò, non avendo a portata di mano la rappresentazione binaria dell'indirizzo, possiamo sfruttare le operazioni di divisione e modulo: `p` sarà dato dalla divisione $\frac{x}{S}=\frac{42}{16}=2$, mentre `offset` è pari a $x\text{ mod }S=42\text{ mod }16=10$; sfruttando la page table, otteniamo che l'indirizzo virtuale $42$ è mappato al $10°$ byte del $37$-esimo frame.
___
##### Esempio n°2

Supponiamo di avere una memoria virtuale e una memoria fisica entrambe di dimensione $M=1024\text{ byte}$ (o $1\text{ KiB}$). Stavolta, però, vogliamo considerare un indirizzamento a word, invece che a byte, assumendo che nella nostra architettura una word sia composta da $32$ bit, o $4$ byte: di conseguenza, prima di valutare il numero di bit necessari per un indirizzo virtuale, dobbiamo prima trovare il numero di word incluse nella memoria che stiamo considerando, ossia $\frac{1024}{4}=256$ words. Ora, sapendo che $256=2^{8}$, troviamo che ci serviranno indirizzi da $8$ bit per poter coprire tutta la memoria. Ora, assumendo si utilizzare un sistema di paging con la dimensione di una page pari a $S=16\text{ byte}$, per sapere quante entry avrà la page table (dunque, quante page si avranno in totale), basterà dividere la dimensione della memoria per la dimensione di una page, ottenendo $T=\frac{M}{S}=\frac{1024}{16}=64$ pages. Poi, vogliamo sapere quali bit dell'indirizzo virtuale corrispondono a `p` e quali a `offset`: sappiamo che un indirizzo virtuale è lungo $8$ bit, e al tempo stesso che una page può contenere $\frac{16}{4}=4$ words, di conseguenza si utilizzeranno i $2$ bit più a destra per l'`offset` e gli $8-2=6$ bit più a sinistra per `p`. Avendo queste informazioni, e assumendo di disporre della seguente page table:

| Page | Frame |
| ---- | ----- |
| 0    | 12    |
| 1    | 5     |
| 2    | 37    |
| 3    | 0     |
| ...  | ...   |
| 63   | 29    |

vogliamo tradurre l'indirizzo virtuale $x=7$ in un indirizzo fisico. Per fare ciò, non avendo a portata di mano la rappresentazione binaria dell'indirizzo, possiamo sfruttare le operazioni di divisione e modulo, facendo stavolta attenzione ad esprimere $S$ in termini di words e non di byte, dato che l'indirizzamento avviene in base alle prime: `p` sarà dato dalla divisione $\frac{x}{S}=\frac{7}{4}=1$, mentre `offset` è pari a $x\text{ mod }S=7\text{ mod }4=3$; sfruttando la page table, otteniamo che l'indirizzo virtuale $7$ è mappato alla $3°$ word del $5°$ frame.
___
##### Il Translation Look-aside Buffer (TLB)

Un processo utente, mentre si trova in esecuzione nella CPU, genera indirizzi virtuali di memoria quasi costantemente, e ogni volta che si fa riferimento a un qualsiasi indirizzo virtuale esso va tradotto in un indirizzo fisico, operazione per cui la MMU deve necessariamente accedere alla page table. Si può intuire che, tutto sommato, si tratta di una serie di operazioni abbastanza dispendiosa e inefficiente.

Un punto importante che potrebbe migliorare l'efficienza di queste operazioni è il **dove conservare la page table**. Le opzioni principali sono due, ossia:
- dei **registri**, che consentirebbero una grande rapidità di accesso ma, al tempo stesso, sono molto costosi e hanno una capienza limitatissima;
- la **memoria principale**, che dispone di una maggiore capienza ma, in compenso, non permette accessi particolarmente rapidi.

Avendo entrambe le opzioni dei pregi e dei difetti, un'opzione relativamente ottimale è rappresentata da una sorta di **combinazione delle due**: è possibile **conservare la page table effettiva in memoria principale**, e **memorizzare in una cache un sottoinsieme della stessa** in quello che viene chiamato "**Translation Look-aside Buffer**", o **TLB** in breve. La cache, infatti, rappresenta un ottimo compromesso tra registri e memoria principale, essendo una memoria accessibile direttamente dalla CPU, e dunque particolarmente veloce, ma al tempo stesso di dimensione più ingente rispetto ai registri.

Sostanzialmente, il TLB consiste in una **memoria cache di tipo L1 particolarmente veloce**, destinata a conservare coppie chiave-valore dove la chiave è un **numero di page**, mentre il valore è il **corrispondente numero di frame** dove la page è fisicamente memorizzata (tipicamente, la dimensione di un TLB si aggira tra le $8$ e le $2048$ coppie del genere). Dunque, il TLB viene utilizzato per conservare a tutti gli effetti una parte della page table, e ciò è utile perché gli accessi alla memoria seguono il **principio di località**: tendenzialmente, se si fa un accesso a una zona di memoria, è probabile che i prossimi accessi avvengano approssimativamente nella stessa zona.

[funzionamento del TLB: 14, slide 26 - 28/30]

[costo di un accesso in memoria con o senza TLB: 14, slide 42]

Il TLB è un componente che è **condiviso tra tutti i processi**: ciò vuol dire che, **in base al processo in esecuzione, uno stesso numero di page può essere mappato a diversi numeri di frame**. Per gestire questa eventualità, dobbiamo assicurarci che il contenuto del TLB sia aggiornato ed effettivamente corretto per il processo attualmente in esecuzione. Possiamo fare ciò in due modi ben diversi:
- con un approccio **più semplice ma meno efficiente**, potremmo eliminare l'intero contenuto del TLB ad ogni context switch, in modo da non avere alcun dato precedente e dunque prevenire qualsiasi possibilità di accessi non accurati (naturalmente, con questo approccio, tutti i primi accessi effettuati dal processo risulteranno in miss nel TLB);
- con un approccio **più complesso ma anche più efficiente**, potremmo conservare determinate coppie del TLB nel [[SO1_03 - Processi#Il PCB|PCB]] del rispettivo processo, o in alternativa aggiungere un "process context ID", o PCID in breve, a ogni coppia del TLB in modo da utilizzare una certa coppia solo se il PCID corrisponde con l'ID del processo attualmente in esecuzione.

Per comprendere più nel dettaglio come gestire il TLB in base a tali approcci, può essere utile approfondire la **struttura di una entry della page table**, o **PTE**. Oltre ai numeri di page (detti anche **VPN**) e ai numeri di frame (detti anche **PFN**), possiamo trovare dei **bit aggiuntivi**, che ci permettono di avere più informazioni relativamente alla entry considerata, tra cui:
- un **bit di validità**, che indica se la mappatura è accurata e utilizzabile o meno;
- dei **bit di protezione**, che specificano il livello di accesso al blocco di memoria indicato;
- un **bit di presenza**, che indica se la page è presente in RAM o se è stata "swappata" nella memoria a disco;
- un **bit di riferimento**, che indica se è stato effettuato un accesso alla page recentemente.

[14, slide 52 - 54 - 56 - 59 - 62 - 64/66]
___
##### Segmentazione e paging

[14, slide 71 - 72 - 76 - 78 - 80 - 84 - 88 - 93 - 97 - 101/105 - 108 - 111 - 113 - 114 - 119 - 122 - 125 - 130 - 132 - 137 - 139/147 - 149 - 152]
___