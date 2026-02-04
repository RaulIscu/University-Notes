## Correlazione e indipendenza tra 2 eventi

Torniamo all'[[CDP_02 - Probabilità#Formula di Bayes|esempio del lotto di componenti]] presentato alla fine del capitolo precedente. Prima ancora di svolgere qualsiasi calcolo effettivo, si può notare che:
$$\mathbb{P}(H_{1}\,|\,E)<\mathbb{P}(H_{1})\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\mathbb{P}(H_{3}\,|\,E)>\mathbb{P}(H_{3})$$
Da tale osservazione, prendiamo spunto per definire due tipi di **correlazione tra $2$ eventi**.

> Siano $A$ e $B$ due eventi, con $\mathbb{P}(A)>0$ e $\mathbb{P}(B)>0$, tali eventi si dicono "**correlati positivamente**" se vale che:
> $$\mathbb{P}(A\,|\,B)>\mathbb{P(A)}$$
> Tale relazione è equivalente alla seguente:
> $$\mathbb{P}(A\cap B)\,>\,\mathbb{P}(A)\cdot\mathbb{P}(B)$$

> Siano $A$ e $B$ due eventi, con $\mathbb{P}(A)>0$ e $\mathbb{P}(B)>0$, tali eventi si dicono "**correlati negativamente**" se vale che:
> $$\mathbb{P}(A\,|\,B)<\mathbb{P(A)}$$
> Tale relazione è equivalente alla seguente:
> $$\mathbb{P}(A\cap B)\,<\,\mathbb{P}(A)\cdot\mathbb{P}(B)$$

Notiamo che la definizione di correlazione positiva impone che $\mathbb{P}(A\cap B)>\mathbb{P}(A)\cdot\mathbb{P}(B)$, mentre la definizione di correlazione negativa si basa sulla disuguaglianza nel verso opposto, ossia $\mathbb{P}(A\cap B)<\mathbb{P}(A)\cdot\mathbb{P}(B)$. E se i due membri fossero invece perfettamente equivalenti?

> Due eventi $A$ e $B$ si dicono "**stocasticamente indipendenti**" se vale che:
> $$\mathbb{P}(A\cap B)\,=\,\mathbb{P}(A)\cdot\mathbb{P}(B)$$

Si osservi che, in quest'ultima definizione, non viene richiesto necessariamente che $\mathbb{P}(A)>0$ e che $\mathbb{P}(B)>0$; ciononostante, se tali condizioni sono verificate, e $A$ e $B$ risultano essere effettivamente degli eventi stocasticamente indipendenti, allora possiamo anche affermare che:
$$\mathbb{P}(A\,|\,B)=\mathbb{P}(A)\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\mathbb{P}(B\,|\,A)=\mathbb{P}(B)$$
Per comprendere meglio come questi concetti si traducono in fenomeni concreti, vediamo un esempio. Consideriamo un esperimento relativo al lancio di due dadi, che ha dunque come spazio campione $\Omega=\{(i,\,j)\,|\,i,\,j\in\{1,\,2,\,3,\,4,\,5,\,6\}\}$; imponiamo che gli eventi elementari possibili siano equiprobabili, e dunque che in generale $\mathbb{P}(\omega_{i})=\frac{1}{36}$, e denotiamo con $X_{1}$ il risultato dato dal lancio del primo dado e con $X_{2}$ il risultato del lancio del secondo. Ora, considerati gli eventi composti:
$$\begin{align} &E_{1}=\{X_{1}\text{ è pari}\}\\&E_{2}=\{X_{1}+X_{2}\text{ è pari}\}\\&E_{3}=\{X_{1}+X_{2}\le 4\}\\&E_{4}=\{X_{1}\le 2\}\\&E_{5}=\{max(X_{1},\,X_{2})>3\} \end{align}$$
vogliamo verificare le seguenti affermazioni:
- $E_{1}$ e $E_{2}$ sono stocasticamente indipendenti;
- $E_{3}$ e $E_{4}$ sono correlati positivamente;
- $E_{3}$ e $E_{5}$ sono correlati negativamente.

