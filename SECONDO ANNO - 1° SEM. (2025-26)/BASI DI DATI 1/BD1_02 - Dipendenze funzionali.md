## Cos'è una dipendenza funzionale?

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

Capita spesso, dato uno schema $R$ e un insieme $F$ di [[BD1_02 - Dipendenze funzionali#Dipendenze funzionali|dipendenze funzionali]] definite su di esso, che **ogni istanza legale di $R$ soddisfi anche dipendenze funzionali che non sono contenute in $F$**, e che dunque non sarebbe necessario soddisfare per poter essere un'istanza legale.

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
## Come calcolare $F^{+}$

In questo paragrafo, capiremo come **calcolare l'insieme $F^{+}$**, ossia la chiusura di $F$ o, in altre parole, l'insieme di tutte le dipendenze funzionali soddisfatte da ogni istanza legale di uno schema $R$ su cui è stato definito un insieme $F$ di dipendenze funzionali.

##### Assiomi di Armstrong e regole corollarie

Partiamo definendo un insieme $F^{A}$ di dipendenze funzionali su $R$, tale per cui:
- se $X\rightarrow Y\,\in\,F$, allora $X\rightarrow Y\,\in\,F^{A}$;
- se $Y\subseteq X$, allora $X\rightarrow Y\,\in\,F^{A}$ (definisce l'assioma della "**riflessività**");
- se $X\rightarrow Y\,\in\,F^{A}$, allora anche $XZ\rightarrow YZ\,\in\,F^{A}$ per ogni $Z\in R$ (definisce l'assioma di "**aumento**");
- se $X\rightarrow Y\,\in\,F^{A}$ e $Y\rightarrow Z\,\in\,F^{A}$, allora anche $X\rightarrow Z\,\in\,F^{A}$ (definisce l'assioma della "**transitività**").

Gli assiomi appena presentati vengono chiamati "**assiomi di Armstrong**". A partire da essi, poi, vengono derivate ulteriori **regole**:
- se $X\rightarrow Y\,\in\,F^{A}$ e $X\rightarrow Z\,\in\,F^{A}$, allora anche $X\rightarrow YZ\,\in\,F^{A}$ (regola dell'**unione**);
- se $X\rightarrow Y\,\in\,F^{A}$ e $Z\subseteq Y$, allora anche $X\rightarrow Z\,\in\,F^{A}$ (regola della **decomposizione**);
- se $X\rightarrow Y\,\in\,F^{A}$ e $WY\rightarrow Z\,\in\,F^{A}$, allora anche $WX\rightarrow Z\,\in\,F^{A}$ (regola della **pseudo-transitività**).

Successivamente, vedremo le **dimostrazioni** di ciascuna di queste tre regole. 

Ora, possiamo fare un'osservazione in relazione alle regole dell'unione e della decomposizione: per la regola dell'unione, possiamo affermare che se $X\rightarrow A_{i}\,\in\,F^{A}$ per un certo intervallo di numeri $i$ che va da $1$ a $n$, allora anche $X\rightarrow A_{1}A_{2}\dots A_{n}\,\in\,F^{A}$; allo stesso tempo, per la regola della decomposizione, possiamo affermare che se $X\rightarrow A_{1}A_{2}\dots A_{n}\,\in\,F^{A}$, allora anche $X\rightarrow A_{i}\,\in\,F^{A}$. Essendo entrambe queste proposizioni vere contemporaneamente, possiamo affermare che:
$$X\rightarrow A_{1}A_{2}\dots A_{n}\,\in\,F^{A}\,\,\iff\,\,X\rightarrow A_{i}\,\in\,F^{A}\,\,\,\text{per }i=1,2,\dots,n$$
___
##### Dimostrazione: regola dell'unione

**Dimostriamo la regola dell'unione**, che afferma che:
$$\text{se }\, X\rightarrow Y\,\in\,F^{A}\, \text{ e }\, X\rightarrow Z\,\in\,F^{A},\, \text{ allora anche }\, X\rightarrow YZ\,\in\,F^{A}$$

Se si ha che $X\rightarrow Y\,\in\,F^{A}$, allora per l'assioma dell'aumento si ha che $XX\rightarrow XY\,\in\,F^{A}$, e dato che stiamo lavorando con insiemi sappiamo che l'unione di un insieme con sé stesso corrisponde all'insieme di partenza, dunque possiamo riformulare l'affermazione precedente come $X\rightarrow XY\,\in\,F^{A}$.

Analogamente, se si ha che $X\rightarrow Z\,\in\,F^{A}$, allora per l'assioma dell'aumento si ha anche che $XY\rightarrow YZ\,\in\,F^{A}$. A questo punto, applicando l'assioma della transitività, si può affermare che $X\rightarrow YZ\,\in\,F^{A}$.
___
##### Dimostrazione: regola della decomposizione

**Dimostriamo la regola della decomposizione**, che afferma che:
$$\text{se }\, X\rightarrow Y\,\in\,F^{A}\, \text{ e }\, Z\subseteq Y,\, \text{ allora anche }\, X\rightarrow Z\,\in\,F^{A}$$

Se si ha che $Z\subseteq Y$, allora per l'assioma della riflessività sappiamo che $Y\rightarrow Z\,\in\,F^{A}$; dato che abbiamo che $X\rightarrow Y\,\in\,F^{A}$ e che $Y\rightarrow Z\,\in\,F^{A}$, possiamo affermare che $X\rightarrow Z\,\in\,F^{A}$ per la proprietà della transitività.
___
##### Dimostrazione: regola della pseudo-transitività

**Dimostriamo la regola della pseudo-transitività**, che afferma che:
$$\text{se }\, X\rightarrow Y\,\in\,F^{A}\, \text{ e }\, WY\rightarrow Z\,\in\,F^{A},\, \text{ allora anche }\, WX\rightarrow Z\,\in\,F^{A}$$

Se si ha che $X\rightarrow Y\,\in\,F^{A}$, allora per l'assioma dell'aumento si ha anche che $WX\rightarrow WY\,\in\,F^{A}$; dato che abbiamo che $WX\rightarrow WY\,\in\,F^{A}$ e che $WY\rightarrow Z\,\in\,F^{A}$, possiamo affermare che $WX\rightarrow Z\,\in\,F^{A}$ per la proprietà della transitività.
___

[08 - slide 9]