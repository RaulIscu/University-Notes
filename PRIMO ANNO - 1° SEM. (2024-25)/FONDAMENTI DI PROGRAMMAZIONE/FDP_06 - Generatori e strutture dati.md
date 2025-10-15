## Generatori

Per ottenere lunghe liste di valori, si può utilizzare un **generatore**, ossia un oggetto che fornisce una sequenza immutabile di numeri. In Python, il generatore principale è l'oggetto **`range`**, e si può ottenere una sequenza del genere mediante la funzione **`range(start, end, step)`**. 

Gli argomenti `start` e `step` della funzione appena citata sono tecnicamente opzionali, mentre per dare un senso alla chiamata deve essere presente almeno un argomento `end`. Vediamo, nel dettaglio, cosa rappresentano ciascuno di questi argomenti:
- l'argomento **`start`**, se specificato, indica il valore da cui inizierà la sequenza di numeri fornita (l'estremo `start` è incluso, e se omesso assumerà di default il valore $0$);
- l'argomento **`end`** indica il valore con cui terminerà la sequenza di numeri fornita (l'estremo `end` non è incluso);
- l'argomento **`step`**, se specificato, indica che i numeri verranno presi ogni `step` numeri.

Di seguito, alcuni esempi di generatori: 
- `range(101)`, che restituirà la sequenza `0, 1, 2, …, 100`; 
- `range(3, 101)`, che restituirà la sequenza `3, 4, 5, …, 100`; 
- `range(3, 101, 2)`, che restituirà la sequenza `3, 5, 7, ..., 99`.
___
## Strutture dati

Avendo introdotto i generatori, diventa importante ora parlare anche dei **contenitori**, alcune **strutture dati** tipiche di Python, ciascuna con varie caratteristiche specifiche. In particolare, vediamo:
- la **lista** (**`list`**), un insieme indicizzato e mutabile di elementi eterogenei;
- la **tupla** (**`tuple`**), un insieme indicizzato e immutabile di elementi eterogenei;
- l’**insieme** (**`set`**), un insieme non indicizzato, mutabile e senza ripetizioni di elementi eterogenei immutabili;
- il **dizionario** (**`dict`**), un insieme mutabile di coppie `chiave : valore` indicizzato sulle chiavi.

A seconda del tipo di contenitore, si utilizzano caratteri diversi per indicarne uno: la lista si delimita con delle parentesi quadre (`[]`), la tupla si delimita con delle parentesi tonde (`()`), e l’insieme si delimita con delle parentesi graffe (`{}`), così come il dizionario.

##### Liste

Una **lista** è una **sequenza indicizzata e mutabile di elementi eterogenei**. Essendo indicizzata (gli indici vanno da `0` per il primo elemento in poi), può essere vista come un **insieme ordinato**, e permette di contenere elementi duplicati. Può contenere elementi anche di tipi diversi, e può essere creata in due modi:
- utilizzando il costruttore **`list()`**, specificando gli elementi che si vogliono inserire nella lista all'interno di parentesi tonde come argomento del costruttore;
- specificando direttamente la lista con gli elementi contenuti tra **parentesi quadre** (**`[]`**).

