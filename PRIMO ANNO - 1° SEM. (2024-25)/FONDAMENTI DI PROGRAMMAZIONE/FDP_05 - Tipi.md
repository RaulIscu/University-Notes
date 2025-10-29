All'interno di Python, vengono definiti vari **tipi** built-in, che permettono di codificare una grande varietà di dati, tra cui:
- i **numeri**, che includono **`int`**, **`float`** e **`complex`**;
- i **booleani**, ossia **`bool`**;
- le **stringhe**, ossia **`str`**;
- i **valori nulli**, ossia **`NoneType`**.

Di seguito, questi tipi verranno analizzati più nel dettaglio.

## I numeri: `int`, `float` e `complex`

Il tipo **`int`** è quello a cui appartengono tutti i **numeri interi**, positivi o negativi che siano.

Il tipo **`float`** è quello a cui appartengono tutti i **numeri con parte decimale**, informalmente i "numeri con la virgola", anch'essi positivi o negativi che siano; per indicare il separatore tra parte intera e parte decimale si utilizza un punto (`.`). Una particolarità dei `float` è che contemplano anche numeri scritti in notazione scientifica, dove si inserirà una `e` seguita da un numero per indicare che il numero inserito a sinistra della `e` viene moltiplicato per la potenza di $10$ avente come esponente il numero a destra.

Il tipo **`complex`** è quello a cui appartengono tutti i **numeri complessi**, ossia numeri formati da una parte reale e una parte immaginaria. Per specificare la parte immaginaria, si inserisce una `j` alla sua destra (ad esempio, `x = 3 + 5j`).

È possibile convertire facilmente un numero di un tipo in un numero di un altro, utilizzando le funzioni **`int()`**, **`float()`** e **`complex()`** (tuttavia, non è possibile convertire un numero complesso in altri tipi).
___
## I booleani: `bool`

