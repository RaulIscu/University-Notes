Le **stringhe**, appartenenti alla classe **`String`**, rappresentano un elemento particolare all'interno di Java, oltre a rappresentare probabilmente il tipo di elemento più utilizzato nella programmazione in questo linguaggio.

Si discosta dai [[Tipi primitivi|tipi primitivi]] visti in precedenza, partendo dal fatto che ogni stringa che viene creata è, in realtà, un **oggetto** vero e proprio, un'istanza della classe `String`. Inoltre, è importante ricordare che, in Java, **le stringhe sono immutabili**: insomma, una volta che un oggetto di tipo `String` viene creato, non è possibile modificarlo in maniera convenzionale. Ciò, tuttavia, non rappresenta un grande problema, in quanto:
- all'evenienza, se serve "modificare" o cambiare una stringa, è sempre possibile crearne una nuova che soddisfi le proprie necessità;
- oltre alla classe `String`, Java offre delle classi come `StringBuffer` o `StringBuilder`, che permettono in qualche modo di modificare delle stringhe.
___
Una stringa può essere definita in vari modi, di cui il più semplice è probabilmente il seguente:

```
String nomeDellaVariabile = "testo";
```

È possibile, inoltre, concatenare varie stringhe in maniera immediata utilizzando l'operatore **`+`**.

La classe `String` contiene diversi metodi utili per lavorare con oggetti di questo tipo, tra cui:
- **`equals(stringaDaConfrontare)`**, che viene utilizzato per confrontare l'uguaglianza tra la stringa su cui viene invocato il metodo e quella presa in *input*;
- **`length()`**, che viene utilizzato per ottenere la lunghezza della stringa su cui viene invocato;
- **`charAt(indice)`**, che viene utilizzato per ottenere il carattere situato a un determinato indice della stringa.