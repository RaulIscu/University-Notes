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

In sistemi Linux, come abbiamo accennato in precedenza, tutto il file system è contenuto all'interno di un'unica directory radice, chiamata `/` o `root`. Quando diciamo "tutto", non intendiamo però solo i file effettivamente contenuti sulla memoria a disco del calcolatore, ma anche eventuali **elementi eterogenei**, come:
- dischi magnetici;
- chiavette USB;
- file system di rete;
- file system virtuali;
- file system in memoria principale.

Ciò è possibile grazie al meccanismo del "**mounting**", o **montaggio**. Sostanzialmente, supponendo ad esempio di voler leggere una chiavetta USB, quello che succede a livello di memoria è che **la directory radice della chiavetta viene "montata" su una directory specifica della memoria a disco del calcolatore**: nel concreto, ciò vuol dire che finché l'elemento considerato (in questo caso, la chiavetta USB) è montato la directory scelta fungerà da nuova directory radice di tale elemento. Ad esempio, avendo la seguente coppia di file system principale e di file system di una chiavetta USB:

![[mounting_esempio.png]]

e supponendo di voler montare la chiavetta sulla directory `/media` del file system principale, si otterrebbe una situazione del genere:

![[mounting_esempio1.png]]

in cui, concretamente, è come se la directory `/media` fosse diventata la nuova radice della chiavetta USB (naturalmente, una volta "smontata" la chiavetta, a meno di altre modifiche i due file system torneranno nella situazione iniziale). **Qualsiasi directory del sistema può diventare un "punto di mount" per un altro file system**. Va ricordata, però, una particolarità: nel caso in cui la directory scelta contenesse già dei file, questi ultimi **diventeranno invisibili finché il nuovo file system non verrà smontato**; essi non verranno dunque eliminati dalla directory, ma diventeranno momentaneamente inaccessibili.

Una singola memoria a disco, eventualmente, può essere suddivisa in due o più "**partizioni**", che possiamo definire sostanzialmente come **sezioni virtuali di memoria indipendenti tra di loro**. Ad esempio, è possibile all'interno di un sistema Linux creare una partizione $A$ destinata esclusivamente al sistema operativo (e montarla, ad esempio, sulla radice `/`), e in seguito una partizione $B$ che contenga invece i dati personali degli utenti (e montarla sulla directory `/home`). Il concetto di partizione fornisce, come si può facilmente intuire, **maggiore flessibilità e sicurezza**: ad esempio, nell'eventualità in cui il sistema operativo venga corrotto in qualche modo, i dati personali non verrebbero sfiorati trovandosi in un'altra partizione; ancora, partizionare il disco in questo modo permette anche di installare diverse versioni di Linux senza dover copiare ogni volta i vecchi dati, ma smontando e rimontando la partizione dei dati personali come necessario. 

In Linux, un file system non assume sempre la stessa forma, tant'è che possono esserci **diversi tipi di file system**. Alcuni dei principali sono:
- **Ext2**;
- **Ext3**;
- **Ext4**;
- **ReiserFS**.

In base al tipo di file system, cambiano alcune caratteristiche relative soprattutto a **limiti di grandezza su file, nomi di file e partizioni**, così come al meccanismo di "**journaling**", che sfrutta un registro speciale per prevenire la corruzione dei dati nel caso venga interrotta improvvisamente la corrente. Possiamo riassumere tali caratteristiche nella seguente tabella:

| Tipo di FS | Limite di grandezza<br>sulle partizioni | Limite di grandezza<br>sui file | Limite di grandezza<br>sui nomi dei file | Journaling |
| ---------- | --------------------------------------- | ------------------------------- | ---------------------------------------- | ---------- |
| Ext2       | 32 TB                                   | 2 TB                            | 255 byte                                 | NO         |
| Ext3       | 32 TB                                   | 2 TB                            | 255 byte                                 | SI         |
| Ext4       | 1000 TB                                 | 16 TB                           | 255 byte                                 | SI         |
| ReiserFS   | 16 TB                                   | 8 TB                            | 4032 byte                                | SI         |

Oltre a questi, ci sono ovviamente anche **tipi di file system non tipici di Linux**, ad esempio come quelli tipici di Windows, tra cui:
- NTFS;
- MSDOS;
- FAT16;
- FAT32;
- FAT64.

Per fortuna, Linux risulta essere **molto compatibile anche con altri file system** (ad esempio, file system di tipo FAT16, FAT32, FAT64 e NTFS possono facilmente essere montati).

Per **eseguire un mounting**, così come **visualizzare informazioni sui file system attualmente montati**, il comando più importante è **`mount`**. La sinossi del comando `mount` è principalmente la seguente:

```
mount [OPZIONI...] [-t type] [OPZIONI...] device mountpoint
```

