Per proseguire nell'approfondimento del funzionamento dei calcolatori, e di conseguenza degli OS, risulta necessario introdurre un concetto a cui si è già accennato alcune volte in precedenza: il "**processo**". Quando parliamo di processi, di cosa si parla concretamente?

Possiamo definire i processi mettendoli a paragone con i **programmi**:
- un **programma** è definito come un **file eseguibile contenuto nella memoria**, che contiene generalmente l'insieme delle istruzioni necessarie per conseguire uno scopo specifico;
- un **processo**, invece, è definito come **un'istanza particolare di un programma in esecuzione, quando viene caricato nella memoria principale**.

Possiamo, dunque, differenziare queste due entità vedendo il programma come un qualcosa di **statico e "passivo"**, mentre il processo come più **dinamico e "attivo"**. Naturalmente, possono esistere **più processi che eseguono lo stesso programma contemporaneamente** (ad esempio, potrebbero essere attive più istanze di un browser sul calcolatore allo stesso tempo), ma **ognuno di questi processi possiede un proprio stato**, distinto dagli altri. 

In questo capitolo, risponderemo a varie domande importanti sui processi. Come vengono rappresentati nell'OS? Quali sono i possibili stati in cui si può trovare un processo, e come viene gestita la transizione tra uno stato e un altro? Come vengono creati concretamente i processi? Come comunicano tra di loro due o più processi?

## Come vengono rappresentati i processi?

