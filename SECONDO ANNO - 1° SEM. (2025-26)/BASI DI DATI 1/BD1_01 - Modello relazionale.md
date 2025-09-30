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
- i **vincoli sulle chiavi primarie**;
- i **vincoli di esistenza del valore**.
___
##### Chiavi

[02 - slide 36/46]
___
## Algebra relazionale

L'**algebra relazionale** fornisce notazioni per specificare "**query**", o "interrogazioni", che vengono usate per ricercare determinati dati tra i contenuti di una tabella. L'utilizzo dell'algebra relazionale facilita la creazione di queste query; del resto, il linguaggio $\text{SQL}$ viene tradotto in notazioni derivate dall'algebra funzionale per processare le query.

Con l'algebra relazionale, possiamo dunque interrogare un qualsiasi database relazionale mediante un linguaggio formale costituito da vari **operatori unari e binari**, che se applicati su una o più istanze di relazione permette di generare una nuova istanza con i dati ricercati. Si tratta, del resto, di un "**linguaggio procedurale**", nel senso che gli operatori vanno applicati nell'esatto ordine descritto per ottenere il risultato desiderato.

In generale, definiamo una forma di "algebra" come una struttura che dispone di **un dominio e di una lista di operatori**: ad esempio, l'algebra aritmetica ha come dominio un insieme di numeri e come operatori la somma, il prodotto, ecc. ecc.; per quanto riguarda l'algebra insiemistica, il dominio sono proprio gli insiemi e gli operatori sono unione, intersezione, e così via. Nell'algebra relazionale, il **dominio** è formato dalle **[[BD1_01 - Modello relazionale#Domini, tuple e relazioni|relazioni]]**, che sono sia gli operandi che i risultati delle varie operazioni; queste **operazioni**, in particolare, sono divisibili in **4 categorie**:
- operazioni di **estrazione da una singola relazione**, come "**proiezione**" e "**selezione**";
- operazioni di **insiemistica**, come **unione**, **intersezione** e **differenza**;
- operazioni di **combinazione delle tuple di due relazioni**, come **prodotto cartesiano** o "**join**";
- operazioni di **rinomina**.

##### Proiezione

L'operazione di "**proiezione**" consiste nella **scelta di un sottoinsieme degli attributi della relazione** considerata; possiamo vederla come una "sezione verticale" della relazione di partenza. Simbolicamente, è rappresentata dal simbolo $\pi$; dunque, possiamo affermare che scrivere:
$$\pi_{A_{1},\,A_{2},\,\dots,\,A_{k}}(R)$$
indica l'operazione di proiezione che estrae le colonne corrispondenti agli attributi $A_{1},\,A_{2},\,\dots,\,A_{k}$ della relazione $R$.

Per comprendere meglio, vediamo un esempio. Supponiamo di avere un'istanza di relazione `Customer`, corrispondente alla seguente tabella:

| Name  | Surname  | Code | Town   |
| ----- | -------- | ---- | ------ |
| Mario | Rossi    | C1   | Roma   |
| Paolo | Bianchi  | C2   | Milano |
| Mario | Esposito | C3   | Roma   |

Eseguendo un'operazione di proiezione mirata ad estrarre le colonne `Name` e `Surname` della tabella ($\pi_{\text{Name,\,Surname}}(\text{Customer})$), si ottiene una lista dei nomi e cognomi dei clienti:

| Name  | Surname  |
| ----- | -------- |
| Mario | Rossi    |
| Paolo | Bianchi  |
| Mario | Esposito |

Si ricordi che il risultato dell'operazione è sempre una relazione, dunque un insieme di tuple distinte, e perciò si dovrà evitare di inserire eventuali tuple duplicate nella relazione risultante; ad esempio, se avessimo effettuato una proiezione solo sul `Name`, la tabella risultante avrebbe contenuto solo 2 righe, una per $\text{Mario}$ e una per $Paolo$.
___
##### Selezione

