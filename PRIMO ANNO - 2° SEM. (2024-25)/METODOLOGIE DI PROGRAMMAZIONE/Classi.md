## Cos'è una classe?

Nella [[Java e la OOP#Cos'è la programmazione a oggetti?|programmazione a oggetti]], la **classe** è uno dei componenti più importanti di un qualsiasi programma, se non il componente per eccellenza. In Java, tutto il codice che viene scritto è contenuto in una classe, e lo scambio di informazioni e messaggi tra classi diverse è alla base del funzionamento di qualsiasi applicazione scritta in Java. Ma cos'è, a livello concreto, una classe?

Una **classe** è, sostanzialmente, del codice sorgente che descrive un particolare tipo di oggetti, il suo comportamento e le sue caratteristiche. Si tratta di un **prototipo astratto** per quel tipo di oggetto, che va a definire di fatto l'intera struttura dello stesso.

Per **definire una classe**, si comincia con la parola chiave **`class`**, seguita dall'identificatore scelto per la classe in questione:

```
class NomeDellaClasse {
	// CORPO DELLA CLASSE
}
```

Per essere più precisi, tuttavia, è opportuno definire una classe specificando prima di tutto anche il [[Modificatori d'accesso|modificatore d'accesso]] desiderato. Ad esempio, la definizione opportuna per una classe pubblica è:

```
public class NomeDellaClasse {
	// CORPO DELLA CLASSE
}
```

È importante ricordare alcune convenzioni:
- ogni singola classe deve essere scritta in un ***file* separato** (fatta eccezione per le [[Classi#Classi annidate|classi annidate]]), che va nominato con lo stesso identico nome assegnato alla classe, e che deve disporre dell'estensione "**.java**";
- i nomi assegnati come identificatori delle classi hanno sempre l'**iniziale maiuscola**, e, come per gli altri casi, ogni parola che compone tale identificatore dovrà disporre anch'essa dell'iniziale maiuscola.
___
## Variabili d'istanza, metodi e costruttori

All'interno del corpo di una classe, si andranno a definire le sue varie componenti (i cosiddetti "**membri**" della classe), che solitamente si dividono in:
- **campi** della classe, ossia le variabili definite al suo interno che, perciò, verranno utilizzate da essa (in particolare, i campi possono essere definiti come `static`, e quindi come indipendenti da una particolare istanza della classe; in caso contrario, sono più propriamente detti "**variabili d'istanza**", in quanto ogni istanza della classe conterrà la propria copia di tali campi);
- **metodi** della classe, ossia le possibili azioni che possono essere eseguite dalle istanze della classe in cui vengono definiti.

Convenzionalmente, la struttura generale del corpo di una classe prevede che prima vengano dichiarati tutti i suoi campi, e in seguito tutti i suoi metodi. Seppur sia fortemente consigliato, **non è obbligatorio precisare il modificatore di accesso dei metodi** della classe, né se essi siano `static` o meno. Ciò che è, tuttavia, necessario, è il **tipo dei campi** e il **tipo di ritorno dei metodi** (se non viene ritornato nulla, si utilizza la keyword **`void`**).

Inoltre, non è necessario che ogni classe abbia al suo interno un **metodo `main()`**, soprattutto nel contesto di un programma complesso composto da più classi: infatti, esso **deve essere presente solamente nella classe da cui viene avviata l'esecuzione** del programma in questione.

Di base, a meno di circostanze particolari o di utilizzi specifici, si cerca di favorire il più possibile l'**[[Java e la OOP#Incapsulamento|incapsulamento]]** nella definizione dei membri di una classe, soprattutto mediante le seguenti convenzioni generali:
- i **campi** di una classe vengono preferibilmente definiti come **privati**;
- i **metodi** di una classe vengono preferibilmente definiti come **privati** se non vengono utilizzati al di fuori della propria classe, altrimenti come **pubblici** o **protetti** a seconda della circostanza.

È naturale chiedersi, perciò, come è possibile visualizzare e manipolare i campi di una classe. Per permettere ciò, spesso tra i metodi di una classe sono inclusi i cosiddetti metodi "**getter**" e "**setter**", utilizzati rispettivamente per restituire e per modificare il valore di un campo della classe. Per convenzione, un metodo getter ha come identificatore "**get**" seguito dall'identificatore del campo a cui è legato; ad esempio, avendo un campo `int counter`, il metodo getter associato è il seguente:

```
public int getCounter() {
	return this.counter;
}
```

Pressoché la stessa regola vale per i metodi setter, che hanno come identificatore "**set**" seguito dall'identificatore del campo a cui è legato; ad esempio, per lo stesso campo dell'esempio precedente, il metodo setter associato è il seguente:

```
public void setCounter(int newCounter) {
	this.counter = newCounter;
}
```

A questo punto, abbiamo parlato di come definire campi e metodi di una classe, come gestire la loro accessibilità e come manipolarli. Sembra che si siano analizzate tutte le componenti essenziali per una classe, tuttavia rimane un punto da specificare: **come avviene, nel dettaglio, la creazione di una nuova istanza della classe?**

Infatti, attualmente, non abbiamo modo di definire delle istruzioni particolari su come costruire un nuovo oggetto, e una sua costruzione avverrebbe con **attributi "nulli"**, privi di valore o a cui vengono automaticamente assegnati valori di default (`0.0f` per campi di tipo `float`, `0` per campi di tipo `int`, `false` per campi di tipo `boolean`, ecc. ecc.); in questo contesto, per assegnare dei valori particolari alle varie variabili d'istanza, si dovrebbero utilizzare manualmente i metodi setter relativi ad ognuna di esse.

Per evitare quest'operazione supplementare, è possibile definire all'interno del corpo della classe un "**costruttore**", ossia un metodo particolare destinato esclusivamente alla **costruzione di nuove istanze della classe** in cui si trova. Si tratta di un metodo tipicamente **pubblico**, a meno di astrazioni particolari (come l'applicazione di certi [[Design pattern|design pattern]]), che deve necessariamente avere lo **stesso identificatore della classe** a cui appartiene e che tipicamente viene inserito nel corpo della stessa come il primo dei suoi metodi. Nel corpo del costruttore, si andranno a stabilire i valori da assegnare immediatamente alle variabili d'istanza di un oggetto. Ad esempio, supponendo di voler definire un costruttore per la classe `Box`, che presenta i campi `width`, `length` e `height`, un possibile costruttore potrebbe essere:

```
public Box() {
	width = 10;
	length = 10;
	height = 10;
}
```

Così facendo, qualsiasi oggetto di tipo `Box` istanziato tramite il costruttore avrà le variabili d'istanza inizializzate tutte a $10$. Tuttavia, si intuisce facilmente che anche un approccio del genere è abbastanza limitato: infatti, inizializzare sempre variabili d'istanza con i medesimi valori è quasi inutile quanto non inizializzarli affatto. Per ovviare a questo problema, conviene sempre definire dei "**costruttori parametrizzati**", ossia dei costruttori che accettano dei parametri in input, parametri che rappresenteranno i valori da assegnare alle variabili d'istanza dell'oggetto costruito. Ad esempio, andando a modificare il costruttore dell'esempio precedente, otteniamo:

```
public Box(int w, int l, int h) {
	width = w;
	length = l;
	height = h;
}
```

In questo modo, sarà facile costruire un certo numero di oggetti con dei valori personalizzati. Infine, è possibile anche sfruttare dell'**[[Java e la OOP#Polimorfismo|overloading]]** e definire più costruttori per una stessa classe, ciascuno con un funzionamento e dei parametri diversi, in modo da aumentare ancora di più la flessibilità e l'accessibilità del codice.
___
## Classi e oggetti

Nel paragrafo "[[Classi#Cos'è una classe?|Cos'è una classe?]]", si è specificato come la classe rappresenti un "prototipo", un modello astratto per un particolare tipo di oggetto. Ma cos'è propriamente un oggetto?

Un **oggetto** non è altro che una particolare **istanza di una classe**, un "esemplare" reale di quella classe. Durante l'esecuzione di un programma, possono essere create una o più istanze di una determinata classe, ossia uno o più oggetti di quel tipo, e ognuno rappresenterà un diverso esemplare appartenente ad esso. 

Per comprendere meglio questo concetto, vediamo le principali **differenze tra classi e oggetti**:
- una classe viene definita a priori manualmente dal programmatore nel codice sorgente di un programma, mentre un oggetto è un'entità generata "**a runtime**", ossia durante l'esecuzione del programma stesso, tramite l'esecuzione di un certo metodo;
- una classe specifica, a livello generale, la struttura che dovrebbe possedere un certo oggetto, definendone i campi e i metodi, mentre un oggetto possiede dei valori specifici e variabili per ciascuno di quei campi, e si comporta nel modo prescritto dalla classe seguendo i metodi che sono stati definiti per esso.

Il connubio tra classi e oggetti è ciò che sta alla base di qualsiasi azione si voglia svolgere tramite codice in Java.

Per **dichiarare un'istanza di una classe**, e dunque costruire un nuovo oggetto a partire da tale classe, si dovrà operare una particolare dichiarazione di variabile, che si divide in due passaggi:
1. dichiarare una nuova variabile appartenente alla classe desiderata, analogamente a come si farebbe con uno qualsiasi dei [[Tipi primitivi|tipi primitivi]];
2. assegnarle una nuova istanza della classe, sfruttando la parola chiave **`new`** e richiamandone il **[[Classi#Variabili d'istanza, metodi e costruttori|costruttore]]**.

Concretamente, tale operazione assume la seguente forma:

```
NomeDellaClasse identificatoreDell'Oggetto = new nomeDellaClasse();
```

Per accedere agli attributi e ai metodi di un oggetto appartenente a una determinata classe, si seguirà l'identificatore di tale oggetto con un punto (**`.`**) e con il nome dell'attributo o del metodo a cui si vuole accedere.
___
## Classi astratte


___
## Classi annidate

Quando una classe è detta "**annidata**", vuol dire che viene **definita all'interno del corpo di un'altra classe**. Tendenzialmente, le classi annidate vengono considerate veri e propri **membri delle classi che le racchiudono**, e si dividono in due categorie principali:
- le ***inner classes***, o "classi interne", ossia classi semplicemente definite all'interno di altre, che sono per natura associate a un'istanza della classe esterna che le racchiude;
- le ***static nested classes***, o "classi annidate statiche", ossia classi statiche definite all'interno di altre, il che le rende indipendenti dalle istanze della classe esterna.

Approfondiamo prima di tutto le **classi interne**. In questo caso, **la classe interna ha accesso a tutti i membri della classe che la contiene**, qualsiasi sia il loro [[Modificatori d'accesso|modificatore d'accesso]]; allo stesso tempo, però, **la classe esterna che la racchiude non ha accesso ai membri privati della classe interna**. Vediamo, a livello di sintassi, come **dichiarare una classe interna**:

```
public class Outer {

	...

	public class Inner {

		...
	}
}
```

Come possiamo notare, a livello di sintassi una classe interna viene dichiarata in maniera perfettamente analoga a una classe qualsiasi, e lo stesso vale per il suo corpo; ovviamente, l'unica differenza è che la definizione non avviene al *top-level*, ma all'interno del corpo di un'altra classe.

Come abbiamo detto, una classe interna è **dipendente da un'istanza della classe esterna**. Infatti, se volessimo istanziare e utilizzare la classe interna, dovremmo scrivere del codice del genere:

```
Outer out = new Outer();
Outer.Inner in = out.new Inner();
...
```

Le **classi annidate statiche**, invece, assumono un comportamento diverso. In questo caso, **la classe annidata statica ha accesso solo ai membri statici della classe esterna**, essendo per natura **indipendente da qualsiasi istanza della classe esterna**. Al contrario, **la classe esterna ha accesso a tutti i membri della classe annidata statica che racchiude**, anche a quelli privati. Vediamo, a livello di sintassi, come **dichiarare una classe annidata statica**:

```
public class Outer {

	...

	public static class Inner {

		...
	}
}
```

Essendo, come abbiamo già detto, indipendenti da un'istanza della classe esterna, per istanziare una classe annidata statica basterà del codice del genere:

```
Outer.Inner in = new Outer.Inner();
```

Le classi annidate, siano esse *inner classes* o *static nested classes*, vengono usate per **raggruppare classi correlate** a livello logico, per **incapsulare classi non necessarie all'esterno** di quella che le racchiude, o anche per **creare istanze temporanee e personalizzate** di certe classi o interfacce, in particolare tramite le [[Classi#Classi anonime|classi anonime]], che verranno approfondite nel prossimo paragrafo.
___
## Classi anonime

Una **classe anonima** è, tecnicamente, un particolare tipo di [[Classi#Classi annidate|classe annidata]], in quanto è a tutti gli effetti una classe definita all'interno di un'altra. La sua particolarità, tuttavia, è quella di **non avere un nome specifico**, e di essere **definita e istanziata "al volo"**.

Tipicamente, le classi anonime vengono utilizzate per scrivere codice conciso in situazioni in cui è necessaria un'**implementazione personalizzata e temporanea** di un'interfaccia (come `ActionListener`) o di una classe astratta. Possono essere, inoltre, utili anche nel contesto di **override temporanei** di certi metodi.

Vediamo un esempio per comprendere meglio la sintassi relativo a questa componente. Supponiamo di avere un `JButton`, e di volergli assegnare una determinata funzionalità nel momento in cui viene cliccato. Per fare ciò, si dovrà istanziare l'interfaccia **`ActionListener`** mediante una classe anonima, associando tale istanza al pulsante in questione e definendo un'implementazione personalizzata del metodo **`actionPerformed(ActionEvent e)`**, nel modo seguente:

```
JButton pulsante = new JButton();

pulsante.addActionListener(new ActionListener() {
	public void actionPerformed(ActionEvent e) {
		// ISTRUZIONI DA ESEGUIRE
	}
});
```

Si tratta, concretamente, di uno strumento abbastanza situazionale, soprattutto per la sua **impossibilità di riutilizzo**, per l'**assenza di costruttori** e per la **minore leggibilità in situazioni complesse**. Ciononostante, in varie circostanze permette di ottimizzare la creazione di oggetti e di gestire in modo rapido varie componenti del programma che si sta progettando.
___