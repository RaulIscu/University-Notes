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
$$\sum_{k = p}^{\infty} \frac{1}{k^\alpha}$$
A seconda del valore $\alpha$, la serie assume i seguenti valori:
 $$\sum_{k=p}^{+\infty} \frac{1}{k^\alpha} = \begin{cases} +\infty & \mbox{se } \alpha \le 1 \\ < +\infty & \mbox{se } \alpha > 1 \end{cases}$$dove $< +\infty$ indica la convergenza della serie a un determinato valore.
___
## TEOREMI, CONDIZIONI E CRITERI DI CONVERGENZA

#### Serie a termini di segno costante

Sia $a_{k}$ una successione; se ogni termine della successione è positivo, allora la corrispondente serie
$$\sum_{k = p}^{\infty} a_{k}$$
o converge a un valore positivo o diverge a $+\infty$. Invece, se ogni termine della successione è negativo, allora la corrispondente serie o converge a un valore negativo o diverge a $-\infty$.

Una serie a termini di segno costante **non è mai indeterminata**.
___
#### Condizione di convergenza di una serie

Se una serie converge, allora un suo singolo termine deve tendere a 0:
$$\mbox{se } \sum_{k=p}^{\infty}a_{k} \space \mbox{ converge, allora } \lim_{n \to +\infty}a_{n} = 0$$
Ne deriva il seguente corollario, che è quello che risulta più utile per l'analisi di una serie:
$$\mbox{se } \lim_{n \to +\infty}a_{n} \ne 0 \mbox{, allora } \sum_{k=p}^{\infty}a_{k} \mbox{ non converge}$$
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
## SERIE DI POTENZE

#### Cos'è una serie di potenze?

Data una successione $a_{k}$ e un valore $x_{0} \in \mathbb{R}$, si definisce come **serie di potenze di centro $x_{0}$ associata alla successione $a_{k}$** la seguente serie:
$$\sum_{k = 0}^{\infty} a_{k} \cdot (x - x_{0})^k$$
dove la successione $a_{k}$ è detta "**successione dei coefficienti**", mentre il valore $x_{0}$ è detto "**centro della serie**".
___
#### Intervallo di convergenza

Una serie di potenze è a tutti gli effetti una funzione $f(x)$. In particolare, per ogni serie di potenze si può trovare il relativo **intervallo di convergenza**, ossia l'intervallo $X \subseteq \mathbb{R}$ per cui, per ogni $x \in X$, vale che:
$$\sum_{k = p}^{\infty} a_{k} \cdot (x - x_{0})^k = l$$
dove $l$ è un valore finito appartenente ai reali. In altre parole, l'intervallo di convergenza è l'intervallo $X \subseteq \mathbb{R}$ per cui, per ogni $x \in X$, la serie di potenze in questione risulta essere convergente.

Ad esempio, l'intervallo di convergenza della serie geometrica (che è una serie di potenze con $a_{k} = 1$ e $x_{0} = 0$) è $X = (-1, 1)$.

Data una qualsiasi serie di potenze e il suo intervallo di convergenza $X$, si avrà sempre che $x_{0} \in X$; in particolare, il centro della serie $x_{0}$ risulterà essere sempre il centro dell'intervallo di convergenza $X$.

Data una qualsiasi serie di potenze, se la serie converge per un valore $x' \neq x_{0}$, allora la serie converge anche per ogni $x \in \mathbb{R}$ tale che $|x| < |x'|$, o in altre parole per ogni $x \in (-x', x')$.
___
#### Raggio di convergenza

Data la serie di potenze
$$\sum_{k = 0}^{\infty} a_{k} \cdot (x - x_{0})^k$$
definiamo come **raggio di convergenza** $\rho$ della serie l'estremo superiore di tutti i valori $x \ge 0$ per cui la serie di potenze converge.

