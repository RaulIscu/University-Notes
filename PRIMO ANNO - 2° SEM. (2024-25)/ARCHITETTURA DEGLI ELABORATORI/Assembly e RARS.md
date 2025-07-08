### Istruzioni aritmetiche

Le principali **istruzioni aritmetiche** previste dall'[[L'architettura RISC-V#L'architettura RISC-V|architettura RISC-V]] sono le seguenti:
- **`add rd, rs1, rs2`**;
- **`addi rd, rs1, 10`**;
- **`sub rd, rs1, rs2`**.

L'istruzione **`add`** corrisponde alla **somma** tra i valori nei registri `rs1` e `rs2`, andando poi a memorizzare il risultato nel registro `rd`.

L'istruzione **`addi`** corrisponde sempre a una somma, ma più in particolare a una **somma in cui è coinvolta una costante** (nell'esempio, vengono sommati il valore memorizzato in `rs1` e la costante $10$); anche in questo caso, il risultato viene memorizzato nel registro `rd`.

L'istruzione **`sub`** corrisponde, infine, alla **sottrazione** tra i valori nei registri `rs1` e `rs2`, andando poi a memorizzare il risultato nel registro `rd`.

[MUL E DIV]
___
### Istruzioni di trasferimento dati

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

[ISTRUZIONE LUI]

Nell'utilizzo di molte delle istruzioni di trasferimento dati, si utilizza il valore contenuto in un determinato registro come "**indirizzo di base**", e gli viene sommata una costante di "**offset**": la somma tra questi due valori consisterà tendenzialmente nell'indirizzo di memoria a cui accedere per eseguire l'istruzione in questione. Ad esempio, nell'esempio di `lw`, si legge la parola contenuta in memoria all'indirizzo `rs3 + 40`, e la si sposta nel registro `rd`.
___
### Istruzioni logiche

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
### Istruzioni di scorrimento

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
### Istruzioni di salto condizionato

Le principali **istruzioni di salto condizionato** previste dall'architettura RISC-V sono le seguenti:
- **`beq rs1, rs2, 100`**;
- **`bne rs1, rs2, 100`**;
- **`blt rs1, rs2, 100`**;
- **`bltu rs1, rs2, 100`**;
- **`bge rs1, rs2, 100`**;
- **`bgeu rs1, rs2, 100`**.

Possiamo generalizzare queste 6 istruzioni nella formula **`inst rs1, rs2, offset`**, dove `inst` rappresenta la particolare condizione che deve venire valutata, `rs1` e `rs2` rappresentano i due registri da confrontare, e `offset` rappresenta lo **spostamento** (in byte) **relativo al PC** (Program Counter), per calcolare così l'indirizzo a cui saltare.

Analizziamo meglio questa caratteristica. Il PC, o Program Counter, è un registro speciale del processore, che contiene dinamicamente l'indirizzo della prossima istruzione da eseguire; nell'architettura RISC-V, ogni istruzione è lunga 4 byte, quindi di default il PC viene aumentato sempre di 4. Nel caso delle istruzioni di salto condizionato, quindi, aggiungere l'`offset` al PC porta a cambiare il flusso di esecuzione, e a saltare ad altre istruzioni.

Vediamo ora, che condizione vanno a valutare le varie singole istruzioni:
- **`beq`** controlla se `rs1` e `rs2` sono uguali, e in tal caso salta all'indirizzo desiderato;
- **`bne`** controlla se `rs1` e `rs2` sono diversi, e in tal caso salta all'indirizzo desiderato;
- **`blt`** controlla se `rs1` è minore di `rs2` (tenendo conto del segno), e in tal caso salta all'indirizzo desiderato;
- **`bltu`** controlla se `rs1` è minore di `rs2` (senza considerare il segno), e in tal caso salta all'indirizzo desiderato;
- **`bge`** controlla se `rs1` è maggiore o uguale di `rs2` (tenendo conto del segno), e in tal caso salta all'indirizzo desiderato;
- **`bgeu`** controlla se `rs1` è maggiore o uguale di `rs2` (senza considerare il segno), e in tal caso salta all'indirizzo desiderato;

[SLT E SLTI]
___
### Istruzioni di salto incondizionato

Le principali **istruzioni di salto incondizionato** previste dall'architettura RISC-V sono le seguenti:
- **`jal rd, 100`**;
- **`jalr rd, 100(rs1)`**.

L'istruzione **`jal`** ("jump and link") va a salvare nel registro `rd` l'indirizzo dell'istruzione successiva ad essa, dunque `PC + 4`, e in seguito salta all'istruzione che si trova all'indirizzo `PC + offset`, dove `offset` è la costante inserita espressa in byte (nell'esempio, $100$).