Tutte queste affermazioni possono naturalmente essere verificate calcolando le varie probabilità e verificando le definizioni appena viste, ma per esercizio cerchiamo di convincercene con dei ragionamenti logici: per quanto riguarda la prima affermazione, i due eventi $E_{1}$ ed $E_{2}$ sono indipendenti dato che, qualsiasi sia il risultato del lancio del primo dado, esso non andrà a influenzare effettivamente la parità o disparità della somma $X_{1}+X_{2}$; la seconda affermazione si dimostra pensando alla probabilità che avvenga $E_{3}$ sapendo che avviene $E_{4}$, ossia che la somma tra $X_{1}$ e $X_{2}$ sia minore o uguale a $4$ sapendo che $X_{1}$ è minore o uguale a $2$, e rendendosi conto che quest'ultima informazione rende più probabile l'evento $E_{3}$, dato che in assenza di $E_{4}$ sono possibili più combinazioni di tipo $(X_{1},\,X_{2})$ tali per cui la somma $X_{1}+X_{2}$ è maggiore di $4$; seguendo un ragionamento analogo, $E_{3}$ ed $E_{5}$ sono correlati negativamente perché, sapendo che avviene $E_{5}$ (dunque che uno dei due lanci è risultato in un numero maggiore di $3$), si intuisce subito che l'evento $E_{3}$ diventa molto meno probabile, anzi impossibile considerando che il lancio di un dado può risultare solo in un numero intero compreso tra $1$ e $6$.

Contestualmente al modello del lancio dei due dadi, si verifica immediatamente che assegnare uguale probabilità pari a $\frac{1}{36}$ a tutti gli eventi elementari implica che gli eventi composti del tipo $\{X_{1}=i\}$ o $\{X_{2}=j\}$ sono a loro volta equiprobabili con probabilità pari a $\frac{1}{6}$; inoltre, si intuisce che coppie di eventi del tipo $\{X_{1}=i\},\,\{X_{2}=j\}$ costituiscono eventi stocasticamente indipendenti. Si può anche verificare il tutto nel verso contrario: partendo dalla condizione che $\mathbb{P}(X_{1}=i)=\mathbb{P}(X_{2}=j)=\frac{1}{6}$, e considerando l'indipendenza stocastica tra tutte le coppie di eventi del tipo $\{X_{1}=i\},\,\{X_{2}=j\}$, possiamo ottenere che tutti gli eventi elementari $\{X_{1}=i\}\cap\{X_{2}=j\}$ hanno probabilità uguale a $\frac{1}{36}$. 

