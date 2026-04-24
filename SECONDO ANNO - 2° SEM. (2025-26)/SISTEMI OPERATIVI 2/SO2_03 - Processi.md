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



[SLIDES: 04 - pag. 10/15]
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