L'istruzione **`jalr`** ("jump and link register") funziona sostanzialmente allo stesso modo dell'istruzione appena spiegata, con la differenza che, invece di saltare a `PC + offset`, si salta all'indirizzo dato da `rs1 + offset`.
___
### Come si traducono le istruzioni in linguaggio macchina?

[02 / pag. da 75 a 81]
___
### Direttive per l'assemblatore

Le **direttive**, nell'utilizzo di RARS, rappresentano sostanzialmente degli indicatori che specificano all'assemblatore la natura o lo scopo del codice che le segue. Due delle direttive più comunemente utilizzate sono:
- **`.data`**, utilizzata per la definizione di **dati statici** a cui accedere poi nel programma effettivo;
- **`.text`**, utilizzata per definire le **istruzioni** del programma.

Tendenzialmente, dunque, un programma in linguaggio assembly propriamente formattato avrà una struttura del tipo seguente:

```
.data
...

.text
...
```

Ci sono anche altre direttive, utili in vari contesti:
- **`.word`**, utilizzata per definire una sequenza di una o più words di dati (ad esempio, `num: .word 2` istanzia in memoria una word contenente il valore 2 all'indirizzo `num`; `array: .word 1, 2, 3, 4` istanzia in memoria 4 word successive, contenenti in ordine i valori specificati e a partire dall'indirizzo `array`);
- **`.asciiz`**, utilizzata per definire una stringa, terminata poi da uno 0;
- **`.byte`**, utilizzata per definire una sequenza di uno o più byte;
- **`.double`**, utilizzata per definire una sequenza di uno o più double;
- **`.float`**, utilizzata per definire una sequenza di uno o più float;
- **`.half`**, utilizzata per definire una sequenza di una o più mezze word;
- **`.space N`**, utilizzata per allocare un numero `N` di byte in memoria, senza definirne necessariamente dei valori iniziali (in RARS, i byte in questione vengono portati a 0).
___
### Etichette

Le istruzioni di salto condizionato e incondizionato risulterebbero profondamente macchinose da utilizzare se si dovesse necessariamente inserire un offset espresso in byte per farle funzionare. Dunque, per poter effettuare salti all'interno di un programma in maniera comoda e intuitiva, si introducono le "**etichette**", ossia sostanzialmente dei **segnaposto** per determinate righe di codice (in particolare, per la riga di codice che le segue). Ad esempio, implementando il seguente programma:

```
even_check:
	beq x1, x4, fine                             
	
	slli x5, x1, 2                               
	add x6, x5, x2                               
	lw x7, (x6)                                  
	
	andi x8, x7, 1                               
	bne x8, x0, odd                              
	
	add x3, x3, x7                               

odd:
	addi x1, x1, 1                               
	j even_check                                 

fine:
```

il funzionamento delle istruzioni di salto inserite risulta molto più intuitivo: il primo salto condizionato che troviamo, ossia `beq x1, x4, fine`, salta direttamente all'etichetta `fine` se il valore contenuto nel registro `x1` è uguale a quello del registro `x4`; il secondo salto condizionato, ossia `bne x8, x0, odd`, salta all'etichetta `odd` se il valore contenuto in `x8` è diverso da 0; infine, la pseudoistruzione `j even_check` rappresenta un salto incondizionato all'etichetta `even_check`.

Le etichette, dette anche "**label**", vengono sostituite dall'assemblatore con indirizzi di memoria reali al momento della compilazione del codice. Risulta chiaro, dunque, che possono essere utilizzate anche per indicare comodamente dei dati dichiarati nella sezione [[Assembly e RARS#Direttive per l'assemblatore|.data]]; ad esempio, scrivere `array: .word 1, 2, 3, 4` associa al vettore appena creato l'etichetta `array`, che potrà poi essere comodamente inserita nel proprio programma.
___
### Pseudoistruzioni

Oltre alle istruzioni di base che abbiamo visto finora, è possibile utilizzare anche le cosiddette "**pseudoistruzioni**", che non sono implementate in maniera diretta nell'hardware ma che possono essere facilmente tradotte in linguaggio macchina dal compilatore. Le pseudoistruzioni risultano comode in quanto, tendenzialmente, vanno a riassumere due o più istruzioni in una sola, oppure vanno a semplificare l'implementazione di una determinata istruzione; vediamo le principali:
- **`la rd, address`**;
- **`li rd, 10`**;
- **`mv rd, rs1`**;
- **`not rd, rs1`**
- **`neg rd, rs1`**;
- **`beqz rs1, label`** e simili;
- **`bgt rs1, rs2, label`**;
- **`jal label`**;
- **`j label`**.

