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
## E se volessimo aggiungere altre istruzioni?

L'implementazione fornita nel [[La CPU#Un'implementazione di base di un processore RISC-V|capitolo precedente]] può essere tranquillamente ampliata, aggiungendo **altre istruzioni dell'[[L'architettura RISC-V#L'architettura RISC-V|architettura RISC-V]]**.

##### L'istruzione `j`

Proviamo, ad esempio, ad aggiungere l'istruzione **`j imm`** ("Jump"), un'istruzione di salto incondizionato. Per poter aggiungere tale istruzione, dovremmo seguire diversi passaggi:
- definire la **codifica dell'istruzione**, cioè sostanzialmente il suo **formato**;
- definire il suo **funzionamento**;
- individuare le **unità funzionali necessarie**, o se esse sono già presenti nell'implementazione precedente;
- individuare il **flusso di dati** necessario per il funzionamento dell'istruzione;
- individuare i **segnali di controllo** necessari a regolare le unità funzionali coinvolte nell'esecuzione dell'istruzione;
- calcolare il **tempo di esecuzione** dell'istruzione, e verificare che non vada a modificare il tempo totale per la massima efficienza.

Partiamo dal primo punto. Per **codificare l'istruzione**, possiamo utilizzare un formato che non è stato trattato finora, ossia il **formato di tipo UJ**, che consiste in una variazione del formato di tipo U:

![[formato_uj.png]]

Come si può notare, i campi presenti e la loro disposizione rimangono invariati, ma il campo `imm` subisce alcune variazioni nella disposizione dei suoi bit. Passiamo, ora, al suo **funzionamento**, in realtà abbastanza banale: all'esecuzione dell'istruzione `j`, **va sommato al PC una certa costante** fornita proprio dai 20 bit del campo `imm`. Per permettere questa funzionalità, quindi, avremo bisogno delle seguenti **unità funzionali**:
- il **PC**;
- un'**unità di estensione del segno**, che provvederà a riordinare i bit dell'immediato e a estenderli a 32 bit;
- un **adder**, per eseguire la somma tra PC e immediato;
- un **multiplexer**, o in alternativa una **porta logica**, per selezionare il nuovo PC.

Notiamo che abbiamo già a disposizione, nella nostra implementazione precedente, tutte queste unità funzionali, fatta eccezione per l'ulteriore multiplexer, che andrà aggiunto.

Andiamo ora, a definire il **flusso di dati** necessario per ottenere il funzionamento desiderato. La sequenza di azioni che andranno eseguite sarà: ottenere l'istruzione, estrapolandone l'immediato; riordinare i bit di quest'ultimo; sommarlo con il PC; trasmetterlo al multiplexer e, in seguito, al PC. Per quanto riguarda i **segnali di controllo**, basterà aggiungere un segnale **`Jal`** abilitato nel contesto dell'esecuzione di quest'istruzione, e assicurarsi che i già presenti `MemWrite` e `RegWrite` non siano abilitati, in modo da evitare modifiche indesiderate nella memoria e nei registri.

[tempi di esecuzione: 11, slide 12]

Andando ad ampliare l'implementazione precedente, otteniamo la seguente schematizzazione:

![[blocco_cpu_con_j.png]]

L'hardware aggiunto è costituito esclusivamente dal **segnale di controllo `Jal`** e dalla **porta OR** che riceve in input quest'ultimo insieme all'AND tra `Branch` e `Zero`. Naturalmente, un'implementazione equivalente avrebbe coinvolto un multiplexer in sostituzione della porta OR.
___
##### L'istruzione `jal`

In seguito all'istruzione `j`, diventa molto semplice implementare anche l'istruzione **`jal rd, imm`** ("Jump And Link"), un'altra istruzione di salto incondizionato.

