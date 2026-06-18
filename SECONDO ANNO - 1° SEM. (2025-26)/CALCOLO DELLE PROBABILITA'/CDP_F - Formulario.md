## Eventi

Proprietà distributiva dell'unione rispetto all'intersezione:
$$(A\cup B)\cap C\,=\,(A\cap C)\cup(B\cap C)$$
Proprietà distributiva dell'intersezione rispetto all'unione:
$$(A\cap B)\cup C\,=\,(A\cup C)\cap(B\cup C)$$
Legge di De Morgan:
$$\overline{A\cap B}=\overline{A}\cup\overline{B}\,\,\,\,\,\text{che equivale a dire che}\,\,\,\,\,A\cap B=\overline{(\overline{A}\cup\overline{B})}$$
___
## Probabilità

##### Misure di probabilità

Dato uno spazio campione $\Omega$ e la famiglia delle sue parti $\mathcal{P}(\Omega)$, definiamo "**misura di probabilità**" una funzione $\mathbb{P}$ che rispetta i seguenti assiomi:
- la funzione è definita come $\mathbb{P}:\mathcal{P}(\Omega)\rightarrow[0, 1]$;
- $\mathbb{P}(\Omega)=1$ (**condizione di normalizzazione**);
- se $E_{1}\cap E_{2}=\emptyset$, allora $\mathbb{P}(E_{1}\cup E_{2})=\mathbb{P}(E_{1})+\mathbb{P}(E_{2})$ (**proprietà di additività**).

La terna $(\Omega,\,\mathcal{P}(\Omega),\,\mathbb{P})$ viene detta "**spazio finito di probabilità**".

**Proprietà di additività finita**

> Siano $E_{1},\,E_{2},\,\dots,\,E_{n}\,\in\,\mathcal{P}(\Omega)$ una serie di eventi incompatibili a due a due, allora si ha che:
> $$\mathbb{P}\left( \bigcup_{i\,=\,1}^{n}E_{i} \right)\,\,=\,\,\sum_{i\,=\,1}^{n}\mathbb{P}(E_{i})$$

**Probabilità di un evento composto**

> Ponendo $p(\omega_{i})=\mathbb{P}(\{\omega_{i}\})$, con $i$ che va da $1$ a $N$, si ha che per ogni $E\,\in\,\mathcal{P}(\Omega)$:
> $$\mathbb{P}(E)\,=\,\sum_{i\,=\,1}^{N}p(\omega_{i})\,=\,\sum_{\omega\,\in\,E}p(\omega)$$

**Probabilità del complementare**

> Per ogni $E\,\in\,\mathcal{P}(\Omega)$, si ha che:
> $$\mathbb{P}(\overline{E})\,=\,1-\mathbb{P}(E)$$

**Probabilità dell'evento impossibile**

> **L'evento impossibile ha probabilità nulla**, ovvero:
> $$\mathbb{P}(\emptyset)=0$$

**Proprietà di monotonia**

> Siano $A,\,B\,\in\,\mathcal{P}(\Omega)$ due eventi tali che $A\subseteq B$, allora si ha che:
> $$\mathbb{P}(A)\leq\mathbb{P}(B)$$
> Inoltre, ricordando che $B / A=B\cap\overline{A}$, si ha che:
> $$\mathbb{P}(B / A)\,=\,\mathbb{P}(B)-\mathbb{P}(A)$$

**Formula di inclusione-esclusione** (per 2 eventi)

> Per due eventi arbitrari $A,\,B\,\in\,\mathcal{P}(\Omega)$, si ha che:
> $$\mathbb{P}(A\cup B)\,=\,\mathbb{P}(A)+\mathbb{P}(B)-\mathbb{P}(A\cap B)$$

**Formula di inclusione-esclusione** (generale)

> Dati $n$ eventi $A_{1},\,A_{2},\,\dots,\,A_{n}\in\mathcal{P}(\Omega)$, la probabilità che almeno uno tra tali eventi si verifichi è pari a:
> $$\mathbb{P}(A_{1}\cup A_{2}\cup\,\dots\,\cup A_{n})=\sum_{k\,=\,1}^{n}\left( (-1)^{k-1}\sum_{\{i_{1},\,i_{2},\,\dots,\,i_{k}\}}\mathbb{P}(A_{i_{1}}\cap A_{i_{2}}\cap\,\dots\,\cap A_{i_{k}})\right)$$

**Proprietà della partizione dell'evento certo**

