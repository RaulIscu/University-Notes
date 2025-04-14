### Serie a termini di segno costante

> Sia $(a_{k})_{k \in \mathbb{N}^+}$ una successione. Se $\forall k \in \mathbb{N}^+$ si ha che $a_{k} \ge 0$, ossia che ogni termine della successione è positivo, allora la corrispondente serie
> $$\sum_{k=0}^{+\infty}a_{k}$$
> converge a un valore non-negativo o diverge a $+\infty$.

> Sia $(b_{k})_{k \in \mathbb{N}^+}$ una successione. Se $\forall k \in \mathbb{N}^+$ si ha che $b_{k} \le 0$, ossia che ogni termine della successione è negativo, allora la corrispondente serie
> $$\sum_{k=0}^{+\infty}b_{k}$$
> converge a un valore non-positivo o diverge a $-\infty$.

Vediamo alcuni esempi di applicazione di questi enunciati. Ad esempio, si nota subito che la seguente serie:
$$\sum_{k=0}^{+\infty} \frac{1}{k}$$
è composta interamente da termini positivi ($1, \frac{1}{2}, \frac{1}{3},$ ecc. ecc.), e dunque si può affermare che essa o converge a un valore non-negativo o diverge a $+\infty$. Vediamo un altro esempio:
$$\sum_{k=0}^{+\infty}\sin\left( \frac{1}{k} \right)$$
Essendo l'argomento $\frac{1}{k}$ di segno costante, anche il seno risulterà avere segno costante positivo: dunque, si possono affermare le stesse caratteristiche dell'esempio precedente. Infine, la seguente serie:
$$\sum_{k=0}^{+\infty}\sin k$$
non ha termini di segno costante, dunque non si può affermare con certezza che essa converga o diverga in un determinato modo.
___
### Condizione per la convergenza di una serie

Data una serie generica $a_{k}$, supponiamo che essa converga ad un valore $l \in \mathbb{R}$:
$$\sum_{k=0}^{\infty}a_{k} = \lim_{n \to +\infty}S_{n} = l$$
Banalmente, è possibile affermare che, se il limite per $n \rightarrow +\infty$ di $S_{n}$ è uguale a un valore finito, lo sarà anche lo stesso limite di $S_{n - 1}$. Di conseguenza, otteniamo che:
$$a_{n} = S_{n} - S_{n - 1} \Longrightarrow \lim_{n \to +\infty}a_{n} = \lim_{n \to +\infty}(S_{n} - S_{n - 1}) \Longrightarrow \lim_{n \to +\infty}a_{n} = l - l = 0$$
Dunque, **se una serie converge, allora un suo singolo termine deve tendere a 0**.

> Data una successione $(a_{k})_{k \in \mathbb{N}^+}$, si ha che:
> $$\mbox{se } \sum_{k=0}^{\infty}a_{k} \space \mbox{ converge, allora } \lim_{n \to +\infty}a_{n} = 0$$

È opportuno ricordare che si tratta di una semplice **implicazione logica**: dunque, seppur la premessa implichi la conclusione, non è detto che la conclusione implichi la premessa; in altre parole, se la serie converge allora un suo singolo termine tende a 0, ma non è detto che se un singolo termine della serie tende a 0 allora essa converga. Un esempio di ciò è la [[Serie|serie armonica]], che diverge nonostante i suoi termini tendano a 0.

Dal teorema esplicitato in precedenza, deriva il seguente **corollario**:

> Data una successione $(a_{k})_{k \in \mathbb{N}^+}$, si ha che:
> $$\mbox{se } \lim_{n \to +\infty}a_{n} \ne 0 \mbox{, allora } \sum_{k=0}^{\infty}a_{k} \mbox{ non converge}$$

In particolare, se la successione considerata in questo corollario è una successione con termini a segno costante, allora si può affermare direttamente che la serie diverge.
___
### Criterio del confronto diretto

[pag. 17]
___
### Criterio del confronto asintotico


___
### Criterio del rapporto


___
### Criterio della radice


___
### Criterio di Leibniz


___
### Criterio di convergenza assoluta