L'operazione di "**selezione**" consiste nella **scelta di un sottoinsieme delle tuple della relazione** considerata; possiamo vederla come una "sezione orizzontale" della relazione di partenza. Simbolicamente, è rappresentata dal simbolo $\sigma$; dunque, possiamo affermare che scrivere:
$$\sigma_{C}(R)$$
indica l'operazione di selezione che estrae le tuple della relazione $R$ che rispettano la condizione $C$. Tale condizione può essere una qualsiasi espressione booleana composita, i cui termini si trovano in una delle due forme generiche seguenti:
$$A\,\,\theta\,\,B\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,A\,\,\theta\,\,a$$
dove $\theta$ è un qualsiasi operatore di confronto come $=,\,\le,\,>$ e altri, $A$ e $B$ sono attributi che dispongono dello stesso dominio, e $a$ è un elemento appartenente al dominio di $A$.

Per comprendere meglio, vediamo un esempio. Torniamo alla stessa istanza di relazione `Customer` presentata nel [[BD1_01 - Modello relazionale#Proiezione|paragrafo precedente]], corrispondente alla seguente tabella:

| Name  | Surname  | Code | Town   |
| ----- | -------- | ---- | ------ |
| Mario | Rossi    | C1   | Roma   |
| Paolo | Bianchi  | C2   | Milano |
| Mario | Esposito | C3   | Roma   |

Eseguendo un'operazione di selezione mirata ad estrarre le tuple della tabella in cui il valore dell'attributo `Town` corrisponde a $\text{Roma}$ ($\sigma_{\text{Town = Roma}}(\text{Customer})$), si ottiene una relazione formata da due sole tuple:

| Name  | Surname  | Code | Town |
| ----- | -------- | ---- | ---- |
| Mario | Rossi    | C1   | Roma |
| Mario | Esposito | C3   | Roma |

___
##### Unione

L'operazione di "**unione**" consiste nella **creazione di una nuova relazione contenente tutte le tuple contenute in almeno una delle relazioni operande**; funziona allo stesso modo dell'unione insiemistica. Simbolicamente, è rappresentata dal simbolo $\cup$; dunque, possiamo affermare che scrivere:
$$R_{1}\cup R_{2}$$
indica l'operazione di unione tra le relazioni $R_{1}$ e $R_{2}$, che genera una nuova relazione che contiene tutte le tuple contenute o in $R_{1}$, o in $R_{2}$, o in entrambe.

L'unione tra relazioni può essere effettuata solo tra operandi "**union-compatible**": per essere union-compatible, due relazioni devono avere lo **stesso numero di attributi**, e gli **attributi corrispondenti devono derivare dallo stesso dominio**. Si noti, dunque, che non è essenziale che gli attributi delle relazioni abbiano gli stessi nomi, anche se eseguire un'unione su due relazioni che non rispettano quest'ultima condizione non avrebbe molto senso.

Per comprendere meglio, vediamo un esempio. Supponiamo di avere due istanze di relazione `Teachers` e `Admins`, corrispondenti alle seguenti tabelle:

| Surname | Code | Department |
| ------- | ---- | ---------- |
| Rossi   | T1   | Math       |
| Rossi   | T2   | Italian    |
| Bianchi | T3   | Math       |
| Verdi   | T4   | English    |

| Surname  | Code | Department |
| -------- | ---- | ---------- |
| Esposito | A1   | English    |
| Riccio   | A2   | Math       |
| Pierro   | A3   | Italian    |
| Bianchi  | A4   | English    |

Eseguendo un'operazione di unione tra le due tabelle `Teachers` e `Admins` ($\text{Teachers }\cup \text{ Admins}$), si ottiene una nuova tabella `AllStaff`, che contiene tutte le righe presenti in almeno una delle due relazioni operande:

| Surname  | Code | Department |
| -------- | ---- | ---------- |
| Rossi    | T1   | Math       |
| Rossi    | T2   | Italian    |
| Bianchi  | T3   | Math       |
| Verdi    | T4   | English    |
| Esposito | A1   | English    |
| Riccio   | A2   | Math       |
| Pierro   | A3   | Italian    |
| Bianchi  | A4   | English    |

Supponiamo, ora, che nella tabella `Admins` fosse presente anche una colonna `Salary`: l'aggiunta di questo attributo renderebbe le due relazioni non più union-compatible. Dunque, per poter effettuare un'unione su di esse, si dovrà prima effettuare una [[BD1_01 - Modello relazionale#Proiezione|proiezione]] sulla tabella `Admins`, in modo da escludere la colonna `Salary`, e poi unire il risultato di tale operazione con la tabella `Teachers`:
$$\text{Teachers }\cup \pi_{\text{Surname, Code, Department}}(\text{Admins})$$
Un approccio simile dovrà essere utilizzato se le due relazioni da unire presentano lo stesso numero di attributi ma alcuni di essi sono definiti su domini diversi, o ancora se le due relazioni sono effettivamente union-compatible ma alcuni dei loro attributi hanno significati diversi.
___
##### Intersezione

L'operazione di "**intersezione**" consiste nella **creazione di una nuova relazione contenente tutte le tuple contenute sia nella prima che nella seconda relazione operanda**; funziona allo stesso modo dell'intersezione insiemistica. Simbolicamente, è rappresentata dal simbolo $\cap$; dunque, possiamo affermare che scrivere:
$$R_{1}\cap R_{2}$$
indica l'operazione di intersezione tra le relazioni $R_{1}$ e $R_{2}$, che genera una nuova relazione che contiene tutte le tuple contenute sia in $R_{1}$ che in $R_{2}$. È possibile vedere tale operazione anche in funzione di [[BD1_01 - Modello relazionale#Differenza|differenze]], in quanto scrivere $R_{1}\cap R_{2}$ equivale a scrivere $R_{1}-(R_{1}-R_{2})$. Come l'[[BD1_01 - Modello relazionale#Unione|unione]], anche l'intersezione può essere effettuata solo tra operandi **union-compatible**, e anch'essa è un'operazione **commutativa**.

Per comprendere meglio, vediamo une esempio. Supponiamo di avere due istanze di relazione `Students` e `Admins`, corrispondenti alle seguenti tabelle:

| Surname | Code | Department |
| ------- | ---- | ---------- |
| Rossi   | C1   | Math       |
| Rossi   | C2   | Italian    |
| Bianchi | C3   | Math       |
| Verdi   | C4   | English    |

| Surname  | Code | Department |
| -------- | ---- | ---------- |
| Esposito | C5   | Italian    |
| Riccio   | C6   | Math       |
| Pierro   | C7   | English    |
| Bianchi  | C3   | Math       |

Eseguendo un'operazione di intersezione tra le due tabelle `Students` e `Admins` ($\text{Students }\cap \text{ Admins}$), si ottiene una nuova tabella che contiene tutti gli studenti che sono anche amministratori, ossia:

| Surname | Code | Department |
| ------- | ---- | ---------- |
| Bianchi | C3   | Math       |

Similmente a come visto per l'unione, anche per l'intersezione è possibile utilizzare una [[BD1_01 - Modello relazionale#Proiezione|proiezione]] per rendere le relazioni operande union-compatible, selezionando un determinato sottoinsieme di attributi.
___
##### Differenza

L'operazione di "**differenza**" consiste nella **creazione di una nuova relazione contenente tutte le tuple contenute nella prima relazione operanda e non nella seconda**; funziona allo stesso modo della differenza insiemistica. Simbolicamente, è rappresentata dal simbolo $-$; dunque, possiamo affermare che scrivere:
$$R_{1}- R_{2}$$
indica l'operazione di differenza tra le relazioni $R_{1}$ e $R_{2}$, che genera una nuova relazione che contiene tutte le tuple contenute in $R_{1}$ e non in $R_{2}$. Come l'[[BD1_01 - Modello relazionale#Unione|unione]] e l'[[BD1_01 - Modello relazionale#Intersezione|intersezione]], anche la differenza può essere effettuata solo tra operandi **union-compatible**; invece, diversamente dall'unione, **la differenza non è commutativa**.

Per comprendere meglio, vediamo un esempio. Supponiamo di avere le stesse due istanze di relazione `Students` e `Admins` utilizzate nel paragrafo precedente, corrispondenti alle seguenti tabelle:

| Surname | Code | Department |
| ------- | ---- | ---------- |
| Rossi   | C1   | Math       |
| Rossi   | C2   | Italian    |
| Bianchi | C3   | Math       |
| Verdi   | C4   | English    |

| Surname  | Code | Department |
| -------- | ---- | ---------- |
| Esposito | C5   | Italian    |
| Riccio   | C6   | Math       |
| Pierro   | C7   | English    |
| Bianchi  | C3   | Math       |

Come detto poco fa, la differenza non è commutativa: dunque, in base all'ordine degli operandi si otterranno risultati diversi. Ad esempio, effettuare la differenza $\text{Students} - \text{Admins}$ risulta in una nuova relazione che contiene tutti gli studenti che non sono amministratori, ossia:

| Surname | Code | Department |
| ------- | ---- | ---------- |
| Rossi   | C1   | Math       |
| Rossi   | C2   | Italian    |
| Verdi   | C4   | English    |

Invece, effettuando la differenza $\text{Admins}-\text{Students}$ si ottiene una nuova relazione che contiene tutti gli amministratori che non sono studenti, ossia:

| Surname  | Code | Department |
| -------- | ---- | ---------- |
| Esposito | C5   | Italian    |
| Riccio   | C6   | Math       |
| Pierro   | C7   | English    |

Similmente a come visto per l'unione e l'intersezione, anche per la differenza è possibile utilizzare una [[BD1_01 - Modello relazionale#Proiezione|proiezione]] per rendere le relazioni operande union-compatible, selezionando un determinato sottoinsieme di attributi.
___
##### Prodotto cartesiano

Spesso, è necessario recuperare delle informazioni che, all'interno di un database, si trovano divise in più relazioni diverse; per ottenere tali dati, occorrerà combinare il contenuto di più tuple provenienti da relazioni diverse in nuove tuple. Per poter ottenere tale risultato, si utilizza il prodotto cartesiano.

L'operazione di "**prodotto cartesiano**" consiste nella **creazione di una nuova relazione con tuple ottenute combinando tutte le tuple della prima relazione con tutte le tuple della seconda**; funziona allo stesso modo del [[BD1_01 - Modello relazionale#Domini, tuple e relazioni|prodotto cartesiano]] introdotto nel capitolo precedente. Simbolicamente, è rappresentata dal simbolo $\times$; dunque, possiamo affermare che scrivere:
$$R_{1}\times R_{2}$$
indica l'operazione di prodotto cartesiano tra le relazioni $R_{1}$ e $R_{2}$, che genera una nuova relazione che contiene nuove tuple generate combinando quelle di $R_{1}$ con quelle di $R_{2}$.

Per comprendere meglio, vediamo un esempio. Supponiamo di avere due istanze di relazione `Customer` e `Order`, corrispondenti alle seguenti tabelle:

| Surname | C#  | Town   |
| ------- | --- | ------ |
| Rossi   | C1  | Roma   |
| Rossi   | C2  | Milano |
| Bianchi | C3  | Roma   |
| Verdi   | C4  | Roma   |

| O#  | C#  | A#  | N° pieces |
| --- | --- | --- | --------- |
| O1  | C1  | A1  | 100       |
| O2  | C2  | A2  | 200       |
| O3  | C3  | A2  | 150       |
| O4  | C4  | A3  | 200       |
| O1  | C1  | A2  | 200       |

Se volessimo ottenere tutti i clienti con abbinati i loro ordini, dovremmo partire dal prodotto cartesiano $\text{Customer}\times \text{Order}$. Prima di tutto, però, conviene rinominare la colonna `C#` della tabella `Order` in modo da poterla distinguere dalla colonna `C#` della tabella `Customer`: per fare ciò, utilizziamo l'operatore di rinomina $\rho$, in modo da creare una copia della tabella `Order` dove `C#` è rinominato a `CC#`:
$$\text{OrderNew}=\rho_{\text{CC\# <- C\#}}(\text{Order})$$
A questo punto, sarà possibile effettuare il prodotto cartesiano $\text{Customer}\times \text{Order}$ generando una nuova tabella `CustomerAndOrder`:

| Surname | C#  | Town   | O#  | CC# | A#  | N° pieces |
| ------- | --- | ------ | --- | --- | --- | --------- |
| Rossi   | C1  | Roma   | O1  | C1  | A1  | 100       |
| Rossi   | C1  | Roma   | O2  | C2  | A2  | 200       |
| Rossi   | C1  | Roma   | O3  | C3  | A2  | 150       |
| Rossi   | C1  | Roma   | O4  | C4  | A3  | 200       |
| Rossi   | C1  | Roma   | O1  | C1  | A2  | 200       |
| Rossi   | C2  | Milano | O1  | C1  | A1  | 100       |
| Rossi   | C2  | Milano | O2  | C2  | A2  | 200       |
| ...     | ... | ...    | ... | ... | ... | ...       |
| Bianchi | C3  | Roma   | O1  | C1  | A1  | 100       |
| ...     | ... | ...    | ... | ... | ... | ...       |
| Verdi   | C4  | Roma   | O1  | C1  | A1  | 100       |
| ...     | ... | ...    | ... | ... | ... | ...       |

Avendo questa nuova tabella, ricordiamo che il nostro obiettivo è quello di ottenere una lista dei clienti con abbinati i rispettivi ordini. Dunque, effettuiamo un'operazione di [[BD1_01 - Modello relazionale#Selezione|selezione]] che restituisca una nuova tabella, contenente solo le tuple in cui l'attributo `C#` coincide con l'attributo `CC#` ($\sigma_{\text{C\# }=\text{ CC\#}}(\text{Customer}\times \text{OrderNew})$); tale operazione restituisce la seguente relazione:

| Surname | C#  | Town   | O#  | CC# | A#  | N° pieces |
| ------- | --- | ------ | --- | --- | --- | --------- |
| Rossi   | C1  | Roma   | O1  | C1  | A1  | 100       |
| Rossi   | C1  | Roma   | O1  | C1  | A2  | 200       |
| Rossi   | C2  | Milano | O2  | C2  | A2  | 200       |
| Bianchi | C3  | Roma   | O3  | C3  | A2  | 150       |
| Verdi   | C4  | Roma   | O4  | C4  | A3  | 200       |

Possiamo eseguire, in seguito, un'operazione di [[BD1_01 - Modello relazionale#Proiezione|proiezione]] $\pi_{\text{Surname, C\#, Town, O\#, A\#, N° pieces}}(\sigma_{\text{C\# }=\text{ CC\#}}$ $(\text{Customer}\times \text{OrderNew}))$, in modo da eliminare l'attributo `CC#`, che risulta ora superfluo. Eseguire quest'ultima operazione risulta nella seguente relazione:

| Surname | C#  | Town   | O#  | A#  | N° pieces |
| ------- | --- | ------ | --- | --- | --------- |
| Rossi   | C1  | Roma   | O1  | A1  | 100       |
| Rossi   | C1  | Roma   | O1  | A2  | 200       |
| Rossi   | C2  | Milano | O2  | A2  | 200       |
| Bianchi | C3  | Roma   | O3  | A2  | 150       |
| Verdi   | C4  | Roma   | O4  | A3  | 200       |

___
##### Join naturale

L'operazione di "**join naturale**" permette sostanzialmente di ottenere lo stesso risultato ottenuto al termine dell'esempio del [[BD1_01 - Modello relazionale#Prodotto cartesiano|paragrafo precedente]] in un'unica operazione. Simbolicamente, è rappresentata dal simbolo $⋈$; dunque, possiamo affermare che scrivere:
$$R_{1}⋈R_{2}$$
equivale a scrivere: 
$$\pi_{\text{XY}}(\sigma_{\text{C}}(R_{1}\times R_{2}))$$
dove $\text{X}$ rappresenta l'insieme degli attributi di $R_{1}$, ,$\text{Y}$ rappresenta l'insieme degli attributi di $R_{2}$ che non si trovano in $R_{1}$, e $\text{C}$ è una determinata condizione booleana nella forma:
$$R_{1}.A_{1}=R_{2}.A_{1}\,\land\, R_{1}.A_{2}=R_{2}.A_{2}\,\land\,\dots\,\land\,R_{1}.A_{k}=R_{2}.A_{k}$$
Bisogna ricordare che gli attributi confrontati nella condizione $\text{C}$ devono disporre degli stessi nomi. Per comprendere meglio, vediamo un esempio. Per comprendere meglio, vediamo lo stesso esempio del paragrafo precedente, avendo le due tabelle `Customer` e `Order`:

| Surname | C#  | Town   |
| ------- | --- | ------ |
| Rossi   | C1  | Roma   |
| Rossi   | C2  | Milano |
| Bianchi | C3  | Roma   |
| Verdi   | C4  | Roma   |

| O#  | C#  | A#  | N° pieces |
| --- | --- | --- | --------- |
| O1  | C1  | A1  | 100       |
| O2  | C2  | A2  | 200       |
| O3  | C3  | A2  | 150       |
| O4  | C4  | A3  | 200       |
| O1  | C1  | A2  | 200       |

Eseguendo un'operazione di join naturale su queste due istanze ($\text{Customer}⋈\text{Order}$), si genererà una nuova relazione contenente tutti i clienti abbinati ai loro ordini, analoga a quella ottenuta al termine del paragrafo precedente: infatti, essendo `C#` l'unico attributo con lo stesso nome tra le due relazioni, esso sarà l'unico a essere confrontato nella condizione $C$, e ne verrà lasciata una sola istanza nella tabella risultante, eliminando colonne duplicate. Si ottiene, così, sempre la seguente tabella:

| Surname | C#  | Town   | O#  | A#  | N° pieces |
| ------- | --- | ------ | --- | --- | --------- |
| Rossi   | C1  | Roma   | O1  | A1  | 100       |
| Rossi   | C1  | Roma   | O1  | A2  | 200       |
| Rossi   | C2  | Milano | O2  | A2  | 200       |
| Bianchi | C3  | Roma   | O3  | A2  | 150       |
| Verdi   | C4  | Roma   | O4  | A3  | 200       |

Vediamo, ora, un esempio più complesso. Supponiamo di avere, oltre a `Customer` e `Order`, la seguente tabella `Article`:

| A#  | Label | Price |
| --- | ----- | ----- |
| A1  | Plate | 3     |
| A2  | Glass | 2     |
| A3  | Mug   | 4     |

e di voler ottenere, a partire da queste tre tabelle, il nome e la città di provenienza dei clienti che hanno ordinato più di 100 articoli che costino più di $2$€ al pezzo. Innanzitutto, partiamo abbinando ai clienti i loro relativi ordini con un join naturale; a questo punto, abbiniamo a ogni ordine le informazioni relative agli articoli con un altro join naturale. Considerate insieme, le operazioni da svolgere sono $(\text{Customer}⋈\text{Order})⋈\text{Article}$, e risultano nella seguente relazione:

| Surname | C#  | Town   | O#  | A#  | N° pieces | Label | Price |
| ------- | --- | ------ | --- | --- | --------- | ----- | ----- |
| Rossi   | C1  | Roma   | O1  | A1  | 100       | Plate | 3     |
| Rossi   | C1  | Roma   | O1  | A2  | 200       | Glass | 2     |
| Rossi   | C2  | Milano | O2  | A2  | 200       | Glass | 2     |
| Bianchi | C3  | Roma   | O3  | A2  | 150       | Glass | 2     |
| Verdi   | C4  | Roma   | O4  | A3  | 200       | Mug   | 4     |

A questo punto, selezioniamo gli ordini da più di 100 articoli e che costano più di $2$€ al pezzo, mediante un'operazione di [[BD1_01 - Modello relazionale#Selezione|selezione]]. Arriviamo dunque alla seguente tabella, generata dall'operazione $\sigma_{\text{N° pieces }>100\,\land\,\text{Price }>2}$$((\text{Customer}⋈\text{Order})⋈\text{Article})$:

| Surname | C#  | Town | O#  | A#  | N° pieces | Label | Price |
| ------- | --- | ---- | --- | --- | --------- | ----- | ----- |
| Verdi   | C4  | Roma | O4  | A3  | 200       | Mug   | 4     |

A questo punto, per ottenere il nome e la città del cliente che ha effettuato l'ordine desiderato, basterà effettuare una [[BD1_01 - Modello relazionale#Proiezione|proiezione]] per estrarre gli attributi `Surname` e `Town`. Sarebbe stato possibile anche utilizzare un approccio alternativo, per certi versi più efficiente dato che permetterebbe di processare meno dati inutili: invece di effettuare subito i vari join naturali, potremmo filtrare prima la tabella `Order` (selezione per considerare solo gli ordini da più di 100 articoli) e poi la tabella `Article` (proiezione per considerare solo le colonne `A#` e `Price`, seguita da selezione per considerare solo gli articoli con prezzo maggiore di $2$€), ed effettuare in seguito i join nello stesso ordine dell'approccio precedente; infine, si potranno selezionare `Name` e `Town` del cliente in maniera analoga.

Il join naturale presenta alcuni **casi particolari**. Supponiamo, ad esempio, che nell'esempio precedente la tabella `Article` venisse sostituita con la seguente:

| A#  | Label | Price |
| --- | ----- | ----- |
| A1  | Plate | 3     |
| A2  | Glass | 2     |
| A3  | Mug   | 4     |
| A4  | Fork  | 1     |

e che invece di ricercare gli ordini di articoli con prezzo maggiore di $2$€, si vogliano trovare quelli con prezzo minore di $2$€; l'unico articolo che rispetta questo criterio è quello indicato dall'ultima tupla, tuttavia tale articolo non viene mai ordinato, e quindi non esistono ordini che rispettano tale criterio. Generalmente, **un join naturale tra due relazioni che hanno attributi in comune, ma dove quest'ultimi non presentano alcun valore in comune, risultano in relazioni vuote**.

Un altro caso particolare è il seguente: **un join naturale tra due relazioni che non hanno attributi in comune** (con lo stesso nome) **degenera in un [[BD1_01 - Modello relazionale#Prodotto cartesiano|prodotto cartesiano]]**. Naturalmente, la soluzione più immediata in questo contesto è effettuare una rinomina di certi attributi.
___
##### Join $\theta$

Può succedere, in alcuni casi, che attributi con nomi diversi in due relazioni abbiano in realtà lo stesso significato: vediamo, ad esempio, le seguenti due tabelle `Artist` e `Painting`:

| Surname | C#  | Town   |
| ------- | --- | ------ |
| Rossi   | C1  | Roma   |
| Rossi   | C2  | Milano |
| Bianchi | C3  | Roma   |
| Verdi   | C4  | Roma   |

| Title  | C#  | Artist |
| ------ | --- | ------ |
| Title1 | C1  | C1     |
| Title2 | C2  | C3     |
| Title3 | C3  | C1     |
| Title4 | C4  | C2     |
| Title5 | C5  | C4     |
| Title6 | C6  | C2     |

In questo caso, supponendo di voler creare una nuova relazione che abbini gli artisti ai loro rispettivi dipinti, effettuare un [[BD1_01 - Modello relazionale#Join naturale|join naturale]] non porterebbe al risultato sperato, dato che l'attributo con nome in comune tra le due tabelle (ossia `C#`) indica prima un determinato artista e poi un determinato dipinto, e ha dunque un significato diverso in base all'istanza di relazione. Per generare correttamente la nuova relazione, gli attributi da confrontare dovranno invece essere `Artist.C#` e `Painting.Artist`; mentre un'operazione di rinomina potrebbe predisporre il problema per essere risolto con un join naturale, in alternativa è possibile utilizzare il "join $\theta$".

L'operazione di "**join $\theta$**" permette di **generare una nuova relazione contenente solo le tuple di un [[BD1_01 - Modello relazionale#Prodotto cartesiano|prodotto cartesiano]] tra due relazioni che rispettano una certa condizione**, che si presenta nella forma:
$$A\,\theta\,B$$
dove $A$ è un attributo della prima relazione operanda, $B$ è un attributo della seconda, e $\theta$ è un qualsiasi operatore di confronto (come $=$, $<$, $\ge$ o altri); si suppone, naturalmente, che $A$ e $B$ derivino dallo stesso dominio, altrimenti l'operazione di confronto risulterebbe impossibile.

Simbolicamente, è possibile indicare il join $\theta$ con lo stesso simbolo del join naturale, ossia $⋈$, e in questo caso scrivere:
$$R_{1}⋈R_{2}$$
equivale a scrivere:
$$\sigma_{A\,\theta\,B}(R_{1}\times R_{2})$$
___