La pseudoistruzione **`la rd, address`** consente di **caricare un indirizzo di memoria `address` in un registro `rd`**. Chiamare questa pseudoistruzione equivale a chiamare le seguenti istruzioni di base:

```
auipc rd, address[31:12]            #
addi rd, rd, address[11:0]          #
```

La pseudoistruzione **`li rd, 10`** consente di **caricare una costante in un registro `rd`**. Chiamare questa pseudoistruzione equivale a chiamare le seguenti istruzioni di base:

```

```

La pseudoistruzione **`mv rd, rs1`** consente di **copiare i contenuti di un registro `rs1` in un altro registro `rd`**. Chiamare questa pseudoistruzione equivale a chiamare la seguente istruzione di base:

```
addi rd, rs1, 0
```

La pseudoistruzione **`not rd, rs1`**...

La pseudoistruzione **`neg rd, rs1`** consente di **salvare in un registro `rd` il valore contenuto in un altro registro `rs1` sfruttando il complemento a 2**. Chiamare questa pseudoistruzione equivale a chiamare la seguente istruzione di base:

```
sub rd, x0, rs1
```

La pseudoistruzione **`beqz rs1, label`** consente di **saltare all'etichetta `label` se il valore contenuto nel registro `rs1` è uguale a 0**. Chiamare questa pseudoistruzione equivale a chiamare la seguente istruzione di base:

```
beq rs1, x0, label
```

Questa è solo una di più pseudoistruzioni molto simili, ossia:
- `beqz rs1, label`, salta a `label` se `rs1` è uguale a 0;
- `bnez rs1, label`, salta a `label` se `rs1` è diverso da 0;
- `blez rs1, label`, salta a `label` se `rs1` è minore o uguale a 0;
- `bltz rs1, label`, salta a `label` se `rs1` è minore di 0;
- `bgez rs1, label`, salta a `label` se `rs1` è maggiore o uguale a 0;
- `bgtz rs1, label`, salta a `label` se `rs1` è maggiore di 0.

La pseudoistruzione **`bgt rs1, rs2, label`** consente di **saltare all'etichetta `label` se il valore contenuto in un registro `rs1` è magggiore di quello contenuto in un altro registro `rs2`**. Chiamare questa pseudoistruzione equivale a chiamare la seguente istruzione di base:

```
blt rs2, rs1, label
```

La pseudoistruzione **`jal label`** consente di **saltare incondizionatamente all'etichetta `label` salvando l'indirizzo di ritorno in `x1`**. Chiamare questa pseudoistruzione equivale a chiamare la seguente istruzione di base:

```
jal x1, label
```

La pseudoistruzione `j label` consente di **saltare incondizionatamente all'etichetta `label` senza salvare un indirizzo di ritorno**. Chiamare questa pseudoistruzione equivale a chiamare la seguente istruzione di base:

```
jal x0, label
```
___
### Syscall

Ci sono dei registri, che in RARS vengono indicati con nomi che vanno da **`a0`** ad **`a7`**, che oltre alla loro regolare funzione di registri coprono anche un ruolo più particolare: sono utilizzati nelle cosiddette "**syscall**", ossia chiamate al sistema operativo per svolgere determinate operazioni. L'operazione in questione viene definita dal valore memorizzato nel registro `a7`, che può impartire l'ordine di svolgere una delle seguenti operazioni:
- **stampare nel terminale**:
	- stampare un **intero** (`a7 = 1`), con l'intero in questione che dovrà essere memorizzato in `a0`;
	- stampare una **stringa** (`a7 = 4`), con l'indirizzo della stringa salvata in memoria che dovrà essere memorizzato in `a0`;
	- stampare un **carattere** (`a7 = 11`), con il codice ASCII del carattere in questione che dovrà essere memorizzato in `a0`;