Il raggio di convergenza $\rho$ di una qualsiasi serie di potenze ha sempre un valore non-negativo, incluso dunque nell'intervallo $[0, +\infty)$. Ricordando che il centro di una serie $x_{0}$ risulta essere anche il centro del suo insieme di convergenza, possiamo affermare che:
- per ogni $x \in \mathbb{R}$ tale per cui $|x - x_{0}| < \rho$, la serie **converge**;
- per ogni $x \in \mathbb{R}$ tale per cui $|x - x_{0}| > \rho$, la serie **non converge**;
- per ogni $x \in \mathbb{R}$ tale per cui $|x - x_{0}| = \rho$, **il comportamento della serie è ignoto**.

Il valore del raggio di convergenza di una serie di potenze è dato da:
$$\rho = \lim_{n \to +\infty} \frac{1}{\left| \frac{a_{n + 1}}{a_{n}} \right|} = \lim_{n \to +\infty} \frac{1}{\sqrt[n]{|a_{n}|}}$$
In forma impropria ma più comoda, possiamo quindi affermare che dato il limite:
$$\lim_{n \to +\infty} \left| \frac{a_{n + 1}}{a_{n}} \right| = \lim_{n \to +\infty} \sqrt[n]{\left| a_{n} \right|} = l$$
si ha che $\rho = \frac{1}{l}$.

Ottenuto il raggio di convergenza di una serie di potenze, il suo intervallo di convergenza sarà $(x_{0} - \rho, x_{0} + \rho)$; per verificare se la serie converga anche per gli estremi dell'intervallo appena ottenuto, si dovranno analizzare le due serie specifiche che si ottengono sostituendo $x = x_{0} - \rho$ e $x = x_{0} + \rho$.
___
#### Derivazione di serie di potenze

Essendo una serie di potenze una funzione di $x$, essa gode della proprietà della derivabilità.

Data una serie di potenze generica
$$f(x) = \sum_{k = p}^{\infty} a_{k} \cdot (x - x_{0})^k$$
avente intervallo di convergenza $X$, la serie è derivabile infinite volte in tale intervallo, e la sua $j$-esima derivata, equivalente a:
$$f^{(j)}(x) = \sum_{k = p + j}^{\infty} k(k - 1)(k - 2)\dots(k - j + 1)a_{k} \cdot (x - x_{0})^{k - j}$$
avrà sempre il medesimo intervallo di convergenza $X$.

Se si vuole calcolare il valore della derivata $j$-esima di una serie di potenze con centro $x_{0}$ proprio nel punto $x_{0}$, esso sarà uguale a:
$$f^{(j)}(x_{0}) = j! \cdot a_{j}$$
___
#### Serie di Taylor


___
#### Espansioni di Taylor notevoli

La serie di Taylor di **$f(x) = e^x$**, avente intervallo di convergenza pari a $\mathbb{R}$, è:
$$e^x = \sum_{k = 0}^{\infty} \frac{x^k}{k!}$$
La serie di Taylor di **$f(x) = \cos x$**, avente intervallo di convergenza pari a $\mathbb{R}$, è:
$$\cos x = \sum_{k = 0}^{\infty} \frac{(-1)^kx^{2k}}{(2k)!}$$
La serie di Taylor di **$f(x) = \sin x$**, avente intervallo di convergenza pari a $\mathbb{R}$, è:
$$\sin x = \sum_{k = 0}^{\infty} \frac{(-1)^kx^{2k + 1}}{(2k + 1)!}$$
La serie di Taylor di **$f(x) = \frac{1}{1 - x}$**, avente intervallo di convergenza pari a $(-1, 1)$, è:
$$\frac{1}{1 - x} = \sum_{k = 0}^{\infty} x^k$$
La serie di Taylor di **$f(x) = \ln(1 + x)$**, avente intervallo di convergenza pari a $(-1, 1)$, è:
$$\ln(1 + x) = \sum_{k = 0}^{\infty} \frac{(-1)^kx^{k + 1}}{k + 1}$$
La serie di Taylor di **$f(x) = \arctan x$**, avente intervallo di convergenza pari a $(-1, 1)$, è:
$$\arctan x = \sum_{k = 0}^{\infty} \frac{(-1)^kx^{2k + 1}}{2k + 1}$$
___