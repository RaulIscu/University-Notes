## Cos'è una stringa?

Le **stringhe** sono un particolare tipo di dato, rappresentante sostanzialmente una **sequenza di caratteri**. In Java, esse **non appartengono ai [[MDP_07 - Tipi primitivi|tipi primitivi]]**, ma sono a tutti gli effetti degli **[[MDP_02 - Classi#Classi e oggetti|oggetti]]**, definiti dalla classe **`String`**, situata nel package **`java.lang`**.

In Java, **le stringhe sono immutabili**: insomma, una volta che un oggetto di tipo `String` viene creato, non è possibile modificarlo in maniera convenzionale. Ciò, tuttavia, non rappresenta un grande problema, in quanto all'evenienza, se è necessario "modificare" una stringa, è sempre possibile crearne una nuova che soddisfi le proprie necessità a partire da quella iniziale.

Pur essendo un oggetto, una stringa non viene creata utilizzando un costruttore. Per definire una [[MDP_05 - Variabili|variabile]] che vada a contenere una stringa, si scrive un codice del genere:

```
String identificatore = "testo";
```

dove `identificatore` rappresenta, ovviamente, l'identificatore della variabile in questione, e `testo` è la sequenza di caratteri concreta che viene associata alla variabile (nell'inizializzazione di una stringa, il testo della stringa va sempre racchiuso tra virgolette).

A livello interno, la classe `String` memorizza i suoi caratteri in un **[[MDP_14 - Strutture dati#Array|array]] di [[MDP_07 - Tipi primitivi#I caratteri `char`|caratteri]]**, attributo che viene definito come **`final`** e che quindi non può essere modificato una volta inizializzato (per questo motivo una stringa è immutabile).
___
## Metodi principali

Per semplicità, è possibile dividere i **metodi principali** definiti nella classe `String` in tre categorie:
- metodi di **interrogazione e confronto**, che forniscono quindi informazioni sulla stringa in questione o la confrontano con altre stringhe;
- metodi di "**modifica**", che restituiscono nuove stringhe a partire da quella di partenza effettuando delle modifiche;
- metodi di **splitting** e di **parsing**, che dividono una stringa e restituiscono le parti ottenute, o che convertono la stringa in vari modi.

I principali **metodi di interrogazione e confronto** sono i seguenti:
- **`charAt(int index)`**, che restituisce il carattere contenuto nella stringa all'indice `index`;
- **`compareTo(String s)`**, che confronta la stringa in questione e la stringa `s` in base all'ordine alfabetico, e restituisce $0$ se le stringhe risultano uguali, un valore $< 0$ se la stringa in questione viene prima di `s`, e un valore $> 0$ se la stringa in questione viene dopo `s`;
- **`contains(String s)`**, che restituisce `true` se la sottostringa `s` è contenuta all'interno della stringa in questione, e `false` altrimenti;
- **`endsWith(String s)`**, che restituisce `true` se la stringa in questione è terminata dalla sottostringa `s` (in poche parole, se `s` è il suffisso della stringa), e `false` altrimenti;
- **`equals(String s)`**, che restituisce `true` se la sequenza di caratteri contenuta nella stringa in questione è la stessa di quella contenuta in `s`, e `false` altrimenti;
- **`equalsIgnoreCase(String s)`**, che restituisce `true` se la sequenza di caratteri contenuta nella stringa in questione è la stessa di quella contenuta in `s` ignorando la differenza tra lettere maiuscole e minuscole, e `false` altrimenti;
- **`indexOf(String s)`**, che restituisce l'indice corrispondente alla prima occorrenza di `s` all'interno della stringa in questione, e $-1$ se `s` non è trovata al suo interno;
- **`isBlank()`**, che restituisce `true` se la stringa ha lunghezza $0$ o se contiene solo spazi vuoti, e `false` altrimenti;
- **`isEmpty()`**, che restituisce `true` se la stringa ha lunghezza $0$, e `false` altrimenti;
- **`lastIndexOf(String s)`**, che restituisce l'indice corrispondente all'ultima occorrenza di `s` all'interno della stringa in questione, e $-1$ se `s` non è trovata al suo interno;
- **`length()`**, che restituisce la lunghezza della stringa, ossia il numero di caratteri contenuti al suo interno;
- **`startsWith(String s)`**, che restituisce `true` se la stringa in questione è iniziata dalla sottostringa `s` (in poche parole, se `s` è il prefisso della stringa), e `false` altrimenti.

I principali **metodi di "modifica"** sono i seguenti:
- **`concat(String s)`**, che restituisce una stringa risultante dalla concatenazione tra la stringa in questione e `s`;
- **`join(String delimiter, String... strings)`**, che restituisce una stringa risultante dalla concatenazione, in ordine, delle stringhe `strings`, intervallate ogni volta da una copia di `delimiter`;
- **`repeat(int times)`**, che restituisce una stringa costituita dalla ripetizione della stringa di partenza `times` volte;
- **`replace(String old, String new)`**, che restituisce una stringa in cui tutte le occorrenze di `old` sono sostituite da `new`;
- **`substring(int startIndex)`**, che restituisce la sottostringa che parte dall'indice `startIndex` (indice incluso) della stringa in questione;
- **`substring(int startIndex, int endIndex)`**, che restituisce la sottostringa che parte dall'indice `startIndex` (indice incluso) della stringa in questione e termina all'indice `endIndex` (indice escluso) della stessa;
- **`toLowerCase()`**, che restituisce la stringa di partenza ma con tutte le lettere minuscole;
- **`toUpperCase()`**, che restituisce la stringa di partenza ma con tutte le lettere maiuscole;
- **`trim()`**, che restituisce la stringa di partenza ma priva di eventuali spazi vuoti iniziali o finali.

I principali **metodi di splitting e parsing** sono i seguenti:
- **`getBytes()`**, che restituisce un [[MDP_14 - Strutture dati#Array|array]] di [[MDP_07 - Tipi primitivi#Gli interi `byte`, `short`, `int` e `long`|byte]] che corrisponde alla sequenza di caratteri della stringa in questione;
- **`split(String regex)`**, che restituisce un array di stringhe ottenute dividendo la stringa in questione in corrispondenza ad ogni occorrenza di `regex` al suo interno;
- **`toCharArray`**, che restituisce un array di [[MDP_07 - Tipi primitivi#I caratteri `char`|caratteri]] che corrisponde alla sequenza di caratteri della stringa in questione.

È possibile, inoltre, concatenare varie stringhe in maniera immediata utilizzando l'operatore **`+`**.
___
## StringBuilder e StringBuffer

Come abbiamo detto in precedenza, in Java una stringa è derivata da un array immutabile di caratteri, e perciò **non può essere modificata *in-place* una volta creata**; per questa ragione, modifiche e concatenazioni varie sono possibili solo creando ogni volta nuove stringhe, e in certe situazioni ciò può diventare problematico a livello di **memoria** e, quindi, di **prestazioni**.

Per ovviare a questo problema, sono state create le due classi **`StringBuilder`** e **`StringBuffer`**, che possiamo definire in poche parole come delle classi **mutabili** che permettono la manipolazione delle stringhe, evitando quindi di creare innumerevoli oggetti intermedi e potendosi concentrare così su un singolo oggetto. La principale differenza tra le due classi sta nella **gestione dei thread**: in particolare, la classe `StringBuilder` viene usata in contesti ***single-threaded*** e **non sincronizzati**, mentre la classe `StringBuffer` viene usata in contesti ***multi-threaded*** e **sincronizzati**; per loro natura, la prima è più veloce della seconda, ma allo stesso tempo anche meno sicura.

Essendo `StringBuilder` stata progettata a partire da `StringBuffer`, entrambe le classi presentano di fatto gli stessi **metodi principali**, che sono i seguenti:
- **`append(String s)`**, che aggiunge la stringa `s` al termine della stringa in questione;
- **`capacity()`**, che restituisce la "capacità" attuale della stringa, ossia lo spazio attualmente allocato ad essa (se esso viene ecceduto tramite delle operazioni, viene automaticamente ridimensionata);
- **`delete(int startIndex, int endIndex)`**, che rimuove i caratteri della stringa dall'indice `startIndex` (indice incluso) all'indice `endIndex` (indice escluso);
- **`deleteCharAt(int index)`**, che rimuove il carattere della stringa all'indice `index`;
- **`ensureCapacity(int n)`**, che stabilisce la nuova capacità della stringa, rendendola almeno pari a `n`;
- **`insert(int index, String s)`**, che inserisce la stringa `s` all'indice `index` della stringa in questione;
- **`length()`**, che restituisce la lunghezza della stringa, ossia il numero di caratteri contenuti al suo interno;
- **`replace(int startIndex, int endIndex, String s)`**, che sostituisce la sottostringa che parte dall'indice `startIndex` (indice incluso) della stringa in questione e termina all'indice `endIndex` (indice escluso) con la stringa `s`;
- **`reverse()`**, che inverte la stringa in questione.

Oltre ai vantaggi di utilizzo della memoria, l'utilizzo di queste due classi offre alcuni **metodi avanzati** per la manipolazione delle stringhe (come `delete()` o `reverse()`), oltre a maggiore **flessibilità** nella costruzione di **stringhe correlate a file di testo** (.txt, .json, .xml, ecc. ecc.).
___
## Lettura di stringhe come input dal terminale

Le stringhe possono anche essere lette a partire dall'**input dell'utente dal terminale**: per fare ciò, si sfrutta la classe **`Scanner`**, situata nel package **`java.util`** e utilissima per leggere **input** da varie fonti, ad esempio anche da un file o addirittura da un'altra stringa.

Per istanziare uno `Scanner` destinato alla lettura da console, lo si deve costruire nel modo seguente:

```
Scanner sc = new Scanner(System.in);
```

dove **`System.in`** è un oggetto di tipo **`InputStream`** (classe contenuta nel package **`java.io`**) che rappresenta uno **stream di byte di input** ricevuti dall'utente tramite tastiera. A questo punto, se si vuole stampare nel terminale un **messaggio** che indirizzi l'input dell'utente, scriviamo una normalissima istruzione di stampa:

```
System.out.print("Inserisci il tuo nome: ");
```

Ora, per leggere effettivamente qualcosa tramite lo `Scanner`, basterà utilizzare uno dei suoi **metodi**, che leggono l'input e, in base a quale metodo si è scelto, restituiscono comodamente un dato di un certo tipo derivato da tale input. I principali metodi della classe `Scanner` sono i seguenti:
- **`next()`**, che viene utilizzato per leggere una parola (la lettura si ferma al primo spazio vuoto incontrato);
- **`nextBoolean()`**, che viene utilizzato per leggere un valore booleano;
- **`nextDouble()`**, che viene utilizzato per leggere un valore di tipo `double`;
- **`nextFloat()`**, che viene utilizzato per leggere un valore di tipo `float`;
- **`nextInt()`**, che viene utilizzato per leggere un intero di tipo `int`;
- **`nextLine()`**, che viene utilizzato per leggere una stringa fino a un carattere "newline" (**`\n`**), che viene "digitato" dall'utente premendo il tasto di invio;
- **`nextLong()`**, che viene utilizzato per leggere un intero di tipo `long`.

Supponiamo di voler leggere, nel nostro esempio, l'intera stringa prima del newline inserita dall'utente. In questo caso, dovremo scrivere il seguente codice:

```
String nome = sc.nextLine();
```

A questo punto, se volessimo chiedere un ulteriore input e leggerlo come un `int`, scriveremo il seguente codice:

```
System.out.print("Inserisci la tua età: ");
int eta = sc.nextInt();
```

Sarà possibile leggere quanti input si vorrà, e contenerli in un pari numero di [[MDP_05 - Variabili|variabili]]. Una volta terminata la ricezione di input dall'utente, converrà sempre chiudere lo `Scanner`, utilizzando l'istruzione **`sc.close()`**.
___
