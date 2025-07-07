## Cos'è un interfaccia?

In Java, possiamo definire un'**interfaccia** come una "classe" particolare, simile per certi versi a una [[Classi#Classi astratte|classe astratta]], che può contenere solo:
- **metodi astratti**;
- **metodi statici**;
- **metodi di default**;
- **costanti**.

Un'interfaccia non viene utilizzata per implementare direttamente un comportamento, ma piuttosto per dichiararlo e definirlo. In sostanza, quello che fa un'interfaccia è **definire un contratto** per tutte le classi che la implementano, in modo tale che **qualsiasi classe implementi una certa interfaccia è obbligata a fornire un'implementazione per i suoi metodi**. Si tratta di uno strumento utile per consentire a **più classi** di implementare un insieme di **metodi comuni**, standardizzando l'interazione tra determinati oggetti.

Qualsiasi metodo dichiarato in un'interfaccia, a meno di altre direttive, è implicitamente dichiarato come **`public abstract`**, e qualsiasi campo dichiarato in un'interfaccia, a meno di altre direttive, è implicitamente dichiarato come **`public static final`**. Va da sé, dunque, che non è possibile fornire alcun dettaglio implementativo per nessun metodo definito in un'interfaccia, a meno che esso non venga definito come `static` o come `default`.

Un'interfaccia viene definita in modo simile a una classe, con la differenza dell'utilizzo della keyword **`interface`** piuttosto che `class`. Ad esempio, supponiamo di voler definire un'interfaccia `Animale`:

```
public interface Animale {
	void emettiVerso();
}
```

Ora, potremmo definire delle classi `Gatto` e `Cane`, che essendo animali vanno a implementare l'interfaccia `Animale`, fornendo necessariamente un'implementazione particolare del metodo `emettiVerso()`. In Java, per specificare che una classe implementa un'interfaccia, si utilizza la keyword **`implements`** nel modo seguente:

```
public class Gatto implements Animale {
	public void emettiVerso() {
		System.out.println("Miao!");
	}
}

public class Cane implements Animale {
	public void emettiVerso() {
		System.out.println("Bau!");
	}
}
```

A questo punto, sarà possibile utilizzare le due classi `Gatto` e `Cane` come due classi distinte a cui è permesso lo stesso comportamento, ma che concretamente fanno cose diverse. Ad esempio, eseguendo il seguente codice:

```
Animale a1 = new Gatto();
Animale a2 = new Cane();

a1.emettiVerso();
a2.emettiVerso();
```

verrà stampato a terminale prima `Miao!` e poi `Bau!`.

Le interfacce offrono vari vantaggi, tra cui una **maggiore separazione tra l'astrazione di un tipo di oggetto e la sua implementazione**, un favoreggiamento del **polimorfismo** (oggetti di classi diverse, se implementano la stessa interfaccia, potranno essere utilizzati in maniera più uniforme), e un incremento nella **modularità** e nella **riutilizzabilità** del codice.
___
## Interfacce vs. classi astratte

