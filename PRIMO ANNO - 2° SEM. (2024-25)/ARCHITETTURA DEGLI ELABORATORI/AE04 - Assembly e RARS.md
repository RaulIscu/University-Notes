Di seguito, si troveranno alcuni paragrafi in cui si esporranno concetti e convenzioni relative alla **programmazione in linguaggio assembly**, e in particolare collegate al software di programmazione **RARS**. Si consideri questo file come "espansione" di "[[AE03 - Le istruzioni]]" sotto questo punto di vista.

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

Le etichette, dette anche "**label**", vengono sostituite dall'assemblatore con indirizzi di memoria reali al momento della compilazione del codice. Risulta chiaro, dunque, che possono essere utilizzate anche per indicare comodamente dei dati dichiarati nella sezione [[AE04 - Assembly e RARS#Direttive per l'assemblatore|.data]]; ad esempio, scrivere `array: .word 1, 2, 3, 4` associa al vettore appena creato l'etichetta `array`, che potrà poi essere comodamente inserita nel proprio programma.
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

Tendenzialmente, risulta comodo definire staticamente vettori che verranno eventualmente utilizzati in un programma nella sezione [[AE04 - Assembly e RARS#Direttive per l'assemblatore|.data]], usando un'[[AE04 - Assembly e RARS#Etichette|etichetta]] che andrà a rappresentare l'indirizzo in memoria del primo elemento del vettore.

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