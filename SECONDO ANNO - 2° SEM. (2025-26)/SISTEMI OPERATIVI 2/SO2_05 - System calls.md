## Cos'è una system call?

Come ben sappiamo, **il kernel** è la componente principale e più importante dell'OS, che **si occupa della gestione delle risorse disponibili** nel calcolatore (CPU, RAM, dispositivi di I/O, ecc. ecc.), offrendo e regolando l'accesso e l'utilizzo delle risorse da parte dei processi. Quest'ultimi, dunque, non possono accederci direttamente, ma devono necessariamente fare riferimento al kernel per farlo. Viene spontaneo chiedersi, dunque, **in che modo i processi possono comunicare al kernel il bisogno di una determinata risorsa o servizio?** La risposta a questa domanda si trova in un mezzo fondamentale per il funzionamento corretto di un calcolatore: le cosiddette "**system calls**", dette anche **chiamate di sistema**.

A grandi linee, possiamo vedere le system calls come un'**interfaccia tra processi utente e kernel**, che permette la comunicazione sicura e regolamentata tra queste due parti. Più nello specifico, le system calls implementate in un determinato OS rappresentano dei **punti di accesso offerti dal kernel**, tramite i quali un processo può **accedere a determinati servizi o risorse grazie al kernel stesso**. Naturalmente, le system calls vengono implementate solo per **gestire mansioni di una certa importanza, che richiedono determinati privilegi per essere svolte** (leggere un file, allocare memoria, ecc. ecc.); inoltre, in base all'OS considerato, il numero di system calls cambia, ad esempio:
- un sistema **UNIX v7** disponeva di circa **50 system calls**;
- un sistema **Linux** moderno dispone di circa **380 system calls**.

Ma **come fa un programmatore a "invocare" una determinata system call?** In Linux, a prescindere dalla tecnica o linguaggio specifico utilizzato per invocare una system call, esse sono definite in [[SO2_04 - C|C]]: si intende, dunque, che **per ogni system call prevista dall'OS esiste una funzione C avente lo stesso nome**. Dunque, l'eventuale processo utente che intende eseguire una system call **eseguirà, prima di tutto, la funzione C corrispondente**, e quest'ultima farà in modo di richiedere il servizio o la risorsa in questione al kernel utilizzando le tecniche necessarie (il più delle volte, ad esempio, **i parametri della funzione vengono inseriti in registri** ben precisi, e in seguito **viene generato un "interrupt"**, in modo che il kernel assuma il controllo dell'esecuzione per gestire la system call).

Per avere maggiori informazioni su determinate system calls su Linux, si può accedere al **manuale `man`** dalla [[SO2_01 - Shell|shell]], e in particolare alla sua **seconda sezione**, nel modo seguente:

```
man 2 system_call
```

##### System calls vs. funzioni di libreria

