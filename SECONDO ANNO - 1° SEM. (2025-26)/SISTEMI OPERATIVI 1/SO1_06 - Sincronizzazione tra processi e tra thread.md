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


___

[09, slide 63 - 68 - 73 - 76 - 79]
