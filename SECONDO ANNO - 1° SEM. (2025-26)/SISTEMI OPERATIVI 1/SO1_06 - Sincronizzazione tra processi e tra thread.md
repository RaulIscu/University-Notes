Abbiamo ben stabilito, a questo punto, che processi e thread possono cooperare per arrivare a un obiettivo comune. Tuttavia, spesso è necessaria una **sincronizzazione tra i vari thread o processi in esecuzione** per permettere una cooperazione senza intoppi: ciò è dovuto all'eventuale presenza delle cosiddette "**sezioni critiche**", dette anche "**regioni critiche**".

Per capire l'importanza della sincronizzazione, consideriamo un banale esempio concreto. Immaginiamo di seguire due coinquilini, chiamati Bob e Carla, durante il loro pomeriggio: Bob arriva a casa alle $17:00$, guarda nel frigorifero e nota che è finito il latte, dunque $10$ minuti dopo essere arrivato esce di nuovo per andare al supermercato e comprarne un po'; parallelamente, mentre Bob sta andando al supermercato, anche Carla arriva a casa, e notando anch'essa che manca il latte esce anche lei diretta al supermercato; Bob torna a casa con il latte nello stesso momento in cui Carla arriva al supermercato, e dopo aver lasciato il latte nel frigo continua la sua giornata come niente fosse, aspettando il ritorno di Carla; dopo un po', anche Carla torna a casa, e quando va a lasciare il latte nel frigo si accorge che Bob l'aveva già preso, e di aver preso troppo latte.

Ora, in questo esempio sciocco si ipotizzi che Bob e Carla siano due processi, o due thread, indipendenti ma cooperanti al tempo stesso: teoricamente il loro compito, lo scopo della loro cooperazione, doveva essere comprare del latte, ma data l'assenza di comunicazione tra di essi si è arrivati a una situazione indesiderata. Lo stesso può avvenire all'interno di un calcolatore, e capiamo dunque che **c'è bisogno di un meccanismo che permetta a due processi, o due thread, di comunicare con successo e di avere una visione coerente dello stato della computazione**.

## Sezioni critiche e la "buona" sincronizzazione

Le "**sezioni critiche**" a cui abbiamo accennato a inizio paragrafo rappresentano proprio questo tipo di situazione: sono **parti dell'esecuzione in cui un processo o un thread va a utilizzare o modificare una risorsa condivisa** (nel nostro esempio, il latte nel frigo), e durante le quali è dunque fondamentale che nessun altro processo o thread entri in un'altra sezione critica, dato che ciò potrebbe portare a comportamenti imprevisti o a modifiche non desiderate (nel nostro esempio, il comprare latte in eccesso). Il segreto per la corretta esecuzione delle sezioni critiche sta proprio nella **sincronizzazione**, e il concetto che sta alla base della sincronizzazione è il **far attendere un processo o thread che vuole entrare in una sezione critica se già un altro processo o thread sta eseguendo la propria**. Una corretta implementazione della sincronizzazione deve poter soddisfare **$3$ proprietà**:
1. la "**mutua esclusione**", ossia il fatto che un solo processo o thread alla volta possa trovarsi in una sezione critica della sua esecuzione;
2. la "**vivacità**", ossia il fatto che se nessun processo o thread si trova in una sezione critica, e se uno o più processi o thread vogliono iniziare l'esecuzione di una sezione critica, allora deve essere garantita la possibilità di farlo a uno qualsiasi di essi;
3. l'"**attesa vincolata**", ossia il fatto che un processo o thread che vuole iniziare l'esecuzione di una sezione critica è certo di poterlo fare prima o poi, e che ci sia un limite a quanti altri processi o thread possono eseguire una sezione critica prima di lui.

Riportandoci al nostro esempio concreto: garantire una mutua esclusione significa garantire che non verrà comprato più latte di quanto è necessario (solo una persona, tra Bob e Carla, andrà a comprarlo); garantire vivacità significa garantire che qualcuno vada effettivamente a comprare il latte, ed evitare una possibilità in cui non lo farà né Bob né Carla; garantire un'attesa vincolata significa garantire che, prima o poi, o Bob o Carla andranno a comprare il latte.

Proviamo, a questo punto, a trovare delle soluzioni per risolvere il problema di Bob e Carla e garantire, al tempo stesso, che si verifichino tutte e $3$ le proprietà di una buona sincronizzazione. Una prima soluzione, molto basilare, consiste nel **far lasciare una nota alla persona che sta eventualmente andando a prendere il latte**, rimuovendola una volta comprato:

```
if (!milk and !note) {
	leave_note();
	buy_milk();
	remove_note();
}
```

