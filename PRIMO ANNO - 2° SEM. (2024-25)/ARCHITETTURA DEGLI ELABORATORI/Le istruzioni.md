## Cos'è un'istruzione?

Per poter comunicare con un [[Il calcolatore|calcolatore]] e impartirgli dei comandi, bisogna parlare nel suo "linguaggio", utilizzando un particolare **insieme di istruzioni**, o "**instruction set**", che possiamo vedere come una sorta di vocabolario, dove una singola **istruzione** è una parola.

Si potrebbe pensare che i linguaggi dei calcolatori siano molti e diversi tra loro, ma in realtà risultano essere tutti relativamente simili, perciò impararne anche uno solo costituisce un grande passo verso la comprensione di tutti gli altri. Il linguaggio analizzato in questo corso è il **RISC-V**, sviluppato all'università di Berkeley a partire dal **2010**.

La somiglianza tra i vari insiemi di istruzioni è dovuta al fatto che tutti i calcolatori sono costruiti a partire dai medesimi principi fondamentali, e dalle stesse componenti hardware di base, oltre che al fatto che un qualsiasi calcolatore debba saper svolgere almeno alcune operazioni di base sempre costanti.
___
## Le istruzioni dell'architettura RISC-V

Le principali **istruzioni definite per l'architettura RISC-V** possono essere divise nelle seguenti categorie:
- istruzioni **aritmetiche**;
- istruzioni di **trasferimento dati**;
- istruzioni **logiche**;
- istruzioni di **scorrimento**;
- istruzioni di **salto condizionato**;
- istruzioni di **salto incondizionato**.

Di seguito, verranno analizzate categoria per categoria, elencando le principiali istruzioni appartenenti a ciascuna categoria e illustrandone il funzionamento. 

##### Istruzioni aritmetiche

Le principali **istruzioni aritmetiche** previste dall'architettura RISC-V sono le seguenti:
- **`add rd, rs1, rs2`**;
- **`addi rd, rs1, 10`**;
- **`sub rd, rs1, rs2`**.

L'istruzione **`add`** corrisponde alla **somma** tra i valori nei registri `rs1` e `rs2`, andando poi a memorizzare il risultato nel registro `rd`.

L'istruzione **`addi`** corrisponde sempre a una somma, ma più in particolare a una **somma in cui è coinvolta una costante** (nell'esempio, vengono sommati il valore memorizzato in `rs1` e la costante $10$); anche in questo caso, il risultato viene memorizzato nel registro `rd`.

L'istruzione **`sub`** corrisponde, infine, alla **sottrazione** tra i valori nei registri `rs1` e `rs2`, andando poi a memorizzare il risultato nel registro `rd`.
___
##### Istruzioni di trasferimento dati

Le principali **istruzioni di trasferimento dati** previste dall'architettura RISC-V sono le seguenti:
- **`lw rd, 40(rs3)`**;
- **`lwu rd, 40(rs3)`**;
- **`sw rs1, 40(rs3)`**;
- **`lh rd, 40(rs3)`**;
- **`lhu rd, 40(rs3)`**;
- **`sh rs1, 40(rs3)`**;
- **`lb rd, 40(rs3)`**;
- **`lbu rd, 40(rs3)`**;
- **`sb rs1, 40(rs3)`**;
- **`lr.d rd, (rs3)`**;
- **`sc.d rs1, rs2, (rs3)`**;
- **`lui rd, 0x12345`**.