- **leggere dati dall'input dell'utente**:
	- leggere un **intero** (`a7 = 5`), che al momento della chiamata consentirà all'utente stesso di inserire il numero desiderato (se si inseriscono caratteri non-numerici, come lettere o simboli speciali, si potrebbe incappare in errori), numero che verrà processato come un intero segnato a 32 bit e memorizzato nel registro `a0`, per poter poi essere letto e manipolato liberamente nel programma;
	- leggere una **stringa** (`a7 = 8`), che al momento della chiamata consentirà all'utente stesso di inserire la stringa desiderata, stringa che verrà memorizzata in memoria all'indirizzo contenuto nel registro `a0` (inoltre, della stringa data come input, verranno letti e memorizzati solo `a1 - 1` caratteri, con `a1` che dovrebbe quindi contenere, al momento della chiamata, la lunghezza massima della stringa incluso il terminatore `\0`) (essendo ogni carattere della stringa contenuto in un singolo byte di memoria, ed essendo la memoria stessa indicizzata al byte, è possibile accedere comodamente ai vari caratteri di una stringa memorizzata a partire dall'indirizzo `buffer` utilizzando ad esempio l'istruzione `lb x1, index(buffer)`, dove `index` rappresenta l'indice del carattere all'interno della stringa);
	- leggere un **carattere** (`a7 = 12`), che al momento della chiamata consentirà all'utente stesso di inserire il carattere desiderato (se si inserisce più di un carattere, verrà letto solo il primo di questi), carattere che verrà memorizzato come codice ASCII nel registro `a0`, per poter poi essere letto e manipolato liberamente nel programma;
- **terminare il programma**:
	- terminare il programma con **codice di default** "$0$" (`a7 = 10`), fondamentale da inserire al termine del proprio programma per evitare malfunzionamenti indesiderati;
	- terminare il programma con **codice arbitrario** (`a7 = 93`), con il codice in questione che dovrà essere memorizzato in `a0`;
