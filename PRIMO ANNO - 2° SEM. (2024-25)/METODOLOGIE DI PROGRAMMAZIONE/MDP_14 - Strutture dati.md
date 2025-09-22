## Array

Un **array** è una collezione indicizzata di elementi dello stesso tipo. Si può creare un array per oggetti di sostanzialmente qualsiasi tipo, e un array può avere una o più dimensioni. L'array più basilare è un **array a una dimensione**, che consiste in una semplice lista di elementi dello stesso tipo. Genericamente, per dichiarare un array a una dimensione si utilizza il seguente codice:

```
tipo[] nomeDellArray;
```

dove `tipo` indica il tipo degli elementi contenuti nell'array: l'array in questione, dunque, potrà contenere solo elementi del tipo specificato. Tuttavia, nonostante con questo codice venga dichiarata una variabile `nomeDellArray`, non ne viene effettivamente creato uno; per creare un nuovo, concreto, array di elementi, bisogna istanziarlo usando la parola chiave **`new`**, similmente a come si fa quando si istanziano nuovi oggetti. Ad esempio:

```
nomeDellArray = new tipo[lunghezza];
```

Con `lunghezza` si intende la dimensione dell'array che si sta creando, ossia il numero di elementi contenuto al suo interno. In base al tipo di array creato, le variabili al suo interno vengono inizializzate nei seguenti modi:
- se si ha un array di **interi**, le variabili vengono inizializzate a 0;
- se si ha un array di **booleani**, le variabili vengono inizializzate a `false`;
- se si ha un array di **tipi di riferimento**, le variabili vengono inizializzate a `null`.

