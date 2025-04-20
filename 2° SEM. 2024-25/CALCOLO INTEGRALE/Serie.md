### Dalle successioni alle serie

In matematica, una **successione** è l'insieme ordinato dei valori assunti da una funzione:
$$a: S \rightarrow \mathbb{R}$$
dove $S \subseteq \mathbb{N}$. Si tratta, quindi, di una **funzione $a_{k}$ che associa dei valori ad un sottoinsieme dei numeri naturali**. Formalmente, una successione descritta dalla funzione *a* andrebbe indicata come l'insieme ordinato:
$$(a_k)_{k \in S} = \left \{a(1), a(2), a(3), \mbox{... }, a(n) \right \}$$
Tuttavia, per praticità e semplicità, in questo corso ci si limiterà alla notazione seguente:
$$a_k = a_1, a_2, a_3, \mbox{... }, a_n$$
dove il pedice di ogni valore viene detto "**indice della successione**".

Alcuni esempi di successione sono i seguenti:
- se $a_{k} = 2k$, allora $(a_{k})_{n \in S} = 2, 4, 6, 8, 10, \space \dots, \space 2n$;
- se $a_{k} = 2^k$, allora $(a_{k})_{n \in S} = 2, 4, 8, 16, 32, \space \dots, \space 2^n$;
- se $a_{k} = \frac{1}{k}$, allora $(a_{k})_{n \in S} = 1, \frac{1}{2}, \frac{1}{3}, \frac{1}{4}, \frac{1}{5}, \space \dots, \space \frac{1}{n}$.

Naturalmente, ogni successione dà vita ad una somma dei suoi termini, e viceversa. È possibile, infatti, **considerare ogni termine di una successione come un termine di una sommatoria**; in particolare, indicando con $S_n$ la sommatoria dei primi $n$ termini di una successione, si otterrebbe:
$$S_n = \sum_{k = 1}^{n}a_k = a_1 + a_2 + a_3 + \mbox{... } + a_n$$
Cosa succederebbe, a questo punto, se l'insieme dei termini da sommare fosse illimitato, e quindi se $S = \mathbb{N}$? Ovviamente, si avrebbe un infinito numero di termini per la sommatoria, che possiamo definire utilizzando il **limite** per $n \rightarrow +\infty$ di $S_{n}$; tale limite viene definito "**serie numerica**".

> Data una successione $a_{k}$, si dice **serie numerica** il limite per $n \rightarrow +\infty$ della somma $S_n$:
$$\lim_{n \to +\infty}S_n = \lim_{n \to +\infty}\sum_{k = 1}^{n}a_k = \sum_{k = 1}^{\infty}a_k$$
___
### Serie convergenti e divergenti

Considerando, ad esempio, la somma dettata dal termine $a_{k} = 0$, ossia:
$$S_n = \sum_{k = 1}^{n}0$$
cosa accade a questa somma considerando $n \rightarrow +\infty$, e quindi alla sua serie numerica? In questo caso, risulta evidente che il risultato della somma sarà sempre 0, infatti:
$$\lim_{n \to +\infty}S_n = \lim_{n \to +\infty}\sum_{k = 1}^{n}0 = \sum_{k = 1}^{\infty}0 = 0$$
Vediamo un altro esempio, considerando la somma dettata dal seguente termine $a_{k}$:
$$a_k = \frac{1}{k(k + 1)} = \frac{1}{k} - \frac{1}{k+1}$$
Per piccoli valori di $n$, la serie numerica corrispondente ha il seguente comportamento:
- $S_{1} = a_{1} = 1 - \frac{1}{2}$;
- $S_{2} = a_{1} + a_{2} = \left( 1 - \frac{1}{2} \right) + \left( \frac{1}{2} - \frac{1}{3} \right) = 1 - \frac{1}{3}$;
- $S_{3} = a_{1} + a_{2} + a_{3} = \left( 1 - \frac{1}{2} \right) + \left( \frac{1}{2} - \frac{1}{3} \right) + \left( \frac{1}{3} - \frac{1}{4} \right) = 1 - \frac{1}{4}$.

