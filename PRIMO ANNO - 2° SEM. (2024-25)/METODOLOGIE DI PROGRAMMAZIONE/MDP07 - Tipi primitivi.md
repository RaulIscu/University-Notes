All'interno di Java, vengono definiti 8 **tipi primitivi**, o **tipi semplici**, di dato, che possono essere raggruppati in quattro macro-categorie:
- gli **interi**, che includono `byte`, `short`, `int` e `long`;
- i **numeri a virgola mobile**, che includono `float` e `double`;
- i **caratteri**, costituiti da `char`, che rappresentano determinati simboli;
- i **booleani**, ossia il tipo `boolean`.

Di seguito, queste macro-categorie verranno analizzate più nel dettaglio.

## Gli interi: `byte`, `short`, `int` e `long`

Gli **interi** (con segno) vengono suddivisi in 4 tipi primitivi: 
- **`byte`**;
- **`short`**;
- **`int`**;
- **`long`**.

Una variabile di tipo **`byte`** può contenere un intero segnato di **8 bit**, che può quindi rappresentare un qualsiasi intero nell'intervallo **$[-128,\, 127]$**. In genere, questo tipo torna utile quando si lavora con [[MDP12 - Interfacce#Stream|stream]] di dati provenienti dalla rete o da un file, quando si vuole risparmiare memoria nel salvataggio di dati in [[MDP14 - Strutture dati#Array|array]], o quando si lavora con dati espressi in binario.

Una variabile di tipo **`short`** può contenere un intero segnato di **16 bit**, che può quindi rappresentare un qualsiasi intero tra **$[-32\,768,\, 32\,767]$**. Similmente al byte, questo tipo viene spesso utilizzato quando si vuole risparmiare memoria nel salvataggio di dati.

Una variabile di tipo **`int`**, probabilmente il tipo più comune tra questi, può contenere un intero segnato di **32 bit**, che può quindi rappresentare un qualsiasi intero nell'intervallo **$[-2\,147\,483\,648,\, 2\,147\,483\,647]$**. Vengono utilizzati per sostanzialmente qualsiasi mansione, come il classico salvataggio di dati, la generazione e conservazione di ID univoci, lo svolgimento di calcoli, la scansione di cicli mediante contatori o l'indicizzazione di array.

Una variabile di tipo **`long`** può contenere un intero segnato di **64 bit**, che può quindi rappresentare un qualsiasi intero nell'intervallo **$[-9\,223\,372\,036\,854\,775\,808,\, 9\,223\,372\,036\,854\,775\,807]$**. Questo tipo viene utilizzato nell'evenienza in cui sia necessario un intero di grandi dimensioni, ad esempio quando si lavora con grandi contatori, con chiavi hash, con dei timestamp, ecc. ecc. Nell'eventuale assegnamento di un valore a una variabile di tipo `long`, tale valore dovrà essere dotato del suffisso `l`.

Ognuno dei tipi primitivi appena analizzati dispone di una **classe wrapper**, che permette di trattarli sostanzialmente come oggetti. Tali classi sono:
- **`Byte`**;
- **`Short`**;
- **`Integer`**;
- **`Long`**.

