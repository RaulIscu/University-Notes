Per approfondire e comprendere al meglio la sintassi di Java, analizziamo un programma di base scritto in tale linguaggio. Di seguito, il codice che permette di stampare la classica frase "*Hello, World!*":

```
public class helloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

Analizziamo gradualmente questo codice. Notiamo, innanzitutto, che la primissima cosa da fare è **creare una** **[[Classi|classe]]**. Ciò risulta fondamentale, in quanto tutto il codice di un qualsiasi *file* `.java` deve essere contenuto in una classe. È convenzione, inoltre, denominare il *file* in maniera identica alla classe principale contenuta al suo interno; in questo caso, ad esempio, il *file* contenente il codice sopra esposto dovrà chiamarsi `helloWorld.java`.

La parola chiave `public`, così come la sua controparte `private` (non presente nel codice d'esempio), indica se ciò che viene definito è accessibile o meno al di fuori della classe di appartenenza. In questo caso, essendo la classe pubblica, i suoi metodi e le sue variabili saranno accessibili anche da metodi definiti al di fuori della classe stessa.

Quello che viene definito il "**corpo**" della classe, ossia il codice e i dati contenuti al suo interno, viene delimitato da parentesi graffe (`{}`).

Passando alla seconda riga, si assiste alla definizione di un **metodo**, in particolare di un metodo pubblico (`public`), statico (`static`), che non ritorna nessun valore (`void`). In particolare, definire "statico" un metodo o un attributo significa renderlo unico e appartenente alla classe in sé piuttosto che alle singole istanze della classe: ciò vuol dire che, concretamente, esisterà una sola istanza del membro della classe, e tutti gli oggetti appartenenti a tale classe lo condivideranno.

Il metodo definito è un metodo **`main()`**, molto importante in quanto **ogni programma scritto in Java deve contenere un metodo che si chiama `main`**. Come per buona parte dei linguaggi di programmazione, il nome dei metodi (o, in altre parole, delle funzioni) è sempre seguito da parentesi tonde (`()`), al cui interno è possibile specificare, al momento della definizione, il tipo specifico di *input* previso per tale metodo: in questo caso, ad esempio, il metodo dovrà ricevere in *input* valori di tipo `String`.

All'interno del corpo del metodo `main`, poi, troviamo un'**istruzione**, ossia l'azione che verrà eseguita alla chiamata del metodo in questione. In Java, ogni istruzione deve essere terminata con un punto e virgola (`;`). In questo caso, il metodo `main()` porterà alla stampa, nella *console*, della frase "*Hello, World!*" (in particolare, il metodo specifico `System.out.println()` porterà alla stampa del testo seguito da un accapo).
___
Prescindendo un po' dall'esempio precedente, esplicitiamo altre caratteristiche e regole di Java importanti da ricordare per scrivere un programma formalmente corretto.

Java è un linguaggio *free-form*, e in quanto tale **non necessita di alcun tipo di indentazione**: questa, infatti, viene inserita puramente per scopi di leggibilità. Potenzialmente, dunque, un programma Java potrebbe essere anche scritto in una sola riga di codice, a patto però che siano presente gli opportuni spazi vuoti come separatori tra le varie parti del codice.

Gli **identificatori**, ossia semplicemente i nomi appartenenti a un oggetto, una classe, o a qualsiasi altro elemento di un programma, possono essere una qualsiasi sequenza di lettere (maiuscole e minuscole), numeri e simboli scelti tra *underscore* (`_`) e segno del dollaro (`$`), anche se quest'ultimo va usato solo in contesti specifici. Un identificatore non può iniziare con un numero; è, inoltre, importante ricordare che Java è un linguaggio ***case-sensitive***, dunque scrivere, ad esempio, scrivere `example` o `Example` porta a due elementi diversi. Infine, convenzionalmente gli identificatori di metodi devono rispettare la convenzione del "***camel case***": se composto da più parole, esse dovranno avere tutte l'iniziale maiuscola tranne la prima, che l'avrà minuscola.

Per inserire dei **commenti**, ossia del testo all'interno del codice che però non viene effettivamente utilizzato, si distinguono tre casi:
- per inserire una sola riga di commento, si deve iniziare la riga con `//`;
- per inserire un commento multi-riga, si inizia con `/*` e si finisce con `*/`;
- per inserire un "*documentation comment*", ossia un commento che viene sfruttato per generare un *file* di documentazione in formato HTML, si inizia con `/**` e si finisce con `*/`.

Ci sono poi, vari **separatori**, che vengono usati in diversi contesti per vari scopi, i principali dei quali sono:
- le **parentesi tonde** (`()`), utilizzate per contenere i vari parametri di un metodo, per definire precedenze in operazioni complesse e per contenere delle condizioni nei controlli;
- le **parentesi quadre** (`[]`), utilizzate spesso in relazione ad *array*;
- le **parentesi graffe** (`{}`), utilizzate principalmente per contenere e delimitare blocchi di codice;
- il **punto e virgola** (`;`), utilizzato per terminare una qualsiasi istruzione;
- la **virgola** (`,`), utilizzata per separare identificatori consecutivi nella dichiarazione di una variabile, e per separare le condizioni all'interno di un ciclo *for*;
- il **punto** (`.`), utilizzato per separare una variabile o un metodo dalla variabile di riferimento, o pacchetti da classi e sotto-pacchetti.