Da ciò, possiamo dedurre un fatto generale: **spesso, l'assegnazione di probabilità non avviene imponendo a priori le probabilità degli eventi elementari, ma piuttosto imponendo che certi eventi composti abbiano certe probabilità e imponendo l'indipendenza stocastica tra alcune coppie di eventi**. Possiamo, ad esempio, riformulare il modello del lancio dei due dadi in questo modo. Assumiamo, dunque, che:
$$\mathbb{P}(X_{1}=i)=\mathbb{P}(X_{2}=j)=\frac{1}{6}\,\,\,\,\,\,\,\,\,\,\text{con }1\le i\le 6\,\text{ e }\,1\le j\le 6$$
e che:
$$\mathbb{P}(\{X_{1}\in I\}\cap\{X_{2}\in J\})\,=\,\mathbb{P}(X_{1}\in I)\cdot\mathbb{P}(X_{2}\in J)$$
considerata un'arbitraria coppia $I,\,J$ di sottoinsiemi di $\{1,\,2,\,\dots,\,6\}$. A questo punto, se volessimo ad esempio calcolare la probabilità dell'evento $E=\{\text{almeno uno dei due lanci risulta in un numero}\ge 5\}$, basterà osservare che $E=\{X_{1}\ge 5\}\cup\{X_{2}\ge 5\}$ e applicare la [[CDP_02 - Probabilità#Proprietà delle probabilità|formula di inclusione-esclusione]]; del resto, nell'applicare tale formula, ci tornerà utile ricordare che i due eventi che compongono $E$ sono, per ipotesi, stocasticamente indipendenti e che $\mathbb{P}(X_{1}\ge 5)=\mathbb{P}(X_{2}\ge 5)=\frac{1}{3}$. A questo punto, possiamo scrivere che:
$$\begin{align} \mathbb{P}(E)&=\mathbb{P}(\{X_{1}\ge 5\}\cup\{X_{2}\ge 5\})\\&= \mathbb{P}(X_{1}\ge 5)+\mathbb{P}(X_{2}\ge 5)-\mathbb{P}(\{X_{1}\ge 5\}\cap\{X_{2}\ge 5\})\\&=2\,\mathbb{P}(X_{1} \ge 5)-[\mathbb{P}(X_{1}\ge 5)]^{2}\\&=2\cdot \frac{1}{3}\,-\frac{\,1}{9}\\&=\frac{5}{9} \end{align}$$

Vediamo ancora un altro esempio. Supponiamo che una persona abbia comprato due biglietti per ciascuna di due diverse lotterie; sono stati emessi $700$ biglietti totali da ciascuna lotteria, e in ognuna di esse vengono estratti $3$ biglietti vincenti (si dà per scontato che tali estrazioni avvengano casualmente e senza reinserimento). Qual è la probabilità che la persona considerata vinca almeno un premio? Cominciamo a risolvere il problema identificando l'indipendenza stocastica tra quello che succede nelle due lotterie, e dunque tra gli eventi:
$$\begin{align} &E_{1}=\{\text{la persona vince almeno un premio nella 1° lotteria}\}\\&E_{2}=\{\text{la persona vince almeno un premio nella 2° lotteria}\} \end{align}$$
A questo punto, consideriamo l'evento $E=\{\text{la persona vince almeno un premio}\}$, che è quello che ci interessa maggiormente, e osserviamo che:
$$\begin{align} \mathbb{P}(E)&=\mathbb{P}(E_{1}\cup E_{2})\\&=\mathbb{P}(E_{1})+\mathbb{P}(E_{2})-\mathbb{P}(E_{1}\cap E_{2})\\&=\mathbb{P}(E_{1})+\mathbb{P}(E_{2})-\mathbb{P}(E_{1})\cdot\mathbb{P}(E_{2}) \end{align}$$
Dato che entrambe le lotterie forniscono $700$ biglietti ed estraggono $3$ biglietti vincenti, possiamo affermare che $\mathbb{P}(E_{1})=\mathbb{P}(E_{2})$, e dunque possiamo riscrivere l'uguaglianza precedente come:
$$\mathbb{P}(E)=2\,\mathbb{P}(E_{1})-[\mathbb{P}(E_{1})]^{2}$$
Ora, per quanto riguarda il calcolo di $\mathbb{P}(E_{1})$, ci conviene calcolarlo sfruttando la probabilità del suo complementare, ossia $\overline{E_{1}}=\{\text{la persona non vince alcun premio nella 1° lotteria}\}$, e porre dunque:
$$\mathbb{P}(E_{1})=1-\mathbb{P}(\overline{E_{1}})$$
Per calcolare $\mathbb{P}(\overline{E_{1}})$, possiamo agire principalmente in due modi:
1. indicando come $A_{1}^{i}$ l'evento tale per cui non viene estratto nessuno dei due biglietti comprati all'estrazione $i$-esima, possiamo affermare che $\mathbb{P}(\overline{E_{1}})=\mathbb{P}(A_{1}^{1}\cap A_{1}^{2}\cap A_{1}^{3})$, e applicando la [[CDP_02 - Probabilità#Formula delle probabilità composte|formula delle probabilità composte]] sappiamo che tale probabilità è pari a $\mathbb{P}(A_{1}^{1})\cdot\mathbb{P}(A_{1}^{2}\,|\,A_{1}^{1})\cdot\mathbb{P}(A_{1}^{3}\,|\,A_{1}^{1}\cap A_{1}^{2}) = \frac{698}{700}\cdot \frac{697}{699}\cdot \frac{696}{698}=\frac{697}{700}\cdot \frac{696}{699}$;
2. [pag. 60].

A questo punto, avendo trovato $\mathbb{P}(\overline{E_{1}})=\frac{697}{700}\cdot \frac{696}{699}$, abbiamo che:
$$\mathbb{P}(E_{1})=1-\mathbb{P}(\overline{E_{1}})=1-\frac{697}{700}\cdot \frac{696}{699}$$

D'ora in poi, per indicare che due eventi $A$ e $B$ sono stocasticamente indipendenti, si utilizzerà la notazione $A\,\bot \,B$.
___
## Indipendenza tra 2 partizioni

Avendo stabilito il concetto di [[CDP_03 - Correlazione e indipendenza tra eventi#Correlazione e indipendenza tra 2 eventi|indipendenza tra 2 eventi]], possiamo estenderlo a comprendere anche due [[CDP_01 - Eventi#Partizione dell'evento certo|partizioni]]. Per fare ciò, partiamo considerando due eventi $A$ e $B$, e le loro rispettive negazioni $\overline{A}$ e $\overline{B}$. È facile dimostrare che le seguenti relazioni sono fra di loro tutte equivalenti:
$$A\,\bot\,B\,\,\,\,\,\,\,\,\,\,\overline{A}\,\bot\,B\,\,\,\,\,\,\,\,\,\,A\,\bot\,\overline{B}\,\,\,\,\,\,\,\,\,\,\overline{A}\,\bot\,\overline{B}$$
Ciò può essere riassunto affermando che, prendendo un qualunque evento della partizione $\{A,\,\overline{A}\}$, e abbinandolo con un qualunque evento della partizione $\{B,\,\overline{B}\}$, si ottiene una **coppia di eventi indipendenti**. Se ciò vale per due partizioni generiche, allora si può affermare che tali partizioni sono "partizioni indipendenti".

> Siano $\mathcal{A}=\{A_{1},\,A_{2},\,\dots,\,A_{n}\}$ e $\mathcal{B}=\{B_{1},\,B_{2},\,\dots,\,B_{m}\}$ due diverse partizioni finite di uno stesso spazio campione $\Omega$. Si ha che $\mathcal{A}$ e $\mathcal{B}$ sono due "**partizioni indipendenti**", se, per ogni $i\in\{1,\,2,\,\dots,\,n\}$ e $j\in\{1,\,2,\,\dots,\,m\}$ vale che:
> $$A_{i}\,\bot \,B_{j}$$

Possiamo dimostrare che tale proprietà delle partizioni indipendenti non vale solo per gli eventi che le costituiscono concretamente, ma anche per qualsiasi unione dei loro eventi.

> Siano $\mathcal{A}=\{A_{1},\,A_{2},\,\dots,\,A_{n}\}$ e $\mathcal{B}=\{B_{1},\,B_{2},\,\dots,\,B_{m}\}$ due diverse partizioni finite e indipendenti di uno stesso spazio campione $\Omega$. Allora, in qualsiasi modo vengano scelti due eventi $E$ ed $F$ tali che:
> $$E=\bigcup_{i\,\in\,I}A_{i}\,\,\,\,\,\,\,\,\,\,F=\bigcup_{j\,\in\,J}B_{j}$$
> dove $I=\{i_{1},\,i_{2},\,\dots,\,i_{k}\}\subseteq\{1,\,2,\,\dots,\,n\}$ e $J=\{j_{1},\,j_{2},\,\dots,\,j_{h}\}\subseteq\{1,\,2,\,\dots,\,m\}$, risulta che:
> $$E\,\bot\,F$$

Per **dimostrare** questa proprietà, consideriamo i due insiemi $I$ e $J$, definiti in modo identico a poco fa. Ora, posti:
$$E=\bigcup_{i\,\in\,I}A_{i}=\bigcup_{r\,=\,1}^{k}A_{i_{r}}\,\,\,\,\,\,\,\,\,\,F=\bigcup_{j\,\in\,J}B_{j}=\bigcup_{s\,=\,1}^{h}B_{j_{s}}$$
allora possiamo affermare che:
$$E\cap F=\bigcup_{i\,\in\,I}\bigcup_{j\,\in\,J}A_{i}\cap B_{j}=\bigcup_{r\,=\,1}^{k}\bigcup_{s\,=\,1}^{h}A_{i_{r}}\cap B_{j_{s}}$$
Ora, utilizziamo il fatto che $\mathcal{A}=\{A_{1},\,A_{2},\,\dots,\,A_{n}\}$ e $\mathcal{B}=\{B_{1},\,B_{2},\,\dots,\,B_{m}\}$ sono due partizioni finite dell'evento certo; ciò ci permette di affermare che:
$$\mathbb{P}(E\cap F)=\sum_{r\,=\,1}^{k}\sum_{s\,=\,1}^{h}\mathbb{P}(A_{i_{r}}\cap B_{j_{s}})$$
equivalenza che si deduce immediatamente dalla [[CDP_02 - Probabilità#Proprietà delle probabilità|proprietà di additività finita]] e dal fatto che, essendo $\mathcal{A}$ e $\mathcal{B}$ due partizioni, se $(i',\,j')\neq(i'',\,j'')$ allora gli eventi $(A_{i'}\cap B_{j'})$ e $(A_{i''}\cap B_{i''})$ sono incompatibili. A questo punto, sfruttando il fatto che le due partizioni sono anche indipendenti, possiamo riformulare l'equivalenza come:
$$\mathbb{P}(E\cap F)=\sum_{r\,=\,1}^{k}\sum_{s\,=\,1}^{h}\mathbb{P}(A_{i_{r}}\cap B_{j_{s}})=\sum_{r\,=\,1}^{k}\sum_{s\,=\,1}^{h}\mathbb{P}(A_{i_{r}})\cdot\mathbb{P}(B_{j_{s}})$$
Ora, possiamo affermare che:
$$\mathbb{P}(E)\mathbb{P}(F)=\left( \sum_{r\,=\,1}^{k}\mathbb{P}(A_{i_{r}}) \right)\left( \sum_{s\,=\,1}^{h}\mathbb{P}(B_{j_{s}}) \right)$$
e quindi, per ottenere l'indipendenza tra $E$ ed $F$, e dunque $E\,\bot\,F$, basterà applicare la proprietà distributiva della somma rispetto al prodotto, ottenendo:
$$\mathbb{P}(E\cap F)=\sum_{r\,=\,1}^{k}\sum_{s\,=\,1}^{h}\mathbb{P}(A_{i_{r}})\cdot\mathbb{P}(B_{j_{s}})=\left( \sum_{r\,=\,1}^{k}\mathbb{P}(A_{i_{r}}) \right)\left( \sum_{s\,=\,1}^{h}\mathbb{P}(B_{j_{s}}) \right)=\mathbb{P}(E)\mathbb{P}(F)$$
Valendo che $\mathbb{P}(E\cap F)=\mathbb{P}(E)\cdot\mathbb{P}(F)$, abbiamo dimostrato che $E$ ed $F$ sono due eventi stocasticamente indipendenti.

##### Algebre generate da famiglie di eventi

> Una famiglia $\mathcal{G}$ di eventi di $\Omega$, dunque tale per cui $\mathcal{G}\subseteq\mathcal{P}(\Omega)$, è un "**algebra**" se sono verificate le seguenti proprietà:
> 1. $\Omega\in\mathcal{G}$;
> 2. $E\in\mathcal{G}\,\Rightarrow\,\overline{E}\in\mathcal{G}$;
> 3. $E_{1},\,E_{2}\in\mathcal{G}\,\Rightarrow\,E_{1}\cup E_{2}\in\mathcal{G}$.

Dalle tre proprietà appena enunciate deriva anche che $\emptyset\in\mathcal{G}$ (per dimostrare ciò, sfruttare le proprietà $1.$ e $2.$ considerando $E=\Omega$), così come $E_{1},\,E_{2}\in\mathcal{G}\,\Rightarrow\,E_{1}\cap E_{2}\in\mathcal{G}$ (per dimostrare ciò, sfruttare la [[CDP_01 - Eventi#Proprietà relative alle operazioni insiemistiche|legge di De Morgan]] e le proprietà $2.$ e $3.$).

Le algebre non devono essere necessariamente generate direttamente da spazi campione, ma possono derivare anche da **famiglie di eventi** contenute in uno spazio campione.   

[pag. 63 - 64]
___
## Indipendenza completa e prove bernoulliane

[pag. 64/68]
___