Possiamo, quindi, affermare che:
$$S_{n} = \sum_{k = 1}^{n}\left( \frac{1}{k} - \frac{1}{k+1} \right) = 1 - \frac{1}{n + 1}$$
Dunque, il limite per $n \rightarrow +\infty$ di questa somma sarà pari a:
$$\lim_{n \to +\infty}S_n = \lim_{n \to +\infty}\sum_{k = 1}^{n}\left( \frac{1}{k} - \frac{1}{k + 1} \right) = \sum_{k = 1}^{\infty}\left( \frac{1}{k} - \frac{1}{k + 1} \right) = 1 - \frac{1}{\infty + 1} = 1$$
In entrambi gli esempi mostrati, per $n \rightarrow +\infty$ le serie **tendono a un valore finito**, e hanno dunque un limite in un determinato valore $l$; una serie del genere viene definita "**serie convergente**".

> Se una serie numerica tende ad un valore $l$, ossia:
> $$\lim_{n \to +\infty}S_{n} = \sum_{k = 1}^{\infty}a_{k} = l$$
> allora tale serie viene detta **serie convergente** in $l$.

Consideriamo, ora, la somma dettata dal termine $a_{k} = 1$, ossia:
$$S_n = \sum_{k = 1}^{n}1$$
Per piccoli valori di $n$, la serie numerica corrispondente ha il seguente comportamento:
- $S_{1} = 1$;
- $S_{2} = 1 + 1 = 2$;
- $S_{3} = 1 + 1 + 1 = 3$.

Possiamo, quindi, affermare che:
$$S_{n} = \sum_{k = 1}^{n}1 = n$$
Dunque, il limite per $n \rightarrow +\infty$ di questa somma sarà pari a:
$$\lim_{n \to +\infty}S_n = \lim_{n \to +\infty}\sum_{k = 1}^{n}1 = \sum_{k = 1}^{\infty}1 = +\infty$$
Vediamo un altro esempio, considerando la somma dettata dal termine $a_{k} = \log{(\frac{1}{k})}$: per piccoli valori di $n$, la serie numerica corrispondente ha il seguente comportamento:
- $S_{1} = \log\left( \frac{1}{1} \right)$;
- $S_{2} = \log\left( \frac{1}{1} \right) + \log\left( \frac{1}{2} \right) = \log\left( \frac{1}{1} \cdot \frac{1}{2} \right) = \log\left( \frac{1}{2} \right)$;
- $S_{3} = \log\left( \frac{1}{1} \right) + \log\left( \frac{1}{2} \right) + \log\left( \frac{1}{3} \right) = \log\left( \frac{1}{1} \cdot \frac{1}{2} \cdot \frac{1}{3} \right) = \log\left( \frac{1}{6} \right)$.

Possiamo, quindi, affermare che:
$$S_{n} = \sum_{k = 1}^{n}\log \left(\frac{1}{k} \right) = \log\left( \frac{1}{n!} \right)$$
Dunque, il limite per $n \rightarrow +\infty$ di questa somma sarà pari a:
$$\lim_{n \to +\infty}S_n = \lim_{n \to +\infty}\sum_{k = 1}^{n}\log\left( \frac{1}{k} \right) = \sum_{k = 1}^{\infty}\log \left( \frac{1}{k} \right) = \log\left( \frac{1}{\infty!} \right) = -\infty$$
In entrambi gli esempi mostrati, per $n \rightarrow +\infty$ le serie **tendono a un valore infinito**; una serie del genere viene definita "**serie divergente**".

> Se una serie numerica tende a $+\infty$ o $-\infty$, ossia:
> $$\lim_{n \to +\infty}S_{n} = \sum_{k = 1}^{\infty}a_{k} = \pm\infty$$
> allora tale serie viene detta **serie divergente**.

Una serie che non converge non è necessariamente divergente, e viceversa una serie che non diverge non è necessariamente convergente. Infatti, **una serie può non convergere e non divergere** contemporaneamente. Ad esempio, la serie derivata dalla successione $a_{k} = (-1)^k$, ossia:
$$S_{n} = \sum_{k = 0}^{n}(-1)^k$$
non è né divergente né convergente. Per piccoli valori di $n$, notiamo che:
- $S_{0} = 1$;
- $S_{1} = 1 - 1 = 0$;
- $S_{2} = 1 - 1 + 1 = 1$;
- $S_{3} = 1 - 1 + 1 - 1 = 0$.

