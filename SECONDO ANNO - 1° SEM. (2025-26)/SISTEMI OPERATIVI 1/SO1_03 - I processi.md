Per proseguire nell'approfondimento del funzionamento dei calcolatori, e di conseguenza degli OS, risulta necessario introdurre un concetto a cui si è già accennato alcune volte in precedenza: il "**processo**". Quando parliamo di processi, di cosa si parla concretamente?

Possiamo definire i processi mettendoli a paragone con i **programmi**:
- un **programma** è definito come un **file eseguibile contenuto nella memoria**, che contiene generalmente l'insieme delle istruzioni necessarie per conseguire uno scopo specifico;
- un **processo**, invece, è definito come **un'istanza particolare di un programma in esecuzione, quando viene caricato nella memoria principale**.

Possiamo, dunque, differenziare queste due entità vedendo il programma come un qualcosa di **statico e "passivo"**, mentre il processo come più **dinamico e "attivo"**. Naturalmente, possono esistere contemporaneamente **più processi che eseguono lo stesso programma contemporaneamente** (ad esempio, potrebbero essere attive più istanze di un browser sul calcolatore allo stesso tempo), ma **ognuno di questi processi possiede un proprio stato**, distinto dagli altri. 

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

Seguendo passo passo l'esecuzione del programma, vediamo come si comportano le varie sezioni della memoria. Innanzitutto, vengono dichiarate tre variabili globali `w`, `x` e `y`: di queste, `w` viene inizializzata a $42$, `x` a $0$ e `y` non viene inizializzata affatto; di conseguenza, `w` verrà conservata nella sezione Data, mentre `x` e `y` nella sezione BSS. Nella sezione Text, invece, rientreranno le istruzioni concretamente da eseguire (naturalmente non scritte in C come nel programma, ma compilato in linguaggio assembly e, di conseguenza, in binario). A questo punto, si entra nella funzione `main()`, in cui viene eseguita prima di tutto l'istruzione `char* c = malloc(128)`, che porta all'allocazione di memoria nello Stack per la variabile `c`, poi l'istruzione `int k = 12`, che porta alla memorizzazione di `k` nello Stack, dopo `c`. La chiamata alla funzione `doSomething(k)`, infine, provoca l'entrata in gioco dell'Heap, e così via.

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

##### Creazione di un processo: processo padre e processo figlio

In generale, **un processo può essere creato da altri processi** mediante delle [[SO1_02 - OS e HW#Categorie di system call|system call]] particolari, ossia quelle inerenti al controllo dei processi. Il processo che ne va a creare un altro viene definito "**padre**" di quest'ultimo, mentre il processo creato prende il nome di "**figlio**"; generalmente, un processo padre condivide risorse e privilegi con il processo figlio, e in base al contesto può interrompere la propria esecuzione in attesa di quella del figlio oppure continuare la sua esecuzione in parallelo.

Qualsiasi processo in un calcolatore possiede un **identificatore di processo**, o in breve **PID**, così come un **identificatore di processo padre**, o in breve **PPID**.

Ma in che modo avviene questa catena di creazione di processi? Vediamo cosa succede tipicamente in **sistemi UNIX**. In questo contesto, il primo "processo" ad essere eseguito all'avvio del calcolatore è il "**process scheduler**", denominato "**`sched`**", a cui viene assegnato $0$ come **PID**. La prima mansione svolta dallo `sched` è la creazione di **`init`**, un nuovo processo che avrà $1$ come **PID** e $0$ come **PPID** (il PID del processo padre, ossia di `sched`); sarà poi `init` ad avviare l'esecuzione degli altri processi più importanti, e a diventare di conseguenza il padre di tali processi.

In base al tipo di sistema, ci sono diverse **system call per creare un processo**: ad esempio, in sistemi UNIX/Linux si utilizza **`fork()`**, mentre su Windows la call utilizzata è **`spawn()`**. C'è anche un'altra differenza tra questi due sistemi, legata invece allo **spazio di indirizzamento dei processi figli**:
- in sistemi UNIX/Linux, lo spazio di indirizzamento del figlio è un **duplicato dello spazio di indirizzamento del padre**, dunque i due processi condivideranno lo stesso programma e gli stessi blocchi di dati in memoria, nonostante ognuno abbia un proprio [[SO1_03 - I processi#Il PCB|PCB]];
- in sistemi Windows, il processo figlio **deriva da un nuovo programma**, dunque avrà uno **spazio di indirizzamento diverso da quello del padre**, con altro codice e altri blocchi di dati (questa soluzione è parzialmente implementata anche nei sistemi UNIX/Linux in certi contesti, in corrispondenza della system call **`exec`**).

Come abbiamo accennato in precedenza, il processo padre può assumere due comportamenti diversi alla creazione del processo figlio: può **attendere l'esecuzione del figlio per proseguire la propria**, oppure può **continuare l'esecuzione in parallelo**, senza bloccaggi. Nel primo caso, il processo padre effettua una system call di tipo **`wait()`**, che mette in pausa la sua esecuzione (si tratta del tipico comportamento di una shell UNIX che attende che termini l'esecuzione dei suoi processi figli per richiedere un nuovo prompt, comportamento che si denota dal simbolo **`>`**); nel secondo caso, invece, il processo padre esegue in parallelo con il processo figlio, magari per tutto il tempo o magari solo in parte (si tratta del tipico comportamento di una shell UNIX che esegue un processo figlio in background, comportamento che si denota dal simbolo **`&`**).



[slide 19/22]

[04, slide 25 - 28 - 29 - 32 - 36 - 38/40 - 42 - 43 - 45 - 46 - 48 - 52 - 54 - 56 - 58 - 61 - 63]
___
