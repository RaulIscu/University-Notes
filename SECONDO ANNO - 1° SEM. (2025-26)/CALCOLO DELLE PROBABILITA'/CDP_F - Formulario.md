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
> 4. $\mathcal{G}(\mathcal{A})$ è un'algebra;
> 5. $\mathcal{A}\subseteq\mathcal{G}(\mathcal{A})$;
> 6. se $\mathcal{C}\subseteq\mathcal{P}(\Omega)$ è un'algebra e $\mathcal{A}\subseteq\mathcal{C}$, allora $\mathcal{G}(\mathcal{A})\subseteq\mathcal{C}$.
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
## Probabilità binomiali e ipergeometriche

##### Probabilità binomiali

Una **distribuzione binomiale di parametri $n$ e $\theta$** è caratteristica di un insieme di $n$ prove bernoulliane, tutte aventi probabilità $\theta$. La misura di probabilità corrispondente è:
$$\mathbf{P}:\mathcal{P}(\{0,\,1,\,\dots,\,n\})\rightarrow[0,\,1],\,\,\,I \mapsto \mathbf{P}(I):=\sum_{k\,\in\,I}p(k)$$
dove $p(k)=\binom{n}{k}\theta^{k}(1-\theta)^{n-k}$ e $0\le k\le n$.

La principale applicazione concreta delle probabilità binomiali, indicate anche come $Bin(n,\,\theta)$, è nell'**estrazione con reinserimento da un'urna**: supponendo di avere $M$ palline nell'urna, con $m_{1}$ palline di tipo $A$ e $m_{2}=M-m_{1}$ palline di tipo $B$, possiamo considerare i vari eventi
$$A_{i}=\{\text{l'oggetto estratto nell'}i\text{-esima estrazione è di tipo A}\}$$
Gli eventi $A_{i}$ sono prove bernoulliane, con probabilità $\theta=\frac{m_{1}}{M}$. Ora, indicando con $X_{i}$ la seguente quantità:
$$X_{i}=\begin{cases}1&\text{se si verifica }A_{i}\\0&\text{se si verifica }\overline{A_{i}}\end{cases}$$
e considerando:
$$S_{n}=\sum_{i\,=\,1}^{n}X_{i}$$
dove $S_{n}$ rappresenta il numero di elementi di tipo $A$ estratti nell'estrazione casuale con reinserimento di $n$ elementi considerata, possiamo affermare che:
$$\mathbb{P}(\{S_{n}=k\})=\binom{n}{k}\left( \frac{m_{1}}{M} \right)^{k}\left( \frac{m_{2}}{M} \right)^{n-k}$$
___
##### Probabilità ipergeometriche

Una **distribuzione ipergeometrica di parametri $M$, $m_{1}$ e $n$**, indicata anche come $Hyp(M,\,m_{1},\,n)$, è caratteristica delle **estrazioni senza reinserimento da un'urna**: supponendo di avere $M$ palline nell'urna, con $m_{1}$ palline di tipo $A$ e $m_{2}=M-m_{1}$ palline di tipo $B$, possiamo considerare i vari eventi
$$A_{i}=\{\text{l'oggetto estratto nell'}i\text{-esima estrazione è di tipo }A\}$$
Ora, indicando con $X_{i}$ la seguente quantità:
$$X_{i}=\begin{cases} 1&\text{se si verifica }A_{i}\\0&\text{se si verifica }\overline{A_{i}} \end{cases}$$
e considerando:
$$S_{n}=\sum_{i\,=\,1}^{n}X_{i}$$
dove $S_{n}$ rappresenta il numero di elementi di tipo $A$ estratti nell'estrazione casuale senza reinserimento di $n$ elementi considerata, possiamo affermare che:
$$\mathbb{P}(\{S_{n}=k\})=\begin{cases} \frac{\binom{m_{1}}{k}\binom{m_{2}}{n\,-\,k}}{\binom{M}{n}}&\text{per }max(0,\,n+m_{1}-M)\le k\le min(n,\,m_{1}) \\0&\text{altrimenti}\end{cases}$$
Nel caso delle estrazioni senza reinserimento le probabilità di estrarre un oggetto di tipo $A$ all'$i$-esima estrazione sono tutte pari alla probabilità di estrarre un oggetto di tipo $A$ alla prima estrazione, e dunque hanno lo stesso valore delle analoghe probabilità calcolate nel caso delle estrazioni con reinserimento:
$$\mathbb{P}(A_{i})=\frac{m_{1}}{M}$$
___
## Variabili aleatorie

