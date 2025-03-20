Un ***array*** è una collezione indicizzata di elementi dello stesso [[Tipi primitivi|tipo]]. Si può creare un *array* per oggetti di sostanzialmente qualsiasi tipo, e un *array* può avere una o più dimensioni.
___
L'*array* più basilare è un ***array* a una dimensione**, che consiste in una semplice lista di elementi dello stesso tipo. Genericamente, per dichiarare un *array* a una dimensione si utilizza il seguente codice:

```
tipo nomeDellArray[lunghezza];
```

dove *tipo* indica il tipo degli elementi contenuti nell'*array*: l'*array* in questione, dunque, potrà contenere solo elementi del tipo specificato. Tuttavia, nonostante con questo codice venga dichiarata una variabile *array*, non ne viene effettivamente creato uno; per creare un nuovo, concreto, *array* di elementi, bisogna istanziarlo usando la parola chiave **`new`**, similmente a come si fa quando si istanziano nuovi oggetti. Ad esempio:

```
nomeDell'Array = new tipo[lunghezza];
```

Con *lunghezza* si intende la dimensione dell'*array* che si sta creando, ossia