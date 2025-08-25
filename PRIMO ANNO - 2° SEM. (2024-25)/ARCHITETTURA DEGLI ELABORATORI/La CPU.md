## Cos'è una CPU?

La **CPU** ("**Central Processing Unit**"), o **processore**, rappresenta forse la componente più importante e imprescindibile in un qualsiasi [[Il calcolatore|calcolatore]]. Si tratta della **parte attiva** del calcolatore, quella che esegue fedelmente le istruzioni di un programma, che è in grado di effettuare operazioni aritmetiche, effettuare controlli sui risultati di quest'ultime, inviare segnali per attivare dispositivi di I/O e molto altro.

Generalmente, una CPU è composta da **due componenti principali**:
- un'**unità di elaborazione dati**, detta anche "**datapath**";
- un'**unità di controllo**, detta anche "**control unit**".

Potremmo definire queste due componenti come rispettivamente il braccio e la mente del processore: infatti, se ad esempio la prima è destinata all'esecuzione concreta di operazioni aritmetiche, la seconda indica alla prima quali operazioni eseguire, a seconda di quanto dettato dalle istruzioni del programma in esecuzione; la control unit, inoltre, è anche responsabile della comunicazione con la memoria e con i dispositivi di I/O.
___
## Un'implementazione di base di un processore RISC-V

In generale, le **prestazioni di un calcolatore** sono principalmente influenzate da tre fattori chiave: il **numero di istruzioni** da eseguire, la **durata del ciclo di clock** e il **numero di cicli di clock per istruzione** (o **CPI**). Seppur il primo di questi fattori dipenda soprattutto dall'architettura e dall'[[Le istruzioni#Cos'è un'istruzione?|insieme di istruzioni]] utilizzato, gli altri due dipendono esclusivamente dalla **particolare implementazione della CPU** di tale calcolatore.

Per comprendere meglio come l'implementazione della CPU vada ad influenzarne le prestazioni, proviamo ad **esaminare un'implementazione basilare di una CPU nell'architettura RISC-V**. Il processore che andremo ad analizzare comprende solo un piccolo sottoinsieme delle effettive [[Le istruzioni#Le istruzioni dell'architettura RISC-V|istruzioni]] previste per tale architettura, ossia:
- alcune istruzioni di trasferimento dati (**`lw`** e **`sw`**);
- alcune istruzioni aritmetiche e logiche (**`add`**, **`sub`**, **`and`**, **`or`**);
- un'istruzione di salto condizionato (**`beq`**).

##### Come fa un'istruzione a essere eseguita?

La prima cosa da fare, nel contesto della progettazione di un qualsiasi processore, è **prevedere le azioni e i mezzi necessari per realizzare concretamente le istruzioni**. Molti componenti necessari per questa mansione sono gli stessi, indipendentemente dal tipo di istruzione, e la stessa cosa vale per i primi passaggi dell'esecuzione delle stesse. Infatti, per ogni istruzione dell'architettura RISC-V i primi due passi dell'esecuzione sono:
1. **inviare il contenuto del PC alla memoria** che contiene il programma, in modo da **prelevare l'istruzione desiderata dalla memoria** (questa operazione, per semplicità, viene anche definita come "**fetch**" dell'istruzione);
2. **decodificare l'istruzione** in questione e, in base ai suoi campi, **leggere il contenuto dei registri desiderati**.