> Sia $\Omega$ un insieme finito. Un'applicazione:
> $$X:\Omega\rightarrow X(\Omega)\subseteq\mathbb{R}$$
> viene detta "**variabile aleatoria**" definita su $(\Omega,\,\mathcal{P}(\Omega))$.

> La funzione:
> $$p_{X}:X(\Omega)\rightarrow[0,\,1]\subset\mathbb{R};\,\,\,\,\,x\mapsto p_{X}(x):=\mathbb{P}(\{X=x\})$$
> viene detta "**densità discreta di $X$**".

> La misura di probabilità $\mathbf{P}_{X}(\cdot)$ su $\mathcal{P}(X(\Omega))$, definita equivalentemente come:
> $$\mathbf{P}_{X}(A)=\mathbb{P}(X\,\in\,A)$$
> o come:
> $$\mathbf{P}_{X}(A)=\sum_{l\,:\,x_{l}\,\in\,A}p_{X}(x_{l})$$
> prende il nome di "**distribuzione di probabilità della variabile aleatoria $X$**".

##### Variabili aleatorie degeneri e binarie

> Una variabile aleatoria $X$, definita su $\Omega$, è una "**variabile aleatoria degenere**" se esiste $\overline{x}\in\mathbb{R}$ tale per cui $X(\Omega)=\{\overline{x}\}$.

> Una variabile aleatoria $X$, definita su $\Omega$, è una "**variabile aleatoria binaria**" se $X(\Omega)=\{0,\,1\}$.

> Sia $E\in\mathcal{P}(\Omega)$ un qualsiasi evento, e sia $1_{E}$ la funzione definita nel modo seguente:
> $$1_{E}(\omega)=\begin{cases} 1&\text{per }\omega\in E\,\,\,\,\,\text{(cioè se si è verificato l'evento E)}\\0&\text{per }\omega\not\in E\,\,\,\,\,\text{(cioè se non si è verificato l'evento E)} \end{cases}$$
> Possiamo affermare che la funzione $1_{E}$, chiamata "**indicatore di $E$**", o anche "**funzione indicatrice di $E$**", costituisce un esempio di variabile aleatoria binaria.

La **distribuzione di una variabile aleatoria binaria** $X=1_{E}$, ponendo $p=\mathbb{P}(E)$, è individuata ovviamente dal fatto che $X(\Omega)=\{0,\,1\}$, e di conseguenza da:
$$\begin{align} &p_{1}=p_{X}(1)=p\\&p_{0}=p_{X}(0)=1-p \end{align}$$
Una distribuzione del genere viene detta "**distribuzione di Bernoulli di parametro $p$**", e si scrive anche $X\sim Bern(p)$.

> Una qualunque variabile aleatoria $X$ può essere riscritta come una **combinazione lineare delle variabili aleatorie binarie di tipo $1_{H_{k}^{X}}$**. Infatti, posto $X(\Omega)=\{x_{1},\,x_{2},\,\dots,\,x_{n}\}$ l'insieme dei valori assumibili da $X$, e considerata la partizione $\mathcal{H}^{X}=\{H_{1}^{X},\,H_{2}^{X},\,\dots,\,H_{n}^{X}\}$ generata da $X$, tale per cui:
> $$H_{l}^{X}=\{X=x_{l}\}\,\,\,\,\,\text{con }l=1,\,2,\,\dots,\,n$$
> allora si ha che:
> $$X(\omega)=\sum_{k\,=\,1}^{n}x_{k}\,1_{H_{k}^{X}}(\omega)$$
___
##### Variabili aleatorie binomiali