Essendo l'array indicizzato, è possibile accedere a singoli elementi di esso conoscendone l'indice (l'indicizzazione parte da 0 e non da 1): ad esempio, per accedere all'elemento posto all'indice 4 di un array generico, si utilizza il seguente codice:

```
nomeDellArray[4]
```

Una volta istanziato un array, **non è possibile modificarne la lunghezza**; tuttavia, è perfettamente possibile modificare dinamicamente singoli elementi dello stesso.

Se si vuole creare un array di una lunghezza precisa e con degli elementi precisi, è possibile utilizzare un **array initializer**, ossia una lista di espressioni, separate da virgole, racchiusa tra due parentesi graffe; utilizzando questo approccio, si creerà un array dotato degli stessi elementi ordinati allo stesso modo dell'array initializer. Usare quest'ultimo, inoltre, permette di omettere la parola chiave `new`, anche se si dovrà comunque specificare il tipo degli elementi. Ad esempio, di seguito il codice che istanzia un array composto dal numero di giorni di ogni mese dell'anno in ordine:

```
int[] month_days = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
```

Oltre agli array a una dimensione, esistono quelli che si definiscono "**array multidimensionali**", ossia sostanzialmente degli array in cui gli elementi sono altri array; ad esempio, un array bidimensionale è un array di array di elementi. Dichiarare un array multidimensionale segue lo stesso procedimento di quelli a una dimensione. Per implementare, per esempio, un array contenente 4 array, ognuno dei quali destinato a contenere 5 interi, sarà necessario il seguente codice:

```
int[][] twoDimensions = new int[4][5];
```

Concettualmente, tale array bidimensionale può essere rappresentato nel modo seguente:

![[array2d_example.png]]

Nella dichiarazione di un array multidimensionale, è necessaria solo la lunghezza dell'array più "esterno", ossia di quello che conterrà tutti gli altri. Non specificare a priori la lunghezza degli array contenuti, come abbiamo invece fatto nell'esempio precedente, può risultare utile in situazioni in cui tali array debbano essere di lunghezze diverse. Infatti, è possibile anche creare una situazione del genere:

```
int[][] twoDimensions = new int[4][];
twoD[0] = new int[1];
twoD[1] = new int[2];
twoD[2] = new int[3];
twoD[3] = new int[4];
```

ossia un array composto a sua volta da altri 4 array, contenenti rispettivamente 1, 2, 3 e 4 interi.

È possibile, inoltre, utilizzare un array initializer anche per array multidimensionali; basterà inizializzare ognuno degli array interni con le proprie parentesi graffe, come nel seguente esempio:

```
int[][] twoDimensions = {
	{0, 0, 0, 0},
	{0, 1, 2, 3},
	{0, 2, 4, 6},
	{0, 3, 6, 9}
};
```
___
## Java Collection Framework

Oltre agli array, che rappresentano la forma di struttura dati più basilare presente in Java, sono disponibili tramite il **Java Collection Framework** le cosiddette "**collezioni**", una serie di strutture dati versatili, potenti, e dotate di vari metodi utili per manipolarle al meglio.

Le collezioni si dividono principalmente in **tre macro-categorie**:
- **liste**;
- **insiemi**;
- **mappe**.

Implementando tutte l'[[MDP_12 - Interfacce|interfaccia]] **`Iterable<E>`**, è possibile per tutte le collezioni iterare comodamente i propri elementi in vari modi:
- sfruttando degli oggetti di tipo **`Iterator<E>`**;
- mediante un ***[[Istruzioni di controllo#Il for loop*|for-each loop]]***;
- solo per le liste, mediante un *for loop* che itera sugli indici degli elementi.

Oltre a queste soluzioni, è possibile anche sfruttare il metodo `Iterable.forEach(Consumer<T>)` per eseguire un'iterazione interna sugli elementi di una collezione, senza specificare necessariamente modi particolari per effettuarla (NB: utilizzare il metodo `forEach` produrrà risultati diversi in base alla classe dell'oggetto su cui si sta iterando, in quanto verrà chiamata l'implementazione di `forEach` relativa a tale classe).

**È altamente sconsigliato modificare una collezione mentre si sta iterando su di essa**, a meno che non lo si stia facendo in maniera controllata (ad esempio, utilizzando `Iterator.remove()`).

##### Le liste: ArrayList, LinkedList

In Java, ci sono principalmente **due tipi** di liste:
- le **`ArrayList`**;
- le **`LinkedList`**.

Entrambe sono basate su **`List`**, una sotto-interfaccia derivata da `Collection` e da `Iterable`.

Una lista di tipo **`ArrayList`** consiste in una **lista dinamica**, basata sull'[[MDP_14 - Strutture dati#Array|array]] ma molto più flessibile e manipolabile, innanzitutto per le sue dimensioni variabili e per il ridimensionamento dinamico della stessa. Si tratta di una struttura potente per memorizzare oggetti (anche duplicati) per cui è importante un accesso rapido tramite indice, ma lo spostamento, l'inserimento o la rimozione di elementi in mezzo alla lista risultano relativamente lenti.

Un'`ArrayList` viene dichiarata come un oggetto di tipo `List<E>`, e una sua costruzione assume tendenzialmente la seguente forma:

```
List<E> identificatore = new ArrayList<>();
```

I metodi principali che presenta l'`ArrayList` per visualizzare e manipolare i dati contenuti al suo interno sono i seguenti:
- **`add(E e)`**, che aggiunge l'elemento `e` alla fine della lista;
- **`add(int index, E e)`**, che aggiunge l'elemento `e` all'indice `index` della lista;
- **`addAll(Collection<? extends E> c)`**, che aggiunge tutti gli elementi contenuti nella collezione `c` alla fine della lista, mantenendone l'ordine precedente, a patto però che il loro tipo sia compatibile con il tipo degli elementi già contenuti nella lista in questione;
- **`clear()`**, che rimuove tutti gli elementi della lista;
- **`clone()`**, che restituisce una "*shallow copy*" della lista;
- **`contains(E e)`**, che restituisce `true` se la lista contiene l'elemento `e`, e `false` se esso non è contenuto nella lista;
- **`get(int index)`**, che restituisce l'elemento all'indice `index` della lista;
- **`indexOf(E e)`**, che restituisce l'indice della prima occorrenza dell'elemento `e` all'interno della lista, o in alternativa -1 se l'elemento non è contenuto in essa;
- **`isEmpty()`**, che restituisce `true` se la lista non contiene elementi, e `false` altrimenti;
- **`lastIndexOf(E e)`**, che restituisce l'indice dell'ultima occorrenza dell'elemento `e` all'interno della lista, o in alternativa -1 se l'elemento non è contenuto in essa;
- **`remove(int index)`**, che rimuove l'elemento all'indice `index` della lista;
- **`remove(E e)`**, che rimuove la prima occorrenza dell'elemento `e` dalla lista, se esso è presente al suo interno;
- **`removeRange(int fromIndex, int toIndex)`**, che rimuove tutti gli elementi della lista compresi tra l'indice `fromIndex` (incluso) e l'indice `toIndex` (escluso) della stessa;
- **`reversed()`**, che restituisce una lista identica a quella su cui viene chiamato, ma ordinata al contrario;
- **`set(int index, E e)`**, che sovrascrive l'elemento all'indice `index` sostituendolo con l'elemento `e`;
- **`size()`**, che restituisce il numero di elementi contenuti nella lista;
- **`toArray()`**, che restituisce l'array corrispondente alla lista.

Una lista di tipo **`LinkedList`** consiste in una classica **linked list** doppiamente collegata, in cui ogni nodo presenta l'elemento memorizzato nella lista, un collegamento all'elemento precedente e un collegamento a quello successivo. È una struttura che, a differenza dell'`ArrayList`, consente inserimenti e rimozioni di elementi in maniera rapida in qualunque punto della lista, e funziona bene anche come rappresentazione di una coda o di uno stack.

Anche la `LinkedList` viene dichiarata come un oggetto di tipo `List<E>`, e una sua costruzione assume tendenzialmente la seguente forma:

```
List<E> identificatore = new LinkedList<>();
```

I metodi principali che presenta l'`LinkedList` per visualizzare e manipolare i dati contenuti al suo interno sono i seguenti:
- **`addFirst(E e)`**, che aggiunge l'elemento `e` in testa alla lista;
- **`addLast(E e)`**, che aggiunge l'elemento `e` in coda alla lista;
- **`descendingIterator()`**, che restituisce un iteratore "decrescente", che quindi parte dalla coda (ultimo elemento) della lista e si sposta verso sinistra;
- **`getFirst()`**, che restituisce il primo elemento della lista;
- **`getLast()`**, che restituisce l'ultimo elemento della lista;
- **`removeFirst()`**, che rimuove e restituisce il primo elemento della lista;
- **`removeLast()`**, che rimuove e restituisce l'ultimo elemento della lista.

Per le liste, oltre al classico `Iterator`, è possibile ottenere anche un **`ListIterator`** tramite il metodo **`listIterator()`**; l'oggetto restituito corrisponde a un **iteratore bidirezionale**, che può quindi scorrere la lista sia nel verso canonico (da sinistra verso destra), sia nel verso contrario (da destra verso sinistra).

Di seguito, i principali metodi utilizzabili con un `ListIterator`:
- **`hasNext()`**, che restituisce `true` se la lista contiene almeno un altro elemento successivo a quello corrente;
- **`hasPrevious()`**, che restituisce `true` se la lista contiene almeno un altro elemento precedente a quello corrente;
- **`next()`**, che restituisce l'elemento successivo della lista;
- **`nextIndex()`**, che restituisce l'indice dell'elemento successivo della lista;
- **`previous()`**, che restituisce l'elemento precedente della lista;
- **`previousIndex()`**, che restituisce l'indice dell'elemento precedente della lista;
- **`remove()`**, che rimuove l'elemento corrente dalla lista;
- **`set(E e)`**, che sovrascrive l'elemento corrente sostituendolo con l'elemento `e`.
___
##### Gli insiemi: HashSet, TreeSet e LinkedHashSet

In Java, ci sono principalmente **tre tipi** di insiemi:
- gli **`HashSet`**;
- i **`TreeSet`**;
- i **`LinkedHashSet`**.

Tutti e tre sono basati su **`Set`**, una sotto-interfaccia di `Collection` e `Iterable`. La loro particolarità, e principale differenza rispetto alle [[MDP_14 - Strutture dati#Le liste ArrayList, LinkedList|liste]], è che **non possono contenere elementi duplicati**.

Un insieme di tipo **`HashSet`** consiste in un insieme di elementi che vengono memorizzati in una **tabella di hash**, in modo da consentire un aggiunta e una ricerca molto efficienti. Se si è sicuri di non prevedere duplicati nei dati che si stanno manipolando, spesso un `HashSet` risulta essere una delle opzioni più preferibili; tuttavia, questa struttura dati **non permette di essere ordinata** in modo convenzionale, quindi diventa inutilizzabile se si vuole conservare un ordine nei dati memorizzati.

Un `HashSet` viene dichiarato come un oggetto di tipo `Set<E>`, e una sua costruzione assume tendenzialmente la seguente forma:

```
Set<E> identificatore = new HashSet<>();
```

I metodi principali che presenta l'`HashSet` per visualizzare e manipolare i dati contenuti al suo interno sono i seguenti:
- **`add(E e)`**, che aggiunge (se non è già presente) l'elemento `e` all'insieme;
- **`clear()`**, che rimuove tutti gli elementi dell'insieme;
- **`clone()`**, che restituisce una "*shallow copy*" dell'insieme;
- **`contains(E e)`**, che restituisce `true` se l'insieme contiene l'elemento `e`, e `false` se esso non è contenuto nell'insieme;
- **`isEmpty()`**, che restituisce `true` se l'insieme non contiene elementi, e `false` altrimenti;
- **`remove(E e)`**, che rimuove l'elemento `e` dall'insieme, se esso è presente al suo interno;
- **`size()`**, che restituisce il numero di elementi contenuti nell'insieme.

Un insieme di tipo **`TreeSet`** presenta sostanzialmente le stesse caratteristiche dell'`HashSet`, ma a differenza di quest'ultimo **ordina automaticamente gli elementi aggiunti ad esso** in base all'ordinamento naturale previsto per il loro tipo, o in base a un [[MDP_12 - Interfacce#Comparator|comparatore]] personalizzato se questo viene specificato nella costruzione dell'insieme, e mantiene tale ordine (questa caratteristica è ottenuta mediante l'implementazione interna particolare del `TreeSet`, che corrisponde a una variante di albero binario di ricerca chiamata "**red-black tree**").

Un `TreeSet` viene dichiarato come un oggetto di tipo `TreeSet<E>`, e una sua costruzione assume tendenzialmente la seguente forma:

```
TreeSet<E> identificatore = new TreeSet<>();
```

I metodi principali che presenta il `TreeSet` per visualizzare e manipolare i dati contenuti al suo interno sono gli stessi previsti per l'`HashSet`, con l'aggiunta dei seguenti:
- **`ceiling(E e)`**, che restituisce l'elemento dell'insieme più piccolo maggiore o uguale di `e`, o `null` se un elemento del genere non è trovato;
- **`descendingSet()`**, che restituisce l'insieme iniziale ma ordinato in ordine decrescente;
- **`first()`**, che restituisce il primo elemento dell'insieme, che essendo un insieme ordinato corrisponderà all'elemento "minore";
- **`floor(E e)`**, che restituisce l'elemento dell'insieme più grande minore o uguale di `e`, o `null` se un elemento del genere non è trovato;
- **`headSet(E e)`**, che restituisce un sottoinsieme degli elementi contenuti nell'insieme di partenza che sono minori di `e`;
- **`higher(E e)`**, che restituisce l'elemento dell'insieme più piccolo maggiore di `e`, o `null` se un elemento del genere non è trovato;
- **`last()`**, che restituisce l'ultimo elemento dell'insieme, che essendo un insieme ordinato corrisponderà all'elemento "maggiore";
- **`lower(E e)`**, che restituisce l'elemento dell'insieme più grande minore di `e`, o `null` se un elemento del genere non è trovato;
- **`pollFirst()`**, che rimuove e restituisce il primo elemento dell'insieme;
- **`pollLast()`**, che rimuove e restituisce l'ultimo elemento dell'insieme;
- **`subSet(E from, E to)`**, che restituisce un sottoinsieme degli elementi contenuti nell'insieme di partenza tra `from` (incluso) e `to` (escluso);
- **`tailSet(E e)`**, che restituisce un sottoinsieme degli elementi contenuti nell'insieme di partenza che sono maggiori o uguali di `e`.

Un insieme di tipo **`LinkedHashSet`** presenta sostanzialmente le stesse caratteristiche dell'`HashSet`, ma a differenza di quest'ultimo **mantiene l'ordine di inserimento degli elementi** al suo interno, implementando una **linked list** doppiamente collegata per mantenere tale ordine e per permettere una ricerca rapida.

Un `LinkedHashSet` viene dichiarato come un oggetto di tipo `LinkedHashSet<E>`, e una sua costruzione assume tendenzialmente la seguente forma:

```
LinkedHashSet<E> identificatore = new LinkedHashSet<>();
```

I metodi principali che presenta il `LinkedHashSet` per visualizzare e manipolare i dati contenuti al suo interno sono gli stessi identici previsti per l'`HashSet`, e non ne vengono aggiunti altri particolarmente rilevanti.
___
##### Le mappe: HashMap, TreeMap e LinkedHashMap

In Java, ci sono principalmente **tre tipi** di mappe:
- le **`HashMap`**;
- le **`TreeMap`**;
- le **`LinkedHashMap`**.

Tutte e tre sono basati su **`Map`**, una sotto-interfaccia di `Collection` e `Iterable`. La loro particolarità, e principale differenza rispetto alle altre strutture dati viste finora, è che non contengono singoli elementi, ma **coppie di elementi della forma "chiave-valore"**, con le chiavi che **non possono essere duplicate**.

Parlando di mappe, è importante anche parlare dell'interfaccia **`Map.Entry`**, un'interfaccia annidata statica contenuta all'interno dell'interfaccia `Map`, che rappresenta una singola "**entry**" della mappa, ossia **una singola coppia chiave-valore**. Questa classe permette una comoda iterazione sulle entry di una mappa, consentendo di lavorare contemporaneamente su una chiave e sui valori associati ad essa, anche grazie a metodi come:
- **`getKey()`** per ottenere la chiave associata a una entry;
- **`getValue()`** per ottenere il valore associato a una entry;
- **`setValue(V value)`** per settare il valore associato a una entry a `value` e restituire il valore precedente;
- **`equals(Map.Entry entry)`** per confrontare due entry, che vengono considerate uguali nel momento in cui sia le loro chiavi che i rispettivi valori coincidono.

Una mappa di tipo **`HashMap`** consiste in un insieme di coppie "chiave-valore" che vengono memorizzate in una **tabella di hash**, in modo da consentire un aggiunta e una ricerca molto efficienti. Come detto, le chiavi delle varie coppie devono essere **uniche**, e nel caso delle `HashMap` non è supportato `null` né come chiave né come valore; inoltre, questa struttura dati **non permette di essere ordinata** in modo convenzionale, quindi diventa inutilizzabile se si vuole conservare un ordine nei dati memorizzati.

Una `HashMap` viene dichiarata come un oggetto di tipo `HashMap<K, V>`, e una sua costruzione assume tendenzialmente la seguente forma:

```
Map<K, V> identificatore = new HashMap<>();
```

I metodi principali che presenta l'`HashMap` per visualizzare e manipolare i dati contenuti al suo interno sono i seguenti:
- **`clear()`**, che rimuove tutti gli elementi della mappa;
- **`compute(K key, BiFunction<? super K, ? super V, ? super V> function)`**,
- **`containsKey(K key)`**, che restituisce `true` se la mappa contiene la chiave `key`, o `false` altrimenti;
- **`containsValue(V value)`**, che restituisce `true` se almeno una chiave è associata al valore `value`, o `false` altrimenti;
- **`entrySet()`**, che restituisce un insieme contenente tutte le entry presenti nella mappa (rappresenta l'unico modo per ottenere concretamente degli oggetti di tipo `Map.Entry`);
- **`forEach(BiConsumer<? super K, ? super V> action)`**, che esegue un'azione definita da `action` per ogni entry della mappa;
- **`get(K key)`**, che restituisce il valore associato alla chiave `key`, o `null` se la chiave in questione non è presente;
- **`getOrDefault(K key, V defaultValue)`**, che restituisce il valore associato alla chiave `key`, o il valore `defaultValue` se la chiave in questione non è presente; 
- **`isEmpty()`**, che restituisce `true` se la mappa è vuota, o `false` altrimenti;
- **`keySet()`**, che restituisce un insieme contenente tutte le chiavi presenti nella mappa;
- **`put(K key, V value)`**, che inserisce la entry con la chiave `key` e il valore `value` nella mappa, e se una entry con tale chiave è già presente, restituisce il vecchio valore e lo sovrascrive con `value`;
- **`putIfAbsent(K key, V value)`**, che inserisce la entry con la chiave `key` e il valore `value` nella mappa solo se tale chiave non è già presente;
- **`remove(K key)`**, che rimuove dalla mappa la entry contenente la chiave `key` e restituisce il valore associato ad essa (o `null` se assente);
- **`replace(K key, V value)`**, che sostituisce il valore associato alla chiave `key` con il valore `value` solo se tale chiave è presente nella mappa;
- **`replace(K key, V oldValue, V newValue)`**, che sostituisce il valore associato alla chiave `key` con il valore `newValue` solo se tale chiave è presente nella mappa e il valore ad essa associato in precedenza corrisponde a `oldValue`;
- **`replaceAll(BiFunction<? super K, ? super V, ? extends V> function)`**, che sostituisce i valori di tutte le entry della mappa con il risultato della funzione `function` applicata su ognuna di esse;
- **`values()`**, che restituisce una `Collection` contenente tutti i valori presenti nella mappa.

Una mappa di tipo **`TreeMap`** presenta sostanzialmente le stesse caratteristiche dell'`HashMap`, ma a differenza di quest'ultima **ordina automaticamente le entry aggiunte ad essa** in base all'ordinamento naturale previsto per il tipo delle chiavi, o in base a un [[MDP_12 - Interfacce#Comparator|comparatore]] personalizzato se questo viene specificato nella costruzione della mappa, e mantiene tale ordine (questa caratteristica è ottenuta mediante l'implementazione interna particolare della `TreeMap`, che corrisponde a una variante di albero binario di ricerca chiamata "**red-black tree**").

Una `TreeMap` viene dichiarata come un oggetto di tipo `TreeMap<K, V>`, e una sua costruzione assume tendenzialmente la seguente forma:

```
TreeMap<K, V> identificatore = new TreeMap<>();
```

I metodi principali che presenta la `TreeMap` per visualizzare e manipolare i dati contenuti al suo interno sono gli stessi previsti per l'`HashMap`, con l'aggiunta dei seguenti:
- **`firstKey()`**, che restituisce la prima chiave della mappa;
- **`higherKey(K key)`**, che restituisce la chiave successiva alla chiave `key` nella mappa;
- **`lastKey()`**, che restituisce l'ultima chiave della mappa;
- **`lowerKey(K key)`**, che restituisce la chiave precedente alla chiave `key` nella mappa;
- **`subMap(K fromKey, K toKey)`**, che restituisce una sottomappa delle entry contenute nella mappa di partenza tra `fromKey` (inclusa) e `toKey` (esclusa).

Una mappa di tipo **`LinkedHashMap`** presenta sostanzialmente le stesse caratteristiche dell'`HashMap`, ma a differenza di quest'ultima **mantiene l'ordine di inserimento delle entry** al suo interno, implementando una **linked list** doppiamente collegata per mantenere tale ordine e per permettere una ricerca rapida.

Una `LinkedHashMap` viene dichiarata come un oggetto di tipo `LinkedHashMap<K, V>`, e una sua costruzione assume tendenzialmente la seguente forma:

```
LinkedHashMap<K, V> identificatore = new LinkedHashMap<>();
```

I metodi principali che presenta il `LinkedHashMap` per visualizzare e manipolare i dati contenuti al suo interno sono gli stessi identici previsti per l'`HashMap`, e non ne vengono aggiunti altri particolarmente rilevanti.
___
