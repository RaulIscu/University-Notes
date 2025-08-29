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
- l'**execute** (**EXE**), che coinvolge principalmente l'**ALU**;
- eventualmente il **memory access** (**MEM**), che coinvolge principalmente la **memoria di dati**;
- eventualmente il **write back** (**WB**), che coinvolge principalmente il **register file**.

Di conseguenza, possiamo affermare che la pipeline dell'architettura RISC-V ha **5 stadi**, e il tempo di esecuzione di ciascuno di essi dipende dal tempo di esecuzione delle **singole operazioni delle unità funzionali**; in particolare, possiamo assumere i seguenti valori di tempo:
- l'**IF**, dunque la lettura dell'istruzione, dura $200\,\,ps$;
- l'**ID**, dunque la decodifica dell'istruzione e la lettura dei registri, dura $100\,\,ps$;
- l'**EXE**, dunque un'operazione dell'ALU, dura $200\,\,ps$;
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

In realtà, gli hazard sui dati sono una **criticità molto comune**, che potrebbero portare a diversi stalli e quindi a un rallentamento considerevole del processore. Un primo approccio per limitare quest'impatto potrebbe essere affidarsi a dei **compilatori**, che effettuino delle ottimizzazioni della serie di istruzioni, tuttavia essi hanno un potere limitato e non sufficiente a risolvere il problema. La soluzione più utilizzata, invece, è basata sull'osservazione che, in realtà, **spesso non è necessario che termini l'esecuzione di un'istruzione per risolvere un hazard sui dati**: ad esempio, nella situazione proposta poco fa, si potrebbe utilizzare il risultato della somma tra `x2` e `x3` non appena esso viene restituito dall'ALU, senza attendere che esso venga scritto in `x1` e poi letto da quest'ultimo. La tecnica che prevede l'aggiunta di un **circuito che fornisca**, in un certo punto dell'esecuzione, **il dato mancante propagandolo da una risorsa interna** è detta "**propagazione**", o "**bypass**".

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


___

[pag. 260...]
[pag. 24 - 34 "Prestazioni"]
