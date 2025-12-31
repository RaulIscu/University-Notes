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
$$\text{Student(Matr, Name, Surname, BirthD)}$$
Sappiamo che l'attributo $\text{Matr}$, ossia la matricola di uno studente, funge da suo numero identificativo, e dunque non possono esserci due studenti con la stessa matricola. Ciò vuol dire che una qualsiasi istanza legale di $\text{Student}$ dovrà rispettare la dipendenza funzionale $\text{Matr}\rightarrow \text{Name, Surname, BirthD}$, dato che due studenti con la stessa matricola dovranno necessariamente essere la stessa persona, e dunque avere gli stessi dati. Perciò, si può affermare che $\text{Matr}$ è una chiave di $\text{Student}$.

Seguendo questa nuova definizione, notiamo che spesso ci potranno essere **più chiavi in una relazione**; il più delle volte, in questo contesto, una di esse verrà scelta come "**chiave primaria**", più importante delle altre e a cui non potrà essere assegnato un [[BD1_01 - Modello relazionale#Valori nulli|valore nullo]].
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
##### Chiusura di un insieme di attributi $X$

> Supponiamo di avere uno schema di relazione $R$, un insieme $F$ di dipendenze funzionali definito su di esso, e un sottoinsieme $X$ di attributi di $R$. Possiamo chiamare "**chiusura di $X$ rispetto a $F$**", simbolicamente indicato come **$X^{+}_{F}$**, l'insieme seguente:
> $$X^{+}_{F}=\{A\,\,|\,\,X\rightarrow A\,\in\,F^{A}\}$$
> ossia l'insieme degli attributi $A$ che sono determinati funzionalmente da $X$ applicando, ove possibile, gli [[BD1_02 - Dipendenze funzionali#Assiomi di Armstrong e regole corollarie|assiomi di Armstrong]].

Ovviamente, si ha a prescindere per riflessività che $X\subseteq X^{+}_{F}$. 

A questo punto, possiamo affermare il seguente **lemma**: 

> Dato uno schema di relazione $R$ e un insieme $F$ di dipendenze funzionali definito su di esso, vale che:
> $$X\rightarrow Y\,\in\,F^{A}\,\,\,\iff\,\,\,Y\subseteq X^{+}$$

L'osservazione appena fatta è dimostrabile riprendendo delle osservazioni fatte qualche paragrafo fa, relativamente alle regole di unione e di decomposizione. Per effettuare questa dimostrazione, scomponiamo la doppia implicazione nelle due implicazioni che la compongono, ossia:
$$X\rightarrow Y\,\in\,F^{A}\,\,\,\Rightarrow\,\,\,Y\subseteq X^{+}$$
$$Y\subseteq X^{+}\,\,\,\Rightarrow\,\,\,X\rightarrow Y\,\in\,F^{A}$$
Per chiarezza, ricordiamo che $Y=A_{1},\,A_{2},\,\dots,\,A_{n}$ è un sottoinsieme di attributi dello schema $R$. La prima proposizione è dimostrata dal fatto che, se vale che $X\rightarrow Y\,\in\,F^{A}$, allora per la regola di decomposizione vale anche che $X\rightarrow A_{i}\,\in\,F^{A}$ per ogni $i$ che va da $1$ ad $n$: ciò comporta che ogni attributo $A_{i}$ appartiene all'insieme $X^{+}$, e dunque che $Y$ è un sottoinsieme di tale insieme. La seconda, invece, è dimostrata dal fatto che, se vale che $Y\subseteq X^{+}$, si ha di conseguenza che $X\rightarrow A_{i}\,\in\,F^{A}$ per ogni $i$ che va da $1$ a $n$, e dunque per la regola di unione vale anche che $X\rightarrow Y\,\in\,F^{A}$.

Il concetto di chiusura di $X$ tornerà particolarmente utile in futuro, quando lavoreremo con la [[BD1_03 - La 3NF e la BCNF|3NF]] e con le chiavi di uno schema di relazione.
___
##### Teorema: $F^{+}=F^{A}$

Arrivati a questo punto, siamo pronti a dimostrare un teorema fondamentale per capire come ottenere con successo l'insieme $F^{+}$. Molto semplicemente, il teorema in questione è il seguente:

> Dato uno schema di relazione $R$ e un insieme $F$ di dipendenze funzionali definito su di esso, vale che:
> $$F^{+}=F^{A}$$

In altre parole, vogliamo dimostrare che **l'insieme di tutte le dipendenze funzionali soddisfatte da ogni istanza legale di $R$ coincide con l'insieme delle dipendenze funzionali generate a partire da $F$ applicando gli assiomi di Armstrong**.

Si tratta di una dimostrazione relativamente complessa, e in quanto tale conviene dividerla in due parti: concretamente, dunque, quello che andremo a fare è dimostrare le due seguenti proposizioni:
$$F^{+}\subseteq F^{A}\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,F^{A}\subseteq F^{+}$$
dato che, **se due insiemi sono entrambi sottoinsiemi uno dell'altro**, vuol dire necessariamente che **tali insiemi sono uguali**.

Partiamo dalla prima, ossia che **$F^{+}\subseteq F^{A}$**. Possiamo dimostrare tale proposizione **per assurdo**, supponendo che possa esistere una dipendenza funzionale $X\rightarrow Y$ tale che appartenga a $F^{+}$ ma non a $F^{A}$. Per dimostrare che ciò porta a una contraddizione, ipotizziamo di avere la seguente istanza $r$ di $R$:

|     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1   | 1   | ... | 1   | 1   | 1   | ... | 1   |
| 1   | 1   | ... | 1   | 0   | 0   | ... | 0   |

dove la prima metà della relazione (ossia le prime quattro colonne) rappresentano $X^{+}$, mentre la seconda metà della relazione (ossia le ultime quattro colonne) rappresentano di conseguenza $R-X^{+}$. L'istanza appena mostrata contiene due [[BD1_01 - Modello relazionale#Domini, tuple e relazioni|tuple]], che sono identiche negli attributi $X^{+}$ ma diverse negli attributi $R-X^{+}$. Per dimostrare che $r$ sia legale, supponiamo per assurdo che non lo sia, e dunque che ci sia almeno una dipendenza $V\rightarrow W\,\in\,F$, che banalmente è contenuta anche in $F^{A}$, che non è soddisfatta da $r$: affermare ciò implica che ci sono almeno due tuple in $r$ che hanno valori uguali per gli attributi di $V$ ma diversi per quelli di $W$. Rapportandoci alla nostra istanza, secondo quanto detto deve necessariamente valere che $V\subseteq X^{+}$ e che $W\cap(R-X^{+})\neq\emptyset$. Dato che $V\subseteq X^{+}$, per il [[BD1_02 - Dipendenze funzionali#Chiusura di un insieme di attributi $X$|lemma della chiusura]] sappiamo che $X\rightarrow V\,\in\,F^{A}$, e di conseguenza per transitività che $X\rightarrow W\,\in\,F^{A}$; valendo quest'ultima proposizione, possiamo affermare sempre per lo stesso lemma anche che $W\subseteq X^{+}$, ma ciò contraddice il fatto che l'intersezione tra $W$ e l'insieme di attributi $R-X^{+}$ sia diversa dall'insieme vuoto. Avendo trovato una contraddizione, abbiamo dimostrato che $r$ è a tutti gli effetti un'istanza legale di $R$.

Avendo dimostrato ciò, possiamo tornare al punto principale della dimostrazione. Supponiamo, dunque, che ci sia una dipendenza $X\rightarrow Y$ che appartiene a $F^{+}$ ma non a $F^{A}$: essendo $r$ un'istanza legale, essa soddisfa tutte le dipendenze contenute in $F^{+}$, e dunque anche $X\rightarrow Y$, e ciò in particolare vuol dire, per definizione di [[BD1_02 - Dipendenze funzionali#Cos'è una dipendenza funzionale?|dipendenza funzionale]], che se due tuple di $r$ sono identiche su $X$ lo devono essere anche su $Y$. Sappiamo, banalmente, che $X\subseteq X^{+}$, dunque guardando la tabella $r$ possiamo affermare tranquillamente che ci sono effettivamente due tuple identiche su $X$; essendo $r$ un'istanza legale, ciò implica che queste due tuple devono essere identiche anche su $Y$, e dato che gli unici attributi che sono identici tra le due tuple sono quelli contenuti in $X^{+}$, si ha necessariamente che $Y\subseteq X^{+}$. Ma siamo arrivati così a una contraddizione: per il lemma della chiusura, se $Y\subseteq X^{+}$, allora vale anche che $X\rightarrow Y\,\in\,F^{A}$, cosa che avevamo escluso per ipotesi. Dunque, abbiamo dimostrato che ogni dipendenza contenuta in $F^{+}$ è contenuta anche in $F^{A}$, o formalmente che $F^{+}\subseteq F^{A}$.

