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

[slide 33 - 34 - 36 - 37 - 40 - 42/50]
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

[slide 69 - 70]
##### Il PCB

[slide 71 - 79 - 80] 
___
