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

[SLIDES: 04 - pag. 12 - 13]

Oltre a PID e PCB, ogni processo dispone di un proprio **spazio di indirizzamento**, ossia di una propria area di memoria nella memoria principale, diviso in **sei aree fondamentali**:
- **Text Segment** (tipicamente accessibile in sola lettura per evitare corruzione dei dati), che contiene le istruzioni in linguaggio macchina da mandare al processore per proseguire l'esecuzione del processo (se si lanciano più istanze dello stesso programma, questo segmento potrebbe essere condiviso per risparmiare memoria);
- **Data Segment**, che contiene le variabili globali o statiche inizializzate in modo esplicito all'interno del codice;
- **BSS Segment**, che contiene le variabili globali o statiche non inizializzate; 
- **Heap**, che rappresenta lo spazio destinato all'[[SO2_04 - C#Allocazione dinamica di memoria|allocazione dinamica di memoria]], controllata dal programmatore durante l'esecuzione del programma tramite funzioni come `malloc`, `calloc` o `free` (si approfondirà l'argomento in seguito);
- **Memory Mapping Segment**, che contiene dati e informazioni relative a librerie esterne dinamiche usate dal processo;
- **Stack**, che contiene le variabili locali e non statiche, oltre che tutte le informazioni relative alle varie chiamate a funzione (parametri passati, indirizzi di ritorno, ecc. ecc.); a differenza del Text Segment, o anche del BSS Segment e del Memory Mapping Segment, lo Stack di un processo non è mai condiviso.
___
##### Stati di un processo

**Un processo non è sempre attivamente in esecuzione nella CPU**: piuttosto, l'OS effettua uno **scheduling** dell'esecuzione dei processi, in modo da distribuire il più equamente possibile il processore tra di essi. Perciò, un processo può trovarsi in vari "**stati**", in base alla situazione in cui si trovano attualmente. In sistemi Linux, gli stati in cui si può trovare un processo sono:
- **Running** (**R**), in cui **il processo sta venendo effettivamente eseguito** dal processore;
- **Runnable** (**R**), in cui **il processo è pronto per essere eseguito** dal processore, e ha tutte le risorse necessarie per farlo, ma sta aspettando che lo scheduling dell'OS assegni ad esso il processore;
- **Sleep** (**S**), in cui **il processo sta aspettando un determinato evento** (ad esempio, l'input dell'utente o l'arrivo di dati dalla memoria) **e non può proseguire l'esecuzione** finché tale evento non accade;
- **Uninterruptible Sleep** (**D**), in cui, similmente a Sleep, **il processo sta aspettando un evento, ma è impegnato in operazioni critiche o di I/O con dischi lenti**, e non può dunque essere interrotto o "ucciso" nel mentre;
- **Stopped** (**T**), in cui **il processo è stato bloccato in modo "esplicito"**, ad esempio avendo ricevuto un segnale `SIGSTOP`;
- **Traced** (**t**), in cui **il processo è in esecuzione tramite debugger** (quindi la sua esecuzione effettiva è bloccata), o **è in attesa di un segnale**;
- **Zombie** (**Z**), in cui **il processo ha terminato la sua esecuzione ma l'OS mantiene in memoria il suo [[SO2_03 - Processi#Come sono rappresentati i processi?|PCB]] vuoto**, contenente solamente l'exit status del processo e avendo già liberato le sei aree di memoria occupate tipicamente da un processo (questo avviene quando il processo padre non ha ancora richiesto l'esito del processo considerato).
___
##### Esecuzione dei processi

I processi possono essere eseguiti principalmente in due modi:
- in "**foreground**" (o "**in primo piano**"), ossia la modalità che abbiamo visto finora, in cui **il processo può leggere l'input da tastiera e stampare sullo schermo** e in cui, **fino alla terminazione del processo, il [[SO2_01 - Shell#Prompt e comandi|prompt]] della shell non viene restituito e non si possono lanciare altri comandi**;
- in "**background**" (o "**in secondo piano**"), una modalità in cui **il processo non può leggere input da tastiera ma può stampare sullo schermo** e in cui **il prompt viene immediatamente restituito**, con la possibilità di eseguire altri comandi mentre quello considerato viene eseguito in background.

Per proseguire la trattazione, è importante fare una **distinzione tra processi e "lavori"**, detti anche "**jobs**": un processo è un gestito direttamente dal kernel, ed è un vero e proprio programma in esecuzione, con un suo PID, le sue aree di memoria, ecc. ecc.; un **lavoro**, invece, è **gestito direttamente dalla [[SO2_01 - Shell|shell]]**, e rappresenta un singolo comando o una singola direttiva che l'utente ha eseguito tramite terminale. Quando un comando viene eseguito in background, la shell associa a tale comando un **numero di lavoro** (partendo da 1), e tale numero potrà essere utilizzato da allora per riferirsi a tale lavoro finché esso sarà in esecuzione. 

Per **eseguire un comando in background**, esso dovrà essere **seguito da una "e commerciale"** (**`&`**).

In generale, **un lavoro può essere composto da uno o più processi**, e dunque da uno o più comandi. Dunque, nella shell, è possibile creare un lavoro che esegua un comando "complesso", a partire da più comandi semplici, tramite un meccanismo chiamato **"pipelining" dei comandi**. Per fare pipelining di due o più comandi, si utilizzano principalmente due operatori:
- l'operatore **`|`**, che permette di **redirezionare lo `stdout` del comando precedente nello `stdin` del comando successivo**;
- l'operatore **`|&`**, che permette di **redirezionare lo `stderr` del comando precedente nello `stdin` del comando successivo**.

Naturalmente, il comando $i+1$-esimo non deve necessariamente utilizzare lo `stdout` o `stderr` del comando $i$-esimo.

Un esempio di pipelining di 3 comandi può essere il seguente:

```
cat mio_file.txt | grep "errore" | wc -l &
```

e, costituendo un unico lavoro, a questo insieme di comandi verrà assegnato un unico numero di lavoro. 
___
## Comandi per la gestione dei processi

Ci sono vari **comandi per la gestione di processi e lavori**, tra cui:
- **`jobs`**;
- **`bg`**;
- **`fg`**;
- **`ps`**;
- **`top`**;
- **`kill`**;
- **`nice`**;
- **`renice`**;
- **`strace`**.

##### `jobs`

Il comando **`jobs`** permette di **ottenere informazioni sui lavori in esecuzione**. La sinossi completa del comando è:

```
jobs [OPZIONI...]
```

Eseguire il comando senza opzioni risulterà in un output che rispecchierà una sorta di tabella, in cui ogni riga rappresenta un singolo lavoro e i cui campi (in ordine) rappresentano:
- il **numero di lavoro**, scritto tra parentesi quadre;
- eventualmente, un **simbolo `+` o `-`**, tali per cui il lavoro contrassegnato da un `+` corrisponde al lavoro che si ha mandato in background o sospeso per ultimo, mentre il lavoro contrassegnato da un `-` corrisponde al penultimo lavoro su cui si ha agito;
- lo **stato del lavoro**, e dunque cosa sta facendo attualmente quest'ultimo (tali stati possono essere `Running`, il che vuol dire che il lavoro sta attivamente venendo eseguito in background, `Stopped` o `Suspended`, il che vuol dire che il lavoro è stato bloccato, ad esempio premendo `CTRL + z`, ed è in attesa di essere ripreso, `Done`, il che vuol dire che il lavoro ha terminato con successo la sua esecuzione, o `Terminated`, il che vuol dire il lavoro è stato "ucciso" tramite un segnale);
- il **comando digitato per lanciare il lavoro**.

Nel caso in cui un lavoro sia composto da più comandi posti in pipeline, ciascuno dei comandi verrà visualizzato su una riga diversa, ma solo la riga contenente il primo comando disporrà del numero di lavoro.

Vediamo, a questo punto, le **opzioni principali** per il comando `jobs`:
- **`-l`**, che permette di visualizzare, oltre alle informazioni standard appena viste, anche il [[SO2_03 - Processi#Come sono rappresentati i processi?|PID]] del "processo leader" di ogni lavoro, ossia del primo degli eventualmente molteplici processi contenuti nel lavoro;
- **`-n`**, che impone al comando di mostrare solo i lavori il cui stato è cambiato dall'ultima volta che la shell ha avvisato l'utente;
- **`-p`**, che impone al comando di mostrare solamente i PID dei processi leader di ogni lavoro;
- **`-r`**, che impone al comando di mostrare solamente i lavori che sono attualmente in esecuzione;
- **`-s`**, che impone al comando di mostrare solamente i lavori che attualmente si trovano nello stato `Stopped` o `Suspended`.
___
##### `bg`

Il comando **`bg`** permette di **portare l'esecuzione di un lavoro in [[SO2_03 - Processi#Esecuzione dei processi|background]]**; tale comando può essere utile, ad esempio, quando si è eseguito per errore un processo o un lavoro molto lungo in foreground, e in tale contesto è possibile sospendere la sua esecuzione con `CTRL + z` e, in seguito, "risvegliarlo" in background proprio grazie a `bg`. La sinossi completa del comando è:

```
bg [job_id]
```

dove **`job_id`** è il **numero di lavoro del lavoro considerato**. Si noti che tale argomento è, in realtà, opzionale: omettere un `job_id`, infatti, porterà all'esecuzione in background del "lavoro corrente", ossia di quello contrassegnato da un `+` nell'output del comando **[[SO2_03 - Processi#`jobs`|jobs]]**. Oltre che con il numero di lavoro, è possibile individuare un determinato lavoro su cui eseguire il comando `bg` anche specificando l'eventuale nome del suo eseguibile.
___
##### `fg`

Il comando **`bg`** permette di **portare l'esecuzione di un lavoro in [[SO2_03 - Processi#Esecuzione dei processi|foreground]]**; tale comando può essere utile, ad esempio, per rispondere a una richiesta di input di un lavoro in esecuzione in background (se un processo in background richiede un input da tastiera, l'OS gli lancerà un segnale `SIGTTIN` che sospenderà la sua esecuzione, e per proseguire si dovrà riportare il lavoro in foreground con `fg`, fornire l'input richiesto, e poi decidere se proseguire l'esecuzione in foreground o in background) o per poter "uccidere" in via definitiva un determinato processo. La sinossi completa del comando è:

```
fg [job_id]
```

Per quanto riguarda il significato di `job_id` e il funzionamento del comando, valgono le stesse considerazioni fatte per il comando **[[SO2_03 - Processi#`bg`|bg]]**.
___
##### `ps`

Il comando **`ps`** viene utilizzato per **ottenere informazioni sui processi in esecuzione**, e fa ciò leggendo le informazioni dei file virtuali contenuti nella directory `/proc`, dove il kernel dell'OS espone le informazioni di sistema in tempo reale. La sinossi completa del comando è:

```
ps [OPZIONI...]
```

Eseguire il comando `ps` senza alcuna istruzione risulta in un output relativamente scarno, dato che equivale a **mostrare informazioni esclusivamente sui processi lanciati dall'utente attuale e dalla shell corrente** (spesso, gli unici processi visualizzati in questo contesto saranno il processo `bash` della shell stessa e il processo `ps` lanciato proprio per visualizzare tali informazioni). Sarà possibile visualizzare più informazioni su tali processi, o anche più processi, grazie a opzioni che vedremo in seguito. A livello di base, eseguire `ps` mostrerà una sorta di tabella, in cui **ogni riga corrisponderà a un diverso processo** e i cui **campi** (in ordine) sono:
- **`PID`**, ossia il PID del processo in questione;
- **`TTY`**, ossia il terminale (fisico o virtuale) da cui è partito il comando;
- **`TIME`**, ossia il tempo totale di utilizzo effettivo della CPU da parte del processo;
- **`CMD`**, ossia il comando eseguito per lanciare tale processo.

Possiamo suddividere le **opzioni principali** del comando `ps` in due categorie: quelle che permettono di selezionare quali processi mostrare, e quelle che permettono di mostrare più o meno informazioni a riguardo. Per quanto riguarda le prime, le più importanti sono:
- **`-e`**, che impone al comando di **mostrare tutti i processi in esecuzione sulla macchina**, compresi quelli di sistema lanciati al boot, o i processi lanciati da altri utenti;
- **`-p PID`**, che impone al comando di **mostrare solamente le informazioni di uno o più processi** specificati grazie alla lista `PID`; 
- **`-u users`**, che impone al comando di **mostrare solamente i processi appartenenti alla lista di utenti `user`**.

Invece, le opzioni che permettono di mostrare più o meno informazioni sui processi considerati sono:
- **`-f`**, che impone al comando di **aggiungere più informazioni** riguardo i processi visualizzati (in particolare, vengono aggiunti i campi **`UID`**, che indica l'utente che sta effettivamente facendo eseguire il processo, **`PPID`**, che corrisponde al PID del processo padre, **`C`**, che corrisponde alla parte intera della percentuale d'uso attuale della CPU da parte del processo, e **`STIME`** o **`START`**, ossia l'orario o la data in cui è stato avviato il comando);
- **`-l`**, che impone al comando di **aggiungere ancora più informazioni**, anche rispetto a `-f` (vengono aggiunti i campi: **`F`**, che rappresenta delle flag associate al processo, con 1 che indica che il processo è stato "biforcato" tramite `fork` ma non ancora eseguito, 4 che indica che il processo ha utilizzato privilegi da `root`, 5 che rappresenta la somma delle due flag precedenti e 0 che indica che nessuno dei casi precedenti è applicabile al processo; **`S`**, che rappresenta lo [[SO2_03 - Processi#Stati di un processo|stato]] attuale del processo; **`PRI`**, che indica l'attuale priorità del processo con un numero tale per cui più è alto e minore è la priorità; **`NI`**, che indica la "niceness" del processo; **`ADDR`**, che corrisponde all'indirizzo in memoria del processo ma che spesso viene mostrato vuoto per motivi di retro-compatibilità; **`SZ`**, che corrisponde alla dimensione totale del processo espressa in numero di pagine RAM e disco; **`WCHAN`**, che indica in quale funzione del kernel il processo si è eventualmente bloccato in attesa di un segnale o di un evento);
- **`-o fields`**, che impone al comando di **mostrare solamente i campi specificati nella lista `fields`**.

Eseguire il comando **`ps -yl`**, in particolare, permette di vedere informazioni leggermente diverse da quelle che verrebbero visualizzate semplicemente tramite `-l`: ad esempio, viene eliminato il campo `F` (spesso poco utile), o ancora viene sostituito il campo `ADDR` con un campo `RSS`, che mostra la dimensione del processo in KB nella memoria principale (non tenendo, dunque, conto delle pagine su disco).
___
##### `top`

Il comando **`top`** può essere visto come una **versione dinamica di [[SO2_03 - Processi#`ps`|ps]]**: mentre quest'ultimo fornisce una "fotografia" dei processi in esecuzione nel momento in cui viene lanciato il comando, `top` offre una **visualizzazione in tempo reale e in continuo aggiornamento**. La sinossi completa del comando è:

```
top [OPZIONI...]
```

Quando si esegue `top`, il terminale diventa sostanzialmente una **dashboard interattiva**: l'interfaccia del terminale viene divisa in due sezioni, di cui la prima costituisce la cosiddetta "**summary area**", che fornisce una panoramica globale dello stato del sistema, e la seconda costituisce la "**task area**", una tabella che elenca i processi in esecuzioni, aggiornati costantemente e ordinati in base alla percentuale di CPU utilizzata.

Le **opzioni principali** per il comando `top` sono:
- **`-b`**, che impone al comando di eseguirsi in "**batch mode**", eliminando qualsiasi interattività e stampando piuttosto i dati a schermo ogni pochi secondi;
- **`-n num`**, che impone al comando di **aggiornarsi solo `num` volte** prima di terminare automaticamente la propria esecuzione; 
- **`-p PID`**, che funziona in modo identico all'opzione omonima di `ps`.

Se `top` viene aperto in modo interattivo (dunque, evitando l'opzione `-b`), sarà possibile premere **`?`** per avere una **lista completa di comandi eseguibili** durante l'esecuzione del comando.
___
##### `kill`

Il comando **`kill`**, nonostante il suo nome abbastanza intimidatorio, serve per **inviare segnali vari a un processo**. La sinossi completa del comando è:

```
kill [-l [signal]] [-signal] [PID...]
```

Analizziamo, passo per passo, i vari contesti in cui può essere utilizzato tale comando, e le opportune combinazioni di opzioni per ciascuno di essi. Il comando `kill` può essere utilizzato per inviare uno qualsiasi dei **57 segnali** previsti, ciascuno dei quali è identificato da un **nome che inizia per `SIG`** (nel riferirsi a un determinato segnale in una chiamata al comando `kill`, tale prefisso può anche essere omesso) o da un **numero**. Per visualizzare tutti i possibili segnali, con annesso il loro numero e nome, basterà eseguire il comando:

```
kill -l
```

Inoltre, è possibile eseguire il comando appena visto anche seguito dal nome di un determinato segnale per ottenere il numero associato ad esso, o viceversa il numero di un segnale per ottenere il suo nome. Ad esempio, eseguire:

```
kill -l SIGKILL
```

stamperà nel terminale il numero `9`.

Ora, andando avanti e ipotizzando di non star usando l'opzione `-l`, sarà possibile utilizzare il comando `kill` per **inviare un certo segnale `signal` ai processi identificati dalla lista `PID`**. Ad esempio, eseguire uno qualsiasi dei seguenti comandi:

```
kill -9 123
kill -SIGKILL 123
kill -KILL 123
```

porterà al medesimo risultato, ossia all'invio del segnale `SIGKILL` al processo avente PID pari a `123`. Nello specificare il segnale da mandare, quando ci si riferisce al suo nome e non al suo numero, è possibile inserire l'opzione **`-s`** prima del segnale e omettere il trattino (`-`) che precede quest'ultimo, ad esempio:

```
kill -s KILL 123
```

Come si può notare, però, **specificare il segnale da inviare non è obbligatorio**: se lo si omette, eseguendo il comando nella forma base `kill PID`, viene inviato un **segnale di default**, ossia **`SIGTERM`** (identificato dal numero **`15`**). Ma **cosa fanno concretamente i vari segnali?** Per rispondere a questa domanda, forniamo di seguito un elenco dei **segnali più comuni** e più potenti tra i 57 disponibili:
- **`SIGINT`** (o **`INT`**, identificato dal numero **`2`**), che è il segnale inviato al processo [[SO2_03 - Processi#Esecuzione dei processi|in foreground]] quando si preme **`CTRL + c`**, e serve per **interrompere il processo** (la maggior parte dei programmi si chiude immediatamente, ma in alcuni casi, come con gli editor di testo, essi possono intercettare il segnale e chiedere all'utente di salvare il proprio lavoro prima di terminare l'esecuzione);
- **`SIGKILL`** (o **`KILL`**, identificato dal numero **`9`**), che serve per **interrompere il processo immediatamente, senza possibilità di intercettazione o ignoramento** (va usato con prudenza, dato che potrebbe portare a corruzione di dati o altri comportamenti non desiderati);
- **`SIGTERM`** (o **`TERM`**, identificato dal numero **`15`**), che serve per **interrompere un processo in modo "gentile"**, dando tempo al processo di salvare dati, chiudere eventuali file aperti e terminare tutte le operazioni in corso prima di terminare la propria esecuzione;
- **`SIGCONT`** (o **`CONT`**, identificato dal numero **`18`**), che serve per **far continuare l'esecuzione di un processo bloccato** (viene usato, ad esempio, dai comandi `bg` e `fg`);
- **`SIGSTOP`** (o **`STOP`**, identificato dal numero **`19`**), che serve per **bloccare il processo immediatamente**, facendolo entrare nello stato di `Sleep`, e come `SIGKILL` non può essere intercettato né ignorato;
- **`SIGSTP`** (o **`STP`**, identificato dal numero **`20`**), che è **molto simile a `SIGSTOP`**, ma a differenza di quest'ultimo **può essere intercettato dal programma** (è il segnale inviato al processo in foreground quando si preme `CTRL + z`).

**I segnali vengono presi in considerazione solo se il "real user" del processo è lo stesso che invia il segnale** (oppure, **se li invia un super-utente**). In generale, quando un processo riceve un segnale, o fa un'**azione predefinita** (come quelle appena viste), oppure un'**azione personalizzata**.

Oltre a quelli analizzati poco fa, ci sono altri due segnali particolari degni di essere approfonditi: **`SIGUSR1`** (o **`USR1`**, identificato dal numero **`10`**) e **`SIGUSR2`** (o **`USR2`**, identificato dal numero **`12`**). Tali segnali sono un esempio di processi che consentono un'operazione personalizzata, e in particolare consentono una **semplice forma di comunicazione tra processi**: supponendo, ad esempio, di star creando un programma `P1`, si può definire un gestore di segnali per `SIGUSR1`, in modo che se un altro programma `P2` invia un segnale `SIGUSR1` a `P1` quest'ultimo eseguirà il codice del gestore creato. Spesso, se si invia uno di questi segnali a un processo che non li gestisce in modo esplicito, essi causano la terminazione del processo in questione.
___
##### `nice`

[SLIDES: 04... pag. 39]
___
##### `renice`

[SLIDES: 04... pag. 40]
___
##### `strace`

Il comando **`strace`** viene utilizzato per **eseguire un comando mostrando tutte le sue [[SO2_05 - System calls|chiamate di sistema]] e le risposte a tali chiamate**, oppure per **visualizzare le chiamate di sistema effettuate da un certo processo**. La sinossi completa del comando è:

```
strace [-p PID] [comando]
```

Per eseguire un comando `comando` monitorando le sue chiamate di sistema (sostanzialmente eseguendolo in modalità debugging), si dovrà eseguire:

```
strace comando
```

Fare ciò stamperà a schermo tutte le librerie caricate dal comando `comando`, tutti gli eventuali [[SO2_02 - File system|file e directory]] aperti durante l'esecuzione, le chiamate di sistema effettuate, ecc. ecc. Alternativamente, è possibile monitorare un processo già in esecuzione eseguendo:

```
strace -p PID
```

dove `PID` è, naturalmente, il PID del processo da monitorare.

Nella maggior parte dei casi, l'esecuzione di un programma o di un comando porterà a migliaia di chiamate di sistema, o comunque a quantità enormi di informazioni, che finiranno per "intasare" il terminale: dunque, in questi casi, si preferisce **ridirezionare l'output del comando in un file**. Per fare ciò, ci sono due modi:
- il modo "grezzo" implica il ridirezionamento dei [[SO2_03 - Processi#Canali standard|canali standard]] del processo, ad esempio eseguendo `strace comando 2> log.txt` (si ridireziona `stderr` e non `stdout`, dato che il comando `strace` stampa sul primo);
- il modo "elegante" implica l'utilizzo dell'opzione **`-o filename`**, che dovrà precedere il comando da eseguire (ad esempio, `strace -o log.txt ls -l`).

Oltre a quelle viste finora, ci sono altre **opzioni utili** per il comando `strace`, tra cui:
- **`-c`**, che impone al comando di stampare solo una "tabella" riassuntiva finale, una volta terminata l'esecuzione del processo monitorato;
- **`-e ops...`**, che permette di filtrare le operazioni di monitorare in base alla lista `ops`.
___