Otteniamo, quindi, che:
$$S_{n} = \begin{cases} 1 & \mbox{se } n \mbox{ è pari} \\ 0 & \mbox{se } n \mbox{ è dispari} \end{cases}$$
Il valore generico $p$ da cui parte la sommatoria ("$k = p$") di una serie **non influenza il carattere della stessa**: che essa valga per $k$ che va da 0 a $+\infty$ o da 10 a $+\infty$, ciò non cambierà il carattere della serie in questione. Inoltre, si può dimostrare che **la somma di due serie convergenti è anch'essa convergente**, mentre **la somma tra una serie convergente e una divergente è anch'essa divergente**.
___
### Serie telescopiche

Le **serie telescopiche** sono un tipo particolare di serie numerica, e risultano essere **convergenti**. Tali serie vengono definite così per via del modo in cui **ogni termine della serie vada ad annullare un termine precedente (interamente o parzialmente)**, portando la serie a "chiudersi" su sé stessa come un telescopio. Generalmente, una serie telescopica è una serie che si presenta o che può essere ricondotta alla seguente forma:
$$\sum_{k = p}^{\infty} a_{k + 1} - a_{k}, \mbox{ oppure } \sum_{k = p}^{\infty} a_{k - 1} - a_{k}, \mbox{ oppure } \sum_{k = p}^{\infty} a_{k} - a_{k - 2} \space \dots$$
Per comprendere meglio questo concetto, analizziamo un esempio:
$$\sum_{k = 2}^{\infty}\left( \frac{1}{k-1} - \frac{1}{k} \right)$$
Espandendo i suoi termini, risulta evidente come essi si cancellino a vicenda (tranne per la prima frazione del primo termine, la seconda frazione di ogni termine viene annullata dalla prima del termine successivo):
$$\begin{align} S_{n} &= \sum_{k=2}^{n}\left( \frac{1}{k-1} - \frac{1}{k} \right) \\ &= \left( \frac{1}{1} - \frac{1}{2} \right) + \left( \frac{1}{2} - \frac{1}{3} \right) + \left( \frac{1}{3} - \frac{1}{4} \right) + \space \dots \space + \left( \frac{1}{n-1} - \frac{1}{n} \right) \\ &= \frac{1}{1} - \frac{1}{2} + \frac{1}{2} - \frac{1}{3} + \frac{1}{3} - \frac{1}{4} + \space \dots \space + \frac{1}{n - 1} - \frac{1}{n} \\ &= 1 - \frac{1}{n} \end{align}$$
La serie in questione, dunque, risulta convergere in $1$, in quanto:
$$\sum_{k=2}^{+\infty} \left( \frac{1}{k - 1} - \frac{1}{k} \right) = \lim_{n \to +\infty}S_{n} = \lim_{n \to +\infty}\left(1 - \frac{1}{n} \right) = 1$$
Vediamo un altro esempio, analizzando la seguente serie:
$$\sum_{k = 3}^{+\infty} \left(\frac{1}{k^2} - \frac{1}{(k - 2)^2}\right)$$
Espandendo i suoi termini, risulta evidente come essi si cancellino a vicenda (tranne per le seconde frazioni dei primi due termini, la prima frazione di un termine viene annullata dalla seconda del termine dopo il successivo):
$$\begin{align} S_{n} &= \sum_{k = 3}^{n}\left( \frac{1}{k^2} - \frac{1}{(k - 2)^2} \right) \\ &= \left( \frac{1}{3^2} - \frac{1}{1^2} \right) + \left( \frac{1}{4^2} - \frac{1}{2^2} \right) + \left( \frac{1}{5^2} - \frac{1}{3^2} \right) + \space \dots \space + \left( \frac{1}{n^2} - \frac{1}{(n - 2)^2} \right) \\ &= - \frac{1}{1^2} - \frac{1}{2^2} + \frac{1}{(n-1)^2} + \frac{1}{n^2} \end{align}$$
La serie in questione, dunque, risulta convergere in $-\frac{5}{4}$, in quanto:
$$\sum_{k=2}^{+\infty} \left( \frac{1}{k^2} - \frac{1}{(k - 2)^2} \right) = \lim_{n \to +\infty}S_{n} = \lim_{n \to +\infty}\left(- \frac{5}{4} + \frac{1}{(n-1)^2} + \frac{1}{n^2} \right) = -\frac{5}{4}$$
___
### Serie geometriche

