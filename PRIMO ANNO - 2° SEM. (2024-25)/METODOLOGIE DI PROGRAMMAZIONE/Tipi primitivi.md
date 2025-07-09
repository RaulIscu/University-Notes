All'interno di Java, vengono definiti 8 **tipi primitivi**, o **tipi semplici**, di dato, che possono essere raggruppati in quattro macro-categorie:
- gli **interi**, che includono `byte`, `short`, `int` e `long`;
- i **numeri a virgola mobile**, che includono `float` e `double`;
- i **caratteri**, costituiti da `char`, che rappresentano determinati simboli;
- i **booleani**, ossia il tipo `boolean`.

Di seguito, queste macro-categorie verranno analizzate più nel dettaglio.
___
## Gli interi: `byte`, `short`, `int` e `long`

Come anticipato, gli **interi** vengono suddivisi in 4 tipi primitivi: `byte`, `short`, `int` e `long`. Si tratta, in ogni caso, di valori con segno (che possono, quindi, essere positivi o negativi).

Una [[Variabili|variabile]] di tipo **`byte`** è un intero segnato lungo 8 bit, che può quindi rappresentare un qualsiasi intero tra -128 e 127. In genere, questo tipo torna utile quando si lavora con *streams* di dati provenienti da una rete o un *file*, ma ovviamente sono anche utili quando si lavora con dati espressi in binario.

Una variabile di tipo **`short`** è un intero segnato lungo 16 bit, che può quindi rappresentare un qualsiasi intero tra - 32 768 e 32 767.

Una variabile di tipo **`int`**, probabilmente il tipo più comune tra questi, è un intero segnato lungo 32 bit, che può quindi rappresentare un qualsiasi intero tra - 2 147 483 648 e 2 147 483 647. Oltre al loro utilizzo puro di memoria di numeri interi, gli `int` vengono spesso utilizzati per controllare dei cicli, o per indicizzare degli *array*.

Una variabile di tipo **`long`** è un intero segnato lungo 64 bit, che può quindi rappresentare un qualsiasi intero tra - 9 223 372 036 854 775 808 e 9 223 372 036 854 775 807. Ovviamente, un `long` torna utile quando si vogliono conservare numeri molto grandi. Nell'eventuale assegnamento di un valore a una variabile di tipo `long`, tale valore dovrà essere dotato del suffisso `l`.
___
## I reali: `float`, `double`

I **numeri a virgola mobile**, o per semplicità i **numeri reali**, sono utilizzati quando si vuole più precisione rispetto agli interi. I numeri reali, in Java, vengono implementati sfruttando lo standard [[Sistema binario|IEEE 754]], e in base al numero di bit allocati al valore, si distinguono due tipi:
- **`float`**;
- **`double`**.

Un numero reale di tipo **`float`** rappresenta un numero lungo 32 bit (dunque, un numero in *single-precision*). In genere, le variabili di tipo `float` sono utili quando è necessario un numero razionale ma non è importante avere una grandissima precisione nel rappresentarlo. Nell'eventuale assegnamento di un valore a una variabile di tipo `float`, tale valore dovrà essere dotato del suffisso `f`. Invece, un numero reale di tipo **`double`** rappresenta un numero lungo 64 bit (dunque, un numero in *double-precision*). Oltre che per manipolare e conservare numeri particolarmente precisi, il tipo `double` torna come tipo dell'*output* di funzioni come `sin()`, `cos()`, `sqrt()`, ecc. ecc.; paradossalmente, del resto, su alcuni processori moderni, progettati e ottimizzati per calcoli matematici veloci, un `double` risulta essere più veloce di un `float`, pur occupando il doppio dello spazio in memoria.
___
## I caratteri: `char`

I **caratteri**, come facilmente intuibile, contengono i dati necessari (in particolare, il codice *Unicode*) per codificare un determinato simbolo o carattere alfanumerico. Al momento della creazione di Java, una qualsiasi codifica Unicode sfruttava 16 bit, o 2 *byte*, e quindi la stessa misurazione vale anche all'interno di Java.

