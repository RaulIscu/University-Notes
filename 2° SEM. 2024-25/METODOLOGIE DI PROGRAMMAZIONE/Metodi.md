Come accennato quando si è parlato delle [[Classi|classi]], i **metodi** di una classe sono le possibili azioni che possono essere compiute sulle variabili d'istanza di tale classe. Genericamente, per dichiarare un metodo, è necessario il seguente codice:

```
tipo nomeDelMetodo(parametri) {
	corpoDelMetodo
}
```
___
In Java, è possibile definire, all'interno di una classe, più di un metodo con lo stesso identificatore, finché vengano dichiarati diversi parametri per ciascuno di questi metodi. 

Questo particolare procedimento viene definito "***method overloading***", ed è una delle manifestazioni più palesi del principio di [[Programmazione a oggetti|polimorfismo]] all'interno di Java. Infatti, invocando un metodo definito in questo modo, che condivide quindi il suo identificatore con altri metodi, **sarà il tipo e il numero dei parametri presi in *input* dal metodo a guidare l'esecuzione verso una sua determinata versione** piuttosto che un'altra. È per questo che risulta fondamentale, se si vuole operare un *method overloading*, differenziare i parametri dei metodi in questione.

Vediamo, di seguito, un esempio concreto:

```
class OverloadDemo {
	void test() {
		System.out.println("No parameters");
	}

	void test(int a) {
		System.out.println("a: " + a);
	}

	void test(int a, int b) {
		System.out.println("a: " + a + ", b: " + b);
	}

	void test(double a) {
		System.out.println("double a: " + a);
	}
}
```

In questo blocco di codice, è stato effettuato un *method overloading* su 4 metodi: la prima versione non prende in *input* alcun parametro; la seconda versione prende in *input* un intero *a*; la terza versione prende in *input* due interi *a* e *b*; infine, la quarta versione prende in *input* un `double` *a*. Dunque, chiamando generalmente il metodo `test`, sarà il tipo e il numero degli *input* dati come argomenti del metodo a decretare quale di queste versioni verrà effettivamente utilizzata.

Supponiamo di non avere la prima delle 4 versioni del metodo `test`, ovvero quella che prende in *input* un singolo intero. A questo punto, se invocassimo il metodo dandogli in *input* un intero, tecnicamente non dovremmo poter accedere ad alcuna delle versioni rimaste del metodo, in quanto nessuno corrisponde in termini di parametri. In questo caso, tuttavia, Java procede a trasformare l'intero in `double` in maniera automatica, in modo da poter chiamare la quarta versione del metodo. Infatti, se il tipo del parametro dato in *input* risulta essere diverso ma compatibile con quello del parametro di una delle versioni del metodo effettivamente dichiarate, **esso verrà automaticamente convertito** in modo da poter risolvere l'invocazione del metodo.

È possibile effettuare un *method overloading* anche con i **costruttori**. Infatti, si può dichiarare un costruttore per un determinato oggetto che prenda in *input* i vari attributi da inizializzare, ma eventualmente anche un costruttore che non prenda nessun parametro in *input* (con il quale, dunque, non verrà inizializzato nessun attributo), o magari un costruttore che prende solo uno di tali attributi come parametro.
___
Finora, come parametri di un metodo sono stati sempre inseriti dati appartenenti a tipi come `int`, `double`, `boolean`, `String`, ecc. ecc.; tuttavia, **è possibile inserire come parametri di un metodo anche oggetti**.

Una delle situazioni in cui si ricorre più comunemente a questa pratica è nell'utilizzo dei costruttori: infatti, spesso si vuole istanziare un oggetto che (almeno inizialmente) risulta essere una copia di un altro oggetto preesistente, e per fare ciò comodamente è possibile definire un costruttore che prende in *input*, come parametro, un oggetto della classe a cui appartiene. Ad esempio:

```
class Box {
	double height;
	double width;
	double depth;

	Box(double h, double w, double d) {
		height = h;
		width = w;
		depth = d;
	}

	Box(Box ob) {
		height = ob.height;
		width = ob.width;
		depth = ob.depth;
	}
}
```
___
[METODI CON NUMERO VARIABILE DI ARGOMENTI: chapter 7 varargs]