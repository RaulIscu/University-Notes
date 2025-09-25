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

Ricapitolando, possiamo formalizzare una relazione come una **tabella**, dove **ogni riga rappresenta una singola tupla** e **ogni colonna corrisponde a un componente** della tupla; all'interno di una colonna, si troveranno valori "omogenei", ossia tutti provenienti dallo stesso dominio, quindi possiamo affermare, per certi versi, che una colonna corrisponde a un determinato dominio. La coppia nome-dominio va a creare l'**attributo**, e l'insieme degli attributi di una relazione è detto "**schema**" della relazione, da non confondere con la relazione effettiva che possiamo chiamare "**istanza**" della relazione.

Avendo una relazione $R$, dotata degli attributi $A_{1},\,A_{2},\,\dots,\,A_{k}$, lo schema della relazione viene spesso indicato come:
$$R(A_{1},\,A_{2},\,\dots,\,A_{k})$$
Ad esempio, supponiamo di avere uno schema di relazione `Info_City(City, Region, Population)`; una possibile istanza di relazione potrebbe essere la seguente:

| City   | Region    | Population |
| ------ | --------- | ---------- |
| Roma   | Lazio     | 3 000 000  |
| Milano | Lombardia | 1 500 000  |
| Genova | Liguria   | 800 000    |
| Pisa   | Toscana   | 150 000    |

Lo schema di una relazione è **costante**, e descrive sostanzialmente la **struttura generale** che deve rispettare una tupla appartenente a tale relazione. L'istanza di relazione, invece, contiene dei **valori concreti**, che possono variare. A questo punto, possiamo definire il concetto di "**schema di database relazionale**", che consiste in un **insieme di schemi di relazione**; avendo uno schema di database formato dagli schemi di relazione $R_{1},\,R_{2},\,\dots,\,R_{k}$, definiamo "**database relazionale**" un **insieme di istanze di relazioni $r_{1},\,r_{2},\,\dots,\,r_{k}$**, dove l'istanza di relazione $r_{i}$ rispetta lo schema di relazione $R_{i}$.

Nella definizione di un modello relazionale, le componenti di una relazione sono indicate dai nomi degli attributi, piuttosto che dalla loro posizione nello schema. Ad esempio, tornando alla tabella appena vista, chiamando $t$ la seconda tupla si ha che $t[\text{Region}] = \text{Lombardia}$.

Chiamando $Y$ un sottoinsieme degli attributi di uno schema di relazione $X$ ($Y \subseteq X$), con $t[Y]$ si indica un sottoinsieme dei dati della tupla $t$ che corrisponde agli attributi inclusi in $Y$: questo sottoinsieme viene detto "**restrizione**" della tupla $t$.
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

Nella compilazione di alcune tabelle, può capitare che ci siano dati che, seppur rientrino nel dominio dell'[[BD1_01 - Modello relazionale#Attributi|attributo]] a cui è associata la colonna in questione, assumano dei valori non plausibili o non compatibili con altri dati della tabella. Vediamo, ad esempio, la seguente tabella `Results`:

| Student | Grade | Honor |
| ------- | ----- | ----- |
| 2178309 | 32    |       |
| 2267768 | 30    | Yes   |
| 2168863 | 27    | Yes   |
| 2168863 | 24    |       |

Possiamo notare che, seppur tutti i dati presenti appartengano ai domini giusti, sono presenti delle incongruenze: 
- nella prima riga, il dato inserito nella colonna `Grade` è il valore $32$, tuttavia il voto massimo conseguibile in un esame è $30$;
- nella terza riga, il voto conseguito dallo studente è $27$, dunque non dovrebbe essere applicabile il valore nella colonna `Honor`, in quanto è impossibile ottenere una lode su un voto inferiore a 30;
- nella quarta riga, la matricola dello studente è identica a quella dello studente della riga precedente, il che dovrebbe essere impossibile.

Per prevenire problematiche del genere, si possono introdurre dei "**vincoli di integrità**", ossia delle restrizioni su certi dati (e, quindi, su certi attributi) che devono essere rispettate da ogni istanza di relazione del database. In questo contesto, un'istanza di database relazionale si dice "**corretta**" se **soddisfa tutti i vincoli di integrità associati al suo schema**.

Alcuni vincoli di integrità che si potrebbero inserire nell'esempio precedente, ad esempio, sono i seguenti:
- i valori inseriti nella colonna `Grade` devono essere $\ge 18$ (un voto inferiore significherebbe non passare l'esame) e $\le 30$ (non è ottenibile un voto maggiore);
- in ogni riga della tabella, deve essere vero o che il dato nella colonna `Grade` è uguale a $30$ o che il dato nella colonna `Honor` non sia $\text{Yes}$ (in parole povere, questo vincolo previene che si ottenga una lode senza aver preso $30$);
- i valori inseriti nella colonna `Student` devono essere univoci, e non possono ripetersi.

Questo tipo di vincoli, che valgono su **un dato specifico**, su **un insieme di dati della stessa riga**, o su **un insieme di righe nella stessa tabella**, vengono detti "**vincoli di integrità intra-relazionali**". Supponiamo, però, che abbinata alla tabella `Results` ci sia anche una tabella `Students` come la seguente:

| Matricola | Surname | Name  |
| --------- | ------- | ----- |
| 2178309   | Rossi   | Mario |
| 2168863   | Bianchi | Luca  |

Considerando anche questa seconda tabella, risulta spontaneo introdurre un ulteriore vincolo, ossia che gli studenti che hanno sostenuto l'esame siano effettivamente degli studenti registrati, e dunque che la colonna `Student` della prima tabella contenga solo valori contenuti nella colonna `Matricola` della seconda. Questo tipo di vincoli, che valgono **su un insieme di tabelle**, o **relazioni**, vengono detti "**vincoli di integrità inter-relazionali**".

È possibile individuare diverse categorie di vincoli di integrità, tra cui:
- i **vincoli di dominio**, che impongono delle condizioni sul range di valori accettabili all'interno di un determinato dominio (ad esempio, $\text{Grade} \ge 18 \text{ AND Grade} \le 30$);
- i **vincoli di tupla**, che impongono delle condizioni su più di un valore all'interno della stessa tupla, ad esempio stabilendo una certa correlazione tra alcuni valori (ad esempio, $\text{Grade} = 30\text{ \,OR NOT\, Honor} = \text{Yes}$);
- i **vincoli di unicità**, che impongono che non ci siano duplicati tra valori della stessa colonna;
- i **vincoli tra valori di tuple di relazioni diverse**, che impongono delle condizioni su valori appartenenti a tuple di relazioni diverse (ad esempio, che un valore di `Student` debba essere contenuto nella colonna `Matricola` della tabella `Students`);
- i **vincoli sulle chiavi primarie**,
- i **vincoli di esistenza del valore**,
___
##### Chiavi

[02 - slide 36/46]
___
## Algebra relazionale


___