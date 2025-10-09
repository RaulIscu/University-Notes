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

Il tipo **`str`** viene utilizzato per contenere qualsiasi **stringa di testo**: per assegnare una stringa di testo a una variabile, si utilizza
___