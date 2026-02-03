Avendo introdotto gli [[CDP_01 - Eventi|eventi]] e le loro varie proprietà, siamo pronti per cominciare a parlare concretamente di "**probabilità**". Tale concetto permette di formalizzare meglio un problema e di esprimere lo stato di incertezza del risultato di un esperimento aleatorio.

## Misure di probabilità

> Dato uno spazio campione $\Omega$, e sia $\mathcal{P}(\Omega)$ la famiglia delle sue parti, definiamo "**misura di probabilità**" o, più semplicemente, "**probabilità su $(\Omega, \mathcal{P}(\Omega))$**", una funzione $\mathbb{P}$ che soddisfa i seguenti assiomi:
> - la funzione è definita come $\mathbb{P}:\mathcal{P}(\Omega)\rightarrow[0, 1]$;
> - vale che $\mathbb{P}(\Omega)=1$ (questa proprietà viene detta "**condizione di normalizzazione**");
> - se si ha che $E_{1}\cap E_{2}=\emptyset$, allora deve valere anche che $\mathbb{P}(E_{1}\cup E_{2})=\mathbb{P}(E_{1})+\mathbb{P}(E_{2})$ (questa proprietà viene detta "**proprietà di additività**").

L'insieme di spazio campione, famiglia delle parti e misura di probabilità vanno a comporre ciò che viene definito "spazio finito di probabilità".

> Uno **spazio finito di probabilità** è una terna **($\Omega$, $\mathcal{P}(\Omega)$, $\mathbb{P}$)**, dove $\Omega$ è un insieme finito, **$\mathcal{P}(\Omega)$** è la famiglia delle parti di $\Omega$, e **$\mathbb{P}$** è una misura di probabilità su ($\Omega$, $\mathcal{P}(\Omega)$).

##### Verificare che $\mathbb{P}$ non è una misura di probabilità

Vediamo un esempio di esercizio, in cui si vuole mostrare che, tra due funzioni $\mathbb{P}_{1}$ e $\mathbb{P}_{2}$ che verranno fornite tra poco, solo $\mathbb{P}_{1}$ è una misura di probabilità su ($\Omega$, $\mathcal{P}(\Omega)$) con $\Omega=\{a,\,b,\,c,\,d\}$. Le funzioni $\mathbb{P}_{1}$ e $\mathbb{P}_{2}$ sono le seguenti:

![[misuradiprobabilita_es1.png]]

L'ipotesi è facilmente verificabile **controllando se $\mathbb{P}_{2}$ rispetta tutti e tre gli assiomi esposti nella definizione di misura di probabilità**: per quanto riguarda la prima condizione, essa viene rispettata in quanto $\mathbb{P}_{2}$ è definita come una funzione di tipo $\mathcal{P}(\Omega)\rightarrow[0,1]$; anche la seconda condizione viene rispettata, in quanto $\mathbb{P}_{2}(\Omega)=\mathbb{P}_{2}(\{a,\,b,\,c,\,d\})=1$; lo stesso, però, non si può dire della terza condizione, dato che c'è almeno una coppia di eventi incompatibili $E_{1}$ ed $E_{2}$ (ad esempio, $\{a,\,b,\,c\}$ e $\{d\}$) tali per cui non vale che $\mathbb{P}(E_{1}\cup E_{2})=\mathbb{P}(E_{1})+\mathbb{P}(E_{2})$.

Per verificare, invece, che $\mathbb{P}_{1}$ sia effettivamente una misura di probabilità su $(\Omega,\,\mathcal{P}(\Omega))$, il primo approccio che potrebbe venire in mente è di verificare la proprietà di additività per tutti gli eventi disgiunti di $\mathcal{P}(\Omega)$: tuttavia, un approccio del genere risulterebbe notevolmente lungo e incline a errori.
___
##### Proprietà delle probabilità

C'è un modo più semplice per dimostrare che una funzione $\mathbb{P}$ è una probabilità, e per ottenerlo cominciamo da alcune affermazioni. Per le prossime considerazioni, ricordiamo che si definirà con $\Omega$ un generico spazio campione finito e, ponendo $N$ come la cardinalità di $\Omega$, possiamo scrivere $\Omega$ come:
$$\Omega=\{\omega_{1},\,\omega_{2},\,\dots,\,\omega_{N}\}$$
Prima di tutto, notiamo che il terzo e ultimo assioma, ossia la proprietà dell'additività, può essere generalizzato considerando $n$ eventi disgiunti a due a due.

> La **proprietà di additività finita**, in generale, afferma che siano $E_{1},\,E_{2},\,\dots,\,E_{n}\,\in\,\mathcal{P}(\Omega)$ una serie di eventi incompatibili a due a due, allora si ha che:
> $$\mathbb{P}\left( \bigcup_{i\,=\,1}^{n}E_{i} \right)\,\,=\,\,\sum_{i\,=\,1}^{n}\mathbb{P}(E_{i})$$

