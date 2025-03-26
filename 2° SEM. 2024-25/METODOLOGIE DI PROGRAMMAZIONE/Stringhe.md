Le **stringhe**, appartenenti alla classe **`String`**, rappresentano un elemento particolare all'interno di Java, oltre a rappresentare probabilmente il tipo di elemento più utilizzato nella programmazione in questo linguaggio.

Si discosta dai [[Tipi primitivi|tipi primitivi]] visti in precedenza, partendo dal fatto che ogni stringa che viene creata è, in realtà, un **oggetto** vero e proprio, un'istanza della classe `String`. Inoltre, è importante ricordare che, in Java, **le stringhe sono immutabili**: insomma, una volta che un oggetto di tipo `String` viene creato, non è possibile modificarlo in maniera convenzionale. Ciò, tuttavia, non rappresenta un grande problema, in quanto:
- all'evenienza, se serve "modificare" o cambiare una stringa, è sempre possibile crearne una nuova che soddisfi le proprie necessità;
- oltre alla classe `String`, Java offre delle classi come `StringBuffer` o `StringBuilder`, che permettono in qualche modo di modificare delle stringhe.

Ad esempio, istanziando un oggetto di tipo `StringBuilder`, è possibile concatenare varie stringhe utilizzando il metodo `append(stringaDaConcatenare)`, e poi convertire il risultato in un oggetto di tipo `String` con il metodo `toString()`:

```
StringBuilder sb = new StringBuilder();
sb.append(s1).append(s2);
String s3 = sb.toString();
```
___
Una stringa può essere definita in vari modi, di cui il più semplice è probabilmente il seguente:

```
String nomeDellaVariabile = "testo";
```

È possibile, inoltre, concatenare varie stringhe in maniera immediata utilizzando l'operatore **`+`**.

La classe `String` contiene diversi metodi utili per lavorare con oggetti di questo tipo, tra cui:
- **`charAt(indice)`**, che viene utilizzato per ottenere il carattere situato a un determinato indice della stringa;
- **`concat(stringaDaConcatenare)`**, che viene utilizzato per concatenare la stringa di partenza con la *stringaDaConcatenare* (funzionalità analoga all'operatore `+`);
- **`endsWith(stringa)`**, che viene utilizzato per verificare se la stringa di partenza finisce con *stringa*;
- **`equals(stringaDaConfrontare)`**, che viene utilizzato per confrontare l'uguaglianza tra la stringa su cui viene invocato il metodo e quella presa in *input* (questo metodo confronta semplicemente se le due stringhe, che possono essere anche oggetti diversi, corrispondono a livello di caratteri, mentre l'operatore `==` confronta il riferimento delle stringhe, dunque restituisce `true` se e solo se si confrontano gli stessi oggetti);
- **`indexOf(carattere)`**, che viene utilizzato per ottenere il primo indice in cui viene trovato *carattere* all'interno della stringa di partenza (restituisce -1 se il carattere non è presente);
- **`indexOf(stringa)`**, che viene utilizzato per ottenere il primo indice di partenza della sottostringa *stringa* all'interno della stringa di partenza (restituisce -1 se il carattere non è presente);
- **`length()`**, che viene utilizzato per ottenere la lunghezza della stringa su cui viene invocato;
- **`replace(old, new)`**, che viene utilizzato per ottenere una nuova stringa a partire da quella di partenza, in cui il carattere o la sottostringa *old* vengono rimpiazzati con il carattere o la sottostringa *new*;
- **`split(separatore)`**, che viene utilizzato per ottenere un *[[Array|array]]* di sottostringhe a partire dalla stringa di partenza, separandola in corrispondenza di ogni occorrenza di *separatore* al suo interno;
- **`startsWith(stringa)`**, che viene utilizzato per verificare se la stringa di partenza comincia con *stringa*;
- **`substring(start, end)`**, che viene utilizzato per ottenere una sottostringa della stringa di partenza, presa dall'indice *start* all'indice *end* di quest'ultima (se non si inserisce il parametro *end*, si otterrà la sottostringa che va da *start* alla fine della stringa di partenza);
- **`toLowerCase()`**, che viene utilizzato per ottenere una nuova stringa corrispondente a quella di partenza tutta minuscola;
- **`toUpperCase()`**, che viene utilizzato per ottenere una nuova stringa corrispondente a quella di partenza tutta maiuscola.
___
[LETTURA DI STRINGHE IN INPUT: 03 Strings, pag.32]