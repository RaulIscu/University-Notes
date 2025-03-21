Essendo Java un linguaggio basato sulla [[Programmazione a oggetti|OOP]], l'incapsulamento risulta essere un meccanismo fondamentale nel suo funzionamento. Come spiegato in precedenza, l'incapsulamento permette, in parole povere, di collegare facilmente determinati dati con il codice che può manipolarli; è possibile, in particolare, avere maggiore controllo su questo aspetto mediante quello che viene definito "***access control***".

Questo meccanismo può risultare utile per prevenire un utilizzo errato del proprio programma, o per impedire l'accesso a dati o metodi progettati come "privati". La modalità principale in cui si controlla l'accesso a una parte del proprio programma è mediante l'utilizzo dei **modificatori d'accesso**, parole chiave che vengono inserite all'inizio della dichiarazione di tali parti. I principali modificatori d'accesso disponibili sono:
- **`public`**;
- **`private`**;
- **`protected`**.

Quando un membro di una classe viene dichiarato come **`public`**, esso permetterà l'accesso a qualsiasi altra parte del programma. Invece, quando un membro di una classe viene dichiarato come **`private`**, esso permetterà l'accesso solo ad altri membri della classe a cui appartiene.

Solitamente, conviene limitare l'accesso (utilizzando la parola chiave `private`) per i dati di una classe, in modo che essi siano accessibili esplicitamente solo mediante determinati metodi (che dovranno, ovviamente, essere `public`). A volte, inoltre, converrà rendere privati alcuni metodi di una classe.
___
Ci saranno dei casi in cui si vorrà definire un membro della classe che venga utilizzato indipendentemente da una specifica istanza della classe. Infatti, solitamente un membro viene invocato solo in relazione a una determinata istanza, ma **è possibile creare un membro che viene utilizzato prescindendo dalla specifica istanza di classe** che lo invoca. Per dichiarare un membro del genere, la parola chiave da utilizzare è **`static`**. Ad esempio, tale parola chiave viene utilizzata nella dichiarazione di un metodo *[[Il metodo main()|main]]*:

```
public static void main(String[] args) {
	bloccoDiCodice;
}
```

Dunque, se un membro è dichiarato come `static`, può essere invocato senza riferimento ad alcuna istanza di classe. Un membro dichiarato come `static` è, sostanzialmente, un membro globale; dunque, quando nuove istanze di classe sono dichiarate, non vengono create nuove copie del membro in questione, ma piuttosto ognuna delle istanze condivide lo stesso membro.

Per invocare un metodo `static`, indipendentemente da un determinato oggetto, basterà il seguente codice:

```
nomeDellaClasse.metodo();
```

dove *nomeDellaClasse* è, ovviamente, l'identificatore della classe in cui viene dichiarato tale metodo.
___
Un determinato membro di una classe, poi, può essere dichiarato come **`final`**: fare ciò rende il membro in questione non modificabile, dunque sostanzialmente una costante.

Per natura del modificatore `final`, è dunque necessario inizializzare la variabile nel momento in cui viene dichiarata. Il modo più comune per fare ciò è quello di inizializzare un determinato valore al momento della dichiarazione, nel seguente modo:

```
final int numberOne = 5;
```