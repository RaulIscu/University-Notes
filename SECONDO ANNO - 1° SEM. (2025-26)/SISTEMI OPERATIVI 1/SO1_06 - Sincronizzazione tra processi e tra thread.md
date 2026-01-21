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

Per risolvere il primo problema, possiamo utilizzare una primitiva dell'OS che porta il thread chiamante a rilasciare la CPU, ossia **`yield()`**: basterà inserire una chiamata a `yield()` all'interno del corpo del ciclo contenuto in `acquire()`, in modo da rilasciare subito la CPU se il thread vuole eseguire una sezione critica e il lock è già occupato. 

[10, slide 64/68]
___