Tralasciamo, per ora, le opzioni `OPZIONI...`, e concentriamoci sulle altre componenti. Il parametro **`device`** corrisponde al **percorso del file speciale che rappresenta la partizione da montare**: generalmente, in Linux, i dispositivi si trovano nella cartella **`/dev`** (ad esempio, una chiavetta USB potrebbe rientrare nel percorso `/dev/sdb1`, mentre un CD nel percorso `/dev/cdrom`). Invece, il parametro **`mountpoint`** corrisponde alla **[[SO2_02 - File system|directory]] del sistema principale in cui montare il `device`** (si tenga a mente che tale directory deve già esistere in precedenza). Per quanto riguarda il parametro **`-t type`**, **opzionale**, esso indica il **tipo di file system che si sta montando**; si tratta di un parametro spesso non necessario, essendo i sistemi moderni solitamente in grado di riconoscere da soli questa informazione, ma in alcuni contesti è fondamentale per evitare errori; i tipi `type` più usati sono:
- **`ext2`**;
- **`ext3`**;
- **`ext4`**;
- **`btrfs`** (file system a B-tree);
- **`reiserfs`**;
- **`vfat`** (FAT16 e FAT32);
- **`exfat`** (FAT64 e exFAT);
- **`ntfs`**;
- **`msdos`**.

Per **visualizzare i file system montati in un istante preciso**, si può eseguire il comando:

```
cat /etc/mtab
```

Invece, per **visualizzare le partizioni caricate automaticamente dal sistema all'accensione**, si può eseguire il comando:

```
cat /etc/fstab
```
___
## Utenti e gruppi di utenti nel file system