Per l'aggiunta di questa istruzione, si seguiranno sempre gli stessi passaggi, a partire dalla **codifica** dell'istruzione: anche in questo caso, un formato che fa al caso nostro è il **formato di tipo UJ**. Per quanto riguarda il **funzionamento** di tale istruzione, essa svolge le stesse azioni di [[La CPU#L'istruzione `j`|quella precedente]], ma oltre a ciò va anche a scrivere nel registro di destinazione `rd` l'indirizzo dell'istruzione successiva, ossia $PC + 4$. Per permettere questa funzionalità, quindi, avremo bisogno delle seguenti **unità funzionali**:
- il **PC**;
- un'**unità di estensione del segno**, che provvederà a riordinare i bit dell'immediato e a estenderli a 32 bit;
- un **adder**, per eseguire la somma tra PC e immediato;
- un **multiplexer**, o in alternativa una **porta logica**, per selezionare il nuovo PC;
- un ulteriore **multiplexer**, stavolta per selezionare il dato da scrivere nel registro `rd`.

Notiamo che, supponendo di aver già implementato l'istruzione `j`, quasi tutte le componenti necessarie sono già a nostra disposizione, fatta eccezione per il secondo multiplexer, che riceverà in input l'indirizzo dell'istruzione successiva e l'eventuale dato da scrivere ottenuto dalla memoria di dati. 

Andiamo ora, a definire il **flusso di dati** necessario per ottenere il funzionamento desiderato. La sequenza di azioni che andranno eseguite sarà: ottenere l'istruzione, estrapolandone l'immediato; calcolare l'indirizzo dell'istruzione successiva; riordinare i bit dell'immediato; sommare quest'ultimo con il PC; scrivere l'indirizzo dell'istruzione successiva nel registro di scrittura; mandare al PC il valore ottenuto dalla somma con l'immediato. 

Per quanto riguarda i **segnali di controllo**, non servirà aggiungerne altri dato che **`Jal`** può essere utilizzato per controllare anche il multiplexer appena aggiunto, mentre ci si dovrà assicurare di abilitare **`RegWrite`** ma non **`MemWrite`**, per permettere la scrittura nel registro di destinazione e, parallelamente, evitare modifiche indesiderate nella memoria.

[tempi di esecuzione: 11, slide 15]

Andando ad ampliare l'implementazione precedente, otteniamo la seguente schematizzazione:

![[blocco_cpu_con_jal.png]]

In questo caso, l'hardware aggiunto è costituito esclusivamente dal **multiplexer** in basso a sinistra, responsabile di controllare la sorgente del dato da scrivere nel registro di destinazione.
___
##### L'istruzione `addi`

Aggiungiamo ancora un'altra istruzione, **`addi rd, rs1, imm`** ("Add Immediate"), un'istruzione aritmetica.

Innanzitutto stabiliamo la **codifica** dell'istruzione in questione, per cui la scelta del **formato di tipo I** risulta pressoché immediata. Per quanto riguarda il **funzionamento** di tale istruzione, essa andrà a operare una semplice somma tra il contenuto del registro operando `rs1` e una costante, fornita nel campo `imm` come stringa di 12 bit segnati; il risultato di tale operazione verrà poi scritto nel registro di destinazione `rd`. Per permettere questa funzionalità, quindi, avremo bisogno delle seguenti **unità funzionali**:
- un'**ALU**, per eseguire concretamente la somma;
- un **multiplexer**, che permetta la selezione dell'immediato come secondo operando per la somma;
- un'**unità di estensione del segno**, per estendere l'immediato a 32 bit.

Notiamo che, in realtà, tutte queste componenti sono già presenti nella nostra implementazione precedente, e non sarà dunque necessario aggiungere hardware.

Andiamo ora, a definire il **flusso di dati** necessario per ottenere il funzionamento desiderato. La sequenza di azioni che andranno eseguite sarà: ottenere l'istruzione, estrapolandone l'immediato; leggere il contenuto del registro operando `rs1`; estendere l'immediato a 32 bit; trasmettere questi due valori all'ALU; effettuare la loro somma; scrivere il risultato nel registro di destinazione `rd`. Per quanto riguarda i **segnali di controllo**, non ci sarà bisogno di introdurne altri.

[tempi di esecuzione: 11, slide 17]
___
##### L'istruzione `jalr`

[TODO: 12, slide 3/4]
___
##### L'istruzione `jr`

[TODO: 12, slide 5]
___
##### L'istruzione `jrr`

[TODO: 12, slide 6/10]
___
## Malfunzionamenti della Control Unit

[TODO: 12, slide 14/23]
___
## Pipeline

Quella che abbiamo analizzato finora è un'implementazione di un processore che potremmo definire a "**singolo ciclo**", sostanzialmente un processore che esegue un'istruzione per volta, iniziando l'esecuzione della successiva solo dopo aver terminato l'esecuzione della precedente. Si tratta di un modello funzionante, ma ciononostante particolarmente inefficiente, e al giorno d'oggi poco utilizzato. Invece, la quasi totalità dei [[Il calcolatore|calcolatori]] di oggi sfruttano una tecnica chiamata "pipeline".

La "**pipeline**" è una tecnica di implementazione di un processore che prevede la **sovrapposizione temporale dell'esecuzione di diverse istruzioni**. 

Per comprendere subito di cosa stiamo parlando, consideriamo un esempio concreto, come fare il bucato: si tratta di un procedimento "complesso", che richiede più passaggi, tra cui:
- caricare la lavatrice con i panni da lavare;
- terminato il lavaggio, spostare i panni lavati nell'asciugatrice;
- una volta asciutti, stirare i panni;
- rimettere i panni stirati nell'armadio.

Supponiamo di affrontare questa serie di passaggi usando un approccio "**non basato su pipeline**": fare ciò vorrebbe dire svolgere tutto il procedimento per un singolo carico di panni, e ripeterlo con un nuovo carico solo al termine del primo. Si tratta di un approccio funzionante, ma concretamente lento, a differenza di un approccio "**basato su pipeline**": in questo caso, dopo che la lavatrice finisce il primo ciclo di lavaggio e i panni vengono trasferiti nell'asciugatrice, si procede subito a riempire la lavatrice con il secondo carico di panni; dopo che il primo carico di panni ha terminato l'asciugatura, possiamo riempire la lavatrice con il terzo carico, l'asciugatrice con il secondo (che nel mentre è stato lavato), e procedere a stirare il terzo carico, e così via. Usare questo approccio porta a un tempo di esecuzione molto minore, come possiamo notare dai seguenti grafici:

![[pipeline_esempio.png]]

Seguendo un approccio basato su pipeline, **tutti gli stadi**, ossia i singoli passaggi, **del procedimento sono attivi contemporaneamente**. Infatti, applicare una pipeline non diminuisce, ovviamente, il tempo impiegato da un singolo stadio per eseguire la propria mansione, e neanche il tempo impiegato per completare un singolo procedimento; piuttosto, **ciò che viene diminuito è il tempo totale impiegato per completare più procedimenti**. In sostanza, ciò che viene migliorato è il "**throughput**" (o anche "**bandwidth**", cioè "**larghezza di banda**"), ossia il **numero di procedimenti completati per unità di tempo**.

##### La pipeline nell'architettura RISC-V

Gli stessi principi si possono applicare anche ai processori, dove ciò che si vuole porre in pipeline è l'**esecuzione di più istruzioni**. Come abbiamo già accennato, l'esecuzione di un'istruzione RISC-V può essere sostanzialmente divisa in **5 fasi**:
- l'**instruction fetch** (**IF**), che coinvolge principalmente il **PC** e la **memoria delle istruzioni**;
- l'**instruction decode** (**ID**), che coinvolge principalmente il **register file** e la **control unit**;
- l'**execute** (**EX**), che coinvolge principalmente l'**ALU**;
- eventualmente il **memory access** (**MEM**), che coinvolge principalmente la **memoria di dati**;
- eventualmente il **write back** (**WB**), che coinvolge principalmente il **register file**.

Di conseguenza, possiamo affermare che la pipeline dell'architettura RISC-V ha **5 stadi**, e il tempo di esecuzione di ciascuno di essi dipende dal tempo di esecuzione delle **singole operazioni delle unità funzionali**; in particolare, possiamo assumere i seguenti valori di tempo:
- l'**IF**, dunque la lettura dell'istruzione, dura $200\,\,ps$;
- l'**ID**, dunque la decodifica dell'istruzione e la lettura dei registri, dura $100\,\,ps$;
- l'**EX**, dunque un'operazione dell'ALU, dura $200\,\,ps$;
- il **MEM**, dunque l'accesso alla memoria di dati, dura $200\,\,ps$;
- il **WB**, dunque la scrittura di un dato in un registro, dura $100\,\,ps$.

A questo punto, tenendo a mente questi tempi e assumendo che multiplexer, unità di controllo, PC e unità di estensione del segno non introducano ulteriori ritardi, possiamo approssimare il **tempo di esecuzione delle istruzioni** di base previste nella [[La CPU#Assemblare le unità funzionali|prima implementazione]] dell'architettura RISC-V che abbiamo analizzato. La seguente tabella mostra proprio questo:

![[tempi_istruzioni_tabella.png]]

**In un'implementazione a singolo ciclo, tutte le istruzioni richiedono un ciclo di clock** per essere eseguite, e per soddisfare questo requisito la durata del ciclo di clock deve essere pari almeno al tempo di esecuzione dell'istruzione più "lenta". Nell'implementazione analizzata finora, tale istruzione sembra essere **`lw`**, con un tempo totale di esecuzione pari a $800\,\,ps$.

Utilizzando invece un'**implementazione basata su pipeline**, **la durata del ciclo di clock deve essere pari almeno al tempo di esecuzione dello stadio più "lento"**. In questo modo, fasi diverse possono essere eseguite contemporaneamente, e l'esecuzione di più istruzioni può essere notevolmente accelerata: infatti, seguendo questa logica, la durata del ciclo di clock può scendere fino a $200\,\,ps$, **moltiplicando così la velocità del processore**.

Del resto, l'architettura RISC-V è stata progettata proprio tenendo a mente un approccio basato su pipeline, e presenta diversi **vantaggi** che lo favoriscono, tra cui:
- la **costanza nella posizione dei campi relativi ai registri** all'interno dei vari [[Le istruzioni#Come vengono rappresentate le istruzioni nel calcolatore?|formati di istruzione]], che velocizza la lettura del contenuto degli stessi (è possibile già durante la fase di ID);
- la presenza di **operandi nella memoria solo per istruzioni di accesso alla stessa**, come `sw` e `lw`, e mai per operazioni aritmetico-logiche, che operano strettamente sui registri;
- l'**allineamento degli operandi in memoria**, e il loro **indirizzamento**, che consentono di effettuare un singolo accesso per dato;
- la **lunghezza fissa delle istruzioni**, sempre a 32 bit, che è il fattore determinante nel consentire una sovrapposizione tra IF e ID (essendo tutte le istruzioni della stessa lunghezza, il nuovo PC può essere calcolato a priori, senza sapere quale sia l'istruzione successiva, vantaggio che non si ha in architettura con istruzioni a dimensione variabile come la [[L'architettura RISC-V#L'architettura RISC-V|CISC]]).
___
## Criticità in una pipeline

In una pipeline, si possono verificare diverse situazioni in cui l'**istruzione successiva non può essere eseguita nel ciclo di clock immediatamente successivo** a quello corrente, per vari possibili motivi. Questo tipo di situazioni viene definito "**hazard**", o **criticità**, e può presentarsi principalmente in tre forme:
- hazard **strutturale**;
- hazard **sui dati**;
- hazard **sul controllo**.

In questo capitolo, analizzeremo ciascuna di queste criticità, quando si possono verificare e come prevenirle.

##### Hazard strutturali

Il primo tipo di hazard che andremo ad analizzare è il cosiddetto "**hazard strutturale**" (o "**structural hazard**"), che si verifica quando **l'hardware presente non è in grado di supportare la combinazione di istruzioni che si vorrebbe eseguire in un singolo ciclo di clock**. Tornando all'[[La CPU#Pipeline|esempio concreto del bucato]], un hazard strutturale potrebbe essere l'avere una sola macchina che funga sia da lavatrice che da asciugatrice, piuttosto che due macchine separate.

Nel contesto di un processore come quello che abbiamo visto finora, una simile situazione potrebbe verificarsi nel caso in cui venga utilizzata la stessa memoria sia per le istruzioni che per i dati: in questo caso, potrebbe tranquillamente succedere che, mentre un'istruzione sta effettuando un accesso alla memoria per leggere o scrivere un dato, il processore voglia effettuare il fetch di un'altra istruzione, provocando un ritardo.

In realtà, essendo l'architettura RISC-V progettata appositamente per un approccio basato su pipeline, è semplice per un progettista evitare gli hazard strutturali nella fase di progettazione del [[La CPU#Cos'è una CPU?|datapath]].
___
##### Hazard sui dati

Vediamo, ora, in cosa consiste un "**hazard sui dati**" (o "**data hazard**"): esso si verifica quando **uno stadio della pipeline deve attendere l'elaborazione di un altro stadio per poter essere eseguito**.

Nel contesto di un processore dotato di pipeline, una simile situazione potrebbe verificarsi nel caso in cui **un'istruzione dipende** (ad esempio, per un suo operando) **dal risultato di un'istruzione precedente**, che sta ancora venendo eseguita. Supponiamo, ad esempio, di voler eseguire la seguente sequenza di istruzioni:

```
add x1, x2, x3
sub x4, x1, x5
```

Si nota subito che `x1` è utilizzato come registro di destinazione nell'istruzione `add`, e come registro operando nell'istruzione `sub`; tuttavia, il risultato dell'operazione svolta dalla prima istruzione non verrà scritto nel registro in questione fino al suo 5° stadio di esecuzione, mentre la seconda istruzione potrebbe leggerne il contenuto già nel 2° stadio, provocando effettivamente un **ritardo di due cicli di clock**.

In realtà, gli hazard sui dati sono una **criticità molto comune**, che potrebbero portare a diversi stalli e quindi a un rallentamento considerevole del processore. Un primo approccio per limitare quest'impatto potrebbe essere affidarsi a dei **compilatori**, che effettuino delle ottimizzazioni della serie di istruzioni, tuttavia essi hanno un potere limitato e non sufficiente a risolvere il problema. La soluzione più utilizzata, invece, è basata sull'osservazione che, in realtà, **spesso non è necessario che termini l'esecuzione di un'istruzione per risolvere un hazard sui dati**: ad esempio, nella situazione proposta poco fa, si potrebbe utilizzare il risultato della somma tra `x2` e `x3` non appena esso viene restituito dall'ALU, senza attendere che esso venga scritto in `x1` e poi letto da quest'ultimo. La tecnica che prevede l'aggiunta di un **circuito che fornisca**, in un certo punto dell'esecuzione, **il dato mancante propagandolo da una risorsa interna** è detta "**propagazione**", detta anche "**bypass**" o "**forwarding**".

Applicando questo ragionamento all'esempio precedente, notiamo che ciò sarebbe possibile propagando il dato in output dalla fase EX della prima istruzione (`add x1, x2, x3`) all'input della fase EX della seconda istruzione (`sub x4, x1, x5`), come si evince dal seguente grafico:

![[pipeline_bypass_esempio.png]]

Naturalmente, una condizione imprescindibile per il corretto funzionamento di questo approccio è che **lo stadio che deve ricevere il dato deve essere successivo nel tempo allo stadio che lo produce**, dato che se non fosse così il primo non avrebbe nulla da ricevere, e quindi uno stallo sarebbe inevitabile. 

È importante tenere a mente, del resto, che per quanto la propagazione possa essere uno strumento molto utile, **non rappresenta una soluzione universale** per tutti gli stalli nell'esecuzione di una pipeline. Supponendo, ad esempio, che l'istruzione `add` venga sostituita da un `lw`, che dunque accede a un dato in memoria piuttosto che in un registro, il dato in questione diventerebbe disponibile solamente al termine del 4° stadio della prima istruzione, rendendo un'applicazione della propagazione impossibile proprio per la regola esposta poco fa. Per questo genere di situazioni (in particolare, quella proposta ora viene detta "**load-use data hazard**"), bisognerà necessariamente **imporre uno stallo** della durata di un ciclo di clock, in modo da permettere effettivamente una qualche forma di propagazione, come possiamo vedere nel seguente grafico:

![[pipeline_bypass_esempio1.png]]

In queste situazioni si parla di "**stallo della pipeline**", o più comunemente di "**bolla**" o "**bubble**".

Il meccanismo della propagazione, al tempo stesso, illustra un'altra caratteristica vantaggiosa dell'architettura RISC-V, ossia che **tutte le istruzioni scrivono un unico risultato** in un unico posto, e sempre **nell'ultimo stadio della pipeline**: ciò semplifica notevolmente l'eventuale applicazione della propagazione, che sarebbe molto più difficile se ogni istruzione producesse più risultati da propagare, o se essi venissero scritti prima del termine dell'esecuzione.

Per concludere questo paragrafo, vediamo un esempio più complesso, con una serie di istruzioni che presenta al suo interno diversi hazard sui dati:

```
lw x1, 0(x31)
lw x2, 4(x31)
add x3, x1, x2
sw x3, 12(x31)
lw x4, 8(x31)
add x5, x1, x4
sw x5, 16(x31)
```

In questo contesto, notiamo che **è presente un hazard in corrispondenza di entrambe le istruzioni `add`**: infatti, la prima cerca di effettuare la somma tra i contenuti dei registri `x1` e `x2` quando `x2` ancora non contiene il dato desiderato; analogamente, la seconda cerca di effettuare la somma tra i contenuti dei registri `x1` e `x4` quando `x4` ancora non contiene il dato desiderato. Fortunatamente, in questo caso non ci si dovrà complicare troppo con bolle o propagazioni, ma basterà modificare l'ordine delle istruzioni:

```
lw x1, 0(x31)
lw x2, 4(x31)
lw x4, 8(x31)
add x3, x1, x2
sw x3, 12(x31)
add x5, x1, x4
sw x5, 16(x31)
```

Spostando l'istruzione `lw x4, 8(x31)`, non solo diamo tempo all'istruzione `lw x2, 4(x31)` di scrivere il dato nel registro `x2` prima che esso diventi un operando in `add x3, x1, x2`, ma consentiamo anche all'istruzione spostata di scrivere il dato nel registro `x4` prima che esso diventi un operando in `add x5, x1, x4`. La nuova serie di istruzioni, dunque, risulta ottimizzata e priva di hazard sui dati. Se invece avessimo voluto mantenere la medesima sequenza di istruzioni, sarebbe stato necessario imporre due bolle, una prima della prima istruzione `add`, e un'altra prima della seconda.
___
##### Hazard sul controllo

Infine, parliamo degli "**hazard sul controllo**", detti anche "**control hazard**" o "**hazard sui salti condizionati**", essendo le istruzioni di questo tipo quelle in cui si presentano solitamente. Essi, infatti, si verificano quando **bisogna prendere una decisione in funzione del risultato dell'esecuzione di un'istruzione, mentre altre istruzioni stanno già venendo eseguite**, con la possibilità che quest'ultime debbano essere scartate.

Nel contesto di un processore dotato di pipeline, una simile situazione potrebbe verificarsi proprio nel contesto di un'**istruzione di salto condizionato**, come **`beq`**. Infatti, l'istruzione (o le istruzioni) successiva ad essa viene caricata nel ciclo di clock immediatamente successivo, prima ancora che venga valutata la condizione su cui si basa il salto, e dunque prima che il processore sappia se quell'istruzione andrà effettivamente eseguita o meno. Una possibile soluzione può essere **imporre uno stallo della pipeline appena viene caricata un'istruzione di salto condizionato, e attendere il risultato del confronto per proseguire con l'esecuzione di altre istruzioni**. Ad esempio, avendo la seguente serie di istruzioni:

```
add x4, x5, x6
beq x1, x0, 40
or x7, x8, x9
...
```

si dovrebbe inserire una bolla pari a un ciclo di clock immediatamente dopo l'IF dell'istruzione `beq x1, x0, 40`, in modo da dare tempo all'ALU di valutare se il contenuto di `x1` è uguale al contenuto di `x0`, sapendo così quale sarà la prossima istruzione da eseguire. Graficamente, possiamo visualizzare questo meccanismo nel modo seguente:

![[pipeline_control_hazard.png]]

A volte, però, non è possibile risolvere la criticità inserendo uno stallo di un solo ciclo di clock, e si rischia di creare rallentamenti più sostanziosi nella pipeline. Una seconda soluzione, più efficiente, potrebbe invece essere **predire un certo risultato per il confronto del salto condizionato, e procedere con l'esecuzione basandosi su tale predizione**. Tendenzialmente, l'approccio più semplice e comunque relativamente efficace è quello di **supporre che il salto non venga effettuato**, caricando a priori la prossima istruzione: infatti, se la predizione si rivela corretta si procede al massimo della velocità; se la predizione, invece, è sbagliata si procederà a "buttare" l'istruzione caricata sostituendola con quella indicata dal salto. Di seguito, due grafici che esemplificano in ordine entrambe queste casistiche:

![[pipeline_control_hazard1.png]]

Naturalmente, nel secondo grafico l'esclusiva presenza della bolla risulta essere una semplificazione di ciò che avviene realmente. Questo secondo approccio risulta essere più vantaggioso del primo, in quanto in alcune situazioni comporta uno stallo di uno o due cicli di clock (risultato inevitabile, invece, con il primo approccio), ma lo elimina completamente in altre.

Una versione più "intelligente" di questo approccio di predizione implica il **prevedere se un salto debba essere eseguito o meno in base al contesto**. Ad esempio, consideriamo i salti posti al termine dei cicli, utilizzati per ritornare all'inizio del ciclo ed effettuare una nuova iterazione dello stesso; si tratta, naturalmente, di salti che vanno "all'indietro", e verosimilmente essi verranno eseguiti la maggior parte delle volte, dunque si potrebbe prevedere che i salti verso indirizzi minori vadano sempre eseguiti.

Ciononostante, questi rimangono **approcci rigidi** alla predizione dei salti, tipici di "**predittori statici**" basati su un'ipotesi costante e noncuranti delle individualità specifiche di ciascuna istruzione di salto. Un "**predittore dinamico**", invece, determina la sua predizione per ciascun salto in base al comportamento precedente di quella specifica istruzione, ed è capace di modificare volta per volta le sue predizioni. Un'implementazione comune di predittore dinamico consiste, ad esempio, nel **memorizzare uno "storico" per ciascuna istruzione di salto condizionato**, ricordando quando è stato effettuato e quando no, e utilizzando il comportamento più frequente o più recente per effettuare la predizione. Si tratta di una soluzione che si è evoluta nel tempo, divenendo sempre più complessa ed efficiente, e arrivando ai giorni nostri a una precisione superiore al 90%.

Infine, vi è un terzo e ultimo approccio per affrontare gli hazard sul controllo, detto "**decisione ritardata**", o "**salto ritardato**": applicando questo approccio, **il processore esegue sempre l'istruzione successiva al salto, ed eventualmente il salto viene eseguito dopo di essa**. Si tratta di un comportamento che può risultare controproducente, dato che apparentemente comporta un'esecuzione in ordine errato delle istruzioni, ma il compilatore riesce a prevenire eventuali errori e a garantire il comportamento previsto dal programmatore. Pur non sempre possibile, si tratta di una soluzione funzionante, adottata principalmente nell'architettura MIPS.
___
## Un'implementazione basata su pipeline di un processore RISC-V

Ora che abbiamo approfondito il concetto di pipeline, e le possibili criticità che ne conseguono, siamo pronti a **integrare una pipeline nell'[[La CPU#Un'implementazione di base di un processore RISC-V|implementazione di base]] di processore che abbiamo analizzato in precedenza**. Per semplicità, andremo a effettuare quest'operazione sulla prima implementazione, quella che prevedeva solamente le istruzioni `add`, `sub`, `and`, `or`, `lw`, `sw` e `beq`, ma naturalmente gli stessi principi possono essere applicati anche su processori più completi.

##### Registri di pipeline

Come abbiamo stabilito, un'istruzione dell'architettura RISC-V può essere "suddivisa" in **5 fasi ben distinte** (IF, ID, EX, MEM, WB), e di conseguenza la pipeline di tale architettura presenterà **5 stadi**. Perciò, per poter integrare una pipeline nella nostra implementazione, occorre innanzitutto **identificare con precisione l'hardware appartenente a ciascuno stadio della pipeline**. Nello schema seguente, rivisitiamo l'implementazione in questione evidenziando questa divisione:

![[blocco_cpu_divisione_pipeline.png]]

Il flusso di istruzioni e dati è quasi completamente direzionato **da sinistra verso destra**, fatta eccezione per i nodi evidenziati in arancione, ossia per la **scrittura del risultato di un'operazione nel registro di destinazione** e per la **selezione del valore successivo del PC**. Si noti, tra l'altro, che proprio queste due parti dell'implementazione possono causare **[[La CPU#Criticità in una pipeline|hazard]]**, in particolare:
- nella scrittura del risultato di un'operazione nel registro di destinazione vi è un **hazard sui dati**;
- nella selezione del valore successivo del PC vi è un **hazard sul controllo**.

Per favorire l'esecuzione di più istruzioni contemporaneamente all'interno di questo stesso processore, in modo che in un qualsiasi momento ogni istruzione utilizzi una specifica parte del circuito, possiamo inserire dei **registri**, che lo vadano a dividere concretamente nelle sezioni relative a ciascuno stadio della pipeline e che conservino i dati parziali generati dalle istruzioni. Possiamo inserire questi registri nel modo seguente:

![[blocco_cpu_divisione_pipeline_registri.png]]

I registri, evidenziati in arancione, rappresentano gli "**intermezzi**" tra due fasi dell'esecuzione di un'istruzione, con tali fasi indicate dalla dicitura che si trova sopra di essi. Analizzando la quantità e il tipo di dati che dovranno conservare, possiamo capire **quanti bit conserva ciascuno di essi**:
- il registro che si trova **tra IF e ID** va a conservare il PC (32 bit) e l'istruzione da eseguire (32 bit), dunque si tratta di un registro **a 64 bit**;
- il registro che si trova **tra ID ed EX** va a conservare il PC (32 bit), i dati eventualmente letti da due registri (32 bit ciascuno, quindi 64 bit) e l'eventuale immediato esteso dall'unità di estensione del segno (32 bit), dunque si tratta di un registro **a 128 bit**;
- il registro che si trova **tra EX e MEM** va a conservare un nuovo PC (32 bit), il segnale `Zero` (1 bit), il risultato dell'operazione svolta dall'ALU (32 bit) ed eventualmente il dato letto da uno dei registri (32 bit), dunque si tratta di un registro a **97 bit**;
- il registro che si trova **tra MEM e WB** va a conservare il dato eventualmente letto dalla memoria di dati (32 bit) e il risultato dell'operazione svolta dall'ALU (32 bit), dunque si tratta di un registro **a 64 bit**.

In ogni ciclo di clock, dunque, l'esecuzione di tutte le istruzioni procede da un "**registro di pipeline**" a quello successivo.
___
##### Esempio: esecuzione di `lw`

Per comprendere meglio come ciò avviene, analizziamo nel dettaglio il funzionamento dell'istruzione `lw` in questo contesto (la scelta ricade su questa istruzione in quanto coinvolge tutte e 5 gli stadi della pipeline). 

Innanzitutto, vi è la fase di **IF**, in cui l'istruzione viene prelevata dalla memoria di istruzioni utilizzando il PC, e scritta nel registro IF/ID; al tempo stesso, il contenuto del PC viene incrementato di 4 e riscritto al suo interno, in modo da essere pronto per il successivo ciclo ci clock, nonché salvato anch'esso nel registro IF/ID, in caso venga richiesto da un'istruzione successiva (come un `beq`):

![[pipeline_lw_if.png]]

Poi, vi è la fase di **ID**, in cui dall'istruzione vengono prelevati l'immediato di 12 bit (che verrà esteso a 32 bit dall'unità di estensione del segno) e il numero del registro da leggere e di quello di scrittura; l'immediato esteso, il contenuto del registro di lettura e anche il PC vengono poi trasmessi al registro ID/EX:

![[pipeline_lw_id.png]]

A questo punto, siamo arrivati alla fase di **EX**, in cui il contenuto del registro di lettura e l'immediato vengono trasmessi all'ALU per essere sommati, con il risultato di questa somma che viene trasmesso al registro EX/MEM:

![[pipeline_lw_exe.png]]

Procediamo alla fase di **MEM**, in cui il risultato della somma effettuata dall'ALU viene trasmessa dal registro EX/MEM alla memoria di dati, utilizzato come indirizzo del dato da leggere; quest'ultimo, poi, viene trasmesso al registro MEM/WB:

![[pipeline_lw_mem.png]]

Infine, giungiamo alla fase di **WB**, in cui il dato prelevato dalla memoria viene letto dal registro MEM/WB e trasferito al register file, per essere scritto nel registro di destinazione:

![[pipeline_lw_wb.png]]

Notiamo, tuttavia, un'**imperfezione** nell'hardware utilizzato, che porterebbe a un funzionamento errato di quest'istruzione nel contesto di una pipeline: supponendo, ad esempio, di star eseguendo più istruzioni `lw` in successione, al momento del WB di una di esse il numero del registro di scrittura non sarà più quello relativo all'istruzione in questione, ma sarà stato sostituito da quello indicato in un'istruzione successiva. In parole povere, c'è bisogno di **integrare un modo per ogni istruzione di ricordare il suo registro di scrittura**; è possibile fare ciò modificando leggermente il flusso dei dati, facendo in modo che il numero del registro di scrittura non venga subito trasmesso al register file nella fase di ID, ma sia piuttosto memorizzato stadio dopo stadio nei vari registri di pipeline, e in seguito trasmesso al register file insieme al dato da scrivere nella fase di WB. Di seguito, una variazione della nostra implementazione dotata di questo accorgimento (i cambiamenti sono evidenziati in arancione):

![[pipeline_lw_fixed.png]]
___
##### Rappresentazione grafica della pipeline

Per facilitare la comprensione del funzionamento di una pipeline, ci sono principalmente **due tipi di diagrammi** che possono essere disegnati:
- un **diagramma di pipeline a più cicli di clock**;
- un **diagramma di pipeline a singolo ciclo di clock**.

Tendenzialmente, **un diagramma di pipeline a più cicli di clock è più semplice, ma meno dettagliato**. Vediamone un esempio, considerando la seguente serie di istruzioni:

```
lw x10, 40(x1)
sub x11, x2, x3
add x12, x3, x4
lw x13, 48(x1)
add x14, x5, x6
```

L'esecuzione in pipeline di queste istruzioni può essere rappresentata graficamente con il seguente diagramma a più cicli di clock:

![[diagramma_pipeline_piùcicli_esempio.png]]

Una versione più semplificata e basilare dello stesso diagramma può essere la seguente:

![[diagramma_pipeline_piùcicli_esempio1.png]]

In questo tipo di diagrammi, il tempo scorre **da sinistra verso destra**, e le istruzioni si susseguono **dall'alto verso il basso**.

Per quanto riguarda i **diagrammi di pipeline a singolo ciclo di clock**, essi mostrano lo stato dell'unità di elaborazione durante un ciclo di clock e, solitamente, le istruzioni caricate nella pipeline vengono identificate da etichette poste sopra lo stadio in cui stanno venendo eseguite. Ad esempio, il seguente diagramma rappresenta lo stato dell'unità di elaborazione che esegue la stessa serie di istruzioni in corrispondenza del quinto ciclo di clock della pipeline:

![[diagramma_pipeline_singolociclo_esempio.png]]
___
##### Control Unit nella pipeline

A questo punto, siamo pronti ad affrontare la questione dei **segnali di controllo** e, di conseguenza, della **control unit** all'interno dell'implementazione basata su pipeline. Supponendo di aver aggiunto alla nostra implementazione l'hardware necessario per effettuare un **branch** (`beq`), l'implementazione dotata dei vari segnali di controllo è la seguente:

![[cpu_pipeline_controllo.png]]

Notiamo che, di fatto, i vari segnali di controllo vengono gestiti pressoché allo stesso modo dell'[[La CPU#Assemblare le unità funzionali|implementazione a singolo ciclo di clock]]; in generale, nell'inserire la control unit si cercherà di **riutilizzare il più possibile la struttura dell'implementazione precedente**.

Dunque, come nell'implementazione precedente supporremo che **il PC venga aggiornato a ogni ciclo di clock**, per cui non ci sarà bisogno di alcun segnale di controllo che regoli tale operazione; per la stessa motivazione, **non si aggiungeranno neanche segnali di controllo che regolino la scrittura di dati nei registri di pipeline**. 

Stabilito ciò, passiamo effettivamente a definire il **funzionamento della control unit**, ossia la particolare combinazione e sequenza di segnali di controllo che andranno abilitati in ogni momento per l'esecuzione di una determinata istruzione. In particolare, converrà **dividere i segnali di controllo in 5 categorie**, corrispondenti ai 5 stadi di esecuzione di un'istruzione RISC-V in pipeline, ossia:
- **IF**, in cui non sarà necessario controllare nessuna unità funzionale direttamente;
- **ID**, in cui non sarà necessario controllare nessuna unità funzionale direttamente;
- **EX**, in cui sarà necessario controllare i segnali **`ALUOp`** e **`ALUSrc`**, dove il primo seleziona il tipo di operazione da far svolgere all'ALU, e il secondo se inviare come input all'ALU il dato letto da un registro o un immediato;
- **MEM**, in cui sarà necessario controllare i segnali **`Branch`**, **`MemRead`** e **`MemWrite`**, dove il primo viene abilitato se viene eseguito un salto condizionato (solo in questo caso il segnale **`PCSrc`** viene abilitato, altrimenti non lo è, selezionando di default l'indirizzo dell'istruzione successiva), il secondo consente la lettura di un dato dalla memoria di dati, e il terzo consente la scrittura di un dato nella memoria di dati;
- **WB**, in cui sarà necessario controllare i segnali **`MemtoReg`** e **`RegWrite`**, dove il primo sceglie se inviare al registro di scrittura il risultato dell'operazione eseguita dall'ALU o il dato letto dalla memoria, e il secondo consente la scrittura di un dato nel registro di destinazione.

Le combinazioni di segnali di controllo necessarie per eseguire una particolare istruzione rimangono pressoché invariate, tuttavia ora è possibile raggruppare questi segnali in base alla loro "**area di competenza**", come possiamo vedere nella seguente tabella:

![[segnali_controllo_pipeline_tabella.png]]

Implementare la control unit significa **impostare correttamente il valore dei segnali di controllo per ciascuno stadio della pipeline, e per ciascuna istruzione**. Dato che questi segnali vengono utilizzati a partire dallo stadio EX, essi possono essere determinati **durante l'ID**, e venire poi utilizzati negli stadi successivi. Il modo più semplice per propagare questi segnali di controllo è quello di **estendere i registri di pipeline**, così che possano includere anche i bit necessari per memorizzarli e trasmetterli avanti, finché non verranno utilizzati. Il flusso dei segnali di controllo tra i vari stadi può essere visualizzato nel modo seguente:

![[segnali_controllo_flusso.png]]

Integrando questa modifica all'interno della nostra implementazione, otteniamo ciò:

![[cpu_pipeline_cu.png]]

Ora che abbiamo sostanzialmente terminato di implementare un processore RISC-V basato su pipeline, rimane un ultimo problema da affrontare: gli **[[La CPU#Criticità in una pipeline|hazard]]**.
___
##### Come affrontare gli hazard sui dati?

Supponiamo, ad esempio, di avere la seguente serie di istruzioni:

```
sub x2, x1, x3
and x12, x2, x5
or x13, x6, x2
add x14, x2, x2
sw x15, 100(x2)
```

Notiamo che **le ultime quattro istruzioni dipendono tutte dal risultato della prima**, ossia dal contenuto del registro **`x2`**: ciò porta chiaramente a un importante **hazard sui dati**, dato che il risultato dell'istruzione `sub x2, x1, x3` sarà scritta nel register file solo al quinto ciclo di clock, in cui l'esecuzione di quasi tutte le altre istruzioni sarà già stata avviata, e ciò potrebbe portare a errori o a comportamenti non previsti in quest'ultime. Osservando un **[[La CPU#Rappresentazione grafica della pipeline|diagramma di pipeline a più cicli di clock]]**, questo problema diventa ancora più evidente nel notare **linee di dipendenza che vanno "indietro nel tempo"**:

![[diagramma_pipeline_piùcicli_esempio2.png]]

Tuttavia, è possibile risolvere il problema mediante la **[[La CPU#Hazard sui dati|propagazione]] del dato necessario**: infatti, tecnicamente, esso è disponibile già al termine del terzo ciclo di clock, e le istruzioni che ne hanno bisogno prima che esso venga eventualmente scritto nel registro `x2`, ossia `and x12, x2, x5` e `or x13, x6, x2`, lo utilizzerebbero rispettivamente nel quarto e quinto ciclo di clock. Dunque, è perfettamente possibile eseguire questa sequenza di istruzioni senza stalli, **propagando il dato alle unità che lo richiedono prima che esso venga scritto nel register file**.

Ma come si applica concretamente la propagazione? Per semplicità, consideriamo un esempio del genere, in cui essa viene applicata su un **dato necessario per un'operazione da eseguire nello stadio EX**, e quindi sostanzialmente all'interno dell'**ALU**. Ciò vuol dire che quando un'istruzione si trova nello stadio EX, e ha bisogno di un dato che deve essere ancora scritto dallo stadio WB di un'istruzione precedente, occorre che il dato in questione venga portato all'input dell'ALU.

Per comprendere e formalizzare al meglio queste dipendenze, possiamo adottare delle **notazioni per i campi dei registri di pipeline**, ossia per i dati particolari che vengono memorizzati e trasmessi da quest'ultimi. Ad esempio, la notazione "**ID/EX.rs1**" si riferisce al numero del primo registro di lettura dell'istruzione (`rs1`) memorizzato nel registro ID/EX. Utilizzando questa notazione, possiamo formalizzare principalmente **due coppie di condizioni che generano hazard sui dati**, ossia:
- la condizione **1a**, ossia che **EX/MEM.rd = ID/EX.rs1**;
- la condizione **1b**, ossia che **EX/MEM.rd = ID/EX.rs2**;
- la condizione **2a**, ossia che **MEM/WB.rd = ID/EX.rs1**;
- la condizione **2b**, ossia che **MEM/WB.rd = ID/EX.rs2**.

Si tratta, naturalmente, di condizioni che si verificano solo nel caso in cui **il campo `RegWrite` del registro a cui appartiene `rd` è abilitato** (se non deve avvenire una scrittura di dati nel register file, propagare i dati non risulta necessario), e in cui **tale campo `rd` è diverso da $0$** (il registro `x0` deve contenere sempre il valore $0$, dunque si evita la propagazione nel caso in cui esso venga indicato come registro di scrittura, in quanto non verrà scritto nulla nel concreto).

[da MEM a MEM: 15, slide 9/18]

A questo punto, tornando ad esempio sul primo degli hazard che abbiamo rilevato nell'esempio precedente, esso si verifica sul registro `x2` tra la scrittura del risultato dell'istruzione `sub x2, x1, x3` e la lettura del primo operando dell'istruzione `and x12, x2, x5`; tale hazard si verifica, in particolare, quando l'istruzione `sub` si trova nello stadio MEM, mentre l'istruzione `and` si trova nello stadio EXE. Di conseguenza, possiamo affermare che si tratta di un **hazard di tipo 1a**, ossia **EX/MEM.rd = ID/EX.rs1**, dove il registro `rd`, che coincide con il registro `rs1`, è `x2`. Seguendo lo stesso ragionamento, notiamo invece che il secondo hazard rilevato consiste in un **hazard di tipo 2b**, ossia **MEM/WB.rd = ID/EX.rs2**, che coinvolge sempre il registro `x2`.

Avendo capito quali tipi di hazard sui dati possono verificarsi, e avendo imparato come individuarli e categorizzarli, non ci resta che **propagare concretamente i dati corretti**. Il grafico seguente consiste in una variazione di quello mostrato in precedenza, dove vengono evidenziate **le linee di dipendenza tenendo in conto l'utilizzo della propagazione**:

![[diagramma_pipeline_piùcicli_esempio3.png]]

Notiamo che i dati da propagare si trovano, in questo nuovo approccio, nei **registri di pipeline**; dunque, per poterli propagare è necessario che **l'ALU possa ricevere input non solo dal registro ID/EX, ma anche da altri registri di pipeline**. Per selezionare l'origine degli input dell'ALU, possiamo aggiungere dei **multiplexer** in corrispondenza degli stessi, insieme agli appositi **segnali di controllo**. Ciascuno dei due multiplexer da inserire selezionerà una delle seguenti **tre possibili casistiche**:
- **non avviene alcuna propagazione**, e dunque il valore di input proviene dal registro di pipeline ID/EX;
- **il dato viene propagato dall'istruzione precedente**, e dunque il valore di input proviene dal registro di pipeline EX/MEM;
- **il dato viene propagato dalla seconda istruzione precedente**, e dunque il valore di input proviene dal registro di pipeline MEM/WB.

Di seguito, uno schema semplificato (vengono omesse varie componenti) dell'hardware appartenente agli **ultimi tre stadi della pipeline contemplando la propagazione** (le componenti aggiunte sono state evidenziate in arancione):

![[cpu_pipeline_forwarding_semp.png]]

La diversa combinazione dei segnali di controllo **`PropagaA`** e **`PropagaB`**, entrambi di 2 bit, determina la particolare selezione di sorgenti di dati. Il loro comportamento può essere riassunto nella seguente tabella:

![[segnali_controllo_pipeline_forwarding_tabella.png]]

Dato che i multiplexer si trovano nello stadio EX, possiamo affermare che **il controllo della propagazione avviene nello stadio EX**; tuttavia, ciò rende necessario **trasportare il numero dei due registri di lettura dallo stadio ID al registro di pipeline ID/EX**, in modo da poter permettere all'unità di propagazione di verificare se è presente o meno un hazard sui dati. 

Stabilito ciò, possiamo esplicitare per comodità le **condizioni che devono verificarsi** perché avvenga ciascuno dei 4 hazard sui dati formalizzati in precedenza (le condizioni 1a e 1b, che rappresentano degli hazard nello stadio EX, e 2a e 2b, che rappresentano degli hazard nello stadio MEM):
- la condizione **1a**, in corrispondenza della quale si dovrebbe avere `PropagaA = 10`, avviene quando:

```
if  (EX/MEM.RegWrite
and (EX/MEM.rd != 0)
and (EX/MEM.rd = ID/EX.rs1))
```

- la condizione **1b**, in corrispondenza della quale si dovrebbe avere `PropagaB = 10`, avviene quando:

```
if  (EX/MEM.RegWrite
and (EX/MEM.rd != 0)
and (EX/MEM.rd = ID/EX.rs2))
```

- la condizione **2a**, in corrispondenza della quale si dovrebbe avere `PropagaA = 01`, avviene quando:

```
if  (MEM/WB.RegWrite
and (MEM/WB.rd != 0)
and (MEM/WB.rd = ID/EX.rs1))
```

- la condizione **2b**, in corrispondenza della quale si dovrebbe avere `PropagaB = 01`, avviene quando:

```
if  (MEM/WB.RegWrite
and (MEM/WB.rd != 0)
and (MEM/WB.rd = ID/EX.rs2))
```

Supponendo che il register file fornisca in uscita il dato corretto anche quando un'istruzione nello stadio ID va a leggere il contenuto di un registro scritto nello stesso ciclo di clock da un'altra istruzione nello stadio WB, si ha che **non si può verificare un hazard nello stadio WB**. Un register file di questo tipo implementa una particolare forma di propagazione direttamente al suo interno, proprio per permettere ciò.

Di seguito, una schematizzazione dell'**implementazione dell'unità di elaborazione con le opportune modifiche per gestire gli hazard sui dati tramite propagazione** (si tratta di uno schema semplificato, che omette varie parti come l'estensione del segno o la logica di branch):

![[cpu_pipeline_forwarding_semp1.png]]

Ci sono casi, tuttavia, in cui **la propagazione non è sufficiente**, e per poterla applicare sarà comunque necessario inserire degli **stalli** nell'esecuzione delle istruzioni. Si pensi, ad esempio, alla seguente sequenza di istruzioni:

```
lw x2, 20(x1)
and x4, x2, x5
or x8, x2, x6
add x9, x4, x2
sub x1, x6, x7
```

In questo esempio, una criticità del genere si presenta con l'istruzione `and x4, x2, x5`, che tenta di leggere un registro che deve ancora essere scritto dall'istruzione di load che la precede, ossia `lw x2, 20(x1)`. Visualizziamo la pipeline di queste istruzioni nel diagramma apposito:

![[diagramma_pipeline_piùcicli_esempio4.png]]

Durante il quarto ciclo di clock, il dato da scrivere in `x2` deve ancora essere letto dalla memoria, ed è dunque ancora non disponibile, ma al tempo stesso l'ALU si appresta a eseguire l'operazione prevista per l'istruzione successiva. Dunque, una regola che vale generalmente è che **occorre mettere in stallo la pipeline quando un'istruzione di load è seguita da un'istruzione che utilizza il dato letto da quest'ultima**.

Risulta quindi necessaria, oltre all'unità di propagazione, anche una cosiddetta "**unità di rilevamento degli hazard**", che possa inserire uno stallo tra l'istruzione di load e l'istruzione successiva che dipende dalla load **durante lo stadio ID** di quest'ultima. Per le istruzioni di load, in particolare, quest'unità implementa la seguente logica:

```
if  (ID/EX.MemRead 
and (ID/EX.rd = IF/ID.rs1) 
or  (ID/EX.rd = IF/ID.rs2)) -> mettere in stallo la pipeline
```

dove la prima condizione (`ID/EX.MemRead`) stabilisce che l'istruzione che si trova nello stadio EX della sua esecuzione è un'istruzione di load, mentre la seconda e la terza (`ID/EX.rd = IF/ID.rs1` e `ID/EX.rd = IF/ID.rs2`) stabiliscono che il numero del registro di scrittura dell'istruzione di load coincide con il numero di uno dei registri di lettura dell'istruzione successiva. 

Se tutte queste condizioni vengono rispettate, l'istruzione nello stadio ID viene messa in **stallo per un ciclo di clock**, permettendo in seguito alla **propagazione** di gestire le dipendenze (in alternativa, sarebbe necessario un ulteriore ciclo di clock di stallo). Al tempo stesso, se l'istruzione nello stadio ID viene messa in stallo, lo stesso deve accadere anche per l'**istruzione nello stadio IF**. Per impedire a queste due istruzioni di procedere nella pipeline, basterebbe semplicemente **impedire l'aggiornamento del PC e del registro di pipeline IF/ID**; al tempo stesso, però, occorre che l'esecuzione degli stadi successivi a ID continui senza effetti, che questi stadi lavorino "a vuoto". Per permettere ciò, bisogna eseguire una "istruzione" particolare, ossia una **`nop`** ("**not operation**").

Ma come possiamo inserire concretamente una `nop` nella pipeline? **Impostando a $0$ tutti i 7 segnali di controllo degli stadi EX, MEM e WB**, è possibile creare effettivamente un'istruzione che non produce risultati, che è proprio ciò di cui abbiamo bisogno. Dunque, andiamo a "trasformare" l'istruzione `and x4, x2, x5` in una `nop`, andando ad **azzerare i segnali di controllo contenuti nei campi EX, MEM e WB del registro di pipeline ID/EX**, che verranno poi trasmessi in avanti ad ogni ciclo di clock, producendo l'assenza di effetti desiderata. Possiamo visualizzare in maniera più chiara ciò che avviene con il seguente diagramma:

![[diagramma_pipeline_piùcicli_esempio5.png]]

Notiamo che, in questo modo, **l'esecuzione dell'intera sequenza di istruzioni**, a partire dalla seconda, **viene ritardata di un ciclo di clock**. La seconda e la terza istruzione, in particolare, dovranno ripetere nel quarto ciclo di clock ciò che avevano già fatto nel terzo. Di seguito, vediamo una versione aggiornata dell'unità di elaborazione, dotata di un'**unità di rilevamento degli hazard** per gestire questo tipo di situazioni (anche stavolta, vengono omesse parti come logica di branch ed estensione del segno):

![[cpu_pipeline_forwarding_semp2.png]]

Ricapitolando, l'**unità di propagazione** controlla i **multiplexer agli input dell'ALU**, in modo da selezionare accuratamente la sorgente degli operandi in base ai segnali di controllo `PropagaA` e `PropagaB`; l'**unità di rilevamento degli hazard** controlla invece la **riscrittura del PC e del registro di pipeline IF/ID**, così come il **multiplexer che seleziona i segnali di controllo da scrivere nel registro di pipeline ID/EX**.
___
##### Come affrontare gli hazard sul controllo?

Prima di procedere, forniamo di seguito una schematizzazione alternativa del nostro processore rispetto a quella vista al termine del [[La CPU#Come affrontare gli hazard sui dati?|paragrafo precedente]], che omette buona parte della logica di propagazione e di rilevamento degli hazard, ma in cui è possibile trovare la **logica di branch e di estensione del segno**:

![[cpu_pipeline_forwarding.png]]

Supponiamo, ad esempio, di avere la seguente serie di istruzioni:

```
beq x1, x0, 16
and x12, x2, x5
or x13, x6, x2
add x14, x2, x2

...

lw x4, 100(x7)
```

e supponiamo che la prima di queste istruzioni, ossia **`beq x1, x0, 16`**, si trovi all'indirizzo $40$, e che l'istruzione **`lw x4, 100(x7)`** si trovi all'indirizzo $72$, rendendola così l'eventuale **destinazione del salto condizionato** della prima istruzione (nelle istruzioni di salto condizionato, l'offset è misurato in mezze parole, dove una mezza parola è pari a 2 byte). Possiamo visualizzare graficamente la corrispondente **pipeline di esecuzione** con il seguente diagramma:

![[diagramma_pipeline_piùcicli_esempio6.png]]

Come sappiamo, **l'istruzione di salto condizionato decide se saltare o meno nello stadio MEM**, corrispondente nell'esempio al quarto ciclo di clock: ciò implica, trovandoci in una pipeline, che nel mentre è stata avviata l'esecuzione di **altre tre istruzioni successive**, che potrebbero compromettere la sequenza di esecuzione o portare a comportamenti imprevisti se il salto venisse effettuato. Ci troviamo, dunque, di fronte a un **hazard sul controllo**. Sostanzialmente, **non esiste una situazione assolutamente efficace per risolvere gli hazard sul controllo**, essendo essi per natura almeno un minimo imprevedibili; per questo motivo, i metodi di risoluzione di questo tipo di hazard rappresentano più che altro delle **ottimizzazioni**, e le modifiche all'hardware sono relativamente semplici.

Un primo approccio, molto basilare e inefficiente, potrebbe essere **mettere in stallo la pipeline fino alla valutazione della condizione**; si tratta di un "rimedio" che rallenterebbe fin troppo la pipeline, e quindi da evitare. 

Una tecnica, invece, frequentemente utilizzata è quella di **predire che il salto non venga effettuato**: in questo modo, le istruzioni successive verrebbero comunque caricate nella pipeline, e nel caso in cui il salto venga effettuato, queste (che, a quel punto, si troveranno nelle fasi di IF, ID ed EX) verranno **scartate**, facendo ripartire l'esecuzione a partire dall'istruzione corrispondente all'indirizzo di destinazione del salto. Si tratta di un rimedio che, per quanto non completamente efficace, permette di **accelerare l'esecuzione in tutti i casi in cui il salto non viene effettuato**. 

Concretamente, per "scartare" le istruzioni, basterà **trasformarle in `nop` portando i segnali di controllo a $0$**, così come si è fatto per ottenere lo stallo nel caso degli [[La CPU#Come affrontare gli hazard sui dati?|hazard sui dati]]. La differenza è che non si effettuerà un **flush** solo di un'istruzione, ma di tre istruzioni che si trovano negli stadi IF, ID ed EX.

Un modo, poi, per **migliorare le prestazioni sui salti condizionati** consiste nell'**anticipare la decisione del salto stesso**. Per fare ciò, bisognerà anticipare due azioni all'interno della pipeline: il **calcolo dell'indirizzo di destinazione** e la **valutazione della condizione su cui si basa il salto**. La prima anticipazione è quella più facilmente realizzabile: infatti, il PC e l'immediato che andrà sommato ad esso sono disponibili già nel registro di pipeline IF/ID, e sarà dunque sufficiente **spostare il sommatore destinato al calcolo del nuovo indirizzo dallo stadio EX allo stadio ID**. 

La seconda anticipazione, invece, è più complessa. Nel caso in cui il salto in questione sia di tipo **`beq`**, o "**branch if equal**", si vuole confrontare il contenuto dei due registri letti nello stadio ID e verificare che il loro contenuto sia uguale. Questo test di uguaglianza, invece che con una sottrazione all'interno dell'ALU, può essere eseguito da un **comparatore** inserito tra i due contenuti letti dal register file: concretamente, ciò che fa il comparatore è dapprima uno [[Porte logiche#Porte logiche a più input *AND*, *OR*, *NAND*, *NOR*, *XOR* e *XNOR*|XOR]] bit a bit del contenuto dei due registri, e in seguito un OR sull'output dei vari XOR effettuati (se l'output dell'OR è $0$, allora i due registri confrontati sono uguali). 

Tuttavia, spostare questo confronto nello stadio ID implica l'aggiunta di **altra logica di propagazione e di rilevamento degli hazard**. Infatti, ci sono principalmente **due complicazioni** con questo approccio:
1. durante lo stadio ID si deve decodificare l'istruzione, decidere se occorre propagare gli operandi all'ingresso del comparatore e valutare l'uguaglianza, in modo che si possa scrivere nel PC l'indirizzo di destinazione del salto se questo deve avvenire; ciò rende necessaria l'aggiunta di **ulteriore logica di propagazione**;
2. poiché i dati su cui fare il confronto sono richiesti già nello stadio ID, ma potrebbero eventualmente essere prodotti più avanti nella pipeline, è possibile che si verifichi un **hazard sui dati**, e che diventi necessario introdurre uno **stallo**; ciò avverrebbe, ad esempio, se il dato letto dalla memoria da un'istruzione di load è uno degli operandi di un'istruzione di salto condizionato immediatamente successiva (in questo caso, sarebbe necessario introdurre uno stallo di due cicli di clock).

Nonostante queste complicazioni, le anticipazioni effettuate rappresentano effettivamente un miglioramento, poiché riducono universalmente a **una sola istruzione** (quella che si trova nello stadio IF) l'eventuale **scarto di un'istruzione di salto condizionato**. Per scartare quest'istruzione, invece di azzerare i vari segnali di controllo, possiamo direttamente **aggiungere un segnale di controllo `IF.Flush`**, che va ad **azzerare il campo `IF/ID.Istruzione`**, ossia l'istruzione scritta nel registro di pipeline IF/ID, rendendola così concretamente una `nop`.

Con le apposite aggiunte, e reinserendo la logica implementata per affrontare gli hazard sui dati, ora la nostra unità di elaborazione può essere schematizzata nel modo seguente (per semplicità, è stata omessa un'ulteriore unità di propagazione, così come altri dettagli):

![[cpu_pipeline_forwarding_efficientbeq.png]]

Quella vista finora rappresenta una **"forma base" di predizione del salto**: si effettua sempre una stessa supposizione, e nel caso essa si riveli corretta bene, altrimenti si scartano le istruzioni contenute nella pipeline. Per una semplice pipeline a cinque stadi come quella analizzata finora, questo approccio risulta sufficientemente adeguato; lo stesso non si può dire, tuttavia, contestualmente a pipeline più profonde, dove il costo dei salti condizionati, in termini di cicli di clock e, di conseguenza, anche di istruzioni scartate, aumenta.

A costo di aumentare l'hardware a disposizione, è possibile effettuare una **predizione dinamica dell'esito dei salti** durante l'esecuzione stessa del programma, in modo da variare di volta in volta le previsioni e ottenendo, così, un'efficienza maggiore. Un possibile approccio a riguardo consiste nel **verificare se, l'ultima volta che un'istruzione di salto condizionato è stata eseguita, tale salto sia stato effettivamente effettuato**: in caso positivo, si assume che il salto verrà effettuato anche stavolta, e vengono quindi caricate le istruzioni a partire da quella presente all'indirizzo di destinazione; altrimenti, si assume che il salto non verrà effettuato, e quindi vengono caricate le istruzioni successive.

Un modo per implementare questa strategia è l'utilizzo di un "**buffer di predizione dei salti**", detto anche "**branch prediction buffer**" o "**tabella della storia dei salti**": si tratta di una **piccola memoria**, indicizzata attraverso la parte inferiore dell'indirizzo dell'istruzione di branch, che contiene **un bit che indica se il salto è stato effettuato o meno nell'ultima esecuzione**. Questa rappresenta la versione più semplice e banale realizzabile, ma aumentando la capacità di questo buffer anche solo a **due bit**, è possibile effettuare **previsioni più accurate** in alcuni contesti, ad esempio nei cicli a forte prevalenza di uno specifico tipo di scelta. Nel caso in cui si adoperino due bit per il buffer di predizione dei salti, la **scelta della previsione in base ai salti precedenti** può essere rappresentata come una **[[FSM]]**:

![[fsm_predizione_dinamica_branch.png]]

Un buffer di predizione dei salti può essere realizzato come un **piccolo buffer speciale**, accessibile tramite l'indirizzo dell'istruzione **durante lo stadio IF** della pipeline.

[SALTO RITARDATO: 16, slide 18/21]
___
## Eccezioni

Come si potrebbe immaginare, la **control unit** di un processore è la parte più complessa da far funzionare correttamente ed efficientemente. Oltre alle sfide palesi, derivate dal coordinamento dell'esecuzione di più istruzioni in una pipeline, una delle difficoltà maggiori è rappresentata dalla gestione delle "**eccezioni**" e degli "**interrupt**", eventi che alterano il normale flusso sequenziale di esecuzione delle istruzioni (ma diversi dai salti).

In varie architetture, non si fa una vera e propria distinzione tra eccezioni ed interrupt, tuttavia ciò non vale solitamente per l'architettura RISC-V, che è quella che trattiamo in questo corso. Qui, si utilizzerà il termine "**eccezione**" per indicare **qualsiasi cambiamento non previsto dal flusso di controllo**, indipendentemente dalla sua natura, e il termine "**interrupt**" per indicare esclusivamente **un cambiamento con cause esterne**. Di seguito, una tabella che riassume la maggior parte di questi eventi imprevisti, categorizzandoli opportunamente:

![[eccezioni_interrupt_tabella.png]]

[pag. 295/300 - 17, slide 10/19]
___
