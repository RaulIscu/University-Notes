## SERIE

#### Cos'è una serie?

Data una successione (funzione con dominio pari a un sottoinsieme dei numeri naturali $\mathbb{N}$) $a_{k}$, si possono considerare i suoi termini come termini di una sommatoria $S_{n}$:
$$\sum_{k = 0}^{n}a_{k}$$
La "**serie numerica**" associata alla successione $a_{k}$ consiste nel limite per $n \rightarrow +\infty$ di $S_{n}$ (ossia considerando i termini della successione generati da tutti i numeri naturali). La serie associata a $a_{k}$ è dunque:
$$\lim_{n \to +\infty} S_{n} = \sum_{k = 0}^{\infty} a_{k}$$
___
#### Serie convergenti e divergenti

Una serie è detta "**convergente**" se tende ad un valore finito $l$; invece, una serie è detta "**divergente**" se tende a $+\infty$ o a $-\infty$.

Se una serie non è convergente, non è detto che essa sia automaticamente divergente, e viceversa. Infatti, una serie può non essere né divergente né convergente.

La convergenza o divergenza di una serie viene detto il suo "**carattere**". Esso non varia al variare del valore $p$ da cui parte $k$ all'interno della sommatoria.

La somma tra due serie convergenti è anch'essa una serie convergente; invece, la somma tra una serie convergente e una divergente risulta essere divergente.
___
#### Serie telescopiche

Una **serie telescopica** è una serie **convergente**, che si riconosce perché i suoi termini tendono ad "annullarsi" l'un l'altro. Essa può presentarsi sotto due forme:
$$\sum_{k = p}^{\infty} a_{k + m} - a_{k}, \mbox{ oppure } \sum_{k = p}^{\infty} a_{k} - a_{k + m}$$
Data una serie telescopica della forma
$$\sum_{k = p}^{\infty} a_{k + m} - a_{k}$$
essa converge al valore $l$, con $l$ pari a:
$$l = - a_{p} - a_{p + 1} - \dots - a_{p + m - 1} + \lim_{n \to +\infty} \left(a_{n + 1} + a_{n + 2} + \dots + a_{n + m} \right)$$
Invece, data una serie telescopica della forma
$$\sum_{k = p}^{\infty} a_{k} - a_{k + m}$$
essa converge al valore $l$, con $l$ pari a:
$$l = a_{p} + a_{p + 1} + \dots + a_{p + m - 1} - \lim_{n \to +\infty} \left(a_{n + 1} + a_{n + 2} + \dots + a_{n + m} \right)$$
___
#### Serie geometriche

Una **serie geometrica** è una serie del seguente tipo:
$$\sum_{k = p}^{\infty} q^k$$
con $q \in \mathbb{R}$. A seconda del valore di $q$, queste serie assumono i seguenti valori:
$$\sum_{k = p}^{\infty}q^k = \begin{cases} +\infty & \mbox{se } q \ge 1 \\ \frac{q^p}{1 - q} & \mbox{se } -1 < q < 1 \\ \mbox{indeterminata} & \mbox{se } q \le -1 \end{cases}$$
___
#### Serie armoniche

Una **serie armonica** è una serie del seguente tipo:
$$\sum_{k = 1}^{\infty} \frac{1}{k^\alpha}$$
A seconda del valore $\alpha$, la serie assume i seguenti valori:
 $$\sum_{k=1}^{+\infty} \frac{1}{k^\alpha} = \begin{cases} +\infty & \mbox{se } \alpha \le 1 \\ < +\infty & \mbox{se } \alpha > 1 \end{cases}$$dove $< +\infty$ indica la convergenza della serie a un determinato valore.
___
## TEOREMI, CONDIZIONI E CRITERI DI CONVERGENZA

#### Serie a termini di segno costante

Sia $a_{k}$ una successione; se ogni termine della successione è positivo, allora la corrispondente serie
$$\sum_{k = 0}^{\infty} a_{k}$$
o converge a un valore positivo o diverge a $+\infty$. Invece, se ogni termine della successione è negativo, allora la corrispondente serie o converge a un valore negativo o diverge a $-\infty$.

Una serie a termini di segno costante **non è mai indeterminata**.
___
#### Condizione di convergenza di una serie

Se una serie converge, allora un suo singolo termine deve tendere a 0:
$$\mbox{se } \sum_{k=0}^{\infty}a_{k} \space \mbox{ converge, allora } \lim_{n \to +\infty}a_{n} = 0$$
Ne deriva il seguente corollario, che è quello che risulta più utile per l'analisi di una serie:
$$\mbox{se } \lim_{n \to +\infty}a_{n} \ne 0 \mbox{, allora } \sum_{k=0}^{\infty}a_{k} \mbox{ non converge}$$
___
#### Criterio del confronto diretto