> Siano $H_{1},\,H_{2},\,\dots,\,H_{n}\,\in\,\mathcal{P}(\Omega)$ eventi tali che vale che:
> $$\bigcup_{i\,=\,1}^{n}H_{i}=\Omega\,\,\,\,\,\bigwedge\,\,\,\,\,H_{i}\cap H_{j}=\emptyset\,\,\,\text{per }i\neq j$$
> ossia costituiscano gli eventi $H_{1},\,H_{2},\,\dots,\,H_{n}$ una partizione dell'evento certo, allora si può affermare che:
> $$\sum_{i\,=\,1}^{n}\,\mathbb{P}(H_{i})=1$$

Formula di scomposizione:
$$\text{per ogni }A\text{ e }B\text{, vale che }\mathbb{P}(A)=\mathbb{P}(A\cap B)+\mathbb{P}(A\cap\overline{B})$$
___
##### Probabilità definita a meno di un fattore di proporzionalità

1. Se c'è una relazione di proporzionalità tra gli eventi elementari, porre $p(\omega_{i})=K\cdot g_{i}$;
2. Trovare la relazione di proporzionalità specifica, e in base ad essa assegnare dei valori a $g_{i}$;
3. Porre la somma delle varie $p(\omega_{i})$ uguale a $1$, e risolvere per $K$;
4. Avendo definito $p(\omega_{i})=K\cdot g_{i}$, trovare i vari valori $p(\omega_{i})$.
___
##### Probabilità uniformi

"**Distribuzione di probabilità uniforme**" su un certo insieme di eventi = tutti quegli eventi sono equiprobabili, dunque:
$$p(\omega_{i})=\frac{1}{|\Omega|}=\frac{1}{N},\,\,\,\,\,\text{per ogni }i=1,\,2,\,\dots,\,N$$
e:
$$\mathbb{P}(E)=\frac{|E|}{|\Omega|}=\frac{|E|}{N},\,\,\,\,\,\text{per ogni }E\in\mathcal{P}(\Omega)$$
___
##### Calcolo combinatorio

**Disposizioni con ripetizione di classe $k$ di $n$ elementi** (numero di $k$-uple ordinate generabili da $n$ elementi, dove è possibile che un elemento si ripeta):
$$n^{k}$$

**Disposizioni senza ripetizione di classe $k$ di $n$ elementi** (numero di $k$-uple ordinate generabili da $n$ elementi, dove non è possibile che un elemento si ripeta):
$$D^{n}_{k}=\frac{n!}{(n-k)!}$$

**Permutazioni di $k$ elementi** (numero di possibili riordinamenti di una sequenza di $k$ elementi):
$$P_{k}=k!$$

**Combinazioni di classe $k$ di $n$ elementi** (numero di possibili sotto-insiemi di cardinalità $k$ generabili da $n$ elementi):
$$C_{k}^{n}=\frac{D^{n}_{k}}{P_{k}}=\frac{n!}{k!\,(n-k)!}:=\binom{n}{k}$$

**Proprietà del coefficiente binomiale**:
$$\binom{n}{0}=1\,\,\,\,\,\,\,\,\,\,\binom{n}{n}=1\,\,\,\,\,\,\,\,\,\,\binom{n}{k}=\binom{n}{n-k}$$
**Formula di Stiefel**:
$$\binom{n}{k}=\binom{n-1}{k-1}+\binom{n-1}{k}$$
**Corollari della formula di Stiefel**:
$$\sum_{r\,=\,k}^{n}\binom{r}{k}=\binom{n+1}{k+1}\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,(a+b)^{n}=\sum_{k\,=\,0}^{n}\binom{n}{k}a^{k}b^{n-k}\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\sum_{k\,=\,0}^{n}\binom{n}{k}=2^{n}$$
**Identità di Vandermonde**:
$$\sum_{k\,=\,max(0,\,n-s)}^{min(n,\,r)}\binom{r}{k}\binom{s}{n-k}=\binom{r+s}{n}\,\,\,\,\,\,\,\,\,\,\text{per qualsiasi }r,\,s,\,n\text{ con }n\le r+s$$
___
##### Probabilità condizionate

> Siano $E$ ed $H$ due eventi, con $\mathbb{P}(H)>0$. Viene detta "**probabilità condizionata di $E$ dato $H$**", e indicata con il simbolo $\mathbb{P}(E\,|\,H)$ la seguente quantità:
> $$\mathbb{P}(E\,|\,H)= \frac{\mathbb{P}(E\cap H)}{\mathbb{P}(H)}$$

**Formula delle probabilità composte**:
$$\mathbb{P}(E_{1}\cap E_{2}\cap\,\dots\,\cap E_{n})\,=\,\mathbb{P}(E_{1})\cdot\mathbb{P}(E_{2}\,|\,E_{1})\cdot\mathbb{P}(E_{3}\,|\,E_{1}\cap E_{2})\cdot\,\dots\,\cdot\mathbb{P}(E_{n}\,|\,E_{1}\cap E_{2}\cap\,\dots\,\cap E_{n-1})$$