Su una lista è possibile effettuare tutte le operazioni che sono state precedentemente introdotte parlando di [[FDP_05 - Tipi#Le stringhe `str`|stringhe]], ossia l'ottenimento del **numero di elementi contenuti**, l'ottenimento di un **elemento a un particolare indice**, lo **slicing**, l'**iterazione sugli elementi contenuti**, la **verifica della presenza di un elemento nella lista**, la **concatenazione di due liste** o di **una lista con sé stessa `n` volte**.

Oltre a ciò, sono disponibili vari **metodi** per manipolare e modificare una lista:
- **`l.append(el)`**, che aggiunge l'elemento `el` alla fine della lista `l`;
- **`l.clear()`**, che elimina tutti gli elementi della lista `l`;
- **`l.copy()`**, che restituisce una copia della lista `l`;
- **`l.count(el)`**, che conta il numero di occorrenze dell'elemento `el` nella lista `l`;
- **`l.extend(it)`**, che aggiunge gli elementi dell'iterabile `it` alla fine della lista `l`; 
- **`l.index(el)`**, che restituisce l'indice della prima occorrenza di `el` all'interno della lista `l` (nel caso in cui tale elemento non sia presente, verrà sollevata un'eccezione);
- **`l.insert(i, el)`**, che inserisce, all’indice `i` della lista `l`, l'elemento `el` (l'elemento precedentemente presente a tale indice non viene eliminato);
- **`l.pop(i)`**, che permette di eliminare l'elemento all'indice `i` della lista `l` (se non viene specificato `i`, verrà eliminato l'ultimo elemento della lista);
- **`l.remove(el)`**, che permette di eliminare la prima occorrenza dell'elemento `el` dalla lista `l` (nel caso in cui tale elemento non sia presente, verrà sollevata un'eccezione);
- **`l.reverse()`**, che inverte l’ordine degli elementi della lista `l`;
- **`l.sort(key, reverse)`**, che ordina gli elementi della lista `l` secondo una funzione `key` (si tratta di un argomento opzionale, che se non inserito porta la funzione a un ordinamento alfanumerico in ordine crescente; se si vuole, invece, invertire l'ordinamento che si otterrebbe di default o con `key`, si inserisca l'argomento opzionale `reverse=True`).

Una funzionalità molto comoda e particolare delle liste è la cosiddetta "**list comprehension**", che permette di creare liste che rispettano determinate condizioni con una sintassi compatta. Generalmente, la sintassi della list comprehension può essere formalizzata nel modo seguente:

```
l = [expression for item in iterable if condition]
```

dove `expression` è una qualsiasi espressione o letterale, e la `condition` è una condizione booleana che permette di "filtrare" gli elementi da inserire nella lista `l` (l'`item` ottenuto dal ciclo `for` viene inserito nella nuova lista solo se `condition` è `True` per quell'elemento).
___
##### Tuple

Una **tupla** è una **sequenza indicizzata e immutabile di elementi eterogenei**. Essendo indicizzata (gli indici vanno da `0` per il primo elemento in poi), può essere vista come un **insieme ordinato**, e permette di contenere elementi duplicati. Può contenere elementi anche di tipi diversi, e può essere creata in due modi:
- utilizzando il costruttore **`tuple()`**, specificando gli elementi che si vogliono inserire nella tupla all'interno di parentesi tonde come argomento del costruttore;
- specificando direttamente la tupla con gli elementi contenuti tra **parentesi tonde** (**`()`**).

Su una tupla è possibile effettuare l'ottenimento del **numero di elementi contenuti**, l'ottenimento di un **elemento a un particolare indice**, lo **slicing**, l'**iterazione sugli elementi contenuti**, la **verifica della presenza di un elemento nella tupla**, la **concatenazione di due tuple** o di **una tupla con sé stessa `n` volte**.

Oltre a ciò, sono disponibili vari **metodi** per manipolare e modificare una tupla:
- **`t.count(el)`**, che conta il numero di occorrenze dell’elemento `el` nella tupla `t`;
- **`t.index(el)`**, che restituisce l'indice della prima occorrenza di `el` all'interno della tupla `l` (nel caso in cui tale elemento non sia presente, verrà sollevata un'eccezione).

Per le tuple, inoltre, è molto comodo eseguire l'**unpacking**, operazione che abbiamo già introdotto parlando dell'[[FDP_02 - Variabili e namespace#Assegnamenti multipli|assegnamento multiplo]] per le variabili. Per effettuare un unpacking da una tupla, e memorizzare quindi ciascuno dei valori contenuti al suo interno in una variabile distinta, scriviamo codice del genere:

```
t = ("red", "blu", "green")

(color1, color2, color3) = t
```

Si ricordi che per un unpacking "puro" come quello appena mostrato è fondamentale che il numero di variabili sia pari al numero di elementi contenuti nella tupla considerata. In alternativa, se il numero di variabili è minore del numero di elementi della tupla, è possibile effettuare anche un unpacking del genere:

```
fruits = ("apple", "banana", "cherry", "strawberry", "raspberry")  
  
(green, yellow, *red) = fruits
```

dove l'asterisco indica che gli elementi rimanenti della tupla verranno inseriti in una lista memorizzata nella variabile `red`.
___
##### Insiemi

Un'**insieme**, detto anche "**set**", è più nello specifico un **insieme non indicizzato, non ordinato e mutabile di elementi eterogenei immutabili**, che inoltre non permette di contenere elementi duplicati. Può contenere elementi anche di tipi diversi, e può essere creato in due modi:
- utilizzando il costruttore **`set()`**, specificando gli elementi che si vogliono inserire nell'insieme all'interno di parentesi tonde come argomento del costruttore;
- specificando direttamente l'insieme con gli elementi contenuti tra **parentesi graffe** (**`{}`**).

Su una tupla è possibile effettuare l'ottenimento del **numero di elementi contenuti**, l'**iterazione sugli elementi contenuti** e la **verifica della presenza di un elemento nell'insieme**.

Oltre a ciò, sono disponibili vari **metodi** per manipolare e modificare un insieme:
- **`s.add(el)`**, che permette di aggiungere un elemento `el` all’insieme `s`;
- **`s.clear()`**, che elimina tutti gli elementi dell’insieme `s`;
- **`s.copy()`**, che restituisce una copia dell'insieme `s`;
- **`s1.difference(s2)`**, oppure **`s1 - s2`**, che risulterà in un insieme contenente gli elementi di `s1` che non sono presenti in `s2`, o in altre parole la differenza tra `s1` ed `s2`;
- **`s.discard(el)`**, che permette di eliminare l'elemento `el` dall'insieme `s`;
- **`s1.intersection(s2)`**, oppure **`s1 & s2`**, che risulterà in un insieme contenente gli elementi di `s1` che sono presenti anche in `s2`, o in altre parole l'intersezione tra `s1` ed `s2`;
- **`s1.isdisjoint(s2)`**, che restituisce `True` se gli insiemi `s1` ed `s2` non hanno elementi in comune, o in altre parole se la loro intersezione è un insieme vuoto;
- **`s1.issubset(s2)`**, oppure `s1 <= s2`, che restituisce `True` se tutti gli elementi di `s1` sono contenuti anche in `s2`, o in altre parole se `s1` è un sottoinsieme di `s2`;
- **`s1.issuperset(s2)`**, oppure `s1 >= s2`, che restituisce `True` se tutti gli elementi di `s2` sono contenuti anche in `s1`, o in altre parole se `s2` è un sottoinsieme di `s1`;
- **`s.pop()`**, che permette di rimuovere un elemento casuale dall'insieme `s` e di restituirlo;
- **`s.remove(el)`**, che permette di eliminare l'elemento `el` dall'insieme `s` (nel caso in cui tale elemento non sia presente, verrà sollevata un'eccezione);
- **`s1.symmetric_difference(s2)`**, oppure **`s1 ^ s2`**, che risulterà in un insieme contenente gli elementi che non sono in comune tra `s1` ed `s2`, o in altre parole
- **`s1.union(s2)`**, oppure **`s1 | s2`**, che risulterà in un insieme contenente gli elementi di `s1` e di `s2`, o in altre parole l'unione tra i due insiemi `s1` ed `s2`;
- **`s1.update(s2)`**, oppure **`s1 |= s2`**, che aggiornerà l'insieme `s1` aggiungendoci tutti gli elementi dell'insieme `s2` (quest'ultimo può essere un qualsiasi iterabile, non necessariamente un insieme).

Insieme ai normali insiemi, Python ne fornisce anche una lieve variazione, ossia i cosiddetti "**frozen set**", che si comportano in maniera analoga agli insiemi analizzati finora ma con la particolarità di essere **immutabili**: dunque, una volta creato un frozen set, non si potranno aggiungere o rimuovere elementi da esso. Per creare un frozen set, occorrerà utilizzare il costruttore **`frozenset()`**. 
___
##### Dizionari

Un **dizionario** è una **sequenza di coppie `chiave : valore`, indicizzata sulle chiavi e mutabile**. Essendo indicizzata sulle chiavi, si può accedere a determinate coppie o, più nello specifico, valori facendo riferimento alla chiave corrispondente; **non è possibile**, inoltre, **avere più coppie con la medesima chiave**. I valori delle coppie possono essere anche di tipi diversi, e un dizionario può essere creato in due modi:
- utilizzando il costruttore **`dict()`**, specificando gli elementi che si vogliono inserire nel dizionario all'interno di parentesi tonde come argomento del costruttore;
- specificando direttamente il dizionario con gli elementi contenuti tra **parentesi graffe** (**`{}`**).

Su un dizionario è possibile effettuare l'ottenimento del **numero di elementi contenuti**, l'ottenimento di un **elemento in base a una particolare chiave**, l'**iterazione sugli elementi contenuti** e la **verifica della presenza di una chiave nel dizionario**.

Oltre a ciò, sono disponibili vari **metodi** per manipolare e modificare un dizionario:

Infine, analizziamo le operazioni fattibili nell’ambito dei **dizionari**:
- **`d1 | d2`**, che fornisce un nuovo dizionario contenente tutte le coppie di `d1` e `d2`;
- **`d.clear()`**, che elimina tutti gli elementi del dizionario `d`;
- **`d.copy()`**, che restituisce una copia del dizionario `d`;
- **`dict.fromkeys(keys, value)`**, che restituisce un nuovo dizionario creando una coppia `chiave : valore` per ciascuna delle chiavi contenute nell'iterabile `keys`, inserendo in ogni coppia lo stesso valore `value`;
- **`d.get(key, default)`**, che restituisce il valore associato alla chiave `key`, nel caso in cui essa sia presente (altrimenti, fornirà il valore `default`);
- **`d.items()`**, che restituisce una lista di tuple, ciascuna delle quali corrisponde a una coppia `chiave : valore` contenuta nel dizionario `d`;
- **`d.keys()`**, che restituisce una lista contenente le chiavi del dizionario `d`;
- **`d.pop(key, default)`**, che rimuove l’elemento associato alla chiave `key` dal dizionario `d`, nel caso in cui esso sia presente (altrimenti, fornirà il valore `default`);
- **`d.popitem()`**, che elimina l'ultimo elemento inserito nel dizionario `d` e lo restituisce;
- **`d.setdefault(key, default)`**, che restituisce il valore associato alla chiave `key`, nel caso in cui essa sia presente (altrimenti, la inserisce con associato il valore `default`);
- **`d1.update(d2)`**, che modifica il dizionario `d1` aggiungendo, in ordine, le coppie `chiave : valore` di `d2` (nel caso in cui venga inserita una coppia con chiave già presente in `d1`, la coppia in questione in quest'ultimo verrà aggiornata con il valore della coppia di `d2`);
- **`d.values()`**, che restituisce una lista contenente i valori del dizionario `d` (compresi eventuali duplicati).
___