In Java, **`static`** e **`final`** sono due modificatori che non rientrano nella categoria dei [[03 - Modificatori d'accesso|modificatori d'accesso]], in quanto svolgono ruoli ben diversi. Vediamo, nel dettaglio, cosa implica l'utilizzo di queste keyword particolari.

## Static

La keyword **`static`** viene utilizzata nella definizione di un **membro di una [[02 - Classi|classe]] condiviso da tutte le istanze della stessa**; insomma, un campo o un metodo definito come `static` appartiene alla classe, e non all'istanza, e ne esiste una sola copia.

Si può definire come `static` pressoché qualsiasi membro di una classe, sia esso un **campo**, un **metodo**, o addirittura una **[[02 - Classi#Classi annidate|classe annidata]]** (ad esempio, il design pattern [[16 - Design pattern#Builder|Builder]] si basa proprio su una classe annidata statica). Nella definizione di un membro statico, la keyword `static` deve seguire il modificatore d'accesso di tale membro, ad esempio:

```
public static int count = 0;
```

In particolare, se dichiariamo un membro statico, esso può essere chiamato **indipendentemente da un'istanza della classe** a cui appartiene: ad esempio, per richiamare il metodo `pow()` della libreria `Math`, non servirà istanziare un oggetto di tipo `Math` e fare riferimento ad esso, ma basterà invocare il metodo nel modo seguente:

```
double d = Math.pow(2.0, 3.0);
```

Tuttavia, proprio non essendo dipendente da un'istanza, **un metodo statico non può accedere direttamente a membri non statici** della classe a cui appartiene.

Insomma, `static` è uno strumento potente in quanto permette una facile **condivisione di dati comuni** tra più istanze, un **accesso diretto** a certi membri di una classe senza bisogno di istanziarla, e di conseguenza una **riduzione dell'utilizzo di memoria** generale, soprattutto per metodi di utilità contenuti in classi come `Math`, `Collection`, `Arrays`, e così via. Un approccio del genere presenta però anche degli svantaggi, tra cui una **ridotta flessibilità e riutilizzabilità**, oltre a una maggiore **difficoltà di testing**.
___
## Final

La keyword **`final`** viene utilizzata nella definizione di un'**entità immutabile o non ridefinibile**. Si può definire come `final` pressoché qualsiasi entità, e si avranno risultati leggermente diversi in base ad essa; in particolare:
- dichiarare una **variabile** come `final` vuol dire che **il suo valore non potrà essere modificato dopo la prima assegnazione**;
- dichiarare un **metodo** come `final` vuol dire che **non potrà essere sovrascritto** (si intende, mediante un [[01 - Java e la OOP#Polimorfismo|override]]);
- dichiarare una **classe** come `final` vuol dire che **non potrà essere [[01 - Java e la OOP#Ereditarietà|ereditata]]** da nessun'altra classe.

Nella definizione di un'entità `final`, la keyword deve seguire il modificatore d'accesso di tale entità e, se presente, anche l'eventuale keyword `static`, ad esempio:

```
public final int i = 0;
public static final int PI = 3.14;
```

Come si è appena visto, è possibile utilizzare sia `static` che `final` insieme nella definizione di un membro di una classe: fare ciò porterà, nel caso di una variabile, alla creazione di una **costante condivisa tra tutte le istanze** (per convenzione, l'identificatore di una costante statica è scritto utilizzando solo maiuscole) e, nel caso di un metodo, alla creazione di un **metodo non-sovrascrivibile e indipendente da un'istanza**.

Insomma, `final` è uno strumento potente in quanto permette una **maggiore sicurezza e manutenibilità** del codice, nonché un eventuale **ottimizzazione delle prestazioni** (una variabile immutabile non potrà mai cambiare, e questa conoscenza aiuta il compilatore a gestirla in modo più efficiente). Un approccio del genere presenta però anche degli svantaggi, primo su tutti (come per `static`) una **ridotta flessibilità e riutilizzabilità**.
___