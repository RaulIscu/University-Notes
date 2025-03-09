Per approfondire e comprendere al meglio la sintassi di Java, analizziamo un programma di base scritto in tale linguaggio. Di seguito, il codice che permette di stampare la classica frase "*Hello, World!*":

```
public class helloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

Analizziamo gradualmente questo codice. Notiamo, innanzitutto, che la primissima cosa da fare è **creare una classe**. Ciò risulta fondamentale, in quanto tutto il codice di un qualsiasi *file* `.java` deve essere contenuto in una classe. È convenzione, inoltre, denominare il *file* in maniera identica alla classe principale contenuta al suo interno; in questo caso, ad esempio, il *file* contenente il codice sopra esposto dovrà chiamarsi `helloWorld.java`.

La parola chiave `public`, così come la sua controparte `private` (non presente nel codice d'esempio), indica se ciò che viene definito è accessibile o meno al di fuori della classe di appartenenza. In questo caso, essendo la classe pubblica, i suoi metodi e le sue variabili saranno accessibili anche da metodi definiti al di fuori della classe stessa.

Quello che viene definito il "**corpo**" della classe, ossia il codice e i dati contenuti al suo interno, viene delimitato da parentesi graffe (`{}`).

Passando alla seconda riga, si assiste alla definizione di un **metodo**, in particolare di un metodo pubblico (`public`), statico (`static`), che non ritorna nessun valore (`void`). In particolare, definire "statico" un metodo significa renderlo unico e appartenente alla classe in sé piuttosto che alle singole istanze della classe: ciò vuol dire che, concretamente, esisterà una sola istanza del metodo, a prescindere da quanti oggetti appartenenti a tale classe vengano creati.

Il metodo definito è un metodo **`main()`**, molto importante in quanto **ogni programma scritto in Java deve contenere un metodo che si chiama `main`**. Come per buona parte dei linguaggi di programmazione, il nome dei metodi (o, in altre parole, delle funzioni) è sempre seguito da parentesi tonde (`()`), al cui interno è possibile specificare, al momento della definizione, il tipo specifico di *input* previso per tale metodo: in questo caso, ad esempio, il metodo dovrà ricevere in *input* valori di tipo `String`.

All'interno del corpo del metodo `main`, poi, troviamo un'**istruzione**, ossia l'azione che verrà eseguita alla chiamata del metodo in questione. In Java, ogni istruzione deve essere terminata con un punto e virgola (`;`). In questo caso, il metodo `main()` porterà alla stampa, nella *console*, della frase "*Hello, World!*" (in particolare, il metodo specifico `System.out.println()` porterà alla stampa del testo seguito da un accapo).