Vediamo, prima di tutto, **come sono concretamente rappresentati e conservati i processi nel calcolatore**. L'OS fornisce a ogni processo lo stesso **[[SO1_02 - OS e HW#Memoria virtuale|spazio di indirizzamento virtuale]]** possibile, e tale intervallo di indirizzi di memoria virtuale validi **dipende dal calcolatore e dall'architettura dello stesso** (ad esempio, in un'architettura a 32 bit, gli indirizzi virtuali possono trovarsi nell'intervallo $[0,\, 2^{32}-1]$, ad eccezione di alcuni indirizzi che vengono riservati al kernel dell'OS).

All'interno di questo spazio di indirizzamento, si individuano generalmente più **sezioni**, ciascuna dedicata a uno scopo ben preciso:
- come abbiamo detto, una parte dello spazio di indirizzamento è dedicata al **kernel dell'OS**;
- un'altra sezione è "**Text**", dove vengono contenute tutte le istruzioni da eseguire;
- poi, abbiamo le sezioni "**Data**" e "**BSS**", con la prima che contiene variabili globali o statiche inizializzate, mentre la seconda contiene variabili globali o statiche non inizializzate o inizializzate a $0$;
- troviamo, in seguito, la sezione "**Stack**", che come suggerisce il nome contiene lo stack effettivo del processo, ossia una struttura di tipo LIFO (Last In, First Out) utilizzata per conservare i dati necessari per una chiamata a funzione;
- infine, individuiamo la sezione "**Heap**", che viene utilizzata per l'allocazione dinamica.

Vediamo un esempio concreto, per capire meglio che ruolo hanno queste sezioni nell'esecuzione di un programma, e dunque in un processo concreto. Supponiamo di avere il seguente programma:

```
int w = 42;
int x = 0;
float y;

void doSomething(int f) {
	int z = 37;
	z += f;
	...
}

int main() {
	char* c = malloc(128);
	int k = 12;
	doSomething(k);
	...
}
```

Seguendo passo passo l'esecuzione del programma, vediamo come si comportano le varie sezioni della memoria. Innanzitutto, vengono dichiarate tre variabili globali `w`, `x` e `y`: di queste, `w` viene inizializzata a $42$, `x` a $0$ e `y` non viene inizializzata affatto; di conseguenza, `w` verrà conservata nella sezione Data, mentre `x` e `y` nella sezione BSS. Nella sezione Text, invece, rientreranno le istruzioni concretamente da eseguire (naturalmente non scritte in C come nel programma, ma compilate in linguaggio assembly e, di conseguenza, in binario). A questo punto, si entra nella funzione `main()`, in cui viene eseguita prima di tutto l'istruzione `char* c = malloc(128)`, che porta all'allocazione di memoria nello Stack per la variabile `c`, poi l'istruzione `int k = 12`, che porta alla memorizzazione di `k` nello Stack, dopo `c`. La chiamata alla funzione `doSomething(k)`, infine, provoca l'entrata in gioco dell'Heap, e così via.

##### Un approfondimento sullo Stack

Come accennato, lo **stack** è una struttura dati lineare e ordinata di tipo **LIFO**, ossia "**Last In, First Out**": ciò implica che **l'ultimo elemento ad essere inserito nello stack sarà il primo ad essere eventualmente rimosso**. Per comprendere meglio il concetto, può essere utile immaginare lo stack come una torre di mattoncini: la torre cresce verticalmente, con i mattoncini che vengono aggiunti in cima ad essa, e se si vuole rimuovere un mattoncino si dovrà necessariamente rimuovere quello in cima, ossia l'ultimo aggiunto. Lo stack, come struttura dati, si comporta in maniera esattamente analoga.

Sullo stack, dunque, sono definite **due operazioni**:
- il "**push**", utilizzato per conservare elementi nello stack (equivale ad aggiungere un mattoncino);
- il "**pop**", utilizzato per rimuovere elementi dallo stack (equivale a rimuovere un mattoncino).

Per il corretto utilizzo dello stack, generalmente il calcolatore possiede un **registro dedicato a conservare lo "stack pointer"** (ad esempio `esp` o `sp`), ossia l'**indirizzo di memoria della cima dello stack**. Convenzionalmente, uno stack cresce dall'alto verso il basso, ossia **da indirizzi di memoria più alti a indirizzi più bassi**.

Ogni chiamata a funzione va ad utilizzare una porzione dello stack, che possiamo definire "**stack frame**". In un momento generico, potrebbero esistere anche più stack frames contemporaneamente (ad esempio, nel caso di chiamate a funzione annidate), tuttavia **solo uno stack frame sarà attivo alla volta**. Ciascun stack frame è diviso in **tre parti**, in base ai contenuti delle stesse:
- i parametri della funzione e l'indirizzo di memoria del valore ritornato;
- un puntatore allo stack frame precedente a quello corrente;
- eventuali variabili locali.

Di queste tre parti, **la prima è responsabilità del chiamante**, dato che è il programma che chiama una funzione a stabilire quali parametri darle, mentre **la seconda e la terza sono responsabilità del chiamato**.

Per comprendere meglio il funzionamento dello stack frame, vediamo un esempio. Supponiamo che venga chiamata la funzione:

```
foo(a, b, c);
```

A livello di stack, chiamare questa funzione equivale a eseguire le seguenti operazioni:

```
push c
push b
push a
call foo
```

Ogni parametro, uno alla volta, viene così inserito nello stack, che cresce verso il basso; per ogni parametro inserito, dunque, il valore dello stack pointer viene decrementato di un certo numero di byte (il numero specifico dipende dall'architettura). In seguito, la chiamata `call foo` inserirà implicitamente l'indirizzo di ritorno nello stack.

Sorge, a questo punto, una problematica: essendo lo stack pointer un indirizzo dinamico, che varia ogni volta che viene inserito o rimosso un elemento dallo stack, ora come ora **non è presente un riferimento fisso allo stack**, e questa assenza rende più difficile alla funzione chiamata accedere ai vari parametri. Una soluzione potrebbe essere l'aggiunta di un "**base pointer**", un puntatore alla base dello stack frame relativo alla chiamata in cui ci si trova, conservato in un altro registro dedicato: in questo modo, si può lasciare lo stack pointer essere dinamico e avere, al tempo stesso, un riferimento fisso in modo da facilitare l'accesso ai singoli parametri. 

In una chiamata a funzione, dunque, si susseguono i seguenti passi: prima di tutto, vengono inseriti nello stack i **parametri della funzione**, e la chiamata in sé porta poi all'inserimento anche dell'**indirizzo di ritorno**:

![[stack_esempio1.png]]

Essendo arrivati alla chiamata effettiva alla funzione `foo(a, b, c)`, **lo stack frame del programma chiamante viene sospeso**, e **inizia quello della funzione chiamata**. A questo punto, viene inserito nello stack anche il **base pointer** (`%ebp`, ossia il contenuto del registro `ebp`):

![[stack_esempio2.png]]

Ora, si va a **sostituire il base pointer con lo stack pointer attuale**. Per chiarire meglio a livello schematico quest'operazione, il base pointer considerato finora, dunque quello relativo allo stack frame chiamante, verrà rinominato da `%ebp` a `%old_ebp`, mentre le occorrenze di `%esp` viste finora nello schema diventeranno `%ebp`, essendo adesso il contenuto del registro `ebp` pari a `%esp`:

![[stack_esempio3.png]]

In questo modo, i parametri della chiamata potranno essere facilmente reperiti tramite il base pointer attuale (quello dello stack frame della funzione chiamata), mentre eventuali **variabili locali** potranno invece essere individuate sfruttando lo stack pointer:

![[stack_esempio4.png]]

Una volta terminata l'esecuzione, per tornare allo stack frame precedente, ossia quello chiamante, basterà **sostituire lo stack pointer con il base pointer dello stack frame chiamante** (`%old_ebp`) e **rimuovere quest'ultimo dallo stack**, in modo da eliminare concretamente lo stack frame della funzione chiamata e ripristinare il base pointer precedente. 
___
## Quali sono i possibili stati di un processo?

In qualsiasi momento, un processo può trovarsi in uno di **5 possibili stati**:
- "**`new`**", in cui il processo è stato appena creato dall'OS;
- "**`ready`**", in cui il processo è pronto ad essere eseguito ma sta aspettando di essere assegnato alla CPU;
- "**`running`**", in cui il processo sta attivamente eseguendo istruzioni sulla CPU;
- "**`waiting`**", in cui il processo ha sospeso la sua esecuzione in attesa di una risorsa o di un evento particolare (ad esempio un input da tastiera, un dato conservato in memoria, un timer, ecc. ecc.);
- "**`terminated`**", in cui il processo ha terminato la sua esecuzione e l'OS può dunque disfarsene.

Possiamo schematizzare questi stati e i possibili passaggi tra uno stato e l'altro nel seguente diagramma a stati:

![[processi_stati.png]]

Vediamo, dunque, che durante l'esecuzione del processo esso può cambiare il proprio stato in base a vari fattori, principalmente attribuibili al **programma** (ad esempio, le system calls), all'**OS** (ad esempio, lo scheduling dell'esecuzione sulla CPU), o **fattori esterni** (ad esempio, le [[SO1_02 - OS e HW#System calls, gestione delle eccezioni e operazioni di I/O|interrupt]] per eventi di I/O).

Analizziamo un esempio concreto e molto semplice, per capire come possono avvenire queste transizioni di stato durante l'esecuzione di un processo. Supponiamo di voler eseguire il seguente programma:

```
int main() {
	...
	printf("Hello World!);
	...
}
```

Appena il processo viene creato, esso si trova nello stato `new`, ed entrerà in seguito nello stato `ready` una volta che sarà pronto ad essere eseguito; quando lo scheduler assegnerà alla CPU il processo che stiamo considerando, esso comincerà effettivamente ad essere eseguito ed entrerà dunque nello stato `running`; tuttavia, una volta arrivato all'istruzione `printf("Hello World!)`, che richiede una [[SO1_02 - OS e HW#System calls, gestione delle eccezioni e operazioni di I/O|system call]] bloccante di I/O per essere eseguita, l'esecuzione del processo viene sospesa ed esso si trova dunque nello stato `waiting`, mentre l'OS procede ad assegnare un altro processo alla CPU; una volta terminata la system call, il processo che stiamo analizzando sarà nuovamente pronto per essere eseguito, rientrando così nello stato `ready`, e quando lo scheduler lo riassegnerà alla CPU entrerà nello stato `running`; infine, al termine della sua esecuzione, si troverà nello stato `terminated`.

##### Il PCB

In generale, lo stato complessivo di un processo consiste almeno nelle seguenti componenti:
- il **codice del programma in esecuzione**;
- i **dati statici del programma in esecuzione**;
- il **program counter**, o **PC**, ossia l'indirizzo della prossima istruzione da eseguire;
- i **registri della CPU**;
- lo **stack frame** del processo in questione;
- l'**heap**;
- l'insieme delle **risorse in utilizzo**;
- lo **stato effettivo del processo**.

Per tenere traccia dello stato dei vari processi, l'OS sfrutta una struttura dati particolare chiamata "**Process Control Block**", o "**PCB**" in breve: all'interno del PCB, verranno conservate la maggior parte delle informazioni appena elencate. L'OS alloca un nuovo PCB alla creazione di un nuovo processo, e lo elimina non appena tale processo conclude la propria esecuzione. Come accennato, nel PCB sono contenute la **maggior parte delle informazioni importanti di un processo**, tra cui:
- lo stato effettivo del processo (`new`, `running`, ecc. ecc.);
- l'ID del processo;
- il PC, lo stack pointer, e altri registri specifici utili;
- l'informazione di scheduling in relazione alla CPU (serve soprattutto per tenere conto della priorità del processo);
- informazioni relative alla gestione della memoria;
- informazioni relative all'utente attuale;
- lo stato dei dispositivi di I/O, nonché una lista di eventuali risorse (principalmente file) aperti o utilizzati dal processo.
___
## Come viene creato e terminato un processo?

##### Creazione di un processo

In generale, **un processo può essere creato da altri processi** mediante delle [[SO1_02 - OS e HW#Categorie di system call|system call]] particolari, ossia quelle inerenti al controllo dei processi. Il processo che ne va a creare un altro viene definito "**padre**" di quest'ultimo, mentre il processo creato prende il nome di "**figlio**"; generalmente, un processo padre condivide risorse e privilegi con il processo figlio, e in base al contesto può interrompere la propria esecuzione in attesa di quella del figlio oppure continuare la sua esecuzione in parallelo.

Qualsiasi processo in un calcolatore possiede un **identificatore di processo**, o in breve **PID**, così come un **identificatore di processo padre**, o in breve **PPID**.

Ma in che modo avviene questa catena di creazione di processi? Vediamo cosa succede tipicamente in **sistemi UNIX**. In questo contesto, il primo "processo" ad essere eseguito all'avvio del calcolatore è il "**process scheduler**", denominato "**`sched`**", a cui viene assegnato $0$ come **PID**. La prima mansione svolta dallo `sched` è la creazione di **`init`**, un nuovo processo che avrà $1$ come **PID** e $0$ come **PPID** (il PID del processo padre, ossia di `sched`); sarà poi `init` ad avviare l'esecuzione degli altri processi più importanti, e a diventare di conseguenza il padre di tali processi.

In base al tipo di sistema, ci sono diverse **system call per creare un processo**: ad esempio, in sistemi UNIX/Linux si utilizza **`fork()`**, mentre su Windows la call utilizzata è **`spawn()`**. C'è anche un'altra differenza tra questi due sistemi, legata invece allo **spazio di indirizzamento dei processi figli**:
- in sistemi UNIX/Linux, lo spazio di indirizzamento del figlio è un **duplicato dello spazio di indirizzamento del padre**, dunque i due processi condivideranno lo stesso programma e gli stessi blocchi di dati in memoria, nonostante ognuno abbia un proprio [[SO1_03 - Processi#Il PCB|PCB]];
- in sistemi Windows, il processo figlio **deriva da un nuovo programma**, dunque avrà uno **spazio di indirizzamento diverso da quello del padre**, con altro codice e altri blocchi di dati (questa soluzione è parzialmente implementata anche nei sistemi UNIX/Linux in certi contesti, in corrispondenza della system call **`exec`**).

Come abbiamo accennato in precedenza, il processo padre può assumere due comportamenti diversi alla creazione del processo figlio: può **attendere l'esecuzione del figlio per proseguire la propria**, oppure può **continuare l'esecuzione in parallelo**, senza bloccaggi. Nel primo caso, il processo padre effettua una system call di tipo **`wait()`**, che mette in pausa la sua esecuzione (si tratta del tipico comportamento di una shell UNIX che attende che termini l'esecuzione dei suoi processi figli per richiedere un nuovo prompt, comportamento che si denota dal simbolo **`>`**); nel secondo caso, invece, il processo padre esegue in parallelo con il processo figlio, magari per tutto il tempo o magari solo in parte (si tratta del tipico comportamento di una shell UNIX che esegue un processo figlio in background, comportamento che si denota dal simbolo **`&`**).

Senza ulteriori accorgimenti, **la chiamata a `fork()` crea sostanzialmente delle copie di processi esistenti**. Seppur interessante, tale funzionalità non risulta però particolarmente utile tutto sommato: infatti, ciò che ci interessa maggiormente è **creare processi nuovi ma differenti**. Per comprendere come sia possibile fare ciò, partiamo da un esempio concreto, considerando il seguente programma:

```
int main() {
	
	string progStr;
	getline(cin, progStr);
	const char *prog = progStr.c_str();
	
	int pid = fork();
	
	if (pid == 0) {
		execlp(prog, prog, 0);
		printf("Can't load the program %s", prog);
	} else {
		sleep(1);
		waitpid(pid, 0, 0);
		printf("Program %s finished", prog);
	}
	
	return 0;
}
```

Analizziamo riga per riga il blocco di codice appena presentato. Le prime tre righe servono a richiedere all'utente il nome di un programma che si desidera eseguire: si dichiara una variabile `progStr` e le si assegna come valore una stringa di testo presa in input dall'utente. In seguito, viene eseguita la riga `int pid = fork()`: con questa riga di codice, andiamo sostanzialmente a creare una copia del processo padre, e dunque da questo momento in poi entrambi i processi (padre e figlio) eseguiranno indipendentemente il codice rimasto nel programma; nella variabile `pid`, dopo l'esecuzione di `fork()`, verrà memorizzato appunto il PID del processo in esecuzione. 

A questo punto, si verifica il valore di `pid`, e in base al processo tale variabile conterrà al suo interno un valore diverso: nel processo padre, `fork()` restituirà il PID del processo figlio, che sarà sicuramente un numero $> 0$; nel processo figlio, `fork()` restituirà $0$; invece, se si è verificato un errore nella creazione del processo figlio, si restituirà $-1$. È proprio in base al valore ritornato da `fork()` che distinguiamo il flusso di esecuzione delle prossime istruzioni. Come abbiamo detto, i due processi attualmente in esecuzione andranno ad eseguire le istruzioni indipendentemente, e dunque l'`if` in cui stiamo entrando imporrà ai processi un comportamento diverso in base alla loro natura. 

Se `pid == 0`, vorrà dire che il processo in questione è il processo figlio, e in tal caso quello che vogliamo fare è eseguire il programma richiesto dall'utente, il cui nome è ora memorizzato in `prog`: per questo scopo utilizziamo l'istruzione `execlp`, che carica il programma il cui nome viene letto da `prog`, e sostanzialmente va a sostituire il programma che stava venendo eseguito dal processo figlio (dunque, seppur il PID del processo rimane lo stesso, il codice e i dati vengono sovrascritti dal nuovo programma, ossia quello indicato da `prog`). È proprio per dimostrare questo funzionamento che viene inserita anche la riga `printf("Can't load the program %s", prog)`: infatti, se il programma `prog` viene caricato con successo, il codice viene sostituito con il suo, e dunque questa riga non dovrebbe essere eseguita dal processo figlio; ciò implica che, se ciò accade, c'è stato un errore nel caricamento del nuovo programma.

Supponendo che non avvengano errori nell'esecuzione di `fork()`, se `pid` non è uguale a $0$ vorrà dire che il processo in questione è invece il processo padre, e in tal caso quello che vogliamo fare è:
- mettere forzatamente in pausa il processo per un breve lasso di tempo con `sleep(1)` (dando un minimo di tempo al processo figlio di iniziare la sua esecuzione);
- far sospendere la propria esecuzione al processo padre in attesa che il processo figlio, ossia il processo con PID pari a `pid`, termini la sua con `waitpid(pid, 0, 0)`;
- eseguire l'istruzione di stampa una volta che il processo figlio ha terminato la sua esecuzione, indicando all'utente che l'esecuzione del programma `prog` è terminata.

Avendo chiaro il modo in cui i processi si sviluppano uno dall'altro, possiamo capire facilmente come ottenere determinate gerarchie di processi ben precise. Ad esempio, se volessimo creare la seguente gerarchia:

![[gerarchia_processi_esempio.png]]

avremmo bisogno di un blocco di codice del genere:

```
int pid = fork();

if (pid == 0) { 

	pid = fork();
	
	if (pid == 0) {
		execlp(...);
	} else {
		...
	}

} else {
	...
}
```

Più in generale, se volessimo creare una sequenza di questo tipo di $n$ processi, avremmo bisogno di una catena di $n-1$ `fork()` che seguano tale struttura. E se invece volessimo creare una struttura come la seguente?

![[gerarchia_processi_esempio1.png]]

In tal caso, quello che dobbiamo fare partendo dal processo $A$ è prima di tutto eseguire una `fork()`, generando il processo $B$, e distinguendo con un `if` se ci si trova nel processo $A$ (padre) o nel processo $B$ (figlio), eseguire un'ulteriore `fork()` nel primo scenario; in questo modo, si avrà che il processo $A$ avrà generato due processi figli distinti. Il blocco di codice corrispondente a ciò è il seguente:

```
int pid = fork();

if (pid == 0) {        // figlio di A (B)
	execlp(...)
} else {               // A
	
	pid = fork();
	
	if (pid == 0) {    // figlio di A (C)
		execlp(...);
	}
}
```

Possiamo generalizzare anche quest'ultima struttura di processi. Supponendo, infatti, di voler creare $n$ processi figli tutti derivanti dallo stesso processo padre, potremmo utilizzare il seguente codice:

```
for (int i = 0; i < n; i++) {
	if (fork() == 0) {
		execlp(...);
	}
}

// far attendere al processo padre il termine dell'esecuzione dei figli
for (int i = 0; i < n; i++) {
	wait(NULL);
}
```

Ricapitolando, vediamo un elenco delle **system call relative alla gestione dei processi** viste finora:
- **`fork()`** viene utilizzata per generare un nuovo processo che rappresenta un esatto duplicato del processo padre;
- **`execlp()`** viene utilizzata per rimpiazzare il programma del processo corrente con un nuovo programma preso in input;
- **`sleep()`** viene utilizzata per sospendere l'esecuzione del processo corrente per un certo periodo di tempo;
- **`wait()`** o **`waitpid()`** vengono utilizzate per sospendere l'esecuzione del processo corrente, aspettando o che un qualsiasi processo o che un processo identificato da un certo PID terminino la propria esecuzione.
___
##### Terminazione di un processo

**Un processo può terminare la propria esecuzione** autonomamente, eseguendo una chiamata alla [[SO1_02 - OS e HW#Controllo dei processi|system call]] **`exit()`**. Tipicamente, questa system call ritorna un valore intero, che verrà poi eventualmente passato al processo padre se quest'ultimo si trovava in attesa dopo una chiamata `wait()`: di norma se il valore intero ritornato è pari a $0$, allora l'esecuzione del processo è terminata con successo, mentre se viene ritornato un valore diverso da $0$ allora potrebbe essersi verificato qualche problema.

I processi possono essere **terminati anche dall'OS** per vari motivi, tra cui:
- l'incapacità dell'OS di fornire determinate risorse al processo;
- l'esecuzione di una chiamata di tipo `kill()`.

È possibile, poi, anche che **un processo padre termini un suo processo figlio**, nell'eventualità in cui il compito ad esso assegnato non sia più necessario. Ma cosa succede se **un processo padre viene terminato prima dei suoi processi figli?** Le precise dinamiche con cui l'OS gestisce questa situazione potrebbero variare da sistema a sistema: ad esempio, in sistemi di tipo UNIX, i cosiddetti **processi "orfani"** sono generalmente ereditati dal processo `init`, e verranno poi terminati da quest'ultimo. 

Quando viene terminata l'esecuzione di un processo, **tutte le risorse di sistema utilizzate dallo stesso vengono rilasciate**, così come eventuali file aperti vengono chiusi, e così via; inoltre, se il processo padre stava attendendo il termine dell'esecuzione del figlio, lo status di terminazione del processo figlio, così come il tempo di esecuzione ed altri dati, vengono ritornati al processo padre (se si tratta di un processo orfano, tali dati vengono ritornati a `init`).

Infine, vi è un caso particolare nelle varie possibilità di terminazione di un processo, ossia il cosiddetto **processo "zombie"**: un processo zombie è **un processo che prova a terminare la propria esecuzione prima che il processo padre cominci ad attendere per tale evento**. Ciò avviene perché, seppur tale processo abbia virtualmente terminato la propria esecuzione, esso occuperà comunque dello spazio e delle risorse dato che non potrà ancora ritornare lo status di terminazione e le altre informazioni al suo processo padre. Di solito, analogamente a ciò che avviene per i processi orfani, anche i processi zombie vengono ereditati da `init` e terminati.
___
## Come vengono programmati i processi nella CPU?

Nel progettare un buon **sistema di scheduling dei processi**, si vogliono conseguire principalmente due obiettivi:
- **mantenere occupata la CPU** il più costantemente possibile;
- **permettere dei tempi di risposta accettabili per qualsiasi programma**, soprattutto per quelli più interattivi.

Per poter rispettare queste aspettative, il "**process scheduler**" dovrà implementare delle strategie opportune per **assegnare e rimuovere processi dalla CPU**. Ciò non è particolarmente immediato, soprattutto se si considera che questi due obiettivi possono essere in conflitto tra di loro: infatti, ogni volta che l'OS deve entrare in gioco per sospendere l'esecuzione di un processo e favorire quella di un altro, verrà utilizzato del tempo in cui la CPU concretamente non lavorerà.

Un metodo abbastanza efficiente per risolvere questa problematica è quello delle cosiddette "**process state queues**". Concretamente, **l'OS mantiene i [[SO1_03 - Processi#Il PCB|PCB]] di tutti i processi esistenti in delle code**: vi è una coda per ognuno dei [[SO1_03 - Processi#Quali sono i possibili stati di un processo?|5 stati]] in cui può trovarsi un processo, e anche una coda per ogni [[SO1_01 - Introduzione#Dispositivi di I/O|dispositivo di I/O]] del calcolatore (si tratta di code dove i processi attendono di ricevere o inviare dati); **quando lo stato di un processo cambia, il PCB del processo viene spostato** dalla coda in cui si trovava a quella relativa al nuovo stato assunto dallo stesso. Di seguito, un esempio delle varie process state queues che l'OS potrebbe dover mantenere:

![[pcb_queues_esempio.png]]

Delle varie code gestite dall'OS, quella che potremmo considerare più importante delle altre è quella relativa allo **stato `running`**, ossia quella contenente i processi attivamente eseguiti dalla CPU. Naturalmente, **la lunghezza di tale coda è limitata dal numero di core del sistema considerato**, dato che un solo processo alla volta può essere eseguito da una CPU. Per quanto riguarda, invece, le altre code, esse hanno potenzialmente una lunghezza pressoché illimitata, dato che non viene posto un limite al numero di processi che possono essere creati (`new`), che possono essere pronti per essere eseguiti (`ready`), che stanno attendendo un qualche evento o dato (`waiting`) o che vengono terminati (`terminated`). 

In base alla frequenza con cui riprogrammano i processi, possiamo dividere i possibili approcci di un process scheduler in tre macro-categorie:
- un "**long-term scheduler**" si attiva a intervalli relativamente lunghi, ed è tipico di un sistema a batch o particolarmente carico;
- un "**short-term scheduler**" si attiva molto frequentemente (in media ogni $100$ millisecondi) e scambia velocemente i processi all'interno della CPU;
- un "**medium-term scheduler**" rappresenta una sorta di via di mezzo, che prioritizza solitamente processi più piccoli e veloci, in modo da liberare il sistema.

Ma come avviene, concretamente, lo scambio di processi in esecuzione all'interno della CPU? La chiave è una procedura chiamata "**context switch**", utilizzata proprio per sospendere l'esecuzione del processo corrente e per permettere alla CPU di eseguirne uno nuovo. Si tratta di un'operazione con **costo alto**, dato che sospendere l'esecuzione del processo corrente implica il salvataggio dell'interezza del suo stato (PC, SP, altri registri, ecc. ecc.) nel relativo PCB, mentre avviare l'esecuzione di un nuovo processo implica il caricamento di quello stesso gruppo di informazioni dal relativo PCB alla CPU. Un context switch **avviene in corrispondenza di una qualsiasi [[SO1_02 - OS e HW#System calls, gestione delle eccezioni e operazioni di I/O|trap]]**: all'occorrenza di una trap, dunque, la CPU dovrà eseguire le seguenti operazioni:
- salvare lo stato del processo corrente;
- passare alla [[SO1_02 - OS e HW#Protezione e sicurezza|modalità kernel]] per gestire la trap;
- restaurare lo stato del processo che si vuole eseguire in seguito.

Un buon sistema di scheduling tiene anche alla cosiddetta "**equità**", ossia al fornire possibilità il più possibile eque a ogni processo di occupare la CPU ed essere eseguito. In questo contesto, possiamo fare una distinzione tra due tipi principali di processo: i **processi vincolati all'I/O** e i **processi vincolati alla CPU**. Mentre i primi sono processi la cui esecuzione necessita di eventi o dati relativi all'I/O, i secondi eseguono perlopiù operazioni computazionali relative alla CPU; dunque, mentre è praticamente inevitabile che i primi sospendano la loro esecuzione almeno una volta, i secondi potrebbero potenzialmente occupare costantemente la CPU, e bloccare così il corretto funzionamento del sistema. Dunque, per evitare che ciò accada, e garantire così la massima equità, **i context switch possono essere attivati anche utilizzando dei timer a livello di HW**, che provocano delle interrupt a intervalli regolari. Tale intervallo corrisponde al cosiddetto "**quanto di tempo**", o "**time slice**", e corrisponde dunque al **tempo massimo che può intercorrere tra due context switch**, in modo da garantire una suddivisione uniforme nell'esecuzione dei processi. Si tratta di un'opzione ampiamente utilizzata, soprattutto nei sistemi moderni, anche per favorire lo [[SO1_01 - Introduzione#Multiprogrammazione|pseudo-parallelismo]] a cui si accennava nell'introduzione di questo corso.

Ma **qual è il quanto di tempo ottimale da porre tra due context switch?** Per poterlo trovare, dobbiamo tenere in conto l'importanza di mantenere un **bilancio tra reattività del sistema e utilizzo della CPU**: infatti, bisogna ricordare che il context switch è un'operazione costosa e che lascia la CPU inutilizzata, dunque diminuire il quanto di tempo e aumentare di conseguenza il numero di context switch porterebbe a una maggiore reattività ma anche a un minore utilizzo della CPU; al tempo stesso, aumentare il quanto di tempo e diminuire di conseguenza il numero di context switch massimizzerebbe l'utilizzo della CPU ma porterebbe a una minore reattività del sistema. Tipicamente, la dimensione scelta per un quanto di tempo si aggira **tra i $10$ e i $100$ millisecondi**.
___
## Come comunicano i processi tra di loro?

I processi possono essere o **indipendenti**, e dunque operare indipendentemente senza influenzare o essere influenzati da altri processi, o **cooperanti**, e dunque operare "insieme" ad altri processi per conseguire un obiettivo comune. Quest'ultima opzione può essere utile per vari motivi, tra cui:
- la **condivisione di informazioni**, che può essere necessaria ad esempio nel momento in cui più processi accedono allo stesso file;
- l'**aumento di velocità nella computazione**, dato che un singolo problema può spesso essere risolto più velocemente se diviso in più sotto-problemi risolti parallelamente da più processi;
- la **modularità**, in contesti in cui dividere un sistema in più "moduli" porta a un aumento dell'efficienza;
- la **convenienza**, dato che un singolo utente potrebbe modificare, compilare o eseguire lo stesso codice in finestre diverse.

La **comunicazione tra due processi cooperanti** può avvenire principalmente in **due modi**: la **memoria condivisa** e il **passaggio di messaggi**.

La **memoria condivisa** risulta essere l'opzione concretamente più veloce, dato che non necessita ulteriori [[SO1_02 - OS e HW#System calls, gestione delle eccezioni e operazioni di I/O|system call]] per funzionare, tuttavia risulta essere più complessa da impostare, e non funziona al meglio se si condivide la memoria tra più calcolatori. È, perciò, preferibile quando si lavora con un grande ammontare di informazioni su un singolo calcolatore. La memoria che viene condivisa in questo contesto è inizialmente contenuta nello spazio di indirizzamento di uno dei processi coinvolti: serviranno dunque specifiche system call per rendere quella memoria disponibile "pubblicamente", e quindi accessibile ad altri processi; quest'ultimi, poi, dovranno eseguire a loro volta altre system call per abbinare la memoria condivisa al loro spazio di indirizzamento. 

Il **passaggio di messaggi**, invece, seppur più lento a causa del bisogno di system call per ogni messaggio trasmesso, è molto più semplice da impostare e si presta bene al lavoro condiviso tra più calcolatori. Per questi motivi, è preferibile quando si lavora con poche informazioni o con trasmissioni poco frequenti, o in generale quando sono coinvolti più calcolatori nella comunicazione. Un sistema di passaggio di messaggi dovrà supportare, come minimo, delle system call per l'invio e per la ricezione di tali messaggi, ma prima ancora si deve assicurare un collegamento tra i processi cooperanti. Nell'implementazione di un sistema del genere, si dovrà pensare a varie problematiche, come ad esempio:
- il mittente comunicherà direttamente col destinatario, o indirettamente attraverso una coda o qualche altra struttura?
- l'invio e la ricezione bloccheranno l'esecuzione dei processi o no?
- come verrà gestita la memoria relativa ai messaggi?
___