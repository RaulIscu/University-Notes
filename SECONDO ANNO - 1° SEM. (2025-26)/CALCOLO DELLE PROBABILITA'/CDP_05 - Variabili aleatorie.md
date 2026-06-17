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

Le variabili aleatorie binarie sono molto importanti anche nel **riformulare altre variabili aleatorie**. Infatti, possiamo dimostrare la seguente affermazione:

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

Nel concreto, naturalmente, $S_{n}$ assume il significato di **numero di successi tra gli eventi $E_{1},\,E_{2},\,\dots,\,E_{n}$**. Si noti che la variabile aleatoria $S_{n}$ può assumere $n+1$ valori, ossia $S_{n}(\Omega)=\{0,\,1,\,\dots,\,n\}$; perciò, la famiglia degli $n$ eventi $E_{1},\,E_{2},\,\dots,\,E_{n}$ non coincide con la partizione $\{\{S_{n}=0\},\,\{S_{n}=1\},\,\dots,\,\{S_{n}=n\}\}$, dato che la prima ha cardinalità $n$ mentre la seconda ha cardinalità $n+1$.

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
___
## Trasformazioni di una variabile aleatoria in spazi finiti

Data una variabile aleatoria $X$ e una funzione $h$, si può definire una seconda variabile aleatoria come la "**trasformata di $X$ tramite la funzione $h$**", ossia:
$$Z:\Omega\rightarrow\mathbb{R},\,\,\,\omega\mapsto Z(\omega):=h(X(\omega))$$
Supponendo nota la distribuzione di $X$, ovvero l'insieme $X(\Omega)=\{x_{1},\,x_{2},\,\dots,\,x_{n}\}$ dei valori che può assumere $X$ e la sua densità discreta $p_{X}(x_{k})=\mathbb{P}(X=x_{k})$ con $k=1,\,2,\,\dots,\,n$, ci chiediamo come **ottenere la distribuzione di $Z$**, ovvero l'insieme $Z(\Omega)=\{z_{1},\,z_{2},\,\dots,\,z_{m}\}$ dei valori che può assumere $Z$ e la sua densità discreta $p_{Z}(z_{h})=\mathbb{P}(Z=z_{h})$ con $h=1,\,2,\,\dots,\,m$.

Per capire come procedere, vediamo un esempio: supponiamo di avere una variabile $X$ che può assumere i valori $\pm\, 2$, $\pm\, 1$ e $0$ (quindi $X(\Omega)=\{-2,\,-1,\,0,\,1,\,2\}$), con $p_{X}(x)=\frac{1}{5}$ per ogni $x\in X(\Omega)$; a questo punto, definiamo la funzione $h(x)=x^2$, e otteniamo di conseguenza che l'ipotetica variabile $Z=X^{2}$ determinata da $h(X)$ potrà assumere i valori $0$, $1$ e $4$. Inoltre, valendo le seguenti relazioni:
$$\begin{align} &\{Z=0\}=\{X=0\}\\&\{Z=1\}=\{X=-1\}\cup\{X=1\}\\&\{Z=4\}=\{X=-2\}\cup\{X=2\} \end{align}$$
si ottiene che:
$$\begin{align} &\mathbb{P}(Z=0)\,=\,\mathbb{P}(X=0)=\frac{1}{5}\\&\mathbb{P}(Z=1)\,=\,\mathbb{P}(X=1)+\mathbb{P}(X=-1)=\frac{2}{5} \\&\mathbb{P}(Z=4)\,=\,\mathbb{P}(X=2)+\mathbb{P}(X=-2)=\frac{2}{5}\end{align}$$
Generalizzando, abbiamo ovviamente che $Z(\Omega)=h(X(\Omega))$, e possiamo affermare che $\{Z=z_{j}\}=\bigcup_{l\,:\,h(x_{l})\,=\,z_{l}}\{X=x_{l}\}$, da cui deriva che:
$$p_{Z}(z_{j})=\mathbb{P}(Z=z_{j})=\sum_{l\,:\,h(x_{l})\,=\,z_{j}}\mathbb{P}(X=x_{l})$$
per ogni $z_{j}\in h(X(\Omega))$.
___
## Distribuzioni congiunte di più variabili aleatorie

In questo paragrafo, andremo ad esaminare alcune definizioni e proprietà relative ai casi in cui **si considerano**, contemporaneamente e su uno stesso spazio di probabilità, **due variabili aleatorie**; in seguito, i concetti esposti potranno facilmente essere estesi anche a casi in cui sono coinvolte più di due variabili.

Consideriamo uno spazio di probabilità $(\Omega,\,\mathcal{P}(\Omega),\,\mathbb{P})$, e una coppia di variabili aleatorie $X$ e $Y$ definite su tale spazio, con:
$$\begin{align} &X:\Omega\rightarrow X(\Omega):=\{x_{1},\,x_{2},\,\dots,\,x_{n}\}\\&Y:\Omega\rightarrow Y(\Omega):=\{y_{1},\,y_{2},\,\dots,\,y_{m}\} \end{align}$$
A questo punto, possiamo considerare su $\Omega$ la partizione costituita dagli eventi del tipo:
$$\{X=x_{i}\}\cap\{Y=y_{j}\}\,:=\,\{\omega\in \Omega\,:\,X(\omega)=x_{i},\,Y(\omega)=y_{j}\}$$
D'ora in poi, per comodità la notazione $\{X=x_{i}\}\cap\{Y=y_{j}\}$ potrebbe essere sostituita con $\{X=X_{i},\,Y=y_{j}\}$. Ora, in analogia con il caso di una sola variabile aleatoria, per riferirci alla probabilità che le variabili $X$ e $Y$ assumano una certa coppia di valori scriviamo che:
$$p_{X,\,Y}(x_{i},\,y_{j})=\mathbb{P}(\{X=x_{i},\,Y=y_{j}\})$$
per mettere in evidenza le variabili coinvolte e i valori che possono assumere.

> La funzione:
> $$X(\Omega)\times Y(\Omega)\rightarrow[0,\,1];\,\,\,\,\,(x_{i},\,y_{j})\mapsto p_{X,\,Y}(x_{i},\,y_{j})$$
> prende il nome di "**densità discreta congiunta di $X$ e $Y$**".

Ovviamente, avendo stabilito che i vari eventi $\{X=x_{1},\,Y=y_{j}\}$ formano una partizione, possiamo anche affermare che:
$$p_{X,\,Y}(x_{i},\,y_{j})\ge 0,\,\,\,\,\,\,\,\,\,\,\sum_{i\,=\,1}^{n}\sum_{j\,=\,1}^{m}p_{X,\,Y}(x_{i},\,y_{j})=1$$
A questo punto, possiamo considerare il nuovo spazio di probabilità definito tramite $X$ e $Y$, ossia:
$$(X(\Omega)\times Y(\Omega),\,\mathcal{P}(X(\Omega)\times Y(\Omega)),\,\mathbf{P}_{X,\,Y})$$
dove, per un qualsiasi $E\subseteq X(\Omega)\times Y(\Omega)$, si pone:
$$\mathbf{P}_{X,\,Y}(E)=\sum_{(i,\,j)\,:\,(x_{i},\,y_{j})\,\in\,E}p_{X,\,Y}(x_{i},\,y_{j})=\mathbb{P}(\{(X,\,Y)\in E\})$$
> La misura di probabilità:
> $$\mathbf{P}_{X,\,Y}:(X(\Omega)\times Y(\Omega),\,\mathcal{P}(X(\Omega)\times Y(\Omega)));\,\,\,\,\,E\mapsto \mathbf{P}_{X,\,Y}(E)=\mathbb{P}(\{(X,\,Y)\in E\})=\sum_{(i,\,j)\,:\,(x_{i},\,y_{j})\,\in\,E}p_{X,\,Y}(x_{i},\,y_{j})$$
> prende il nome di "**distribuzione di probabilità congiunta di $X$ e $Y$**".

Considerate due variabili aleatorie $X$ e $Y$, i cui insiemi di valori possibili siano rispettivamente $\{x_{1},\,x_{2},\,\dots,\,x_{n}\}$ e $\{y_{1},\,y_{2},\,\dots,\,y_{m}\}$, e sia la loro distribuzione di probabilità congiunta individuata dalla densità discreta congiunta, ossia dalle probabilità:
$$p_{X,\,Y}(x_{i},\,y_{j})=\mathbb{P}(\{X=x_{i},\,Y=y_{j}\})$$
nel momento in cui tale distribuzione di probabilità congiunta è nota, è possibile ottenere la distribuzione relativa a una sola delle due variabili considerate: tali distribuzioni vengono dette "**distribuzioni marginali**", e attribuiscono ai valori possibili di ciascuna delle due variabili aleatorie le seguenti probabilità:
$$\begin{align} &p_{X}(x_{i})=\mathbb{P}(X=x_{i})=\sum_{j\,=\,1}^{m}\mathbb{P}(\{X=x_{i},\,Y=y_{j}\})=\sum_{j\,=\,1}^{m}p_{X,\,Y}(x_{i},\,y_{j}) \\& p_{Y}(y_{j})=\mathbb{P}(Y=y_{j})=\sum_{i\,=\,1}^{n}\mathbb{P}(\{X=x_{i},\,Y=y_{j}\})=\sum_{i\,=\,1}^{n}p_{X,\,Y}(x_{i},\,y_{j})\end{align}$$
In questo contesto, la funzione $x_{i}\mapsto p_{X}(x_{i})$ viene detta "**densità discreta marginale di $X$**", mentre $y_{j}\mapsto p_{Y}(y_{j})$ viene detta "**densità discreta marginale di $Y$**".

Vediamo un esempio. Siano $X$ e $Y$ due variabili aleatorie che possono rispettivamente assumere i valori $\{-1,\,0,\,1\}$ e $\left\{ \frac{1}{4},\, \frac{1}{2},\, \frac{3}{4},\, 1 \right\}$, con le seguenti probabilità congiunte:

![[prob_congiunte_esempio.png]]

che possiamo indicare sinteticamente nella seguente tabella:

![[prob_congiunte_esempio1.png]]

A questo punto, potremmo applicare le formule appena viste per ottenere, ad esempio, la distribuzione di probabilità marginale della variabile $X$. La probabilità che, ad esempio, si ottenga $X=0$ è la seguente:
$$\begin{align} \mathbb{P}(X=0)&=\mathbb{P}\left( X=0,\,Y= \frac{1}{4} \right)+\mathbb{P}\left( X=0,\,Y= \frac{1}{2} \right)+\mathbb{P}\left( X=0,\,Y= \frac{3}{4} \right)+\mathbb{P}( X=0,\,Y=1)\\&=0.2+0.12+0.1+0.04\\&=0.46 \end{align}$$
In modo analogo, possiamo ottenere la totalità della distribuzione di probabilità marginale della variabile $X$, e lo stesso vale per quella della variabile $Y$; volendo aggiungere tali distribuzioni alla tabella vista poco fa, si otterrebbe:

![[prob_congiunte_esempio2.png]]

Ora, questo tipo di tabella può essere generalizzato considerando una coppia generica di variabili aleatorie, che per comodità chiameremo sempre $X$ e $Y$, in quella che viene detta "**tabella a doppia entrata**", che assume la forma seguente:

![[prob_congiunte_esempio3.png]]

È interessante osservare che, in generale, dati due insiemi $\{x_{1},\,x_{2},\,\dots,\,x_{n}\}$ e $\{y_{1},\,y_{2},\,\dots,\,y_{m}\}$ e considerata una tabella a doppia entrata riempita dei valori $p_{i,\,j}$ per $i=1,\,2,\,\dots,\,n$ e $j=1,\,2,\,\dots,\,m$, se i valori $p_{i,\,j}$ soddisfano le seguenti condizioni:
$$p_{i,\,j}\ge 0;\,\,\,\,\,\,\,\,\,\,\sum_{i\,=\,1}^{n}\sum_{j\,=\,1}^{m}p_{i,\,j}=1$$
allora è possibile costruire uno spazio di probabilità a partire dall'insieme $\{x_{1},\,x_{2},\,\dots,\,x_{n}\}\times\{y_{1},\,y_{2},\,\dots,\,y_{m}\}$, dove la probabilità è definita a partire dalla seguente densità:
$$p:\{x_{1},\,x_{2},\,\dots,\,x_{n}\}\times\{y_{1},\,y_{2},\,\dots,\,y_{m}\}\rightarrow[0,\,1];\,\,\,\,\,(x_{i},\,y_{j})\mapsto p(x_{i},\,y_{j}):=p_{i,\,j}$$
Inoltre, definendo $p'_{i}$ come:
$$p'_{i}=\sum_{j\,=\,1}^{m}p_{i,\,j}$$
allora naturalmente $p'_{i}$ è una densità su $\{x_{1},\,x_{2},\,\dots,\,x_{n}\}$, in quanto risulta che:
$$p'_{i}\ge 0;\,\,\,\,\,\,\,\,\,\,\sum_{i\,=\,1}^{n}p_{i}'=\sum_{i\,=\,1}^{n}\left( \sum_{j\,=\,1}^{m}p_{i,\,j} \right)=1$$
Ovviamente, una considerazione analoga vale per $p''_{j}=\sum_{i\,=\,1}^{n}p_{i,\,j}$.