All'interno del file system, **utenti** e **gruppi di utenti** si trovano all'interno del [[SO2_02 - File system#Il path|path]] **`/etc`**, e in particolare dentro la directory `etc` ci sono due directory che contengono rispettivamente utenti e gruppi di utenti:
- in **`/etc/passwd`** si trovano tutti gli utenti;
- in **`/etc/group`** si trovano tutti i gruppi di utenti.

I file in questione sono organizzati per righe, ciascuna contenente vari campi separati dal carattere `:`. Ad esempio, il file **`passwd`** ha la seguente struttura:

```
username:password:uid:gid:gecos:homedir:shell
```

anche se, generalmente, al posto della `password` si trova soltanto una `x`, dato che la password dell'utente è generalmente cifrata. Invece, il file **`group`** ha la seguente struttura:

```
groupname:password:groupID:listautenti
```

dove gli utenti contenuti nella `listautenti` sono separati da virgole, e dove anche in questo caso la password è cifrata.
___
## Struttura di file e directory

All'interno del file system, ogni file è rappresentato da una **struttura dati** detta "**inode**", e ogni inode è univocamente identificato da un "**inode number**"; dunque, la cancellazione di un file implica la liberazione dell'inode number in questione, che potrà quindi essere riutilizzato quando necessario per un nuovo file. Si può visualizzare la **struttura dell'inode** nel modo seguente:

![[inode_struttura.png]]

Come si può vedere, si tratta di una struttura relativamente complessa, dotata di vari attributi e componenti. Vediamo i **principali attributi dell'inode** più nel dettaglio:
- "**type**", che indica il **tipo di file** considerato (può essere regular, block, FIFO);
- "**user ID**", che indica l'**ID dell'utente proprietario** del file considerato;
- "**group ID**", che indica l'**ID del gruppo** a cui è associato il file considerato;
- "**mode**", che indica i **[[SO2_02 - File system#Permessi di accesso ai file|permessi di accesso]]** al file considerato per il proprietario, per il gruppo associato e per gli altri utenti (si approfondiranno nel paragrafo successivo);
- "**size**", che indica la **dimensione del file** considerato in byte;
- "**timestamps**", che contiene alcuni tempi importanti per il file considerato, tra cui il **`ctime`**, o "**inode changing time**" (il momento in cui è avvenuto l'ultimo cambiamento di un attributo dell'inode), il **`mtime`**, o "**content modification time**" (il momento in cui è avvenuta l'ultima scrittura del file), e il **`atime`**, o "**content access time**" (il momento in cui è avvenuta l'ultima lettura del file);
- "**link count**", che indica il **numero di [[SO2_02 - File system#`ln`|hard links]]** associati al file considerato (anche questo concetto verrà approfondito in seguito);
- "**data pointers**", ossia **puntatori alle varie liste di blocchi** che compongono concretamente il file considerato.

All'interno della memoria, che in sistemi Linux viene divisa in "Block Groups", gli inode si trovano in una sezione particolare di ciascun block group chiamata "**Inode Table**". Oltre all'inode table, un block group contiene anche le seguenti sezioni:
- "**Super Block**" e "**Group Descriptors**", due sezioni che contengono informazioni globali sul file system (ad esempio quanto è grande, quanti blocchi liberi ci sono, ecc.);
- "**Data Block Bitmap**" e "**Inode Bitmap**", due sezioni che contengono delle "bitmap", ossia sequenze lunghissime di bit che permettono al sistema di avere informazioni sulla situazione della memoria più velocemente (ad esempio, nella Data Block Bitmap, ogni bit corrisponde sostanzialmente a un preciso blocco di memoria fisica, e se il bit vale `0` allora tale blocco è libero e disponibile a essere scritto, mentre se vale `1` il blocco è occupato);
- "**Data Blocks**", la sezione più grande del Block Group, dove vengono salvati i dati effettivi dei vari file.

Abbiamo, quindi, ben capito come è strutturato internamente un file. Ma qual è, invece, la **struttura di una directory**? In realtà, **una directory non è altro che un "file speciale"**, il cui inode punta a un blocco di dati che funge da **tabella di associazione**: all'interno di tale tabella, si può trovare una lista dei nomi dei file e delle directory contenute all'interno della directory considerata, e a ciascuno di questi nomi è associato il rispettivo inode. Dunque, concretamente la directory funziona come una sorta di **"rubrica" per i suoi contenuti**: se, ad esempio, il sistema vuole accedere a un file contenuto in una certa directory, esso accederà prima all'inode della directory in questione, arrivando così al blocco di dati associato ad essa, poi cercherà il nome del file desiderato nella tabella di associazione e, una volta trovato, leggerà l'inode e procederà a cercare quest'ultimo nell'Inode Table, in modo da poter accedere ai blocchi di memoria in cui sono memorizzati i contenuti effettivi del file. Vediamo un esempio di questo procedimento nella seguente immagine, che ipotizza di star cercando un file `hello.txt` nella directory `/home/ealtieri`:

![[inode_directory_esempio.png]]

È possibile, attraverso il comando **`ls`**, **visualizzare le informazioni contenute nell'inode**. Ad esempio, eseguendo il comando nel modo seguente:

```
ls -i filename
```

verrà stampato l'inode number del file `filename`, seguito proprio dal nome del file. Invece, eseguendo il comando nel modo seguente:

```
ls -l filename
```

verranno stampate varie informazioni riguardo al file (in ordine, i permessi di accesso al file, il numero di directory contenute all'interno dell'eventuale directory, l'utente proprietario, il gruppo a cui è associato il file, l'`mtime`, e infine il nome del file stesso). Per visualizzare, invece del nome esteso di utente e gruppo, i rispettivi ID, si può aggiungere l'opzione **`-n`**. Invece, per vedere anche gli altri timestamps del file basterà aggiungere, oltre all'opzione `-l`, le seguenti opzioni:
- **`-c`** per il `ctime`;
- **`-u`** per l'`atime`.
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

Per ciascuno di questi livelli si definisce una combinazione di permessi specifica, quindi tecnicamente ogni file o directory dovrebbe presentare come "**attributi di accesso**" tre cifre ottali. Tuttavia, spesso queste tre cifre sono precedute da una quarta cifra ottale, che rappresenta i cosiddetti **permessi speciali**. Tale cifra ottale è naturalmente rappresentabile con 3 bit binari, e ciascuno di questi bit rappresenta un singolo "permesso speciale"; in ordine da destra (lsb) a sinistra (msb), questi bit sono detti:
- **sticky bit**;
- **SetGID bit**;
- **SetUID bit**.

Lo **sticky bit**, se settato, provvede a risolvere un'incongruenza nell'assegnazione di permessi di accesso a una directory: supponendo che un utente abbia controllo totale di una directory (`rwx`), esso potrebbe teoricamente cancellare qualsiasi file al suo interno, anche se non ha i permessi di scrittura su tali file. Per ovviare a questo problema, con lo sticky bit settato a `1` sarà necessario avere i permessi di scrittura (`w`) anche sul file in questione per poterlo cancellare, anche se si ha controllo totale sulla directory che lo contiene.

Il **SetUID bit** viene utilizzato nel contesto di file eseguibili: se settato a `1`, permette all'utente che esegue un determinato file di acquisire, nel contesto dell'esecuzione, i privilegi dell'utente proprietario del file (ad esempio, se il proprietario del file è `root`, un qualsiasi utente che può eseguire il file lo esegue con i privilegi di `root`). Un esempio concreto di comando per cui si ha un funzionamento del genere è il comando **`passwd`**, che permette a un utente di modificare la propria password.

Il **SetGID bit** è sostanzialmente analogo al SetUID bit, ma invece di considerare i singoli utenti considera i gruppi di utenti: dunque, se in un file il SetGID bit è settato a `1`, qualsiasi utente che esegue tale file assume i privilegi del gruppo che è proprietario di tale file. Il SetGID bit può essere applicato anche alle directory: in tal caso, ogni file creato all'interno della directory in questione "erediterà" il gruppo di appartenenza della cartella "madre", anziché quello primario del creatore dei file stessi.

Per **visualizzare i permessi di accesso** a un file o directory, si potrà utilizzare il comando **`ls`**, visto [[SO2_02 - File system#Contenuto di una directory|poco fa]], con l'aggiunta dell'[[SO2_01 - Shell#Approfondimento sulle opzioni|opzione]] **`-l`** e specificando come argomento principale il file o directory in questione; in alternativa, si potrà utilizzare il comando **`stat`**. La **visualizzazione dei permessi speciali** è invece più particolare: innanzitutto, chiariamo che la visualizzazione dei permessi di accesso assume generalmente la seguente forma, oltre a quella delle cifre ottali:

```
drwxrwxrwx
```

dove il primo carattere `d` è presente solo se si sta considerando una directory (se, invece, si sta lavorando con un file, tale carattere viene sostituito da un trattino `-`); i seguenti 9 caratteri, invece, sono proprio le tre terne di attributi di accesso da assegnare, rispettivamente, all'utente proprietario (`u`), al gruppo di utenti a cui è assegnato il file o directory (`g`) e a tutti gli altri (`o`). Anche per i permessi di accesso, se uno dei tre livelli non è garantito, il carattere corrispondente verrà sostituito da `-`. Ora, tornando sui permessi speciali, per poter inserire anche tale informazione in questo schema senza perdere informazioni né aumentare le dimensioni della stringa, si adotta un sistema particolare: **se settati, i permessi speciali prendono il posto dei caratteri `x`**, ossia dei bit di esecuzione. In particolare:
- il setuid bit, rappresentato dal carattere **`s`**, prende il posto del bit di esecuzione nella terna `u`;
- il setgid bit, rappresentato dal carattere **`s`**, prende il posto del bit di esecuzione nella terna `g`;
- lo sticky bit, rappresentato dal carattere **`t`**, prende il posto del bit di esecuzione nella terna `o`.

È naturale, però, che venga un dubbio: così facendo non si perderebbe l'informazione relativa proprio al bit di esecuzione di ciascuna terna? In realtà no, grazie a un piccolo accorgimento: **se il bit di esecuzione è anch'esso settato, allora il carattere del permesso speciale sarà minuscolo**, mentre **se il bit di esecuzione non è settato, allora il carattere del permesso speciale sarà maiuscolo**. Si tenga a mente, comunque, che questo "problema" sorge solo se i permessi speciali sono effettivamente attivi, dato che in caso contrario verrà semplicemente visualizzato il carattere `x` (o `-` se non si hanno i permessi di esecuzione).

Così come possiamo visualizzare i permessi di accesso a un file o directory, sarà possibile anche **modificare i permessi di accesso**: per fare ciò, utilizziamo il comando:

```
chmod mode[, mode...] filename
```

dove `filename` è naturalmente il file o directory per cui si vogliono modificare i permessi, mentre `mode` è la nuova combinazione di permessi che si vuole inserire. Tipicamente, la combinazione di permessi viene specificata utilizzando proprio **4 cifre ottali**, come visto in precedenza: la prima per i permessi speciali, la seconda per i permessi di `u`, la terza per i permessi di `g` e la terza per i permessi di `o`. Alternativamente, se si inseriscono solo tre cifre, si assumerà che non vengano assegnati permessi speciali (dunque, che tutti e 3 i bit dei permessi speciali siano settati a `0`).

È possibile anche **utilizzare il comando `chmod` in modalità simbolica**, ossia utilizzando caratteri e non cifre ottali. Per fare ciò, `mode` assume la seguente forma:

```
[ugoa][+-=][perms...]
```

Vediamo più nel dettaglio ciascuna di queste componenti:
- **`[ugoa]`** rappresenta l'insieme dei caratteri e combinazioni di caratteri rappresentanti le varie terne di permessi di accesso (`a`, in particolare, indica tutti gli utenti, quindi dei permessi specificati per `a` verranno assegnati a tutte e tre le terne);
- **`[+-=]`** rappresenta i possibili operatori che possono essere utilizzati per assegnare i permessi alle terne indicate (`+` permette di aggiungere permessi a quelli già presenti, `-` permette di rimuoverli, mentre `=` permette di aggiungere permessi e di rimuovere quelli eventualmente non specificati);
- **`[perms...]`** rappresenta i permessi effettivi che possono essere assegnati alle terne, e consistono o in una qualsiasi combinazione dei caratteri `rwx`, oppure in uno dei caratteri dell'insieme `ugo` nel caso in cui si vogliano considerare i permessi assegnati a una di tali terne.

Vediamo alcuni esempi di utilizzo del comando `chmod` in modalità simbolica. Eseguire:

```
chmod ug=rwx,o=rx filename
```

corrisponde ad eseguire:

```
chmod 775 filename
```

Ancora, eseguire:

```
chmod a=rwx filename
```

corrisponde ad eseguire:

```
chmod 777 filename
```

e così via.

Infine, vediamo i comandi **`chown`** e **`chgrp`**, che possono utilizzati rispettivamente per **modificare l'utente proprietario** e **il gruppo a cui è assegnato** un determinato file o directory. Sono comandi che possono essere utilizzati solo da `root`, e in quanto tali richiedono l'utilizzo di `sudo` per poter essere eseguiti. Un'opzione utile nel contesto di questi comandi è **`-R`**, equivalente a **`--recursive`**, che permette, se si considera una directory, di applicare il comando anche a tutte le eventuali sotto-directory contenute al suo interno.
___
## Altri comandi utili per il file system

In questo paragrafo, andremo ad analizzare nel dettaglio una **lista di altri comandi utili per lavorare con il file system**. I comandi che considereremo sono i seguenti:
- **`umask`**;
- **`cp`**;
- **`mv`**;
- **`rm`**;
- **`ln`**;
- **`touch`**;
- **`du`**;
- **`df`**;
- **`dd`**;
- **`mkfs`**.

##### `umask`

Finora, approfondendo i [[SO2_02 - File system#Permessi di accesso ai file|permessi di accesso]] a file e directory, abbiamo visto cosa permette di fare una determinata combinazione di permessi e come, eventualmente, modificarli. Ma **come vengono decisi i permessi di accesso di un file al momento della creazione?**

Di default, in un sistema Linux ogni nuovo elemento nasce con dei **"permessi massimi" predefiniti**:
- per le **directory**, si prevedono permessi **`777`**, o **`rwxrwxrwx`**;
- per i **file**, si prevedono permessi **`666`**, o **`rw-rw-rw-`** (insomma, non vengono mai creati file eseguibili di default).

In questo contesto, **`umask`** funziona come una sorta di "filtro di sicurezza": come suggerisce il nome, è un comando usato per **decidere una maschera utilizzata per sottrarre automaticamente determinati permessi di accesso**. Ad esempio, il valore predefinito di `umask` per la maggior parte dei sistemi Linux moderni è **`022`**; ciò vuol dire che, ogni volta che si creerà un file o una directory in un sistema Linux, quest'ultimo "sottrarrà" preventivamente `2` al valore dei permessi per il gruppo e `2` al valore dei permessi per gli altri. Vediamo cosa implica ciò per directory e file:
- le directory hanno permessi massimi pari a `777`, o `rwxrwxrwx`, dunque applicare la maschera `022` renderà i permessi, al momento della creazione di una directory, pari a **`755`**, o **`rwxr-xr-x`** (in parole povere, **il creatore della directory avrà pieno controllo su di essa, mentre il gruppo e gli altri utenti potranno leggere ed entrare, ma non potranno modificare nulla**);
- i file hanno permessi massimi pari a `666`, o `rw-rw-rw-`, dunque applicare la maschera `022` renderà i permessi, al momento della creazione di un file, pari a `644`, o `rw-r--r--` (in parole povere, **il creatore del file potrà leggerlo e modificarlo, mentre il gruppo e gli altri utenti potranno solo leggerlo**).

Per **visualizzare la maschera attuale**, basterà eseguire il comando:

```
umask
```

Si tenga conto che si potrebbero vedere 4 cifre invece delle 3 viste finora: in tal caso, la prima cifra si riferirà ai permessi speciali `SetUID`, `SetGID` e `Sticky Bit`. Invece, per **modificare la maschera**, si eseguirà il comando:

```
umask [mode]
```

dove `mode` corrisponde proprio alla sequenza di cifre che si vuole assegnare alla maschera. Si ricordi, però, un dettaglio fondamentale: **se l'`umask` viene modificata tramite comando nel terminale, la modifica durerà solo per la sessione corrente**; ciò vuol dire che, alla chiusura della finestra in questione del terminale, o anche al riavvio del sistema, **la maschera tornerà al suo valore di default**, ossia **`022`**. Per rendere una modifica del genere permanente, si dovrebbero andare a modificare alcuni file di configurazione nascosti del sistema.
___
##### `cp`

Il comando **`cp`** permette di **copiare file o directory**; in particolare, permette di copiare un file in un altro oppure più file o directory in un'altra directory. Considerando solo gli argomenti obbligatori, una chiamata al comando `cp` prende la seguente forma:

```
cp {filesorgenti} filedestinazione
```

dove naturalmente **`filesorgenti`** rappresenta il (o i) file da copiare mentre **`filedestinazione`** rappresenta il file o directory di destinazione della copia. La differenza di funzionalità dipende proprio dalla scelta dei `filesorgenti` e dei `filedestinazione`:
- se si inserisce **un file come file sorgente** e **un file come file di destinazione**, allora il comando andrà a copiare i contenuti del file sorgente in un nuovo file, nominato come il file indicato come destinazione;
- se si inseriscono **più file o una directory come file sorgente** e **una directory come file di destinazione**, allora il comando andrà a copiare i file sorgente (sia i contenuti che i rispettivi nomi) all'interno della directory di destinazione (se si specifica una directory come file sorgente, si dovrà necessariamente inserire l'opzione `-r`, altrimenti verrà restituito un errore al momento dell'esecuzione del comando).

Sono previste anche varie opzioni facoltative, tra cui:
- **`-f`**, o **`--force`**, che, nell'eventualità in cui un file di destinazione da sovrascrivere non possa essere aperto, impone di cancellare tale file e di riprovare ad effettuare la copia;
- **`-i`**, o **`--interactive`**, che impone al comando di avvisare l'utente nell'eventualità in cui stia per avvenire una sovrascrittura;
- **`-p`**, o **`--preserve`**, che permette al comando di copiare i file specificati copiando anche metadati come i [[SO2_02 - File system#Permessi di accesso ai file|permessi di accesso]], l'utente e il gruppo di appartenenza e i timestamp;
- **`-r`**, **`-R`** o **`--recursive`**, che permette di copiare ricorsivamente anche i contenuti dell'eventuale directory specificata come sorgente;
- **`-u`**, o **`--update=older`**, che impone, in caso di possibilità di sovrascrittura, di sovrascrivere il file solo se la sorgente è più recente della destinazione;
- **`-v`**, o **`--verbose`**, che impone al comando di stampare nel terminale i dettagli di ogni operazione che effettua.
___
##### `mv`

Il comando **`mv`** permette di **spostare** e di **rinominare un file**. Considerando solo gli argomenti obbligatori, una chiamata al comando `mv` prende la seguente forma:

```
mv {filesorgenti} filedestinazione
```

La differenza di funzionalità dipende proprio dalla scelta dei `filesorgenti` e dei `filedestinazione`:
- se si inserisce **un file come file sorgente** e **un altro file come file di destinazione**, verrà effettuata la rinomina del file sorgente seguendo il nome indicato come file di destinazione;
- se si inserisce **un file come file sorgente** e **una directory già esistente come file di destinazione**, verrà effettuato lo spostamento del file sorgente all'interno della directory indicata (se, nel path della directory di destinazione, al termine si specifica anche un nome `nuovoNomeFile` il file sorgente non solo verrà spostato ma anche rinominato a `nuovoNomeFile`);
- se si inseriscono **più file come file sorgente** (vanno inseriti separati da uno spazio) e **una directory già esistente come file di destinazione**, verrà effettuato lo spostamento di tutti quei file nella directory indicata (se si devono spostare tutti i file presenti che condividono una medesima estensione, si può utilizzare un trucco per spostarli tutti comodamente, ossia indicare come file sorgente solamente `*.estensione`).

Sono previste anche varie opzioni facoltative, tra cui:
- **`-f`**, o **`--force`**, che è attiva di default e che permette al comando di effettuare sovrascritture in automatico, senza chiedere conferma all'utente;
- **`-i`**, o **`--interactive`**, che impone al comando di avvisare l'utente nell'eventualità in cui stia per avvenire una sovrascrittura;
- **`-n`**, o **`--no-clobber`**, che proibisce al comando qualsiasi operazione di sovrascrittura;
- **`-u`**, o **`--update=older`**, che impone, in caso di possibilità di sovrascrittura, di sovrascrivere il file solo se la sorgente è più recente della destinazione;
- **`-v`**, o **`--verbose`**, che impone al comando di stampare nel terminale i dettagli di ogni operazione che effettua.

Si nota facilmente che `-f`, `-i` e `-n` impongono condizioni ben diverse sullo stesso aspetto: e se ne venissero specificate più di una? In quel caso, verrà considerata solo l'opzione che compare per ultima nella chiamata al comando.
___
##### `rm`

Il comando **`rm`** permette di **eliminare file e cartelle** dal file system. Si tratta di un comando in realtà molto potente, anche per una caratteristica da tenere a mente: in Linux, di base le operazioni effettuate nel terminale non dispongono del tipico "cestino", dunque se si elimina un file o una cartella utilizzando comandi come `rm` tali dati sono pressoché irrecuperabili. Considerando solo gli argomenti obbligatori, una chiamata al comando `mv` prende la seguente forma:

```
rm {file}
```

dove **`file`** può essere uno o più file o directory da eliminare. Sono previste anche varie opzioni facoltative, tra cui:
- **`-f`**, o **`--force`**, che permette al comando di eliminare automaticamente qualsiasi file venga indicato, ignorando eventuali file non esistenti; 
- **`-i`**, o **`--interactive`**, che impone al comando di chiedere conferma all'utente per ogni cancellazione che esso vuole effettuare;
- **`-r`**, o **`--recursive`**, che permette di eliminare ricorsivamente anche i contenuti dell'eventuale directory specificata;
- **`-v`**, o **`--verbose`**, che impone al comando di stampare nel terminale i dettagli di ogni operazione che effettua.
___
##### `ln`

Per parlare del comando **`ln`**, è opportuno approfondire i concetti di "**hard link**" e di "**soft link**" in Linux. Hard link e soft link sono due tipi di **collegamento**, in particolare di collegamento tra file; per semplicità, si può vedere l'hard link come un "collegamento fisico", mentre il soft link è piuttosto un "collegamento simbolico".

Nel caso dell'**hard link**, esso è per certi versi **un secondo nome dato a un file sul disco rigido**: in altre parole, il file originale non viene copiato né modificato, ma viene creato un nuovo file che rappresenta semplicemente un nuovo collegamento a quello stesso link. Immaginando il disco rigido come una libreria, e un determinato file come un libro ben preciso, si può immaginare un hard link a tale file come una seconda scheda, all'interno del catalogo dei libri, che punta sempre allo stesso libro. Concretamente, ciò avviene facendo in modo che **il file creato come hard link abbia lo stesso inode number del file originale**. Dunque, creando un ipotetico hard link `hard_link.txt` per un determinato file `file_originale.txt`, anche eliminando quest'ultimo i dati non verranno persi, dato che rimarrà ancora `hard_link.txt` come collegamento a quei dati; al tempo stesso, **qualsiasi verifica a uno dei due file verrà istantaneamente trasposta anche nell'altro**, dato che essi condividono letteralmente gli stessi dati in memoria. Gli hard link, rispetto ai soft link, presentano però un limite: **gli hard link non possono essere creati per directory, e neanche tra dischi o partizioni diverse**.

I **soft link**, invece, sono esattamente equivalenti ai collegamenti di Windows, o agli alias di macOS: si tratta di **file speciali che contengono semplicemente il [[SO2_02 - File system#Il path|path]] che porta al file originale**. Dunque, creando un ipotetico soft link `soft_link.txt` per un determinato file `file_originale.txt`, si creerà un file che se aperto ricondurrà proprio a `file_originale.txt` seguendo il suo path. I soft link, rispetto agli hard link, presentano però un limite: **se il file originale viene spostato, rinominato o cancellato, il soft link smetterà di funzionare** e diventerà quello che viene definito un "dangling link", o "collegamento orfano" (spesso, in tal caso, se si visualizza il file da terminale esso verrà colorato di rosso proprio per indicare che il link non porta più a nulla).

Ora, avendo chiarito i concetti di hard link e soft link, passiamo effettivamente a parlare del comando `ln`. Tale comando permette proprio di **creare hard link e soft link**. La sinossi del comando è la seguente:

```
ln [OPZIONI] sorgente [destinazione]
```

dove **`sorgente`** è il file a cui si riferisce il link creato. Come si può vedere, inserire un path e un nome per il link creato non è obbligatorio: se si omette **`destinazione`**, il sistema proverà a creare un link chiamato con lo stesso nome del file `sorgente`, nella stessa directory in cui ci si trova correntemente; ciò, però, non funzionerà nel momento in cui tale comando in tale forma verrà eseguito nella directory in cui si trova il file originale, dato che esisterà già un file con quel nome. In generale, è buona pratica specificare path e nome del link.

Ci sono varie opzioni facoltative per il comando `ln`, ma la più comune e di gran lunga più importante è **`-s`**: se tale opzione non viene specificata, il comando creerà un hard link; al contrario, se essa viene specificata, il comando creerà un soft link.
___
##### `touch`

Seppur venga spesso utilizzato per **creare file vuoti**, il comando **`touch`** serve principalmente per **aggiornare i [[SO2_02 - File system#Struttura di file e directory|timestamps]] di un file**. Considerando solo gli argomenti obbligatori, una chiamata al comando `touch` prende la seguente forma:

```
touch {file}
```

dove **`file`** è il nome del file in questione. Se il file `file` esiste già, eseguire tale comando non farà altro che aggiornare i timestamps relativi all'ultimo accesso (`atime`) e all'ultima modifica (`mtime`) impostandoli all'orario esatto in cui si è lanciato il comando, pur non aprendo né modificando effettivamente il file stesso; invece, se il file `file` non esiste, il comando creerà un file completamente vuoto con tale nome.

Sono previste anche varie opzioni facoltative, tra cui:
- **`-a`**, che impone al comando di aggiornare solamente il timestamp relativo all'ultimo accesso, ossia l'`atime`;
- **`-c`**, o **`--no-create`**, che proibisce al comando di creare nuovi file nell'eventualità in cui il nome di file inserito non venga trovato;
- **`-m`**, che impone al comando di aggiornare solamente il timestamp relativo all'ultimo accesso, ossia l'`atime`;
- **`-r=FILE`**, o **`--reference=FILE`**, che impone al comando di aggiornare i timestamps prendendo come riferimento quelli del file `FILE`, invece di quelli attuali;
- **`-t timestamp`**, che permette di specificare un timestamp specifico della forma **`[[CC]YY]MMDDhhmm[.ss]`** e di utilizzare quello invece di quello attuale.
___
##### `du`

Il comando **`du`** serve per **stimare lo spazio di memoria occupato dai file e/o directory specificate**. La sinossi del comando è la seguente:

```
du [OPZIONI] [files...]
```

dove **`files`** sono i file o directory da considerare. Si noti che l'argomento `files` è in realtà facoltativo: infatti, se omesso, il comando verrà eseguito sulla directory corrente.

Sono previste anche varie opzioni facoltative, tra cui:
- **`-a`**, o **`--all`**, che impone al comando di stampare le dimensioni occupate anche da ogni singolo file contenuto nell'eventuale directory indicata, e non solo quelle complessive delle varie sotto-directory;
- **`-B=SIZE`**, o **`--block-size=SIZE`**, che impone al comando di stampare le dimensioni misurate in unità di grandezza `SIZE` (di default, l'unità considerata è il $KiB$, o $1024\,\,B$); 
- **`-c`**, o **`--total`**, che impone al comando di stampare, dopo tutte le dimensioni che esso calcola normalmente, la dimensione totale in modo esplicito;
- **`--exclude=PATTERN`**, che impone al comando di non stampare i file che rispecchiano la forma `PATTERN` (il carattere `?` coincide con qualsiasi singolo carattere, mentre il carattere `*` coincide con qualsiasi stringa; ad esempio, indicare `--exclude='*.txt'` evita che venga stampato qualsiasi file con estensione `.txt`);
- **`-h`**, o **`--human-readable`**, che impone al comando di stampare le dimensioni in modo più "leggibile", tipicamente aggiungendo un simbolo che indichi l'unità di misura oppure essendo più preciso con certe misure;
- **`-s`**, o **`--summarize`**, che impone al comando di stampare solamente la dimensione totale dell'argomento specificato (e non di eventuali sotto-directory o file contenuti).
___
##### `df`

Il comando **`df`** permette di **avere informazioni sulla dimensione e sullo spazio occupato dal file system**. Una chiamata al comando **`df`** assume la seguente forma:

```
df [OPZIONI...] [file]
```

dove **`file`** consiste in uno o più nomi di file; se si specifica qualcosa come `file`, il comando visualizzerà informazioni sui file system in cui è contenuto quel qualcosa, mentre se non si specifica nulla e si esegue semplicemente `df` si visualizzeranno informazioni su tutti i file system attualmente [[SO2_02 - File system#Mounting, partizioni e tipi di file system|montati]]. Le informazioni vengono visualizzate sotto forma di una **tabella a 6 colonne**, in cui ogni riga rappresenta un singolo file system e in cui le colonne, in ordine, informano su:
1. **nome tecnico del file system** considerato (ad esempio, `/dev/sda1` è la prima partizione del primo disco fisico);
2. **dimensione totale in blocchi** del file system considerato, espressa in blocchi da 1 kilobyte;
3. **blocchi effettivamente occupati** all'interno file system considerato attualmente;
4. **blocchi liberi**, e dunque non ancora occupati all'interno del file system considerato attualmente;
5. **percentuale di spazio occupato** rispetto alla dimensione totale del file system considerato attualmente;
6. **directory su cui è montato il file system** considerato.

Sono previste anche varie opzioni facoltative, tra cui:
- **`-h`**, o **`--human-readable`**, che impone al comando di stampare le dimensioni in modo più "leggibile", tipicamente aggiungendo un simbolo che indichi l'unità di misura oppure essendo più preciso con certe misure;
- **`-i`**, o **`--inodes`**, che permette di visualizzare informazioni diverse rispetto a quelle canoniche, concentrate non più sullo spazio di memoria ma piuttosto sugli inode (in particolare, su quanti ne può contenere in totale ogni file system, quanti sono attualmente presenti e quanti "posti" sono ancora liberi);
- **`-l`**, o **`--local`**, che impone al comando di visualizzare esclusivamente i file system "locali", ignorando dunque qualsiasi file system di rete o remoto collegato alla macchina;
- **`-T`**, o **`--print-type`**, che impone al comando di aggiungere una colonna alla tabella di informazioni, contenente il tipo di file system.
___
##### `dd`

[SLIDES: 03, slide 17 - 18]
___
##### `mkfs`

Il comando **`mkfs`** permette di **creare un file system su un dispositivo**, ma è comunemente utilizzato anche per **formattare un disco** e per **prepararlo a ospitare file secondo un determinato formato**, specificato proprio dal tipo di file system utilizzato. Una chiamata al comando **`mkfs`** assume la seguente forma:

```
mkfs [OPZIONI...] [-t type] [fs-options] device [size]
```

dove:
- **`type`**
- **`device`**
- **`size`**

[SLIDES: 03, slide 20]
___