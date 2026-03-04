Il **file system** è una delle componenti più importanti, se non la più importante, di un calcolatore e del suo funzionamento. Concretamente, un file system è un'**organizzazione di un'area di memoria di massa**, generalmente basata su due concetti fondamentali:
- il "**file**";
- la "**directory**".

Mentre il primo rappresenta un **insieme effettivo di dati**, il secondo è più che altro un **contenitore**, che può contenere sia file che altre directory. Un file system di questo tipo può essere formalizzato secondo una **struttura gerarchica ad albero**, in cui **solo le directory possono avere figli**, e dunque in cui **i file sono sempre foglie**. In particolare, si può effettuare una distinzione tra "**file regolari**" e "**file non regolari**": mentre i primi sono quelli a cui siamo abituati, ossia sequenze di bit conservate nell'area di memoria di competenza del file system considerato, i secondi hanno forme diverse e vengono utilizzati per scopi particolari, ad esempio per l'accesso di basso livello a periferiche o dispositivi vari.

Un singolo calcolatore, a seconda del caso e delle scelte architetturali, può supportare **uno o più file system**. Ad esempio, di default, **i sistemi Linux e Unix hanno un solo file system principale**, che ha come "directory radice" la directory **`/`**, spesso chiamata anche **`root`**: di conseguenza, tutti i file e le directory del file system saranno contenute nella cartella `/`.

Ricordiamo alcune **regole per la nomina di file e directory**. Infatti, all'interno di una stessa directory, è impossibile creare:
- due file con lo stesso nome;
- due directory con lo stesso nome;
- un file e una directory con lo stesso nome.

Inoltre, i nomi di file e directory sono **case-sensitive**, dunque due nomi che presentano gli stessi caratteri ma che variano in termini di lettere maiuscole o minuscole verranno considerati diversi.
## Il path

Ogni file e directory all'interno di un file system è raggiungibile seguendo un "**path**", ossia letteralmente un percorso, un cammino verso tale entità. Dato che tutto ciò che è contenuto in un file system è contenuto nella sua directory radice (nel nostro caso, `/`), di conseguenza **qualsiasi file o directory è raggiungibile seguendo un "path assoluto" che parte dalla cartella radice**. Ad esempio, il path:

```
/home/utente1/dir1/dir11/dir112/file.pdf
```

punta al file `file.pdf`, che è contenuto nella directory `dir112/`, che è contenuta a sua volta nella directory `dir11/`, e così via fino ad arrivare proprio alla directory radice `/`. Dato che capita spesso che i file e directory di interesse si trovino all'interno della cartella relativa all'utente loggato in quel momento, in molti casi si può **abbreviare la parte `/home/user` del path in `~`**, ad esempio:

```
~/dir1/dir11/dir112/file.pdf
```