**Formula delle probabilità totali**:
 
> Sia $\{H_{1},\,H_{2},\,\dots,\,H_{m}\}$ una partizione di $\Omega$, con $\mathbb{P}(H_{l})>0$ per ogni $l\in\{1,\,2,\,\dots,\,m\}$, si ha che per qualsiasi evento $E\in\mathcal{P}(\Omega)$:
> $$\mathbb{P}(E)\,=\,\mathbb{P}(E\,|\,H_{1})\,\mathbb{P}(H_{1})\,+\,\mathbb{P}(E\,|\,H_{2})\,\mathbb{P}(H_{2})\,+\,\dots\,+\,\mathbb{P}(E\,|\,H_{m})\,\mathbb{P}(H_{m})$$
> o, più in breve:
> $$\mathbb{P}(E)=\sum_{k\,=\,1}^{m}\mathbb{P}(E\,|\,H_{k})\,\mathbb{P}(H_{k})$$

**Formula di Bayes**:

> Sia $\{H_{1},\,H_{2},\,\dots,\,H_{m}\}$ una partizione di $\Omega$, con $\mathbb{P}(H_{l})>0$ per ogni $l\in\{1,\,2,\,\dots,\,m\}$. Si ha che, per un qualsiasi evento $E\in\mathcal{P}(\Omega)$:
> $$\mathbb{P}(H_{l}\,|\,E)=\frac{\mathbb{P}(E\,|\,H_{l})\cdot\mathbb{P}(H_{l})}{\sum_{r\,=\,1}^{m}\mathbb{P}(E\,|\,H_{r})\mathbb{P}(H_{r})}$$
___
## Correlazione e indipendenza tra eventi

##### Correlazione e indipendenza tra due eventi

> Siano $A$ e $B$ due eventi, con $\mathbb{P}(A)>0$ e $\mathbb{P}(B)>0$, tali eventi si dicono "**correlati positivamente**" se vale che:
> $$\mathbb{P}(A\,|\,B)>\mathbb{P}(A)$$
> Tale relazione è equivalente alla seguente:
> $$\mathbb{P}(A\cap B)\,>\,\mathbb{P}(A)\cdot\mathbb{P}(B)$$

> Siano $A$ e $B$ due eventi, con $\mathbb{P}(A)>0$ e $\mathbb{P}(B)>0$, tali eventi si dicono "**correlati negativamente**" se vale che:
> $$\mathbb{P}(A\,|\,B)<\mathbb{P(A)}$$
> Tale relazione è equivalente alla seguente:
> $$\mathbb{P}(A\cap B)\,<\,\mathbb{P}(A)\cdot\mathbb{P}(B)$$

> Due eventi $A$ e $B$ si dicono "**stocasticamente indipendenti**" se vale che:
> $$\mathbb{P}(A\cap B)\,=\,\mathbb{P}(A)\cdot\mathbb{P}(B)$$
___
##### Indipendenza tra partizioni

 > Siano $\mathcal{A}=\{A_{1},\,A_{2},\,\dots,\,A_{n}\}$ e $\mathcal{B}=\{B_{1},\,B_{2},\,\dots,\,B_{m}\}$ due diverse partizioni finite di uno stesso spazio campione $\Omega$. Si ha che $\mathcal{A}$ e $\mathcal{B}$ sono due "**partizioni indipendenti**", se, per ogni $i\in\{1,\,2,\,\dots,\,n\}$ e $j\in\{1,\,2,\,\dots,\,m\}$ vale che:
> $$A_{i}\,\bot \,B_{j}$$
___
##### Algebra generata da una famiglia di eventi

> Una famiglia $\mathcal{G}$ di eventi di $\Omega$, dunque tale per cui $\mathcal{G}\subseteq\mathcal{P}(\Omega)$, è un "**algebra**" se sono verificate le seguenti proprietà:
> 1. $\Omega\in\mathcal{G}$;
> 2. $E\in\mathcal{G}\,\Rightarrow\,\overline{E}\in\mathcal{G}$;
> 3. $E_{1},\,E_{2}\in\mathcal{G}\,\Rightarrow\,E_{1}\cup E_{2}\in\mathcal{G}$.