Questa soluzione non è corretta, perché **non garantisce una mutua esclusione**: venendo eseguiti parallelamente, i due thread Bob e Carla potrebbero benissimo verificare entrambi che non ci sia né il latte né una nota, prima che uno dei due abbia avuto il tempo di affiggere una nota per avvisare il secondo, dunque il risultato è che entrambi i thread penseranno di dover andare a comprare il latte e di conseguenza si comprerà latte in eccesso. Una seconda soluzione, più avanzata, potrebbe essere **lasciare una nota personalizzata subito, prima ancora di controllare se sarà necessario prendere il latte o no**. In questo caso, il thread Bob eseguirà il seguente codice:

```
leave_note(Bob);

if (!note(Carla)) {
	if (!milk) {
		buy_milk();
	}
}

remove_note();
```

mentre il thread Carla eseguirà il seguente codice:

```
leave_note(Carla);

if (!note(Bob)) {
	if (!milk) {
		buy_milk();
	}
}

remove_note();
```

Con questa soluzione garantiamo la mutua esclusione, dato che sicuramente almeno uno dei due thread avrà eseguito, a un certo punto, l'istruzione `leave_note()`, e garantiamo così che al massimo uno dei due thread comprerà il latte; tuttavia, **non è garantita la vivacità**, dato che a causa dello scheduling dei thread può succedere che sia Bob che Carla lascino una nota, e dunque che nessuno dei due abbia la possibilità di andare a comprare il latte. Vediamo una terza soluzione, molto simile alla seconda ma con un piccolo aggiustamento: entrambi i thread, come prima, lasceranno una nota personalizzata subito, ma **uno dei due thread, invece di controllare una volta la presenza o meno di una nota dell'altro, rimarrà in attesa finché ci sarà tale nota, e controllerà se c'è o meno il latte solo dopo**. In questo caso, mentre il codice da far eseguire al thread Carla rimane invariato, al thread Bob si assegna il seguente codice leggermente modificato:

```
leave_note(Carla);

while(note(Carla)) {
	do_nothing();
}

if (!milk) {
	buy_milk();
}

remove_note();
```

**Questa soluzione rispetta tutte e $3$ le proprietà di una buona sincronizzazione**: viene garantita la mutua esclusione, dato che il sistema di note eviterà che i due thread comprino il latte contemporaneamente; viene garantita la vivacità, dato che ora entrambi avranno sicuramente una possibilità di eseguire la loro sezione critica, ossia di verificare se è presente del latte e in caso di andarlo a comprare; viene garantita l'attesa vincolata, dato che il thread Bob, che potrebbe eventualmente dover attendere a causa della presenza della nota di Carla, prima o poi eseguirà sicuramente la sua sezione critica dato che Carla prima o poi rimuoverà la sua nota.

In realtà, tale soluzione non è propriamente una "buona" soluzione, e sicuramente non è la soluzione ottimale che si poteva trovare, dato che presenta i seguenti difetti:
- è relativamente complessa e contorta;
- è necessario un programma diverso per i due thread, e all'aumentare dei thread questa asimmetria rischia di diventare incontrollabile;
- il thread Bob, mentre esegue il ciclo `while`, occupa un processore senza fare nulla di utile.
___
## Implementare la sincronizzazione