A questo punto, procediamo ad elencare alcune **proprietà della probabilità**, che risultano in buona parte conseguenze immediate degli assiomi esposti nella [[CDP_02 - La probabilità#Misure di probabilità|definizione di misure di probabilità]]. Partiamo con la prima $(a)$, che riguarda la **probabilità di un evento composto $E$**:

> Ponendo $p(\omega_{i})=\mathbb{P}(\{\omega_{i}\})$, con $i$ che va da $1$ a $N$, si ha che per ogni $E\,\in\,\mathcal{P}(\Omega)$:
> $$\mathbb{P}(E)\,=\,\sum_{i\,=\,1}^{N}p(\omega_{i})\,=\,\sum_{\omega\,\in\,E}p(\omega)$$

In altre parole, tale proprietà afferma che **la probabilità di un evento composto $E$ è dato dalla somma delle probabilità degli eventi elementari $\omega_{i}$ che lo compongono**. Tale proprietà è facilmente dimostrabile: per definizione di evento composto, abbiamo che $E=\bigcup_{\omega\,\in\,E}(\{\omega\})$, e naturalmente i vari eventi $\omega$ sono incompatibili a due a due (trattandosi di eventi elementari); di conseguenza, per la proprietà di additività finita, possiamo affermare che:
$$\mathbb{P}(E)=\mathbb{P}\left(\bigcup_{i\,=\,1}^{N}\omega_{i}\right)=\sum_{i\,=\,1}^{N}\mathbb{P}(\omega_{i})$$
come volevasi dimostrare.

La prossima proprietà che analizzeremo $(b)$ è la cosiddetta "**probabilità del complementare**", e riguarda proprio la relazione tra **probabilità di un evento e del suo complementare**.

> Per ogni $E\,\in\,\mathcal{P}(\Omega)$, si ha che:
> $$\mathbb{P}(\overline{E})\,=\,1-\mathbb{P}(E)$$

In sostanza, ciò che afferma questa proprietà è che, dato un qualsiasi evento $E$, o accadrà tale evento $E$ o non accadrà, dato che riformulando la proprietà si ha che $\mathbb{P}(E)+\mathbb{P}(\overline{E})=1$, con $1$ che rappresenta una probabilità certa. Una conseguenza, per certi versi, di quanto appena detto è la seguente proprietà $(c)$ sull'**evento impossibile**:

> **L'evento impossibile ha probabilità nulla**, ovvero:
> $$\mathbb{P}(\emptyset)=0$$

Passiamo, ora, a definire la cosiddetta "**proprietà di monotonia**" $(d)$:

> Siano $A,\,B\,\in\,\mathcal{P}(\Omega)$ due eventi tali che $A\subseteq B$, allora si ha che:
> $$\mathbb{P}(A)\leq\mathbb{P}(B)$$
> Inoltre, ricordando che $B / A=B\cap\overline{A}$, si ha che:
> $$\mathbb{P}(B / A)\,=\,\mathbb{P}(B)-\mathbb{P}(A)$$

Ciò vale perché, come accennato nel [[CDP_01 - Eventi#Eventi dal punto di vista logico e insiemistico|capitolo precedente]], affermare che $A\subseteq B$ equivale a dire che ogni evento elementare che soddisfa $A$ soddisfa anche $B$, ed essendo $A$ un sottoinsieme proprio di $B$ ci sarà un numero maggiore di eventi elementari che soddisfano quest'ultimo (ossia quelli che soddisfano $A$ più altri ancora): ciò porta la probabilità $\mathbb{P}(B)$ ad essere maggiore o uguale della probabilità $\mathbb{P}(A)$.

Di seguito, esponiamo la **formula di inclusione-esclusione** nella sua forma più semplice, ossia considerando **due eventi** $(e)$.

> Per due eventi arbitrari $A,\,B\,\in\,\mathcal{P}(\Omega)$, si ha che:
> $$\mathbb{P}(A\cup B)\,=\,\mathbb{P}(A)+\mathbb{P}(B)-\mathbb{P}(A\cap B)$$

Tale formula è facilmente dimostrabile riflettendo sui significati concreti di unione e intersezione: fare l'unione di due eventi $A$ e $B$ significa considerare sia tutti gli eventi di $A$ che tutti gli eventi di $B$, tuttavia nel fare ciò verranno considerati due volte gli elementi che eventualmente si trovano sia in $A$ che in $B$, ossia $A\cap B$, dunque per eliminare questo eccesso basterà sottrarre tali elementi una volta. Naturalmente, nel caso in cui gli eventi considerati siano incompatibili, la loro intersezione sarà $A\cap B=\emptyset$, dunque tale operazione non sarà necessaria.

Possiamo generalizzare la formula di inclusione-esclusione in modo da poter considerare un numero $n$ di eventi. Dunque, dati $n$ eventi $A_{1},\,A_{2},\,\dots,\,A_{n}$, la probabilità che almeno uno tra tali eventi si verifichi è pari a:
$$\begin{align} \mathbb{P}(A_{1}\cup A_{2}\cup\,\dots\,\cup A_{n})&=\mathbb{P}(A_{1})+\mathbb{P}(A_{2})+\,\dots\,+\mathbb{P}(A_{n})\\ &-\mathbb{P}(A_{1}\cap A_{2})-\mathbb{P}(A_{1}\cap A_{3})-\,\dots\,-\mathbb{P}(A_{i}\cap A_{j})-\,\dots\,\mathbb{P}(A_{n-1}\cap A_{n}) \\ &+\, \dots \\ &+(-1)^{k-1}\sum_{\{i_{1},\,i_{2},\,\dots,\,i_{k}\}}\mathbb{P}(A_{i_{1}}\cap A_{i_{2}}\cap\,\dots\,\cap A_{i_{k}}) \\ &+\,\dots\\ &+(-1)^{n-1}\,\,\,\mathbb{P}(A_{1}\cap A_{2}\cap\,\dots\,\cap A_{n}) \end{align}$$
Possiamo riassumere tale formula utilizzando la seguente notazione:
$$\mathbb{P}(A_{1}\cup A_{2}\cup\,\dots\,\cup A_{n})=\sum_{k\,=\,1}^{n}\left( (-1)^{k-1}\sum_{\{i_{1},\,i_{2},\,\dots,\,i_{k}\}}\mathbb{P}(A_{i_{1}}\cap A_{i_{2}}\cap\,\dots\,\cap A_{i_{k}})\right)$$

Arriviamo, infine, a un'ultima proprietà $(f)$ facilmente deducibile dalla definizione di **partizione dell'evento certo**.

> Siano $H_{1},\,H_{2},\,\dots,\,H_{n}\,\in\,\mathcal{P}(\Omega)$ eventi tali che vale che:
> $$\bigcup_{i\,=\,1}^{n}H_{i}=\Omega\,\,\,\,\,\bigwedge\,\,\,\,\,H_{i}\cap H_{j}=\emptyset\,\,\,\text{per }i\neq j$$
> ossia costituiscano gli eventi $H_{1},\,H_{2},\,\dots,\,H_{n}$ una [[CDP_01 - Eventi#Partizione dell'evento certo|partizione dell'evento certo]], allora si può affermare che:
> $$\sum_{i\,=\,1}^{n}\,\mathbb{P}(H_{i})=1$$

Tutte queste proprietà, ad eccezione della prima che è già stata dimostrata, sono dimostrabili sfruttando la seguente relazione detta "**proprietà di base**":
$$\text{per ogni }A\text{ e }B\text{, vale che }\mathbb{P}(A)=\mathbb{P}(A\cap B)+\mathbb{P}(A\cap\overline{B})$$
che a sua volta è facilmente dimostrabile nel modo seguente: $A$ può essere definita come $(A\cap B)\cup(A\cap\overline{B})$ per un qualsiasi $B$, dato che
$$A=A\cap \Omega=A\cap(B\cup\overline{B})=(A\cap B)\cup(A\cap\overline{B})$$
Inoltre, è immediato verificare che $A\cap B$ e $A\cap\overline{B}$ siano eventi disgiunti, dato che
$$(A\cap B)\cap(A\cap\overline{B})=A\cap B\cap\overline{B}=A\cap\emptyset=\emptyset$$
Dunque, essendo $A\cap B$ e $A\cap\overline{B}$ due eventi disgiunti, ed essendo $A$ un evento composto dall'unione di essi, per la proprietà di additività possiamo affermare che:
$$\mathbb{P}(A)=\mathbb{P}(A\cap B)+\mathbb{P}(A\cap\overline{B})$$

Ora, avendo dimostrato tale relazione, possiamo sfruttarla per dimostrare le proprietà dalla $(b)$ alla $(f)$ elencate in precedenza. Partiamo dalla proprietà $(b)$: affermare che $\mathbb{P}(\overline{E}) = 1-\mathbb{P}(E)$ si deriva dalla relazione appena dimostrata prendendo $A=\Omega$ e $B=E$, per cui $A\cap B=\Omega\cap E=E$, mentre $A\cap\overline{B}=\Omega\cap\overline{E}=\overline{E}$; di conseguenza, possiamo affermare che:
$$\mathbb{P}(\Omega)=\mathbb{P}(\Omega\cap E)+P(\Omega\cap\overline{E})=\mathbb{P}(E)+\mathbb{P}(\overline{E})$$
Sapendo che $\mathbb{P}(\Omega)=1$, abbiamo dunque che $\mathbb{P}(E)+\mathbb{P}(\overline{E})=1$, e di conseguenza come formula inversa che $\mathbb{P}(\overline{E})=1-\mathbb{P}(E)$, come volevasi dimostrare.

Vediamo, ora, la proprietà $(c)$: banalmente, essa può essere dimostrata osservando che $\emptyset$, ossia l'evento impossibile, è il complementare di $\Omega$, ossia dell'evento certo ($\emptyset=\overline{\Omega}$), dunque se abbiamo che $\mathbb{P}(\Omega)=1$ per la [[CDP_02 - La probabilità#Misure di probabilità|condizione di normalizzazione]], allora abbiamo che $\mathbb{P}(\emptyset)=1-\mathbb{P}(\Omega)=1-1=0$.

A questo punto, passiamo alla proprietà $(d)$: per dimostrarla, osserviamo che se $A\subseteq B$ allora necessariamente $A\cap B=A$, e quindi $\mathbb{P}(A)=\mathbb{P}(A\cap B)$; dunque, scambiando i ruoli di $A$ e $B$ nella relazione mostrata in precedenza (il risultato non cambia nonostante questo scambio), abbiamo che:
$$\mathbb{P}(B)=\mathbb{P}(B\cap A)+\mathbb{P}(B\cap\overline{A})=\mathbb{P}(A)+\mathbb{P}(B\cap\overline{A})$$
Dunque, abbiamo che la probabilità $\mathbb{P}(B)$ è data dalla probabilità di $A$ ($\mathbb{P}(A)$) sommata alla probabilità di eventuali eventi che rientrano in $B$ e non in $A$ ($\mathbb{P}(B\cap\overline{A})$): di conseguenza, si ottiene che $\mathbb{P}(B)\ge\mathbb{P}(A)$. Inoltre, ricordando che $B/A=B\cap\overline{A}$, e presupponendo sempre che $A\subseteq B$, possiamo affermare in base all'equivalenza appena ottenuta che:
$$\mathbb{P}(B/A)=\mathbb{P}(B)-\mathbb{P}(A)$$

Arriviamo, così, alla proprietà $(e)$, ossia alla formula di inclusione-esclusione a due eventi: partiamo osservando che l'unione tra due eventi $A$ e $B$ è equivalente all'unione tra $3$ eventi incompatibili tra loro, ossia l'intersezione tra $A$ e $B$, gli elementi contenuti in $A$ e non in $B$, e gli elementi contenuti in $B$ e non in $A$:
$$A\cup B=(A\cap B)\cup(A\cap\overline{B})\cup(\overline{A}\cap B)$$
di conseguenza, possiamo affermare che:
$$\mathbb{P}(A\cup B)=\mathbb{P}(A\cap B)+\mathbb{P}(A\cap \overline{B})+\mathbb{P}(\overline{A}\cap B)$$
Applicando la solita relazione, possiamo ridurre $\mathbb{P}(A\cap B)+\mathbb{P}(A\cap\overline{B})$ a $\mathbb{P}(A)$, e dalla dimostrazione della proprietà $(d)$ sappiamo che $\mathbb{P}(\overline{A}\cap B)=\mathbb{P}(B)-\mathbb{P}(A\cap B)$, dunque l'equivalenza precedente può essere riscritta come:
$$\mathbb{P}(A\cup B)=\mathbb{P}(A)+\mathbb{P}(B)-\mathbb{P}(A\cap B)$$

Infine, dimostriamo la proprietà $(f)$: essa è un'immediata conseguenza degli assiomi utilizzati nella definizione di misura di probabilità, in particolare della condizione di normalizzazione e della proprietà di additività finita. Infatti, da una parte $H_{1},\,H_{2},\,\dots,\,H_{m}$ sono per definizione eventi incompatibili a due a due, dunque per la proprietà di additività finita si ha che:
$$\mathbb{P}\left(\bigcup_{l\,=\,1}^{m}H_{l}\right)=\sum_{l\,=\,1}^{m}\mathbb{P}(H_{l})$$
Al tempo stesso, sapendo che $H_{1},\,H_{2},\,\dots,\,H_{m}$ rappresentano una partizione dell'evento certo $\Omega$, sappiamo che:
$$\mathbb{P}\left(\bigcup_{l\,=\,1}^{m}H_{l}\right)=\mathbb{P}(\Omega)=1$$
e perciò, unendo queste due deduzioni, si ottiene che:
$$\sum_{l\,=\,1}^{m}\mathbb{P}(H_{l})=1$$
come volevasi dimostrare.
___
##### Due modi di vedere la probabilità

Considerando $\Omega$ come un insieme finito, possiamo guardare la probabilità in **due modi**, apparentemente diversi ma in realtà **equivalenti**. Vediamoli in questo paragrafo.

Il **primo modo** consiste nel partire da una "**funzione di insieme**" (ossia una funzione che prende come "input" un insieme di elementi, in questo caso un evento composto $E$) $\mathbb{P}$, definita come:
$$\mathbb{P}:\mathcal{P}(\Omega)\rightarrow[0,\,1];\,\,\,\,\,\,\,\,\,\,E\mapsto\mathbb{P}(E)$$
e che soddisfi i [[CDP_02 - La probabilità#Misure di probabilità|tre assiomi]] visti a inizio capitolo; di seguito, in base a tale funzione di insieme, definiamo la seguente "**funzione di punto**" (ossia una funzione che prende come "input" un singolo elemento, in questo caso un evento elementare $\omega_{i}$):
$$p:\Omega\rightarrow[0,1];\,\,\,\,\,\,\,\,\,\,\omega_{i}\mapsto p(\omega_{i}):=\mathbb{P}(\{\omega_{i}\})$$
che dovrò soddisfare, a sua volta, le due seguenti condizioni:
$$p(\omega_{i})\ge 0\,\,\,\,\,\bigwedge\,\,\,\,\,\sum_{i\,=\,1}^{N}p(\omega_{i})=1$$

Il **secondo modo** consiste invece nel partire da una funzione di punto $p$, definita come:
$$p:\Omega\to[0,\,1];\,\,\,\,\,\,\,\,\,\,\omega_{i}\mapsto p(\omega_{i})$$
e che soddisfi le condizioni appena viste; in seguito, si vorrà definire una funzione di insieme basata su tale funzione di punto, tale per cui:
$$E\mapsto\mathbb{P}(E):=\sum_{\omega\,\in\,E}p(\omega)$$
___
##### Probabilità definita a meno di un fattore di proporzionalità

Per definizione, una misura di probabilità sullo spazio $\Omega=\{\omega_{1},\,\omega_{2},\,\dots,\,\omega_{N}\}$ è individuata quando vengono assegnati i numeri $p(\omega_{i})=\mathbb{P}(\{\omega_{i}\})$ per ogni $i$ che va da $1$ a $N$, assegnati in modo che ogni valore $p(\omega_{i})$ sia maggiore o uguale a $0$ e che la loro somma, per la [[CDP_02 - La probabilità#Misure di probabilità|condizione di normalizzazione]], sia pari a $1$. Supponiamo, ora, che **ci sia una qualche proporzionalità tra i valori $p(\omega_{i})$**, e dunque che i valori $p(\omega_{i})$ vengano assegnati "**a meno di una costante di proporzionalità**": ciò vuol dire che esiste una costante positiva $K$, così come dei numeri $g_{i}$, tali per cui:
$$\text{per ogni }i=1,\,2,\,\dots,\,N\text{ vale }\,\,\,p(\omega_{i})=K\cdot g_{i}$$
o, in breve, che:
$$p(\omega_{i})\propto g_{i}$$
Sommando su $i$, si ottiene che:
$$\sum_{i\,=\,1}^{N}p(\omega_{i})\,=\,\sum_{i\,=\,1}^{N}K\cdot g_{i}\,=\,K\sum_{i\,=\,1}^{N}g_{i}$$
e sapendo che tale sommatoria deve risultare in $1$ per la condizione di normalizzazione, ci è possibile **ricavare il valore di $K$**, che possiamo chiamare "**fattore di proporzionalità**":
$$K\sum_{i\,=\,1}^{N}g_{i}=1\,\,\,\Rightarrow\,\,\,K=\frac{1}{\sum_{i\,=\,1}^{N}g_{i}}$$
Come diretta conseguenza, avendo definito $p(\omega_{i})=K\cdot g_{i}$ in questo contesto, possiamo ottenere una formula per calcolare un determinato valore $p(\omega_{i})$:
$$p(\omega_{i})=\frac{g_{i}}{\sum_{j\,=\,1}^{N}g_{j}}$$

Questi concetti e queste formule tornano utili nel momento in cui si lavora con **fenomeni dove ogni evento elementare ha una certa probabilità di verificarsi rispetto a un altro**: infatti, possiamo vedere i vari numeri $g_{i}$ come una sorta di **"pesi" relativi**, che ci fanno capire, in base al tipo di proporzionalità che si verifica, quale evento dovrebbe essere più probabile rispetto ad altri. Naturalmente, i valori $g_{i}$ sono solo pesi relativi, e non possono valere come probabilità effettive: è qui che entra in gioco la **costante di proporzionalità $K$**, che formalizza la relazione tra i vari pesi relativi e contribuisce a "normalizzarli" in modo da ottenere le probabilità effettive ($p(\omega_{i})=K\cdot g_{i}$), assicurando che venga rispettata la condizione di normalizzazione.

Per comprendere meglio questo concetto, vediamo un paio di **esempi**. Supponiamo di avere un dado a $6$ facce, numerate da $1$ a $6$, ma pesato in modo tale che ciascuna faccia abbia una probabilità di presentarsi, in un singolo lancio, direttamente proporzionale al suo valore (dunque, $2$ è più probabile di $1$, $3$ è più probabile di $2$, e così via). Considerato l'evento $A$ definito nel modo seguente:
$$A=\{\text{si presenta un numero pari}\}$$
vogliamo trovare $\mathbb{P}(A)$. Dato che stiamo lavorando con un dado a $6$ facce, sappiamo che lo spazio campione sarà $\Omega=\{\omega_{1},\,\omega_{2},\,\dots,\,\omega_{6}\}$, ed essendoci una relazione tra le probabilità delle varie facce, vogliamo imporre:
$$p(\omega_{i})=K\cdot g_{i},\,\,\,\text{per }i=1,\,2,\,\dots,\,6$$
Essendo la probabilità del presentarsi di ciascuna faccia del dado direttamente proporzionale al suo valore, possiamo assumere direttamente che $g_{i}=i$, e dunque otteniamo che:
$$\begin{align} 1&=p(\omega_{1})+p(\omega_{2})+p(\omega_{3})+p(\omega_{4})+p(\omega_{5})+p(\omega_{6})\\&=K\cdot 1 + K\cdot 2 + K\cdot 3+K\cdot 4+K\cdot 5+K\cdot 6\\&=21K\end{align}$$
Da ciò, si ricava che $K=\frac{1}{21}$, di conseguenza abbiamo che:
$$p(\omega_{i})=\frac{i}{21}$$
Ora, avendo trovato un modo per calcolare concretamente la probabilità di ciascun evento elementare del nostro esperimento, possiamo tranquillamente rispondere alla domanda iniziale. L'evento $A$, ossia che si presenti un numero pari, è un [[CDP_01 - Eventi#Eventi elementari e composti|evento composto]] definito dall'unione tra gli eventi $\omega_{2}$, $\omega_{4}$ e $\omega_{6}$, dunque la probabilità $\mathbb{P}(A)$, per la [[CDP_02 - La probabilità#Proprietà delle probabilità|proprietà di additività finita]], è pari a:
$$\mathbb{P}(A)=p(\omega_{2})+p(\omega_{4})+p(\omega_{6})=\frac{2}{21}+\frac{4}{21}+\frac{6}{21}=\frac{12}{21}=\frac{4}{7}$$

Vediamo un altro esempio abbastanza simile. Supponiamo di avere un dado a $6$ facce, numerate da $1$ a $6$, ma pesato in modo tale che una faccia con valore pari abbia il doppio della probabilità di presentarsi di una faccia con valore dispari. Considerato l'evento $A$ definito nel modo seguente:
$$A=\{\text{si presenta un numero pari}\}$$
vogliamo trovare $\mathbb{P}(A)$. Dato che stiamo lavorando con un dado a $6$ facce, sappiamo che lo spazio campione sarà $\Omega=\{\omega_{1},\,\omega_{2},\,\dots,\,\omega_{6}\}$, ed essendoci una relazione tra le probabilità delle varie facce, vogliamo imporre:
$$p(\omega_{i})=K\cdot g_{i},\,\,\,\text{per }i=1,\,2,\,\dots,\,6$$
Essendo la probabilità che si presenti una faccia con valore pari doppia rispetto a quella che si presenti una faccia con valore dispari, possiamo affermare ad esempio che $g_{i} = 2$ per $i$ pari, e allo stesso tempo che $g_{i}=1$ per $i$ dispari. Dunque, otteniamo che:
$$\begin{align} 1&=p(\omega_{1})+p(\omega_{2})+p(\omega_{3})+p(\omega_{4})+p(\omega_{5})+p(\omega_{6})\\&=K\cdot 1+K\cdot 2+K\cdot 1 + K\cdot 2+K \cdot 1 +K\cdot 2\\&=9K\end{align}$$
Da ciò, si ricava che $K=\frac{1}{9}$, di conseguenza abbiamo che:
$$p(\omega_{i})=\frac{g_{i}}{9}$$
Ora, avendo trovato un modo per calcolare concretamente la probabilità di ciascun evento elementare del nostro esperimento, rispondiamo alla domanda iniziale. L'evento $A$, ossia che si presenti un numero pari, è un evento composto definito dall'unione tra gli eventi $\omega_{2}$, $\omega_{4}$ e $\omega_{6}$, dunque la probabilità $\mathbb{P}(A)$, per la proprietà di additività finita, è pari a:
$$\mathbb{P}(A)=p(\omega_{2})+p(\omega_{4})+p(\omega_{6})=\frac{2}{9}\cdot 3= \frac{6}{9}=\frac{2}{3}$$
___
## Probabilità "uniformi" e calcolo combinatorio

Sia $\Omega=\{\omega_{1},\,\omega_{2},\,\dots,\,\omega_{N}\}$, e supponiamo che si voglia porre:
$$p(\omega_{i})=K,\,\,\,\,\,\forall \omega_{i}\in \Omega$$
dove $K$ corrisponde a una certa costante positiva. Imponendo questa condizione, affermiamo che **tutti gli eventi elementari relativi al fenomeno considerato sono "equiprobabili"**, cioè hanno tutti la stessa probabilità di avvenire in una singola osservazione del fenomeno. Formalmente, una casistica del genere viene definita come una "**distribuzione di probabilità uniforme sugli eventi elementari**".

Lavorando con tale distribuzione di probabilità, e tenendo a mente la **[[CDP_02 - La probabilità#Misure di probabilità|condizione di normalizzazione]]**, possiamo affermare che:
$$p(\omega_{i})=\frac{1}{|\Omega|}=\frac{1}{N},\,\,\,\,\,\text{per ogni }i=1,\,2,\,\dots,\,N$$
Di conseguenza, ricordando la **[[CDP_02 - La probabilità#Proprietà delle probabilità|proprietà di additività finita]]**, si ottiene che:
$$\mathbb{P}(E)=\frac{|E|}{|\Omega|}=\frac{|E|}{N},\,\,\,\,\,\text{per ogni }E\in\mathcal{P}(\Omega)$$
Tale formula può essere letta, in parole povere, come l'affermazione del fatto che, nel caso in cui tutti gli eventi elementari di uno spazio finito $\Omega$ siano equiprobabili, la probabilità di un generico [[CDP_01 - Eventi#|evento composto]] $E$ è pari al **rapporto tra eventi favorevoli e eventi possibili**. Dunque, in questo tipo di situazioni, il problema del calcolare la probabilità di $E$ si riduce ai **problemi di calcolo combinatorio** dati dall'individuare i due valori $N=|\Omega|$ e $|E|$.

Passiamo, dunque, ad approfondire alcuni **concetti di calcolo combinatorio**, che ci saranno utili per affrontare vari problemi di calcolo delle probabilità. Innanzitutto, partiamo ricordando due fatti fondamentali:
- due insiemi finiti hanno la **stessa cardinalità** se e solo se fra di essi è possibile stabilire una **corrispondenza biunivoca**;
- dati due insiemi arbitrari $A$ e $B$, si definisce "**prodotto cartesiano** tra $A$ e $B$" l'insieme costituito dalle coppie ordinate $(a, b)$ dove $a\in A$ e $b\in B$, indicato con la notazione $A\times B$; nel caso in cui $A$ e $B$ siano insiemi finiti, la cardinalità del prodotto cartesiano $A\times B$ sarà pari al prodotto tra le cardinalità di $A$ e $B$.

##### Disposizioni con ripetizione

Una "**disposizione con ripetizione di classe $k$ di $n$ elementi**" non è altro che una **$k$-upla ordinata** formata a partire da tali $n$ elementi, dove **è possibile che un elemento si ripeta**.

Dunque, a partire da un insieme $A=\{a_{1},\,a_{2},\,\dots,\,a_{n}\}$, tali disposizioni costituiscono l'insieme:
$$A^{k}=\{A\times A\times\dots \times A\}$$
dove il prodotto cartesiano viene ripetuto $k$ volte, e la cardinalità $|A^{k}|$ di tale insieme è pari a $n^{k}$. 
___
##### Disposizioni senza ripetizione

Una "**disposizione senza ripetizione di classe $k$ di $n$ elementi**" si definisce sostanzialmente allo stesso modo delle [[CDP_02 - La probabilità#Disposizioni con ripetizione|disposizioni con ripetizione]], ma con la sostanziale differenza che **non è possibile che un elemento si ripeta**, o in altri termini che **gli elementi della disposizione sono tutti diversi tra loro**. Ciò pone un vincolo implicito ai valori che può assumere $k$, dato che **deve necessariamente valere che $k\le n$**.

L'insieme delle disposizioni senza ripetizione è in realtà un sottoinsieme di $A^{k}$, ossia dell'insieme delle disposizioni con ripetizione, e ha cardinalità pari a:
$$n\cdot(n-1)\cdot(n-2)\cdot\,\dots \,\cdot(n-(k-1))=\frac{n!}{(n-k)!}$$
Possiamo indicare il numero delle possibili disposizioni senza ripetizione di classe $k$ di $n$ elementi con la dicitura $D^{n}_{k}$.
___
##### Permutazioni

Le "**permutazioni**" rappresentano una sorta di **caso particolare di [[CDP_02 - La probabilità#Disposizioni senza ripetizione|disposizione senza ripetizione]]**, e consistono sostanzialmente in un **riordinamento di $n$ elementi**; la relazione con le disposizioni senza ripetizione è data dalla cardinalità dell'insieme delle possibili permutazioni di $n$ elementi, dato che essa si ottiene come la cardinalità delle prime, ma ponendo $k=n$, e dunque:
$$\frac{n!}{(n-n)!}=\frac{n!}{1}=n!$$
Dunque, dati $n$ elementi, ci saranno $n!$ modi possibili di riordinare quegli stessi $n$ elementi.

Possiamo indicare il numero delle possibili permutazioni di $k$ elementi con la dicitura $P_{k}$.
___
##### Combinazioni

Le "**combinazioni di classe $k$ di $n$ elementi**" sono **$k$-uple non ordinate**, dunque in cui non conta l'ordine degli elementi ma solo gli elementi effettivamente presenti, formate a partire da tali $n$ elementi, dove **non è possibile che un elemento si ripeta**, o in altri termini che **gli elementi della disposizione sono tutti diversi tra loro**. Ciò, come per le [[CDP_02 - La probabilità#Disposizioni senza ripetizione|disposizioni senza ripetizione]], implica che debba necessariamente valere che $k\le n$.

Un modo alternativo, più semplice, di definire una combinazione di classe $k$ di $n$ elementi è come **un sottoinsieme di cardinalità $k$ degli elementi di un insieme di cardinalità $n$**.

Ad esempio, considerato l'insieme $A=\{a,\,b,\,c,\,d,\,e,\,f,\,g\}$, che ha $n=7$ elementi, e considerato $k=3$, una possibile disposizione senza ripetizioni di classe $k$ può essere la terna ordinata $(a,\,d,\,f)$, e per sua natura tale terna sarà concretamente diversa dalla terna $(d,\,f,\,a)$, proprio perché pur contenendo gli stessi elementi essi sono posti in ordine diverso. Invece, se a partire dallo stesso insieme $A$ estrapoliamo la combinazione di classe $k$ $\{a,\,d,\,f\}$, essa sarà perfettamente coincidente con la combinazione $\{d,\,f,\,a\}$, dato che nelle combinazioni non è rilevante l'ordine in cui sono posti gli elementi. 

Possiamo indicare il numero delle possibili combinazioni di classe $k$ di $n$ elementi con la dicitura $C_{k}^{n}$. Ora, risulta banale che $C_{0}^{n}$ equivale al numero di modi in cui si possono estrarre $0$ elementi da un insieme di $n$ elementi, e ciò si può fare in un unico modo: non prendendo alcun elemento (l'insieme vuoto $\emptyset$); dunque $C_{0}^{n}=1$. Allo stesso modo, sappiamo che $C_{n}^{n}=1$ perché, analogamente, c'è un unico modo di estrarre $n$ elementi da un insieme di $n$ elementi, ossia prendendoli tutti. Inoltre, è facile convincersi che $C_{k}^{n}=C_{n-k}^{n}$: per dimostrare questa affermazione, basta pensare che una combinazione di classe $k$ non è altro che un sottoinsieme di $k$ elementi dell'insieme di partenza, e dunque estrarre tale sottoinsieme lascerà necessariamente un altro sottoinsieme di $n-k$ elementi; dunque, è possibile trovare una corrispondenza biunivoca tra la famiglia dei sottoinsiemi di cardinalità $k$ (ossia $C_{k}^{n}$ e quella dei sottoinsiemi di cardinalità $n-k$ (ossia $C_{n-k}^{n}$). Infine, un'ultima equivalenza mette in relazione le combinazioni con le disposizioni senza ripetizione e con le [[CDP_02 - La probabilità#Permutazioni|permutazioni]], ed è la seguente:
$$D_{k}^{n}=C_{k}^{n}\cdot P_{k}$$
È possibile dimostrare questa affermazione ragionando sulle caratteristiche di ciascuna di queste entità: innanzitutto, le disposizioni senza ripetizione di classe $k$ di $n$ elementi possono essere "raggruppate" in modo da avere, all'interno di ciascuno di questi gruppi, solo disposizioni che contengono gli stessi elementi, e che dunque differiscono tra loro solo per l'ordinamento degli stessi; sostanzialmente, ognuno dei gruppi ottenuti identifica una singola combinazione di classe $k$ degli $n$ elementi iniziali, e dunque possiamo affermare che il nostro raggruppamento ha generato $C_{k}^{n}$ gruppi. Ora, come abbiamo detto, ogni gruppo contiene disposizioni che differiscono tra loro solo per l'ordinamento, dunque che rappresentano la serie di permutazioni possibili dei $k$ elementi che ogni disposizione del gruppo contiene: si deduce, da ciò, che ogni gruppo contiene $P_{k}$ disposizioni. Avendo stabilito che le $D_{k}^{n}$ disposizioni possono essere raggruppate in $C_{k}^{n}$ gruppi, dove ogni gruppo contiene $P_{k}$ disposizioni, si è dimostrato proprio che $D_{k}^{n}=C_{k}^{n}\cdot P_{k}$.

A partire dall'equivalenza appena dimostrata possiamo ricavare una **formula per calcolare il numero di combinazioni possibili di classe $k$ di $n$ elementi**, ossia $C_{k}^{n}$. Infatti, sapendo che $D_{k}^{n}=\frac{n!}{(n-k)!}$, e che $P_{k}=k!$, si ottiene che:
$$\frac{n!}{(n-k)!}=C_{k}^{n}\cdot k!\,\,\,\Rightarrow\,\,\,C_{k}^{n}=\frac{n!}{k!\cdot(n-k)!}$$
Per brevità, la formula appena ottenuta si indica anche con il cosiddetto "**coefficiente binomiale $n$ sopra $k$**", letto anche come "**$n$ su $k$**" o come "**scegli $k$ tra $n$**":
$$\frac{n!}{k!\cdot(n-k)!}:=\binom{n}{k}$$

Nello studio del calcolo combinatorio, è utile tenere presente anche alcune **proprietà dei coefficienti binomiali**. Innanzitutto, come anticipato, possiamo affermare che $C_{0}^{n}=\binom{n}{0}=1$, e anche che $C_{n}^{n}=\binom{n}{n}=1$; allo stesso modo, si ha anche che $\binom{n}{k}=\binom{n}{n\,-\,k}$. Un'altra identità meno immediata di quelle appena viste è la cosiddetta "**formula di Stiefel**", che afferma che:
$$\binom{n}{k}=\binom{n-1}{k-1}+\binom{n-1}{k}$$
che vale purché si abbia che $1\le k\le n-1$. Possiamo dimostrare tale formula ricordando che $\binom{n}{k}=C_{k}^{n}$, ossia il numero dei sottoinsiemi di cardinalità $k$ di un insieme $A=\{a_{1},\,a_{2},\,\dots,\,a_{n-1},\,a_{n}\}$; di conseguenza, la formula di Stiefel può essere riformulata nel modo seguente:
$$C_{k}^{n}=C_{k-1}^{n-1}+C_{k}^{n-1}$$
I sottoinsiemi di cardinalità $k$ di $A$ possono essere divisi in due classi: i sottoinsiemi $C$ che contengono l'elemento $a_{n}$, e i sottoinsiemi $D$ che non contengono tale elemento; di conseguenza, il numero $C_{k}^{n}$ di sottoinsiemi di cardinalità $k$ di $A$ può essere espresso come somma delle cardinalità di queste due classi. Sappiamo che gli insiemi di tipo $C$ si possono esprimere come $C=C'\cup\{a_{n}\}$, dove $C'$ è un sottoinsieme di $A-\{a_{n}\}$ che ha cardinalità $k-1$, dunque sappiamo che il numero di sottoinsiemi di tipo $C$ è pari al numero di sottoinsiemi di cardinalità $k-1$ di $n-1$ elementi, ossia $C_{k-1}^{n-1}$; invece, gli insiemi di tipo $D$ sono semplicemente sottoinsiemi di cardinalità $k$ dell'insieme $A-\{{a_{n}}\}$, che a sua volta ha cardinalità $n-1$, dunque ci saranno $C_{k}^{n-1}$ sottoinsiemi di tipo $D$. Abbiamo stabilito che $C_{k}^{n}$ è pari alla somma tra numero di insiemi $C$ e di insiemi $D$, e abbiamo così dimostrato che $C_{k}^{n}=C_{k-1}^{n-1}+C_{k}^{n-1}$. 

Tramite la formula appena esplicitata, si può anche ottenere la seguente equivalenza:
$$\sum_{r\,=\,k}^{n}\binom{r}{k}=\binom{n+1}{k+1}$$
purché si abbia che $0\le k\le n$. Inoltre, possiamo anche affermare che:
$$(a+b)^{n}=\sum_{k\,=\,0}^{n}\binom{n}{k}a^{k}b^{n-k}$$
che, ponendo $a=b=1$, ci porta alla seguente proprietà:
$$\sum_{k\,=\,0}^{n}\binom{n}{k}=2^{n}$$
Tenendo presente che $\binom{n}{k}$ coincide con il numero di combinazioni di classe $k$ di $n$ elementi, e dunque con il numero di sottoinsiemi di cardinalità $k$ ottenibili da un insieme di $n$ elementi, si deduce che **la cardinalità della [[CDP_01 - Eventi#Eventi elementari e composti|famiglia delle parti]] di un insieme di $n$ elementi è pari a $2^{n}$**, e dunque che in un esperimento aleatorio che presenta $n$ eventi elementari ci saranno un totale di $2^{n}$ tra eventi elementari e composti, inclusi anche l'evento certo e l'evento impossibile.

Un'altra identità utile è la cosiddetta "**identità di Vandermonde**", ossia:

> Per una qualunque terna di numeri naturali $r$, $s$ e $n$, con $n\le r+s$, si ha che:
> $$\sum_{k\,=\,0\,\lor\,(n-s)}^{n\,\land\,r}\binom{r}{k}\binom{s}{n-k}=\binom{r+s}{n}$$
> dove con $k=0\lor(n-s)$ si intende che la sommatoria parte dal valore $k$ più grande tra $0$ e $n-s$, mentre con $n\land r$ si intende che la sommatoria arriva al valore più piccolo tra $n$ e $r$.

[dimostrazione: pag. 33 - 34]

[proprietà dei coefficienti binomiali: pag. 35]
___
##### Principio fondamentale del calcolo combinatorio

[pag. 42]
___
##### Alcuni esempi di applicazione del calcolo combinatorio

In questo paragrafo, andiamo a vedere alcuni **esempi classici** di applicazione del calcolo combinatorio nel calcolo delle probabilità.

Partiamo con il cosiddetto "**problema del compleanno**": si vuole sapere qual è la probabilità che, tra $M$ persone scelte a caso, ve ne siano almeno due che festeggiano il compleanno nello stesso giorno (supponendo che l'anno sia sempre di $365$ giorni, e che tutte le date siano equiprobabili). Per ottenere la nostra soluzione, pensiamo "al contrario": per trovare la probabilità che almeno due persone festeggino il compleanno nello stesso giorno, possiamo trovare invece quella per cui nessuno festeggi il compleanno nello stesso giorno, e sottrarla alla probabilità totale. Dunque, concentriamoci sul calcolare la probabilità del seguente evento:
$$\overline{E}=\{\text{Le M persone festeggiano tutte il compleanno in giorni diversi}\}$$
Lo spazio campione $\Omega$, dunque l'insieme degli eventi elementari possibili di questo esperimento, è costituito dalle [[CDP_02 - La probabilità#Disposizioni con ripetizione|disposizioni con ripetizione]] di classe $M$ di $365$ elementi (i giorni dell'anno); dunque, lo spazio $\Omega$ ha cardinalità $365^{M}$. Al tempo stesso, si deduce subito che $\overline{E}$ è un [[CDP_01 - Eventi#Eventi elementari e composti|evento composto]], costituito da tutte le disposizioni senza ripetizione di classe $M$ di $365$ elementi; dunque, $\overline{E}$ ha cardinalità $\frac{365!}{(365-M)!}$. Avendo preposto che tutte le date hanno uguale probabilità di essere il compleanno di uno degli individui considerati, sappiamo di trovarci in una [[CDP_02 - La probabilità#Probabilità "uniformi" e calcolo combinatorio|distribuzione di probabilità uniforme]], e dunque possiamo affermare che:
$$\mathbb{P}(\overline{E})=\frac{|\overline{E}|}{|\Omega|}=\frac{\frac{365!}{(365-M)!}}{365^{M}}=\frac{365\cdot 364\cdot\,\dots\,\cdot(365-M+1)}{365^{M}}$$
A questo punto, avendo trovato la probabilità $\mathbb{P}(\overline{E})$ dell'evento complementare a quello $E$ che ci viene chiesto dal problema, avremo che $\mathbb{P}(E)=1-\mathbb{P}(\overline{E})$. Indichiamo, da questo momento in poi, tale probabilità come $\mathbb{P}_{M}(E)$, per evidenziare la sua dipendenza dal valore di $M$, e osserviamo un fenomeno interessante: già per $M\ge 23$, dunque considerando almeno $23$ persone nell'esperimento, troviamo che $\mathbb{P}_{M}(E)>0.5$, dunque basta considerare $23$ persone casuali per avere una possibilità di più del $50\%$ che almeno $2$ di esse facciano il compleanno nello stesso giorno. 

Vediamo, ora, un ulteriore esempio, che viene chiamato "**paradosso del Cavalier De Méré**". La domanda alla base del paradosso è la seguente: è più probabile ottenere almeno un $1$ in $4$ lanci consecutivi di un dado o ottenere un doppio $1$ in $24$ lanci consecutivi di una coppia di dadi? Anche in questo caso, per ottenere la risposta converrà agire calcolando prima la probabilità degli eventi complementari a quelli cercati:
$$\mathbb{P}(\{\text{almeno un 1 in 4 lanci di un dado}\})=1-\mathbb{P}(\{\text{nessun 1 in 4 lanci di un dado}\})$$
$$\mathbb{P}(\{\text{almeno un doppio 1 in 24 lanci di una coppia di dadi}\})=1-\mathbb{P}(\{\text{nessun doppio 1 in 24 lanci di una coppia di dadi}\})$$
Partiamo con il calcolo della prima probabilità complementare, dunque della probabilità di non ottenere nemmeno un $1$ in $4$ lanci di un singolo dado a $6$ facce. Lo spazio $\Omega$ dei $4$ lanci del dado consiste nell'insieme delle disposizioni con ripetizione di classe $4$ di $6$ elementi, ossia l'insieme delle quaterne ordinate $(x_{1},\,x_{2},\,x_{3},\,x_{4})$ con $x_{i}\in\{1,\,2,\,3,\,4,\,5,\,6\}$: dunque, abbiamo che $|\Omega|=6^{4}$. Gli eventi elementari che costituiscono l'evento composto che stiamo considerando, invece, corrispondono alle disposizioni con ripetizione di classe $4$ di $5$ elementi, dato che si rimuove l'opzione di ottenere $1$: dunque, abbiamo che la cardinalità di tale evento composto è di $5^{4}$. A questo punto, essendo il dado bilanciato a meno di altre indicazioni, possiamo affermare che:
$$\mathbb{P}(\{\text{almeno un 1 in 4 lanci di un dado}\})=1-\frac{6^{4}}{5^{4}}\approx 0.52$$
Un procedimento analogo può essere utilizzato per la seconda sotto-soluzione cercata: l'unico accorgimento da fare è che il numero di lanci aumenta da $4$ a $24$, e che il numero di "elementi" non è più $6$, ossia i possibili risultati del lancio di un singolo dado, ma $36$, ossia i possibili risultati (ordinati) del lancio di una coppia di dadi. Applicando questi accorgimenti al medesimo procedimento, arriviamo a:
$$\mathbb{P}(\{\text{almeno un doppio 1 in 24 lanci di una coppia di dadi}\})=1-\frac{35^{24}}{36^{24}}\approx 0.49$$
Dunque, abbiamo ottenuto che è più probabile ottenere almeno un $1$ in $4$ lanci consecutivi di un singolo dado piuttosto che ottenere un doppio $1$ in $24$ lanci consecutivi di una coppia di dadi.

Vediamo un ultimo esempio. Supponiamo di avere un gruppo di $4n$ persone, che comprende $2n$ ragazzi e $2n$ ragazze, e di voler formare casualmente $2$ squadre formate ciascuna da $2n$ persone. Si vuole sapere la probabilità che tutte le ragazze vengano messe in una squadra e tutti i ragazzi nell'altra, così come la probabilità che ciascuna squadra sia perfettamente divisa tra $n$ ragazzi e $n$ ragazze. Lo spazio $\Omega$ di questo esperimento sarà dato dal numero di modi di scegliere $2n$ individui tra le $4n$ persone totali, e dunque abbiamo che $|\Omega|=\binom{4n}{2n}$. Stabilito ciò, pensiamo alla prima incognita: per sapere la probabilità che le $2$ squadre siano perfettamente divise in base al genere, possiamo intuire che le uniche scelte (gli unici eventi elementari, insomma) che permettono ciò sono quella in cui si scelgono solo ragazzi e quella in cui si scelgono solo ragazze; dunque, abbiamo $2$ casi favorevoli tra gli $|\Omega|$ casi possibili, per cui:
$$\mathbb{P}(\{\text{tutte le ragazze in una squadra e tutti i ragazzi nell'altra}\})=\frac{2}{\binom{4n}{2n}}$$
Passiamo, ora, alla seconda incognita: scegliere una squadra composta perfettamente da $n$ ragazzi e $n$ ragazze significa scegliere precisamente $n$ ragazzi tra i $2n$ ragazzi totali e $n$ ragazze tra le $2n$ ragazze totali, dunque questa scelta può essere eseguita in $\binom{2n}{n}\binom{2n}{n}$ modi, che corrispondono di conseguenza agli eventi favorevoli. Perciò, si ottiene che:
$$\mathbb{P}(\{\text{squadra composta da n ragazzi e n ragazze}\})=\frac{\binom{2n}{n}\binom{2n}{n}}{\binom{4n}{2n}}$$
___
## Il problema delle concordanze

Supponiamo di avere la seguente situazione: una segretaria ha $n$ lettere indirizzate a $n$ persone distinte, e $n$ buste con già scritti gli indirizzi di tali persone in cui dovrà inserire le lettere. Se l'inserimento delle lettere nelle buste avvenisse in modo casuale, quale sarebbe la probabilità $p(n)$ che nessuna lettera finisca nella busta corrispondente? E quanto varrebbe, invece, la probabilità che $q(n)$ che almeno una lettera venga inserita nella busta giusta?

Nel contesto del nostro esempio, affermiamo che c'è una "**concordanza**" nel momento in cui una lettera viene messa nella busta corrispondente: dunque, la probabilità $p(n)$ è quella che non si verifichino concordanze, mentre $q(n)$ è la probabilità che ci sia almeno una concordanza. Va da sé che le due probabilità sono una il complemento dell'altra, e dunque vale che:
$$p(n)=1-q(n)$$
Si tratta di un problema classico e ricorrente, che può avere anche altre interpretazioni, ma che può sempre essere ricondotto alla seguente riformulazione: data un'urna contenente $n$ palline numerate da $1$ a $n$, si estraggono le palline una alla volta, e se per un $h\in\{1,\,2,\,\dots,\,n\}$ si estrae la pallina col numero $h$ proprio all'estrazione $h$-esima, allora avviene una concordanza. Si precisa che stiamo assumendo che lo spazio $\Omega$ sia l'insieme di tutte le permutazioni $(j_{1},\,j_{2},\,\dots,\,j_{n})$, dunque dei possibili ordini di estrazione delle palline, e si ha almeno una concordanza se $j_{h}=h$ per almeno un $h\in\{1,\,2,\,\dots,\,n\}$; inoltre, stiamo assumendo che tutte le permutazioni siano equiprobabili. Tornando all'esempio iniziale, la probabilità $q(n)$ diventa dunque la probabilità che si verifichi uno degli eventi del seguente tipo:
$$A_{h}=\{\text{la lettera }h\text{-esima viene inserita nella }h\text{-esima busta}\}$$
I vari eventi $A_{h}$ consistono negli eventi $\{A_{1},\,A_{2},\,\dots,\,A_{n}\}$, dunque possiamo affermare che:
$$\begin{align} q(n)&=\mathbb{P}(A_{1}\cup A_{2}\cup\,\dots\,\cup A_{n})\\&= \sum_{k\,=\,1}^{n}\left( (-1)^{k-1}\sum_{\{i_{1},\,i_{2},\,\dots,\,i_{k}\}}\mathbb{P}(A_{i_{1}}\cap A_{i_{2}}\cap\,\dots\,\cap A_{i_{k}}) \right) \end{align}$$
Ora, qualunque sia la combinazione $\{i_{1},\,i_{2},\,\dots,\,i_{k}\}$, possiamo dimostrare che $\mathbb{P}(A_{i_{1}}\cap A_{i_{2}}\cap\,\dots\,\cap A_{i_{k}})=\frac{(n-k)!}{n!}$: [pag. 36]. Di conseguenza, si ha che:
$$\sum_{\{i_{1},\,i_{2},\,\dots,\,i_{k}\}}\mathbb{P}(A_{i_{1}}\cap A_{i_{2}}\cap\,\dots\,\cap A_{i_{k}})=\frac{1}{k!}$$
dato che la sommatoria $\sum_{\{i_{1},\,i_{2},\,\dots,\,i_{k}\}}$ corrisponde alla somma fatta su tutte le $\binom{n}{k}=\frac{n!}{k!(n-k)!}$ combinazioni $\{i_{1},\,i_{2},\,\dots,\,i_{k}\}$ degli $n$ elementi $\{1,\,2,\,\dots,\,n\}$, e perciò abbiamo che:
$$\sum_{\{i_{1},\,i_{2},\,\dots,\,i_{k}\}}\mathbb{P}(A_{i_{1}}\cap A_{i_{2}}\cap\,\dots\,\cap A_{i_{k}})=\frac{n!}{k!(n-k)!}\cdot \frac{(n-k)!}{n!}= \frac{1}{k!}$$
Avendo ottenuto tale equivalenza, possiamo tornare al problema principale. La probabilità $q(n)$ che avvenga almeno una concordanza è pari a:
$$\begin{align} q(n)&=\frac{1}{1!}-\frac{1}{2!}+\frac{1}{3!}-\frac{1}{4!}+\,\dots\,+(-1)^{n-1}\frac{1}{n!} \\ &= \sum_{k\,=\,1}^{n}\left( (-1)^{k-1} \frac{1}{k!} \right)\end{align}$$
e, naturalmente, la probabilità di $p(n)$, evento complementare a $q(n)$ è uguale alla probabilità che non avvenga alcuna concordanza, è pari a:
$$\begin{align} p(n) &= 1 - q(n) \\ &= 1 - \frac{1}{1!}-\frac{1}{2!}+\frac{1}{3!}-\frac{1}{4!}+\,\dots\,+(-1)^{n-1}\frac{1}{n!} \\ &=\sum_{k\,=\,0}^{n}\left( (-1)^{k} \frac{1}{k!} \right) \end{align}$$
___
## Probabilità condizionate



[pag. 44/54]
___