Come si è accennato parlando di [[SO2_01 - Shell#Prompt e comandi|prompt]] nella shell, **qualsiasi comando** venga eseguito dall'utente all'interno di quest'ultima **viene eseguito "all'interno" di una directory**, ossia la directory in cui si sta attualmente lavorando, detta anche "**current working directory**", o **`cwd`** in breve. Oltre ad essere indicata come parte del prompt, la `cwd` può essere anche ottenuta eseguendo il comando:

```
pwd
```

Naturalmente, in base alle proprie esigenze, è possibile **cambiare la `cwd`**: per fare ciò, si utilizza il comando:

```
cd
```

Chiamare il comando **`cd`** senza [[SO2_01 - Shell#Approfondimento sulle opzioni|opzioni]] rende la directory **`/home/user`** la `cwd`; il più delle volte, invece, si inserirà come opzione un path, che può essere assoluto (a partire dalla directory radice `/`) o relativo (una directory all'interno della `cwd`). Inoltre, è possibile utilizzare come opzione anche **`..`** per recarsi nella directory "genitore" della `cwd`, o **`.`** per rimanere nella `cwd` attuale.
___
## Contenuto di una directory

Essendo buona parte delle azioni che possiamo eseguire nella [[SO2_01 - Shell|shell]] legata al file system e alle directory e file contenuti al suo interno, ci è utile poter ottenere informazioni su di essi, ad esempio sul **contenuto di una directory**. Il comando più importante in questo contesto è senza dubbio:

```
ls
```

Consultando le istruzioni ottenibili tramite il comando `man ls` si possono vedere nel dettaglio tutte le potenzialità di questo comando. Ci sono, ciononostante, alcuni casi di utilizzo principali che analizzeremo qui. Ad esempio, chiamare il comando `ls` senza ulteriori [[SO2_01 - Shell#Approfondimento sulle opzioni|opzioni]] stamperà nel terminale un **elenco del contenuto della `cwd`**; alternativamente, si può fare una chiamata del tipo:

```
ls nomedir
```

per ottenere un elenco del genere riguardante però la directory `nomedir`. 

Utilizzando l'opzione **`-a`** o **`--all`**, si potranno visualizzare anche eventuali **file nascosti** che contenuti nella directory in questione (tipicamente si tratta di file di configurazione o di supporto a comandi e applicazioni, ad esempio `.bash_history` che contiene la cronologia dei comandi eseguiti o `.bashrc` che contiene la configurazione della shell `bash`).

Invece, se non vogliamo fermarci alla directory considerata, ma vogliamo **visualizzare ricorsivamente anche il contenuto delle sotto-directory**, potremo utilizzare l'opzione **`-R`**, o **`--recursive`**.

È inoltre possibile **visualizzare un albero delle directory**, con radice in quella considerata (la `cwd` o un'altra indicata al momento della chiamata del comando) sfruttando il comando:

```
tree
```

Anch'esso accetta varie opzioni facoltative, tra cui:
- **`-a`**, che impone al comando di stampare tutti i file contenuti nell'albero considerato (di default, i file non verrebbero stampati);
- **`-d`**, che impone al comando di elencare solo ed esclusivamente le directory;
- **`-f`**, che impone al comando di stampare il [[SO2_02 - File system#Il path|path]] completo per arrivare a ciascun file mostrato come prefisso dello stesso;
- **`-L level`**, che impone un limite massimo alla profondità dell'albero di directory stampato dal comando;
- **`-x`**, che impone al comando di rimanere all'interno del file system corrente (naturalmente, tale opzione ha senso di essere utilizzata solo nel momento in cui il sistema su cui si sta lavorando presenta più file system).
___
## Creazione di directory e file

Per **creare una directory**, lo strumento più comune e veloce è il comando:

```
mkdir nomedir
```

dove **`nomedir`** è il **nome da assegnare alla directory vuota** che viene creata (è opportuno specificare che tale directory verrà creata all'interno della [[SO2_02 - File system#Il path|current working directory]]). Utilizzando questo comando, sarà possibile anche creare **path di directory**, specificando il path da seguire a partire dalla `cwd` per arrivare alla directory "foglia" del path, dunque a quella finale (per fare ciò, è opportuno inserire anche l'opzione **`-p`**, o **`--parents`**, che permetterà al comando di creare le opportune cartelle "genitore" ove necessarie).

Per **creare un file**, invece, tipicamente si utilizza il comando:

```
touch nomefile
```

dove **`nomefile`** è il **nome da assegnare al file vuoto** che viene creato (anche in questo caso, il file viene creato nella `cwd`). Per **modificare**, poi, **il contenuto del file**, si potranno sfruttare comandi come **`nano`**, **`pico`**, **`gedit`**, **`vi`** e simili.
___
## Mounting, partizioni e tipi di file system

[SLIDES: 02 - slide 20/27]
___
## Utenti e gruppi di utenti nel file system

All'interno del file system, **utenti** e **gruppi di utenti** si trovano all'interno del [[SO2_02 - File system#Il path|path]] **`/etc`**, e in particolare dentro la directory `etc` ci sono due directory che contengono rispettivamente utenti e gruppi di utenti:
- in **`/etc/passwd`** si trovano tutti gli utenti;
- in **`/etc/group`** si trovano tutti i gruppi di utenti.

[SLIDES: 02 - slide 29/32]
___
## Struttura dei file

[SLIDES: 02 - slide 34/42]
___
## Permessi di accesso ai file

Non tutti gli utenti possono accedere allo stesso modo ai file del sistema: per questo, esistono vari **gradi di accesso** ai file, che possono essere modificati per stabilire cosa può fare un determinato utente con un determinato file. In generale, è l'**utente proprietario** (solitamente chi ha creato il file o la directory) che definisce i permessi di accesso.

Un utente può avere sostanzialmente **tre tipi di permesso di accesso** a un file o directory:
- può **leggere il file** o **elencare i file della directory** (**`r`**);
- può **modificare il file** o **creare ed eliminare file della directory** (**`w`**);
- può **eseguire un file** o **entrare all'interno della directory** (**`x`**).

È possibile avere o non avere qualsiasi combinazione di questi tre tipi di permesso, dunque è molto comodo **codificare le possibili combinazioni di permessi con una cifra ottale**. Possiamo riassumerle nella seguente tabella:

| Permesso | Ottale | Significato                                                                                                                                                                                          |
| -------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ---      | 0      | Nessun accesso (sia file che directory)                                                                                                                                                              |
| --x      | 1      | Sola esecuzione del file (non si può leggere il codice); sola "traversata" della directory (non si può conoscere il contenuto)                                                                       |
| -w-      | 2      | Sola scrittura o sovrascrittura del file (non lettura); nessuna azione possibile in una directory                                                                                                    |
| -wx      | 3      | Modifica ed esecuzione del file; entrata e traversata della directory, creazione e cancellazione di file al suo interno, ma non si può conoscere effettivamente il suo contenuto                     |
| r--      | 4      | Sola lettura del file; si può conoscere il contenuto della directory, ma non ci si può entrare né si possono manipolare i file contenuti al suo interno                                              |
| r-x      | 5      | Lettura ed esecuzione del file; si può entrare nella cartella, conoscerne il contenuto e leggere i file al suo interno, ma non si può modificare nulla                                               |
| rw-      | 6      | Lettura e scrittura del file; si può conoscere il contenuto della directory e tecnicamente anche modificarne i file, ma quest'ultima operazione è in realtà impossibile perché non ci si può entrare |
| rwx      | 7      | Controllo totale (sia file che directory)                                                                                                                                                            |

Nel modificare i permessi di accesso per un file o directory, **si possono specificare permessi diversi per utenti o gruppi di utenti diversi**. In particolare, generalmente si contemplano tre categorie di utenti:
- l'**utente proprietario**, abbreviato in **`u`**;
- il **gruppo di utenti a cui è assegnato il file** (di default è quello dell'utente proprietario, ma può variare), abbreviato in **`g`**;
- **tutti gli altri utenti** (quindi tutti gli utenti che non sono né l'utente proprietario né inclusi nel gruppo `g`), abbreviato in **`o`**.

Per ciascuno di questi livelli si definisce una combinazione di permessi specifica, quindi tecnicamente ogni file o directory dovrebbe presentare come "**attributi di accesso**" tre cifre ottali. Tuttavia, spesso queste tre cifre sono precedute da una quarta, che rappresenta i cosiddetti **permessi speciali**

[SLIDES: 02 - slide 46/61]
___
## Altri comandi utili per il file system

[SLIDES: 03]
___