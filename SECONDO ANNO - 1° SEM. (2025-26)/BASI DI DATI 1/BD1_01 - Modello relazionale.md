## Cos'è il modello relazionale?

La maggioranza dei database degni di nota al giorno d'oggi implementa, in qualche modo, una forma di "**modello relazionale**". Questo modello è stato proposto per la prima volta da **E. F. Codd** nel **1970**, e già nel **1981** è stato reso disponibile e largamente utilizzato in **DBMS** (Database Management Systems) reali.

Il modello relazionale, come suggerisce il nome, si basa sulla nozione matematica di "**relazione**": questa scelta risulta molto comoda e intuitiva, soprattutto per la stretta vicinanza del concetto di relazione con le tabelle. All'interno di un database relazionale, tutto è rappresentato utilizzando **valori concreti**, che costituiscono sia i **dati** effettivi sia i **collegamenti** e le **associazioni** tra diversi insiemi di dati.

##### Domini, tuple e relazioni

Per comprendere meglio il concetto di "modello relazionale", occorrerà introdurre alcuni **concetti fondamentali**, a partire da quello di "dominio". Possiamo definire **dominio** un qualsiasi **insieme di valori**, finito o infinito che sia. Alcuni esempi di dominio possono essere:
- l'insieme dei numeri interi;
- l'insieme dei numeri decimali;
- l'insieme delle stringhe di testo lunghe 20 caratteri;
- l'insieme $\{0, 1\}$.

Supponiamo, a questo punto, di avere $k$ domini non necessariamente distinti $D_{1},\, D_{2},\, \dots,\, D_{k}$. Definiamo "**prodotto cartesiano**" di questi $k$ domini l'operazione:
$$D_{1} \times D_{2} \times \dots \times D_{k}$$
che ha come risultato il seguente insieme:
$$\{(v_{1},\,v_{2},\,\dots,\,v_{k})\,\,|\,\,v_{1} \in D_{1},\,v_{2} \in D_{2},\,\dots,\,v_{k} \in D_{k}\}$$
ossia un insieme di elementi detti "**tuple**", o anche "**$k$-uple**" (dove $k$ rappresenta il numero di elementi contenuti nella tupla). Come possiamo notare, concretamente una tupla consiste in un **insieme ordinato di $k$ elementi**, dove $k$ è pari al **numero di domini** su cui viene operato il prodotto cartesiano che l'ha generata, e per "ordinato" si intende che il primo valore della tupla proviene sempre dal primo dominio del prodotto cartesiano, il secondo valore dal secondo dominio, e così via. Per indicare un singolo dato all'interno di una tupla $t$, possiamo utilizzare la dicitura $t[i]$ oppure $t.i$, dove $i$ è l'indice di tale dato all'interno della sua tupla. L'insieme risultante da un prodotto cartesiano conterrà un **numero di tuple pari alla moltiplicazione tra le cardinalità dei domini considerati** da esso.

A questo punto, introduciamo il concetto di "**relazione**", che consiste in un **qualsiasi sottoinsieme di un prodotto cartesiano**, dunque dell'insieme di tuple generato da esso. Una relazione in un prodotto cartesiano di $k$ domini è detto "**di grado $k$**", e il numero di tuple contenute in una determinata relazione rappresenta la sua **cardinalità**. Inoltre, **tutte le tuple contenute in una relazione sono necessariamente distinte**.

Per comprendere meglio i concetti appena introdotti, e come essi vadano a intrecciarsi tra loro, analizziamo un semplice esempio concreto. Supponiamo di avere $2$ domini, ossia:
$$D_{1} = \{A, B\}\,\,\,\,\,\,\,\,\,\,D_{2} = \{0, 1, 2\}$$
Il prodotto cartesiano tra questi due domini risulta nel seguente insieme:
$$D_{1} \times D_{2} = \{(A,\,0),\,(A,\,1),\,(A,\,2),\,(B,\,0),\,(B,\,1),\,(B,\,2)\}$$
Una possibile relazione, all'interno di questo insieme, potrebbe essere $\{(A,\,0),\,(B,\,0),\,(B,\,2)\}$: si tratta di una relazione di grado $2$ (deriva da un prodotto cartesiano tra $2$ domini), con cardinalità pari a $3$ (contiene $3$ tuple), e che contiene le tuple $(A, 0)$, $(B, 0)$ e $(B, 2)$.

