## Cos'è un processo?

In sistemi Unix e Linux, l'intero funzionamento del calcolatore si basa su due entità fondamentali:
- i **file**, che rappresentano risorse vere e proprie, contenenti dati e programmi;
- i **processi**, che permettono di elaborare tali dati e di utilizzare le risorse di sistema.

Ma **cos'è**, concretamente, **un processo?** Possiamo vederlo, in parole povere, come **un'istanza di un programma in esecuzione**: in altre parole, un processo "nasce" sempre da un programma o un file eseguibile, e rappresenta l'esecuzione effettiva di tale programma (possono esistere anche più processi che eseguono lo stesso programma simultaneamente).

Per **creare**, o in altre parole **"lanciare" un processo** si dovrà dunque **eseguire il file corrispondente**, digitandone il nome nella [[SO2_01 - Shell|shell]] come fosse un normale comando o cliccando sull'icona corrispondente. Ad esempio, molti dei comandi visti in precedenza (come `dd`, `ls`, `cat`, `cp`, `ln`, `adduser`, `groups`, `sudo`, `su` e altri ancora) creano dei processi al momento della loro esecuzione, mentre altri (come `echo` o `cd`) non creano processi a sé stanti, ma vengono piuttosto eseguiti all'interno del processo della shell.

Come anticipato, **un file può essere eseguito più volte, dando vita a un nuovo processo ogni volta**, e non occorre aspettare il termine dell'esecuzione prima di lanciarlo nuovamente. Ciò è possibile grazie alla natura **multi-processo** dei sistemi Unix e Linux.

##### Canali standard

Ogni processo in un sistema Unix o Linux ha tipicamente accesso ad **almeno tre "canali"**, ossia dei **file speciali** che rappresentano una sorta di **flusso di dati** (detto, perciò, anche "**stream**"):
- lo "**standard input**", abbreviato spesso in **`stdin`**;
- lo "**standard output**", abbreviato spesso in **`stdout`**;
- lo "**standard error**", abbreviato spesso in **`stderr`**.

Il primo, ossia `stdin`, rappresenta un **flusso di dati in ingresso al processo**, che riceve dati tipicamente dalla **tastiera** e che viene identificato con il **descrittore file `0`**; il secondo, ossia `stdout`, rappresenta un **flusso di dati in uscita dal processo**, che tipicamente **stampa sullo schermo** e che viene identificato con il **descrittore file `1`**; infine, il terzo, ossia `stderr`, rappresenta un **flusso per eventuali messaggi di errore o di diagnostica**, che tipicamente **stampa sullo schermo** e che viene identificato con il **descrittore file `2`**.

Ora, seppur abbiamo specificato dei "mezzi" di default per ciascuno di questi tre canali standard, tutti e tre **possono essere "ridirezionati" in modo indipendente**. Per fare ciò con i canali di un comando eseguito da terminale, si utilizzeranno le **parentesi angolari** (**`<`** e **`>`**), con la seguente sintassi:

```
[descrittore_canale] > file
```

dove `descrittore_canale` è il descrittore file del canale standard (`0`, `1` o `2`), che se omesso assume il valore di default `1` (indicando, dunque, lo `stdout`), mentre `file` è il nome del file dove ridirezionare il flusso indicato. Ad esempio, eseguire:

```
ls > dirlist
```

vuol dire eseguire il comando `ls` e ridirezionare il suo `stdout` sul file `dirlist`, dunque in altre parole scrivere in `dirlist` l'output del comando (in questo caso, una lista dei file e cartelle contenuti nella cartella corrente). Al tempo stesso, eseguire:

```
ls cartella_non_esistente 2> errori.log
```

vuol dire eseguire il comando `ls` su una cartella `cartella_non_esistente` che non esiste nel file system, portando dunque a un fallimento del comando e cioè alla stampa di un errore tramite `stderr`, tuttavia visto che tale flusso viene ridirezionato sul file `errori.log` non verrà stampato nulla a schermo.

L'operatore **`<`**, invece, viene utilizzato per **ridirezionare l'input** (dunque, invece di aspettare dati dalla tastiera, il comando leggerà dati da un file). Ad esempio, eseguire:

```
sort < nomi.txt
```

vuol dire eseguire il comando `sort` non sull'input digitato da tastiera, come accadrebbe di default, ma sulle righe di testo lette dal file `nomi.txt`.

Oltre agli operatori `>` e `<`, esiste anche **`>>`**, che funziona pressoché allo stesso modo di `>`, con la differenza che, se il file di destinazione esiste già, va a **aggiungere i dati alla fine** dello stesso, senza cancellare il contenuto precedente del file.

Nell'utilizzare gli operatori di ridirezionamento, un ulteriore operatore fondamentale da conoscere è **`&`**, che sostanzialmente coincide con "**copia il descrittore di…**": se, ad esempio, scriviamo `2>&1`, stiamo imponendo di far puntare `stderr` allo stesso posto a cui sta puntando attualmente `stdout`. Inoltre, **la shell legge le ridirezioni da sinistra verso destra**. Se, ad esempio, si esegue:

```
ls > dirlist 2>&1
```

si sta ridirezionando lo `stdout` di `ls` nel file `dirlist`, e in seguito si ridireziona `stderr` sullo stesso canale a cui è attualmente assegnato `stdout`, che per il ridirezionamento precedente è diventato proprio il file `dirlist` (in parole povere, sia `stdout` che `stderr` verranno ridirezionati sul file `dirlist`). Ancora, se eseguissimo:

```
ls 2>&1 > dirlist
```

andremmo prima a ridirezionare `stderr` sullo stesso flusso a cui punta `stdout` (lo schermo, dunque in realtà non cambia nulla), e poi a ridirezionare `stdout` nel file `dirlist`; in seguito a ciò, `dirlist` conterrà dunque solo lo `stdout` e non lo `stderr`.
___
##### Come sono rappresentati i processi?

Per poter gestire i vari processi, l'OS deve avere un modo per **rappresentare un processo nella memoria principale**. Ciò avviene principalmente grazie a due elementi:
- il **PID**, o **Process ID**;
- il **PCB**, o **Process Control Block**.

Il **PID**, come suggerisce il nome, è un **numero identificativo univoco** assegnato al momento della creazione del processo (dunque, nessun'altro processo in esecuzione avrà lo stesso PID di un altro); **quando un processo termina la sua esecuzione, il suo PID viene liberato** e diventa di nuovo eventualmente disponibile per nuovi processi. In sistemi moderni come Linux, **l'assegnazione dei PID spesso avviene in modo casuale** per motivi di sicurezza. 

Il **PCB**, invece, rappresenta una sorta di **"documento d'identità" per un processo**, mantenuto costantemente aggiornato dal kernel dell'OS. **Ogni processo ha un PCB unico**, e ogni PCB contiene tutte le informazioni fondamentali che l'OS deve sapere su ogni processo, tra cui:
- il **PID** del processo;
- il **PPID** (**Parent Process ID**), ossia il PID del padre del processo;
- il **Real UID** (**Real User ID**), ossia l'ID dell'utente che ha avviato il processo;
- il **Real GID** (**Real Group ID**), ossia l'ID del gruppo a cui appartiene l'utente che ha avviato il processo;
- l'**Effective UID** (**Effective User ID**), ossia l'ID dell'utente che ha assunto il controllo del processo in esecuzione;
- l'**Effective GID** (**Effective Group ID**), ossia l'ID del gruppo dell'utente che ha assunto il controllo del processo in esecuzione;
- il **Saved UID** (**Saved User ID**),
- il **Saved GID** (**Saved Group ID**),
- la **current working directory**, ossia la [[SO2_02 - File system|directory]] all'interno della quale sta venendo eseguito il processo;
- la **[[SO2_02 - File system#`umask`|umask]]**;
- la "**Nice**", che indica la priorità statica del processo.

[SLIDES: 04 - pag. 12 - 13

Oltre a PID e PCB, ogni processo dispone di un proprio **spazio di indirizzamento**, ossia di una propria area di memoria nella memoria principale, diviso in **sei aree fondamentali**:
- **Text Segment** (tipicamente accessibile in sola lettura per evitare corruzione dei dati), che contiene le istruzioni in linguaggio macchina da mandare al processore per proseguire l'esecuzione del processo (se si lanciano più istanze dello stesso programma, questo segmento potrebbe essere condiviso per risparmiare memoria);
- **Data Segment**, che contiene le variabili globali o statiche inizializzate in modo esplicito all'interno del codice;
- **BSS Segment**, che contiene le variabili globali o statiche non inizializzate; 
- **Heap**, che rappresenta lo spazio destinato all'[[SO2_04 - C#Allocazione dinamica di memoria|allocazione dinamica di memoria]], controllata dal programmatore durante l'esecuzione del programma tramite funzioni come `malloc`, `calloc` o `free` (si approfondirà l'argomento in seguito);
- **Memory Mapping Segment**, che contiene dati e informazioni relative a librerie esterne dinamiche usate dal processo;
- **Stack**, che contiene le variabili locali e non statiche, oltre che tutte le informazioni relative alle varie chiamate a funzione (parametri passati, indirizzi di ritorno, ecc. ecc.); a differenza del Text Segment, o anche del BSS Segment e del Memory Mapping Segment, lo Stack di un processo non è mai condiviso.
___
##### Stati di un processo

[SLIDES: 04 - pag. 16]
___
##### Esecuzione dei processi

[SLIDES: 04 - pag. 17 - 18 - 21 - 22]
___
## Comandi per la gestione dei processi

[SLIDES: 04 - pag. 18/20 - 24/30 - 32 - 34/36 - 38/41]
___