Le **serie geometriche** sono un altro tipo particolare di serie. Dato $q \in \mathbb{R}$, considerando la successione $(q^k)_{k \in \mathbb{N}^+}$ (definita "progressione geometrica"), le serie che ne derivano vengono definite "**serie geometriche**". La loro analisi risulta interessante, soprattutto poiché il loro comportamento varia al variare della base $q$. In particolare:
- se $q = 1$, allora si ha che
$$\sum_{k=0}^{+\infty}q^k = \lim_{n \to +\infty}\sum_{k=0}^{n}1 = \lim_{n \to +\infty}n + 1 = +\infty$$
- se $q \ne 1$, allora si ha che
$$\begin{align} S_{n} - qS_{n} &= \sum_{k=0}^{n}q^k - q\sum_{k=0}^{n}q^k \\ &= \sum_{k=0}^{n}q^k - \sum_{k=0}^{n}q^{k+1} \\ &= (1 + q + q^2 + \space \dots \space + q^n) - (q + q^2 + q^3 + \space \dots \space + q^n + q^{n + 1}) \\ &= 1 + q^{n + 1} \end{align}$$
  Si nota, infatti, che (tranne per il primo termine della prima parentesi) ogni termine della prima parentesi viene annullato dal termine all'indice precedente della seconda parentesi. Possiamo, quindi, affermare che:
  $$S_{n} - qS_{n} = 1 + q^{n + 1} \Longrightarrow S_{n} = \frac{1 + q^{n + 1}}{1 - q}$$
Unendo questi due casi, otteniamo che:
$$S_{n} = \sum_{k=0}^{n}q^k = \begin{cases} \frac{1 + q^{n + 1}}{1 - q} & \mbox{se } q \ne 1 \\ n + 1 & \mbox{se } q = 1 \end{cases}$$
Per capire come si comporta una serie geometrica per $n \rightarrow +\infty$, bisogna analizzare il comportamento del termine $q^{n + 1}$ nell'unico caso rilevante, ossia quando $q \ne 1$; per fare ciò, calcoliamo il seguente limite:
$$\lim_{n \to +\infty}q^{n + 1} = \begin{cases} +\infty & \mbox{se } q > 1 \\ 0 & \mbox{se } -1 < q < 1 \\ \not\exists & \mbox{se } q \le -1 \end{cases}$$
Unendo i due risultati, si ottiene quindi la seguente definizione generica del risultato di una serie geometrica:

> Data una **serie geometrica**, in base alla variazione di $q$ si avranno i seguenti risultati:
> $$\sum_{k = p}^{\infty}q^k = \begin{cases} +\infty & \mbox{se } q > 1 \\ \frac{q^p}{1 - q} & \mbox{se } -1 < q < 1 \\ \mbox{indeterminata} & \mbox{se } q \le -1 \end{cases}$$
___
### Serie armoniche

Le **serie armoniche** sono un altro tipo particolare di serie, e risultano essere **divergenti**.

> Una serie viene definita **armonica** se assume la seguente forma:
> $$\sum_{k=1}^{+\infty} \frac{1}{k}$$
> Tale tipo di serie risulta essere **divergente**, e in particolare risulta sempre in $+\infty$.

A prima vista, si potrebbe pensare che tale serie sia in qualche modo convergente, dato che, all'aumentare di $k$, verranno sommati termini sempre più vicini allo 0. Si può dimostrare, tuttavia, che tale serie risulta effettivamente in $+\infty$.

[DIMOSTRAZIONE: pag. 11 - 12]

È opportuno, però, precisare che tale serie diverge solo se l'esponente del denominatore (che possiamo definire $\alpha$) è minore o uguale a $1$; infatti, per esponenti maggiori di $1$, si dimostra che la serie armonica converge. Conviene, quindi, ricavare una **forma generalizzata** della serie armonica:

> Una **serie armonica generalizzata** ha i seguenti risultati al variare di $\alpha$:
> $$\sum_{k=1}^{+\infty} \frac{1}{k^\alpha} = \begin{cases} +\infty & \mbox{se } \alpha \le 1 \\ < +\infty & \mbox{se } \alpha > 1 \end{cases}$$
> dove $< +\infty$ indica la convergenza della serie a un determinato valore.

[DIMOSTRAZIONE: pag. 13]
___