A primo impatto, come suggerito anche nell'introduzione del [[Interfacce#Cos'è un interfaccia?|paragrafo precedente]], le interfacce sembrano essere particolarmente simili a delle [[Classi#Classi astratte|classi astratte]], e viene naturale chiedersi perché si dovrebbe preferire l'una o l'altra.

Innanzitutto, la caratteristica forse più importante che differenzia queste due componenti ha a che fare con il principio dell'**[[Java e la OOP#Ereditarietà|ereditarietà]]**. In Java, infatti, **non è prevista l'ereditarietà multipla**, il che vuol dire che una classe non può ereditare da più di una superclasse (sia essa astratta o meno); tuttavia, **una classe può implementare più di un'interfaccia**, e addirittura è possibile che una classe implementi più interfacce e al tempo stesso erediti da una superclasse. Quindi, da questo punto di vista, se si vuole raggiungere un "maggior grado di ereditarietà", il più delle volte converrà l'utilizzo di interfacce piuttosto che di classi astratte.

Passando a dettagli più tecnici:
- un'interfaccia può presentare solo metodi astratti, o concreti solo se definiti come `static` o come `default`; invece, una classe astratta può presentare metodi astratti e concreti, senza alcuna particolare limitazione;
- similmente, un'interfaccia può avere come campi solo delle costanti, definite dunque come `public static final`, mentre una classe astratta può sostanzialmente disporre di qualsiasi tipo di campo si desideri;
- non è possibile definire un costruttore all'interno di un'interfaccia, mentre si può fare nel contesto di una classe astratta.

Di fatto, le differenze principali stanno nello **scopo** e nell'**utilizzo tipico** di queste due componenti. Se si vuole definire solamente un contratto, un comportamento generico che alcuni tipi di oggetti dovranno rispettare, e si prevede la possibilità che un tipo vada a "firmare" più di un contratto, allora probabilmente converrà utilizzare delle interfacce. Se, invece, si vuole definire piuttosto una base di classe, che possa presentare anche un'implementazione parziale del proprio comportamento, e si prevede una struttura più gerarchica in senso classico, allora si potrebbero utilizzare delle classi astratte.
___
## Alcune interfacce comuni

#### Collection

L'interfaccia **`Collection<E>`** è una delle interfacce più importanti, se non la più importante, del [[Strutture dati#Java Collection Framework|Java Collection Framework]].

Si trova nel package **`java.util`**, e rappresenta la principale interfaccia implementata dalle più comuni **[[Strutture dati|strutture dati]]** del framework, che in particolare vanno singolarmente a implementare delle sotto-interfacce di `Collection<E>`, come `List<E>`, `Set<E>` o `Queue<E>` (l'unica eccezione tra le strutture dati più utilizzate è `Map<K, V>`).

Il contratto definito dall'interfaccia va a teorizzare un **oggetto che contiene un gruppo di elementi** (a seconda della sottoclasse, sono permessi o meno duplicati), e fornisce una lista di metodi di base per aggiungere, rimuovere, visualizzare e iterare sugli elementi. In particolare, i **metodi principali** definiti all'interno di `Collection<E>` sono:
- **`boolean add(E e)`**;
- **`boolean addAll(Collection<? extends E> c)`**;
- **`void clear()`**;
- **`boolean contains(Object o)`**;
- **`boolean containsAll(Collection<?> c)`**;
- **`boolean isEmpty()`**;
- **`Iterator<E> iterator()`**;
- **`boolean remove(Object o)`**;
- **`boolean removeAll(Collection<?> c)`**;
- **`boolean retainAll(Collection<?> c)`**;
- **`int size()`**;
- **`E[] toArray()`**.
___
#### Stream


___
#### Iterable


___
#### Iterator



___
## Interfacce funzionali

In poche parole, un'**interfaccia funzionale** è un tipo particolare di [[Interfacce#Cos'è un interfaccia?|interfaccia]] che si caratterizza per **definire un solo metodo astratto** al suo interno. Per indicare che un'interfaccia è funzionale al momento della sua definizione, si può anticipare il corpo dell'interfaccia con la seguente annotazione facoltativa:

```
@FunctionalInterface
```

Si tratta di uno strumento più potente di quello che può sembrare, soprattutto per la possibilità del loro **utilizzo insieme a [[Espressioni lambda e riferimenti a metodi#Espressioni lambda|espressioni lambda]] e [[Espressioni lambda e riferimenti a metodi#Riferimenti a metodi|riferimenti a metodi]]**. Infatti, essendo dotate di un solo metodo astratto, è possibile istanziare delle interfacce funzionali con compiti personalizzati in maniera comoda e veloce, proprio sfruttando i due strumenti appena citati. Ad esempio, supponiamo di definire la seguente interfaccia funzionale:

```
@FunctionalInterface
public interface Calcolatore {
	int calcola(int a, int b);
}
```

Possiamo istanziare vari oggetti che implementano `Calcolatore` in maniera diversa sfruttando pochissimo codice e tempo, con delle espressioni lambda:

```
Calcolatore somma = (a, b) -> a + b;
Calcolatore prodotto = (a, b) -> a * b;
```

oppure con dei riferimenti a metodi che siano compatibili:

```
public class Matematica {
	public static int prodotto(int a, int b) {
		return a * b;
	}
}

Calcolatore prodotto = Matematica::prodotto;
```

Sotto questo punto di vista, possiamo vedere l'interfaccia funzionale come una "tipizzazione" dell'espressione lambda, rendendola riutilizzabile e definendone il contratto in maniera più precisa.
___
## Alcune interfacce funzionali comuni

#### Comparable


___
#### Comparator


___
#### Predicate e BiPredicate


___
#### Function e BiFunction


___
#### Consumer e BiConsumer


___
#### Supplier


___