Passiamo ora alla seconda proposizione, ossia che $F^{A}\subseteq F^{+}$. Consideriamo una generica dipendenza funzionale $X\rightarrow Y\,\in\,F^{A}$; possiamo provare **per induzione** che tale dipendenza funzionale appartenga anche a $F^{+}$, considerando nell'induzione il numero $i$ di applicazioni di uno degli assiomi di Armstrong. La **base** della nostra induzione è che $i=0$: in questo caso, la dipendenza funzionale $X\rightarrow Y$ appartiene ad $F$ (non sono stati applicati gli assiomi di Armstrong, quindi $F^{A}=F$), e dunque logicamente appartiene anche a $F^{+}$. A questo punto, procediamo a considerare il **passo induttivo**, ossia $i>0$: per ipotesi, qualsiasi dipendenza funzionale ottenuta da $F$ applicando gli assiomi di Armstrong un numero di volte minore o uguale di $i-1$ appartiene a $F^{+}$, si deve dunque dimostrare che ciò valga anche per $i$. 

Come abbiamo detto, $i$ rappresenta il numero di applicazioni di uno degli assiomi di Armstrong: dunque, si dovrà fornire una dimostrazione per ciascuno dei [[BD1_02 - Dipendenze funzionali#Assiomi di Armstrong e regole corollarie|tre assiomi]]. Partiamo con quello di riflessività: consideriamo dunque una dipendenza $X\rightarrow Y$ ottenuta in $F^{A}$ applicando la riflessività, e dunque avendo che $Y\subseteq X$; supponendo di avere un'istanza $r$ di uno schema $R$, con due tuple $t_{1}$ e $t_{2}$, in questa circostanza se vale che $t_{1}[X]=t_{2}[X]$ allora si ha sicuramente anche che $t_{1}[Y]=t_{2}[Y]$ (si tratta di una [[BD1_02 - Dipendenze funzionali#Dipendenze funzionali triviali|dipendenza triviale]]), dunque possiamo affermare che $X\rightarrow Y\,\in\,F^{+}$.

Consideriamo ora l'assioma di aumento: in questo caso, dunque, consideriamo una dipendenza $X\rightarrow Y$ ottenuta in $F^{A}$ applicando l'aumento su una dipendenza $V\rightarrow W\,\in\,F^{A}$, che a sua volta è stata ottenuta applicando ricorsivamente gli assiomi di Armstrong un numero di volte minore o uguale di $i-1$; quest'ultima caratteristica, per ipotesi induttiva, comporta che la dipendenza $V\rightarrow W$ appartenga a $F^{+}$. Applicando l'aumento su di essa, otteniamo la dipendenza $X\rightarrow Y$, dunque possiamo porre $X=VZ$ e $Y=WZ$ per qualche $Z\subseteq R$. Ora, supponendo di avere un'istanza $r$ di uno schema $R$, con due tuple $t_{1}$ e $t_{2}$, in questa circostanza se vale che $t_{1}[X]=t_{2}[X]$, vale trivialmente anche che $t_{1}[V]=t_{2}[V]$ e che $t_{1}[Z]=t_{2}[Z]$; invece, per ipotesi induttiva, da $t_{1}[V]=t_{2}[V]$ deriviamo che $t_{1}[W]=t_{2}[W]$, e dunque possiamo affermare anche che $t_{1}[Y]=t_{2}[Y]$. Possiamo quindi affermare che $X\rightarrow Y\,\in\,F^{+}$.

Infine, è il turno dell'assioma di transitività: in questo caso, consideriamo una dipendenza $X\rightarrow Y$ ottenuta in $F^{A}$ applicando la transitività su due dipendenze $X\rightarrow Z$ e $Z\rightarrow Y$ appartenenti a $F^{A}$, che a loro volta sono state ottenute applicando ricorsivamente gli assiomi di Armstrong un numero di volte minore o uguale di $i-1$; quest'ultima caratteristica, per ipotesi induttiva, comporta che le due dipendenze $X\rightarrow Z$ e $Z\rightarrow Y$ appartengano a $F^{+}$. Ora, supponendo di avere un'istanza $r$ di uno schema $R$, con due tuple $t_{1}$ e $t_{2}$, in questa circostanza se vale che $t_{1}[X]=t_{2}[X]$, allora per ipotesi induttiva vale anche che $t_{1}[Z]=t_{2}[Z]$, e di conseguenza abbiamo che $t_{1}[Y]=t_{2}[Y]$. Perciò, si può affermare che $X\rightarrow Y\,\in\,F^{+}$.

Avendo dimostrato per induzione che qualsiasi dipendenza ottenuta applicando gli assiomi di Armstrong appartiene anche a $F^{+}$, abbiamo dimostrato che $F^{A}\subseteq F^{+}$. 
___
##### Conclusioni

Avendo dimostrato il teorema del [[BD1_02 - Dipendenze funzionali#Teorema $F {+}=F {A}$|paragrafo precedente]], ora abbiamo un modo per **trovare tutte le dipendenze funzionali contenute in $F^+$**: infatti, per fare ciò basterà applicare ricorsivamente gli assiomi di Armstrong (e le regole derivate) sulle dipendenze già definite in $F$, e continuare finché se ne potranno ottenere di nuove. Ciononostante, computare l'insieme $F^{+}$ rimane un'operazione lunga e dispendiosa, richiedente un **costo esponenziale in termini di operazioni svolte**.

Ma se è così inefficiente trovare l'insieme di dipendenze funzionali $F^{+}$, **perché dovremmo volerlo calcolare?** L'importanza maggiore di tale insieme sta nel suo ruolo nella **definizione della [[BD1_03 - La 3NF e la BCNF|3NF]]**, dato che, se si vuole ottenere uno schema in 3NF da uno schema che non lo è, l'approccio generalmente utilizzato sarà quello di scomporlo e, nel fare ciò, si dovrà cercare di **preservare l'insieme $F^{+}$ dello schema originale**.
___