Siano $a_{k}$ è $b_{k}$ due successioni, tali che esista un valore $N \in \mathbb{N}$ per cui, $\forall n \ge N$, valga che $0 \le a_{n} \le b_{n}$. Verificato ciò, **se la serie associata a $b_{k}$ converge, allora anche la serie associata a $a_{k}$ converge**:
$$\mbox{se } \sum_{k=0}^{\infty}b_{k} \mbox{ converge, allora anche } \sum_{k=0}^{\infty}a_{k} \mbox{ converge}$$
Dunque:
$$\mbox{se } \sum_{k=0}^{\infty}a_{k} \mbox{ non converge, allora anche } \sum_{k=0}^{\infty}b_{k} \mbox{ non converge}$$
___
#### Criterio del confronto asintotico

Siano $a_{k}$ e $b_{k}$ due successioni, tali per cui:
$$\lim_{n \to +\infty} \frac{a_{n}}{b_{n}} = l$$
con $l$ che corrisponde a un valore finito positivo (escluso lo 0), allora si ha che le serie derivate dalle due successioni hanno lo stesso carattere. Quindi:
$$\sum_{k = 0}^{\infty}a_{k} \space \mbox{ converge/diverge} \iff \sum_{k = 0}^{\infty}b_{k} \mbox{ converge/diverge}$$
Invece, se si ha che $l = 0$, allora si può affermare solo che:
$$\sum_{k = 0}^{\infty} b_{k} \mbox{ converge } \Longrightarrow \sum_{k = 0}^{\infty} a_{k} \mbox{ converge}$$
___

#### Approssimazione di Stirling

Per $k \rightarrow +\infty$, si può affermare che:
$$k! \sim k^k \cdot e^{-k} \cdot \sqrt{2 \pi k}$$
___
#### Criterio del rapporto

Data una successione a termini positivi $a_{k}$, tale per cui:
$$\lim_{n \to +\infty} \frac{a_{n + 1}}{a_{n}} = l$$
con $0 \le l < +\infty$, possiamo affermare che:
- se $l < 1$, allora la serie associata alla successione $a_{k}$ **converge**;
- se $l > 1$, allora la serie associata alla successione $a_{k}$ **diverge**;
- se $l = 1$, non si possono trarre conclusioni.

Tendenzialmente, il criterio del rapporto risulta utile quando nella serie compaiono **fattoriali**.
___
#### Criterio della radice

Data una successione a termini positivi $a_{k}$, tale per cui:
$$\lim_{n \to +\infty} \sqrt[n]{a_{n}} = l$$
con $0 \le l < +\infty$, possiamo affermare che:
- se $l < 1$, allora la serie associata alla successione $a_{k}$ **converge**;
- se $l > 1$, allora la serie associata alla successione $a_{k}$ **diverge**;
- se $l = 1$, non si possono trarre conclusioni.

Tendenzialmente, il criterio della radice risulta utile quando nella serie compaiono **potenze di $n$**.
___
#### Criterio di Leibniz

Sia $a_{k}$ una successione a segno alterno, ossia $a_{k} = (-1)^k \cdot b_{k}$. Se si verificano i seguenti tre requisiti:
- $b_{k}$ è una successione di termini di **segno non negativo**;
- $\forall k \in \mathbb{N}^+$ si ha che $b_{k + 1} \le b_{k}$, ossia **$b_{k}$ è una successione decrescente**;
- **$\lim_{n \to +\infty} b_{n} = 0$**;

allora la serie $\sum_{k = 0}^{\infty} a_{k}$ **converge**.
___
#### Criterio di convergenza assoluta

Data una successione $a_{k}$:
$$\sum_{k = 0}^{\infty} |a_{k}| \mbox{ converge } \Longrightarrow \space \sum_{k = 0}^{\infty}a_{k} \mbox{ converge}$$
In tal caso, si dice che la serie converge assolutamente.
___
## GUIDA PER ESERCIZI DI ANALISI DI UNA SERIE

Se si deve ricavare il **carattere di una serie** (convergente, divergente, ecc. ecc.):
1. verificare che si tratti di una serie telescopica, geometrica o armonica;
	1. se la serie è **telescopica**, allora sarà convergente;
	2. se la serie è **geometrica**, ricavare il risultato in base al valore di $q$;
	3. se la serie è **armonica**, ricavare il risultato in base al valore di $\alpha$;
2. se non rientra in nessuna delle tre categorie precedenti, verificare che si tratti di una **serie con termini a segno costante**;
	4. applicare **il corollario della condizione di convergenza** di una serie;
	5. se il passaggio precedente non porta ulteriori conclusioni, applicare il criterio del **confronto diretto** o del **confronto asintotico**;
	6. se il passaggio precedente non porta ulteriori conclusioni, applicare il criterio del **rapporto** o della **radice**;
3. se non rientra nella categoria precedente, verificare che si tratti di una **serie con termini a segno alterno** ($a_{k} = (-1)^k \cdot b_{k}$);
	1. applicare il **criterio di Leibniz**;
4. se non rientra nella categoria precedente, applicare il **criterio di convergenza assoluta** e ricondursi a uno dei criteri precedenti.