Prima di proseguire, è opportuno fare una netta **distinzione tra [[SO2_05 - System calls#Cos'è una system call?|system calls]] e "funzioni di libreria"**. 

Quest'ultime, nonostante nella scrittura di codice si presentino effettivamente in modo identico alle prime, **non rappresentano punti di accesso diretti al kernel**, ma sono semplicemente delle [[SO2_04 - C#Funzioni|funzioni]] a tutti gli effetti, dei blocchi di codice riutilizzabili e atti a semplificare la vita del programmatore. Del resto, **una funzione di libreria potrebbe invocare**, "segretamente", **una o più system calls** per svolgere la sua mansione (si pensi, ad esempio, a `printf`, che per stampare del testo sullo schermo fa riferimento alla system call `write`), ma **potrebbe anche non invocarne nessuna** e non interagire mai con il kernel (si pensi, ad esempio, a funzioni come `strcpy` o `atoi`).

Forse, la differenza principale tra system calls e funzioni di libreria sta nella **sostituibilità**: in particolare, **una funzione di libreria può essere rimpiazzata, ma una system call no**. Ciò è vero semplicemente per il fatto che una funzione di libreria rappresenta a tutti gli effetti una sovrastruttura, creata ad hoc per semplificare l'esecuzione di un compito ma non necessariamente invariabile e inamovibile, e dunque un programmatore potrebbe scrivere una sua libreria personalizzata sostituendo quella standard, senza incappare in alcun problema; **le system calls**, invece, **sono specifiche dell'OS, e non sono modificabili né sostituibili**, dato che rappresentano i precisi punti di accesso forniti dal kernel. Per comprendere meglio, possiamo vedere un esempio confrontando la **system call `sbrk`** e la **funzione di libreria `malloc`**: la prima, in parole povere, ha il compito di allocare al processo dei blocchi di memoria, e per fare ciò lavora a stretto contatto con il kernel; la seconda, invece, rappresenta una semplice sovrastruttura, ed è implementata utilizzando `sbrk`; potremmo implementare una nostra versione della `malloc`, ma in un modo o nell'altro dovremmo sempre fare riferimento a `sbrk` per farlo.

Ciononostante, anche le funzioni di libreria sono importantissime, e in quanto tali è opportuno conoscerne il funzionamento nel dettaglio. Come per le system calls, il `man` prevede anche una **sezione dedicata alle funzioni di libreria**, ossia la **terza sezione**, accessibile nel modo seguente dalla [[SO2_01 - Shell|shell]]:

```
man 3 fun_lib
```
___
##### Errori nelle system calls

**Invocare una system call non garantisce sempre il servizio o la risorsa richiesti**: è perfettamente possibile, infatti, che l'esecuzione di una system call non vada a buon fine e che restituisca un qualche **errore**. È una situazione che può verificarsi per vari motivi, tra cui:
- **privilegi insufficienti** del processo che ha invocato la system call;
- **risorse insufficienti** per l'esecuzione;
- **argomenti non validi** in input;

e altri ancora. Per questo motivo, è sempre buona pratica **controllare il valore di ritorno di ogni system call**, per essere in grado di gestire gli eventuali errori ed evitare crash o comportamenti imprevisti nel programma. 

Tipicamente, **una system call che ha generato un errore durante la sua esecuzione ritorna `-1`**; tuttavia, per ottenere informazioni più specifiche riguardo l'errore in questione, si dovrà controllare il valore contenuto nella **variabile globale `errno`**. Si tratta di una variabile definita nell'header file **`errno.h`**, e in generale contiene il **codice di errore dell'ultima system call invocata che ha generato un errore** (se una system call termina la sua esecuzione con successo, `errno` rimane invariata, dunque ha senso controllarne il contenuto solo dopo essersi accertati che la system call considerata abbia effettivamente ritornato `-1`).

Contestualmente agli errori delle system call e alla variabile `errno`, ci tornano utili **due funzioni**:
- **`perror`**, definita nella libreria standard **`stdio.h`**;
- **`strerror`**, definita nella libreria **`string.h`**.

La funzione **`perror`**, la cui sinossi completa è:

```
void perror(const char *prefix)
```

serve a **stampare sul [[SO2_03 - Processi#Canali standard|canale]] `stderr` un messaggio di errore, convertendo il codice contenuto in `errno` in una stringa**. Tale stringa, in particolare, segue la struttura **`prefix:errno_string`**, dove `prefix` è la **stringa `prefix` passata in input alla funzione**, mentre `errno_string` rappresenta il **messaggio di errore associato al valore di `errno` letto**. Ad esempio, effettuare la seguente chiamata:

```
perror("main");
```

porterebbe alla seguente stampa su `stderr`:

```
main:errno_string = errno
```

La funzione **`strerror`**, la cui sinossi completa è:

```
char *strerror(int errnum)
```

serve invece a **convertire il codice contenuto in `errno` nel messaggio di errore associato ad esso**, che viene restituito come stringa.

Di seguito, possiamo vedere un esempio basilare di utilizzo di queste funzioni:

```
if (syscall() == -1)
{
	int errsv = errno;
	perror("main");
	printf("Si è verificato il seguente errore: %s\n", strerror(errsv));
}
```
___
## System calls per la gestione della memoria

Per parlare delle **system calls utilizzate per la gestione della memoria**, ricordiamo innanzitutto quali sono le principali **[[SO2_05 - System calls#System calls vs. funzioni di libreria|funzioni di libreria]]** utilizzate per questo scopo, ossia:
- **`void *malloc(size_t size)`**;
- **`void *calloc(size_t nmemb, size_t size)`**;
- **`void *realloc(void *ptr, size_t size)`**;
- **`void free(void *ptr)`**;
- **`void *alloca(size_t size)`**.

Le prime 4 sono state già viste approfondendo l'[[SO2_04 - C#Allocazione dinamica di memoria|allocazione dinamica di memoria]] in C, mentre l'ultima è un po' più particolare, dato che piuttosto che allocare memoria dinamicamente (dunque, nell'Heap) essa **alloca memoria nello Stack del [[SO2_06 - Threads|thread]] corrente**. Le funzioni relative all'allocazione dinamica sono tutte definite nell'header file **`stdlib.h`**, mentre `alloca` è definita in **`alloca.h`**.

Ancora, abbiamo anche altre **funzioni di libreria utili per manipolare byte** grezzi, prime su tutte:
- **`void *memset(void *s, int c, size_t n)`**, che viene utilizzata per **assegnare un valore `c` a `n` bytes contigui dell'area di memoria a cui punta `s`**;
- **`void *memcpy(void *dest, const void *src, size_t n)`**, che viene utilizzata per **copiare `n` bytes contigui dall'area di memoria a cui punta `src` nell'area a cui punta `dest`** (per il corretto funzionamento di tale funzione, è fondamentale che le due aree di memoria a cui puntano `src` e `dest` non si sovrappongano).

Tutte le funzioni di libreria che abbiamo visto in questo paragrafo utilizzano delle system calls per gestire la memoria. In particolare, quelle che vedremo sono le seguenti:
- **`brk`**;
- **`sbrk`**;
- **`mmap`**;
- **`msync`**;
- **`munmap`**.

Le prime due, ossia **`brk`** e **`sbrk`**, sono in realtà molto semplici e simili tra loro; per poterle spiegare, però, è opportuno introdurre un concetto legato al funzionamento dell'Heap: il "**Program Break**". In parole povere, l'Heap è a tutti gli effetti costituito da un singolo segmento contiguo di memoria, che cresce "verso l'alto", o meglio verso indirizzi di memoria più grandi; il **confine superiore** di questo segmento di memoria è proprio il Program Break, tale per cui tutto ciò che sta sotto di esso è memoria allocata al processo, mentre tutto ciò che sta sopra di esso è memoria a cui il processo non può accedere. Detto ciò, lo scopo di `brk` e `sbrk`, la cui sinossi completa è:

```
int brk(void *addr)
void *sbrk(intptr_t increment)
```

è quello di **spostare il Program Break dell'Heap del processo chiamante**. 

In particolare, **`brk` chiede di spostare il Program Break precisamente all'indirizzo `addr`**, in modo che se quest'ultimo è più alto del Program Break corrente allora verrà allocata più memoria, mentre se è più basso allora della memoria verrà liberata e restituita all'OS. Questa system call **restituisce `0` in caso di successo** e **`-1`** altrimenti.

Invece, **`sbrk`** (quella più comunemente utilizzata) **chiede di spostare il Program Break di un numero esatto `increment` di byte**; in base al segno del valore `increment`, dunque, l'area di memoria dell'Heap verrà o aumentata o diminuita. Questa system call **restituisce l'indirizzo del Program Break precedente**, ossia l'inizio della nuova memoria appena allocata, **in caso di successo**, e **`-1`** altrimenti.

[SLIDES: 10, slide 30/32]
___
## System calls per la gestione di file e directory

In sistemi Linux, **qualsiasi risorsa è rappresentata con un file** (ad eccezione dei processi effettivi): file su disco, dispositivi di I/O, periferiche hardware, sockets, tutto viene gestito utilizzando l'astrazione del file. Se il programmatore vuole lavorare sui file, deve necessariamente seguire una **sequenza tipica di azioni**:
1. **aprire il file** in una determinata modalità (lettura, scrittura, ecc. ecc.);
2. **operare sul file**;
3. **chiudere il file** dopo aver finito di leggerlo o manipolarlo.

L'ultimo passaggio può sembrare, apparentemente, superfluo, dato che **un [[SO2_03 - Processi#Cos'è un processo?|processo]], quando termina la sua esecuzione, chiude automaticamente tutti i file che aveva aperto**; ciononostante, è sempre buona pratica chiuderli esplicitamente nel codice, per evitare comportamenti imprevisti.

Quando viene aperto un file, il kernel non restituisce mai direttamente i dati grezzi: di base, l'apertura di un file **genera sequenzialmente un intero piccolo a partire da 0**, intero che prende il nome di "**file descriptor**", o "**descrittore del file**", che viene utilizzato come riferimento a uno specifico file aperto. In particolare, i **[[SO2_03 - Processi#Canali standard|canali standard]]** sono visti come file che **vengono aperti di default per ogni processo**, e assumono i seguenti file descriptors:
- **`0`** per **`stdin`**;
- **`1`** per **`stdout`**;
- **`2`** per **`stderr`**.

Quando un file viene chiuso, il suo file descriptor viene liberato e può essere riutilizzato. È possibile, del resto, anche aprire uno stesso file e ottenere due file descriptor diversi (ad esempio, se due utenti distinti aprono lo stesso file).

Come accennato già in precedenza, all'apertura del file l'OS deve sapere **come si intende utilizzare il file** in questione: per permettere ciò, l'apertura di un file deve disporre anche di determinate "**flags**", che possono essere divise in due categorie:
- le **"file status" flags**, associato allo **stato corrente di un file** e che sono condivise tra tutti i file descriptors ottenuti, per duplicazione, da un unico file descriptor;
- le **"file descriptor" flags**, associate al **file descriptor specifico** e che sono indipendenti dal contenuto o dallo stato del file in questione.

Possiamo categorizzare le flags di un file anche in base allo **scopo**, caso in cui otteniamo altre tre categorie:
- flags relative alla **modalità di accesso**, che vengono specificate all'apertura e che non possono essere modificate in seguito;
- flags relative all'**apertura**, che definiscono più nello specifico il modo in cui un file viene aperto, e non vengono mantenute in seguito;
- flags relative alla **modalità operativa**, che definiscono il comportamento delle operazioni di manipolazione del file (lettura, scrittura, ecc. ecc.), e che possono essere modificate in seguito.

Concretamente, le flags sono rappresentate come delle **maschere di bit**, ossia delle sequenze di bit settati quasi tutti a `0` e con un bit settato a `1`, dove la posizione del bit settato a `1` permette di capire quale flag si sta considerando. Al momento dell'apertura di un file, dunque, si potranno **combinare una o più flags con un OR bit a bit tra le stesse**.

A questo punto, siamo pronti per affrontare il vero fulcro di questo paragrafo: le **system calls** (e anche alcune **[[SO2_05 - System calls#System calls vs. funzioni di libreria|funzioni di libreria]]**) **per la gestione dei file**. In particolare, approfondiremo le system calls e funzioni di libreria utilizzate per i seguenti ambiti:
- **[[SO2_05 - System calls#Apertura di un file|apertura]], [[SO2_05 - System calls#Manipolazione di un file|manipolazione]] e [[SO2_05 - System calls#Chiusura di un file|chiusura di un file]]**;
- **[[SO2_05 - System calls#Gestione dei metadati di un file|gestione dei metadati di un file]]**;
- **[[SO2_05 - System calls#Gestione delle directory|gestione delle directory]]**;
- **[[SO2_05 - System calls#Controllo avanzato dei file|controllo avanzato dei file]]**.

##### Apertura di un file

L'**apertura di un file** viene fatta attraverso la system call **`open`**, la cui sinossi completa è:

```
int open(const char *pathname, int flags)
```

dove **`pathname`** è la **stringa contenente il path** (relativo o assoluto) **del file che si vuole aprire**, mentre **`flags`** è l'**insieme delle [[SO2_05 - System calls#System calls per la gestione di file e directory|flags]] specificate per il file in questione** (come accennato in precedenza, ogni singola flag è una maschera di bit, e se si vogliono specificare più flags si devono porre in OR bit a bit). Se l'operazione ha successo, **`open` restituisce i file descriptor del file appena aperto**, e in caso contrario restituisce **`-1`**.

**Il parametro `flags`**, dunque le flags relative al file che si sta aprendo, **è sostanzialmente equivalente al parametro `mode` della funzione di libreria `fopen`**, tant'è che è possibile stilare una tabella in cui si pongono a confronto questi due parametri, per capire quali flags siano necessarie per ottenere l'effetto di una determinata modalità di `fopen` (o viceversa):

| `mode` di `fopen` | `flags` di `open`                 |
| ----------------- | --------------------------------- |
| `r`               | `O_RDONLY`                        |
| `w`               | `O_WRONLY \| O_CREAT \| O_TRUNC`  |
| `a`               | `O_WRONLY \| O_CREAT \| O_APPEND` |
| `r+`              | `O_RDWR`                          |
| `w+`              | `O_RDWR \| O_CREAT \| O_TRUNC`    |
| `a+`              | `O_RDWR \| O_CREAT \| O_APPEND`   |

Vien da chiedersi, a questo punto, **cosa comporti ciascuna delle `flags` specificabili all'apertura di un file**. Di seguito, si fornisce un elenco comprensivo di queste informazioni, partendo dalle **flags relative alla modalità di accesso**:
- **`O_RDONLY`** impone di aprire il file in **sola lettura**;
- **`O_WRONLY`** impone di aprire il file in **sola scrittura**;
- **`O_RDWR`** impone di aprire il file **sia in lettura che in scrittura**.

Abbiamo, poi, le **flags relative all'apertura**:
- **`O_CREAT`** impone che, **se il file** specificato con `pathname` **non esiste**, **esso venga creato** (come un file vuoto, inizialmente);
- **`O_EXCL`** viene utilizzato esclusivamente in coppia con `O_CREAT`, e fa in modo che **`open` restituisca un errore se si cerca di creare un file che esiste già** (può essere utile per evitare di sovrascrivere inavvertitamente dei dati).

Infine, vediamo le **flags relative alla modalità operativa**:
- **`O_APPEND` forza il cursore del file sempre alla fine dello stesso** prima di ogni operazione di scrittura;
- **`O_TRUNC`** impone che, **se il file esiste già e viene aperto in scrittura, esso viene completamente sovrascritto al momento dell'apertura** (in altre parole, il contenuto precedente del file viene svuotato appena esso viene aperto);
- **`O_SYNC`** impone che **le scritture nel file debbano essere "sincrone"** (più lento, ma anche più sicuro).

Va specificata una particolarità: nell'eventualità in cui venga specificata la flag `O_CREAT`, la sinossi della system call cambia, dato che **si richiede di specificare anche i [[SO2_02 - File system#Permessi di accesso ai file|permessi di accesso]] al file che verrebbe eventualmente creato**. In tal caso, la nuova firma di `open` è la seguente:

```
int open(const char *pathname, int flags, mode_t mode)
```

dove **`mode`** rappresenta una **stringa di cifre ottali**, simile a quelle già viste in precedenza per condensare i permessi di accesso a un file.

Oltre al confronto tra `flags` e `mode`, la system call `open` e la funzione di libreria `fopen` si differenziano anche per un altro aspetto fondamentale: **`fopen` restituisce un puntatore a un oggetto di tipo `FILE`, mentre `open` restituisce un semplice file descriptor, gestito dal kernel**. Ciò vuol dire che, come si può immaginare, utilizzare `fopen` mette a disposizione molte più informazioni al programmatore, dato che tale oggetto `FILE` contiene, oltre al file descriptor, anche un puntatore a un **buffer**, la **dimensione del buffer** in questione, un **contatore dei caratteri attualmente contenuti nel buffer**, una **flag di errore**, ecc. ecc.
___
##### Manipolazione di un file

Per **"manipolazione" di un file** intendiamo principalmente due operazioni: **lettura** e **scrittura**. In questo paragrafo, andremo ad approfondire proprio tali operazioni.

Per **leggere un file aperto**, estraendone i dati, si utilizza la system call **`read`**, la cui sinossi completa è:

```
ssize_t read(int fd, void *buf, size_t count)
```

dove **`fd`** è il **file descriptor del file da leggere**, **`buf`** è un **puntatore a un'area di memoria precedentemente allocata**, in cui `read` andrà a depositare i dati letti dal file, e **`count`** è il **numero massimo di byte da leggere** con tale chiamata. Questa system call **restituisce il numero di byte effettivamente letti** (dato che, se il file finisce prima del previsto, `read` leggerà un numero di byte inferiore a `count`), altrimenti **restituisce `-1` in caso di errore**, aggiornando il valore della variabile `errno` con uno dei seguenti codici di errore:
- **`EBADF`**, se il file descriptor `fd` non è valido, o non è stato aperto con la modalità corretta;
- **`EFAULT`**, se il puntatore `buf` non è valido;
- **`EINTR`**, se l'esecuzione è stata interrotta dall'arrivo di un segnale di sistema prima che si potesse trasferire anche solo un byte;
- **`EINVAL`**, se gli argomenti passati al momento della chiamata non sono validi;
- **`EIO`**, se si è verificato un errore a livello di hardware;
- **`EISDIR`**, se il file descriptor `fd` che si sta cercando di leggere indica una directory.

Anche per la system call `read`, possiamo fare un **confronto con `fread`**, la sua funzione di libreria corrispondente. La differenza principale sta nella **"bufferizzazione" dei dati letti**: **la system call `read` non è bufferizzata**, dunque se viene chiamata un certo numero di volte $n$ per leggere anche solo un singolo byte da un file, dovrà effettuare $n$ accessi diretti ai byte grezzi del file su disco, con un grande decremento delle prestazioni; invece, **la funzione di libreria `fread`, lavorando su un oggetto `FILE`, è effettivamente bufferizzata**, dunque, quando `fread` viene chiamata la prima volta per leggere anche solo un singolo byte dal file in questione, essa procede (tramite una chiamata alla system call `read`) a trasferire un ampio blocco di memoria dal disco al buffer, in modo che eventuali chiamate successive restituiscano i dati richiesti quasi istantaneamente. Un'altra differenza importante sta nella **tipizzazione dei dati in lettura**: `read` vede semplicemente byte grezzi, mentre `fread` accetta come parametro anche la grandezza in byte del tipo di dato che si sta leggendo e il numero di elementi letti, "tipizzando" di fatto i dati ottenuti dal file.

Per **scrivere in un file aperto**, invece, si utilizza la system call **`write`**, la cui sinossi completa è:

```
ssize_t write(int fd, const void *buf, size_t count)
```

dove **`fd`** è il **file descriptor del file in cui scrivere**, **`buf`** è un **puntatore a un'area di memoria precedentemente allocata**, da cui `write` leggerà i dati da scrivere, e **`count`** è il **numero di byte da scrivere** con tale chiamata. Questa system call **restituisce il numero di byte effettivamente scritti** (dato che, se ad esempio l'esecuzione viene interrotta da un segnale, `write` scriverà un numero di byte inferiore a `count`), altrimenti **restituisce `-1` in caso di errore**, aggiornando il valore della variabile `errno` con uno dei seguenti codici di errore:
- **`EBADF`**, se il file descriptor `fd` non è valido, o non è stato aperto con la modalità corretta;
- **`EFAULT`**, se il puntatore `buf` non è valido;
- **`EINTR`**, se l'esecuzione è stata interrotta dall'arrivo di un segnale di sistema prima che si potesse trasferire anche solo un byte;
- **`EINVAL`**, se gli argomenti passati al momento della chiamata non sono validi;
- **`EIO`**, se si è verificato un errore a livello di hardware;
- **`ENOSPC`**, se il disco è completamente pieno e non c'è più spazio per scrivere i dati richiesti;
- **`EFBIG`**, se si vogliono scrivere dati che porterebbero il file in questione a superare la dimensione massima consentita dal file system o dall'OS.

Il **confronto tra la system call `write` e la funzione di libreria `fwrite`** porta pressoché alle stesse differenze esposte in precedenza parlando di `read` e `fread`: la differenza principale, dunque, sta nel fatto che `write` non è bufferizzata, mentre `fwrite` sì.

Un'altra system call, meno fondamentale di `read` e `write` ma comunque molto utile, è **`lseek`**, la cui sinossi completa è:

```
off_t lseek(int fd, off_t offset, int whence)
```

Quello che fa, in parole povere, è **spostare il cursore del file descriptor `fd` di un numero di byte pari a `offset`, a partire da `whence`**. In particolare, `whence` può accettare tre costanti:
- **`SEEK_SET`**, che fa in modo che l'`offset` parta **dall'inizio del file**;
- **`SEEK_CUR`**, che fa in modo che l'`offset` parta **dalla posizione corrente**;
- **`SEEK_END`**, che fa in modo che l'`offset` parta **dalla fine del file**.

Se `lseek` viene eseguita con successo, essa **restituisce il nuovo offset a partire dall'inizio del file** (in byte), e **`-1`** altrimenti.
___
##### Chiusura di un file

Per **chiudere un file precedentemente aperto**, la system call di riferimento è **`close`**, la cui sinossi completa è:

```
int close(int fd)
```

dove **`fd`** è il **file descriptor del file da chiudere**. Tale system call **restituisce `0` in caso di successo**, e **`-1`** altrimenti, aggiornando il valore della variabile `errno` con uno dei seguenti codici di errore:
- **`EBADF`**, se si cerca di chiudere un file descriptor che non corrisponde a nessun file attualmente aperto, oppure se si cerca di chiudere un file descriptor più di una volta;
- **`EIO`**, se fallisce la scrittura finale dei dati nel file da chiudere o se, per qualche motivo, i dati vengono persi. 

Concretamente, quello che succede è che viene "reciso" il collegamento tra il file descriptor `fd` e la struttura dati interna che rappresenta il file aperto. Una volta chiamata `close` su un certo file descriptor, quest'ultimo dunque torna a essere disponibile, e potrà essere riassegnato se verranno aperti altri file (tipicamente, infatti, **a un nuovo file aperto si assegna sempre il file descriptor più basso disponibile**).

Bisogna fare attenzione nei contesti in cui un processo apre un grande numero di file senza chiuderli gradualmente: infatti, in Linux, **ogni processo ha un limite massimo di file descriptors che può tenere aperti** (tipicamente, circa 1024); dunque, se si riempiono tutti i posti disponibili, avviene quello che viene chiamato "**File Descriptor Leak**", e il programma risulterà di fatto bloccato, dato che non potrà più aprire file, connessioni di rete, ecc. ecc.

I sistemi Unix e Linux presentano una particolarità proprio riguardo la chiusura di file: **cancellare un file**, in generale, **rimuove "apparentemente" il file dalla cartella** (rendendolo, di fatto, inaccessibile), **ma non distrugge i dati effettivi finché c'è almeno un programma che lo sta ancora leggendo o scrivendo**. In altre parole, un file rimosso viene effettivamente cancellato quando viene chiuso l'ultimo file descriptor che fa riferimento ad esso. Questo comportamento, oltre che utile per evitare comportamenti indesiderati, può essere sfruttato in vari contesti (ad esempio, la creazione di file temporanei sicuri).
___
##### Gestione dei metadati di un file

A questo punto, dopo aver visto system calls atte a lavorare concretamente con i contenuti di un file, vediamone altre che sono piuttosto destinate a **visualizzare, manipolare e gestire i metadati di un file**. In particolare, in questo paragrafo, andremo ad approfondire le seguenti system calls:
- **`dup`**;
- **`stat`**;
- **`fstat`**;
- **`chmod`**;
- **`fchmod`**;
- **`chown`**.

La prima system call che analizziamo è **`dup`**, la cui sinossi completa è:

```
int dup(int oldfd)
```

Tale system call serve a **duplicare il file descriptor `oldfd`, restituendo un nuovo file descriptor che però punterà allo stesso identico file**. Il nuovo file descriptor generato sarà il file descriptor più basso disponibile in quel momento (come si è accennato [[SO2_05 - System calls#Chiusura di un file|nello scorso paragrafo]]). Se la system call incappa in un errore durante la sua esecuzione, `dup` restituirà **`-1`**.

Vediamo, poi, una coppia di system calls che restituisce una sorta di **"carta d'identità" di un determinato file**, ossia **`stat`** e **`fstat`**. La sinossi completa di queste due system calls è: 

```
int stat(const char *path, struct stat *buf)
int fstat(int fd, struct stat *buf)
```

Entrambe queste system calls svolgono pressoché lo stesso ruolo: in caso di successo, **scrivono nell'area di memoria a cui punta `buf` le informazioni di stato del file specificato**, formattandole in una **[[SO2_04 - C#Strutture|struttura]] `stat`**; sia `stat` che `fstat`, inoltre, **restituiscono `0` in caso di successo**, e **`-1`** altrimenti. Il contenuto della struttura `stat` consiste in una serie di attributi che contengono dettagli riguardo il file considerato, tra cui:
- **`ino_t st_ino`**, ossia il **numero di [[SO2_02 - File system#Struttura di file e directory|inode]]** del file;
- **`mode_t st_mode`**, ossia il **tipo di file** e la sua **modalità**;
- **`nlink_t st_nlink`**, ossia il **numero di [[SO2_02 - File system#`ln`|hard links]]** associati a tale file;
- **`uid_t st_uid`**, ossia l'**ID dell'utente proprietario** del file;
- **`gid_t st_gid`**, ossia l'**ID del gruppo proprietario** del file;
- **`off_t st_size`**, ossia la **dimensione del file** (espressa in byte);

e altri ancora. In particolare, per "decodificare" le informazioni espresse dal campo `st_mode`, esistono alcune macro utili, tra cui:
- **`S_ISREG`**, che ritorna `true` se il file in questione è un file regolare;
- **`S_ISDIR`**, che ritorna `true` se il file in questione è una directory;
- **`S_ISLNK`**, che ritorna `true` se il file in questione è un link simbolico;
- **`S_ISSOCK`**, che ritorna `true` se il file in questione è una socket;
- **`S_ISFIFO`**, che ritorna `true` se il file in questione è una FIFO;

e così via. L'unica **differenza tra `stat` e `fstat`** sta nei loro parametri: **`stat` cerca il file a partire dal suo path** (relativo o assoluto), mentre **`fstat` cerca il file usando il suo file descriptor**.

Infine, diamo un'occhiata a un'altra coppia di system calls, che viene principalmente utilizzata per **modificare i [[SO2_02 - File system#Permessi di accesso ai file|permessi di accesso]] a un file**, ossia **`chmod`** e **`fchmod`**. La sinossi completa di queste due system calls è: 

```
int chmod(const char *pathname, mode_t mode)
int fchmod(int fd, mode_t mode)
```

Anche in questo caso, l'unica **differenza tra `chmod` e `fchmod`** sta nei loro parametri: **`chmod` cerca il file a partire dal suo path** (relativo o assoluto), mentre **`fchmod` cerca il file usando il suo file descriptor**. Concretamente, quello che fanno queste due system calls è manipolare i permessi di accesso al file considerato, aggiornandoli con i permessi specificati in **`mode`**: questo parametro può essere espresso sia in **codifica ottale**, sia utilizzando delle **maschere di bit poste in OR bit a bit** tra di loro. Ad esempio, alcune di queste maschere sono:
- **`S_ISUID`**, che permette di settare il **SetUID bit**;
- **`S_ISGID`**, che permette di settare il **SetGID bit**;
- **`S_ISVTX`**, che permette di settare lo **sticky bit**;
- **`S_IRUSR`**, che permette di settare il **permesso di lettura per l'utente proprietario**;
- **`S_IRGRP`**, che permette di settare il **permesso di lettura per il gruppo proprietario**;
- **`S_IROTH`**, che permette di settare il **permesso di lettura per gli altri utenti**.

Entrambe le system calls **restituiscono `0` in caso di successo**, e **`-1`** altrimenti.

Infine, vediamo la system call **`chown`**, la cui sinossi completa è:

```
int chown(const char *path, uid_t owner, gid_t group)
```

Lo scopo di `chown` è quello di **modificare l'ID dell'utente proprietario e del gruppo proprietario associati al file indicato da `path`**, sovrascrivendoli rispettivamente con **`owner`** e **`group`**.
___
##### Gestione delle directory

In questo paragrafo, vedremo **3 funzioni di libreria** e **3 system calls**, tutte molto importanti dato che rappresentano il modo principale per **lavorare con directory**. Le funzioni di libreria che approfondiremo sono tutte definite nell'header file **`dirent.h`**, e sono:
- **`DIR *opendir(const char *name)`**;
- **`struct dirent *readdir(DIR *dirp)`**;
- **`int closedir(DIR *dirp)`**.

La funzione **`opendir`** viene utilizzata per **aprire la directory**, **restituendo un puntatore a un oggetto di tipo `DIR`**, molto simile concettualmente al tipo `FILE` utilizzato per i file. L'unico parametro della funzione è **`name`**, ossia una **stringa contenente il percorso** (relativo o assoluto) **della directory da aprire**. In caso di errore, la funzione restituisce un **valore nullo `NULL`**.

Una volta aperta una directory e ottenuto un puntatore a un oggetto `DIR`, possiamo **leggere il contenuto della directory** utilizzando la funzione **`readdir`**: più nello specifico, `readdir` viene utilizzata per **leggere il prossimo elemento disponibile contenuto nella directory**, sia esso un file, una sotto-directory o un link. L'unico parametro della funzione è **`dirp`**, ossia un **puntatore all'oggetto `DIR` rappresentante la directory considerata**; il suo valore di ritorno, invece, è un **puntatore a una [[SO2_04 - C#Strutture|struttura]] di tipo `dirent`**, contenente varie informazioni riguardo all'entità appena letta, tra cui:
- **`ino_t d_ino`**, ossia il **numero di [[SO2_02 - File system#Struttura di file e directory|inode]] del file appena letto**;
- **`off_t d_off`**, ossia un **offset** utilizzato dal file system per capire a che punto della lettura della directory si è arrivati;
- **`unsigned short d_reclen`**, ossia la **lunghezza in byte del file appena letto**;
- **`unsigned char d_type`**, ossia il **tipo di file appena letto** (ad esempio, un file regolare ha tipo `DT_REG`, una directory ha tipo `DT_DIR`, un link simbolico `DT_LNK`, e così via);
- **`char d_name[256]`**, ossia il **nome del file appena letto**.

Se si sono esauriti gli elementi della directory, invece, `readdir` restituisce un valore nullo `NULL`.

Infine, una volta terminato il lavoro, per **chiudere una directory precedentemente aperta** si utilizza la funzione **`closedir`**: prende come unico parametro **`dirp`**, ossia un **puntatore alla directory da chiudere**, e restituisce **`0` in caso di successo**, e **`-1`** altrimenti.

Vediamo, ora, le system calls a cui avevamo accennato in precedenza, ossia:
- **`int mkdir(const char *pathname, mode_t mode)`**;
- **`int rmdir(const char *pathname)`**;
- **`int chdir(const char *pathname)`**.

La system call **`mkdir`** viene utilizzata per **creare una nuova directory, specificata nel path `pathname`**, con il parametro **`mode`** che, come per la system call `open`, definisce i **permessi di accesso iniziali alla nuova directory**.

La system call **`rmdir`** viene utilizzata per **eliminare la directory specificata nel path `pathname`**, directory che per poter essere eliminata deve necessariamente essere vuota, altrimenti l'esecuzione della system call fallirà.

La system call **`chdir`** viene utilizzata per **cambiare la `cwd`**, ossia la "Current Working Directory", **rendendola la directory specificata nel path `pathname`**. Si tenga a mente, utilizzando questa system call, che tale modifica ha effetto esclusivamente sul processo corrente.
___
##### Controllo avanzato dei file

[SLIDES: 11, slide 25/33 - 35/37]
___
## System calls per la gestione di processi

Prima di approfondire le **[[SO2_05 - System calls#Cos'è una system call?|system calls]] relative alla gestione di [[SO2_03 - Processi|processi]]**, facciamo un piccolo rimando ad alcuni concetti relativi a questi ultimi, soprattutto relativamente al loro **ciclo di vita**.

Nei sistemi Linux, c'è una rigida "**gerarchia dei processi**", una sorta di albero genealogico che ha sempre, come capostipite, il processo **`init`** (avente **[[SO2_03 - Processi#Come sono rappresentati i processi?|PID]]** pari a 1), processo che sarà quindi padre (o antenato) di tutti i processi in esecuzione. Un qualsiasi processo, primo su tutti `init`, può **creare un "processo figlio"** attraverso la system call **`fork`**, che va sostanzialmente a **duplicare il processo chiamante**, creando al contempo la relazione padre-figlio tra processo chiamante e processo creato. È proprio questo il meccanismo che sta alla base dell'intera gerarchia dei processi di un sistema, gerarchia che può essere visualizzata utilizzando il comando:

```
pstree
```

Ogni processo della gerarchia fa riferimento al suo processo padre, nel senso che:
- al momento della sua creazione, **il processo figlio eredita il codice sorgente e altri dati dal processo padre**;
- al momento della sua terminazione, **il processo figlio restituisce il suo "codice di uscita" al processo padre**.

Nel caso in cui **il processo padre termina la sua esecuzione prima del processo figlio**, quest'ultimo diventa "**orfano**" e viene subito "adottato" da `init`. Invece, più in generale, quando un processo termina la sua esecuzione, non viene subito eliminato dal calcolatore, ma entra in uno **stato "Zombie"** (**`Z`**), in cui l'esecuzione è effettivamente terminata ma **il suo PCB è mantenuto dal kernel in attesa che il processo padre legga il codice di uscita**; solo a quel punto il processo Zombie potrà essere veramente terminato ed eliminato. In casi di cattiva progettazione, può succedere anche che **il processo padre termini senza leggere il codice di uscita del processo figlio**, e in tal caso **il processo figlio rimarrà perennemente nello stato Zombie**, senza possibilità di essere terminato ed eliminato. 

Fatte queste premesse, siamo finalmente pronti ad approfondire le system calls utilizzate per la gestione dei processi. Possiamo, innanzitutto, dividere tali system calls in più categorie, in base al loro scopo:
- **[[SO2_05 - System calls#Getters di attributi di un processo|ottenimento e modifica degli attributi di un processo]]**;
- **[[SO2_05 - System calls#Creazione e terminazione di un processo|creazione e terminazione di un processo]]**;
- **[[SO2_05 - System calls#Sincronizzazione tra processi|sincronizzazione tra processi]]**;
- **[[SO2_05 - System calls#Eseguire altri programmi in un processo figlio|esecuzione di un nuovo programma in un processo]]**;
- **[[SO2_05 - System calls#Gestione dell'ambiente di un processo|gestione dell'ambiente di un processo]]**.

##### Getters e setters di attributi di un processo

Le prime system calls che andiamo a vedere sono quelle legate all'**ottenimento** e alla **modifica degli attributi di un processo**, ossia quelle che potremmo definire "**getters**" e "**setters**". Tutte le system calls che approfondiremo in questa sezione, per poter essere utilizzate, necessitano dell'inclusione degli header files **`sys/types.h`** e **`unistd.h`**.

Partiamo dalle system calls che servono per l'ottenimento di determinati attributi, tra cui:
- **`pid_t getpid()`**, che restituisce il **PID del processo chiamante**;
- **`pid_t getppid()`**, che restituisce il **PID del processo padre di quello chiamante**;
- **`uid_t getuid()`**, che restituisce il **[[SO2_03 - Processi#Come sono rappresentati i processi?|Real UID]] del processo chiamante**, ossia l'ID dell'utente che ha avviato il processo;
- **`uid_t geteuid()`**, che restituisce l'**Effective UID del processo chiamante**, ossia l'ID dell'utente che ha assunto il controllo del processo in esecuzione.

Tutte queste system calls **terminano sempre la loro esecuzione con successo**, dato che banalmente è garantito che ogni processo disponga degli attributi a cui fanno riferimento.

Passiamo, ora, alle system calls utilizzate per modificare determinati attributi, tra cui:
- **`int setuid(uid_t uid)`**, che tenta di **settare l'Effective UID del processo chiamante a `uid`**;
- **`int setgid(uid_t gid)`**, che tenta di **settare l'Effective GID del processo chiamante a `gid`**.

A differenza delle system calls viste prima, queste ultime due possono generare errori durante la loro esecuzione: in particolare, **restituiscono `0` se la modifica è avvenuta con successo**, mentre **restituiscono `-1` in caso di errore**, aggiornando il valore della variabile `errno` (spesso inserendoci il codice **`EPERM`**, che rappresenta un'operazione non permessa). Quest'ultimo scenario può avvenire quando un programma lanciato da un normale utente cerca di punto in bianco di assumere privilegi da `root`, chiamando ad esempio `setuid(0)`; tali operazioni, infatti, vanno a buon fine solo se il processo sta già venendo eseguito con privilegi da `root`, oppure se l'eseguibile del programma ha il bit [[SO2_02 - File system#Permessi di accesso ai file|bit SetUID]] settato a `1`.
___
##### Creazione e terminazione di un processo

Nonostante in altri OS (come, ad esempio, Windows) sia possibile creare processi "da zero", lo stesso non si può dire dei sistemi Linux e UNIX, in cui **l'unico modo per creare un nuovo processo è clonare un processo esistente, generando un processo figlio**. Per fare ciò, come accennato [[SO2_05 - System calls#System calls per la gestione di processi|in precedenza]], si utilizza la system call **`fork`**, la cui sinossi completa è:

```
pid_t fork()
```

Naturalmente, tale system call va a clonare il processo chiamante, e una sua caratteristica peculiare è che **a una sola sua chiamata corrispondono due valori di ritorno**: infatti, `fork()` **restituisce al processo padre il [[SO2_03 - Processi#Come sono rappresentati i processi?|PID]] del processo figlio appena creato**, mentre **restituisce al processo figlio `0`**. Invece, nel caso in cui ci sia un qualche errore e l'esecuzione fallisca, viene restituito semplicemente `-1` al processo padre, e nessun processo figlio viene mai creato.

Seppur, inizialmente, il processo figlio sia a tutti gli effetti un clone del processo padre, il primo non eredita tutto dal secondo. In particolare, **gli attributi e le risorse che vengono effettivamente ereditati** sono:
- il **Real UID** e **Real GID**;
- l'**Effective UID** e **Effective GID**;
- la **`cwd`**, o "current working directory";
- l'**ambiente** del processo (approfondiremo questo concetto [[SO2_05 - System calls#Gestione dell'ambiente di un processo|in seguito]]);
- i **descrittori dei file eventualmente aperti**;
- le **risorse condivise**.

Non vengono ereditati, invece:
- il **PID** e il **PPID**;
- eventuali **timer**;
- i **contatori dell'utilizzo delle risorse** del calcolatore;
- qualsiasi tipo di **lock**;
- la **coda dei segnali**.

Una volta eseguita con successo una chiamata a `fork()`, **entrambi i processi** (padre e figlio) **riprendono la loro esecuzione dalla riga di codice immediatamente successiva a tale chiamata**; è opportuno, dunque, distinguere due flussi di esecuzione separati per i due processi. Il modo più semplice ed efficace per farlo è proprio utilizzare il doppio valore di ritorno di `fork()`, implementando un'[[SO2_04 - C#L'`if` statement|if statement]] che controlla tale valore, come nel seguente esempio:

```
int pid = fork();
if (pid == 0)
{
	// Codice che verrà eseguito dal figlio...
}
else
{
	// Codice che verrà eseguito dal padre...
}
```

Per quanto riguarda la **terminazione di un processo**, la system call a cui facciamo riferimento è:

```
void _exit(int status)
```

Chiamare direttamente la system call `_exit` porta a una **terminazione "violenta" del processo chiamante**: non viene invocato alcun tipo di handler per gestire al meglio la terminazione, tutti i descrittori di file eventualmente aperti vengono subito chiusi, tutti gli eventuali processi figli vengono ereditati dal processo `init`, il processo padre riceve un segnale `SIGCHLD` come "avviso" della terminazione del figlio, e il processo chiamante viene subito trasformato in un processo Zombie, in attesa che il padre ne legga il codice di uscita. La system call **restituisce il codice `status`**, oltre al codice di uscita del processo.

Spesso, però, si vuole evitare una terminazione "violenta" di un processo, in favore piuttosto di una terminazione più graduale e schematica; in questi casi, la system call `_exit` viene utilizzata indirettamente, attraverso la **funzione di libreria `exit`**, la cui sinossi completa è:

```
void exit(int status)
```

Prima di invocare la system call quasi omonima, `exit` invoca tutti gli handler previsti (anche eventuali handler personalizzati, implementati dal programmatore) e svuota tutti i buffer e i canali eventualmente rimasti in sospeso. 

Per poter utilizzare la system call `_exit`, si dovrà includere l'header file **`unistd.h`**, mentre per utilizzare la funzione di libreria `exit` si dovrà includere **`stdlib.h`**.

C'è, però, un altro modo ancora per terminare un processo, che si utilizza in contesti in cui **il programma si trova in una situazione "anormale", critica o non recuperabile**, in cui dunque non è possibile un'uscita pulita come avverrebbe con `exit`. In tal caso, si utilizza:

```
void abort()
```

Tale **funzione di libreria** (che richiede l'inclusione di **`stdlib.h`** per essere utilizzata) fa in modo che **il processo chiamante invii a sé stesso un segnale `SIGABRT`**, che risulta in una "terminazione anormale" del processo. Tale segnale può essere intercettato e gestito dal programma in questione, ma il processo verrà comunque terminato appena possibile.
___
##### Sincronizzazione tra processi

Passiamo, ora, alle system calls utilizzate per **sincronizzare l'esecuzione dei processi**. In particolare, le due system calls che approfondiremo sono:
- **`pid_t wait(int *status)`**;
- **`pid_t waitpid(pid_t pid, int *status, int options)`**.

[SLIDES: 12, slide 16/20]
___
##### Eseguire altri programmi in un processo figlio

[SLIDES: 12, slide 23/28]
___
##### Gestione dell'ambiente di un processo

[SLIDES: 12, slide 29/31 - 33]
___