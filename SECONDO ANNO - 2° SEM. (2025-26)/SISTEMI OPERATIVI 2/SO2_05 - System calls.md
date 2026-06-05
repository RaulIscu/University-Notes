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

[SLIDES: 10, slide 30/32]
___
## System calls per la gestione di file e directory

[SLIDES: 11, slide 4/16 - 18/21 - 23 - 25/33 - 35/37]
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