> Siano $E_{1},\,E_{2},\,\dots,\,E_{n}$ degli eventi in uno spazio $(\Omega,\,\mathcal{P}(\Omega))$, e indicati con $X_{1},\,X_{2},\,\dots,\,X_{n}$ i loro rispettivi indicatori, si può definire sullo stesso spazio anche la variabile aleatoria $S_{n}=\sum_{h\,=\,1}^{n}X_{h}$, e si ha dunque che:
> $$S_{n}(\omega_{i})=\sum_{h\,=\,1}^{n}X_{h}(\omega_{i})=\sum_{h\,=\,1}^{n}1_{E_{h}}(\omega_{i})$$

Nel concreto, naturalmente, $S_{n}$ assume il significato di **numero di successi tra gli eventi $E_{1},\,E_{2},\,\dots,\,E_{n}$**. Supponiamo di avere $n$ prove bernoulliane, ciascuna di probabilità $\theta$ (con $0<\theta<1$); consideriamo, a questo punto, la variabile aleatoria $S_{n}=\{\text{numero di successi sulle }n\text{ prove}\}$. Naturalmente, i valori che può assumere tale variabile aleatoria sono $S_{n}(\Omega)=\{0,\,1,\,\dots,\,n\}$, e si ha che:
$$p_{S_{n}}(k)=\mathbb{P}(\{S_{n}=k\})=\binom{n}{k}\,\theta^{k}\,(1-\theta)^{n-k}$$
In casi del genere, si dice che $S_{n}$ segue una **distribuzione binomiale di parametri $n$ e $\theta$**, proprietà che scriviamo come $S_{n}\sim Bin(n,\,\theta)$.
___
##### Variabili aleatorie ipergeometriche

Supponiamo di effettuare $n$ **estrazioni casuali senza reinserimento** da una popolazione che contiene complessivamente $M$ elementi, di cui $m_{1}$ elementi sono di tipo $A$ e $m_{2}=M-m_{1}$ elementi sono di tipo $B$. Consideriamo, ora, la variabile aleatoria $S_{n}=\{\text{numero di elementi di tipo }A$$\text{ estratti dopo }n\text{ estrazioni}\}$. Si ha che:
$$p_{S_{n}}(k)=\mathbb{P}(\{S_{n}=k\})=\frac{\binom{m_{1}}{k}\binom{m_{2}}{n-k}}{\binom{M}{n}}$$
per qualsiasi $k$ tale per cui $0\le k\le m_{1}$ e $0\le n-k\le m_{2}$. In casi del genere, si dice che $S_{n}$ segue una **distribuzione ipergeometrica di parametri $M$, $m_{1}$ e $n$**, proprietà che scriviamo come $S_{n}\sim Hyp(M,\,m_{1},\,n)$.
___
##### Variabili aleatorie a valori interi

> Per una variabile aleatoria $X$ a valori interi, cioè tale per cui $X(\Omega)\subseteq\mathbb{Z}$, può essere spesso conveniente calcolare la distribuzione di probabilità tenendo conto della relazione:
> $$\mathbb{P}(X=k)=\mathbb{P}(X\le k)-\mathbb{P}(X\le k-1)$$
> Al tempo stesso, può tornare utile anche la seguente equivalenza:
> $$\begin{align} \mathbb{P}(X=k)&=\mathbb{P}(X\ge k)-\mathbb{P}(X\ge k+1) \\&= \mathbb{P}(X>k-1)-\mathbb{P}(X>k) \end{align}$$
___
##### Variabili aleatorie geometriche

