### Cos'è una serie di potenze?

In precedenza si è parlato delle [[Serie#Serie geometriche|serie geometriche]], che in generale assumono la seguente forma:
$$\sum_{k = 0}^{\infty} q^k$$
Volendo rappresentare i singoli termini di questa serie, si noterà subito come essa vada a formare un polinomio di infiniti termini e di "grado infinito":
$$\sum_{k = 0}^{\infty} q^k = 1 + q + q^2 + q^3 + q^4 + \dots$$
Generalizzando, tali polinomi vengono detti "**serie di potenze**":

> Data una successione $a_{k}$ e un valore $x_{0} \in \mathbb{R}$, si definisce come **serie di potenze di centro $x_{0}$ associata alla successione $a_{k}$** la seguente serie:
> $$\sum_{k = 0}^{\infty} a_{k} \cdot (x - x_{0})^k$$
> dove la successione $a_{k}$ è detta "**successione dei coefficienti**", mentre il valore $x_{0}$ è detto "**centro della serie**".

Nel caso della serie geometrica, ad esempio, la successione dei coefficienti è $a_{k} = 1$, mentre il centro della serie è $x_{0} = 0$.
___
### Intervallo di convergenza

Una delle caratteristiche principali delle serie di potenze risulta essere il loro "**intervallo di convergenza**":

> Data una serie di potenze, definiamo come **intervallo di convergenza** della serie l'intervallo $X \subseteq \mathbb{R}$ per cui, per ogni $x \in X$, esiste un valore finito $l \in \mathbb{R}$ tale che:
> $$\sum_{k = 0}^{\infty} a_{k} \cdot (x - x_{0})^k = l$$
> In parole povere, l'intervallo di convergenza di una serie di potenze è **l'intervallo $X \subseteq \mathbb{R}$ per cui tale serie risulta essere convergente**.

Ad esempio, tornando alla serie geometrica, sappiamo che il suo intervallo di convergenza è l'intervallo $(-1, 1)$, in quanto per ogni $x \in (-1, 1)$ la serie geometrica converge al valore $\frac{1}{1 - x}$.

Data una serie di potenze avente come intervallo di convergenza l'insieme $X$, si avrà sempre che $x_{0} \in X$. In particolare, l'insieme $X$ risulta sempre essere un intervallo che ha come centro proprio il centro della serie $x_{0}$.

Le serie di potenze, inoltre, posseggono la seguente proprietà:

> Data la serie di potenze
> $$\sum_{k = 0}^{\infty} a_{k} \cdot (x - x_{0})^k$$
> se la serie converge per un valore $x' \neq x_{0}$, allora la serie converge anche per ogni $x \in \mathbb{R}$ tale che $|x| < |x'|$, o in altre parole, per ogni $x \in (-x', x')$.

[DIMOSTRAZIONE: pag. 33]
___
### Raggio di convergenza

A questo punto, introduciamo il concetto di "**raggio di convergenza**":

> Data la serie di potenze
> $$\sum_{k = 0}^{\infty} a_{k} \cdot (x - x_{0})^k$$
> definiamo come **raggio di convergenza** $\rho$ della serie l'estremo superiore di tutti i valori $x \ge 0$ per cui la serie di potenze converge.

Dalla definizione appena data, segue che $\rho$ debba avere un valore positivo, incluso dunque nell'intervallo $[0, +\infty)$. Inoltre, ricordando che il centro della serie $x_{0}$ risulta sempre essere anche il centro del suo insieme di convergenza, possiamo affermare che:
- per ogni $x \in \mathbb{R}$ tale per cui $|x - x_{0}| < \rho$, la serie **converge**;
- per ogni $x \in \mathbb{R}$ tale per cui $|x - x_{0}| > \rho$, la serie **non converge**;
- per ogni $x \in \mathbb{R}$ tale per cui $|x - x_{0}| = \rho$, **il comportamento della serie è ignoto**.

Tornando alla nostra serie geometrica, sappiamo già che il suo centro sia $x_{0} = 0$, e che il suo intervallo di convergenza sia $[-1, 1]$: si può affermare, perciò, che il suo raggio di convergenza sia $\rho = 1$. In generale, per **calcolare il raggio di convergenza di una serie di potenze**, si utilizza il seguente teorema:

> Data la serie di potenze
> $$\sum_{k = 0}^{\infty} a_{k} \cdot (x - x_{0})^k$$
> il suo raggio di convergenza $\rho$ è dato da:
> $$\rho = \lim_{n \to +\infty} \frac{1}{\left| \frac{a_{n + 1}}{a_{n}} \right|} = \lim_{n \to +\infty} \frac{1}{\sqrt[n]{|a_{n}|}}$$

In forma impropria ma più comoda, possiamo quindi affermare che dato il limite:
$$\lim_{n \to +\infty} \left| \frac{a_{n + 1}}{a_{n}} \right| = \lim_{n \to +\infty} \sqrt[n]{\left| a_{n} \right|} = l$$
si ha che $\rho = \frac{1}{l}$.

Vediamo degli esempi di applicazione di questo teorema. Consideriamo, ad esempio, la seguente serie di potenze:
$$\sum_{k = 0}^{\infty} \frac{(x - 2)^k}{(k + 1)(k + 2)} = \sum_{k = 0}^{\infty} \frac{1}{(k + 1)(k + 2)} (x - 2)^k$$
Procediamo, quindi a calcolare il raggio di convergenza $\rho$:
$$l = \lim_{n \to +\infty} \left| \frac{\frac{1}{(n + 2)(n + 3)}}{\frac{1}{(n + 1)(n + 2)}} \right| = \lim_{n \to +\infty} \left| \frac{(n + 1)(n + 2)}{(n + 2)(n + 3)} \right| = 1$$
Essendo $l = 1$, abbiamo che $\rho = \frac{1}{1} = 1$. Notiamo facilmente che il centro della serie sia $x_{0} = 2$, dunque l'intervallo di convergenza della serie sarà $(2 - \rho, 2 + \rho) = (1, 3)$. Ora, dato che il teorema utilizzato non ci permette di conoscere il comportamento della serie per $x = 1$ e $x = 3$, analizziamo questi casi utilizzando gli altri strumenti che abbiamo a disposizione:
- per $x = 1$, si ha che:
$$\sum_{k = 0}^{\infty} \frac{(1 - 2)^k}{(k + 1)(k + 2)} = \sum_{k = 0}^{\infty} \frac{(-1)^k}{k^2 + 3k + 2}$$
  applicando il [[Teoremi, condizioni e criteri di convergenza#Criterio di Leibniz|criterio di Leibniz]], si trova che la serie ottenuta **converge**;
- per $x = 3$, si ha che:
$$\sum_{k = 0}^{\infty} \frac{(3 - 2)^k}{(k + 1)(k + 2)} = \sum_{k = 0}^{\infty} \frac{1}{k^2 + 3k + 2}$$
  applicando il [[Teoremi, condizioni e criteri di convergenza#Criterio del confronto asintotico|criterio del confronto asintotico]], la serie ottenuta è confrontabile con una serie armonica generalizzata con $\alpha > 1$, e dunque **converge**.

Convergendo la serie sia per $x = 1$ che per $x = 3$, possiamo ampliare il suo intervallo di convergenza a $[1, 3]$. Vediamo ora un altro esempio, con la seguente serie di potenze:
$$\sum_{k = 0}^{\infty} \frac{3^k(2x - 1)^k}{k!} = \sum_{k = 0}^{\infty} \frac{6^k}{k!} \left(x - \frac{1}{2} \right)^k$$
Procediamo, quindi a calcolare il raggio di convergenza $\rho$:
$$l = \lim_{n \to +\infty} \left| \frac{\frac{6^{n + 1}}{(n + 1)!}}{\frac{6^n}{n!}} \right| = \lim_{n \to +\infty} \left| \frac{6^{n + 1}}{(n + 1)!} \cdot \frac{n!}{6^n} \right| = \lim_{n \to +\infty} \left| \frac{6}{(n + 1)!} \cdot n! \right| = \lim_{n \to +\infty} \left| \frac{6}{n + 1} \right| = 0$$
Essendo $l = 0$, abbiamo che $\rho = \frac{1}{0} = +\infty$. Notiamo facilmente che il centro della serie sia $x_{0} = \frac{1}{2}$, dunque l'intervallo di convergenza della serie sarà $\left( \frac{1}{2} - \rho, \frac{1}{2} + \rho \right) = (-\infty, +\infty)$ $= \mathbb{R}$.
___
### Derivazione di serie di potenze

[pag. 36 - 37 - 38]
___
### Serie di Taylor

[pag. 39 - 40 - 41 - 42 - 43]
___
### Espansioni di Taylor (notevoli e non)

[pag. 44]
___