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

##### Alcuni concetti utili

Prima di addentrarci nell'analisi e nella progettazione del processore, ricordiamo alcuni **concetti fondamentali** per la comprensione di ciò che segue.

Le diverse componenti del processore, quelle che potremmo definire **[[La CPU#Unità funzionali|unità funzionali]]**, possono appartenere a due diverse classi di elementi logici: ci sono elementi che si limitano a operare su dei dati, ossia elementi di tipo **combinatorio**, ed elementi che contengono al loro interno uno stato, ossia elementi di tipo **sequenziale**. 

In un elemento di tipo combinatorio, in ogni istante i suoi output dipendono esclusivamente dai suoi input in tale istante (infatti, **un elemento combinatorio è privo di memoria**), di conseguenza dando gli stessi input a un elemento combinatorio si otterranno sempre gli stessi output. In un elemento di tipo sequenziale, invece, i suoi output dipendono sia dai suoi input sia dallo stato già memorizzato al suo interno (infatti, **un elemento sequenziale è dotato di memoria**); per questa caratteristica, gli elementi sequenziali vengono anche detti "**elementi di stato**". Un elemento di stato, generalmente, possiede sempre **almeno due input e un output**: i due input sono il dato da memorizzare e il **clock**, segnale che determina quando memorizzare il dato; l'output è invece il dato memorizzato al suo interno in un ciclo di clock passato.

Nel nostro processore, incontreremo esempi sia dell'una che dell'altra categoria (ad esempio, l'ALU è un componente combinatorio, mentre i registri o le memorie sono componenti di stato).

A questo punto, avendo stabilito con che tipo di componenti andremo a lavorare, è opportuno stabilire una **metodologia di temporizzazione**, scegliendo dunque quando i segnali potranno essere effettivamente scritti e letti. Ciò è importante per regolare il flusso delle informazioni, evitare sovrapposizioni o malfunzionamenti, e favorire una maggiore prevedibilità del circuito. Per semplicità, supporremo di utilizzare una metodologia di temporizzazione "**sensibile ai fronti**", o "**edge-triggered**", che garantisce dunque che gli elementi di stato possano essere aggiornati solamente in corrispondenza di un **fronte** del segnale di clock, ossia di una transizione tra livello alto e basso dello stesso; in particolare, verrà utilizzata una metodologia "**positive edge-triggered**", che dà dunque importanza solo ai fronti di transizione da segnale basso a segnale alto.
___
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

L'**ALU**, invece, avrà come input **due valori interi a 32 bit** e come output il **risultato dell'operazione** svolta su di essi, operazione scelta tramite i segnali **`OperazioneALU`** (è previsto anche un output **`Zero`**, un singolo bit abilitato solo se l'operazione svolta dall'ALU risulta in tale valore). Graficamente, possiamo schematizzare quest'unità in questo modo:

![[alu.png]]

Infine, la **memoria di dati** è un'unità di memoria che riceve in input un **indirizzo a 32 bit**, che indica quale parola di memoria va letta o scritta, un segnale **`MemRead`**, utilizzato per abilitare o meno la lettura della memoria a tale indirizzo, un **dato a 32 bit**, nel caso in cui si voglia scrivere in suddetto indirizzo di memoria, e un segnale **`MemWrite`**, utilizzato per abilitare o meno la scrittura della memoria a tale indirizzo; come output, invece, avrà il **dato a 32 bit** eventualmente letto dalla memoria. Graficamente, possiamo schematizzare quest'unità in questo modo:

![[memoria_dati.png]]

Un'altra componente che può tornare utile è l'**unità di estensione del segno**, che serve a **estendere un intero** espresso in [[Sistema binario#Numeri binari segnati segno/grandezza e complemento a due|complemento a 2]] **a 32 bit**, copiando il bit del segno nei bit più significativi della parola. Graficamente, possiamo schematizzare quest'unità in questo modo:

![[estensione_segno.png]]

Tutte queste unità funzionali saranno interconnesse da vari **nodi**, definendo il flusso delle informazioni nella CPU e andando a formare il **datapath**. Naturalmente, per evitare sovrapposizioni, se un'unità funzionale può ricevere dati da più sorgenti bisogna inserire un **[[Circuiti combinatori#Multiplexer|multiplexer]]** per selezionarne una alla volta. Le unità funzionali nel datapath, poi, saranno attivate e coordinate dai segnali prodotto dalla **control unit**.
___
##### Assemblare le unità funzionali

Cominciamo, a questo punto ad **assemblare le unità funzionali**, soffermandoci passo per passo sui passaggi di esecuzione di un'istruzione che abbiamo visto a inizio paragrafo. 

Il primissimo passaggio, universale per tutte le istruzioni, è il **fetch** della stessa: per effettuare il fetch di un'istruzione, sarà necessario naturalmente avere il **PC**, ossia l'indirizzo di quest'ultima, e di trasmetterlo come input alla **memoria di istruzioni** in modo da ottenere, come output da essa, l'istruzione da eseguire; al tempo stesso, il PC va anche passato all'**adder**, che a meno di salti procederà ad aumentarlo di 4, ottenendo così l'indirizzo dell'istruzione successiva e ritrasmettendolo al registro del PC. È possibile ottenere un funzionamento del genere collegando le unità funzionali appena nominate in questo **circuito**:

![[fetch.png]]

Si noti che **tutti i nodi del circuito** appena esposto, in realtà, **rappresentano dei bus da 32 bit**. A questo punto, abbiamo estratto con successo un'istruzione dalla memoria, sotto forma di una stringa di 32 bit; come ben sappiamo, però, non tutte le [[Le istruzioni#Come vengono rappresentate le istruzioni nel calcolatore?|istruzioni]] hanno lo stesso formato e non possono essere interpretate allo stesso modo.

Consideriamo, ad esempio, le istruzioni in formato di tipo R, come `add x1, x2, x3`, che legge il contenuto dei registri `x2` e `x3`, li somma e scrive il risultato nel registro `x1`. Naturalmente, il primo componente fondamentale per l'esecuzione di un'istruzione del genere è il **register file**, che ricevendo in input l'istruzione dovrà **decodificarla**, individuando i campi contenenti i registri operandi e il registro di scrittura del risultato, leggere i contenuti dei registri operandi e restituirli come output. A questo punto, per eseguire concretamente l'operazione dettata dall'istruzione in esecuzione, sarà necessaria un'**ALU**, che esegua tale operazione sui dati ricevuti dal register file e ne fornisca il risultato in output. Quest'ultimo, come vedremo tra poco, potrà poi essere restituito come input al register file, in modo da venire memorizzato nel registro di scrittura.

Vediamo, ora cosa succederebbe con istruzioni come `lw x1, offset(x2)` (di tipo I) o `sw x1, offset(x2)` (di tipo S), utilizzate rispettivamente per caricare un dato dalla memoria a un registro e per trasferire un dato da un registro alla memoria. In entrambi i casi, per l'esecuzione dell'istruzione è necessario calcolare un indirizzo di memoria mediante l'ALU, sommando il contenuto del registro `x2` con l'`offset`, un intero segnato di 12 bit (nel formato di tipo I è interamente memorizzato in un unico campo `imm[11:0]`, mentre nel formato di tipo S è diviso nei suoi 7 bit più significativi, scritti in `imm[11:5]`, e nei suoi 5 bit meno significativi, scritti in `imm[4:0]`). Riguardo, invece, al registro `x1`, nel caso dell'istruzione `lw` esso diventa un registro di scrittura per il dato letto dalla memoria, mentre nel caso dell'istruzione `sw` esso è un registro di lettura che fornisce il dato da scrivere in memoria. Come abbiamo detto parlando dell'[[La CPU#Unità funzionali|ALU]], però, essa riceve come input due stringhe di 32 bit, lunghezza diversa dai 12 bit che abbiamo per la costante dell'istruzione: diventa, dunque, necessaria l'**unità di estensione del segno**, che andrà a estendere la costante fornita dall'istruzione in un valore a 32 bit. Infine, dato che si sta lavorando con la memoria (scrivendo e leggendo dati), risulta ovviamente necessario l'utilizzo di una **memoria di dati**, che in caso di lettura riceva in input l'indirizzo del dato desiderato e restituisca quest'ultimo in output, e in caso di scrittura riceva invece in input il dato da scrivere e l'indirizzo di memoria dove farlo.

Graficamente, possiamo schematizzare il blocco di unità funzionali responsabile dell'esecuzione delle istruzioni trattate finora nel modo seguente:

![[blocco_cpu_istruzioni_alu&memoria.png]]

Dallo schema, capiamo in maniera più immediata il flusso di informazioni tra le varie unità funzionali. **L'istruzione viene trasmessa al blocco di registri**, con l'eventuale **costante** contenuta in essa (se l'istruzione è di tipo I o S) che viene estesa a 32 bit tramite l'**unità di estensione del segno**. Il blocco di registri procede alla **lettura dei registri** indicati, e trasmette il loro contenuto in output: se si tratta di un'istruzione di tipo **R**, all'ALU verranno trasmessi i contenuti dei **due registri di lettura**; se, invece, si ha un'istruzione di tipo **I** o **S**, l'ALU riceverà il contenuto di **un registro** e il valore di **una costante a 32 bit** (questa scelta viene effettuata tramite un **[[Circuiti combinatori#Multiplexer|multiplexer]]**, che sceglie cosa trasmettere in base al segnale **`ALUSrc`**). A questo punto, il segnale **`OperazioneALU`** stabilisce quale debba essere l'operazione svolta dall'ALU, e il risultato può essere o un **indirizzo di memoria** (`lw`, `sw`) o un **dato da scrivere in un registro di scrittura** (`add`, `sub`, `and`, `or`): nel primo caso, esso viene trasmesso alla **memoria di dati**; nel secondo caso, esso dovrà essere ritrasmesso al blocco di registri. Arriviamo dunque alla memoria di dati, che riceve un **indirizzo di memoria** ed, eventualmente, un **dato da scrivere** in memoria proveniente da un registro di lettura, e che sa quale azione eseguire in base ai due segnali di controllo **`MemWrite`** e **`MemRead`**. Se si vorrà scrivere un dato in memoria, allora non sono previsti output rilevanti, mentre se si vorrà leggere un dato dalla memoria, esso verrà restituito in output. Infine, troviamo **un altro multiplexer**, i cui input stavolta sono il **dato letto dalla memoria** e il **risultato dell'operazione dell'ALU**; infatti, se si sta eseguendo un'istruzione come `lw`, si vorrà trasmettere al registro di scrittura il dato letto dalla memoria, mentre se si sta eseguendo un'istruzione come `add` o `or`, si vorrà trasmettere al registro di scrittura il risultato di tale operazione effettuata dall'ALU. Il segnale di controllo **`MemtoReg`** è responsabile proprio di scegliere quale di questi due dati verrà trasmesso al registro di scrittura.

A questo punto, l'unica istruzione che rimane da progettare è quella di salto condizionato, ossia `beq x1, x2, offset`. Come possiamo subito notare, essa dispone di tre operandi: i due registri `x1` e `x2`, il cui contenuto verrà confrontato, e la costante `offset`, una stringa di 16 bit utilizzata per calcolare l'indirizzo di destinazione del salto a partire dall'indirizzo dell'istruzione in esecuzione (dunque, il PC). L'esecuzione di tale istruzione, dunque, necessita innanzitutto di effettuare questo calcolo tramite un **adder**, andando a sommare l'`offset` (dopo averlo esteso a 32 bit con un'unità di estensione del segno) con il PC; poi, in base al risultato del confronto dei due registri, confronto effettuato dall'ALU, il circuito dovrà decidere se effettuare il salto (rendendo il valore appena calcolato il nuovo PC, evento definito anche "**branch taken**") o se ignorarlo (calcolando il nuovo PC normalmente e ignorando l'operazione appena svolta, evento definito anche "**branch not taken**"). Nell'ALU, il confronto viene effettuato sottraendo i contenuti dei due registri, che saranno uguali se la loro differenza sarà pari a $0$, e dunque se la sottrazione abiliterà il segnale di output `Zero`.

Graficamente, possiamo integrare la logica necessaria per questa istruzione nello schema visto in precedenza nel modo seguente:

![[blocco_cpu_beq 1.png]]

Ora siamo pronti a collegare tutti i blocchi che abbiamo creato finora. Una possibile schematizzazione totale dell'implementazione progettata finora è la seguente:

![[blocco_cpu.png]]

L'ultimo accorgimento che è stato fatto, evidenziato in arancione, è l'inserimento della **control unit**, responsabile della lettura del `codop` dell'istruzione e, di conseguenza, dei vari segnali di controllo del circuito; in particolare, per alcune istruzioni esso lavorerà anche con i campi `funz3` e `funz7` mediante un **controllore ALU**, in modo da precisare al meglio a quest'ultima cosa fare.
___
##### Segnali di controllo

Di seguito, si inserisce anche una tabella riassuntiva del ruolo dei vari **segnali di controllo** (il segnale `PCSrc`, apparentemente non presente nello schema dell'implementazione, non è altro che l'output della porta AND che riceve in input i segnali `Branch` e `Zero`):

![[segnali_controllo_tabella.png]]

Per quanto riguarda il segnale **`ALUOp`**, esso rappresenta in realtà un segnale di 2 bit, **`ALUOp1`** e **`ALUOp2`**, e indica quale comportamento deve assumere l'ALU in base al `codop`. In particolare, gli scenari possibili sono i seguenti:
- se l'istruzione è di **tipo R**, va eseguita l'operazione indicata dal campo `funz3` dell'istruzione;
- se l'istruzione **accede alla memoria**, va svolta la somma necessaria a calcolare l'indirizzo di memoria desiderato;
- se l'istruzione è un **salto condizionato**, va svolta la differenza tra i due registri operandi.

È possibile inserire in una tabella i **valori che i segnali di controllo devono avere per eseguire una determinata istruzione**:

![[segnali_controllo_tabella1.png]]
___
##### Come viene controllata l'ALU?

Nell'implementazione progettata [[La CPU#Assemblare le unità funzionali|un paio di paragrafi fa]], in base all'istruzione in esecuzione l'ALU dovrà eseguire una delle seguenti **quattro operazioni**:
- **somma**;
- **sottrazione**;
- **AND**;
- **OR**.

Per le istruzioni `lw` e `sw`, essa dovrà eseguire una somma, in modo da calcolare un indirizzo di memoria; per le istruzioni di tipo R, l'operazione che dovrà eseguire verrà stabilita in base ai campi `funz7` (i 7 bit più significativi dell'istruzione) e `funz3` (i 3 bit compresi tra `rs1` e `rd`); per l'istruzione di salto condizionato, infine, essa dovrà eseguire una sottrazione tra i due registri operandi. Per sapere quale operazione svolgere, l'ALU riceve in input **4 bit di controllo**, e una determinata operazione è codificata da una certa combinazione di questi bit. In particolare:
- l'operazione di **somma** è codificata come **`0010`**;
- l'operazione di **sottrazione** è codificata come **`0110`**;
- l'operazione di **AND** è codificata come **`0000`**;
- l'operazione di **OR** è codificata come **`0001`**.

Questi 4 bit di controllo vengono generati tramite quello che nell'implementazione è stato chiamato "**controllore ALU**", che riceve in input non solo i campi `funz7` e `funz3`, ma anche il segnale a 2 bit **`ALUOp`**, fornito dalla control unit. Il segnale **`ALUOp`** indica al controllore ALU se l'operazione da svolgere è:
- una **somma per un'istruzione con accesso alla memoria** (**`00`**);
- una **sottrazione per un salto condizionato** (**`01`**);
- un'**istruzione di formato di tipo R**, da determinare insieme ai campi `funz7` e `funz3` (**`10`**).

È possibile schematizzare tutti questi fattori in una tabella, mediante la quale è possibile capire quale combinazione di dati comporta ciascuna istruzione:

![[controllo_alu_tabella.png]]
___
##### Tempi di esecuzione

[TODO]
[10 ultima slide]
___
## E se volessimo aggiungere altre istruzioni?

L'implementazione fornita nel [[La CPU#Un'implementazione di base di un processore RISC-V|capitolo precedente]] può essere tranquillamente ampliata, aggiungendo **altre istruzioni dell'[[L'architettura RISC-V#L'architettura RISC-V|architettura RISC-V]]**.

##### L'istruzione **`j`**

Proviamo, ad esempio, ad aggiungere l'istruzione **`j`**, un'istruzione di salto incondizionato. Per poter aggiungere tale istruzione, dovremmo seguire diversi passaggi:
- definire la **codifica dell'istruzione**, cioè sostanzialmente il suo **formato**;
- definire il suo **funzionamento**;
- individuare le **unità funzionali necessarie**, o se esse sono già presenti nell'implementazione precedente;
- individuare il **flusso di dati** necessario per il funzionamento dell'istruzione;
- individuare i **segnali di controllo** necessari a regolare le unità funzionali coinvolte nell'esecuzione dell'istruzione;
- calcolare il **tempo di esecuzione** dell'istruzione, e verificare che non vada a modificare il tempo totale per la massima efficienza.

Partiamo dal primo punto. Per **codificare l'istruzione**, possiamo utilizzare un formato che non è stato trattato finora, ossia il **formato di tipo UJ**, che consiste in una variazione del formato di tipo U:

![[formato_uj.png]]

Come si può notare, i campi presenti e la loro disposizione rimangono invariati, ma il campo `imm` subisce alcune variazioni nella disposizione dei suoi bit. Passiamo, ora, 
___

[pag. 24 - 34 "Prestazioni"]
[pag. 236...]