- **lavorare con file** (i file in questione devono trovarsi nella stessa cartella del file `.asm` su cui si sta lavorando):
	- **aprire** un file (`a7 = 1024`), con il path per il file in questione che dovrà essere memorizzato come stringa in `a0`, la modalità di apertura del file indicata dal codice che dovrà essere memorizzato in `a1` ($0$ = modalità di lettura, $1$ = modalità di sovrascrittura ed eventuale creazione del file se esso non esisteva precedentemente, $9$ = modalità di "scrittura in coda" ed eventuale creazione del file se esso non esisteva precedentemente), ed eventuali permessi (rilevanti solo se il file dovrà essere creato, altrimenti vengono ignorati) che dovranno essere memorizzati in `a2`  (in seguito alla chiamata, nel registro `a0` viene memorizzato il "file descriptor" del file in questione, per futuri utilizzi);
	- **chiudere** un file precedentemente aperto (`a7 = 57`), con il "file descriptor" del file da chiudere che dovrà essere memorizzato in `a0` (in seguito alla chiamata, in `a0` verrà memorizzato automaticamente $0$ se l'operazione è stata compiuta con successo, o in alternativa un valore negativo in caso di errore);
	- **leggere** un file precedentemente aperto (`a7 = 63`), con il "file descriptor" del file da leggere che dovrà essere memorizzato in `a0`, l'indirizzo in memoria da dove cominciare a conservare i dati letti che dovrà essere memorizzato in `a1`, e il numero massimo di byte da leggere del file in questione che dovrà essere memorizzato in `a2` (in seguito alla chiamata, in `a0` verrà memorizzato automaticamente il numero di byte effettivamente letti, in quanto esso non è sempre pari al valore massimo stabilito, o in alternativa un valore negativo in caso di errore);
	- **scrivere** in un file precedentemente aperto (`a7 = 64`), con il "file descriptor" del file in cui scrivere che dovrà essere memorizzato in `a0`, l'indirizzo in memoria da dove cominciano i dati da scrivere nel file che dovrà essere memorizzato in `a1`, e il numero di byte da scrivere nel file che dovrà essere memorizzato in `a2` (in seguito alla chiamata, in `a0` verrà memorizzato il numero di byte effettivamente scritti nel file, o in alternativa un valore negativo in caso di errore);
- **impostare un tempo di sleep per il thread corrente** (`a7 = 32`), con il tempo di sleep espresso in millisecondi che dovrà essere memorizzato in `a0`.

Per eseguire concretamente le istruzioni codificate nei modi appena visti, bisogna prima assegnare ai registri coinvolti i valori desiderati, e quindi utilizzare l'istruzione **`ecall`**, che va semplicemente ad eseguire l'istruzione codificata dal valore contenuto in `a7`, utilizzando eventualmente i dati presenti in registri come `a0`.
___
### Vettori e matrici

Un **vettore** è una **sequenza di elementi di dimensioni uguali**, memorizzati in memoria consecutivamente e indirizzabili con indici che vanno da 0 a $N - 1$, dove $N$ è la lunghezza del vettore e dunque il numero dei suoi elementi. Naturalmente, lo spazio totale in termini di memoria occupato da un vettore sarà dato dal prodotto tra $N$ e la dimensione di un singolo elemento.

Tendenzialmente, risulta comodo definire staticamente vettori che verranno eventualmente utilizzati in un programma nella sezione [[Assembly e RARS#Direttive per l'assemblatore|.data]], usando un'[[Assembly e RARS#Etichette|etichetta]] che andrà a rappresentare l'indirizzo in memoria del primo elemento del vettore.

Dunque, per **accedere all'elemento $i$-esimo di un vettore** bisognerà aggiungere all'indirizzo di base un determinato `offset`, dato dal prodotto tra l'indice $i$ e la dimensione di un singolo elemento del vettore. Ad esempio, lavorando sul vettore:

```
vector: .word 1, 2, 3, 4
```

l'indirizzo base del vettore, ossia quello del primo elemento, sarà `vector`, dunque caricare il valore memorizzato all'indirizzo `vector` mediante un'istruzione come `la t0, vector` restituirà `1`. Per accedere, ad esempio, al secondo elemento del vettore, bisogna tenere a mente la dimensione di un elemento di quest'ultimo: in questo caso, ogni elemento occupa una word, ossia 32 bit o 4 byte, dunque l'`offset` sarà dato da $1 \times 4$; supponendo che il registro `t0` contenga l'indice dell'elemento desiderato, che `t1` contenga l'indirizzo base del vettore, e che si voglia memorizzare l'indirizzo dell'elemento desiderato in `t2`, per ottenere quest'ultimo si dovrà implementare un codice del genere:

```
slli t2, t0, 2
add t2, t2, t1
lw s0, (t2)
```

Ovviamente, a seconda della dimensione di ogni elemento del vettore in questione (word, mezza word, byte, ecc. ecc.), si andrà a modificare la prima istruzione.

Per quanto riguarda le **matrici** (in particolare, qui andremo a trattare quelle **bidimensionali** e **tridimensionali**), esse vengono trattate concretamente come dei vettori monodimensionali, o più propriamente come sequenze di più vettori. Per capire meglio questo concetto, parliamo prima di tutto delle matrici a due dimensioni.

Una **matrice a due dimensioni**, di dimensioni $M \times N$, non è altro che una successione di $M$ vettori monodimensionali di lunghezza $N$: se ne evince che il numero totale di elementi della matrice sarà proprio $M \times N$, che lo spazio totale occupato in memoria dalla matrice sarà dato dal prodotto tra il numero totale dei suoi elementi e la dimensione di un singolo elemento, e che in quanto equivalente a una sequenza di vettori monodimensionali la si definisce staticamente come un vettore di lunghezza $M \times N$.

Supponiamo, ora, di avere una matrice con $M$ righe e $N$ colonne, e di voler **accedere all'elemento `matrix[y][x]`**: si dovrà accedere all'indirizzo ottenuto sommando l'indirizzo base della matrice con un `offset` dato dal prodotto tra $(y \times N + x)$ e la dimensione in byte di un singolo elemento. Questa formula può essere dimostrata ragionando sul numero di elementi che precedono l'elemento cercato: sappiamo, infatti, che prima di quest'ultimo ci saranno non solo $y \times N$ elementi, ossia $y$ righe di $N$ elementi, ma anche altri $x$ elementi sulla sua stessa riga, arrivando così alla formula appena data. Ad esempio, supponendo di avere una matrice bidimensionale di dimensioni 4x3, ossia da 4 righe e 3 colonne, per accedere all'elemento `matrix[1][2]` si dovrà implementare il seguente codice:

```
.data
matrix: .word 1, 2, 3,
              4, 5, 6,
              7, 8, 9,
              10, 11, 12

.text
main:
	li t0, 3
	li t1, 1
	li t2, 2

	mul t3, t1, t0
	add t3, t3, t2
	slli t3, t3, 2

	la t4, matrix
	add t5, t3, t4
	lw t6, 0(t5)
```

Un discorso sostanzialmente analogo vale per una **matrice a tre dimensioni**, di dimensioni $M \times N \times P$, interpretabile come una successione di $P$ matrici di dimensioni $M \times N$. In questo caso, per ottenere la formula dell'`offset`, sappiamo prima di tutto che l'elemento `matrix[z][y][x]` sarà preceduto da $z$ matrici di dimensioni $M \times N$, ma anche da $y$ righe di $M$ elementi, e infine da $x$ elementi sulla sua riga; dunque, la formula per ottenere l'`offset` da sommare all'indirizzo base della matrice per ottenere l'indirizzo dell'elemento `matrix[z][y][x]` è $(z \times (M \times N)) + (y \times N) + x$.
___
### Funzioni

[07]
___
### Ricorsione

[08]
___