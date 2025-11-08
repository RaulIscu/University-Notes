Avendo introdotto gli [[CDP_01 - Eventi|eventi]] e le loro varie proprietà, siamo pronti per cominciare a parlare concretamente di "**probabilità**". Tale concetto permette di formalizzare meglio un problema e di esprimere lo stato di incertezza del risultato di un esperimento aleatorio.

## Misure di probabilità

> Dato uno spazio campione $\Omega$, e sia $\mathcal{P}(\Omega)$ la famiglia delle sue parti, definiamo "**misura di probabilità**" o, più semplicemente, "**probabilità su $(\Omega, \mathcal{P}(\Omega))$**", una funzione $\mathbb{P}$ che rispetta i seguenti assiomi:
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
A questo punto, procediamo ad elencare alcune **proprietà della probabilità**, che risultano in buona parte conseguenze immediate degli assiomi esposti nella [[CDP_02 - La probabilità#Misure di probabilità|definizione di misure di probabilità]]. Prima di tutto, notiamo che il terzo e ultimo assioma, ossia la proprietà dell'additività, può essere generalizzato considerando $n$ eventi disgiunti a due a due.

> La **proprietà di additività finita**, in generale, afferma che siano $E_{1},\,E_{2},\,\dots,\,E_{n}\,\in\,\mathcal{P}(\Omega)$ una serie di eventi incompatibili a due a due, allora si ha che:
> $$\mathbb{P}\left( \bigcup_{i\,=\,1}^{n}E_{i} \right)\,\,=\,\,\sum_{i\,=\,1}^{n}\mathbb{P}(E_{i})$$

[proprietà (a): pag. 19]

La prossima proprietà che analizzeremo riguarda la relazione tra **probabilità di un evento e del suo complementare**.

> Per ogni $E\,\in\,\mathcal{P}(\Omega)$, si ha che:
> $$\mathbb{P}(\overline{E})\,=\,1-\mathbb{P}(E)$$

In sostanza, ciò che afferma questa proprietà è che, dato un qualsiasi evento $E$, o accadrà tale evento $E$ o non accadrà, dato che riformulando la proprietà si ha che $\mathbb{P}(E)+\mathbb{P}(\overline{E})=1$, con $1$ che rappresenta una probabilità certa. Una conseguenza, per certi versi, di quanto appena detto è la seguente proprietà sull'**evento impossibile**:

> L'evento impossibile ha probabilità nulla, ovvero:
> $$\mathbb{P}(\emptyset)=0$$

Passiamo, ora, a definire la cosiddetta "**proprietà di monotonia**":

> Siano $A,\,B\,\in\,\mathcal{P}(\Omega)$ due eventi tali che $A\subseteq B$, allora si ha che:
> $$\mathbb{P}(A)\leq\mathbb{P}(B)$$
> Inoltre, ricordando che $B / A=B\cap\overline{A}$, si ha che:
> $$\mathbb{P}(B / A)\,=\,\mathbb{P}(B)-\mathbb{P}(A)$$

Ciò vale perché, come accennato nel [[CDP_01 - Eventi#Eventi dal punto di vista logico e insiemistico|capitolo precedente]], affermare che $A\subseteq B$ equivale a dire che ogni evento elementare che soddisfa $A$ soddisfa anche $B$, ed essendo $A$ un sottoinsieme proprio di $B$ ci sarà un numero maggiore di eventi elementari che soddisfano quest'ultimo (ossia quelli che soddisfano $A$ più altri ancora): ciò porta la probabilità $\mathbb{P}(B)$ ad essere maggiore o uguale della probabilità $\mathbb{P}(A)$.

Di seguito, esponiamo la **formula di inclusione-esclusione** nella sua forma più semplice, ossia considerando **due eventi**.

> Per due eventi arbitrari $A,\,B\,\in\,\mathcal{P}(\Omega)$, si ha che:
> $$\mathbb{P}(A\cup B)\,=\,\mathbb{P}(A)+\mathbb{P}(B)-\mathbb{P}(A\cap B)$$

Tale formula è facilmente dimostrabile riflettendo sui significati concreti di unione e intersezione: fare l'unione di due eventi $A$ e $B$ significa considerare sia tutti gli eventi di $A$ che tutti gli eventi di $B$, tuttavia nel fare ciò verranno considerati due volte gli elementi che si trovano sia in $A$ che in $B$, ossia $A\cap B$, dunque per eliminare questo eccesso basterà sottrarre tali elementi una volta. Naturalmente, nel caso in cui gli eventi considerati siano incompatibili, la loro intersezione sarà $A\cap B=\emptyset$, dunque tale operazione non sarà necessaria.

Arriviamo, infine, a un'ultima proprietà facilmente deducibile dalla definizione di **partizione dell'evento certo**.

> Siano $H_{1},\,H_{2},\,\dots,\,H_{n}\,\in\,\mathcal{P}(\Omega)$ eventi tali che vale che:
> $$\bigcup_{i\,=\,1}^{n}H_{i}=\Omega\,\,\,\,\,\bigwedge\,\,\,\,\,H_{i}\cap H_{j}=\emptyset\,\,\,\text{per }i\neq j$$
> ossia costituiscano gli eventi $H_{1},\,H_{2},\,\dots,\,H_{n}$ una [[CDP_01 - Eventi#Partizione dell'evento certo|partizione dell'evento certo]], allora si può affermare che:
> $$\sum_{i\,=\,1}^{n}\,\mathbb{P}(H_{i})=1$$

[dimostrazioni varie: pag. 21 - 22]



[pag. 23]