L'istruzione **`lw`** consiste nella **lettura di una parola** di memoria, e al suo spostamento in un registro. Invece, l'istruzione **`lwu`** consiste nella **lettura di una parola senza segno** della memoria, e al suo spostamento in un registro. L'istruzione **`sw`**, poi, consiste nella **memorizzazione di una parola**, ossia nello spostamento di essa da un registro (nell'esempio, `rs1`) a un indirizzo in memoria (nell'esempio, `rs3 + 40`).

L'istruzione **`lh`** consiste nella **lettura di una mezza parola** di memoria, e al suo spostamento in un registro. Invece, l'istruzione **`lhu`** consiste nella **lettura di una mezza parola senza segno** della memoria, e al suo spostamento in un registro. L'istruzione **`sh`**, poi, consiste nella **memorizzazione di una mezza parola**, ossia nello spostamento di essa da un registro (nell'esempio, `rs1`) a un indirizzo in memoria (nell'esempio, `rs3 + 40`).

L'istruzione **`lb`** consiste nella **lettura di un byte** di memoria, e al suo spostamento in un registro. Invece, l'istruzione **`lbu`** consiste nella **lettura di un byte senza segno** della memoria, e al suo spostamento in un registro. L'istruzione **`sb`**, poi, consiste nella **memorizzazione di un byte**, ossia nello spostamento di esso da un registro (nell'esempio, `rs1`) a un indirizzo in memoria (nell'esempio, `rs3 + 40`).

[ISTRUZIONI LR.D E SC.D]

L'istruzione **`lui`** consiste nel **caricamento nel registro `rd` dei 20 bit più significativi di una costante**, inserendoli nei 20 bit più significativi (dall'indice $12$ all'indice $31$) del registro in questione, e riempiendo i restanti 12 bit meno significativi (dall'indice $0$ all'indice $11$) con degli zeri. 

Nell'utilizzo di molte delle istruzioni di trasferimento dati, si utilizza il valore contenuto in un determinato registro come "**indirizzo di base**", e gli viene sommata una costante di "**offset**": la somma tra questi due valori consisterà tendenzialmente nell'indirizzo di memoria a cui accedere per eseguire l'istruzione in questione. Ad esempio, nell'esempio di `lw`, si legge la parola contenuta in memoria all'indirizzo `rs3 + 40`, e la si sposta nel registro `rd`.
___
##### Istruzioni logiche

Le principali **istruzioni logiche** previste dall'architettura RISC-V sono le seguenti:
- **`and rd, rs1, rs2`**;
- **`andi rd, rs1, 0b10101010`**;
- **`or rd, rs1, rs2`**;
- **`ori rd, rs1, 0b10101010`**;
- **`xor rd, rs1, rs2`**;
- **`xori rd, rs1, 0b10101010`**.

È importante ricordare che, nel linguaggio assembly dell'architettura RISC-V, le istruzioni logiche eseguono le loro rispettive operazioni **bit a bit**: ad esempio, dato `rs1 = 0b11001100` e `rs2 = 0b10101010`, si avrà che `and rd, rs1, rs2` porterà a memorizzare in `rd` il valore `0b10001000`.

L'istruzione **`and`** restituisce l'AND bit a bit tra i due registri `rs1` e `rs2`, e ne memorizza il risultato in `rd`. L'istruzione **`andi`**, invece, restituisce l'AND bit a bit tra il registro `rs1` e una costante (nell'esempio, `0b10101010`).

L'istruzione **`or`** restituisce l'OR bit a bit tra i due registri `rs1` e `rs2`, e ne memorizza il risultato in `rd`. L'istruzione **`ori`**, invece, restituisce l'OR bit a bit tra il registro `rs1` e una costante (nell'esempio, `0b10101010`).

L'istruzione **`xor`** restituisce lo XOR bit a bit tra i due registri `rs1` e `rs2`, e ne memorizza il risultato in `rd`. L'istruzione **`xori`**, invece, restituisce lo XOR bit a bit tra il registro `rs1` e una costante (nell'esempio, `0b10101010`).
___
##### Istruzioni di scorrimento

Le principali **istruzioni di scorrimento** previste dall'architettura RISC-V sono le seguenti:
- **`sll rd, rs1, rs2`**;
- **`slli rd, rs1, 2`**;
- **`srl rd, rs1, rs2`**;
- **`srli rd, rs1, 2`**;
- **`sra rd, rs1, rs2`**;
- **`srai rd, rs1, 2`**.

L'istruzione **`sll`** consiste nello **scorrimento** (o **shift**) **a sinistra** del valore nel registro `rs1` di un numero di posizioni specificato nei 5 bit meno significativi di `rs2`, e memorizza il risultato in `rd` (riempiendo con zeri a destra). Invece, l'istruzione **`slli`** funziona allo stesso modo ma con il numero di posizioni specificato da una **costante** (nell'esempio, $2$ posizioni).

L'istruzione **`srl`** consiste nello **scorrimento** (o **shift**) **a destra** del valore nel registro `rs1` di un numero di posizioni specificato nei 5 bit meno significativi di `rs2`, e memorizza il risultato in `rd` (riempiendo con zeri a sinistra). Invece, l'istruzione **`slli`** funziona allo stesso modo ma con il numero di posizioni specificato da una **costante** (nell'esempio, $2$ posizioni).

L'istruzione **`sra`** consiste nello **scorrimento** (o **shift**) **aritmetico a destra** del valore nel registro `rs1` di un numero di posizioni specificato nei 5 bit meno significativi di `rs2`, e memorizza il risultato in `rd` (riempiendo con bit di segno a sinistra). Invece, l'istruzione **`srai`** funziona allo stesso modo ma con il numero di posizioni specificato da una **costante** (nell'esempio, $2$ posizioni). Questa coppia di istruzioni viene tendenzialmente utilizzata quando si lavora con **valori negativi**.
___
##### Istruzioni di salto condizionato

Le principali **istruzioni di salto condizionato** previste dall'architettura RISC-V sono le seguenti:
- **`beq rs1, rs2, 100`**;
- **`bne rs1, rs2, 100`**;
- **`blt rs1, rs2, 100`**;
- **`bltu rs1, rs2, 100`**;
- **`bge rs1, rs2, 100`**;
- **`bgeu rs1, rs2, 100`**.

Possiamo generalizzare queste 6 istruzioni nella formula **`inst rs1, rs2, offset`**, dove `inst` rappresenta la particolare condizione che deve venire valutata, `rs1` e `rs2` rappresentano i due registri da confrontare, e `offset` rappresenta lo **spostamento** (in byte) **relativo al PC** (Program Counter), per calcolare così l'indirizzo a cui saltare.

Vediamo ora, che condizione vanno a valutare le varie singole istruzioni:
- **`beq`** controlla se `rs1` e `rs2` sono uguali, e in tal caso salta all'indirizzo desiderato;
- **`bne`** controlla se `rs1` e `rs2` sono diversi, e in tal caso salta all'indirizzo desiderato;
- **`blt`** controlla se `rs1` è minore di `rs2` (tenendo conto del segno), e in tal caso salta all'indirizzo desiderato;
- **`bltu`** controlla se `rs1` è minore di `rs2` (senza considerare il segno), e in tal caso salta all'indirizzo desiderato;
- **`bge`** controlla se `rs1` è maggiore o uguale di `rs2` (tenendo conto del segno), e in tal caso salta all'indirizzo desiderato;
- **`bgeu`** controlla se `rs1` è maggiore o uguale di `rs2` (senza considerare il segno), e in tal caso salta all'indirizzo desiderato;

[SLT E SLTI]
___
##### Istruzioni di salto incondizionato

Le principali **istruzioni di salto incondizionato** previste dall'architettura RISC-V sono le seguenti:
- **`jal rd, 100`**;
- **`jalr rd, 100(rs1)`**.

L'istruzione **`jal`** ("jump and link") va a salvare nel registro `rd` l'indirizzo dell'istruzione successiva ad essa, dunque `PC + 4`, e in seguito salta all'istruzione che si trova all'indirizzo `PC + offset`, dove `offset` è la costante inserita espressa in byte (nell'esempio, $100$).

L'istruzione **`jalr`** ("jump and link register") funziona sostanzialmente allo stesso modo dell'istruzione appena spiegata, con la differenza che, invece di saltare a `PC + offset`, si salta all'indirizzo dato da `rs1 + offset`.
___
## Come vengono rappresentate le istruzioni nel calcolatore?

Abbiamo appena visto la maggioranza delle istruzioni più importanti previste per l'architettura RISC-V. Tuttavia, seppur esse siano evidentemente di più basso livello rispetto a quelle di linguaggi come Java o Python, vi è comunque un certo livello di astrazione rispetto a ciò che il calcolatore legge concretamente quando incontra un'istruzione. Vediamo, quindi, **come un'istruzione viene tradotta dal linguaggio assembly al linguaggio macchina** per essere letta ed eseguita dal calcolatore.

A livello di base, le varie componenti di un'istruzione (dette anche **campi**, o "**fields**", dell'istruzione) vengono memorizzate come **numeri**, e dunque una singola istruzione può essere memorizzata e visualizzata come una **sequenza di numeri** disposti uno dopo l'altro. Ad esempio, analizziamo la seguente istruzione:

```
add x9, x20, x21
```

che indica al calcolatore di sommare i valori presenti nei registri `x20` e `x21` e di memorizzare il risultato di tale operazione nel registro `x9`. Tale istruzione astratta viene codificata nella seguente sequenza di 32 bit:

```
0000000 10101 10100 000 01001 0110011
```

Vediamo cosa viene indicato da ciascuno dei 6 campi in cui è divisa la sequenza di bit. La combinazione del primo, del quarto e del sesto campo (dunque, la combinazione dei numeri decimali $0$, $0$ e $51$) indica al processore che l'istruzione in questione è una **somma**; il secondo campo indica, invece, il numero del **registro del primo operando**, così come il terzo campo indica il numero del **registro del secondo operando**; infine, il quinto campo indica il numero del **registro dove memorizzare il risultato**.

Come si può notare, l'istruzione appena analizzata, così come qualsiasi istruzione RISC-V, **richiede esattamente 32 bit**, o **una parola**, di memoria.

Questa scomposizione di un'istruzione in campi è definita "**formato**" dell'istruzione. Per rendere più facile la trattazione, ai diversi campi di un'istruzione RISC-V viene associato un nome; nel caso del formato appena analizzato, questi nomi sono:
- **`codop`** per il sesto campo, lungo 7 bit;
- **`rd`** per il quinto campo, lungo 5 bit;
- **`funz3`** per il quarto campo, lungo 3 bit;
- **`rs1`** e **`rs2`** per il terzo e secondo campo, lunghi 5 bit ciascuno;
- **`funz7`** per il primo campo, lungo 7 bit.

Il **`codop`**, chiamato anche "**codice operativo**", è il numero che codifica l'operazione base dell'istruzione in questione (in questo caso, la somma); oltre al `codop` in sé, i campi **`funz3`** e **`funz7`** forniscono ulteriori informazioni aggiuntive. I campi **`rs1`** e **`rs2`**, invece, contengono il numero associato ai due registri che contengono i due **operandi** dell'operazione (in questo caso, `x20` e `x21`). Infine, il campo **`rd`** contiene il numero associato al registro che conterrà il **risultato** dell'operazione (in questo caso, `x9`). Si noti come i campi destinati ai registri sono lunghi esattamente **5 bit**, dato che l'architettura RISC-V prevede 32 registri e 5 bit possono codificare esattamente 32 numeri distinti (da $0$ a $31$).

Tuttavia, questo **non è un formato valido universalmente per tutte le istruzioni** dell'architettura RISC-V, in quanto non ricopre in maniera efficiente tutte le situazioni in cui operano quest'ultime. Ad esempio, nell'utilizzo dell'istruzione `lw` sono richiesti 2 registri e una costante (l'offset), tuttavia mantenere il formato appena analizzato limiterebbe la costante a un valore massimo di $31$. Per ovviare a questa problematica, si è deciso di mantenere la lunghezza fissa di 32 bit per ogni istruzione, ma di **predisporre diversi formati** per diversi tipi di istruzione; i principali sono:
- il formato di **tipo R**;
- il formato di **tipo I**;
- il formato di **tipo S**;
- il formato di **tipo SB**;
- il formato di **tipo U**.

Quello dell'esempio è un formato di tipo R (R sta per "register"), la cui disposizione dei campi può essere schematizzata così:

![[formato_r.png]]

Analizziamo, invece, il formato di **tipo I** (I sta per "immediate"). Tale formato viene utilizzato, come suggerisce il nome, dalle **istruzioni aritmetiche in cui un operando è una costante**, ma anche dalle **istruzioni di trasferimento dati dalla memoria**. In questo caso, i campi di un'istruzione di tipo I sono divisi nel seguente modo:
- i primi 12 bit vengono chiamati **`imm[11:0]`**, o **immediato**;
- i successivi 5 bit vengono chiamati **`rs1`**;
- i successivi 3 bit vengono chiamati **`funz3`**;
- i successivi 5 bit vengono chiamati **`rd`**;
- i successivi 7 bit vengono chiamati **`codop`**.

Possiamo schematizzare la disposizione dei campi del formato di tipo I così:

![[formato_i.png]]

Similmente alle istruzioni di tipo R, anche in questo caso troviamo i campi `codop`, `rd`, `funz3` e `rs1`, situati nella stessa posizione e aventi lo stesso scopo. Ciò che cambia è la sostituzione dei 7 bit di `funz7` e dei 5 bit di `rs2` con 12 bit di `imm[11:0]`, che vanno a contenere una **costante**, interpretata in complemento a 2 e che può, perciò, rappresentare un qualsiasi intero dell'intervallo $[-2^{11}, 2^{11} - 1]$.

Poi, vediamo il formato di **tipo S** (S sta per "store"), utilizzato dalle **istruzioni di trasferimento dati nella memoria**, che necessitano di due registri-sorgente (uno per l'indirizzo base e un altro per il dato da memorizzare) e di una costante (l'offset rispetto all'indirizzo base). In questo caso, i campi di un'istruzione di tipo S sono divisi nel seguente modo:
- i primi 7 bit vengono chiamati **`imm[11:5]`**;
- i successivi 5 bit vengono chiamati **`rs2`**;
- i successivi 5 bit vengono chiamati **`rs1`**;
- i successivi 3 bit vengono chiamati **`funz3`**;
- i successivi 5 bit vengono chiamati **`imm[4:0]`**;
- i successivi 7 bit vengono chiamati **`codop`**.

Possiamo schematizzare la disposizione dei campi del formato di tipo S così:

![[formato_s.png]]

Anche in questo caso, i campi `codop` e `funz3` rimangono invariati, e affianco a `rs1` ritorna `rs2`, che presentano anch'essi posizioni invariate. La particolarità di questo formato sta nella **suddivisione dei bit dell'immediato**, diviso tra i primi 7 bit (quelli più significativi) e i 5 bit compresi tra `funz3` e `codop` (quelli meno significativi). Questa particolare scelta architetturale è stata fatta per semplicità, in quanto permette di **mantenere invariate le posizioni dei campi `rs2` e `rs1`** (quando presenti).

[TODO: formato di tipo SB]

Possiamo schematizzare la disposizione dei campi del formato di tipo SB così:

![[formato_sb.png]]

[TODO: spiegazione campi di formato di tipo SB]

Infine, analizziamo il formato di **tipo U**, utilizzato soprattutto da **istruzioni di trasferimento di costanti di grandi dimensioni in un registro**, che necessitano di un registro-destinazione e di una costante. In questo caso, i campi di un'istruzione di tipo U sono divisi nel seguente modo:
- i primi 20 bit vengono chiamati **`imm[19:0]`**;
- i successivi 5 bit vengono chiamati **`rd`**;
- i successivi 7 bit vengono chiamati **`codop`**.

Possiamo schematizzare la disposizione dei campi del formato di tipo U così:

[PIC: schema dei campi di un'istruzione di formato di tipo U]

Qui, l'unico campo a rimanere invariato è `codop`, mentre ritorna il campo `rd`, nella stessa posizione che assumeva nei formati di tipo R e di tipo I; i primi 20 bit, invece, vengono occupati dal campo `imm[19:0]`, contenente proprio i 20 bit che verranno inseriti come bit più significativi del registro indicato da `rd`.

In generale, possiamo riassumere alcune **caratteristiche comuni o ricorrenti** dell'organizzazione dei campi di questi formati, che potranno tornare utili in fase di progettazione. In particolare:
- il campo **`codop`** è sempre contenuto nei **7 bit meno significativi** dell'istruzione, e a seconda del formato, **i campi `funz3` e `funz7` forniscono informazioni aggiuntive** sull'operazione da svolgere;
- il primo registro operando, ossia **`rs1`**, quando presente è sempre contenuto nei **bit nelle posizioni dalla $19$ alla $15$**;
- il secondo registro operando, ossia **`rs2`**, quando presente è sempre contenuto nei **bit nelle posizioni dalla $24$ alla $20$**;
- il registro di destinazione, ossia **`rd`**, quando presente è sempre contenuto nei **bit nelle posizioni dalla $11$ alla $7$**.

Di seguito, una **tabella riassuntiva** dell'organizzazione dei campi per i vari formati di istruzione (è stato omesso il formato U):

![[formati_istruzioni_tabella.png]]

La distinzione tra formati può essere facilmente svolta dall'hardware, al momento dell'esecuzione dell'istruzione, in base al valore contenuto in `codop`. Istruzioni come `add`, `sub`, `and`, `or` e `xor` utilizzano il formato di tipo R; istruzioni come `addi`, `lw`, `slli`, `srli`, `andi`, `ori` e `xori` rientrano invece nel formato di tipo I; istruzioni come `sw` vengono codificate in un formato di tipo S; infine, istruzioni come `lui` vengono codificate in un formato di tipo U. Per completezza, di seguito una tabella con la **maggior parte delle istruzioni dell'architettura RISC-V**, con annesso per ciascuna di esse il corrispettivo **formato**:

![[formati_istruzioni_tabella1.png]]
___
## Procedure

Le **procedure**, dette anche **funzioni**, costituiscono uno degli strumenti più comunemente utilizzati nella scrittura e organizzazione di un programma, con lo scopo principale di rendere il **codice più leggibile e riutilizzabile**. La creazione di procedure consente ai programmatori di concentrarsi su una parte del problema alla volta, e l'interfaccia tra una determinata procedura e il resto del programma è costituita dai **parametri**, utilizzati per fornire dei valori ben precisi alla procedura e per restituirne altri al programma chiamante.

Per l'esecuzione di una procedura, il programma deve eseguire principalmente **6 passi**:
- posizionare i parametri in un luogo di memoria accessibile dalla procedura;
- trasferire il controllo dell'esecuzione alla procedura;
- acquisire le risorse necessarie all'esecuzione della procedura;
- eseguire il compito previsto;
- posizionare i risultati in un luogo di memoria accessibile dal programma chiamante;
- restituire il controllo dell'esecuzione al programma chiamante.

Naturalmente, i **registri** costituiscono il luogo che consente l'accesso più rapido ai dati, dunque soprattutto nel contesto di una procedura conviene utilizzarli il più possibile. In particolare, nell'architettura RISC-V, ci sono delle **convenzioni riguardanti l'utilizzo dei registri** in relazione a una procedura:
- gli 8 registri **da `x10` a `x17`** vengono utilizzati per contenere i parametri in "**input**" e per restituire i valori calcolati come "**output**";
- il registro **`x1`** viene utilizzato per contenere l'**indirizzo di ritorno** per tornare al punto d'origine, ossia al punto del programma dove è stata chiamata la procedura.

È proprio nell'utilizzo delle procedure che entrano in gioco le **[[Le istruzioni#Istruzioni di salto incondizionato|istruzioni di salto incondizionato]]**. Ad esempio, l'istruzione `jal x1, IndirizzoProcedura` (dove `IndirizzoProcedura` rappresenta l'etichetta corrispondente alla procedura in questione), che porta alla conservazione dell'indirizzo di ritorno in `x1` e al salto dell'esecuzione del programma a `IndirizzoProcedura`, è l'istruzione comunemente utilizzata per avviare una determinata procedura nel programma. Similmente, l'istruzione `jalr x0, 0(x1)`, che salta l'esecuzione del programma all'indirizzo contenuto in `x1` e non si cura dell'indirizzo di ritorno (il registro `x0` contiene sempre il valore $0$, quindi non andrà a conservare nient'altro), viene utilizzata all'interno del corpo di una procedura per restituire il controllo al programma chiamante.

Risulta evidente, ad esempio nel concetto stesso di "indirizzo di ritorno", la necessità di memorizzare in un registro specifico l'indirizzo dell'istruzione in esecuzione. Questo registro viene chiamato "**program counter**", o più semplicemente **PC**. Dato che nell'architettura RISC-V la memoria è indirizzata al byte, e che ogni istruzione in tale architettura è lunga esattamente 32 bit, ossia 4 byte, di default il PC viene incrementato di 4 ad ogni istruzione che viene eseguita. L'istruzione `jal`, salvando in `x1` l'indirizzo di ritorno, salva in realtà l'indirizzo `PC + 4`, ossia l'indirizzo dell'istruzione successiva a quella appena eseguita.

##### Utilizzo di molti registri in una procedura: lo stack

In alcuni casi, all'interno di una procedura sarà necessario un numero di registri maggiore rispetto agli 8 convenzionalmente destinati come parametri; questo bisogno, abbinato con la necessità di ripristinare i valori dei registri utilizzati a quelli precedenti alla chiamata della procedura una volta terminata la sua esecuzione, porta al dover **copiare il contenuti dei registri in memoria**, per poter essere ritrasferiti al loro posto in seguito.

La struttura dati ideale per permettere questo tipo di operazione è lo **stack**, detto anche **pila**, definibile come una **coda del tipo "last-in-first-out"**, o "**LIFO**". Per poter utilizzare efficientemente lo stack, è necessario avere a disposizione l'**indirizzo dell'ultimo dato introdotto** nello stack, per sapere dove possa essere salvato il contenuto del registro successivo o da dove recuperare il vecchio valore di un registro: tale indirizzo viene detto "**stack pointer**", e nell'architettura RISC-V viene convenzionalmente conservato nel registro **`x2`**, detto anche **`sp`**. Inoltre, possiamo definire "**push**" l'operazione di **inserimento nello stack** di un determinato dato, e "**pop**" l'operazione di **estrazione dallo stack** di un determinato dato. Per natura stessa dello stack (last-in-first-out), esso va a "crescere" a partire da indirizzi di memoria più alti verso indirizzi più bassi: perciò, **quando vengono inseriti dati, lo stack pointer diminuisce** e, viceversa, **quando vengono estratti dati, lo stack pointer aumenta**. Essendo la memoria contenuta in un registro pari a 32 bit, ossia 4 byte o 1 word, convenzionalmente lo stack pointer diminuirà o aumenterà sempre di 4.

Stabilito che possono esserci dei registri con valori da preservare nel caso in cui venga chiamata una procedura, vediamo ora delle **ulteriori convenzioni** che riguardano proprio questa caratteristica:
- i registri **da `x5` a `x7`** e **da `x28` a `x31`** sono considerati a tutti gli effetti **registri temporanei**, il cui contenuto non è necessariamente preservato nello stack in caso di chiamata a procedura;
- i registri **`x8`**, **`x9`** e **da `x18` a `x27`** sono considerati **registri da preservare** in caso di chiamata a procedura (ovviamente, solo nel caso in cui quest'ultima li vada a utilizzare).
___
## Pseudoistruzioni

[pag. 115]
___