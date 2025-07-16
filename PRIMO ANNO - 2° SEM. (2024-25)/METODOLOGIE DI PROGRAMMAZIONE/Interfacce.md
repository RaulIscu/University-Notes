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

L'interfaccia **`Stream<T>`** è stata introdotta in Java 8, si trova nel package **`java.util.stream`** e rappresenta, sostanzialmente, un **flusso astratto di elementi** di un certo tipo, su cui possono essere eseguite varie **operazioni funzionali in stile dichiarativo**.

Un oggetto `Stream` può essere **creato** in vari modi, tra cui:
- a partire da una struttura dati che implementa l'interfaccia `Collection`, utilizzando **`Collection.stream()`**;
- a partire da un elenco di dati o elementi, utilizzando **`Stream.of(...)`**;
- a partire da un array, utilizzando **`Arrays.stream(array)`**;
- a partire dalle righe di un file, utilizzando **`Files.lines(path)`**.

Un oggetto `Stream` viene sempre generato a partire da una fonte di dati separata (ad esempio una collezione, un [[Strutture dati#Array|array]] o un file), ma non costituisce di per sé una fonte di dati; insomma, uno Stream non memorizza nulla, ma permette di definire e applicare efficientemente **una pipeline di operazioni** su dati già esistenti.

Uno Stream particolare **può essere consumato una sola volta**, può essere eseguito in maniera **sequenziale** o **parallela** con altri Stream, e **non va mai a modificare la sorgente originale**. Le operazioni che si possono compiere su di esso si dividono principalmente in due categorie: **intermedie** e **terminali**. La pipeline di operazioni di uno Stream, tendenzialmente, è costituita da un certo numero di operazioni intermedie in sequenza, che restituiscono ognuna un nuovo Stream diverso da quello di partenza, seguite da un'operazione terminale che lo esaurisce.

Per poter utilizzare in maniera ottimale gli oggetti che implementano l'interfaccia `Stream<T>`, analizziamo i principali metodi definiti al suo interno, e quindi le principali **operazioni** che possono essere eseguite su di essi. Le principali **operazioni intermedie** sono:
- **`distinct()`**, che permette di scartare qualsiasi elemento duplicato presente nello stream;
- **`filter(Predicate<T> p)`**, che permette di filtrare gli elementi dello stream in base alla condizione booleana definita da `p` (se `p` restituisce `true` per un certo elemento, esso viene conservato, altrimenti viene scartato);
- **`flatMap(Function<T, R> f)`**, che permette di "appiattire" stream ottenuti a partire da strutture dati annidate, trasformando gli elementi in base a `f`;
- **`limit(int n)`**, che permette di ottenere uno stream contenente solo i primi `n` elementi dello stream di partenza;
- **`map(Function<T, R> f)`**, che permette di trasformare gli elementi dello stream (solitamente, con qualche conversione di tipo) in base alla funzione definita da `f`;
- **`skip(int n)`**, che permette di ottenere uno stream contenente tutti gli elementi seguenti ai primi `n` dello stream di partenza;
- **`sorted()`**, che permette di riordinare gli elementi dello stream in base all'implementazione di `Comparable` relativa al tipo degli oggetti contenuti al suo interno;
- **`sorted(Comparator c)`**, che permette di riordinare gli elementi dello stream in base al comparatore `c`.

Per quanto riguarda, invece, le principali **operazioni terminali**, esse sono:
- **`allMatch(Predicate<T> p)`**, che restituisce `true` se tutti gli elementi dello stream rispettano la condizione booleana definita da `p`, e `false` altrimenti;
- **`anyMatch(Predicate<T> p)`**, che restituisce `true` se almeno uno degli elementi dello stream rispetta la condizione booleana definita da `p`, e `false` altrimenti;
- **`collect(Collector)`**, che permette di raccogliere gli elementi dello stream in una determinata struttura dati in base al `Collector` preso in input;
- **`count()`**, che restituisce il numero di elementi presenti nello stream;
- **`findAny()`**, che restituisce un elemento qualsiasi dello stream;
- **`findFirst()`**, che restituisce il primo elemento dello stream;
- **`forEach(Consumer<T> c)`**, che permette di eseguire l'azione definita da `c` su ogni elemento dello stream;
- **`noneMatch(Predicate<T> p)`**, che restituisce `true` se nessuno degli elementi dello stream rispetta la condizione booleana definita da `p`, e `false` altrimenti;
- **`toArray()`**, che restituisce un array contenente tutti gli elementi dello stream.

Si tratta di uno strumento molto potente soprattutto per la **manipolazione di grandi quantità di dati**, e la sua **struttura** **dichiarativa**, **leggibile** e **concisa** lo rendono anche particolarmente comodo da utilizzare. Inoltre, per natura si integra molto facilmente con **[[Espressioni lambda e riferimenti a metodi#Espressioni lambda|espressioni lambda]]**, e il supporto al **parallelismo** consente eventualmente di lavorare su più stream in contemporanea velocemente.
___
#### Iterable

L'interfaccia **`Iterable<T>`** è un'interfaccia importantissima e relativamente di base che si trova nel package **`java.lang`**. Essa rappresenta una **generica collezione di elementi iterabili**, ossia una collezione i cui elementi possono essere ottenuti uno ad uno, tipicamente tramite un **[[Istruzioni di controllo#Il *for loop*|for-each loop]]**, tant'è che l'implementazione dell'interfaccia `Iterable<T>` è concretamente necessaria per poter utilizzare un qualsiasi oggetto in un loop del genere.

Si tratta, quindi, di un'interfaccia importantissima, e pressoché essenziale per qualsiasi [[Strutture dati|struttura dati]] si voglia definire. Infatti, anche l'interfaccia **`Collection`** rappresenta, di fatto, una sottoclasse di `Iterable`, e quindi qualsiasi classe implementi la prima andrà automaticamente ad implementare anche la seconda.

L'interfaccia `Iterable` definisce **un solo metodo astratto**, ossia **`iterator()`**, che restituisce un oggetto di tipo `Iterator` responsabile dello scorrimento degli elementi della collezione, e a partire da Java 8 anche alcuni metodi di default, ossia:
- **`forEach(Consumer<? super T> c)`**, che funziona in maniera analoga al metodo omonimo definito in `Stream`, e dunque va ad eseguire l'azione definita da `c` su ogni elemento della collezione;
- **`spliterator()`**, che restituisce un oggetto di tipo `Spliterator` relativo alla collezione, utile per delle elaborazioni parallele.

Notiamo, però, un'incongruenza: **`Iterable<T>` definisce al suo interno un solo metodo astratto, eppure non è considerata un'interfaccia funzionale**. Perché?

Seppur venga rispettata la definizione formale di [[Interfacce#Interfacce funzionali|interfaccia funzionale]], `Iterable` funziona in maniera completamente diversa da una qualsiasi delle interfacce appartenenti a tale categoria. Quest'ultime, infatti, rappresentano in particolare un **comportamento** o una **funzione** ben precisa, che nella maggior parte dei casi presenta un input, un output, o entrambi. Ciò non può assolutamente essere affermato per `Iterable`, che rappresenta la funzionalità di un contenitore iterabile di dati. Oltre a ciò, un altro fattore che favorisce notevolmente la sua separazione dalle interfacce funzionali è la sua **incompatibilità con le espressioni lambda**, che sono invece il fulcro del funzionamento di interfacce come `Predicate`, `Function` e molte altre.
___
#### Iterator


___
#### Comparable


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

#### Comparator

L'interfaccia funzionale **`Comparator<T>`** rappresenta un **criterio di ordinamento** tra oggetti di tipo generico `T`. Il suo unico **metodo astratto** è:

```
int compare(T o1, T o2);
```

che, per convenzione, deve ritornare un numero negativo se, secondo il criterio di ordinamento deciso, `o1` è "minore" di `o2`, un numero positivo se `o1` è "maggiore" di `o2`, e $0$ se `o1` è "uguale" a `o2`. Oltre a questo metodo, presenta anche altri **metodi di default**, come:
- **`comparing(Function<T, U> f)`**, che restituisce un `Comparator` creato automaticamente su un attributo dell'oggetto di tipo `T`, sfruttando `f`;
- **`thenComparing(Function<T, U> f)`**, utilizzato in concatenazione con il metodo precedente, per applicare un ordinamento secondario definito da `f` successivo a quello iniziale;
- **`reversed()`**, che inverte l'ordine di un `Comparator`.
___
#### Predicate e BiPredicate

L'interfaccia funzionale **`Predicate<T>`** rappresenta una **funzione logica** basata su **un singolo argomento** di tipo generico `T` in input. Il suo unico **metodo astratto** è:

```
boolean test(T t);
```

ma presenta anche altri **metodi di default**, come:
- **`Predicate<T> and(Predicate<? super T> other)`**, che restituisce un nuovo `Predicate` corrispondente all'AND tra quello su cui viene chiamato il metodo e `other`;
- **`Predicate<T> or(Predicate<? super T> other)`**, che restituisce un nuovo `Predicate` corrispondente all'OR tra quello su cui viene chiamato il metodo e `other`;
- **`Predicate<T> negate()`**, che restituisce un nuovo `Predicate` corrispondente alla negazione logica di quello su cui viene chiamato il metodo.

Invece, l'interfaccia funzionale **`BiPredicate<T, U>`** rappresenta sempre una **funzione logica** ma basata su **due argomenti** di tipi generici `T` e `U` in input. Presenta gli stessi metodi (astratti e non), con le opportune variazioni per permettere l'utilizzo di più di un input.
___
#### Function e BiFunction

L'interfaccia funzionale **`Function<T, R>`** rappresenta una **funzione che accetta un input di tipo `T` e restituisce un output di tipo `R`**. Naturalmente, viene utilizzata soprattutto per operazioni di trasformazione e conversione di tipo. Il suo unico **metodo astratto** è:

```
R apply(T t);
```

ma presenta anche altri **metodi di default**, come:
- **`Function<V, R> compose(Function<? super V, ? extends T> before)`**, che restituisce una nuova `Function` corrispondente all'applicazione sequenziale prima di `before` e poi di quella su cui viene chiamato il metodo;
- **`Function<T, V> andThen(Function<? super R, ? extends V> after)`**, che restituisce una nuova `Function` corrispondente all'applicazione sequenziale prima di quella su cui viene chiamato il metodo e poi di `after`;
- **`Function<T, T> identity()`**, che restituisce una nuova `Function` corrispondente a un'identità (come output avrà il suo input, privo di variazioni).

Invece, l'interfaccia funzionale **`BiFunction<T, U, R>`** rappresenta una **funzione che prende due input di tipo `T` e `U` e restituisce un output di tipo `R`**. Presenta lo stesso metodo astratto, con le opportune variazioni per permettere l'utilizzo di più di un input, mentre come metodo di default si ha solo:
- **`BiFunction<T, U, V> andThen(Function<? super R, ? extends V> after)`**, che restituisce una nuova `BiFunction` corrispondente all'applicazione sequenziale prima di quella su cui viene chiamato il metodo e poi di `after`.
___
#### Consumer e BiConsumer

L'interfaccia funzionale **`Consumer<T>`** rappresenta un'**operazione che accetta un input di tipo `T` e non restituisce nulla**. Viene utilizzata soprattutto per operazioni come stampe, logging, salvataggi o modifiche su oggetti mutabili. Il suo unico **metodo astratto** è:

```
void accept(T t);
```

e presenta anche un **metodo di default**, ossia:
- **`Consumer<T> andThen(Consumer<? super T> after)`**, che restituisce un nuovo `Consumer` corrispondente all'applicazione sequenziale prima di quello su cui viene chiamato il metodo e poi di `after`.

Invece, l'interfaccia funzionale **`BiConsumer<T, U>`** rappresenta un'**operazione che accetta due input di tipi `T` e `U` e non restituisce nulla**. Presenta gli stessi metodi (astratti e non), con le opportune variazioni per permettere l'utilizzo di più di un input.
___
#### Supplier

L'interfaccia funzionale **`Supplier<T>`** rappresenta un'**operazione che non accetta input e restituisce un output di tipo `T`**. Viene utilizzata soprattutto per fornire elementi come valori casuali, istanze ritardate di determinate classi, o dati predefiniti. Il suo unico **metodo astratto** è:

```
T get();
```
___