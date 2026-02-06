## Cos'è una variabile aleatoria?

Un concetto importantissimo nello studio della probabilità, che contribuisce in realtà a formalizzare molte situazioni già viste anche in precedenza, è quello di "**variabile aleatoria**". Essa torna utile nell'analisi di vari fenomeni, come:
- la somma dei punteggi risultanti dal lancio di due dadi;
- il numero di votanti per uno schieramento in un sondaggio elettorale;
- il numero di successi su $n$ [[CDP_03 - Correlazione e indipendenza tra eventi#Prove bernoulliane|prove bernoulliane]];
- il massimo tra cinque numeri risultanti da un'estrazione del lotto;

e così via. Non considerando la diversa natura di tutti questi problemi, notiamo che si tratta sempre di situazioni in cui si considera **una grandezza aleatoria $X$** che rispetta le seguenti condizioni:
1. **il valore che assumerà $X$ sarà connesso**, in qualche modo, **al risultato elementare di un qualche esperimento aleatorio**;
2. **è possibile elencare i valori che possono essere assunti da $X$**;
3. sussiste una **situazione di incertezza relativamente allo specifico valore che $X$ assumerà** effettivamente, e in base alla [[CDP_02 - Probabilità#Misure di probabilità|misura di probabilità]] assegnata allo spazio campione $\Omega$ dell'esperimento considerato, si può valutare la probabilità che si presentino i vari possibili valori di $X$.

Da queste considerazioni, possiamo dare una **prima definizione provvisoria** di variabile aleatoria.

> Sia $\Omega$ un insieme finito. Un'applicazione:
> $$X:\Omega\rightarrow X(\Omega)\subseteq\mathbb{R}$$
> viene detta "**variabile aleatoria**" definita su $(\Omega,\,\mathcal{P}(\Omega))$.

Essendo $\Omega=\{\omega_{1},\,\omega_{2},\,\dots,\,\omega_{N}\}$ un insieme finito, l'immagine di $X$, ossia $X(\Omega)$, è un insieme del tipo $\{x_{1},\,x_{2},\,\dots,\,x_{n}\}$, con $x_{l}\in\mathbb{R}$ per ogni $l=1,\,2,\,\dots,\,n$ e, naturalmente, con $n\le N$. Consideriamo, ora, gli eventi $\{X=x_{l}\}$ come sottoinsiemi di $\Omega$; un tale evento si verifica se e solo se $\omega\in\{X=x_{l}\}$, o in altri termini:
$$\{X=x_{l}\}\,=\,\{\omega\in \Omega\,:\,X(\omega)=x_{l}\}\,=\,X^{-1}(\{x_{l}\})$$
Indichiamo tali eventi con i simboli $H_{1}^{X}=\{X=x_{1}\},\,H_{2}^{X}=\{X=x_{2}\},\,\dots,\,H_{n}^{X}=\{X=x_{n}\}$, ed è immediato verificare che la famiglia di eventi:
$$\mathcal{H}^{X}=\{H_{1}^{X},\,H_{2}^{X},\,\dots,\,H_{n}^{X}\}$$
costituisce una [[CDP_01 - Eventi#Partizione dell'evento certo|partizione]] di $\Omega$, detta anche **partizione generata da $X$**. Ora, proprio grazie a quest'ultimo fatto, se $\mathbb{P}:\mathcal{P}(\Omega)\rightarrow[0,\,1]$ è una probabilità, ponendo:
$$p_{X}(x_{l}):=\mathbb{P}(\{X=x_{l}\})\,\,\,\,\,\text{con }l=1,\,2,\,\dots,\,n$$
risulta che:
$$\sum_{l\,=\,1}^{n}p_{X}(x_{l})=\sum_{l\,=\,1}^{n}\mathbb{P}(\{X=x_{l}\})=1$$
> La funzione:
> $$p_{X}:X(\Omega)\rightarrow[0,\,1]\subset\mathbb{R};\,\,\,\,\,x\mapsto p_{X}(x):=\mathbb{P}(\{X=x\})$$
> viene detta "**densità discreta di $X$**".

La proprietà mostrata poco fa, relativa al fatto che la somma delle varie probabilità $\mathbb{P}(\{X=x_{l}\})$ è uguale a $1$, ci permette di definire **un nuovo spazio di probabilità**, che assume la seguente forma:
$$(X(\Omega),\,\mathcal{P}(X(\Omega)),\,\mathbf{P}_{X})$$
dove, per ogni $A\in\mathcal{P}(X(\Omega))$, la probabilità $\mathbf{P}_{X}(A)$ è definita come:
$$\mathbf{P}_{X}(A)=\sum_{l\,:\,x_{l}\,\in\,A}p_{X}(x_{l})$$
Come vedremo tra poco, vale la seguente relazione:
$$\mathbf{P}_{X}(A)=\mathbb{P}(X^{-1}(A))=\mathbb{P}(X\in A)$$
dove $X^{-1}(A)$ indica la controimmagine dell'insieme $A$ tramite la funzione $X$, ossia l'insieme $\{\omega\in \Omega:X(\omega)\in A\}$. Infatti, possiamo interpretare la probabilità $\mathbf{P}_{X}(A)$ come $\mathbb{P}(\{X\in A\})$, evento che si può scrivere come:
$$\{X\in A\}=\bigcup_{l\,:\,x_{l}\,\in\,A}\{X=x_{l}\}$$
Di conseguenza, si può affermare che:
$$\mathbb{P}(X^{-1}(A)):=\mathbb{P}(\{X\in A\})=\sum_{l\,:\,x_{l}\,\in\,A}\mathbb{P}(\{X=x_{l}\})=\sum_{l\,:\,x_{l}\,\in\,A}p_{X}(x_{l})=\mathbf{P}_{X}(A)$$
> La misura di probabilità $\mathbf{P}_{X}(\cdot)$ su $\mathcal{P}(X(\Omega))$, definita equivalentemente come:
> $$\mathbf{P}_{X}(A)=\mathbb{P}(X\,\in\,A)$$
> o come:
> $$\mathbf{P}_{X}(A)=\sum_{l\,:\,x_{l}\,\in\,A}p_{X}(x_{l})$$
> prende il nome di "**distribuzione di probabilità della variabile aleatoria $X$**".

Ovviamente, **a qualunque variabile aleatoria $X$**, definita su uno spazio di probabilità, **si può associare la relativa distribuzione di probabilità $\mathbf{P}_{X}$**. Infatti, come per qualunque altra misura di probabilità, per fare ciò basterà specificare $X(\Omega)$, ossia l'insieme dei valori che può assumere $X$, e la densità discreta $p_{X}$, ossia i vari valori $p_{X}(X_{l})=\mathbf{P}_{X}(\{x_{l}\})=\mathbb{P}(X=x_{l})$ per ogni $x_{l}\in X(\Omega)$.
___
## Variabili aleatorie degeneri e binarie

Le variabili aleatorie possono presentarsi in diverse forme, e in questo paragrafo andremo ad analizzare due tipologie particolari: le **variabili aleatorie "degeneri"** e le **variabili aleatorie "binarie"**.

> Una variabile aleatoria $X$, definita su $\Omega$, è una "**variabile aleatoria degenere**" se esiste $\overline{x}\in\mathbb{R}$ tale per cui $X(\Omega)=\{\overline{x}\}$.

In parole povere, una variabile aleatoria $X$ può essere definita degenere se esiste un valore $\overline{x}$ tale per cui $X$ assume il valore costante $\overline{x}$ su tutto $\Omega$. Sostanzialmente, una variabile aleatoria degenere rappresenta **un risultato che è certo che accada**; infatti, banalmente, la [[CDP_05 - Variabili aleatorie#Cos'è una variabile aleatoria?|distribuzione di probabilità]] di una variabile aleatoria degenere, considerato che $X(\Omega)=\{\overline{x}\}$ e che, di conseguenza, $\mathcal{P}(X(\Omega))=\{\emptyset,\,\{\overline{x}\}\}$, è definita nel modo seguente:
$$\mathbf{P}_{X}(\emptyset)=0\,\,\,\,\,\,\,\,\,\,\mathbf{P}_{X}(\{\overline{x}\})=1$$

> Una variabile aleatoria $X$, definita su $\Omega$, è una "**variabile aleatoria binaria**" se $X(\Omega)=\{0,\,1\}$.

La variabile aleatoria binaria, nel concreto, formalizza un bivio tra $2$ strade: **o l'evento $E$ succede, o non succede**. Per comprendere meglio l'applicazione di una variabile aleatoria binaria, introduciamo il concetto di "indicatore" di un evento.

> Sia $E\in\mathcal{P}(\Omega)$ un qualsiasi evento, e sia $1_{E}$ la funzione definita nel modo seguente:
> $$1_{E}(\omega)=\begin{cases} 1&\text{per }\omega\in E\,\,\,\,\,\text{(cioè se si è verificato l'evento E)}\\0&\text{per }\omega\not\in E\,\,\,\,\,\text{(cioè se non si è verificato l'evento E)} \end{cases}$$
> Possiamo affermare che la funzione $1_{E}$, chiamata "**indicatore di $E$**", o anche "**funzione indicatrice di $E$**", costituisce un esempio di variabile aleatoria binaria.

Possiamo affermare che per qualunque variabile aleatoria binaria $X$ esiste un evento $E\subseteq \Omega=\{\omega_{1},\,\omega_{2},\,\dots,\,\omega_{N}\}$ tale per cui:
$$X(\omega_{i})=1_{E}(\omega_{i})\,\,\,\,\,\text{con }i=1,\,2,\,\dots,\,N$$
Infatti, ponendo $E=\{\omega_{i}\in \Omega:\,X(\omega_{i})=1\}$ abbiamo definito di conseguenza anche $\overline{E}=\{\omega_{i}\in \Omega:\,X(\omega_{i})=0\}$, e dunque possiamo scrivere $X(\omega_{i})$ come $1_{E}(\omega_{i})$ per ogni $i$ che va da $1$ a $N$. La **distribuzione di una variabile aleatoria binaria** $X=1_{E}$, ponendo $p=\mathbb{P}(E)$, è individuata ovviamente dal fatto che $X(\Omega)=\{0,\,1\}$, e di conseguenza da:
$$\begin{align} &p_{1}=p_{X}(1)=p\\&p_{0}=p_{X}(0)=1-p \end{align}$$
Una distribuzione del genere viene detta "**distribuzione di Bernoulli di parametro $p$**", e si scrive anche $X\sim Bern(p)$.

Le variabili aleatorie sono molto importanti anche nel **riformulare altre variabili aleatorie**. Infatti, possiamo dimostrare la seguente affermazione:

> Una qualunque variabile aleatoria $X$ può essere riscritta come una **combinazione lineare delle variabili aleatorie binarie di tipo $1_{H_{k}^{X}}$**. Infatti, posto $X(\Omega)=\{x_{1},\,x_{2},\,\dots,\,x_{n}\}$ l'insieme dei valori assumibili da $X$, e considerata la partizione $\mathcal{H}^{X}=\{H_{1}^{X},\,H_{2}^{X},\,\dots,\,H_{n}^{X}\}$ generata da $X$, tale per cui:
> $$H_{l}^{X}=\{X=x_{l}\}\,\,\,\,\,\text{con }l=1,\,2,\,\dots,\,n$$
> allora si ha che:
> $$X(\omega)=\sum_{k\,=\,1}^{n}x_{k}\,1_{H_{k}^{X}}(\omega)$$

Vediamo la **dimostrazione** di quanto appena detto. Siano $X_{1},\,X_{2},\,\dots,\,X_{n}$ le variabili aleatorie binarie definite come indicatori dei vari eventi $H_{l}^{X}$, avendo dunque che:
$$X_{l}=1_{H_{l}^{X}}$$
A questo punto, in questa dimostrazione vogliamo dimostrare che la funzione $Y(\omega)$, definita come:
$$Y(\omega):=\sum_{l\,=\,1}^{n}x_{l}\cdot X_{l}(\omega)$$
coincida con la variabile aleatoria originale $X(\omega)$ per ogni $\omega$. Per fare ciò, sarà utile ricordare che la famiglia di eventi $H_{l}^{X}$ rappresenta una [[CDP_01 - Eventi#Partizione dell'evento certo|partizione dell'evento certo]] $\Omega$: stabilito ciò, sappiamo che un qualsiasi evento elementare possibile $\omega$ deve necessariamente rientrare in uno e un solo evento $H_{l}^{X}$ della partizione. Consideriamo quindi un generico $1\le k\le n$, e consideriamo che $\omega$ rientri nell'evento $H_{k}^{X}$: per definizione degli insiemi $H_{l}^{X}$, ciò implica che $X(\omega)=x_{k}$; ora, vediamo in cosa risulta la funzione $Y(\omega)$ nello stesso contesto:
$$\begin{align} Y(\omega)&=\sum_{l\,=\,1}^{n}x_{l}\cdot X_{l}(\omega)\\&=\sum_{l\,=\,1}^{n}x_{l}\cdot 1_{H_{l}^{X}}(\omega)\\&= \overbrace{x_{1}\cdot 0+x_{2}\cdot 0 + \dots}^{\text{termini prima di }k}+\overbrace{x_{k}\cdot 1}^{\text{termine }k}+\overbrace{x_{k+1}\cdot 0+x_{k+2}\cdot 0+\,\dots\,+x_{n}\cdot 0}^{\text{termini dopo }k}\\&= x_{k}\end{align}$$
Abbiamo appena dimostrato che, per un qualsiasi evento elementare $\omega\in \Omega$, si ha che $Y(\omega)=X(\omega)=x_{k}$, e dunque abbiamo dimostrato anche che:
$$X(\omega)=\sum_{k\,=\,1}^{n}x_{k}\,1_{H_{k}^{X}}(\omega)$$
___
## Esempi di distribuzioni di probabilità su variabili aleatorie

Vediamo, di seguito, alcuni **esempi concreti di distribuzioni di probabilità** utilizzando le [[CDP_05 - Variabili aleatorie#Cos'è una variabile aleatoria?|variabili aleatorie]].

##### Lancio di due dadi

Consideriamo nuovamente l'esperimento legato al lancio di due dadi, in cui lo spazio campione $\Omega$ è definito come $\{(h,\,k)\,\,:\,\,1\le h\le 6,\,\,1\le k\le 6\}$, e in cui si ha che:
$$\mathbb{P}(\omega)=\mathbb{P}(\{(h,\,k)\})=\frac{1}{36}$$
Su questo spazio si possono definire diverse variabili aleatorie, ad esempio:
- $X_{1}:(h,\,k)\rightarrow h$, ossia il **punteggio risultante dal primo dado**;
- $X_{2}:(h,\,k)\rightarrow k$, ossia il **punteggio risultante dal secondo dado**;
- $X_{3}:(h,\,k)\rightarrow h+k$, ossia la **somma dei punteggi dei due dadi**;
- $X_{4}:(h,\,k)\rightarrow \frac{h}{k}$, ossia il **rapporto tra i punteggi dei due dadi**;

e così via. Analizziamo in particolare le prime tre delle variabili aleatorie a cui abbiamo accennato: è facile verificare, ad esempio, che **$X_{1}$ e $X_{2}$ hanno la stessa [[CDP_05 - Variabili aleatorie#Cos'è una variabile aleatoria?|distribuzione di probabilità]]**, data da:
$$\begin{align} &p_{X_{1}}(x)=\mathbf{P}_{X_{1}}(\{x\})=\mathbb{P}(\{X_{1}=x\})=\frac{1}{6}\\&p_{X_{2}}(x)=\mathbf{P}_{X_{2}}(\{x\})=\mathbb{P}(\{X_{2}=x\})=\frac{1}{6} \end{align}$$
Tale distribuzione costituisce una **distribuzione uniforme**. Invece, la distribuzione di probabilità della variabile aleatoria $X=X_{1}+X_{2}$ è definita come:
$$p_{X}(x)=\mathbf{P}_{X}(\{x\})=\mathbb{P}(\{X=x\})=\begin{cases} \frac{x-1}{36}&\text{per }x=2,\,3,\,\dots,\,7\\ \frac{13-x}{36}&\text{per }x=8,\,9,\,\dots,\,12 \end{cases}$$
___
##### Variabili aleatorie binomiali

Prima di considerare questo esempio, è opportuno soffermarsi sulla seguente osservazione:

> Siano $E_{1},\,E_{2},\,\dots,\,E_{n}$ degli eventi in uno spazio $(\Omega,\,\mathcal{P}(\Omega))$, e indicati con $X_{1},\,X_{2},\,\dots,\,X_{n}$ i loro rispettivi indicatori, si può definire sullo stesso spazio anche la variabile aleatoria $S_{n}=\sum_{h\,=\,1}^{n}X_{h}$, e si ha dunque che:
> $$S_{n}(\omega_{i})=\sum_{h\,=\,1}^{n}X_{h}(\omega_{i})=\sum_{h\,=\,1}^{n}1_{E_{h}}(\omega_{i})$$

Nel concreto, naturalmente, $S_{n}$ assume il significato di **numero di successi tra gli eventi $E_{1},\,E_{2},\,\dots,\,E_{n}$**. Si noti che la variabile aleatoria $S_{n}$ può assumere $n+1$ valori, ossia $S_{n}(\Omega)=\{0,\,1,\,\dots,\,n\}$; inoltre, la famiglia degli $n$ eventi $E_{1},\,E_{2},\,\dots,\,E_{n}$ non coincide con la partizione $\{\{S_{n}=0\},\,\{S_{n}=1\},\,\dots,\,\{S_{n}=n\}\}$, dato che la prima ha cardinalità $n$ mentre la seconda ha cardinalità $n+1$.

Passiamo ora all'esempio. Supponiamo di avere $n$ [[CDP_03 - Correlazione e indipendenza tra eventi#Prove bernoulliane|prove bernoulliane]], che si ricorda sono $n$ eventi completamente indipendenti ed equiprobabili, ciascuno di probabilità $\theta$ (con $0<\theta<1$); consideriamo, a questo punto, la variabile aleatoria $S_{n}=\{\text{numero di successi sulle }n\text{ prove}\}$. Naturalmente, i valori che può assumere tale variabile aleatoria sono $S_{n}(\Omega)=\{0,\,1,\,\dots,\,n\}$, e come abbiamo visto parlando di [[CDP_04 - Probabilità binomiali e ipergeometriche#Probabilità binomiali|probabilità binomiali]], si ha che:
$$p_{S_{n}}(k)=\mathbb{P}(\{S_{n}=k\})=\binom{n}{k}\theta^{k}(1-\theta)^{n-k}$$
In casi del genere, si dice che $S_{n}$ segue una **distribuzione binomiale di parametri $n$ e $\theta$**, proprietà che scriviamo in maniera compatta come $S_{n}\sim Bin(n,\,\theta)$. Le variabili aleatorie $S_{n}$, al variare di $n$ e $\theta$, rappresentano il prototipo delle "**variabili aleatorie binomiali**".
___
##### Variabili aleatorie ipergeometriche

Supponiamo, in questo esempio, di effettuare $n$ **estrazioni casuali senza reinserimento** da una popolazione che contiene complessivamente $M$ elementi, di cui $m_{1}$ elementi sono di tipo $A$ e $m_{2}=M-m_{1}$ elementi sono di tipo $B$. Consideriamo, ora, la variabile aleatoria $S_{n}=\{\text{numero di elementi di tipo }A\text{ estratti dopo }n\text{ estrazioni}\}$. Ricordando ciò che abbiamo detto riguardo le [[CDP_04 - Probabilità binomiali e ipergeometriche#Probabilità ipergeometriche|probabilità ipergeometriche]], si ha che:
$$p_{S_{n}}(k)=\mathbb{P}(\{S_{n}=k\})=\frac{\binom{m_{1}}{k}\binom{m_{2}}{n-k}}{\binom{M}{n}}$$
per qualsiasi $k$ tale per cui $0\le k\le m_{1}$ e $0\le n-k\le m_{2}$. In casi del genere, si dice che $S_{n}$ segue una **distribuzione ipergeometrica di parametri $M$, $m_{1}$ e $n$**, proprietà che scriviamo in maniera compatta come $S_{n}\sim Hyp(M,\,m_{1},\,n)$. Le variabili aleatorie $S_{n}$, al variare di $M$, $m_{1}$ e $n$, rappresentano il prototipo delle "**variabili aleatorie ipergeometriche**".
___
##### Variabili aleatorie a valori interi

Si noti che, finora, abbiamo sempre assunto di star lavorando con **variabili aleatorie a valori interi**, cioè tali per cui $X(\Omega)\subseteq\mathbb{Z}$, ma ciò non è sempre garantito. Banalmente, tornando all'[[CDP_05 - Variabili aleatorie#Variabili aleatorie ipergeometriche|esempio appena visto]], la variabile aleatoria $Y_{n}$ definita come la frequenza dei successi, e dunque dalla relazione:
$$Y_{n}=\frac{S_{n}}{n}$$
è una variabile aleatoria non a valori interi. Per adesso, però, continuiamo a concentrarci sulla categoria di variabili aleatorie viste finora, e portiamo ulteriori esempi di situazioni in cui possono comparire.

Prima di procedere, facciamo un'osservazione.

> Per una variabile aleatoria $X$ a valori interi, cioè tale per cui $X(\Omega)\subseteq\mathbb{Z}$, può essere spesso conveniente calcolare la distribuzione di probabilità tenendo conto della relazione:
> $$\mathbb{P}(X=k)=\mathbb{P}(X\le k)-\mathbb{P}(X\le k-1)$$
> Al tempo stesso, può tornare utile anche la seguente equivalenza:
> $$\begin{align} \mathbb{P}(X=k)&=\mathbb{P}(X\ge k)-\mathbb{P}(X\ge k+1) \\&= \mathbb{P}(X>k-1)-\mathbb{P}(X>k) \end{align}$$


Vediamo come poter applicare queste formule in situazioni concrete. Consideriamo i lancio di due dadi, indichiamo con $X_{1}$ e $X_{2}$ i punteggi ottenuti rispettivamente dal primo e dal secondo dado, e concentriamoci sulla variabile aleatoria $Z$ definita come il **massimo dei due punteggi**: vogliamo individuare i valori che può assumere $Z$ (dunque, formalmente, $Z(\Omega)$) e con quali probabilità essa assume tali valori. Rispondere alla prima domanda è banale: trattandosi del lancio di due dadi, è ovvio che il punteggio massimo sarà necessariamente compreso tra $1$ e $6$, e dunque $Z(\Omega)=\{1,\,2,\,\dots,\,6\}$. Ora, tenendo conto che le due famiglie di eventi $\mathcal{A}=\{\{X_{1}=1\},\,\{X_{1}=2\},\,\dots,\,\{X_{1}=6\}\}$ e $\mathcal{B}=\{\{X_{2}=1\},\,\{X_{2}=2\},\,\dots,\,\{X_{2}=6\}\}$ sono [[CDP_03 - Correlazione e indipendenza tra eventi#Indipendenza completa di partizioni|indipendenti]], e di conseguenza lo sono anche gli eventi che li compongono, risulta che:
$$\begin{align} \mathbb{P}(Z=k)&=\,\mathbb{P}(Z\le k)-\mathbb{P}(Z\le k-1)\\&=\,\mathbb{P}(\{X_{1}\le k\}\cap\{X_{2}\le k\})-\mathbb{P}(\{X_{1}\le k-1\}\cap\{X_{2}\le k-1\})\\&=\,\mathbb{P}(X_{1}\le k)\cdot\mathbb{P}(X_{2}\le k)\,-\,\mathbb{P}(X_{1}\le k-1)\cdot\mathbb{P}(X_{2}\le k -1)\\&=\,\left( \frac{k}{6} \right)^{2}-\left( \frac{k-1}{6} \right)^{2}=\frac{2k-1}{36} \end{align}$$

Vediamo un altro esempio, molto simile: consideriamo di nuovo il lancio di due dadi, indicando sempre con $X_{1}$ e $X_{2}$ i punteggi ottenuti, ma stavolta concentriamoci sulla variabile aleatoria $W$ definita come il **minimo dei due punteggi**. Anche in questo caso, è banale che $W(\Omega)=\{1,\,2,\,\dots,\,6\}$, e tenendo conto che le medesime famiglie $\mathcal{A}=\{\{X_{1}=1\},\,\{X_{1}=2\},\,\dots,\,\{X_{1}=6\}\}$ e $\mathcal{B}=\{\{X_{2}=1\},\,\{X_{2}=2\},\,\dots,\,\{X_{2}=6\}\}$ sono indipendenti, si arriva a:
$$\begin{align} \mathbb{P}(W=k)&=\,\mathbb{P}(W\ge k)-\mathbb{P}(W\ge k+1)\\&=\,\mathbb{P}(\{X_{1}\ge k\}\cap\{X_{2}\ge k\})-\mathbb{P}(\{X_{1}\ge k+1\}\cap\{X_{2}\ge k+1\})\\&=\,\mathbb{P}(X_{1}\ge k)\cdot\mathbb{P}(X_{2}\ge k)\,-\,\mathbb{P}(X_{1}\ge k+1)\cdot\mathbb{P}(X_{2}\ge k+1)\\&=\mathbb{P}(X_{1}>k-1)\cdot\mathbb{P}(X_{2}>k-1)\,-\,\mathbb{P}(X_{1}>k)\cdot\mathbb{P}(X_{2}>k)\\&= (1-\mathbb{P}(X_{1}\le k-1))\cdot(1-\mathbb{P}(X_{2}\le k-1))\,-\,(1-\mathbb{P}(X_{1}\le k))\cdot(1-\mathbb{P}(X_{2}\le k)) \\&=\,\left(1- \frac{k-1}{6} \right)^{2}-\left(1- \frac{k}{6} \right)^{2}\\&=\frac{49-14k+k^{2}-(36-12k+k^{2})}{36}=\frac{13-2k}{36} \end{align}$$


[pag. 91]
___