In seguito a questi due passaggi, in base al tipo di istruzione le azioni richieste per completare l'**esecuzione** variano leggermente, pur rimanendo a grandi linee molto simili. Ad esempio, **tutte le istruzioni dell'architettura RISC-V**, eccetto per i [[Le istruzioni#Istruzioni di salto incondizionato|salti incondizionati]], **utilizzano in qualche modo l'ALU** (unità logico-aritmetica) **dopo la lettura dei registri**: le istruzioni che accedono alla memoria la usano per calcolare l'indirizzo del dato desiderato; le istruzioni aritmetiche e logiche, naturalmente, la usano per eseguire operazioni; le istruzioni di salto condizionato la usano per effettuare i confronti su cui si basano.

Una volta terminato il lavoro con l'ALU, per completare l'esecuzione **diversi tipi di istruzioni faranno cose diverse**. Un'istruzione che accede alla memoria dovrà scriverci o leggerne dati, un'istruzione aritmetico-logica dovrà memorizzare il risultato della propria operazione nel registro di destinazione (operazione chiamata anche "write back"), un'istruzione di salto condizionato dovrà variare o meno l'indirizzo dell'istruzione successiva in base al risultato del confronto da essa eseguito.
___
##### Unità funzionali

Per poter progettare un processore in grado di fare tutto ciò, avremo bisogno di diverse **unità funzionali**, tra cui:
- il **PC**, ossia il registro contenente l'indirizzo in memoria dell'istruzione in esecuzione;
- una **memoria di istruzioni** da eseguire, dove possano essere conservate;
- un **adder**, utilizzato per calcolare volta per volta il nuovo PC (sia normalmente sia in caso di salti);
- un **blocco di [[Circuiti sequenziali#Registro|registri]]**, o "**register file**", necessari per contenere i parametri delle istruzioni;
- un'**ALU**, responsabile delle operazioni aritmetico-logiche, dei confronti e del calcolo degli indirizzi di memoria;
- una **memoria di dati**, da cui leggere (`lw`) e dove scrivere (`sw`) quest'ultimi.

Approfondiamo più nel dettaglio alcune delle unità funzionali appena esposte, per comprendere meglio come funzionano, a partire dalla **memoria di istruzioni**, che avrà come input un **indirizzo a 32 bit**, e come output l'**istruzione**, sempre di 32 bit, situata nell'indirizzo di memoria preso in input. Graficamente, possiamo schematizzare quest'unità in questo modo:

![[memoria_istruzioni.png]]

Per quanto riguarda l'**adder**, esso avrà invece come input **due valori interi a 32 bit**, e come output la loro **somma**. Graficamente, possiamo schematizzare quest'unità insieme al PC in questo modo:

![[pc_adder.png]]

Vediamo, ora, le caratteristiche del **blocco di registri**. Nell'architettura RISC-V, esso è composto da **32 registri di 32 bit** ciascuno, e presenta in input **3 porte a 5 bit** per indicare gli eventuali 2 registri da leggere e l'eventuale registro di scrittura, così come **3 porte dati a 32 bit**, di cui **una in input** per il valore eventualmente da memorizzare, e **due in output** per i valori eventualmente letti dai registri (inoltre, per regolare la scrittura nel registro di scrittura, si dovrà utilizzare un segnale **`RegWrite`**, che se abilitato consentirà la scrittura). Graficamente, possiamo schematizzare quest'unità in questo modo:

![[register_file.png]]

L'**ALU**, invece, avrà come input **due valori interi a 32 bit** e come output il **risultato dell'operazione** svolta su di essi, operazione scelta tramite i segnali **`OperazioneALU`** (è previsto anche un output **`Zero`**, un singolo bit settato a $0$ e abilitato solo se l'operazione svolta dall'ALU risulta in tale valore). Graficamente, possiamo schematizzare quest'unità in questo modo:

![[alu.png]]

Infine, la **memoria di dati** è un'unità di memoria che riceve in input un **indirizzo a 32 bit**, che indica quale parola di memoria va letta o scritta, un segnale **`MemRead`**, utilizzato per abilitare o meno la lettura della memoria a tale indirizzo, un **dato a 32 bit**, nel caso in cui si voglia scrivere in suddetto indirizzo di memoria, e un segnale **`MemWrite`**, utilizzato per abilitare o meno la scrittura della memoria a tale indirizzo; come output, invece, avrà il **dato a 32 bit** eventualmente letto dalla memoria. Graficamente, possiamo schematizzare quest'unità in questo modo:

![[memoria_dati.png]]

Un'altra componente che può tornare utile è l'**unità di estensione del segno**, che serve a **estendere un intero** espresso in [[Sistema binario#Numeri binari segnati segno/grandezza e complemento a due|complemento a 2]] **da 16 a 32 bit**, copiando il bit del segno nei 16 bit più significativi della parola. Graficamente, possiamo schematizzare quest'unità in questo modo:

![[estensione_segno.png]]

Tutte queste unità funzionali saranno interconnesse da vari **nodi**, definendo il flusso delle informazioni nella CPU e andando a formare il **datapath**. Naturalmente, per evitare sovrapposizioni, se un'unità funzionale può ricevere dati da più sorgenti bisogna inserire un **[[Circuiti combinatori#Multiplexer|multiplexer]]** per selezionarne una alla volta. Le unità funzionali nel datapath, poi, saranno attivate e coordinate dai segnali prodotto dalla **control unit**.
___
##### Assemblare le unità funzionali

Cominciamo, a questo punto ad **assemblare le unità funzionali**, soffermandoci passo per passo sui passaggi di esecuzione di un'istruzione che abbiamo visto a inizio paragrafo. 

Il primissimo passaggio, universale per tutte le istruzioni, è il **fetch** della stessa: per effettuare il fetch di un'istruzione, sarà necessario naturalmente avere il **PC**, ossia l'indirizzo di quest'ultima, e di trasmetterlo come input alla **memoria di istruzioni** in modo da ottenere, come output da essa, l'istruzione da eseguire; al tempo stesso, il PC va anche passato all'**adder**, che a meno di salti procederà ad aumentarlo di 4, ottenendo così l'indirizzo dell'istruzione successiva e ritrasmettendolo al registro del PC. È possibile ottenere un funzionamento del genere collegando le unità funzionali appena nominate in questo **circuito**:

![[fetch.png]]

Si noti che **tutti i nodi del circuito appena esposto rappresentano in realtà dei bus da 32 bit**. 
___

[pag. 24 - 34 "Prestazioni"]
[pag. 220... "Il processore"]