##### Distribuzioni condizionate

In una situazione come quella descritta finora in questo paragrafo, ossia due variabili aleatorie $X$ e $Y$ definite su uno stesso spazio $\Omega$, consideriamo che venga osservato l'evento $\{Y=y_{j}\}$ per un $j=1,\,2,\,\dots,\,m$, e ci si domanda quale sia la **distribuzione di probabilità che esprime lo stato di informazione parziale circa $X$ sapendo l'esito di $Y$**. Leggendo questa richiesta, dovrebbe venire alla mente un argomento affrontato in precedenza, che possiamo riapplicare nel nuovo contesto in cui ci troviamo in questo capitolo: le **[[CDP_02 - Probabilità#Probabilità condizionate|probabilità condizionate]]**. Infatti, possiamo fornire la seguente definizione:

> Fissato $y_{j}\in Y(\Omega)$, con $\mathbb{P}(Y=y_{j})>0$, definiamo come "**distribuzione di probabilità condizionata della variabile $X$ dato l'evento $\{Y=y_{j}\}$**" la distribuzione che concentra, sui vari valori $x_{i}$, le probabilità condizionate di tipo:
> $$\mathbb{P}(X=x_{i}\,|\,Y=y_{j})=\frac{\mathbb{P}(X=x_{i},\,Y=y_{j})}{\mathbb{P}(Y=y_{j})}$$

Useremo, contestualmente a questo tipo di probabilità, anche la notazione:
$$p_{X\,|\,Y}(x_{i}\,|\,y_{j}):=\mathbb{P}(X=x_{i}\,|\,Y=y_{j})$$
e il termine "**densità discreta di $X$ condizionata a $Y=y_{j}$**" per denotare la seguente funzione:
$$p_{X\,|\,Y}(\cdot\,|\,y_{j}):\,X(\Omega)\rightarrow[0,\,1];\,\,\,\,\,\,\,\,\,\,x_{i}\mapsto p_{X\,|\,Y}(x_{i}\,|\,y_{j})$$
Possiamo facilmente ricavare i valori di $p_{X\,|\,Y}(x_{i}\,|\,y_{j})$ sfruttando le probabilità congiunte, infatti:
$$p_{X\,|\,Y}(x_{i}\,|\,y_{j})=\frac{\mathbb{P}(X=x_{i},\,Y=y_{j})}{\mathbb{P}(Y=y_{j})}=\frac{p_{X,\,Y}(x_{i},\,y_{j})}{p_{Y}(y_{j})}=\frac{p_{X,\,Y}(x_{i},\,y_{j})}{\sum_{i\,=\,1}^{n}p_{X,\,Y}(x_{i},\,y_{j})}$$
Va da sé che tutto ciò che abbiamo detto finora sulle distribuzioni condizionate vale anche invertendo il ruolo delle variabili aleatorie. Dunque, ricapitolando, considerando una coppia di variabili aleatorie $X$ e $Y$, per le quali gli insiemi di valori possibili sono $X(\Omega)=\{x_{1},\,x_{2},\,\dots,\,x_{n}\}$ e $Y(\Omega)=\{y_{1},\,y_{2},\,\dots,\,y_{m}\}$, la distribuzione di probabilità congiunta è individuata dall'insieme delle probabilità congiunte identificato come:
$$\{p_{i,\,j}=p_{X,\,Y}(x_{i},\,y_{j})\},\,\,\,\,\,\text{con }i=1,\,2,\,\dots,\,n\text{ e }y=1,\,2,\,\dots,\,m$$
In base a tali probabilità congiunte, possiamo determinare univocamente le probabilità marginali $p_{i}'$ e $p''_{j}$, così come le probabilità condizionate $p_{i\,|\,j}'=p_{X\,|\,Y}(x_{i}\,|\,y_{j})$ e $p_{j\,|\,i}''=p_{Y\,|\,X}(y_{j}\,|\,x_{i})$. Ora, supponiamo di assegnare la coppia delle densità discrete marginali $p_{i}'$ e $p''_{j}$; si ricorda che vanno rispettati i seguenti vincoli, dati dalla [[CDP_02 - Probabilità#Misure di probabilità|condizione di normalizzazione]]:
$$\sum_{i\,=\,1}^{n}p_{i}'=1\,\,\,\,\,\,\,\,\,\,\sum_{j\,=\,1}^{m}p_{j}''=1$$
Considerando una generica tabella a doppia entrata riempita dai valori $p_{i,\,j}$, che ammette come probabilità marginali $p_{i}'$ e $p_{j}''$, deve allora necessariamente valere che:
$$\begin{cases} \sum_{j\,=\,1}^{m}p_{i,\,j}=p_{i}'&\text{con }i=1,\,2,\,\dots,\,n \\\sum_{i\,=\,1}^{n}p_{i,\,j}=p_{j}''&\text{con }j=1,\,2,\,\dots,\,m\\\sum_{i\,=\,1}^{n}\sum_{j\,=\,1}^{m}p_{i,\,j}=1\end{cases}$$

Siano date due variabili aleatorie $X$ e $Y$. La loro densità discreta congiunta, e dunque la loro distribuzione di probabilità congiunta, è determinata dagli insiemi $X(\Omega)$ e $Y(\Omega)$, così come dalla tabella a doppia entrata contenente i valori $p_{i,\,j}=p_{X,\,Y}(x_{i},\,y_{j})$ per $i=1,\,2,\,\dots,\,n$ e $j=1,\,2,\,\dots,\,m$. Tale tabella risulta univocamente determinata quando si impongono, ad esempio, sia le probabilità marginali di tipo $\{p_{i}'=p_{X}(x_{i})\}$ che le probabilità condizionate di tipo $\{p_{j\,|\,i}''=p_{Y\,|\,X}(y_{j}\,|\,x_{i})\}$, infatti si ha che:
$$\mathbb{P}(X=x_{i},\,Y=y_{j})=\mathbb{P}(X=x_{i})\cdot\mathbb{P}(Y=y_{j}\,|\,X=x_{i})\,\,\,\iff\,\,\,p_{i,\,j}=p_{i}'\cdot p_{j\,|\,i}''$$
Naturalmente, scambiare il ruolo di $X$ e $Y$ nelle considerazioni appena fatte non intacca la loro validità. Notiamo anche che la relazione che lega le probabilità appena viste coincide, sostanzialmente, con la [[CDP_02 - Probabilità#Formula di Bayes|formula di Bayes]]; infatti:
$$\mathbb{P}(X=x_{i}\,|\,Y=y_{j})=\frac{\mathbb{P}(X=x_{i})\cdot\mathbb{P}(Y=y_{j}\,|\,X=x_{i})}{\mathbb{P}(Y=y_{j})}=\frac{\mathbb{P}(X=x_{i})\cdot\mathbb{P}(Y=y_{j}\,|\,X=x_{i})}{\sum_{l}\mathbb{P}(X=x_{l})\mathbb{P}(Y=y_{j}\,|\,X=x_{l})}$$
oppure, riadattando la formula al simbolismo breve introdotto:
$$p'_{i\,|\,j}=\frac{p_{i}'\cdot p''_{j\,|\,i}}{p_{j}''}=\frac{p_{i}'\cdot p_{j\,|\,i}''}{\sum_{l}p_{l}'\cdot p_{j\,|\,l}''}$$

Per comprendere meglio come possiamo applicare quanto detto finora, vediamo un esempio. Sia $X$ una variabile aleatoria che segue una [[CDP_05 - Variabili aleatorie#Variabili aleatorie binomiali|distribuzione binomiale]] di parametri $n=3$ e $\theta=\frac{1}{4}$, dunque tale per cui:
$$\begin{align} &p_{X}(0)\,=\,\mathbb{P}(X=0)\,=\,\binom{3}{0}\left( \frac{1}{4} \right)^0\left( \frac{3}{4} \right)^3\,=\,\frac{27}{64} \\&p_{X}(1)\,=\,\mathbb{P}(X=1)\,=\,\binom{3}{1}\left( \frac{1}{4} \right)^1\left( \frac{3}{4} \right)^2\,=\,\frac{27}{64} \\&p_{X}(2)\,=\,\mathbb{P}(X=2)\,=\,\binom{3}{2}\left( \frac{1}{4} \right)^2\left( \frac{3}{4} \right)^1\,=\,\frac{9}{64} \\&p_{X}(3)\,=\,\mathbb{P}(X=3)\,=\,\binom{3}{3}\left( \frac{1}{4} \right)^3\left( \frac{3}{4} \right)^0\,=\,\frac{1}{64} \end{align}$$
Supponiamo, inoltre, che per ogni $h\in X(\Omega)$, la distribuzione condizionata di $Y$ dato $\{X=h\}$ sia uniforme in valori interi $k$ tali per cui $0\le k\le h$, o in altre parole che tale distribuzione contempli esclusivamente valori $k$ inclusi tra $0$ e $h$ (compresi), e che tutti questi valori $k$ sono equiprobabili. Ciò implica, ad esempio, che:
$$p_{Y\,|\,X}(0\,|\,0)=\mathbb{P}(Y=0\,|\,\{X=0\})=1\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,p_{Y\,|\,X}(k\,|\,0)=\mathbb{P}(Y=k\,|\,\{X=0\})=0\,\,\,\,\,\text{per }k=1,\,2,\,3$$
se $X=0$, dunque che nell'eventualità in cui la variabile aleatoria $X$ valga $0$ la variabile $Y$ assume una distribuzione uniforme sui valori $\{0\}$, ed essendoci un solo valore in tale insieme esso avrà necessariamente probabilità $1$ (sarà, sostanzialmente, certo), mentre tutti gli altri valori possibili avranno probabilità $0$. Invece, nel caso in cui $X=1$, si ha la seguente situazione:
$$p_{Y\,|\,X}(k\,|\,1)=\mathbb{P}(Y=k\,|\,\{X=1\})=\frac{1}{2}\,\,\,\,\,\text{per }k=0,\,1\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,p_{Y\,|\,X}(k\,|\,1)=\mathbb{P}(Y=k\,|\,\{X=1\})=0\,\,\,\,\,\text{per }k=2,\,3$$
e così via. Possiamo, a questo punto, dedurre la densità concreta congiunta di $X$ e $Y$, ossia $p_{X,\,Y}(h,\,k)$, dato che disponiamo sia delle densità marginali $p_{X}$ sia delle densità condizionate $p_{Y\,|\,X}$:
$$p_{X,\,Y}(h,\,k)=\begin{cases} \frac{1}{h+1}\,\binom{3}{h}\left( \frac{1}{4} \right)^h\left( \frac{3}{4} \right)^{3-h}&\text{per }0\le k\le h\\\\ 0&\text{altrimenti} \end{cases}$$
Inoltre, a questo punto, sarà possibile anche calcolare la densità marginale di $Y$, e conseguentemente stilare una tabella a doppia entrata che riassuma la situazione:

![[dist_condizionate_esempio.png]]

Infine, potremo calcolare anche la densità discreta condizionata di $X$ dato $\{Y=k\}$.
___
##### Trasformazioni di coppie di variabili aleatorie in spazi finiti

Supponiamo di avere due variabili aleatorie $X$ e $Y$, e di fissare una funzione $g(x,\,y)$ di due variabili a valori reali. Possiamo considerare una terza variabile aleatoria $U$, definita come:
$$U=g(X,\,Y)$$
il cui funzionamento è sostanzialmente analogo alla [[CDP_05 - Variabili aleatorie#Trasformazioni di una variabile aleatoria in spazi finiti|trasformata di una singola variabile aleatoria]]. Di conseguenza, allo stesso modo, possiamo ottenere la distribuzione della variabile $U$ ottenendo i vari valori:
$$p_{U}(u)=\mathbb{P}(U=u)=\sum_{(x_{i},\,y_{j})\,\in\,X(\Omega)\,\times\,Y(\Omega)\,:\,g(x_{i},\,y_{j})\,=\,u}p_{X,\,Y}(x_{i},\,y_{j})$$
In casi specifici, il calcolo della densità discreta di $U$ può essere effettuato utilizzando la tabella della densità discreta congiunta di $X$ e $Y$. Consideriamo nuovamente l'[[CDP_05 - Variabili aleatorie#Distribuzioni congiunte di più variabili aleatorie|esempio]] visto un paio di paragrafi fa, dove siamo arrivati a definire la seguente tabella a doppia entrata:

![[prob_congiunte_esempio1.png]]

A questo punto, consideriamo la funzione $g(x,\,y)=|xy|$, e la variabile aleatoria $U=g(X,\,Y)$. Alla tabella appena ripresa, possiamo dunque accostare una tabella in cui, relativamente a ogni coppia $(x_{i},\,y_{j})$, inseriamo il valore assunto dalla funzione $g(x_{i},\,y_{j})$:

![[prob_congiunte_esempio4.png]]

Analizzando la seconda tabella, notiamo immediatamente che $U(\Omega)=\left\{ 0,\, \frac{1}{4},\, \frac{1}{2},\, \frac{3}{4},\, 1 \right\}$. Ora, per calcolare la distribuzione della variabile $U$, basterà sommare le probabilità $p_{X,\,Y}$ corrispondenti; ad esempio, la probabilità che $U=0$ è la seguente:
$$\begin{align} \mathbb{P}(U=0)\,&=\,\mathbb{P}\left( X=0,\,Y=\frac{1}{4} \right)+\mathbb{P}\left( X=0,\,Y= \frac{1}{2} \right)+\mathbb{P}\left( X=0,\,Y= \frac{3}{4} \right)+\mathbb{P}(X=0,\,Y=1)\\&=\,0.2+0.12+0.1+0.04\\&=\,0.46 \end{align}$$
In modo del tutto analogo si potranno calcolare anche le altre probabilità. Possiamo procedere, alternativamente, anche senza l'aiuto della tabella: ad esempio, sfruttando il fatto che la famiglia $H_{i}^{X}=\{X=x_{i}\}$ è una partizione, scrivendo dunque:
$$\{U=u\}\,=\,\{U=u\}\cap \,\Omega\,=\,\{U=u\}\cap\bigcup_{i\,=\,1}^{n}H_{i}^{X}\,=\,\bigcup_{i\,=\,1}^{n}(\{U=u\}\cap H_{i}^{X})$$
e osservando che, per ogni $i=1,\,2,\,\dots,\,n$:
$$\{U=u\}\cap H_{i}^{X}\,=\,\{g(X,\,Y)=u\}\cap\{X=x_{i}\}\,=\,\{g(x_{i},\,Y)=u\}\cap\{X=x_{i}\}$$
otteniamo che:
$$\begin{align} p_{U}(u)=\mathbb{P}(U=u)&=\sum_{x_{i}\,\in\,X(\Omega)}\mathbb{P}(H_{i}^{X}\cap\{g(X,\,Y)=u\})\\&=\sum_{x_{i}\,\in\,X(\Omega)}\mathbb{P}(X=x_{i},\,g(X,\,Y)=u)\\&=\sum_{x_{i}\,\in\,X(\Omega)}\mathbb{P}(X=x_{i},\,g(x_{i},\,Y)=u) \end{align}$$
con la quale riusciamo a ricondurci alla formula generale esplicitata in precedenza.

Si procede in modo analogo anche se si ha una **coppia di funzioni del tipo $(x,\,y)\mapsto g_{1}(x,\,y)$ e $(x,\,y)\mapsto g_{2}(x,\,y)$**, che definiscano rispettivamente le variabili aleatorie:
$$U=g_{1}(X,\,Y)\,\,\,\,\,\,\,\,\,\,V=g_{2}(X,\,Y)$$
In questo caso, possiamo scrivere:
$$p_{U,\,V}(u,\,v)=\mathbb{P}(U=u,\,V=v)=\sum_{(x_{i},\,y_{j})\,:\,g_{1}(x_{i},\,y_{j})\,=\,u,\,g_{2}(x_{i},\,y_{j})\,=\,v}p_{X,\,Y}(x_{i},\,y_{j})$$
___
##### Indipendenza stocastica tra variabili aleatorie

Ricordando quanto detto nel caso dell'[[CDP_03 - Correlazione e indipendenza tra eventi#Correlazione e indipendenza tra 2 eventi|indipendenza tra 2 eventi]], possiamo definire l'**indipendenza stocastica tra $2$ variabili aleatorie** nel modo seguente: due variabili $X$ e $Y$ sono indipendenti se qualunque informazione raccolta su una delle due variabili non porta a modificare lo stato di informazione sull'altra. A partire da tale considerazione, arriveremo a fornire una definizione più formale di tale concetto.

Per arrivare a quest'ultima, partiamo analizzando un esercizio semplice ma fondamentale. Siano $X$ e $Y$ due variabili aleatorie, vogliamo verificare che le seguenti condizioni siano tra di loro equivalenti:
- le [[CDP_05 - Variabili aleatorie#Distribuzioni condizionate|probabilità condizionate]] $y_{j}\mapsto p_{j\,|\,i}''=p_{Y\,|\,X}(y_{j}\,|\,x_{i})=\mathbb{P}(Y=y_{j}\,|\,X=x_{i})$ non dipendono dall'indice $i$, bensì dal valore $x_{i}$;
- per ogni $1\le i\le n$ e $1\le j\le m$, risulta:
$$p_{j\,|\,i}''=p_{j}''\,\,\iff\,\,p_{Y\,|\,X}(y_{j}\,|\,x_{i})=p_{Y(y_{j})}\,\,\iff\,\,\mathbb{P}(Y=y_{j}\,|\,X=x_{i})=\mathbb{P}(Y=y_{j})$$
- per ogni $1\le i\le n$ e $1\le j\le m$, risulta:
$$p_{i,\,j}=p_{i}'\cdot p_{j}''\,\,\iff\,\,p_{X,\,Y}(x_{i},\,y_{j})=p_{X}(x_{i})\,p_{Y}(y_{j})\,\,\iff\,\,\mathbb{P}(X=x_{i},\,Y=y_{j})=\mathbb{P}(X=x_{i})\,\mathbb{P}(Y=y_{j})$$

[dimostrazione: pag. 106]

Avendo dimostrato l'equivalenza delle tre condizioni precedenti, possiamo affermare che $X$ e $Y$ sono due variabili stocasticamente indipendenti qualora si verifichi una (e quindi tutte) di esse. A partire, in particolare, dalla terza e ricordando la definizione di [[CDP_03 - Correlazione e indipendenza tra eventi#Indipendenza completa di partizioni|indipendenza tra partizioni]], arriviamo a formulare una definizione formale.

> Le variabili $X$ e $Y$ si dicono **stocasticamente indipendenti** se
> $$\mathbb{P}(X\in I,\,Y\in J)\,=\,\mathbb{P}(X\in I)\cdot\mathbb{P}(Y\in J)$$
> per un qualsiasi $I\subseteq X(\Omega)$ e $J\subseteq Y(\Omega)$ o, equivalentemente, se le due partizioni:
> $$\mathcal{A}=\{\{X=x_{1}\},\,\{X=x_{2}\},\,\dots,\,\{X=x_{n}\}\}\,\,\,\,\,\,\,\,\,\,\mathcal{B}=\{\{Y=y_{1}\},\,\{Y=y_{2}\},\,\dots,\,\{Y=y_{m}\}\}$$
> sono indipendenti tra loro.

In altre parole, le variabili aleatorie $X$ e $Y$ sono stocasticamente indipendenti se e solo se la densità discreta congiunta è il prodotto delle densità discrete marginali.

Vediamo di applicare i concetti appena esplicitati nel seguente esercizio. Siano $X$ e $Y$ due variabili aleatorie stocasticamente indipendenti, con $X(\Omega)=\{x_{1},\,x_{2},\,\dots,\,x_{n}\}$ e $Y(\Omega)=\{y_{1},\,y_{2},\,\dots,\,y_{m}\}$, e siano note le relative densità discrete marginali; vogliamo trovare l'espressione della distribuzione di probabilità della variabile $Z=X+Y$, e in seguito l'espressione della [[CDP_05 - Variabili aleatorie#Distribuzioni condizionate|distribuzione condizionata]] di probabilità di $X$ dato $\{Z=z\}$. Pensiamo al primo punto: possiamo affermare subito che:
$$Z(\Omega)=\{z\in\mathbb{R}: \exists x_{k}\in X(\Omega),\,y_{h}\in Y(\Omega):x_{k}+y_{h}=z\}$$
Allo stesso modo, applicando i principi ottenuti parlando di [[CDP_05 - Variabili aleatorie#Trasformazioni di coppie di variabili aleatorie in spazi finiti|trasformazioni di coppie di variabili aleatorie]], possiamo arrivare a scrivere che:
$$\begin{align} \{Z=z\}=\{X+Y=z\}&=\,\bigcup_{(x_{k},\,y_{h})\,:\,x_{k}\,+\,y_{h}\,=\,z}\{X=x_{k},\,Y=y_{j}\}\\&=\,\bigcup_{k}\{X=x_{k},\,Y=z-x_{k}\}\\&=\,\bigcup_{h}\{X=z-y_{h},\,Y=y_{h}\} \end{align}$$
dove gli eventi $\{X=x_{k},\,Y=y_{h}\}$ sono disgiunti a due a due, così come gli eventi $\{X=x_{k},\,Y=z-x_{k}\}$ e gli eventi $\{X=z-y_{h},\,Y=y_{h}\}$. Dunque, ricordando che le variabili $X$ e $Y$ sono stocasticamente indipendenti, si ottiene che:
$$\begin{align} \mathbb{P}(\{Z=z\})&=\mathbb{P}(X+Y=z)\\&=\sum_{(x_{k},\,y_{h})\,:\,x_{k}\,+\,y_{h}\,=\,z}\mathbb{P}(X=x_{k})\,\mathbb{P}(Y=y_{h})\\&=\sum_{k}\mathbb{P}(X=x_{k})\,\mathbb{P}(Y=z-x_{k})\\&=\sum_{h}\mathbb{P}(X=z-y_{h})\,\mathbb{P}(Y=y_{h}) \end{align}$$
Risolviamo, ora, il secondo punto. Si tratta, sostanzialmente, di trovare l'espressione di:
$$\mathbb{P}(X=x_{k}\,|\,\{Z=z\})=\frac{\mathbb{P}(\{X=x_{k}\}\cap\{Z=z\})}{\mathbb{P}(Z=z)}$$
per i valori di $z$ tali per cui $\mathbb{P}(Z=z)\neq 0$. Basterà osservare che $\{X=x_{k}\}\cap\{Z=z\}=\{X=x_{k},\,Z=z\}$ coincide con l'evento $\{X=x_{k},\,X+Y=z\}=\{X=x_{k},\,Y=z-x_{k}\}$, e dunque sfruttando quanto ottenuto nel punto precedente possiamo scrivere:
$$\mathbb{P}(\{X=x_{k}\}\,|\,\{X+Y=z\})=\frac{\mathbb{P}(X=x_{k},\,Y=z-x_{k})}{\sum_{k'}\mathbb{P}(X=x_{k'},\,Y=z-x_{k'})}$$

Consideriamo, ora, un altro esempio. Siano $X$ e $Y$ due variabili aleatorie stocasticamente indipendenti, con distribuzioni binomiali rispettivamente di parametri $(r,\,\theta)$ e $(s,\,\theta)$: vogliamo determinare, in questo contesto, la distribuzione di probabilità della variabile $Z=X+Y$, e la distribuzione di probabilità condizionata di $X$ dato $\{Z=k\}$, con $0\le k\le r+s$. Per il primo punto, ricordiamo che $X\sim Bin(r,\,\theta)$ e $Y\sim Bin(s,\,\theta)$ sono due variabili indipendenti, e che $Z=X+Y$; da ciò, otteniamo che:
$$Z=X+Y\sim Bin(r+s,\,\theta)$$
Infatti, essendo $X\sim Bin(r,\,\theta)$ e $Y\sim Bin(s,\,\theta)$, abbiamo che $Z(\Omega)=0,\,1,\,2,\,\dots,\,r+s$, e dunque che:
$$\begin{align} \mathbb{P}(Z=l)=\mathbb{P}(X+Y=l)&=\sum_{k,\,h\,:\,k+h=l,\,0\,\le\,k\,\le\,r,\,0\,\le\,h\,\le\,s}\binom{r}{k}\theta^k(1-\theta)^{r-k}\,\binom{s}{h}\theta^h(1-\theta)^{s-h}\\&=\sum_{k,\,h\,:\,k+h=l,\,0\,\le\,k\,\le\,r,\,0\,\le\,h\,\le\,s}  \binom{r}{k}\binom{s}{h}\,\theta^l(1-\theta)^{r+s-l}\\&=\theta^l(1-\theta)^{r+s-l}\,\sum_{0\,\le\,k\,\le\,r,\,0\,\le\,l-k\,\le\,s}\binom{r}{k}\binom{s}{l-k} \end{align}$$
La sommatoria presente nel risultato finale può essere riscritta sfruttando l'[[CDP_02 - Probabilità#Combinazioni|identità di Vandermonde]], portando al seguente risultato:
$$\mathbb{P}(Z=l)=\theta^l\,(1-\theta)^{r+s-l}\,\binom{r+s}{l}$$
Per il secondo punto, dimostreremo che la distribuzione condizionata di $X$ dato $\{Z=k\}$ è di tipo ipergeometrico, e in particolare che:
$$\mathbf{P}_{X\,|\,Z}(\cdot\,|\,\{k\})\sim Hyp(r+s,\,r,\,k)$$
Per dimostrare ciò, utilizziamo la definizione di [[CDP_05 - Variabili aleatorie#Distribuzioni condizionate|probabilità condizionata tra variabili aleatorie]], e scriviamo dunque:
$$\mathbb{P}(X=i\,|\,Z=k)=\frac{\mathbb{P}(X=i,\,Z=k)}{\mathbb{P}(Z=k)}$$
Ricordiamo, a questo punto, che l'evento $\{X=i,\,Z=k\}$ coincide con l'evento $\{X=i,\,Y=k-i\}$, e che quest'ultimo è diverso dall'insieme vuoto (dunque, ha una probabilità $>0$ di avvenire) solo se $0\le i\le r$ e $0\le k-i \le s$. Inoltre, tenendo conto che $\theta^i\theta^{k-i}=\theta^k$, e che $(1-\theta)^{r-i}(1-\theta)^{s-(k-i)}=(1-\theta)^{r+s-k}$, si ottiene che:
$$\begin{align} \mathbb{P}(X=i\,|\,Z=k)= \frac{\mathbb{P}(X=i,\,Y=k-i)}{\mathbb{P}(Z=k)}&=\frac{\mathbb{P}(X=i)\,\mathbb{P}(Y=k-i)}{\mathbb{P}(Z=k)}\\&=\frac{\binom{r}{i}\theta^i(1-\theta)^{r-i}\,\binom{s}{k\,-\,i}\theta^{k-i}(1-\theta)^{s-(k-i)}}{\binom{r\,+\,s}{k}\theta^k(1-\theta)^{r+s-k}}\\&= \frac{\binom{r}{i}\binom{s}{k\,-\,i}}{\binom{r\,+\,s}{k}}\end{align}$$
Il risultato ottenuto, com'è facile notare, definisce una distribuzione ipergeometrica.
___
## Valore atteso di una variabile aleatoria

In questo paragrafo, si introdurrà il concetto di "**valore atteso di una variabile aleatoria**", spiegandone il significato e alcune proprietà fondamentali.

In molti problemi di tipo probabilistico, considerata una variabile aleatoria $X$ sorge la necessità di individuare una quantità deterministica che, in certi versi, sia "equivalente" a $X$. Cominciamo, per capire meglio cosa si intende, a vedere la definizione di tale concetto:

> Sia $X:\Omega\rightarrow X(\Omega)$, con $\Omega=\{\omega_{1},\,\omega_{2},\,\dots,\,\omega_{N}\}$ una variabile aleatoria definita su $(\Omega,\,\mathcal{P}(\Omega))$; se su tale tupla è definita una probabilità $\mathbb{P}$, si può definire "**valore atteso di $X$ rispetto a $\mathbb{P}$**" il valore:
> $$\mathbb{E}(X):=\sum_{i\,=\,1}^{N}p(\omega_{i})\,X(\omega_{i})$$

Potremmo vedere, in modo forse inaccurato ma più comprensibile, il valore atteso di una variabile aleatoria come una sorta di "**media pesata**" dei valori che tale variabile può assumere, dove i pesi in questione sono determinati dalla distribuzione di probabilità della variabile considerata. Del resto, oltre a "valore atteso" si utilizzano anche i termini "**valore medio**", "**aspettazione**" e "**speranza matematica**" per riferirsi a questo concetto.

##### Proprietà del valore atteso

Prima di passare ad alcuni esempi illustrativi, elenchiamo alcune **proprietà** che derivano immediatamente dalla definizione appena data, in cui considereremo variabili aleatorie $X$, $Y$ e $Z$ tutte definite sullo stesso spazio $\Omega=\{\omega_{1},\,\omega_{2},\,\dots,\,\omega_{N}\}$. La prima proprietà che andremo a vedere è abbastanza banale:

> Se $X$ è una [[CDP_05 - Variabili aleatorie#Variabili aleatorie degeneri e binarie|variabile aleatoria degenere]], dunque tale per cui $X(\omega_{i})=\hat{x}$ per ogni $i=1,\,2,\,\dots,\,N$, allora si ha che:
> $$\mathbb{E}(X)=\hat{x}$$

Passiamo, ora, a una proprietà relativa alle [[CDP_05 - Variabili aleatorie#Variabili aleatorie degeneri e binarie|variabili aleatorie binarie]].

> Sia $E\subseteq \Omega$ un evento, e $X=1_{E}$ la variabile aleatoria indicatrice di $E$, si ha che:
> $$\mathbb{E}(X)=\mathbb{E}(1_{E})=\mathbb{P}(E)$$

Ciò è facilmente dimostrabile ricordando la definizione di "indicatore": una variabile $1_{E}(\omega)$ del genere può assumere solo i valori $0$ e $1$, e in particolare assume il valore $0$ se e solo se $\omega\in\overline{E}$, mentre assume il valore $1$ se e solo se $\omega\in E$, dunque si ottiene che:
$$\begin{align} \mathbb{E}(X)=\mathbb{E}(1_{E})&=\sum_{i\,=\,1}^{N}1_{E}(\omega_{i})\,p(\omega_{i})\\&=\sum_{i\,:\,\omega_{i}\,\in\,E}\overbrace{1_{E}(\omega_{i})}^{=\,1}\,p(\omega_{i})\,+\,\sum_{i\,:\,\omega_{i}\,\in\,\overline{E}}\overbrace{1_{E}(\omega_{i})}^{=\,0}\,p(\omega_{i})\\&=\sum_{i\,:\,\omega_{i}\,\in\,E}p(\omega_{i})=\mathbb{P}(E) \end{align}$$

> Siano $a\le b$ due numeri reali tali che $a\le X(\omega_{i})\le b$ per ogni $i$ compreso tra $1$ e $N$, allora si ha sicuramente che:
> $$a\le\mathbb{E}(X)\le b$$

Più in generale vale la cosiddetta "**proprietà di monotonia**":

> Siano $X$ e $Y$ due variabili aleatorie, e sia $X(\omega)\le Y(\omega)$ per ogni $\omega\in \Omega$, allora si ha sicuramente che:
> $$\mathbb{E}(X)\le\mathbb{E}(Y)$$

Verificare la proprietà di monotonia è molto semplice: essendo $p(\omega)\ge 0$ per ogni $\omega\in \Omega$, si ha che se $X(\omega)\le Y(\omega)$ allora anche $X(\omega)\,p(\omega)\le Y(\omega)\,p(\omega)$ per ogni $\omega$; di conseguenza, si può affermare che:
$$\overbrace{\sum_{i\,=\,1}^{N}X(\omega_{i})\,p(\omega_{i})}^{=\,\mathbb{E}(X)}\,\le\,\overbrace{\sum_{i\,=\,1}^{N}Y(\omega_{i})\,p(\omega_{i})}^{=\,\mathbb{E}(Y)}$$

Un'altra proprietà, assolutamente fondamentale per la comprensione e l'utilizzo del valore atteso, è la "**proprietà di linearità**".

> Siano $a$ e $b$ due numeri reali arbitrari, e $X$ e $Y$ due variabili aleatorie definite su $\Omega$. Ora, consideriamo la variabile aleatoria $Z$ definita come la **combinazione lineare di $X$ e $Y$ con coefficienti $a$ e $b$**, ossia:
> $$Z(\omega_{i})=aX(\omega_{i})+bY(\omega_{i})\,\,\,\,\,\,\,\,\,\,\text{per ogni }1\le i\le N$$
> Si ha che:
> $$\mathbb{E}(Z)=a\mathbb{E}(X)+b\mathbb{E}(Y)$$

Per dimostrare questa proprietà, basterà sviluppare l'espressione di $\mathbb{E}(Z)$:
$$\begin{align} \mathbb{E}(Z)=\mathbb{E}(aX+bY)&=\sum_{i\,=\,1}^{N}p(\omega_{i})\,[aX(\omega_{i})+bY(\omega_{i})]\\&=\sum_{i\,=\,1}^{N}[aX(\omega_{i})\,p(\omega_{i})+bY(\omega_{i})\,p(\omega_{i})]\\&= a\sum_{i\,=\,1}^{N}p(\omega_{i})\,X(\omega_{i})+b\sum_{i\,=\,1}^{N}p(\omega_{i})\,Y(\omega_{i})\\&=a\mathbb{E}(X)+b\mathbb{E}(Y)\end{align}$$

Come immediati corollari della proprietà appena dimostrata, otteniamo le due seguenti proprietà.

> Sia $a$ un numero reale, e considerata una variabile aleatoria $X$ poniamo un'altra variabile $Z=aX$; risulta che:
> $$\mathbb{E}(Z)=a\mathbb{E}(X)$$

> Sia $b$ un numero reale, e considerata una variabile aleatoria $X$ poniamo un'altra variabile $Z=X+b$; risulta che:
> $$\mathbb{E}(Z)=\mathbb{E}(X)+b$$

Inoltre, si specifica che la proprietà di linearità può essere facilmente estesa al caso generico in cui si stanno considerando $l$ variabili aleatorie.

> Date $l$ variabili aleatorie $X_{1},\,X_{2},\,\dots,\,X_{l}$ e $l$ numeri reali $a_{1},\,a_{2},\,\dots,\,a_{l}$, si ha che:
> $$\mathbb{E}\left( \sum_{k\,=\,1}^{l}a_{k}X_{k} \right)=\sum_{k\,=\,1}^{l}a_{k}\,\mathbb{E}(X_{k})$$

Di fatto, per calcolare il valore atteso $\mathbb{E}(X)$ di una variabile aleatoria $X$, occorre naturalmente conoscere la distribuzione di probabilità di $X$, ossia i vari valori $p(\omega_{i})$ per $i=1,\,2,\,\dots,\,N$, ma non è necessariamente richiesto conoscere quale sia l'intero spazio di probabilità $\Omega$ su cui $X$ è definita, né quale sia la misura di probabilità su $(\Omega,\,\mathcal{P}(\Omega))$. **Il valore atteso**, infatti, **dipende solo dalla distribuzione di $X$ e dai valori che $X$ può assumere**, come viene esplicitato chiaramente nella seguente proposizione.

> Sia $X$ una variabile aleatoria definita su un arbitrario spazio finito $\Omega$, e tale per cui $X(\Omega)=\{x_{1},\,x_{2},\,\dots,\,x_{n}\}$. Risulta, allora, che:
> $$\mathbb{E}(X)\,=\,\sum_{j\,=\,1}^{n}x_{j}\cdot\mathbb{P}(\{X=x_{j}\})\,=\,\sum_{j\,=\,1}^{n}x_{j}\cdot p_{X}(x_{j})$$

Dimostriamo questa proposizione. Dal momento che $\{\{X=x_{1}\},\,\{X=x_{2}\},\,\dots,\,\{X=x_{n}\}\}$ rappresenta una partizione dello spazio $\Omega$, possiamo scrivere:
$$\mathbb{E}(X)=\sum_{i\,=\,1}^{N}p(\omega_{i})\,X(\omega_{i})=\sum_{j\,=\,1}^{n}\left[ \sum_{i\,:\,X(\omega_{i})\,=\,x_{j}}p(\omega_{i})\,X(\omega_{i}) \right]$$
ossia la somma prima di tutti i prodotti $p(\omega_{i})\,X(\omega_{i})$ tali per cui $\omega_{i}$ appartiene a $\{X=x_{1}\}$, poi dei prodotti tali per cui $\omega_{i}$ appartiene a $\{X=x_{2}\}$, e a seguire fino ad arrivare a $\{X=x_{n}\}$. D'altra parte, per ogni $j\in\{1,\,2,\,\dots,\,n\}$ fissato, si ha naturalmente che:
$$\sum_{i\,:\,X(\omega_{i})\,=\,x_{j}}p(\omega_{i})\,X(\omega_{i})\,=\,\sum_{i\,:\,X(\omega_{i})\,=\,x_{j}}p(\omega_{i})\,x_{j}\,=\,x_{j}\sum_{i\,:\,X(\omega_{i})\,=\,x_{j}}p(\omega _{i})\,=\,x_{j}\cdot\mathbb{P}(\{X=x_{j}\})$$
come volevasi dimostrare.
___
##### Valore atteso di una variabile aleatoria a valori interi non negativi

Nel caso specifico in cui si sta considerando una **variabile aleatoria $X$ con valori in $\{0,\,1,\,\dots,\,n\}$**, il calcolo del valore atteso può convenientemente essere eseguito considerando la funzione $j\mapsto\mathbb{P}(\{X>j\})$. Vale, infatti, la seguente equivalenza:

> Sia $X(\Omega)\subseteq\{0,\,1,\,\dots,\,n\}$; allora si ha:
> $$\mathbb{E}(X)=\sum_{j\,=\,0}^{n\,-\,1}\mathbb{P}(\{X>j\})$$
> In particolare, se $X(\Omega)=\{1,\,2,\,\dots,\,n\}$, allora si ha:
> $$\mathbb{E}(X)=1+\sum_{j\,=\,1}^{n\,-\,1}\mathbb{P}(\{X>j\})$$

Per dimostrare le proposizioni appena ottenute, ricordiamo innanzitutto la principale conclusione che abbiamo ottenuto parlando, in precedenza, di [[CDP_05 - Variabili aleatorie#Variabili aleatorie a valori interi|variabili aleatorie a valori interi]]:
$$\mathbb{P}(\{X=j\})\,=\,\mathbb{P}(\{X>j-1\})-\mathbb{P}(\{X>j\})$$
Possiamo utilizzare questa relazione nello sviluppo dell'espressione generica di $\mathbb{E}(X)$:
$$\begin{align} \mathbb{E}(X)&=\sum_{j\,=\,0}^{n}j\cdot\mathbb{P}(\{X=j\})\\&=\sum_{j\,=\,1}^{n}j\cdot\mathbb{P}(\{X=j\})\\&= \sum_{j\,=\,1}^{n}j\cdot[\mathbb{P}(\{X>j-1\})-\mathbb{P}(\{X>j\})]\\&=\sum_{j\,=\,1}^{n}[j\cdot\mathbb{P}(\{X>j-1\})-j\cdot\mathbb{P}(\{X>j\})]\\&=\sum_{j\,=\,1}^{n}j\cdot\mathbb{P}(\{X>j-1\})-\sum_{j\,=\,1}^{n}j\cdot\mathbb{P}(\{X>j\}) \end{align}$$
Ora, ponendo $h=j-1$, e ricordando che stiamo considerando $X(\Omega)\subseteq\{0,\,1,\,\dots,\,n\}$, per cui $\mathbb{P}(\{X>n\})=0$, possiamo scrivere:
$$\begin{align} \mathbb{E}(X)&=\sum_{j\,=\,1}^{n}j\cdot\mathbb{P}(\{X>j-1\})-\sum_{j\,=\,1}^{n}j\cdot\mathbb{P}(\{X>j\})\\&=\sum_{h\,=\,0}^{n\,-\,1}(h+1)\,\mathbb{P}(\{X>h\})-\sum_{j\,=\,1}^{n\,-\,1}j\cdot\mathbb{P}(X>j)\\&= 1\cdot\mathbb{P}(\{X>0\})+2\cdot\mathbb{P}(\{X>1\})+\,\dots\,+n\cdot\mathbb{P}(\{X>n-1\})-1\cdot\mathbb{P}(\{X>1\})-2\cdot\mathbb{P}(\{X>2\})-\,\dots\,-(n-1)\,\mathbb{P}(\{X>n-1\})\\&=\mathbb{P}(\{X>0\})+(2-1)\,\mathbb{P}(\{X>1\})+\,\dots\,+(n-(n-1))\,\mathbb{P}(\{X>n-1\})\\&=\mathbb{P}(\{X>0\})+\sum_{h\,=\,1}^{n\,-\,1}((h-1)-h)\,\mathbb{P}(\{X>h\})\\&=\sum_{h\,=\,0}^{n\,-\,1}\mathbb{P}(\{X>h\}) \end{align}$$
il che dimostra la prima forma della proposizione presentata. Per quanto riguarda la seconda, la sua dimostrazione deriva direttamente da quella della prima, con l'unica differenza che, ponendo $X(\Omega)=\{1,\,2,\,\dots,\,n\}$, si ha che $\mathbb{P}(\{X>0\})=1$.

Applichiamo, ora, questo modo di calcolare il valore atteso a un esempio concreto. Consideriamo il lancio di due dadi, con le due variabili $X$ e $Y$ che rappresentano i punteggi ottenuti dagli stessi, e consideriamo anche la variabile $Z=max(X,\,Y)$, ossia la variabile aleatoria definita come il punteggio massimo ottenuto tra i due dadi lanciati; vogliamo calcolare $\mathbb{E}(Z)$. Innanzitutto, chiariamo che per natura di $Z$ si ha $Z(\Omega)=\{1,\,2,\,\dots,\,6\}$; inoltre, ricordando dei calcoli fatti in un [[CDP_05 - Variabili aleatorie#Variabili aleatorie a valori interi|esempio simile]] qualche paragrafo fa, sappiamo che:
$$\mathbb{P}(\{Z\le x\})=\left( \frac{x}{6} \right)^{2}$$
per qualsiasi $x\in Z(\Omega)$, dunque si può affermare di conseguenza che:
$$\mathbb{P}(\{Z>x\})=1-\mathbb{P}(\{Z\le x\})=1-\left( \frac{x}{6} \right)^{2}$$
Da ciò, possiamo applicare la formula che abbiamo dimostrato poco fa per ottenere il valore atteso $\mathbb{E}(Z)$:
$$\begin{align} \mathbb{E}(Z)&=1+\sum_{j\,=\,1}^{6\,-\,1}\mathbb{P}(\{Z>j\})\\&=1+\sum_{j\,=\,1}^{5}(1-\mathbb{P}(\{Z\le j\}))\\&=1+\sum_{j\,=\,1}^{5}1-\sum_{j\,=\,1}^{5}\mathbb{P}(\{Z\le j\})\\&= 1 + 5 - \frac{1+4+9+16+25}{36}\\&=1+5- \frac{55}{36}\\&\approx 4.472 \end{align}$$
___
##### Valori attesi notevoli

In questo paragrafo, espliciteremo alcuni "**valori attesi notevoli**", ossia valori attesi di tipi di variabili aleatorie noti, che abbiamo già visto in precedenza.

Vediamo un primo caso, ossia quello delle **[[CDP_05 - Variabili aleatorie#Variabili aleatorie binomiali|variabili aleatorie con distribuzione binomiale]]**: considerata una variabile $X$ con distribuzione binomiale di parametri $n$ e $\theta$, abbiamo che:
$$\mathbb{E}(X)=\sum_{k\,=\,0}^{n}k\cdot p_{X}(k)=\sum_{k\,=\,0}^{n}k\binom{n}{k}\theta^{k}(1-\theta)^{n-k}$$
In realtà, possiamo ottenere il valore di $\mathbb{E}(X)$ anche senza tutti questi calcoli. Consideriamo $n$ [[CDP_05 - Variabili aleatorie#Variabili aleatorie degeneri e binarie|variabili aleatorie binarie]] $X_{1},\,X_{2},\,\dots,\,X_{n}$, con $\mathbb{P}(\{X_{j}=1\})=\theta$ per ogni $j=1,\,2,\,\dots,\,n$; è immediato il calcolo del valore atteso di ciascuna delle variabili $X_{j}$, ossia:
$$\mathbb{E}(X_{j})=0\cdot\mathbb{P}(X_{j}=0)+1\cdot\mathbb{P}(X_{j}=1)=\theta$$
di conseguenza, per la [[CDP_05 - Variabili aleatorie#Proprietà del valore atteso|proprietà di linearità]] del valore atteso, si ha che:
$$\mathbb{E}\left( \sum_{j\,=\,1}^{n}X_{j} \right)=\sum_{j\,=\,1}^{n}\mathbb{E}(X_{j})=n\theta$$
Sappiamo, d'altra parte, che nel caso particolare in cui $X_{1},\,X_{2},\,\dots,\,X_{n}$ sono indicatori di eventi completamente indipendenti, la variabile aleatoria $S=\sum_{j\,=\,1}^{n}X_{j}$ segue una distribuzione binomiale di parametri $n$ e $\theta$, la stessa di $X$; dunque, visto che il valore atteso di una variabile aleatoria dipende soltanto dalla sua distribuzione di probabilità, abbiamo che, per la nostra variabile aleatoria $X$:
$$\mathbb{E}(X)=\mathbb{E}(S)=n\theta$$

Consideriamo, stavolta, una **distribuzione ipergeometrica di parametri $M$, $m_{1}$ e $n$**, che sappiamo essere ad esempio la distribuzione di probabilità di una variabile aleatoria $S$ che conta il numero di successi su $n$ eventi non indipendenti, ciascuno di probabilità $\frac{m_{1}}{M}$. Possiamo scrivere:
$$S=\sum_{i\,=\,1}^{n}1_{A_{i}}$$
con $A_{i}=\{\text{l'}i\text{-esimo evento risulta in un successo}\}$. Riconducendoci al problema delle [[CDP_04 - Probabilità binomiali e ipergeometriche#Probabilità ipergeometriche|estrazioni casuali senza reinserimento]], problema perfettamente equivalente, sappiamo che $\mathbb{P}(A_{i})=\mathbb{P}(A_{1})=\frac{m_{1}}{M}$, e quindi:
$$\mathbb{E}(S)=\mathbb{E}\left( \sum_{i\,=\,1}^{n}1_{A_{i}} \right)=\sum_{i\,=\,1}^{n}\mathbb{E}(1_{A_{i}})=n\cdot\mathbb{P}(A_{1})=n\cdot \frac{m_{1}}{M}$$

Ora, spostiamoci nel considerare il **valore atteso di una media aritmetica**. In particolare, consideriamo $n$ variabili aleatorie $X_{1},\,X_{2},\,\dots,\,X_{n}$, definite su uno stesso spazio $(\Omega,\,\mathcal{P}(\Omega))$ e che abbiano tutte lo stesso valore atteso, il che vuol dire che usando il simbolo $\mu:=\mathbb{E}(X_{j})$ vale che:
$$\mathbb{E}(X_{1})=\mathbb{E}(X_{2})=\,\dots\,=\mathbb{E}(X_{n})=\mu$$
Consideriamo, ora, sullo stesso spazio la variabile aleatoria $Y_{n}$, definita come media aritmetica delle variabili $X_{1},\,X_{2},\,\dots,\,X_{n}$:
$$Y_{n}(\omega_{i})=\frac{\sum_{j\,=\,1}^{n}X_{j}(\omega_{i})}{n}$$
Si ha che:
$$\mathbb{E}(Y_{n})=\mu$$
La dimostrazione di quest'equivalenza è banale: basta osservare che, per la proprietà di linearità, si ottiene che:
$$\mathbb{E}(Y_{n})=\frac{1}{n}\sum_{j\,=\,1}^{n}\mathbb{E}(X_{j})=\frac{n\mu}{n}=\mu$$
A parità di valore atteso, però, possono sussistere anche situazioni ben diverse per quanto riguarda la probabilità di $Y_{n}$, a seconda delle correlazioni tra le variabili $X_{1},\,X_{2},\,\dots,\,X_{n}$; si approfondirà questo aspetto quando parleremo di [[CDP_05 - Variabili aleatorie#Varianza e covarianza di variabili aleatorie|varianza e covarianza]]. Per ora, consideriamo un esempio concreto e, in un certo senso, estremo di quanto detto finora. Consideriamo una lotteria in cui vengono venduti $n$ biglietti, numerati progressivamente, e supponiamo che tale lotteria distribuisca un totale di $r$ premi (naturalmente, $r<n$), di cui:
- $r_{1}$ "primi premi", di entità $c_{1}$;
- $r_{2}$ "secondi premi", di entità $c_{2}$;
- $r_{3}$ "terzi premi", di entità $c_{3}$;

con $r=r_{1}+r_{2}+r_{3}$ e con $c_{1}>c_{2}>c_{3}>0$. Indichiamo con $X_{1},\,X_{2},\,\dots,\,X_{n}$ le vincite rispettivamente associate ai biglietti $1,\,2,\,\dots,\,n$: esse rappresentano delle variabili aleatorie, i cui valori possibili costituiscono l'insieme $\{0,\,c_{1},\,c_{2},\,c_{3}\}$. Le variabili $X_{1},\,X_{2},\,\dots,\,X_{n}$ hanno tutte la stessa distribuzione di probabilità, definita da:
$$\mathbb{P}(\{X_{j}=c_{1}\})=\frac{r_{1}}{n}\,\,\,\,\,\,\,\,\,\,\mathbb{P}(\{X_{j}=c_{2}\})=\frac{r_{2}}{n}\,\,\,\,\,\,\,\,\,\,\mathbb{P}(\{X_{j}=c_{3}\})=\frac{r_{3}}{n}$$
mentre, per quanto riguarda $X_{j}=0$ si ha che:
$$\mathbb{P}(\{X_{j}=0\})=\frac{n-r}{n}\,\,\,\,\,\text{oppure}\,\,\,\,\,1-\mathbb{P}(\{X_{j}=c_{1}\})-\mathbb{P}(\{X_{j}=c_{2}\})-\mathbb{P}(\{X_{j}=c_{3}\})$$
Si ha, dunque, che il valore atteso della variabile aleatoria generica $X_{j}$ è:
$$\mathbb{E}(X_{j})=\frac{r_{1}c_{1}+r_{2}c_{2}+r_{3}c_{3}}{n}$$
Volendo, avremmo potuto procedere anche in un altro modo, sfruttando il concetto di valore atteso della media aritmetica. Logicamente, è ovvio che $X_{1},\,X_{2},\,\dots,\,X_{n}$ abbiano tutte lo stesso valore atteso $\mathbb{E}(X_{j})=\mu$; a questo punto, andiamo a considerare la variabile aleatoria
$$S_{n}=\sum_{j\,=\,1}^{n}X_{j}$$
Osserviamo che $S_{n}$ assume il significato di ammontare complessivo dei premi distribuiti dalla lotteria, e perciò risulta essere una variabile aleatoria degenere di valore $r_{1}c_{1}+r_{2}c_{2}+r_{3}c_{3}$, ovvero:
$$S_{n}(\omega)=r_{1}c_{1}+r_{2}c_{2}+r_{3}c_{3}\,\,\,\,\,\text{per ogni }\omega\in \Omega$$
Come abbiamo visto [[CDP_05 - Variabili aleatorie#Proprietà del valore atteso|in precedenza]], il valore atteso di una variabile aleatoria degenere coincide con il valore assunto dalla stessa, dunque abbiamo che:
$$\mathbb{E}(S_{n})=r_{1}c_{1}+r_{2}c_{2}+r_{3}c_{3}$$
e per la proprietà di linearità si deve avere:
$$\mathbb{E}(S_{n})=\mathbb{E}\left( \sum_{j\,=\,1}^{n}X_{j} \right)=n\mu$$
Dunque, si ottiene facilmente che:
$$\mu=\frac{\mathbb{E}(S_{n})}{n}=\frac{r_{1}c_{1}+r_{2}c_{2}+r_{3}c_{3}}{n}$$

Vediamo un altro esempio, in cui supponiamo di avere un biglietto di una lotteria $A$  e un biglietto di un'altra lotteria $B$, dove $A$ distribuisce $r_{1}'$ premi di entità $c_{1}'$ e $r_{2}'$ premi di entità $c_{2}'$ su un totale di $n'$ biglietti, mentre $B$ distribuisce $r_{1}''$ premi di entità $c_{1}''$ e $r_{2}''$ premi di entità $c_{2}''$ su un totale di $n''$ biglietti. Indichiamo, a questo punto, con $X$ la variabile aleatoria che indica la vincita complessivamente derivante dai due biglietti, e vogliamo calcolare il valore atteso $\mathbb{E}(X)$. Per comodità, indichiamo con $X'$ e $X''$ rispettivamente le vincite relative ai due singoli biglietti, in modo che $X=X'+X''$; in questo contesto, abbiamo che $X'$ può assumere i valori $\{0,\,c_{1}',\,c_{2}'\}$, mentre $X''$ può assumere i valori $\{0,\,c_{1}'',\,c_{2}''\}$, e risulta:
$$\mathbb{E}(X')=\frac{c_{1}'r_{1}'+c_{2}'r_{2}'}{n'}\,\,\,\,\,\,\,\,\,\,\mathbb{E}(X'')=\frac{c_{1}''r_{1}''+c_{2}''r_{2}''}{n''}$$
Sempre grazie alla proprietà di linearità, sottolineiamo che per calcolare il valore atteso $\mathbb{E}(X)$ non sarà necessario calcolare interamente la distribuzione di probabilità di $X$; infatti, possiamo ottenere immediatamente che:
$$\mathbb{E}(X)=\mathbb{E}(X')+\mathbb{E}(X'')$$

Torniamo all'esempio precedente, quello relativo a una singola lotteria, e introduciamo stavolta anche il costo $c$ di un singolo biglietto. L'acquirente del biglietto $j$, dunque, pagherà sicuramente un prezzo $c$ per avere una possibilità di vincita di un guadagno aleatorio $X_{j}$, il cui valore atteso è $\mu=\frac{r_{1}c_{1}\,+\,r_{2}c_{2}\,+\,r_{3}c_{3}}{n}$; per quanto riguarda, invece, l'organizzatore della lotteria, nell'ipotesi che esso venda tutti gli $n$ biglietti ottiene un ricavo $R$ pari a:
$$R=n\cdot(c-\mu)$$
che sarà positivo, negativo o nullo a seconda che $\mu$ sia rispettivamente minore, maggiore o uguale a $c$; ciononostante, $R$ è un ricavo certo, nel senso che non dipende dal risultato aleatorio della lotteria, a differenza del guadagno $X_{j}$ di chi compra un biglietto. Su tale base, si può interpretare il valore atteso $\mathbb{E}(X_{j})=\mu$ come il "**prezzo equo**" per l'acquisto di un singolo biglietto, ossia quello per cui nessuna delle due parti coinvolte si trova sicuramente in perdita rispetto all'altra; più in generale, si parla di "**gioco equo**" quando, a lungo termine, le probabilità di guadagno e di perdita sono uguali per tutti i giocatori.
___
##### Valori attesi di trasformazioni di variabili aleatorie

Per parlare del **valore atteso di una trasformazione di variabili aleatorie**, è opportuno esplicitare la seguente proprietà:

> Siano $X$ e $Y$ due [[CDP_05 - Variabili aleatorie#Indipendenza stocastica tra variabili aleatorie|variabili aleatorie indipendenti]] definite su uno stesso spazio di probabilità, allora si ha che:
> $$\mathbb{E}(X\cdot Y)=\mathbb{E}(X)\cdot\mathbb{E}(Y)$$

Dimostriamo questa proprietà. Siano rispettivamente $X(\Omega)=\{x_{1},\,x_{2},\,\dots,\,x_{n}\}$ e $Y(\Omega)=\{y_{1},\,y_{2},\,\dots,\,y_{m}\}$ gli insiemi di valori assumibili dalle variabili $X$ e $Y$, possiamo considerare la partizione dello spazio campione $\Omega$ costituita dagli eventi del tipo:
$$H^{X,\,Y}_{h,\,k}=\{X=x_{h}\}\cap\{Y=y_{k}\}:=\{\omega_{i}\in \Omega:X(\omega_{i})=x_{h},\,Y(\omega_{i})=y_{k}\}$$
per $h=1,\,2,\,\dots,\,n$ e $k=1,\,2,\,\dots,\,m$. A questo punto, consideriamo che:
$$X\cdot Y=\sum_{h\,=\,1}^{n}\sum_{k\,=\,1}^{m}x_{h}\, y_{k}\cdot1_{H_{h,\,k}^{X,\,Y}}$$
Per la [[CDP_05 - Variabili aleatorie#Proprietà del valore atteso|proprietà di linearità]] del valore atteso, ora, possiamo scrivere che:
$$\mathbb{E}(X\cdot Y)=\sum_{h\,=\,1}^{n}\sum_{k\,=\,1}^{m}x_{h}\,y_{k}\cdot\mathbb{E}(1_{H_{h,\,k}^{X,\,Y}})=\sum_{h\,=\,1}^{n}\sum_{k\,=\,1}^{m}x_{h}\,y_{k}\cdot\mathbb{P}(\{X=x_{h}\}\cap\{Y=y_{k}\})$$
Infine, ricordandoci che le variabili aleatorie $X$ e $Y$ sono indipendenti, possiamo riscrivere la probabilità $\mathbb{P}(\{X=x_{h}\}\cap\{Y=y_{k}\})$ come $\mathbb{P}(\{X=x_{h}\})\cdot\mathbb{P}(\{Y=y_{k}\})$, il che ci porta a riscrivere il risultato appena ottenuto come:
$$\begin{align} \mathbb{E}(X\cdot Y)&=\sum_{h\,=\,1}^{n}\sum_{k\,=\,1}^{m}x_{h}\,y_{k}\cdot\mathbb{P}(X=x_{h})\cdot\mathbb{P}(Y=y_{k})\\&=\sum_{h\,=\,1}^{n}x_{h}\,\mathbb{P}(X=x_{h})\,\cdot\,\sum_{k\,=\,1}^{m}y_{k}\,\mathbb{P}(Y=y_{k})\\&=\mathbb{E}(X)\cdot\mathbb{E}(Y) \end{align}$$
come volevasi dimostrare.

[pag. 128/130]
___
##### Valore atteso condizionato e formula del valore atteso totale

Supponiamo di essere venuti a conoscenza del fatto che si è verificato un evento $A$, con $\mathbb{P}(A)>0$, e che per valutare la probabilità di un ulteriore evento $E$ vada utilizzata la [[CDP_02 - Probabilità#Probabilità condizionate|probabilità condizionata]] ad $A$, ossia $\mathbb{P}(E\,|\,A)$; in modo del tutto analogo, per valutare il valore atteso di una variabile aleatoria, andrebbe calcolato il valore atteso condizionato all'evento $A$, e per fare ciò utilizziamo la seguente definizione.

> Sia $A$ un evento, con $\mathbb{P}(A)>0$, e sia $X$ una variabile aleatoria che può assumere i valori $X(\Omega)=\{x_{1},\,x_{2},\,\dots,\,x_{n}\}$, si definisce "**valore atteso di $X$ condizionato all'evento $A$**" il valore:
> $$\mathbb{E}(X\,|\,A)\,=\,\sum_{i\,=\,1}^{N}X(\omega_{i})\,\mathbb{P}(\{\omega_{i}\}\,|\,A)\,=\,\sum_{k\,=\,1}^{n}x_{k}\,\mathbb{P}(X=x_{k}\,|\,A)$$

A questo punto, a partire dalla definizione appena data e dalla [[CDP_02 - Probabilità#Formula delle probabilità totali|formula delle probabilità totali]], possiamo ottenere la cosiddetta "**formula del valore atteso totale**", che mette in relazione il valore atteso $\mathbb{E}(X)$ di una variabile aleatoria $X$ con i valori attesi condizionati $\mathbb{E}(X\,|\,H_{j})$, con $j=1,\,2,\,\dots,\,m$ e dove gli eventi $H_{j}$ formano una partizione dello spazio campione $\Omega$.

> Data una partizione formata dagli eventi $H_{1},\,H_{2},\,\dots,\,H_{m}$, e se $\mathbb{P}(H_{j})>0$ per ogni $j=1,\,2,\,\dots,\,m$, allora vale che:
> $$\mathbb{E}(X)=\sum_{j\,=\,1}^{m}\mathbb{E}(X\,|\,H_{j})\,\mathbb{P}(H_{j})$$

La formula è facilmente dimostrabile applicando la definizione di valore atteso condizionato a un evento. Infatti, sappiamo che per ogni $j=1,\,2,\,\dots,\,m$ vale che:
$$\mathbb{E}(X\,|\,H_{j})=\sum_{k\,=\,1}^{n}x_{k}\,\mathbb{P}(X=x_{k}\,|\,H_{j})$$
e perciò sarà possibile riscrivere l'uguaglianza fornita come:
$$\mathbb{E}(X)=\sum_{j\,=\,1}^{m}\sum_{k\,=\,1}^{n}x_{k}\,\mathbb{P}(X=x_{k}\,|\,H_{j})\,\mathbb{P}(H_{j})$$
Ora, trattandosi di sommatorie finite sarà possibile scambiarne l'ordine senza alterare il risultato, dunque otteniamo:
$$\begin{align}\mathbb{E}(X) &= \sum_{k\,=\,1}^{n}\sum_{j\,=\,1}^{m}x_{k}\,\mathbb{P}(X=x_{k}\,|\,H_{j})\,\mathbb{P}(H_{j})\\&=\sum_{k\,=1}^{n}x_{k}\,\sum_{j\,=\,1}^{m}\mathbb{P}(X=x_{k}\,|\,H_{j})\,\mathbb{P}(H_{j}) \end{align}$$
Applichiamo, infine, la formula delle probabilità totali, in modo da arrivare alla seguente notazione:
$$\begin{align}\mathbb{E}(X)&=\sum_{k\,=\,1}^{n}x_{k}\,\sum_{j\,=\,1}^{m}\mathbb{P}(X=x_{k}\,|\,H_{j})\,\mathbb{P}(H_{j})\\&=\sum_{k\,=\,1}^{n}x_{k}\,\mathbb{P}(X=x_{k}) \end{align}$$
Notiamo che la notazione ottenuta equivale perfettamente alla definizione generale di valore atteso di una variabile aleatoria, dunque si è dimostrata la validità della formula del valore atteso totale.

Un'applicazione interessante della formula appena dimostrata si ha quando la partizione con cui si sta lavorando è generata da una variabile aleatoria $Y$ con valori in $Y(\Omega)=\{y_{1},\,y_{2},\,\dots,\,y_{m}\}$, ed è dunque composta da eventi del tipo:
$$H_{j}^{Y}:=\{Y=y_{j}\},\,\,\,\,\,\text{per }j=1,\,2,\,\dots,\,m$$
In questo caso, la formula diventa:
$$\begin{align} \mathbb{E}(X)&=\sum_{j\,=\,1}^{m}\mathbb{E}(X\,|\,H_{j}^{Y})\,\mathbb{P}(H_{j}^{Y})\\&=\sum_{j\,=\,1}^{m}\mathbb{E}(X\,|\,\{Y=y_{j}\})\,\mathbb{P}(Y=y_{j})\\&=\sum_{j\,=\,1}^{m}\left( \sum_{k\,=\,1}^{n}x_{k}\,\mathbb{P}(X=x_{k}\,|\,\{Y=y_{j}\}) \right)\,\mathbb{P}(Y=y_{j})\\&=\sum_{j\,=\,1}^{m}\left( \sum_{k\,=\,1}^{n}x_{k}\,p_{X\,|\,Y}(x_{k}\,|\,y_{j}) \right)\,p_{Y}(y_{j}) \end{align}$$

La formula del valore atteso totale torna particolarmente utile dato che permette di **calcolare il valore atteso della variabile aleatoria $X$ senza doverne calcolare la distribuzione**, nel caso in cui siano noti i valori attesi $\mathbb{E}(X\,|\,H_{j})$ (o, in altri casi, i valori attesi dell'eventuale variabile aleatoria $Y$).
___
## Varianza e covarianza di variabili aleatorie

Supponiamo di avere due [[CDP_05 - Variabili aleatorie#Cos'è una variabile aleatoria?|variabili aleatorie]] con lo stesso [[CDP_05 - Variabili aleatorie#Valore atteso di una variabile aleatoria|valore atteso]], ma con una distribuzione di probabilità diversa. A prima vista, le due variabili aleatorie sembrano risultare equivalenti (avendo lo stesso valore atteso), ed è dunque necessario trovare altri modi per differenziarle: uno di questi è considerare la cosiddetta "varianza" delle variabili aleatorie considerate. Ma cos'è la varianza?

> Sia $X:\Omega\to X(\Omega)$ una variabile aleatoria, ed indicato brevemente con $\mu$ il valore atteso di $X$, si dice "**varianza** di $X$", e si indica con la notazione $Var(X)$, il valore:
> $$Var(X)\,=\,\mathbb{E}((X-\mathbb{E}(X))^{2})\,:=\,\sum_{\omega_{i\,\in\,\Omega}}p(\omega_{i})\,(X(\omega_{i})-\mu)^{2}$$
> ossia, in parole povere, il valore atteso di $(X-\mu)^{2}$.

Come il valore atteso $\mathbb{E}(X)$, anche **la varianza $Var(X)$ dipende esclusivamente dalla distribuzione di probabilità di $X$**. 

In parole povere, il concetto di "varianza" può essere visto come un **indicatore dell'affidabilità del valore atteso**: nel caso in cui **la varianza sia un valore molto piccolo, i valori che può assumere la variabile aleatoria considerata dovrebbero essere per la maggior parte molto vicini tra loro**, dunque il valore atteso sarà notevolmente vicino a qualsiasi di questi valori; invece, **se la varianza è più grande, ciò implica che i valori assumibili dalla variabile considerata dovrebbero essere più dispersi** e contenuti in un intervallo più grande, dunque il valore atteso potrebbe anche essere notevolmente lontano da uno di questi valori.   

##### Proprietà della varianza

A questo punto, per comprendere più in profondità questo nuovo concetto, elenchiamo le **proprietà fondamentali della varianza**.

> **La varianza di una variabile aleatoria $X$ è sempre non negativa**, ovvero:
> $$Var(X)\ge 0$$
> Inoltre, se $p(\omega_{i})>0$ per ogni $\omega_{i}\in \Omega$, allora si avrà $Var(X)=0$ se e solo se $X$ è una [[CDP_05 - Variabili aleatorie#Variabili aleatorie degeneri e binarie|variabile aleatoria degenere]].

> Per ogni variabile aleatoria $X$, è possibile calcolarne la varianza anche attraverso la seguente formula:
> $$Var(X)\,=\,\mathbb{E}(X^{2})-\mu^{2}\,=\,\mathbb{E}(X^{2})-(\mathbb{E}(X))^{2}$$

La validità di tale formula è facilmente dimostrabile osservando che $(X-\mu)^{2}=X^{2}-2\mu X+\mu^{2}$, e applicando la [[CDP_05 - Variabili aleatorie#Proprietà del valore atteso|proprietà di linearità del valore atteso]], dunque:
$$Var(X)\,=\,\mathbb{E}((X-\mu)^{2})\,=\,\mathbb{E}(X^{2}-2\mu X+\mu^{2})\,=\,\mathbb{E}(X^{2})-2\mu\mathbb{E}(X)+\mu^{2}\,=\,\mathbb{E}(X)-(\mathbb{E}(X))^{2}$$

> Sia $Y=X+b$, con $b\in\mathbb{R}$, allora si ha che:
> $$Var(Y)=Var(X+b)=Var(X)$$

> Sia $Y=a\cdot X$, con $a\in\mathbb{R}$, allora si ha che:
> $$Var(Y)=Var(a\cdot X)=a^{2}\cdot Var(X)$$

Queste due proprietà, sostanzialmente, aiutano a semplificare e manipolare le varianze con cui si sta lavorando: la prima afferma che **le costanti additive nelle varianze sono trascurabili**, mentre la seconda afferma che **per estrapolare una costante moltiplicativa da una varianza, la si deve elevare al quadrato**.

> Siano $X$ e $Y$ due variabili aleatorie definite su $(\Omega,\,\mathcal{P}(\Omega))$, allora si ha che:
> $$Var(X+Y)=Var(X)+Var(Y)+2\mathbb{E}[(X-\mathbb{E}(X))(Y-\mathbb{E}(Y))]$$

Per dimostrare questa proprietà, ricordiamo la definizione di varianza, e sviluppiamo i calcoli che ne conseguono:
$$\begin{align} Var(X+Y)&=\mathbb{E}[(X+Y-\mathbb{E}(X+Y))^{2}]\\&=\mathbb{E}[(X-\mathbb{E}(X)+Y-\mathbb{E}(Y))^{2}]\\&=\mathbb{E}[(X-\mathbb{E}(X))^{2}+(Y-\mathbb{E}(Y))^{2}+2(X-\mathbb{E}(X))(Y-\mathbb{E}(Y))] \end{align}$$
A questo punto, possiamo applicare la proprietà di linearità del valore atteso, che ci permette di arrivare alla formula vista in precedenza:
$$\begin{align} Var(X+Y)&=\mathbb{E}[(X-\mathbb{E}(X))^{2}+(Y-\mathbb{E}(Y))^{2}+2(X-\mathbb{E}(X))(Y-\mathbb{E}(Y))]\\&=\mathbb{E}[(X-\mathbb{E}(X))^{2}]+\mathbb{E}[(Y-\mathbb{E}Y)^{2}]+2\mathbb{E}[(X-\mathbb{E}(X))(Y-\mathbb{E}(Y))]\\&=Var(X)+Var(Y)+2\mathbb{E}[(X-\mathbb{E}(X))(Y-\mathbb{E}(Y))] \end{align}$$
come volevasi dimostrare.
___
##### Covarianza di due variabili aleatorie

Se la [[CDP_05 - Variabili aleatorie#Varianza e covarianza di variabili aleatorie|varianza]] di una variabile aleatoria permette di avere più informazioni sui possibili risultati della stessa, la "covarianza" di due variabili aleatorie permette di ottenere informazioni sul **legame tra i valori assumibili da due variabili aleatorie distinte**. Prima di approfondire meglio questo concetto, si fornisce la sua definizione formale.

> Siano date, su uno stesso spazio di probabilità, due variabili aleatorie $X$ e $Y$ e, per comodità, si indichino brevemente con $\mu_{X}$ e $\mu_{Y}$ rispettivamente il valore atteso di $X$ e il valore atteso di $Y$. Si definisce "**covarianza** fra $X$ e $Y$", e si indica con la notazione $Cov(X,\,Y)$, il valore:
> $$Cov(X,\,Y)=\,\mathbb{E}[(X-\mu_{X})\cdot(Y-\mu_{Y})]$$

Tipicamente, la covarianza fra due variabili $X$ e $Y$ si può inserire in uno dei seguenti **tre scenari**:
- **$Cov(X,\,Y)>0$**, ovvero c'è una "**covarianza positiva**", caso in cui **le due variabili aleatorie considerate "viaggiano" nella stessa direzione** (se scende il valore di una, scende anche il valore dell'altra, e viceversa);
- $Cov(X,\,Y)>0$, ovvero c'è una "**covarianza negativa**", caso in cui **le due variabili aleatorie considerate "viaggiano" in direzioni opposte** (se scende il valore di una, sale il valore dell'altra, e viceversa);
- $Cov(X,\,Y)=0$, ovvero c'è una "**covarianza nulla**", caso in cui **la variazione di una variabile non dice nulla sulla variazione dell'altra** (è questo il caso delle variabili completamente indipendenti, la cui covarianza è necessariamente nulla).

Naturalmente, $Cov(X,\,Y) = Cov(Y,\,X)$; inoltre, se $Y=X$, allora la formula degenera in:
$$Cov(X,\,Y)\,=\,Cov(X,\,X)=Var(X)$$
Svolgendo il prodotto $(X-\mu_{X})\cdot(Y-\mu_{Y})$, e applicando la [[CDP_05 - Variabili aleatorie#Proprietà del valore atteso|proprietà di linearità del valore atteso]], è possibile poi ottenere una **formula alternativa per la covarianza**:
$$\begin{align} Cov(X,\,Y)&=\mathbb{E}[(X-\mu_{X})\cdot(Y-\mu_{Y})]\\&=\mathbb{E}(XY-X\mu_{Y}-Y\mu_{X}+\mu_{X}\mu_{Y})\\&=\mathbb{E}(X\cdot Y)-\mathbb{E}(X\cdot \mu_{Y})-\mathbb{E}(Y\cdot \mu_{X})+\mathbb{E}(\mu_{X}\cdot \mu_{Y})\\&=\mathbb{E}(X\cdot Y)-\mathbb{E}(X)\,\mu_{Y}-\mathbb{E}(Y)\,\mu_{X}+\mu_{X}\,\mu_{Y}\\&=\mathbb{E}(X\cdot Y)-\mu_{X}\,\mu_{Y}\\&=\mathbb{E}(X\cdot Y)-\mathbb{E}(X)\cdot\mathbb{E}(Y) \end{align}$$
Inoltre, utilizzando la covarianza sarà possibile riscrivere in modo più compatto una formula fornita elencando le [[CDP_05 - Variabili aleatorie#Proprietà della varianza|proprietà della varianza]], in particolare quella relativa alla varianza della somma di due variabili aleatorie $X$ e $Y$:
$$\begin{align} Var(X+Y)&=Var(X)+Var(Y)+2\mathbb{E}[(X-\mathbb{E}(X))(Y-\mathbb{E}(Y))]\\&=Var(X)+Var(Y)+2\,Cov(X,\,Y) \end{align}$$

Come abbiamo accennato in precedenza, c'è una stretta correlazione tra covarianza e [[CDP_05 - Variabili aleatorie#Indipendenza stocastica tra variabili aleatorie|indipendenza tra due variabili aleatorie]]. In particolare, vale la seguente proposizione:

> Siano date due variabili aleatorie $X$ e $Y$ definite sullo stesso spazio di probabilità, e siano $X$ e $Y$ stocasticamente indipendenti tra di loro, allora:
> $$Cov(X,\,Y)=0\,\,\,\,\,\,\,\,\,\,\text{e}\,\,\,\,\,\,\,\,\,\,Var(X+Y)=Var(X)+Var(Y)$$

La seconda conclusione è banale sfruttando la nuova formula della varianza $Var(X+Y)$ trovata poco fa, ma per ottenerla dobbiamo comunque dimostrare che $Cov(X,\,Y)=0$ se $X$ e $Y$ sono indipendenti: a questo scopo, basta ricordare che $Cov(X,\,Y)=\mathbb{E}(X\cdot Y)-\mathbb{E}(X)\cdot\mathbb{E}(Y)$, e che per due variabili aleatorie indipendenti si ha che $\mathbb{E}(X\cdot Y)=\mathbb{E}(X)\cdot\mathbb{E}(Y)$, il che porta all'annullamento della covarianza, come volevasi dimostrare.

Ora, generalmente l'implicazione vale con certezza in un solo verso: se due variabili $X$ e $Y$ sono indipendenti tra loro, la loro covarianza è nulla, ma se la covarianza di due variabili $X$ e $Y$ è nulla, non posso dire con certezza che $X$ e $Y$ sono indipendenti (in altri termini, **la condizione $Cov(X,\,Y)=0$ è necessaria, ma non sufficiente per l'indipendenza tra le variabili $X$ e $Y$**). Ciò vale sempre tranne per un caso particolare, ossia quello delle [[CDP_05 - Variabili aleatorie#Variabili aleatorie degeneri e binarie|variabili aleatorie binarie]], ossia quelle con valori in $\{0,\,1\}$. Infatti:

> Siano $X$ e $Y$ due variabili aleatorie binarie, definite su uno stesso spazio di probabilità, anche il loro prodotto $X\cdot Y$ sarà una variabile aleatoria binaria, con:
> $$\mathbb{E}(X\cdot Y)\,=\,\mathbb{P}(\{X\cdot Y=1\})=\mathbb{P}(\{X=1\}\cap\{Y=1\})$$
> Dunque, si ha che:
> $$Cov(X,\,Y)\,=\,\mathbb{P}(\{X=1\}\cap\{Y=1\})-\mathbb{P}(\{X=1\})\cdot\mathbb{P}(\{Y=1\})$$

A questo punto, se ponessimo la covarianza $Cov(X,\,Y)=0$, otterremmo che:
$$\mathbb{P}(\{X=1\}\cap\{Y=1\})=\mathbb{P}(\{X=1\})\cdot\mathbb{P}(\{Y=1\})$$
e dato che una variabile aleatoria binaria può assumere solo valori in $\{0,\,1\}$, questo risultato copre sostanzialmente tutti i possibili scenari, e dunque si può dire con certezza che $X$ e $Y$ sono stocasticamente indipendenti.
___
##### Varianza di variabili aleatorie binomiali e ipergeometriche

Vediamo, in questo paragrafo, come si comporta la **varianza contestualmente a [[CDP_05 - Variabili aleatorie#Variabili aleatorie binomiali|variabili aleatorie binomiali]] e [[CDP_05 - Variabili aleatorie#Variabili aleatorie ipergeometriche|ipergeometriche]]**, partendo prima di tutto dalle binomiali.

Sia $X$ una variabile aleatoria con distribuzione binomiale di parametri $n$ e $\theta$, dunque:
$$X\sim Bin(n,\,\theta)$$
vogliamo sapere il valore della varianza $Var(X)$. Per ottenerla, conviene **vedere $X$ come la somma di $n$ [[CDP_05 - Variabili aleatorie#Variabili aleatorie degeneri e binarie|variabili aleatorie binarie]] indipendenti $X_{1},\,X_{2},\,\dots,\,X_{n}$**: per ogni $i=1,\,2,\,\dots,\,n$, considereremo $X_{i}=1_{A}$, dove i vari eventi $A_{1},\,A_{2},\,\dots,\,A_{n}$ formano uno [[CDP_03 - Correlazione e indipendenza tra eventi#Prove bernoulliane|schema bernoulliano]] (ossia sono tutti eventi indipendenti e aventi probabilità $\theta$ di accadere). Date le premesse, è facile convincersi che ciascuna delle variabili $X_{i}$ ha valore atteso $\mathbb{E}(X_{i})=\theta$ e varianza $Var(X_{i})=\theta \cdot(1-\theta)$, dunque si ottiene che:
$$Var(X)\,=\,Var\left(\sum_{i\,=\,1}^{n}X_{i}\right)\,=\,\sum_{i\,=\,1}^{n}Var(X_{i})\,=\,n\theta\,(1-\theta)$$

Consideriamo, stavolta, una variabile aleatoria $X$ con distribuzione ipergeometrica di parametri $M$, $m_{1}$ e $n$, dunque: 
$$X\sim Hyp(M,\,m_{1},\,n)$$
In questo caso, ci conviene **vedere $X$ coma la somma di $n$ variabili aleatorie binarie $X_{1},\,X_{2},\,\dots,\,X_{n}$ non indipendenti**: per ogni $i=1,\,2,\,\dots,\,n$, considereremo $X_{i}=1_{A_{i}}$, con l'evento $A_{i}=\{\text{all'}i\text{-esima estrazione esce un elemento di tipo }A\}$. Si tratta sostanzialmente di fare $n$ estrazioni senza reinserimento da un'urna che contiene $M$ palline, di cui $m_{1}$ di tipo $A$ e $m_{2}=M-m_{1}$ di tipo $B$. Date le premesse, è facile convincersi che ciascuna delle variabili $X_{i}$ ha valore atteso $\mathbb{E}(X_{i})=\frac{m_{1}}{M}$ e varianza $\frac{m_{1}}{M}\cdot\left( 1-\frac{m_{1}}{M} \right)$, tuttavia la situazione è più complicata di prima per il fatto che le varie variabili $X_{i}$ non sono indipendenti tra loro. Prese a due a due, le variabili $X_{i}$ hanno la stessa covarianza, dunque potremo scrivere che:
$$Var(X)\,=\,\sum_{k\,=\,1}^{n}Var(X_{k})+\sum_{h\,\neq\,k}^{1\,\le\,h,\,k\,\le\,n}Cov(X_{h},\,X_{k})\,=\,n\cdot \frac{m_{1}}{M}\left( 1-\frac{m_{1}}{M} \right)+n(n-1)\,Cov(X_{1},\,X_{2})$$
Ora, essendo $X_{1}$ e $X_{2}$ variabili aleatorie binarie, si ha che:
$$\begin{align} Cov(X_{1},\,X_{2})&=\mathbb{P}(\{X_{1}=1\}\cap\{X_{2}=1\})-\mathbb{P}(\{X_{1}=1\})\cdot\mathbb{P}(\{X_{2}=1\})\\&=\mathbb{P}(\{X_{1}=1\})\cdot\mathbb{P}(\{X_{2}=1\}\,|\,\{X_{1}=1\})-\left( \frac{m_{1}}{M} \right)^{2}\\&=\frac{m_{1}}{M}\cdot \frac{m_{1}-1}{M-1}-\left(\frac{m_{1}}{M}\right)^{2}\\&=\frac{m_{1}}{M}\left( \frac{m_{1}-1}{M-1}-\frac{m_{1}}{M} \right)\\&=-\frac{m_{1}}{M}\left( \frac{M-m_{1}}{M(M-1)} \right)\\&=-\frac{m_{1}}{M}\,\left( 1-\frac{m_{1}}{M} \right)\, \frac{1}{M-1} \end{align}$$
Infine, concludiamo il nostro calcolo inserendo il risultato appena ottenuto nella formula precedentemente trovata per la varianza $Var(X)$:
$$\begin{align} Var(X)&=n\cdot \frac{m_{1}}{M}\left( 1-\frac{m_{1}}{M} \right)+n(n-1)\,Cov(X_{1},\,X_{2}) \\&= n\, \frac{m_{1}}{M}\,\left( 1-\frac{m_{1}}{M} \right)+n(n-1)\left( -\frac{m_{1}}{M} \right)\left( 1-\frac{m_{1}}{M} \right) \frac{1}{M-1}\\&=n\cdot \frac{m_{1}}{M}\cdot \frac{M-m_{1}}{M}\cdot \left( 1- \frac{n-1}{M-1} \right) \end{align}$$
Indicando con $p$ la probabilità $\frac{m_{1}}{M}$, si può scrivere:
$$Var(X)=np(1-p)\left( 1-\frac{n-1}{M-1} \right)$$
___
##### Media aritmetica di variabili aleatorie

Supponiamo di avere $n$ variabili aleatorie $X_{1},\,X_{2},\,\dots,\,X_{n}$, non necessariamente binarie, e per semplicità facciamo le seguenti assunzioni:
- tutte le variabili considerate hanno lo stesso [[CDP_05 - Variabili aleatorie#Valore atteso di una variabile aleatoria|valore atteso]], dunque $\mathbb{E}(X_{i})=\mu$ per $i=1,\,2,\,\dots,\,n$;
- tutte le variabili considerate hanno la stessa [[CDP_05 - Variabili aleatorie#Varianza e covarianza di variabili aleatorie|varianza]], dunque $Var(X_{i})=\sigma^{2}$ per $i=1,\,2,\,\dots,\,n$;
- per ogni coppia di indici $h$ e $k$ diversi tra loro, inclusi nell'intervallo $[1,\,n]$, tutte le coppie di variabili $X_{h}$ e $X_{k}$ hanno la stessa covarianza, dunque $Cov(X_{h},\,X_{k})=\varphi$.

A questo punto, consideriamo una nuova variabile aleatoria $Y_{n}$, rappresentante la **media aritmetica** delle $n$ variabili che abbiamo, ossia:
$$Y_{n}:=\frac{1}{n}\sum_{h\,=\,1}^{n}X_{h}$$
Risulta facile il calcolo del valore atteso e della varianza di tale media aritmetica.

> Date $n$ variabili aleatorie $X_{1},\,X_{2},\,\dots,\,X_{n}$, aventi tutte lo stesso valore atteso, la stessa varianza, e con covarianza costante per ogni coppia di variabili diverse scelte dalle stesse $n$, indicando con $Y_{n}$ la media aritmetica delle variabili $X_{1},\,X_{2},\,\dots,\,X_{n}$ si ha che:
> $$\mathbb{E}(Y_{n})=\mathbb{E}\left( \frac{1}{n} \sum_{h\,=\,1}^{n}X_{h}\right)=\mu$$
> $$Var(Y_{n})=Var\left( \frac{1}{n}\sum_{h\,=\,1}^{n}X_{k} \right)=\frac{1}{n}[\sigma^{2}+(n-1)\varphi]$$
> 

Le formule appena fornite sono facilmente verificabili svolgendo i calcoli. Ad esempio, per la prima:
$$\begin{align} \mathbb{E}(Y_{n})&=\mathbb{E}\left( \frac{1}{n}\sum_{h\,=\,1}^{n}X_{h} \right)\\&=\frac{1}{n}\,\mathbb{E}\left( \sum_{h\,=\,1}^{n}X_{h} \right)\\&=\frac{1}{n}\,\sum_{h\,=\,1}^{n}\mathbb{E}(X_{h})\\&=\frac{1}{n}\,n\mu=\mu \end{align}$$
Mentre, per la seconda:
$$\begin{align} Var(Y_{n})&=Var\left( \frac{1}{n}\sum_{h\,=\,1}^{n}X_{h} \right)\\&=\frac{1}{n^{2}}\,Var\left( \sum_{h\,=\,1}^{n}X_{h} \right)\\&=\frac{1}{n^{2}}\,\left[ \sum_{h\,=\,1}^{n}Var(X_{h})+\sum_{h\,\neq\,k}Cov(X_{h},\,X_{k}) \right]\\&=\frac{1}{n^{2}}\,[n\sigma^{2}+n(n-1)\,\varphi]\\&=\frac{1}{n}\,[\sigma^{2}+(n-1)\varphi] \end{align}$$
___
##### Disuguaglianza di Chebyshev

[pag. 144/147]
___
##### Standardizzazione di una variabile aleatoria

[pag. 147 - 148]
___
##### Disuguaglianza di Cauchy e coefficiente di correlazione

[pag. 148 - 149]
___
##### Covarianza della somma di variabili aleatorie7

[pag. 149 - 150]
___