Ma allora come possiamo **implementare dei buoni meccanismi di sincronizzazione**? Per farlo, avremo bisogno di strumenti appropriati, i cosiddetti "**costrutti primitivi**", forniti dai linguaggi di programmazione e utilizzati per costruire una corretta sincronizzazione tra processi e thread. Ci concentreremo principalmente su $3$ di questi costrutti primitivi, ossia:
- i "**locks**", che vengono "occupati" da un processo o thread quando questo esegue una [[SO1_06 - Sincronizzazione tra processi e tra thread#Sezioni critiche e la "buona" sincronizzazione|sezione critica]] e "rilasciati" una volta che termina l'esecuzione di quest'ultima;
- i "**semafori**", che in parole povere costituiscono una generalizzazione dei locks;
- i "**monitors**", utilizzati sostanzialmente per condividere dati in comune.

##### Locks

I **locks** sono costrutti che, come suggerisce il nome, possono essere utilizzati per **"bloccare" l'esecuzione contemporanea di più di una sezione critica alla volta**: dunque, contribuiscono soprattutto a garantire la **[[SO1_06 - Sincronizzazione tra processi e tra thread#Sezioni critiche e la "buona" sincronizzazione|mutua esclusione]]** tra processi e thread.

Concretamente, il lock può essere visto come una sorta di **lasciapassare per l'esecuzione di sezioni critiche**: esiste un solo lasciapassare, e se un processo o thread vuole eseguire una sezione critica deve necessariamente disporre di quest'ultimo; se nessuno lo sta utilizzando, allora può prenderlo e se lo terrà finché non terminerà l'esecuzione della sezione critica, dopodiché lo lascerà nuovamente libero e disponibile; se un processo o thread cerca di eseguire una sezione critica mentre il lasciapassare non è disponibile, esso viene messo in attesa e potrà partire con l'esecuzione quando sarà finita quella del processo o thread che stava occupando il lasciapassare. Dunque, possiamo definire le seguenti **regole per l'utilizzo di lock**:
1. bisogna sempre acquisire il lock se si vuole eseguire una sezione critica (ad esempio, se si vuole accedere o modificare dei dati condivisi);
2. bisogna sempre rilasciare il lock quando si termina l'esecuzione di una sezione critica;
3. per poter acquisire il lock, esso deve essere libero e non acquisito da nessun altro.

Il lock, per permettere tale funzionamento, presenta due "**primitive atomiche**", dove con "atomiche" si intende che **la loro esecuzione non può essere interrotta**:
- **`lock.acquire()`**, che acquisisce il lock o, se è occupato, attende che venga rilasciato per farlo;
- **`lock.release()`**, che rilascia il lock e notifica eventuali thread che lo stavano aspettando.

Applicando il lock all'esempio visto nel [[SO1_06 - Sincronizzazione tra processi e tra thread#Sezioni critiche e la "buona" sincronizzazione|paragrafo precedente]], abbiamo che i thread Bob e Carla, per ottenere l'obiettivo desiderato, possono eseguire questo semplice blocco di codice, uguale per entrambi:

```
lock.acquire();

if (!milk) {
	buy_milk();
}

lock_release();
```

In questo modo, si ottiene una soluzione corretta, pulita e simmetrica.

Ma come possiamo **implementare concretamente una lock**? Lo scopo delle lock è di evitare che lo [[SO1_04 - Scheduling della CPU#Introduzione allo scheduling|scheduler della CPU]] prenda il controllo ed esegua un context switch durante l'esecuzione di una sezione critica; per fare ciò, dobbiamo prevenire:
- **eventi interni**, ossia eventi in cui il thread considerato sospende volontariamente la propria esecuzione (ad esempio, in corrispondenza di una richiesta di I/O);
- **eventi esterni**, ossia interrupts che portano lo scheduler ad attivarsi e a rimpiazzare il thread attualmente in esecuzione.

Per gestire la prima di queste evenienze, basta **evitare che i thread facciano richieste di I/O all'interno dell'esecuzione di una sezione critica**; tuttavia, il discorso si complica per la gestione degli eventi esterni, dato che in questo caso si dovrà pensare ad esempio a **disabilitare momentaneamente le interrupts**, e dunque forzare un ritardo nella gestione di un certo evento esterno da parte dell'HW finché il thread che stiamo considerando non avrà terminato l'esecuzione della sezione critica. Ciò potrebbe essere ottenuto **implementando `acquire()` e `release()` come system call**, ossia come istruzioni privilegiate che non potranno essere bloccate, che tra le altre cose rispettivamente disabilitano e riabilitano le interrupts. Tuttavia, seppur sembri una soluzione semplice ed efficace al nostro problema, questo approccio presenta numerosi difetti: intanto **non funzionerebbe su sistemi con più processori**; oltre a ciò, **un programma pesante o maligno potrebbe abusare di questa caratteristica**, occupando indefinitamente la CPU e bloccando di conseguenza tutto il sistema; poi, disabilitare le interrupts in generale potrebbe portare alla **perdita di interrupts importanti**, oltre ad essere alla lunga un'**operazione abbastanza inefficiente**.

Un'altra alternativa potrebbe essere implementare i lock con una struttura simile alla seguente:

```
class Lock {
	private int flag;
	
	Lock() {
		this.flag = 0;
	}
	
	public void acquire(Thread t) {
		while(this.flag == 1) {
			// do nothing
		}
		
		this.flag = 1;
	}
	
	public void release() {
		this.flag = 0;
	}
}
```

sfruttando dunque un attributo `flag` che indichi quando il lock è occupato (`1`) e quando è libero (`0`). Tuttavia, questa soluzione riscontra un altro problema: **non garantisce la mutua esclusione**. Potrebbe infatti succedere, assumendo che si parta con `flag = 0`, che un thread $A$ cerchi di acquisire il lock, e che un interrupt sostituisca il thread con un altro thread $B$ prima che $A$ possa eseguire l'istruzione `this.flag = 1`, ma dopo aver verificato la condizione che controlla il ciclo `while`; in questo modo, se $B$ finirà per settare `flag` a `1`, e un altro interrupt restituirà il controllo ad $A$, anche quest'ultimo cercherà di settare lo stesso valore, e avremo tecnicamente due thread che acquisiscono il lock nello stesso momento, cosa che non dovrebbe essere possibile. Oltre a ciò, notiamo anche che **l'implementazione di `acquire()` prevede di far occupare la CPU a un thread senza fare nulla** per un determinato lasso di tempo.

A questo punto, arriviamo a un'alternativa comoda e sicura, abilitata in parte dall'HW, e a cui abbiamo accennato [[SO1_02 - OS e HW#Scheduling e sincronizzazione|qualche capitolo fa]]: le **istruzioni atomiche**, ossia **istruzioni durante l'esecuzione delle quali non possono avvenire interrupts**, e che quindi terminano sempre la loro esecuzione "in un colpo solo". Alcuni esempi tipici di istruzioni atomiche sono:
- **`test&set`**, che scrive `1` in una determinata cella di memoria e restituisce il valore contenuto in precedenza nella stessa;
- **`fetch&add`**, che incrementa di un certo valore i contenuti di una determinata cella di memoria;
- **`compare&swap`**, o **`compare&exchange`**, che confronta il contenuto di una determinata cella di memoria con un valore dato e, se sono uguali, modifica tale contenuto in un nuovo valore.

A questo punto, proviamo a **implementare il meccanismo di lock sfruttando ad esempio l'istruzione atomica `test&set`**:

```
class Lock {
	private int flag;
	
	Lock() {
		this.flag = 0;
	}
	
	public void acquire() {
		while(test&set(this.flag) == 1) {
			// do nothing
		}
	}
	
	public void release() {
		this.flag = 0;
	}
}
```

Al momento della chiamata `test&set(this.flag)`, se `this.flag` è pari a `0` (dunque se il lock è libero) allora la chiamata leggerà e restituirà `0` e, al contempo, assegnerà `this.flag = 1`, quindi occuperà il lock e non entrerà nel ciclo di attesa, consentendo così l'esecuzione indisturbata della sezione critica; invece, se `this.flag` è pari a `1` (dunque se il lock è occupato) allora la chiamata leggerà e restituirà `1` e, al contempo, assegnerà `this.flag = 1`, che era il valore già contenuto in precedenza in tale parte di memoria, quindi il lock rimarrà occupato e il thread in questione attenderà senza fare nulla finché il lock non verrà rilasciato. Abbiamo, così, ottenuto un'implementazione di lock più soddisfacente, che garantisce la mutua esclusione.

Ciononostante, troviamo ancora dei difetti: ad esempio, continua a presentarsi un qualche **ciclo in cui la CPU viene occupata senza svolgere alcuna mansione**; inoltre, non è chiaramente specificato come ci si comporterà nel momento in cui ci saranno **più thread, magari con diverse priorità, ad attendere il rilascio del lock**.

Per risolvere il primo problema, possiamo utilizzare una primitiva dell'OS che porta il thread chiamante a rilasciare la CPU, ossia **`yield()`**: basterà inserire una chiamata a `yield()` all'interno del corpo del ciclo contenuto in `acquire()`, in modo da rilasciare subito la CPU se il thread vuole eseguire una sezione critica e il lock è già occupato. E per quanto riguarda l'attesa di più thread per il rilascio del lock? Quest'ultimo problema viene in realtà ignorato dalla soluzione appena ipotizzata, ma possiamo trovarne un'altra che li risolve entrambi contemporaneamente, con un'implementazione di lock che presenta le seguenti caratteristiche principali:
- aggiungiamo come attributo una **coda `q`**, destinata ad ospitare i thread in attesa di acquisire il lock;
- utilizziamo le system calls **`park()`** e **`unpark(t)`**, con la prima che quando eseguita sospende l'esecuzione del thread chiamante e lo mette in attesa, e la seconda che quando eseguita risveglia il thread `t`, reinserendolo nella coda `ready`.

Vediamo il codice:

```
class Lock {
	private int flag, guard;
	private Queue q;
	
	Lock() {
		this.flag = 0;
		this.guard = 0;
		this.q = new Queue();
	}
	
	public void acquire(Thread t) {
		while (test&set(this.guard) == 1) {
			// do nothing
		}
		
		if (this.flag == 0) {
			this.flag = 1;
			this.guard = 0;
		} else {
			this.q.push(t);
			this.guard = 0;
			park();
		}
	}
	
	public void release() {
		while (test&set(this.guard) == 1) {
			// do nothing
		}
		
		if (q.is_empty()) {
			this.flag = 0;
		} else {
			t = q.pop();
			unpark(t);
		}
		
		this.guard = 0;
	}
}
```

A questo punto, cerchiamo di spiegare in parole povere cosa succede. Dall'implementazione precedente, manteniamo l'attributo `flag`, indicatore dell'occupazione o meno del lock; oltre ad esso, però, troviamo anche `q`, ossia la coda dove saranno ospitati i thread in attesa di acquisire il lock, e `guard`, un attributo che, per certi versi, può essere visto come un lock a sua volta: all'interno del codice, in particolare quello relativo ad `acquire(t)` e `release()`, notiamo che se il thread rileva che `guard == 1`, esso verrà messo in attesa e non eseguirà nulla dato che ciò implica che un altro thread sta già acquisendo o rilasciando il lock, e tale operazione non permette interferenze (in poche parole, dunque, `guard` contribuisce a garantire la mutua esclusione). Il lock viene inizializzato come libero in tutti i sensi, e la sua coda di thread è inizialmente vuota. Ora, nel momento in cui **un thread cerca di acquisire il lock** (dunque chiama `acquire(t)`), la prima cosa che succede è il **controllo di `guard`**: se `guard` è settato a `0`, il thread in questione può procedere e l'attributo viene settato a `1` per prevenire interferenze da parte di altri thread; se `guard` è settato a `1`, il thread in questione viene messo in attesa. Ora, supponendo che si possa effettivamente procedere con il tentativo di acquisizione, il prossimo passo è **controllare `flag`**: se `flag == 0`, vuol dire che il lock è libero e dunque disponibile ad essere acquisito, quindi `flag` viene settato a `1` e, essendo terminata l'operazione di acquisizione, `guard` viene settato nuovamente a `0`; invece, se `flag == 1`, vuol dire che il lock è già occupato da qualche altro thread, dunque in questo caso il thread in questione viene aggiunto alla coda `q` e messo in attesa, mentre `guard` anche in questo caso viene nuovamente settato a `0`. Vediamo, adesso, che succede quando **un thread rilascia il lock** (dunque chiama `release()`): anche stavolta, la prima cosa che avviene è il **controllo di `guard`**, con lo stesso identico funzionamento valido per `acquire(t)`; a questo punto, si va a **controllare se la coda `q` è vuota o meno**, e se `q` è vuota allora non ci sono thread in attesa di acquisire il lock, dunque lo si può semplicemente liberare settando `flag` a `0` e, in seguito, anche `guard` a `0`, mentre se `q` contiene almeno un thread allora si estrae il primo (la coda è di tipo FIFO) thread dalla coda e lo si "sveglia". Si noti che, nel momento in cui viene svegliato un altro thread, dunque in corrispondenza della chiamata a `unpark(t)`, `flag` non viene settato a `0`, dunque è come se il lock venisse direttamente passato da un thread a un altro, rimanendo occupato tutto il tempo.

Purtroppo, non siamo comunque in grado di eliminare completamente eventuali momenti in cui la CPU è occupata senza eseguire nulla, ma con questo approccio si minimizzano tali frangenti di tempo il più possibile. Un problema che può sorgere e che è invece riparabile è l'eventualità che avvenga un context switch precisamente prima che venga chiamata `park()`: per evitare che ciò accada, si può utilizzare un'altra primitiva dell'OS, **`setpark()`**, che sostanzialmente dà un preavviso del fatto che il thread chiamante sta per essere messo in attesa; inserendo una chiamata a `setpark()` prima dell'istruzione `this.guard = 0` nel corpo di `acquire(t)` risolviamo il problema.
___
##### Semafori

Un'altra alternativa per garantire la mutua esclusione in presenza di sezioni critiche è il cosiddetto "**semaforo**". Si tratta di una sorta di **generalizzazione dei [[SO1_06 - Sincronizzazione tra processi e tra thread#Locks|locks]]**, inventata da Dijkstra nel 1965, e oltre al suo scopo principale può anche essere utilizzata come una forma di "**contatore atomico**".

Un semaforo può essere definito come un **tipo speciale di valore intero**, che supporta principalmente **$2$ istruzioni atomiche**:
- **`wait()`**, o **`P()`**, un decremento che nel nostro contesto indica un blocco, in vigore finché il semaforo non viene aperto;
- **`signal()`**, o **`V()`**, un incremento che nel nostro contesto permette a un thread di "passare".

Associata a ogni semaforo troviamo una **coda di processi o thread in attesa**, e nel momento in cui un thread effettua una **chiamata a `wait()`**, **l'esecuzione del thread continua solo se il semaforo è "aperto"**, altrimenti **il thread viene bloccato e aggiunto alla coda**. Invece, una **chiamata a `signal()` apre il semaforo**, e se è presente un thread nella coda allora **il thread in questione viene sbloccato**, mentre se non ci sono thread nella coda allora questa "apertura" viene memorizzata per l'eventuale arrivo di un prossimo thread. Dunque, indicando con `S` un semaforo, idealmente un flusso di esecuzione di una sezione critica sfruttando questo strumento dovrebbe rispecchiare il seguente:

```
S.wait();     // attendi finché S non è "aperto"

<sezione critica dell'esecuzione>

S.signal();   // aprire il semaforo e notificare eventuali thread
```

Nel momento in cui un processo o thread effettua una chiamata `S.wait()`, se il semaforo è aperto la sua esecuzione continua indisturbata nella sezione critica, mentre se è chiuso allora l'OS metterà in attesa tale processo o thread, inserendolo nella coda; con la chiamata a `S.signal()`, invece, viene sbloccato un processo o thread dalla coda in attesa, e si apre il semaforo.

In questo paragrafo, approfondiremo principalmente **due tipi di semafori**:
- i "**semafori binari**";
- i "**semafori di conteggio**".

Partiamo dai primi. I **semafori binari** hanno come obiettivo principale il **garantire la mutua esclusione tra sezioni critiche**, e dunque sono sostanzialmente **analoghi ai locks**; la variabile intera associata ad essi (ricordiamo che i semafori sono una sorta di "sovrastruttura" costruita su un valore intero) può assumere solo due valori, `0` o `1`, dove generalmente `0` indica un semaforo chiuso e `1` ne indica uno aperto, e sono inizializzati come aperti.

Essendo sostanzialmente analoghi ai lock, i semafori binari sono un'alternativa perfettamente viabile per risolvere il problema del latte che abbiamo utilizzato come esempio dall'[[SO1_06 - Sincronizzazione tra processi e tra thread#Sezioni critiche e la "buona" sincronizzazione|inizio del capitolo]]. Basterà sostituire alle chiamate `lock.acquire()` e `lock.release()` delle chiamate `S.wait()` e `S.signal()`, nel modo seguente:

```
S.wait();

if (!milk) {
	buy_milk();
}

S.signal();
```

Un **semaforo di conteggio**, invece, rappresenta sostanzialmente una generalizzazione dei semafori binari. In questo caso, il valore intero di riferimento non indica più semplicemente uno stato di apertura o di chiusura del semaforo, ma **il numero di thread che possono passare**, e dunque tecnicamente il **numero di risorse disponibili**: 
- se il valore è $> 0$, allora potranno "passare" tanti thread quanto è il valore;
- se il valore è $\leq 0$, nessun thread potrà passare, e il valore assoluto di tale numero indicherà quanti thread si trovano già in attesa nella coda.

Per comprendere meglio il **funzionamento interno di un semaforo di conteggio**, diamo un'occhiata a una sua possibile implementazione:

```
class Semaphore {
	private int value, guard;
	private Queue q;
	
	Semaphore(int val) {
		this.value = val;
		this.q = new Queue();
	}
	
	public void wait(Thread t) {
		while (test&set(this.guard) == 1) {
			// do nothing
		}
		
		this.value -= 1;
		
		if (this.value < 0) {
			q.push(t);
			this.guard = 0;
			park();
		} else {
			this.guard = 0;
		}
	}
	
	public void signal() {
		while (test&set(this.guard) == 1) {
			// do nothing
		}
		
		this.value += 1;
		
		if (!q.is_empty()) {
			t = q.pop();
			unpark(t);
		}
		
		this.guard = 0;
	}
}
```

Un semaforo di conteggio non viene necessariamente inizializzato con `1` come valore `value`, ma dipende dal contesto; invece, la sua coda `q` partirà sempre come vuota.

Ora, diamo un'occhiata all'implementazione del metodo **`wait(Thread t)`**. Notiamo che inizialmente esso è perfettamente analogo al metodo `acquire(t)` dei locks: infatti, anche in questo caso, la prima cosa che andiamo a fare è controllare e settare il valore di `guard`, ed eventualmente obbligare il processo o thread a non fare nulla. In seguito, andiamo a **diminuire di $1$ il valore di `value`**, sostanzialmente dichiarando l'intenzione del thread di accedere a una risorsa, e dunque di eseguire una sezione critica. Dopo tale decremento, **se `value` è diventato negativo, ciò indica che non ci sono risorse libere al momento**, e dunque che il thread non potrà eseguire in sicurezza la sua sezione critica: perciò, in questo caso il processo o thread viene messo in attesa nella coda FIFO `q`, si setta `guard` a `0` e si sospende la sua esecuzione con `park()`; invece, **se `value` non è diventato negativo, ciò vuol dire che il thread potrà procedere con l'esecuzione della sua sezione critica**, dunque l'unica istruzione che viene eseguita è il settare `guard` a `0` per permettere ad altri thread di eseguire le loro rispettive chiamate a `wait()` o a `signal()`.

Passiamo, ora, al metodo **`signal()`**. Anche in questo caso, il ciclo iniziale rimane perfettamente analogo a quelli già visti finora. In seguito, si va ad **aumentare di $1$ il valore di `value`**, sostanzialmente indicando che una risorsa sta venendo liberata, e poi si va a **verificare se ci sono dei processi o thread in attesa**: se ciò è vero, dunque se la coda `q` non è vuota (in altre parole, se `value <= 0`), si estrae un processo dalla coda e lo si "risveglia". A questo punto, l'ultima cosa che rimane da fare è settare `guard` a `0`.

Oltre all'obiettivo già esplicitato del garantire la mutua esclusione, i semafori possono essere utili anche per **mantenere in attesa dei thread in contesti specifici**. Ad esempio, supponendo che ci siano due thread $A$ e $B$, con $B$ che attende il termine dell'esecuzione di $A$ tramite una chiamata di tipo `waitpid()` per fare qualcosa, è possibile abilitare questo meccanismo inizializzando un semaforo con `value = 0`, inserendo una chiamata `S.wait()` nel codice di $B$ prima di tale blocco di esecuzione, e una chiamata `S.signal()` al termine dell'esecuzione di $A$.

Seppur siano uno strumento molto potente, **i semafori non sono perfetti** e presentano alcuni difetti e limiti, tra cui:
- il fatto che sono, sostanzialmente, delle semplici variabili globali può portare a problemi di sicurezza;
- non vi è una diretta connessione tra un semaforo e le risorse verso le quali tale semaforo controlla l'accesso;
- la loro implementazione specifica in base al contesto può dover variare, e in base all'abilità del programmatore il semaforo può funzionare più o meno bene.

Tali difetti sono in parte evitati con lo strumento che vedremo nel prossimo paragrafo: i **[[SO1_06 - Sincronizzazione tra processi e tra thread#Monitors|monitors]]**.
___
##### Monitors

Un **monitor** è un costrutto tipico dei linguaggi di programmazione, il cui scopo principale è **controllare l'accesso a risorse condivise**. Può essere visto, a grandi linee, come **una classe che incorpora dati, operazioni e sincronizzazione** in un unico posto; tuttavia, le differenze principali da una classe normale sono che:
- viene garantita la **mutua esclusione**, e dunque un qualsiasi metodo del monitor può essere eseguito da un solo processo o thread alla volta;
- viene imposto che **tutti i dati siano privati**, ossia accessibili solo dall'interno della classe stessa.

Formalmente, possiamo definire un monitor come un costrutto avente le seguenti proprietà:
- definisce un **[[SO1_06 - Sincronizzazione tra processi e tra thread#Locks|lock]]** e **$0$ o più "variabili di condizione"** per gestire accessi concorrenti alle risorse condivise;
- utilizza il lock per **garantire che al massimo un thread sia attivo nel monitor** in un qualsiasi momento.

È molto semplice, ad esempio, **trasformare una qualsiasi classe Java in un monitor**, infatti per fare ciò basterebbe:
- rendere privati tutti i dati;
- assicurare una buona sincronizzazione tra tutti i metodi non privati.

Fortunatamente, il nostro lavoro viene ancora semplificato proprio dal fatto di star utilizzando Java, in quanto ci viene fornita dal linguaggio la **keyword `synchronized`**, che se abbinata a un metodo ci assicura che tale metodo sia soggetto a mutua esclusione. Se volessimo, ad esempio, implementare un monitor relativo a una coda FIFO `Queue`, un esempio di possibile implementazione è il seguente:

```
class Queue {
	...
	private ArrayList<Item> data;
	...
	
	public void synchronized add(Item i) {
		data.add(i);
	}
	
	public Item synchronized remove() {
		if (!data.isEmpty()) {
			Item i = data.remove(0);
			return i;
		}
	}
}
```

In questo esempio, notiamo però una particolarità che può causare problemi: per natura del metodo `remove()`, che ricordiamo essere sincronizzato, tecnicamente esso dovrebbe attendere che ci sia effettivamente qualcosa da rimuovere nella coda prima di poter procedere nella sua esecuzione; ciò vorrebbe dire che **il thread in questione dovrebbe "dormire" all'interno della sua sezione critica**, ma se avviene ciò, e dunque il thread rimane inattivo mentre detiene il lock, allora nessun altro thread potrà accedere alla coda, aggiungere un elemento ed eventualmente risvegliarlo, portando a una situazione di stallo. 

È in questo contesto che tornano utili le "**variabili di condizione**", che possiamo vedere come **code di thread, ciascuna associata a un lock, dove i thread possono "dormire" in attesa che una certa condizione si verifichi**: la presenza di una variabile di condizione permetterebbe a un thread di attendere all'interno di una sezione critica, mentre **un qualsiasi lock detenuto dal thread verrebbe rilasciato atomicamente prima che quest'ultimo diventi inattivo**. Ogni variabile di condizione deve supportare **$3$ operazioni**:
- **`wait`**, che impone al thread chiamante di rilasciare il lock e di unirsi alla coda di thread in attesa (il tutto atomicamente);
- **`signal`**, che "risveglia" un thread in attesa se esiste, altrimenti la chiamata non risulterà in nulla;
- **`broadcast`**, che "risveglia" tutti i thread eventualmente in attesa.

In Java, tornando al nostro esempio precedente, queste tre operazioni corrispondono rispettivamente alle chiamate **`wait()`**, **`notify()`** e **`notifyAll()`**. Dunque, un'implementazione più corretta della classe `Queue` sarebbe la seguente:

```
class Queue {
	...
	private ArrayList<Item> data;
	...
	
	public void synchronized add(Item i) {
		data.add(i);
		notify();
	}
	
	public Item synchronized remove() {
		while (data.isEmpty()) {
			wait();
		}
		
		Item i = data.remove(0);
		return i;
	}
}
```

Si potrebbe notare una certa **somiglianza tra [[SO1_06 - Sincronizzazione tra processi e tra thread#Semafori|semafori]] e monitors**, dato che entrambi a primo impatto sembrano svolgere le stesse operazioni e anche con nomi pressoché identici. In realtà, ci sono alcune differenze sottili ma sostanziali:
- la chiamata a **`wait()`**, in un semaforo, porta semplicemente il semaforo ad essere messo in attesa nella coda, mentre in un monitor il thread che fa tale chiamata deve per definizione disporre di un lock, dunque in questo caso il thread deve anche rilasciare tale lock prima di finire in attesa;
- la chiamata a **`signal()`**, in un semaforo, incrementa il contatore associato ad esso, contatore che viene effettivamente "ricordato" dal semaforo anche se non vi è alcun thread in attesa in quel momento, e utilizzato poi all'arrivo di un nuovo thread, mentre in un monitor se non c'è alcun thread in attesa la chiamata viene sostanzialmente ignorata.

[10, slide 153 - 154 - 157 - 158]
___
## Problemi di sincronizzazione tipici

Spesso, quando si evince un bisogno di sincronizzazione per risolvere un determinato problema, tali problemi assumono delle **strutture più o meno ricorrenti**. Vediamone un paio.
##### Producer-Consumer

[10, slide 109 - 111 - 112 - 114]
___
##### Readers-Writers

Il problema **Readers-Writers** suppone la presenza di una certa **risorsa condivisa**, e di **due tipi di utenti**:
- i "**readers**", che non modificano mai la risorsa e accedono ad essa solo in lettura;
- i "**writers**", che accedono alla risorsa sia in lettura che in scrittura, andandola nel secondo caso a modificare.

Come possiamo sincronizzare le varie operazioni dei due tipi di utenti in modo da non avere comportamenti imprevisti? La soluzione più semplice sarebbe **porre un singolo [[SO1_06 - Sincronizzazione tra processi e tra thread#Locks|lock]] sulla risorsa**, in modo che non possano avvenire due operazioni nello stesso momento e dunque vengano prevenite letture di dati non validi o scritture contemporanee. Tuttavia, è facilmente intuibile che si tratta di una soluzione "pigra" e troppo restrittiva: infatti, seppur abbia senso sul fronte dei writers (è giusto volere una sola scrittura alla volta), non dovrebbero esserci problemi nel permettere che più readers accedano alla risorsa nello stesso momento, dato che nessuno di essi la va a modificare.

[10, slide 167 - 170/172]
___
## Deadlock

##### Cos'è un deadlock?

[11, slide 8/16 - 20 - 24]
___
##### Quando può avvenire un deadlock?

[11, slide 30]
___
##### Come prevenire o evitare un deadlock?

[11, slide 32/35 - 40 - 43 - 48 - 49 - 53 - 54 - 56/60 - 62 - 65/100]
___
##### Come individuare e risolvere un deadlock?

[11, slide 107/108 - 110 - 114 - 117/120 - 126 - 129 - 133]
___