> Sia $\mathcal{A}=\{A_{1},\,A_{2},\,\dots,\,A_{n}\}$ una famiglia di eventi in uno spazio campione $\Omega$; definiamo "**algebra generata da $\mathcal{A}$**" la famiglia $\mathcal{G}(\mathcal{A})$ di eventi di $\Omega$ caratterizzata dalle seguenti proprietà:
> 1. $\mathcal{G}(\mathcal{A})$ è un'algebra;
> 2. $\mathcal{A}\subseteq\mathcal{G}(\mathcal{A})$;
> 3. se $\mathcal{C}\subseteq\mathcal{P}(\Omega)$ è un'algebra e $\mathcal{A}\subseteq\mathcal{C}$, allora $\mathcal{G}(\mathcal{A})\subseteq\mathcal{C}$.
___
##### Indipendenza completa

> Sia $\{E_{1},\,E_{2},\,\dots,\,E_{n}\}$ una famiglia di eventi in uno stesso spazio di probabilità, e consideriamo le varie partizioni $\mathcal{P}_{1}=\{E_{1},\,\overline{E_{1}}\},\,\mathcal{P}_{2}=\{E_{2},\,\overline{E_{2}}\},\,\dots,\,\mathcal{P}_{n}=\{E_{n},\,\overline{E_{n}}\}$ di tale spazio. Gli eventi $E_{1},\,E_{2},\,\dots,\,E_{n}$ si dicono una famiglia di eventi "**completamente indipendenti**", o "**globalmente indipendenti**", se per ogni $m$ tale che $2\le m\le n$, comunque siano presi degli indici $\{j_{1},\,j_{2},\,\dots,\,j_{m}\}$ dall'insieme $\{1,\,2,\,\dots,\,n\}$ e comunque siano scelti degli eventi $\tilde{E_{j_{i}}}\in\mathcal{P}_{j_{i}}$ (dunque, $\tilde{E_{j_{i}}}=E_{j_{i}}$ oppure $\tilde{E_{j_{i}}}=\overline{E_{j_{i}}}$), si ha che:
> $$\mathbb{P}(\tilde{E_{j_{1}}}\cap\tilde{E_{j_{2}}}\cap\,\dots\,\cap\tilde{E_{j_{m}}})\,=\,\mathbb{P}(\tilde{E_{j_{1}}})\cdot\mathbb{P}(\tilde{E_{j_{2}}})\cdot\,\dots\,\cdot\mathbb{P}(\tilde{E_{j_{m}}})$$

**Condizioni equivalenti**: 
1. se consideriamo solo casi in cui $\tilde{E_{j_{i}}}=E_{j_{i}}$, dunque in cui si lavora solo con gli eventi effettivi e non con i loro complementari, allora abbiamo che:
$$\mathbb{P}(E_{j_{1}}\cap E_{j_{2}}\cap\,\dots\,\cap E_{j_{m}})\,=\,\mathbb{P}(E_{j_{1}})\cdot\mathbb{P}(E_{j_{2}})\cdot\,\dots\,\cdot\mathbb{P}(E_{j_{m}})$$
       per ogni sottoinsieme $\{j_{1},\,j_{2},\,\dots,\,j_{m}\}$ di $\{1,\,2,\,\dots,\,n\}$ e considerando $2\le m\le n$ (si tratterà di valutare $2^{n} -n-1$ condizioni, dato che si hanno $2^{n}$ sottoinsiemi totali di $\{1,\,2,\,\dots,\,n\}$ a cui vanno sottratti gli $n$ singoletti, dato che $m$ deve essere almeno pari a $2$, e l'insieme vuoto $\emptyset$, per lo stesso ragionamento);
2. se consideriamo il caso in cui $m=n$, ma lasciando che $\tilde{E_{j_{i}}}$ possa rappresentare sia l'evento $E_{j_{i}}$ che il suo complementare:
$$\mathbb{P}(\tilde{E_{1}}\cap \tilde{E_{2}}\cap\,\dots\,\cap \tilde{E_{n}})\,=\,\mathbb{P}(\tilde{E_{1}})\cdot\mathbb{P}(\tilde{E_{2}})\cdot\,\dots\,\cdot\mathbb{P}(\tilde{E_{n}})$$
       si tratterà di valutare $2^{n}$ condizioni.

Infine, se volessimo verificare la condizione principale, quella che effettivamente definisce l'indipendenza completa ad esempio tra $3$ eventi, si dovrebbero verificare sia le $2^{n}$ sotto-condizioni appena indicate, sia le altre $12$ sotto-condizioni corrispondenti a tutte le possibili combinazioni di classe $2$ di intersezioni tra i $3$ eventi e i loro complementari.
___
##### Prove bernoulliane

> Gli eventi $E_{1},\,E_{2},\,\dots,\,E_{n}$ costituiscono delle "**prove bernoulliane**" se sussiste un'[[CDP_03 - Correlazione e indipendenza tra eventi#Indipendenza completa e prove bernoulliane|indipendenza completa]] tra di loro e se tutti hanno una stessa probabilità $\theta$, con $0<\theta<1$.
___