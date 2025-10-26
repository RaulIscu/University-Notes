## Come formulare un "buon" schema di database?

Supponiamo di voler creare un database contenente alcuni dati riguardo a degli studenti universitari. Più nello specifico, si vogliono memorizzare:
- i dati identificativi di ogni studente (nome, cognome, data di nascita, città e provincia di nascita, matricola e "tax code");
- i dati curriculari relativi a ogni esame effettuato dagli studenti (codice, titolo e professore del corso, voto dell'esame e data).

Un primo approccio, forse il più semplice, può essere di formulare **un solo schema di relazione** che contempli l'interezza dei dati appena esposti. Nel nostro caso, ciò risulterebbe in uno schema di relazione del genere:
$$\text{Curriculum(Matr, Name, Surname, TC, Birth, City, Prov, C\#, Title, Prof, Date, Grade)}$$
Concretamente, tale schema potrebbe presentare un'istanza del genere:

| Matr | Name  | Surname | TC  | Birth | City  | Prov | C#  | Title     | Prof     | Date | Grade |
| ---- | ----- | ------- | --- | ----- | ----- | ---- | --- | --------- | -------- | ---- | ----- |
| 01   | Mario | Rossi   | ... | ...   | Tolfa | Rome | 10  | Physics   | Aiello   | ...  | ...   |
| 02   | Paolo | Bianchi | ... | ...   | Tolfa | Rome | 10  | Physics   | Aiello   | ...  | ...   |
| 01   | Mario | Rossi   | ... | ...   | Tolfa | Rome | 20  | Chemistry | Carlucci | ...  | ...   |

Apparentemente, sembra che lo scopo desiderato sia effettivamente raggiunto. Tuttavia, possiamo notare diversi **problemi**, soprattutto legati alla **ridondanza**: ad esempio, i dati biografici di ciascuno studente dovranno essere nuovamente registrati ogni volta che esso effettuerà un esame; lo stesso discorso può essere fatto per i dati del corso, che dovranno essere reinseriti per ogni esame. Si tratta di problemi importanti, dato che possono facilmente portare non solo a **spreco di spazio di memoria**, ma anche a varie **anomalie**, legate all'aggiornamento, all'inserimento e all'eliminazione di dati. In particolare:
- l'**anomalia di aggiornamento dei dati** si palesa nel momento in cui, ad esempio, se il professore di un corso cambia l'informazione in questione dovrà essere aggiornata per ogni esame di tale corso che è stato effettuato;
- l'**anomalia di inserimento dei dati** si trova nel fatto che non sarà possibile inserire i dati identificativi di uno studente finché questo non avrà effettuato almeno un esame (un discorso analogo vale per i dati curriculari dei vari corsi);
- l'**anomalia di eliminazione dei dati** si verifica, ad esempio, nel momento in cui un esame è stato effettuato da un solo studente, e dunque l'eliminazione dei dati di tale studente comporterebbe anche l'eliminazione dei dati del corso relativo a tale esame.

Cerchiamo, dunque, di trovare un nuovo approccio alla formulazione di questo database, dividendolo stavolta in **tre schemi di relazione**, come i seguenti:
$$\begin{align} &\text{Student(Matr, Name, Surname, TC, Birth, City, Prov)} \\ &\text{Course(C\#, Title, Prof)} \\ &\text{Exam(Matr, C\#, Date, Grade)} \end{align}$$
A questo punto, la stessa informazione contenuta nell'esempio di istanza precedente potrà essere contenuta nelle tre seguenti tabelle:

| Matr | Name  | Surname | TC  | Birth | City  | Prov |
| ---- | ----- | ------- | --- | ----- | ----- | ---- |
| 01   | Mario | Rossi   | ... | ...   | Tolfa | Rome |
| 02   | Paolo | Bianchi | ... | ...   | Tolfa | Rome |

| C#  | Title     | Prof     |
| --- | --------- | -------- |
| 10  | Physics   | Aiello   |
| 20  | Chemistry | Carlucci |

| Matr | C#  | Date | Grade |
| ---- | --- | ---- | ----- |
| 01   | 10  | ...  | ...   |
| 02   | 10  | ...  | ...   |
| 01   | 20  | ...  | ...   |

Con questa soluzione, abbiamo eliminato i problemi evidenziati prima, tuttavia se ne palesano ancora degli altri:
- l'associazione tra una municipalità e la sua provincia viene ripetuta per ogni studente di tale municipalità (**ridondanza**);
- nell'ipotesi, remota ma possibile, che una municipalità cambi provincia (ad esempio, come conseguenza della creazione di nuove province), si dovrebbero aggiornare molte tuple (**anomalia di aggiornamento**);
- non è possibile memorizzare che una municipalità si trovi in una determinata provincia a meno che non sia registrato almeno uno studente appartenente a tale municipalità (**anomalia di inserimento**);
- se è registrato un solo studente proveniente da una determinata municipalità, l'eliminazione dei suoi dati comporterebbe anche l'eliminazione dei dati relativi a tale municipalità (**anomalia di eliminazione**).

Avendo chiari questi nuovi problemi, proviamo un ulteriore approccio, stavolta con uno schema di database composto da **quattro schemi di relazione**:
$$\begin{align} &\text{Student(Matr, Name, Surname, TC, Birth, City)} \\ &\text{Course(C\#, Title, Prof)} \\ &\text{Exam(Matr, C\#, Date, Grade)} \\ &\text{Municipality(City, Prov)} \end{align}$$
Vediamo, infine, le istanze che potrebbero conservare i dati visti finora considerando, stavolta, quest'ultimo schema di database:

| Matr | Name  | Surname | TC  | Birth | City  |
| ---- | ----- | ------- | --- | ----- | ----- |
| 01   | Mario | Rossi   | ... | ...   | Tolfa |
| 02   | Paolo | Bianchi | ... | ...   | Tolfa |

| C#  | Title     | Prof     |
| --- | --------- | -------- |
| 10  | Physics   | Aiello   |
| 20  | Chemistry | Carlucci |

| Matr | C#  | Date | Grade |
| ---- | --- | ---- | ----- |
| 01   | 10  | ...  | ...   |
| 02   | 10  | ...  | ...   |
| 01   | 20  | ...  | ...   |

| City  | Prov |
| ----- | ---- |
| Tolfa | Rome |

Con questa soluzione, non si verifica più alcuna forma di ridondanza o di altre anomalie; possiamo affermare che lo schema di database formulato è un **"buon" schema di database**. In generale, dunque, **un buon schema di database**, per essere definito tale, **deve essere privo di ridondanze e di qualsiasi forma di anomalia**.

Ma come possiamo progettare uno schema del genere? Per capirlo, torniamo ad analizzare l'esempio visto finora, e notiamo che **i problemi trovati derivano dal fatto che più concetti ben diversi e distinti venivano rappresentati in un'unica relazione**: nel primo approccio che abbiamo utilizzato, in un'unica istanza erano condensate le informazioni relative a studenti, corsi, esami e municipalità; nel secondo, in parte migliore, i problemi derivavano dall'associazione tra studenti e municipalità; infine, nel terzo e ultimo, tutti i concetti rappresentati nel database sono perfettamente isolati e indipendenti uno dall'altro, eliminando ridondanze e anomalie. Dunque, generalmente, la prima regola da seguire per la creazione di un buon schema di database è di **rappresentare entità diverse in relazioni diverse**.

Stabilito ciò, è chiaro che il punto diventa l'identificazione di tali entità, in modo da permettere il loro isolamento. Per fare ciò, tornano utili le **[[BD1_01 - Modello relazionale#Chiavi|chiavi]]**, ossia un attributo o insieme di attributi che permette di determinare le cosiddette "**dipendenze funzionali**", un particolare tipo di **vincolo**. Approfondiremo meglio questo concetto nel paragrafo successivo. 
___
## Dipendenze funzionali

Come abbiamo anticipato nel [[BD1_01 - Modello relazionale#Vincoli di integrità|capitolo precedente]], un componente fondamentale nella progettazione di determinati database è la presenza di **vincoli**, ossia di **condizioni sullo schema di database che devono essere rispettate dai dati delle [[BD1_01 - Modello relazionale#Schemi e istanze di relazioni|istanze]]**. Posti dei vincoli, un database si dice "**legale**" se li rispetta tutti.

All'interno di un DBMS, è solitamente possibile:
- **definire dei vincoli** all'interno di uno schema di database;
- **verificare che un database sia legale**;
- **prevenire l'inserimento di tuple illegali** sulla base di vincoli definiti in precedenza.

Inoltre, tendenzialmente saranno disponibili a priori procedure per **vincoli particolarmente comuni**, come i **vincoli di dominio** (ad esempio, un valore numerico di un attributo deve essere compreso in un determinato intervallo), i **vincoli di contenimento** (ad esempio, un valore di un attributo di una relazione deve necessariamente essere presente anche in un'altra relazione), o i vincoli relativi alle **chiavi** (ad esempio, i valori di un attributo devono essere tutti diversi tra loro). Per altri tipi di vincoli, invece, si dovranno definire delle procedure appropriate. 

Tra i vari vincoli che si possono stabilire su uno schema di database, uno dei più importanti è sicuramente la "dipendenza funzionale". Possiamo definire il concetto di dipendenza funzionale nel modo seguente:

> Dato uno schema di relazione $R$, definiamo "**dipendenza funzionale** su $R$" una coppia ordinata $(X, Y)$ di sottoinsiemi non vuoti di attributi di $R$, e la scriviamo:
> $$X\rightarrow Y$$
> dove $X$ viene detto "**determinante**" e $Y$ viene detto "**dipendente**", e di conseguenza si dice che "**$X$ determina funzionalmente $Y$**" oppure che "**$Y$ è funzionalmente dipendente da $X$**".
>
> Dato uno schema di relazione $R$ e una dipendenza funzionale $X\rightarrow Y$ definita su $R$, diciamo che un'istanza $r$ dello schema $R$ **soddisfa la dipendenza funzionale $X\rightarrow Y$** se vale che:
> $$\forall\, t_{1}, t_{2}\in r\, :\, t_{1}[X]=t_{2}[X]\,\Rightarrow\,t_{1}[Y]=t_{2}[Y]$$
> cioè che, per ogni coppia di tuple $t_{1}, t_{2}$ appartenenti all'istanza $r$, se i valori relativi al sottoinsieme di attributi $X$ delle due tuple sono uguali, allora lo sono anche i valori relativi al sottoinsieme di attributi $Y$.

Ciò detto, si precisa per evitare fraintendimenti che tale condizione va rispettata solo ed esclusivamente nel momento in cui $t_{1}[X]=t_{2}[X]$: se questa premessa viene meno, la dipendenza funzionale in questione è comunque soddisfatta qualsiasi siano i valori di $t_{1}[Y]$ e di $t_{2}[Y]$.

Per comprendere meglio questo concetto, vediamo un esempio. Supponiamo di avere uno schema $R=ABCD$, e di stabilire la dipendenza funzionale $AB\rightarrow C$; a questo punto, analizziamo la seguente istanza $r_{1}$:

| A   | B   | C   | D   |
| --- | --- | --- | --- |
| a1  | b1  | c1  | d1  |
| a1  | b2  | c1  | d2  |
| a1  | b1  | c1  | d3  |

Possiamo affermare che $r_{1}$ soddisfa la dipendenza funzionale $AB\rightarrow C$, dato che, presa una qualsiasi coppia di tuple $t_{1},\,t_{2}$ dalla relazione, ogni volta che $t_{1}[AB]=t_{2}[AB]$ si ha anche che $t_{1}[C]=t_{2}[C]$. Al contrario, la seguente istanza $r_{2}$:

| A   | B   | C   | D   |
| --- | --- | --- | --- |
| a1  | b1  | c1  | d1  |
| a1  | b1  | c2  | d2  |
| a1  | b2  | c1  | d3  |

non soddisfa la dipendenza funzionale $AB\rightarrow C$, dato che c'è almeno una coppia di tuple (ad esempio, la prima e la seconda), per cui tale condizione non è rispettata. Generalmente, dato uno schema $R$ e un insieme $F$ di dipendenze funzionali definite su di esso, **un istanza di $R$ si dice "legale" se soddisfa tutte le dipendenze funzionali contenute in $F$**.
___
## Chiusura di $F$

Capita spesso, dato uno schema $R$ e un insieme $F$ di [[BD1_02 - Progettare un database relazionale#Dipendenze funzionali|dipendenze funzionali]] definite su di esso, che **ogni istanza legale di $R$ soddisfi anche dipendenze funzionali che non sono contenute in $F$**, e che dunque non sarebbe necessario soddisfare per poter essere un'istanza legale.

> Dato uno schema $R$ e un insieme $F$ di dipendenze funzionali definite su di esso, definiamo "**chiusura di $F$**" l'insieme di tutte le dipendenze funzionali che sono soddisfatte da ogni istanza legale di $R$. Simbolicamente, la chiusura di $F$ si rappresenta con:
> $$F^{+}$$
> Banalmente, si ha che $F\subseteq F^{+}$.

##### Una nuova definizione di chiave

Avendo introdotto questo nuovo concetto, possiamo fornire anche una **nuova definizione di [[BD1_01 - Modello relazionale#Chiavi|chiave]]**: infatti, dato uno schema $R$ e un insieme $F$ di dipendenze funzionali, possiamo affermare che un sottoinsieme $K$ di attributi di $R$ è una chiave di $R$ se sono rispettate due condizioni:
- $K\rightarrow R\,\in\,F^{+}$;
- non esiste un sottoinsieme proprio $K'\subseteq K$ tale per cui venga soddisfatta la dipendenza funzionale $K'\rightarrow R$.

Vediamo un esempio. Supponiamo di avere il seguente schema di relazione:
$$\text{Student = Matr, Name, Surname, BirthD}$$
Sappiamo che l'attributo $\text{Matr}$, ossia la matricola di uno studente, funge da suo numero identificativo, e dunque non possono esserci due studenti con la stessa matricola. Ciò vuol dire che una qualsiasi istanza legale di $\text{Student}$ dovrà rispettare la dipendenza funzionale $\text{Matr}\rightarrow \text{Name, Surname, BirthD}$, dato che due studenti con la stessa matricola dovranno necessariamente essere la stessa persona, e dunque avere gli stessi dati. Perciò, si può affermare che $\text{Matr}$ è una chiave di $\text{Student}$.

[07 - slide 24]
___
##### Dipendenze funzionali triviali

> Dato uno schema $R$ e due sottoinsiemi non vuoti $X, Y$ di attributi di $R$, **tali per cui $Y\subseteq X$**, possiamo affermare che **ogni istanza $r$ di $R$ soddisfa la dipendenza funzionale $X\rightarrow Y$**.

Dunque, in generale possiamo dire che dati due sottoinsiemi di attributi $X$ e $Y$, se si ha che $Y$ è un sottoinsieme proprio di $X$, allora la dipendenza funzionale $X\rightarrow Y$ appartiene sicuramente all'insieme $F^{+}$, ossia alla chiusura di $F$. Questo tipo di dipendenze funzionali vengono dette "**dipendenze funzionali triviali**".

Vediamo un esempio concreto che dimostra ciò che è stato appena detto. Supponiamo di avere uno schema $R=ABCD$, con un'istanza $r$ come la seguente:

| A   | B   | C   | D   |
| --- | --- | --- | --- |
| a1  | b1  | c1  | d1  |
| a1  | b2  | c1  | d2  |
| a1  | b1  | c1  | d3  |

Consideriamo i due sottoinsiemi di attributi $X = ABC$ e $Y=AB$, che sono tali per cui $Y\subseteq X$: notiamo immediatamente come l'istanza $r$ soddisfi effettivamente la dipendenza funzionale triviale $X\rightarrow Y$.

Possiamo generalizzare il concetto appena esposto rivelando una particolare **proprietà delle dipendenze funzionali**:

> Dato uno schema $R$ e un insieme $F$ di dipendenze funzionali definite su $R$, si ha che:
> $$X\rightarrow Y\,\in\,F^{+}\,\,\iff\,\,\forall\, A\in Y\,:\,X\rightarrow A\,\in\,F^{+}$$
> In altre parole, la dipendenza funzionale $X\rightarrow Y$ è soddisfatta da ogni istanza legale di $R$ se e solo se, per ogni attributo $A$ contenuto nel sottoinsieme $Y$, si verifica che anche la dipendenza funzionale $X\rightarrow A$ è soddisfatta da ogni istanza legale di $R$.
___
##### Come calcolare $F^{+}$

In questo paragrafo, 

[08]
___