Un ***array*** è una collezione indicizzata di elementi dello stesso [[Tipi primitivi|tipo]]. Si può creare un *array* per oggetti di sostanzialmente qualsiasi tipo, e un *array* può avere una o più dimensioni.
___
L'*array* più basilare è un ***array* a una dimensione**, che consiste in una semplice lista di elementi dello stesso tipo. Genericamente, per dichiarare un *array* a una dimensione si utilizza il seguente codice:

```
tipo nomeDellArray[lunghezza];
```

dove *tipo* indica il tipo degli elementi contenuti nell'*array*: l'*array* in questione, dunque, potrà contenere solo elementi del tipo specificato. Tuttavia, nonostante con questo codice venga dichiarata una variabile *array*, non ne viene effettivamente creato uno; per creare un nuovo, concreto, *array* di elementi, bisogna istanziarlo usando la parola chiave **`new`**, similmente a come si fa quando si istanziano nuovi oggetti. Ad esempio:

```
nomeDellArray = new tipo[lunghezza];
```

Con *lunghezza* si intende la dimensione dell'*array* che si sta creando, ossia il numero di elementi contenuto al suo interno. In base al tipo di *array* creato, le variabili al suo interno vengono inizializzate nei seguenti modi:
- se si ha un *array* di **interi**, le variabili vengono inizializzate a 0;
- se si ha un *array* di **booleani**, le variabili vengono inizializzate a `false`;
- se si ha un *array* di **tipi di riferimento**, le variabili vengono inizializzate a `null`.

Essendo l'*array* indicizzato, è possibile accedere a singoli elementi di esso conoscendone l'indice (come per Python, l'indicizzazione parte da 0 e non da 1): ad esempio, per accedere all'elemento posto all'indice 4 di un *array* generico, si utilizza il seguente codice:

```
nomeDellArray[4]
```

Una volta istanziato un *array*, **non è possibile modificarne la lunghezza**; tuttavia, è perfettamente possibile modificare dinamicamente singoli elementi dello stesso.

Se si vuole creare un *array* di una lunghezza precisa e con degli elementi precisi, è possibile utilizzare un ***array initializer***, ossia una lista di espressioni, separate da virgole, racchiusa tra due parentesi graffe; utilizzando questo approccio, si creerà un *array* dotato degli stessi elementi ordinati allo stesso modo dell'*array initializer*. Usare quest'ultimo, inoltre, permette di omettere la parola chiave `new`, anche se si dovrà comunque specificare il tipo degli elementi. Ad esempio, di seguito il codice che istanzia un *array* composto dal numero di giorni di ogni mese dell'anno in ordine:

```
int month_days[] = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
```
___
Oltre agli *array* a una dimensione, esistono quelli che si definiscono "***array* multidimensionali**", ossia sostanzialmente degli *array* in cui gli elementi sono altri *array*; ad esempio, un *array* bidimensionale è un *array* di *array* di elementi.

Dichiarare un *array* multidimensionale segue lo stesso procedimento di quelli a una dimensione. Per implementare, per esempio, un *array* contenente 4 *array*, ognuno dei quali destinato a contenere 5 interi, sarà necessario il seguente codice:

```
int twoD[][] = new int[4][5];
```

Concettualmente, tale *array* bidimensionale può essere rappresentato nel modo seguente:

![[array2d_example.png]]

Nella dichiarazione di un *array* multidimensionale, è necessaria solo la lunghezza dell'*array* più "esterno", ossia di quello che conterrà tutti gli altri. Non specificare a priori la lunghezza degli *array* contenuti, come abbiamo invece fatto nell'esempio precedente, può risultare utile in situazioni in cui tali *array* debbano essere di lunghezze diverse. Infatti, seppur sia possibile implementare lo stesso *array* bidimensionale dell'esempio con il seguente codice:

```
int twoD[][] = new int[4][];
twoD[0] = new int[5];
twoD[1] = new int[5];
twoD[2] = new int[5];
twoD[3] = new int[5];
```

è possibile anche creare una situazione del genere:

```
int twoD[][] = new int[4][];
twoD[0] = new int[1];
twoD[1] = new int[2];
twoD[2] = new int[3];
twoD[3] = new int[4];
```

ossia un *array* composto da 4 *array*, composti a loro volta rispettivamente da 1, 2, 3 e 4 interi.

È possibile, inoltre, utilizzare un *array initializer* anche per *array* multidimensionali; basterà inizializzare ognuno degli *array* interni con le proprie parentesi graffe, come nel seguente esempio:

```
int twoD[][] = {
	{0, 0, 0, 0},
	{0, 1, 2, 3},
	{0, 2, 4, 6},
	{0, 3, 6, 9}
};
```