Consideriamo una successione di prove bernoulliane $\{E_{1},\,E_{2},\,\dots\}$ di probabilità $\theta$ (con $0<\theta<1$). Siano $X_{1},\,X_{2},\,\dots$ le corrispondenti variabili aleatorie indicatrici, e sia $T$ la variabile aleatoria definita da:
$$T:=min\{n\ge 1\,|\,X_{n}=1\}$$
ossia la variabile aleatoria che indica **il numero minimo di prove da effettuare per ottenere un successo**, o in altre parole il "**tempo di primo successo**". Si dice che la variabile $T$ segue una "**distribuzione geometrica di parametro $\theta$**", e si utilizza la notazione $T\sim Geom(\theta)$.

La densità discreta di $T$ è:
$$p_{T}(k)\,=\,\mathbb{P}(T=k)\,=\,(1-\theta)^{k-1}\,\theta$$

Considerando, invece, la variabile aleatoria $T'$ definita come **il numero di insuccessi prima del primo successo**, si ha che:
$$p_{T'}(k)\,=\,\mathbb{P}(T'=k)\,=\,\mathbb{P}(T=k+1)\,=\,(1-\theta)^k\,\theta$$
___
##### Variabili aleatorie di Pascal

tempo di r-esimo successo 
$$\mathbb{P}(X=k)=\binom{k-1}{r-1}\,\theta^{r}\,(1-\theta)^{k-r}$$
___
##### Trasformazioni di variabili aleatorie

Avendo una variabile aleatoria $X$, e un'ulteriore variabile $Z=h(X)$, dunque una funzione della variabile aleatoria $X$, per ottenere più informazioni su $Z$ si potrà:
1. ricavare $Z(\Omega)$ a partire da $X(\Omega)$, applicando la funzione $h$ a tutti i singoli valori contenuti in $X(\Omega)$;
2. ricavare le densità discrete di $Z$, sommando per ogni valore in $Z(\Omega)$ le probabilità dei valori corrispondenti in $X(\Omega)$.
___
##### Distribuzioni congiunte di più variabili aleatorie

D'ora in poi, per comodità la notazione $\{X=x_{i}\}\cap\{Y=y_{j}\}$ potrebbe essere sostituita con $\{X=X_{i},\,Y=y_{j}\}$.

> La funzione:
> $$X(\Omega)\times Y(\Omega)\rightarrow[0,\,1];\,\,\,\,\,(x_{i},\,y_{j})\mapsto p_{X,\,Y}(x_{i},\,y_{j})$$
> prende il nome di "**densità discreta congiunta di $X$ e $Y$**".

I vari eventi $\{X=x_{1},\,Y=y_{j}\}$ formano una partizione, quindi possiamo affermare che:
$$p_{X,\,Y}(x_{i},\,y_{j})\ge 0,\,\,\,\,\,\,\,\,\,\,\sum_{i\,=\,1}^{n}\sum_{j\,=\,1}^{m}p_{X,\,Y}(x_{i},\,y_{j})=1$$
Considerate due variabili aleatorie $X$ e $Y$, e sia la loro distribuzione di probabilità congiunta individuata dalla densità discreta congiunta, ossia dalle probabilità:
$$p_{X,\,Y}(x_{i},\,y_{j})=\mathbb{P}(\{X=x_{i},\,Y=y_{j}\})$$
nel momento in cui tale distribuzione è nota, è possibile ottenere la distribuzione relativa a una sola delle due variabili considerate: tali distribuzioni vengono dette "**distribuzioni marginali**", e attribuiscono ai valori possibili di ciascuna delle due variabili aleatorie le seguenti probabilità:
$$\begin{align} &p_{X}(x_{i})=\mathbb{P}(X=x_{i})=\sum_{j\,=\,1}^{m}\mathbb{P}(\{X=x_{i},\,Y=y_{j}\})=\sum_{j\,=\,1}^{m}p_{X,\,Y}(x_{i},\,y_{j}) \\& p_{Y}(y_{j})=\mathbb{P}(Y=y_{j})=\sum_{i\,=\,1}^{n}\mathbb{P}(\{X=x_{i},\,Y=y_{j}\})=\sum_{i\,=\,1}^{n}p_{X,\,Y}(x_{i},\,y_{j})\end{align}$$
In questo contesto, la funzione $x_{i}\mapsto p_{X}(x_{i})$ viene detta "**densità discreta marginale di $X$**", mentre $y_{j}\mapsto p_{Y}(y_{j})$ viene detta "**densità discreta marginale di $Y$**".