Una variabile di tipo `char`, dunque, può contenere o la stringa contenente il carattere considerato, o il codice Unicode relativo a tale carattere. Inoltre, una particolarità di questo tipo di dato è che, pur due variabili `char` rappresentando tecnicamente due stringhe, è possibile effettuare delle operazioni aritmetiche su di essi trattandoli come degli interi.
___
## I booleani: `boolean`

Infine, i **booleani**, appartenenti al tipo **`boolean`**, rappresentano valori logici come "vero", ossia **`true`**, e "falso", ossia **`false`**. Tutti gli operatori relazionali (maggiore di, minore di, uguale a, ecc. ecc.) ritornano un booleano come risultato della loro operazione; oltre a ciò, è richiesto che le condizioni su cui si basano le espressioni condizionali risultino in booleani.
___
## Conversioni di tipo

Nel caso in cui si voglia **convertire il tipo di una variabile** in un altro, bisogna farlo in maniera esplicita mediante un'operazione chiamata "***casting***". In forma generale, un *casting* richiede il seguente codice:

```
(tipoDesiderato) variabileDaConvertire;
```

Per esempio, se si dichiarano una variabile *a* di tipo `int` e una variabile *b* di tipo `byte`, e si vuole assegnare a *b* il valore di *a*, si potrà utilizzare il seguente blocco di codice:

```
int a;
byte b;

b = (byte) a;
```

Vediamo ora un esempio più complesso, come il seguente:

```
class Conversion {
	public static void main(String[] args) {
		byte b;
		int i = 257;
		double d = 323.142;

		b = (byte) i;
		i = (int) d;
		b = (byte) d;
	}
}
```

Analizziamo ognuna delle tre conversioni che avvengono in questo blocco di codice. Nella prima, il valore di tipo `int` conservato in *i*, ossia 257, viene trasformato in `byte` in modo da poter essere conservato in *b*; il risultato di questa conversione sarà il resto della divisione di 257 per 256 (ossia il *range* di un `byte`), che è pari a 1. Nella seconda, il valore di tipo `double` conservato in *d*, ossia 323.142, viene trasformato in `int` in modo da poter essere conservato in *i*; il risultato di questa conversione sarà la parte intera di *d*, che è pari a 323. Nella terza, il valore di tipo `double` conservato in *d* viene trasformato in `byte` in modo da poter essere conservato in *b*; il risultato di questa conversione sarà il resto della divisione di 323 (la parte intera di *d*) per 256, che è pari a 67.

Alternativamente, è possibile utilizzare dei metodi *built-in* per effettuare delle **conversioni esplicite** di un valore di un tipo in un altro. Ad esempio, **`Integer.parseInt(a)`** trasforma in `int` il valore *a*, mentre **`Double.parseDouble(a)`** trasforma in `double` il valore *a*.

Certe volte, la conversione di un tipo in un altro avviene in maniera automatica, senza bisogno di *casting*. Ciò accade, ad esempio, quando si lavora con "**tipi compatibili**" in cui il tipo di arrivo è più "grande" del tipo di partenza.

Una conversione di tipo avviene automaticamente anche quando, all'interno di un eventuale operazione aritmetica, il risultato di un'operazione tra due operandi di un certo tipo eccede il *range* di quest'ultimo (in questo caso, si parla piuttosto di "***type promotion***"). È possibile definire delle regole generali che delineano il funzionamento di questo meccanismo:
- in genere, tutti i valori di tipo `byte`, `short` e `char` vengono promossi a `int`;
- se, in un'operazione aritmetica, almeno un operando è di tipo `long`, allora anche il risultato dell'operazione verrà promosso a `long`;
- se, in un'operazione aritmetica, almeno un operando è di tipo `float`, allora anche il risultato dell'operazione verrà promosso a `float`;
- se, in un'operazione aritmetica, almeno un operando è di tipo `double`, allora anche il risultato dell'operazione verrà promosso a `double`.