Il tipo **`bool`** è quello a cui appartengono i **valori booleani**, che possono essere solo **`True`** o **`False`**. Un valore booleano viene restituito dal confronto di due variabili tramite gli [[FDP_04 - Operatori#Operatori di confronto|operatori di confronto]].

In Python, è possibile valutare pressoché qualsiasi espressione come un valore booleano tramite la funzione **`bool()`**, che prende come argomento l'espressione in questione. A seconda del contesto, possiamo prevedere se la funzione restituirà `True` o `False`. Ad esempio, le seguenti espressioni corrispondono a `True`:
- il valore booleano `True` stesso;
- qualsiasi numero che non sia `0`;
- qualsiasi stringa non vuota;
- qualsiasi lista, tupla, insieme o dizionario non vuoti.

Al contrario, le seguenti espressioni corrispondono a `False`:
- il valore booleano `False` stesso;
- il numero `0`;
- una stringa vuota;
- una lista, tupla, insieme o dizionario vuoti;
- il valore nullo `None`.
___
## Le stringhe: `str`

Il tipo **`str`** viene utilizzato per contenere qualsiasi **stringa di testo**. È possibile pensare una stringa come un **array di caratteri**, che è anche il modo in cui una stringa viene concretamente memorizzata in memoria. In Python, la stringa è una struttura dati **immutabile**: una volta creata una specifica stringa, essa non potrà essere “modificata” in sé.

Una qualsiasi stringa, per essere tale, deve essere delimitata da **apici** (`' '`) o **doppi apici** (`" "`). Se si vuole, invece, scrivere una stringa di testo che contiene accapi, senza utilizzare [[FDP_03 - Print|escape characters]], esse vanno delimitate da **tripli apici** (`''' '''` o `""" """`). Va da sé che, se si delimita una stringa con un determinato tipo di apice, non si potrà includere tale apice all'interno della stringa stessa, a meno che non si utilizzino gli escape characters.

##### Stringhe e operatori

Le stringhe sono compatibili con alcuni degli **operatori di base**. In particolare, è possibile **concatenare due stringhe** utilizzando l'operatore **`+`**:

```
s = "Hello, "
s1 = "World!"

print(s + s1)              # verrà stampato "Hello, World!"
```

È possibile utilizzare anche la **moltiplicazione** (**`*`**) con le stringhe. Ad esempio, scrivere **`s * n`**, dove `s` è una stringa e `n` un intero positivo, porterà alla creazione di una nuova stringa costituita dalla stringa `s` concatenata con sé stessa `n` volte. 
___
##### Stringhe come array di caratteri

Come accennato in precedenza, **una stringa può essere interpretata come array di caratteri**. Per questo motivo, molte delle operazioni di manipolazione di una lista possono essere eseguite anche su una stringa di testo. Ad esempio, è possibile ottenere la **lunghezza**, ossia il **numero di caratteri**, di una stringa utilizzando la funzione **`len(s)`**:

```
s = "Hello, World!"

print(len(s))               # verrà stampato 13
```

Poi, è possibile ottenere il **carattere a un determinato indice della stringa** con la dicitura **`s[i]`**, dove `i` è l'indice del carattere che si vuole estrapolare:

```
s = "Hello, World!"

print(s[3])                 # verrà stampato "l"
```

Per individuare un carattere specifico della stringa, è possibile utilizzare anche **indici negativi**: essi funzionano allo stesso modo degli indici positivi, con la differenza che l'indicizzazione parte dal termine della stringa, invece che dall'inizio (ad esempio, `s[-1]` restituirà l'ultimo carattere della stringa, `s[-2]` restituirà il penultimo, e così via). Un'altra operazione utilissima eseguibile su una stringa è il cosiddetto "**slicing**", che permette di estrapolare un determinato intervallo di caratteri della stringa considerata: per fare ciò, si utilizzerà una dicitura del tipo **`s[start:end:step]`**, dove:
- `start` indica l'indice del primo carattere della slice;
- `end` indica l'indice dell'ultimo carattere della slice (tale carattere non è incluso, l'ultimo carattere effettivamente incluso nella slice sarà il carattere a indice `end - 1`);
- `step` indica il cosiddetto "incremento" della slice, e se specificato i caratteri della slice verranno presi ogni `step` caratteri.

È possibile omettere alcuni dei tre parametri, ottenendo risultati diversi in base a quali e quanti parametri sono omessi: ad esempio, se si omette `start`, e si scrive quindi `s[:end:step]`, la slice partirà dal primo carattere della stringa `s`; se si omette `end`, e si scrive quindi `s[start::step]`, la slice terminerà all'ultimo carattere della stringa `s`; se si omettono sia `start` che `end`, e si scrive quindi `s[::step]` la slice verrà presa a partire dall'intera stringa `s`; se si omette `step`, e si scrive quindi `s[start:end]`, la slice non presenterà alcuna forma di incremento; e così via. Vediamo alcuni esempi:

```
s = "Hello, World!"

print(s[:5:2])               # verrà stampato "Hlo"
print(s[::-1])               # verrà stampato "!dlroW ,olleH"
print(s[1:8])                # verrà stampato "ello, W"
```

Ancora, è possibile **iterare sui caratteri di una stringa**, utilizzando un ciclo `for` o un ciclo `while`:

```
for carattere in s:
	print(carattere)
```

Infine, si può **verificare se una stringa è contenuta in un'altra**, utilizzando gli operatori **`in`** e **`not in`**:

```
print("Hello" in "Hello, World!")          # verrà stampato True
```
___
##### Metodi sulle stringhe

Ci sono molte altre funzioni che possono essere utili nel lavorare con stringhe, tra cui:
- **`s.capitalize()`**, che “capitalizza” la stringa `s`, rendendone maiuscolo il primo carattere;
- **`s.count(el)`**, che conta quante volte è presente `el` nella stringa `s`;
- **`s.endswith(el)`**, che restituisce `True` se la stringa `s` termina con `el`, e `False` altrimenti;
- **`s.find(el)`**, che restituisce l'indice di inizio della prima occorrenza di `el` nella stringa `s` (se `el` non viene trovato, restituisce `-1`);
- **`s.index(el)`**, che restituisce l’indice di inizio della prima occorrenza di `el` nella stringa `s` (solleva un'eccezione se `el` non viene trovato);
- **`s.isalnum()`**, che restituisce ```True``` se tutti i caratteri della stringa sono alfanumerici;
- **`s.isalpha()`**, che restituisce ```True``` se tutti i caratteri della stringa sono alfabetici;
- **`s.isdigit()`**, che restituisce `True` se tutti i caratteri della stringa sono cifre numeriche;
- **`s.islower()`**, che restituisce `True` se tutti i caratteri alfabetici della stringa sono minuscoli;
- **`s.isspace()`**, che restituisce ```True``` se tutti i caratteri della stringa sono spazi vuoti;
- **`s.isupper()`**, che restituisce `True` se tutti i caratteri alfabetici della stringa sono maiuscoli;
- **`s.join(els)`**, che crea una nuova stringa unendo gli elementi `els`, con `s` che rappresenta il separatore che verrà inserito all’interno della stringa tra i vari elementi;
- **`s.lower()`**, che crea una nuova stringa equivalente alla stringa `s` ma composta esclusivamente da caratteri minuscoli;
- **`s.replace(old, new, count)`**, che sostituisce le occorrenze di `old` all'interno della stringa `s` con `new`; il parametro `count`, opzionale, serve a specificare un numero preciso di occorrenze dell’elemento `old` da sostituire, mentre la sua assenza porterà alla sostituzione di tutte le occorrenze;
- **`s.split(sep, maxsplit)`**, che divide la stringa `s` in corrispondenza delle varie occorrenze del separatore `sep` (se omesso, verrà considerato come separatore lo spazio vuoto) e inserisce i vari frammenti ottenuti in una lista; inserire il parametro opzionale `maxsplit` specificherà il numero di divisioni da fare (se omesso, verranno effettuate divisioni considerando l'interezza della stringa `s`);
- **`s.strip()`**, che crea una nuova stringa a partire dalla stringa `s` rimuovendo eventuali spazi vuoti iniziali o finali;
- **`s.upper()`**, che crea una nuova stringa equivalente alla stringa `s` ma composta esclusivamente da caratteri maiuscoli.
___
##### F-Strings

A partire da Python 3.6, è possibile costruire **stringhe con parti dipendenti da variabili** utilizzando le cosiddette "**f-strings**", o "**format strings**". Per definire una stringa come f-string, basterà anteporre una **`f`** al letterale della stringa in questione, e all'interno della stessa specificare le parti che si vogliono ottenere a partire da altre variabili tra parentesi graffe (**`{}`**), inserendo al loro interno il nome della variabile che si vuole utilizzare. Vediamo un esempio:

```
name = Raul  
s = f"Hi, my name is {name}"
```
___