> Le variabili $X$ e $Y$ si dicono **stocasticamente indipendenti** se
> $$\mathbb{P}(X\in I,\,Y\in J)\,=\,\mathbb{P}(X\in I)\cdot\mathbb{P}(Y\in J)$$
> per un qualsiasi $I\subseteq X(\Omega)$ e $J\subseteq Y(\Omega)$ o, equivalentemente, se le due partizioni:
> $$\mathcal{A}=\{\{X=x_{1}\},\,\{X=x_{2}\},\,\dots,\,\{X=x_{n}\}\}\,\,\,\,\,\,\,\,\,\,\mathcal{B}=\{\{Y=y_{1}\},\,\{Y=y_{2}\},\,\dots,\,\{Y=y_{m}\}\}$$
> sono indipendenti tra loro.

In altre parole, le variabili aleatorie $X$ e $Y$ sono stocasticamente indipendenti se e solo se la densità discreta congiunta è il prodotto delle densità discrete marginali.
___
## Valore atteso di una variabile aleatoria

> Sia $X:\Omega\rightarrow X(\Omega)$, con $\Omega=\{\omega_{1},\,\omega_{2},\,\dots,\,\omega_{N}\}$ una variabile aleatoria definita su $(\Omega,\,\mathcal{P}(\Omega))$; se su tale tupla è definita una probabilità $\mathbb{P}$, si può definire "**valore atteso di $X$ rispetto a $\mathbb{P}$**" il valore:
> $$\mathbb{E}(X):=\sum_{i\,=\,1}^{N}p(\omega_{i})\,X(\omega_{i})$$

##### Proprietà del valore atteso