Utilizzare un valore tramite la sua classe wrapper è necessario in alcuni contesti (ad esempio, nelle [[MDP14 - Strutture dati#Java Collection Framework|collezioni]]), e utile in altri per la possibilità di sfruttare alcuni metodi come `Integer.parseInt()` o `Long.compare()`.
___
## I reali: `float`, `double`

I **numeri a virgola mobile**, o per semplicità i **numeri reali**, vengono implementati sfruttando lo standard **IEEE 754**, e vengono suddivisi in 2 tipi primitivi:
- **`float`**;
- **`double`**.

Una variabile di tipo **`float`** può contenere un numero codificato dallo standard IEEE 754 in ***single-precision***, quindi sfruttando **32 bit** distribuiti nel modo seguente:
- **1 bit** per il **segno**;
- **8 bit** per l'**esponente**;
- **23 bit** per la **mantissa**.

Un `float` può rappresentare numeri positivi o negativi il cui valore assoluto si trova, all'incirca, nell'intervallo **$[1.4 \cdot 10^{-45}, \, 3.4 \cdot 10^{38}]$**. Nell'assegnamento di un valore a una variabile di tipo `float`, tale valore dovrà essere dotato del suffisso `f`, ad esempio:

```
float pi = 3.1415927f;
```

Una variabile di tipo **`double`** può contenere un numero codificato dallo standard IEEE 754 in ***double-precision***, quindi sfruttando **64 bit** distribuiti nel modo seguente:
- **1 bit** per il **segno**;
- **11 bit** per l'**esponente**;
- **52 bit** per la **mantissa**.

Un `double` può rappresentare numeri positivi o negativi il cui valore assoluto si trova, all'incirca, nell'intervallo $[4.9 \cdot 10^{-324},\, 1.8 \cdot 10^{308}]$. È tendenzialmente più utilizzato rispetto al `float`, sia per la sua maggiore precisione ed estensione, sia per la comodità dell'assenza di suffissi nell'assegnazione di valori.

In generale, per la natura della rappresentazione binaria, **non tutti i numeri decimali sono rappresentati con assoluta precisione** da questi tipi. Perciò, è sostanzialmente proibito confrontare dei valori di tipo `float` o `double` usando operatori come `==`, e si preferisce invece utilizzare un certo margine di tolleranza per fare un'operazione del genere, ad esempio effettuando un controllo sul risultato della sottrazione tra i due valori.

Entrambi i tipi primitivi appena analizzati dispongono di una **classe wrapper**, che permette di trattarli sostanzialmente come oggetti. Tali classi sono:
- **`Float`**;
- **`Double`**.

Utilizzare un valore tramite la sua classe wrapper è necessario in alcuni contesti (ad esempio, nelle [[MDP14 - Strutture dati#Java Collection Framework|collezioni]]), e utile in altri per la possibilità di sfruttare alcuni metodi come `Double.parseDouble()` o `Float.isNan()`. Inoltre, tali classi presentano alcune **costanti** che potrebbero tornare utili nel calcolo matematico, come:
- **`POSITIVE_INFINITY`**, che rappresenta $+\infty$;
- **`NEGATIVE_INFINITY`**, che rappresenta $-\infty$;
- **`NaN`**, che rappresenta un "non-numero".
___
## I caratteri: `char`

I **caratteri**, come facilmente intuibile, contengono i dati necessari per codificare un determinato simbolo o carattere alfanumerico, ossia tendenzialmente il **codice Unicode** relativo a quest'ultimo. Al momento della creazione di Java, una qualsiasi codifica Unicode sfruttava 16 bit, o 2 byte, e quindi la stessa allocazione di memoria è stata conservata per il tipo `char`.

Una variabile di tipo `char`, dunque, può contenere o la **stringa contenente il carattere desiderato**, o un **intero** che verrà interpretato come il codice Unicode di un determinato carattere. Proprio per questa doppia natura delle variabili di tipo `char`, è possibile effettuare su di esse sia operazioni caratteristiche delle stringhe, sia operazioni aritmetiche come con un qualsiasi intero.
___
## I booleani: `boolean`

Infine, i **booleani**, appartenenti al tipo **`boolean`**, rappresentano valori logici come "vero", ossia **`true`**, e "falso", ossia **`false`**.

Tutti gli [[MDP06 - Operatori#Operatori logici|operatori logici]] e gli [[MDP06 - Operatori#Operatori di confronto|operatori di confronto]] ritornano un booleano come risultato della loro operazione.
___
## Conversioni di tipo

E se volessimo convertire variabili di un tipo in variabili di un altro? Ci sono diversi modi per effettuare una **conversione di tipo** in Java, ossia:
- mediante un **casting implicito**;
- mediante un **casting esplicito**;
- mediante una **type promotion**.

Un "**casting implicito**", detto anche "*widening conversion*", avviene in maniera automatica e senza perdita di dati quando si cerca di convertire una variabile di un tipo più "piccolo", o meno preciso, in una di un tipo più "grande", o più preciso. Ad esempio, supponiamo di avere una [[MDP05 - Variabili|variabile]] `num` di tipo `int`, a cui si è assegnato il valore `42`, e di voler memorizzare quello stesso dato in una variabile di tipo `long`, con il seguente codice:

```
int num = 42;
long l = num;
```

Ciò che avviene, in questo caso, è che Java converte automaticamente il dato in questione (nell'esempio, il numero `42`) in un dato di tipo equivalente a quello della variabile di destinazione. Si tratta di una conversione completamente **sicura** e **automatica** proprio perché, passando da un tipo meno preciso a uno più preciso, quest'ultimo potrà sicuramente rappresentare correttamente qualsiasi valore rappresentabile dal primo.

Generalmente, la "**gerarchia**" che definisce l'ordine in cui avviene il casting implicito è la seguente, ordinata dal tipo meno preciso a quello più preciso:
- `byte`;
- `short`;
- `int`;
- `long`;
- `float`;
- `double`.

Un "**casting esplicito**", detto anche "*narrowing conversion*", consiste invece in una **conversione forzata** che avviene quando si cerca di convertire una variabile di un tipo più "grande", o più preciso, in una di un tipo più "piccolo", o meno preciso. Con tutta probabilità, un casting esplicito porterà almeno a una perdita di precisione o a un overflow, ed eventualmente a una perdita di dati; non essendo un'operazione sempre sicura come il casting implicito, essa richiede una sintassi particolare per essere eseguita, del tipo:

```
(tipoDesiderato) variabileDaConvertire;
```

Ad esempio, supponiamo di avere una variabile `d` di tipo `double`, a cui si è assegnato il valore `9.78`, e di voler convertire quel dato in uno di tipo `int`. Per fare ciò, si scriverà il seguente codice:

```
double d = 9.78;
int i = (int) d;
```

Quest'operazione porterà alla trasformazione più ragionevole e che comporti la minor perdita di dati possibile. In questo caso, nella variabile `i` verrà inserito il valore `9`, risultante dal troncamento della parte decimale del valore contenuto in `d`. Vediamo ora un esempio più complesso, come il seguente:

```
byte b;
int i = 257;
double d = 323.142;

b = (byte) i;
i = (int) d;
b = (byte) d;
```

Analizziamo ognuna delle tre conversioni che avvengono in questo blocco di codice:
- nella prima, il valore di tipo `int` conservato in `i`, ossia `257`, viene trasformato in `byte` in modo da poter essere conservato in `b`, e il risultato di questa conversione sarà il resto della divisione di $257$ per $256$ (ossia il range dei valori contenibili in un `byte`), che è pari a 1;
- nella seconda, il valore di tipo `double` conservato in `d`, ossia `323.142`, viene trasformato in `int` in modo da poter essere conservato in `i`; il risultato di questa conversione sarà la parte intera di `d`, che è pari a $323$;
- nella terza, il valore di tipo `double` conservato in `d` viene trasformato in `byte` in modo da poter essere conservato in `b`; il risultato di questa conversione sarà il resto della divisione di $323$ (la parte intera di `d`) per $256$, che è pari a `67`.

Alternativamente, è possibile utilizzare dei metodi built-in per effettuare delle conversioni esplicite di un valore di un tipo in un altro. Ad esempio, **`Integer.parseInt(a)`** trasforma in `int` il valore `a`, mentre **`Double.parseDouble(a)`** trasforma in `double` il valore `a`.

Una "**type promotion**", infine, consiste in una **conversione automatica** di tipo che viene effettuata da Java contestualmente a **operazioni aritmetiche tra dati di tipi diversi**; in questi casi, i tipi di tali dati, così come quello del risultato dell'operazione, vengono promossi a un tipo comune per comodità e uniformità.

È possibile definire delle regole generali che delineano il funzionamento di questo meccanismo:
- in genere, tutti i valori di tipo `byte`, `short` e `char` vengono promossi a `int`;
- se, in un'operazione aritmetica, almeno un operando è di tipo `long`, allora anche il risultato dell'operazione verrà promosso a `long`;
- se, in un'operazione aritmetica, almeno un operando è di tipo `float`, allora anche il risultato dell'operazione verrà promosso a `float`;
- se, in un'operazione aritmetica, almeno un operando è di tipo `double`, allora anche il risultato dell'operazione verrà promosso a `double`.