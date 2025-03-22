Le **classi** costituiscono la base del funzionamento di Java: del resto, tutto il codice scritto in un *file* in formato Java va incapsulato in una classe.

Concettualmente, una classe costituisce una categoria di oggetti, una **generalizzazione** di un determinato oggetto, un modello per tale oggetto, che ne definisce gli attributi e i metodi, e dunque ogni cosa che lo definisce. Un concetto importante relativo a questo meccanismo è che, sostanzialmente, una classe definisce un nuovo **[[Tipi primitivi|tipo]]** di oggetto, che può essere usato per generarne varie **istanze**.
___
Per **dichiarare una classe**, si comincia con la parola chiave **`class`**, seguita dall'identificatore scelto per la classe in questione:

```
class nomeDellaClasse {

}
```

All'interno del [[Sintassi|corpo]] di una classe, si andranno a definire le sue varie componenti, tra cui:
- le **variabili di istanza**, ossia le variabili definite all'interno della classe e, dunque, che verranno utilizzate da essa (vengono chiamate "variabili di istanza" perché ogni istanza della classe, cioè ogni oggetto appartenente ad essa, conterrà la propria copia di queste variabili);
- i **metodi**, ossia le possibili azioni che possono essere operate sulle variabili di istanza della classe a cui appartengono.

Complessivamente, le variabili di istanza e i metodi di una classe vengono definiti i "**membri**" della classe. Di seguito, ampliamo l'esempio di classe precedente con gli adeguati membri:

```
class nomeDellaClasse {
	tipo variabileDiIstanza1;
	tipo variabileDiIstanza2;

	tipo nomeDelMetodo1(parametri) {
		corpoDelMetodo;
	} 

	tipo nomeDelMetodo2(parametri) {
		corpoDelMetodo;
	}
}
```

Si noti che, seppur sia consigliato, i metodi non devono necessariamente precisare la loro accessibilità (`public`, `private`, ecc. ecc.), né se siano `static` o meno, o altre caratteristiche. Inoltre, non è necessario che ogni classe abbia al suo interno un [[Il metodo main()|metodo main()]], in quanto questo è necessario solo nella classe che costituisce il punto d'inizio dell'avvio del programma.
___
Un *setup* come quello appena visto, tuttavia, prevede che un oggetto venga istanziato inizialmente con degli attributi "nulli", privi di qualsiasi valore; per inizializzare le sue variabili di istanza, si dovrebbero assegnare manualmente, separatamente, dei valori ad esse. Per evitare quest'operazione supplementare, è possibile definire all'interno del corpo della classe un "**costruttore**".

**Definire un costruttore** all'interno di una classe è un procedimento simile alla definizione di un metodo; il nome di tale "metodo" dovrà essere il nome della classe in cui esso viene definito, e nel suo corpo si stabiliranno i valori con cui le variabili di istanza di un oggetto creato col costruttore verranno inizializzate. Ad esempio:

```
class Box {
	double width;
	double length;
	double height;

	Box() {
		width = 10;
		length = 10;
		height = 10;
	}

	double volume() {
		return width * length * height;
	} 
}
```

In questo esempio, il costruttore (`Box()`) genererà un oggetto a cui verranno automaticamente associati una larghezza di 10, una lunghezza di 10 e un'altezza di 10. 

Tuttavia, si intuisce facilmente che un costruttore che inizializza sempre variabili contenenti il medesimo valore è tanto inutile quanto un'assenza di costruttori: per ovviare a questo problema, conviene sempre definire dei **costruttori parametrizzati**. Mediante quest'ultimi, è possibile specificare dei valori precisi per gli attributi di ogni oggetto, pur mantenendo il vantaggio di farlo in maniera compatta al momento della dichiarazione dell'oggetto stesso. L'esempio precedente, rendendo il costruttore un costruttore parametrizzato, diventa:

```
class Box {
	double width;
	double length;
	double height;

	Box(double w, double l, double h) {
		width = w;
		length = l;
		height = h;
	}

	double volume() {
		return width * length * height;
	}
}
```

In questo modo, se volessimo dichiarare tre istanze della classe *Box* con diverse variabili di istanza, potremmo scrivere il seguente codice:

```
Box box1 = new Box(10, 10, 10);
Box box2 = new Box(5, 20, 5);
Box box3 = new Box(10, 15, 20);
```
___
Per **dichiarare un'istanza di una classe**, si dovrà operare una particolare [[Variabili|dichiarazione di variabile]], che si divide in due passaggi:
1. innanzitutto, dichiarare una nuova variabile appartenente alla classe desiderata, analogamente a come si farebbe con uno qualsiasi dei [[Tipi primitivi|tipi primitivi]];
2. poi, per rendere effettivamente un oggetto questa variabile, assegnarle una nuova istanza di classe sfruttando la parola chiave **`new`**.

Concretamente, tale operazione prevede il seguente codice:

```
nomeDellaClasse nomeDellOggetto = new nomeDellaClasse();
```

Per accedere agli attributi e ai metodi di un oggetto appartenente a una determinata classe, si seguirà l'identificatore di tale oggetto con un punto (`.`) e con il nome dell'attributo a cui si vuole accedere, o del metodo che si vuole operare, come nel seguente esempio.
___
È possibile definire una classe all'interno di un'altra classe, andando a creare una **classe annidata**.

Naturalmente, se una classe B viene definita all'interno di una classe A, la classe B non potrà esistere indipendentemente dalla classe A. Inoltre, **una classe annidata ha accesso a tutti i membri della classe che la contiene**, inclusi quelli dichiarati come [[Public, private, static, final|privati]]; tuttavia, **la classe che racchiude quelle annidate** (per intenderci, la classe A) **non ha accesso ai loro membri privati**. Una classe annidata viene considerata come un membro della classe all'interno della quale è definita.

Una classe annidata può essere di due tipi, **statica** o **non-statica**. Una classe annidata statica, definita dunque sfruttando la parola chiave `static`, non potrà accedere direttamente ai membri non-statici della classe che la racchiude; per questo motivo, in realtà, le classi annidate statiche vengono usate di rado.

Molto più comuni sono invece le **classi annidate non-statiche**, denominate semplicemente "***inner classes***", o "classi interne". Esse, essendo non-statiche, hanno accesso a tutti i membri delle classi che le racchiudono, e potranno accedere ad essi direttamente. **Dichiarare una *inner class*** è molto semplice e intuitivo, come si può vedere nel seguente esempio:

```
class Outer {
	int outer_x = 100;

	void test() {
		Inner inner = new Inner();
		inner.display();
	}

	class Inner {
		void display() {
			System.out.println("display: outer_x = " + outer_x);
		}
	}
}
```

Seppur, nell'esempio, la *inner class* venga dichiarata come un membro di una determinata classe esterna, è perfettamente possibile dichiarare una *inner class* all'interno di qualsiasi blocco di codice, tenendo comunque a mente dello *scope* che essa avrà.