> Se $X$ è una [[CDP_05 - Variabili aleatorie#Variabili aleatorie degeneri e binarie|variabile aleatoria degenere]], dunque tale per cui $X(\omega_{i})=\hat{x}$ per ogni $i=1,\,2,\,\dots,\,N$, allora si ha che:
> $$\mathbb{E}(X)=\hat{x}$$

> Sia $E\subseteq \Omega$ un evento, e $X=1_{E}$ la variabile aleatoria indicatrice di $E$, si ha che:
> $$\mathbb{E}(X)=\mathbb{E}(1_{E})=\mathbb{P}(E)$$

> Siano $a\le b$ due numeri reali tali che $a\le X(\omega_{i})\le b$ per ogni $i$ compreso tra $1$ e $N$, allora si ha sicuramente che:
> $$a\le\mathbb{E}(X)\le b$$

> Siano $X$ e $Y$ due variabili aleatorie, e sia $X(\omega)\le Y(\omega)$ per ogni $\omega\in \Omega$, allora si ha sicuramente che:
> $$\mathbb{E}(X)\le\mathbb{E}(Y)$$

> Siano $a$ e $b$ due numeri reali arbitrari, e $X$ e $Y$ due variabili aleatorie definite su $\Omega$. Ora, consideriamo la variabile aleatoria $Z$ definita come la **combinazione lineare di $X$ e $Y$ con coefficienti $a$ e $b$**, ossia:
> $$Z(\omega_{i})=aX(\omega_{i})+bY(\omega_{i})\,\,\,\,\,\,\,\,\,\,\text{per ogni }1\le i\le N$$
> Si ha che:
> $$\mathbb{E}(Z)=a\mathbb{E}(X)+b\mathbb{E}(Y)$$

> Sia $a$ un numero reale, e considerata una variabile aleatoria $X$ poniamo un'altra variabile $Z=a\cdot X$; risulta che:
> $$\mathbb{E}(Z)=a\cdot\mathbb{E}(X)$$

> Sia $b$ un numero reale, e considerata una variabile aleatoria $X$ poniamo un'altra variabile $Z=X+b$; risulta che:
> $$\mathbb{E}(Z)=\mathbb{E}(X)+b$$
___
##### Valore atteso di una variabile aleatoria a valori interi non negativi

> Sia $X(\Omega)\subseteq\{0,\,1,\,\dots,\,n\}$; allora si ha:
> $$\mathbb{E}(X)=\sum_{j\,=\,0}^{n\,-\,1}\mathbb{P}(\{X>j\})$$
> In particolare, se $X(\Omega)=\{1,\,2,\,\dots,\,n\}$, allora si ha:
> $$\mathbb{E}(X)=1+\sum_{j\,=\,1}^{n\,-\,1}\mathbb{P}(\{X>j\})$$
___
##### Valori attesi notevoli

Valore atteso di una variabile aleatoria $X$ che segue una **distribuzione uniforme**, dove $a$ è il valore più piccolo possibile e $b$ è il valore più grande possibile:
$$\mathbb{E}(X)=\frac{a+b}{2}$$

Valore atteso di una variabile aleatoria $X$ che segue una **distribuzione bernoulliana di parametro $\theta$** (successo di un evento avente probabilità $\theta$):
$$\mathbb{E}(X)=\theta$$

Valore atteso di una variabile aleatoria $X$ che segue una **distribuzione binomiale di parametri $n$ e $\theta$** (numero di successi su $n$ prove bernoulliane con probabilità $\theta$):
$$\mathbb{E}(X)=n\cdot\theta$$

Valore atteso di una variabile aleatoria $X$ che segue una **distribuzione ipergeometrica di parametri $M$, $m_{1}$ e $n$** (numero di elementi di tipo $A$, con $|A|=m_{1}$, estratti da $M$ elementi totali in $n$ estrazioni senza reinserimento):
$$\mathbb{E}(X)=n\cdot \frac{m_{1}}{M}$$

Valore atteso di una **media aritmetica $Y_{n}$ di $n$ variabili aleatorie $X_{1},\,X_{2},\,\dots,\,X_{n}$ aventi tutte stesso valore atteso $\mu$**:
$$\mathbb{E}(Y_{n})=\mu$$

Valore atteso di una variabile aleatoria $X$ che segue una **distribuzione geometrica di parametro $\theta$** (tempo di primo successo, ossia numero di tentativi da fare per ottenere un evento di probabilità $\theta$, tentativo di successo compreso):
$$\mathbb{E}(X)=\frac{1}{\theta}$$

Valore atteso di una variabile aleatoria $X$ che segue una **distribuzione di Pascal di parametri $r$ e $\theta$** (tempo di $r$-esimo successo, ossia numero di tentativi da fare per ottenere $r$ volte un evento di probabilità $\theta$, tentativo di successo compreso):
$$\mathbb{E}(X)=\frac{r}{p}$$

[esponenziale, poisson, gaussiana]
___
##### Valore atteso condizionato e formula del valore atteso totale

> Sia $A$ un evento, con $\mathbb{P}(A)>0$, e sia $X$ una variabile aleatoria che può assumere i valori $X(\Omega)=\{x_{1},\,x_{2},\,\dots,\,x_{n}\}$, si definisce "**valore atteso di $X$ condizionato all'evento $A$**" il valore:
> $$\mathbb{E}(X\,|\,A)\,=\,\sum_{i\,=\,1}^{N}X(\omega_{i})\,\mathbb{P}(\{\omega_{i}\}\,|\,A)\,=\,\sum_{k\,=\,1}^{n}x_{k}\,\mathbb{P}(X=x_{k}\,|\,A)$$

> Data una partizione formata dagli eventi $H_{1},\,H_{2},\,\dots,\,H_{m}$, e se $\mathbb{P}(H_{j})>0$ per ogni $j=1,\,2,\,\dots,\,m$, allora vale che:
> $$\mathbb{E}(X)=\sum_{j\,=\,1}^{m}\mathbb{E}(X\,|\,H_{j})\,\mathbb{P}(H_{j})$$
___
## Varianza e covarianza

> Sia $X:\Omega\to X(\Omega)$ una variabile aleatoria, ed indicato brevemente con $\mu$ il valore atteso di $X$, si dice "**varianza** di $X$", e si indica con la notazione $Var(X)$, il valore:
> $$Var(X)\,=\,\mathbb{E}((X-\mathbb{E}(X))^{2})\,:=\,\sum_{\omega_{i\,\in\,\Omega}}p(\omega_{i})\,(X(\omega_{i})-\mu)^{2}$$
> ossia, in parole povere, il valore atteso di $(X-\mu)^{2}$.

##### Proprietà della varianza

> **La varianza di una variabile aleatoria $X$ è sempre non negativa**, ovvero:
> $$Var(X)\ge 0$$
> Inoltre, se $p(\omega_{i})>0$ per ogni $\omega_{i}\in \Omega$, allora si avrà $Var(X)=0$ se e solo se $X$ è una [[CDP_05 - Variabili aleatorie#Variabili aleatorie degeneri e binarie|variabile aleatoria degenere]].

> Per ogni variabile aleatoria $X$, è possibile calcolarne la varianza anche attraverso la seguente formula:
> $$Var(X)\,=\,\mathbb{E}(X^{2})-\mu^{2}\,=\,\mathbb{E}(X^{2})-(\mathbb{E}(X))^{2}$$

> Sia $Y=X+b$, con $b\in\mathbb{R}$, allora si ha che:
> $$Var(Y)=Var(X+b)=Var(X)$$

> Sia $Y=a\cdot X$, con $a\in\mathbb{R}$, allora si ha che:
> $$Var(Y)=Var(a\cdot X)=a^{2}\cdot Var(X)$$

> Siano $X$ e $Y$ due variabili aleatorie definite su $(\Omega,\,\mathcal{P}(\Omega))$, allora si ha che:
> $$Var(X+Y)=Var(X)+Var(Y)+2\mathbb{E}[(X-\mathbb{E}(X))(Y-\mathbb{E}(Y))]$$
___
##### Varianze notevoli

Varianza di una variabile aleatoria $X$ che segue una **distribuzione uniforme**, dove $a$ è il valore più piccolo possibile e $b$ è il valore più grande possibile:
$$Var(X)=\frac{(b-a)(b-a+2)}{12}$$

Varianza di una variabile aleatoria $X$ che segue una **distribuzione bernoulliana di parametro $\theta$** (successo di un evento avente probabilità $\theta$):
$$Var(X)=\theta\,(1-\theta)$$

Varianza di una variabile aleatoria $X$ che segue una **distribuzione binomiale di parametri $n$ e $\theta$** (numero di successi su $n$ prove bernoulliane con probabilità $\theta$):
$$Var(X)=n\cdot\theta\,(1-\theta)$$

Varianza di una variabile aleatoria $X$ che segue una **distribuzione ipergeometrica di parametri $M$, $m_{1}$ e $n$** (numero di elementi di tipo $A$, con $|A|=m_{1}$, estratti da $M$ elementi totali in $n$ estrazioni senza reinserimento), indicando con $p$ la quantità $\frac{m_{1}}{M}$:
$$Var(X)=n\cdot p\,(1-p)\,\left( 1-\frac{n-1}{M-1} \right)$$

Varianza di una **media aritmetica $Y_{n}$ di $n$ variabili aleatorie $X_{1},\,X_{2},\,\dots,\,X_{n}$ aventi tutte stessa varianza $\sigma^{2}$** (se $X_{1},\,X_{2},\,\dots,\,X_{n}$ sono indipendenti):
$$Var(Y_{n})=\frac{\sigma^{2}}{n}$$
Varianza di una **media aritmetica $Y_{n}$ di $n$ variabili aleatorie $X_{1},\,X_{2},\,\dots,\,X_{n}$ aventi tutte stessa varianza $\sigma^{2}$** (se $X_{1},\,X_{2},\,\dots,\,X_{n}$ non sono indipendenti, con covarianza $\varphi$ tra le varie coppie):
$$Var(Y_{n})=\frac{1}{n}\,[\sigma^{2}+(n-1)\varphi]$$

Varianza di una variabile aleatoria $X$ che segue una **distribuzione geometrica di parametro $\theta$** (tempo di primo successo, ossia numero di tentativi da fare per ottenere un evento di probabilità $\theta$, tentativo di successo compreso):
$$Var(X)=\frac{1-\theta}{\theta^{2}}$$

Varianza di una variabile aleatoria $X$ che segue una **distribuzione di Pascal di parametri $r$ e $\theta$** (tempo di $r$-esimo successo, ossia numero di tentativi da fare per ottenere $r$ volte un evento di probabilità $\theta$, tentativo di successo compreso):
$$Var(X)=r\cdot\frac{1-\theta}{\theta^{2}}$$

[esponenziale, poisson, gaussiana]
___
##### Covarianza di due variabili aleatorie

> Siano date, su uno stesso spazio di probabilità, due variabili aleatorie $X$ e $Y$ e, per comodità, si indichino brevemente con $\mu_{X}$ e $\mu_{Y}$ rispettivamente il valore atteso di $X$ e il valore atteso di $Y$. Si definisce "**covarianza** fra $X$ e $Y$", e si indica con la notazione $Cov(X,\,Y)$, il valore:
> $$Cov(X,\,Y)=\,\mathbb{E}[(X-\mu_{X})\cdot(Y-\mu_{Y})]$$

La covarianza fra due variabili $X$ e $Y$ si può inserire in uno dei seguenti **tre scenari**:
- **$Cov(X,\,Y)>0$** (**covarianza positiva**), caso in cui **le due variabili aleatorie considerate "viaggiano" nella stessa direzione**;
- $Cov(X,\,Y)>0$ (**covarianza negativa**), caso in cui **le due variabili aleatorie considerate "viaggiano" in direzioni opposte**;
- $Cov(X,\,Y)=0$ (**covarianza nulla**), caso in cui **la variazione di una variabile non dice nulla sulla variazione dell'altra**.

Se $Y=X$, allora la formula degenera in:
$$Cov(X,\,Y)\,=\,Cov(X,\,X)=Var(X)$$
È possibile poi ottenere una **formula alternativa per la covarianza**:
$$Cov(X,\,Y)=\mathbb{E}(X\cdot Y)-\mathbb{E}(X)\cdot\mathbb{E}(Y)$$
Inoltre, utilizzando la covarianza sarà possibile riscrivere in modo più compatto la formula per il calcolo della varianza della somma di due variabili aleatorie $X$ e $Y$:
$$Var(X+Y)=Var(X)+Var(Y)+2\,Cov(X,\,Y)$$

> Siano date due variabili aleatorie $X$ e $Y$ definite sullo stesso spazio di probabilità, e siano $X$ e $Y$ stocasticamente indipendenti tra di loro, allora:
>$$Cov(X,\,Y)=0\,\,\,\,\,\,\,\,\,\,\text{e}\,\,\,\,\,\,\,\,\,\,Var(X+Y)=Var(X)+Var(Y)$$

> Siano $X$ e $Y$ due variabili aleatorie binarie, definite su uno stesso spazio di probabilità, anche il loro prodotto $X\cdot Y$ sarà una variabile aleatoria binaria, con:
> $$\mathbb{E}(X\cdot Y)\,=\,\mathbb{P}(\{X\cdot Y=1\})=\mathbb{P}(\{X=1\}\cap\{Y=1\})$$
> Dunque, si ha che:
> $$Cov(X,\,Y)\,=\,\mathbb{P}(\{X=1\}\cap\{Y=1\})-\mathbb{P}(\{X=1\})\cdot\mathbb{P}(\{Y=1\})$$
___