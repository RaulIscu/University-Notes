All'interno di Java, vengono definiti 8 **tipi primitivi**, o **tipi semplici**, di dato, che possono essere raggruppati in quattro macro-categorie:
- gli **interi**, che includono `byte`, `short`, `int` e `long`;
- i **numeri a virgola mobile**, che includono `float` e `double`;
- i **caratteri**, costituiti da `char`, che rappresentano determinati simboli;
- i **booleani**, ossia il tipo `boolean`.

Di seguito, queste macro-categorie verranno analizzate più nel dettaglio.
___
Come anticipato, gli **interi** vengono suddivisi in 4 tipi primitivi: `byte`, `short`, `int` e `long`. Si tratta, in ogni caso, di valori con segno (che possono, quindi, essere positivi o negativi).

Una variabile di tipo **`byte`** è un intero segnato lungo 8 bit, che può quindi rappresentare un qualsiasi intero tra -128 e 127. In genere, questo tipo torna utile quando si lavora con *streams* di dati provenienti da una rete o un *file*, ma ovviamente sono anche utili quando si lavora con dati espressi in binario.

Una variabile di tipo **`short`** è un intero segnato lungo 16 bit, che può quindi rappresentare un qualsiasi intero tra - 32 768 e 32 767.

Una variabile di tipo **`int`**, probabilmente il tipo più comune tra questi, è un intero segnato lungo 32 bit, che può quindi rappresentare un qualsiasi intero tra - 2 147 483 648 e 2 147 483 647. Oltre al loro utilizzo puro di memoria di numeri interi, gli `int` vengono spesso utilizzati per controllare dei cicli, o per indicizzare degli *array*.

Una variabile di tipo **`long`** è un intero segnato lungo 64 bit, che può quindi rappresentare un qualsiasi intero tra - 9 223 372 036 854 775 808 e 9 223 372 036 854 775 807. Ovviamente, un `long` torna utile quando si vogliono conservare numeri molto grandi.
___
I **numeri a virgola mobile**, o per semplicità i **numeri reali**, sono utilizzati quando si vuole più precisione rispetto agli interi. I numeri reali, in Java, vengono implementati sfruttando lo standard [[Sistema binario|IEEE 754]], e in base al numero di bit allocati al valore, si distinguono due tipi:
- **`float`**;
- **`double`**.

Un numero reale di tipo **`float`** rappresenta un numero lungo 32 bit (dunque, un numero in *single-precision*). In genere, le variabili di tipo `float` sono utili quando è necessario un numero razionale ma non è importante avere una grandissima precisione nel rappresentarlo. Invece, un numero reale di tipo **`double`** rappresenta un numero lungo 64 bit (dunque, un numero in *double-precision*). Oltre che per manipolare e conservare numeri particolarmente precisi, il tipo `double` torna come tipo dell'*output* di funzioni come `sin()`, `cos()`, `sqrt()`, ecc. ecc.; paradossalmente, del resto, su alcuni processori moderni, progettati e ottimizzati per calcoli matematici veloci, un `double` risulta essere più veloce di un `float`, pur occupando il doppio dello spazio in memoria.
___
I **caratteri**, come facilmente intuibile, contengono i dati necessari (in particolare, il codice *Unicode*) per codificare un determinato carattere. Al momento della creazione di Java, una qualsiasi codifica Unicode sfruttava 16 bit, o 2 *byte*, e quindi la stessa misurazione vale anche all'interno di Java.

Una variabile di tipo `char`, dunque, può contenere o la stringa contenente il carattere considerato, o il codice Unicode relativo a tale carattere. Inoltre, una particolarità di questo tipo di dato è che, pur due variabili `char` rappresentando tecnicamente due stringhe, è possibile effettuare delle operazioni aritmetiche su di essi trattandoli come degli interi.
___