Tendenzialmente, nel corso si useranno **domini comuni** e **facilmente ricollegabili alla programmazione**. Ad esempio, di seguito una relazione contenente due $4$-uple composte da due stringhe di testo, un intero e un numero reale:

|       |         |     |      |
| ----- | ------- |:--- | ---- |
| Paolo | Rossi   | 2   | 26.5 |
| Mario | Bianchi | 10  | 28.7 |
___
##### Attributi

A questo punto, però, dobbiamo capire come interpretare i dati che abbiamo. Nel modello relazionale, ciò che viene fatto è innanzitutto **assegnare un nome alla tabella**, che indichi che tipo di entità viene rappresentato da ciascuna tupla della stessa. Per chiarire il significato dei singoli dati, poi, si va ad **assegnare a ogni colonna della tabella delle "intestazioni"**, dei nomi che indicano cosa rappresenta il dato della colonna a cui appartengono. Una singola intestazione ($A$), insieme al dominio da cui provengono i dati della sua colonna ($dom(A)$), definisce un singolo "**attributo**".

A questo punto, possiamo riproporre la tabella di esempio che ha chiuso il [[BD1_01 - Modello relazionale#Domini, tuple e relazioni|paragrafo precedente]] chiamandola **`Student`** e dotandola degli opportuni attributi:

| Name  | Surname | Exams | Avg  |
| ----- | ------- | ----- | ---- |
| Paolo | Rossi   | 2     | 26.5 |
| Mario | Bianchi | 10    | 28.7 |

In questo modo, è facile capire che ogni riga della tabella (e quindi ogni entità) rappresenta un singolo studente, e che le colonne della stessa rappresentano rispettivamente il nome e il cognome dello studente, il numero di esami che ha sostenuto e la media dei voti ottenuti da tali esami.

Avendo introdotto il concetto di attributo, è possibile fornire un'**interpretazione alternativa delle tuple**: esse, infatti, possono essere viste come delle **funzioni definite in $R$**, dove $R$ è un insieme di attributi, che associa ad ogni attributo $A$ un elemento del dominio $dom(A)$. Di conseguenza, data una tupla $t$, possiamo indicare con $t(A)$ l'elemento attribuito all'attributo $A$ dalla tupla-funzione $t$.
___
##### Schemi e istanze di relazioni

[02 - slide 14/20]

Oggetti = tuple, i campi o attributi sono le varie informazioni di una tupla, si dà anche un soggetto alla tabella in sé per chiarire che oggetti stanno venendo registrati nella stessa. Una tabella può essere semplicemente definita come un insieme di tuple "omogenee".
___
##### Valori nulli

È perfettamente possibile, all'interno di una tabella come quelle viste finora, che un'informazione sia **mancante** o **non valida**. Tuttavia, in situazioni del genere, non è possibile evitare di inserire tale informazione, dato che una tupla deve attenersi sempre al suo [[BD1_01 - Modello relazionale#Schemi e istanze di relazioni|schema]] ben definito: per ovviare a questo problema, si utilizzano dei "valori di default", chiamati "**valori nulli**", o **`NULL`**. È possibile, del resto, che per alcuni attributi **non venga contemplata la possibilità di un valore `NULL`**, rendendo così **obbligatorio inserirli**.

Il valore `NULL` è un **valore polimorfico**, nel senso che non appartiene concretamente a nessun dominio, ma può rimpiazzare un qualsiasi valore appartenente a un qualsiasi dominio. 

Per comprendere meglio come si utilizzano i valori nulli, vediamo l'esempio di una tabella `Courses`, come la seguente:

| Course | Title     | Lecturer |
| ------ | --------- | -------- |
| 01     | Math      | NULL     |
| 02     | Chemistry | M. Rossi |

In questo esempio, notiamo che nell'attributo `Lecturer` della prima tupla è stato inserito un `NULL`, il che ci indica che il professore che insegnerà in tale corso non è ancora noto.
___
##### Vincoli di integrità

[02 - slide 31/35]
___