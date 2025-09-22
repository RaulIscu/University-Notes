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

È opportuno ricordare che si tratta di una semplice **implicazione logica**: dunque, seppur la premessa implichi la conclusione, non è detto che la conclusione implichi la premessa; in altre parole, se la serie converge allora un suo singolo termine tende a 0, ma non è detto che se un singolo termine della serie tende a 0 allora essa converga. Un esempio di ciò è la [[CI_01 - Serie|serie armonica]], che diverge nonostante i suoi termini tendano a 0.

Dal teorema esplicitato in precedenza, deriva il seguente **corollario**:

> Data una successione $(a_{k})_{k \in \mathbb{N}^+}$, si ha che:
> $$\mbox{se } \lim_{n \to +\infty}a_{n} \ne 0 \mbox{, allora } \sum_{k=0}^{\infty}a_{k} \mbox{ non converge}$$

In particolare, se la successione considerata in questo corollario è una successione con termini a segno costante, allora si può affermare direttamente che la serie diverge.
___
### Criterio del confronto diretto

Proviamo ad analizzare una serie più complessa di quelle viste finora, come la seguente:
$$\sum_{k=1}^{+\infty}\sin\left( \frac{1}{k^2} \right)$$
Si nota subito che si tratta di una serie con termini di segno costante (in particolare, positivi), dunque essa dovrà necessariamente convergere o divergere. Si nota, poi, anche che:
$$\lim_{n \to +\infty}\sin\left( \frac{1}{n^2} \right) = 0$$
Venendo meno la condizione di non convergenza, non è possibile escludere questo comportamento, e dunque **non è possibile stabilire con certezza se la serie in questione converga o diverga**. Proviamo un altro approccio, ossia **confrontare** i termini della serie con quelli di un'altra, per cui sia più facile stabilire se essa converga.

Per poter fare ciò, bisogna trovare una funzione con cui effettuare il confronto. Ponendo $\frac{1}{k^2} = x$, proviamo ad esempio a dimostrare che $\forall x \in \mathbb{R}^+$ (per ogni $x$ positiva appartenente ai reali) vale che $\sin x \le x$:
- creiamo la funzione $f(x) = \sin x - x$, e consideriamo la sua derivata $f'(x) = \cos x - 1$;
- per $x \ge 0$, si nota che $f'(x) \le 0$;
- essendo la derivata $f'(x)$ negativa per ogni $x$ positiva, ciò vuol dire che la funzione $f(x)$ sarà decrescente nello stesso intervallo;
- si può assumere, perciò, che per $x \ge 0$ si abbia che $\sin x - x \le 0$, e dunque che $\sin x \le x$, come volevasi dimostrare.

Avendo dimostrato che $\sin x \le x$, possiamo sostituire la $x$ e affermare che $\sin \left( \frac{1}{k^2} \right) \le \frac{1}{k^2}$, e dunque che:
$$0 \le \sum_{k = 1}^{\infty}\sin\left( \frac{1}{k^2} \right) \le \sum_{k = 1}^{\infty} \frac{1}{k^2}$$
Si nota immediatamente che la seconda serie del confronto non è altro che una [[CI_01 - Serie|serie armonica]] con $\alpha > 1$, che risulta perciò essere convergente a un determinato valore finito $l$. Dunque, poiché la serie di partenza è positiva e limitata da una serie convergente, anch'essa **deve necessariamente convergere** a un valore finito.

Generalizzando questo procedimento, possiamo ottenere il seguente teorema che definisce il cosiddetto "**criterio del confronto diretto**":

> Siano $a_{k}$ e $b_{k}$ due successioni, tali che esista un valore $N \in \mathbb{N}$ per cui, $\forall n \ge N$, valga che $0 \le a_{n} \le b_{n}$. Verificato ciò, **se la serie associata a $b_{k}$ converge, allora anche la serie associata a $a_{k}$ converge**:
> $$\mbox{se } \sum_{k=0}^{\infty}b_{k} \mbox{ converge, allora anche } \sum_{k=0}^{\infty}a_{k} \mbox{ converge}$$

Da questo criterio ne deriva il **corollario**, ossia che:

> $$\mbox{se } \sum_{k=0}^{\infty}a_{k} \mbox{ non converge, allora anche } \sum_{k=0}^{\infty}b_{k} \mbox{ non converge}$$
___
### Criterio del confronto asintotico

Vediamo, ora, un altro esempio:
$$\sum_{k = 1}^{\infty}\sin\left( \frac{1}{k} \right)$$
Notiamo facilmente che anche questa è una serie con termini a segno costante (in particolare, positivi), dunque essa dovrà necessariamente convergere o divergere. Analogamente all'esempio del capitolo precedente, si nota anche che:
$$\lim_{n \to +\infty}\sin\left( \frac{1}{n} \right) = 0$$
Non si può, dunque, verificare se la serie risulta essere convergente o divergente. Proviamo, quindi, ad applicare il **criterio del confronto diretto** anche in questo caso: sfruttando la dimostrazione del capitolo precedente, sappiamo che $\sin \frac{1}{k} \le \frac{1}{k}$, e possiamo quindi affermare che:
$$0 \le \sum_{k = 1}^{\infty}\sin \left(\frac{1}{k} \right) \le \sum_{k = 1}^{\infty} \frac{1}{k}$$
La serie usata per il confronto, tuttavia, è la serie armonica con $\alpha = 1$, e in quanto tale risulta essere divergente: questo particolare confronto non ci è quindi di nessun aiuto, così come non lo sarebbe qualsiasi confronto con serie divergenti (l'obiettivo del confronto diretto è proprio dimostrare la convergenza di una serie mostrando che essa è delimitata da un'altra serie convergente).

È possibile applicare un'altra strategia: utilizzando i limiti notevoli, sappiamo che:
$$\lim_{n \to +\infty} \frac{\sin\left( \frac{1}{n} \right)}{\frac{1}{n}} = \lim_{y \to 0} \frac{\sin y}{y} = 1$$
Dunque, per $n \rightarrow +\infty$, si ha che $\sin \left(\frac{1}{n} \right) \sim \frac{1}{n}$ (letto "$\sin\left( \frac{1}{n} \right)$ è simile a $\frac{1}{n}$"), ossia che i due termini si comportano in modo equivalente per $n \rightarrow +\infty$, e quindi lo stesso faranno le serie ad essi associate. Pertanto, sapendo che la serie derivata da $\frac{1}{k}$ diverge positivamente, ne risulta che anche la serie di partenza diverge positivamente.

Generalizzando questo procedimento, possiamo ottenere il seguente teorema che definisce il cosiddetto "**criterio del confronto asintotico**":

> Siano $a_{k}$ e $b_{k}$ due successioni, tali che:
> $$\lim_{n \to +\infty} \frac{a_{n}}{b_{n}} =  l$$
> con $l$ che corrisponde a un numero finito positivo (escluso lo 0), allora si ha che **le serie derivate dalle due successioni hanno lo stesso carattere**. Ciò vuol dire che:
> $$\sum_{k = 0}^{\infty}a_{k} \space \mbox{ converge/diverge} \iff \sum_{k = 0}^{\infty}b_{k} \mbox{ converge/diverge}$$

[DIMOSTRAZIONE: pag. 19 - 20]

Come abbiamo visto, questo enunciato non considera il caso in cui $l = 0$. Tuttavia, questo risultato non è completamente inutile, ma solo meno versatile ai fini del calcolo del carattere della serie $a_{n}$; possiamo affermare, infatti, solo che:

> Siano $a_{k}$ e $b_{k}$ due successioni, tali che:
> $$\lim_{n \to +\infty} \frac{a_{n}}{b_{n}} = 0$$
> allora si ha che se la serie derivata da $b_{n}$ converge, allora anche la serie derivata da $a_{n}$ converge, ossia:
> $$\sum_{k = 0}^{\infty} b_{k} \mbox{ converge } \Longrightarrow \sum_{k = 0}^{\infty} a_{k} \mbox{ converge}$$

Il criterio del confronto asintotico è di fatto uno degli strumenti più utili e comuni per determinare la convergenza o divergenza di una serie, in quanto affidabile e facile da applicare.
___
### Approssimazione di Stirling

A partire dal criterio del confronto asintotico, si è elaborata un'approssimazione molto utile in alcuni casi particolari, chiamata "**approssimazione di Stirling**":

> Per $k \rightarrow +\infty$, possiamo affermare che **$k!$ è simile a $k^k \cdot e^{-k} \cdot \sqrt{2 \pi k}$**, ossia che:
> $$k! \sim k^k e^{-k} \sqrt{2 \pi k} \space \Longrightarrow \lim_{k \to +\infty} \frac{k!}{k^k e^{-k} \sqrt{2 \pi k}} = 1$$

Questa consapevolezza facilita notevolmente l'analisi di alcuni limiti, che sarebbero altrimenti complessi da confrontare. Ad esempio, consideriamo la seguente serie:
$$\sum_{k=0}^{\infty} \frac{k^k}{e^k \cdot k!}$$
È possibile riscrivere il termine del denominatore $k!$ utilizzando l'approssimazione di Stirling, e a quel punto semplificare il tutto fino ad ottenere una serie notevolmente più facile da analizzare e gestire:
$$\sum_{k=0}^{\infty} \frac{k^k}{e^k \cdot k!} \sim \sum_{k=1}^{\infty} \frac{k^k}{e^k \cdot k^k \cdot e^{-k} \cdot \sqrt{2 \pi k}} = \sum_{k=1}^{\infty} \frac{1}{\sqrt{2 \pi} \sqrt{k}} = \frac{1}{\sqrt{2 \pi}} \cdot \sum_{k=1}^{\infty} \left(\frac{1}{\sqrt{k}} \right)$$
La serie ottenuta risulta essere un multiplo di una serie armonica generalizzata con $\alpha < 1$: dunque, così come diverge quest'ultima, diverge anche la serie iniziale.
___
### Criterio del rapporto

> Data una successione $a_{k}$ a termini positivi, tale per cui:
> $$\lim_{n \to +\infty} \frac{a_{n + 1}}{a_{n}} = l$$
> con $0 \le l < +\infty$, possiamo affermare che:
> - se $l < 1$, allora la serie associata alla successione $a_{k}$ **converge**;
> - se $l > 1$, allora la serie associata alla successione $a_{k}$ **diverge**.
> 
> Invece, se $l = 1$, non si possono trarre conclusioni.

[DIMOSTRAZIONE: pag. 21 - 22]

Per comprendere meglio il funzionamento del **criterio del rapporto**, analizziamo degli esempi. Consideriamo la seguente serie:
$$\sum_{k = 0}^{\infty} \frac{k^3}{2^k}$$
Applicando il criterio, si ottiene:
$$\lim_{n \to +\infty} \frac{\frac{(n + 1)^3}{2^{n + 1}}}{\frac{n^3}{2^n}} = \lim_{n \to +\infty} \left( \frac{(n + 1)^3}{2^{n + 1}} \cdot \frac{2^n}{n^3} \right) = \lim_{n \to +\infty} \left( \frac{(n + 1)^3}{2} \cdot \frac{1}{n^3} \right) = \frac{1}{2}$$
In questo caso, si ha che $l = \frac{1}{2}$, e dato che $l < 1$ possiamo affermare che la serie converge. Vediamo, ora, un altro esempio con la seguente serie:
$$\sum_{k = 0}^{\infty} \frac{k!}{2^k}$$
Applicando il criterio, si ottiene:
$$\lim_{n \to +\infty} \frac{\frac{(n + 1)!}{2^{n + 1}}}{\frac{n!}{2^n}} = \lim_{n \to +\infty} \left( \frac{(n + 1)!}{2^{n + 1}} \cdot \frac{2^n}{n!} \right) = \lim_{n \to +\infty} \left( \frac{(n + 1)!}{2} \cdot \frac{1}{n!} \right) = \lim_{n \to +\infty} \frac{n + 1}{2} = +\infty$$
In questo caso, si ha che $l = +\infty$, e dato che $l > 1$ possiamo affermare che la serie diverge.
___
### Criterio della radice

> Data una successione $a_{k}$ a termini positivi, tale per cui:
> $$\lim_{n \to +\infty} \sqrt[n]{a_{n}} = l$$
> con $0 \le l < +\infty$, possiamo affermare che:
> - se $l < 1$, allora la serie associata alla successione $a_{k}$ **converge**;
> - se $l > 1$, allora la serie associata alla successione $a_{k}$ **diverge**.
> 
> Invece, se $l = 1$, non si possono trarre conclusioni.

[DIMOSTRAZIONE: pag. 24 - 25]

Il criterio del rapporto e il criterio della radice risultano essere effettivamente molto simili, e spesso il limite calcolato tramite l'uno o l'altro criterio coincide. Pertanto, **la scelta tra l'uno o l'altro ricade sulla preferenza personale e sulla serie particolare** che si sta cercando di analizzare. Considerando, ad esempio, la seguente serie che abbiamo analizzato già in precedenza:
$$\sum_{k = 0}^{\infty} \frac{k!}{2^k}$$
Per questo esempio, il criterio del rapporto risulta ottimale, mentre il criterio della radice potrebbe essere più complesso da applicare.
___
### Criterio di Leibniz

I criteri di convergenza finora mostrati lavoravano su serie con termini a segno costante. Non abbiamo, però, ancora modo di determinare con certezza la convergenza o divergenza di una **serie con termini a segno alterno**, che tendenzialmente sono serie in cui un termine è costituito (in parte o totalmente) da:
$$(-1)^k$$
Per analizzare questo tipo di serie, si utilizza il "**criterio di Leibniz**":

> Sia $a_{k}$ una successione a segno alterno, ossia $a_{k} = (-1)^k \cdot b_{k}$. Se si verificano i seguenti tre requisiti:
> - $b_{k}$ è una successione di termini di **segno non negativo**;
> - $\forall k \in \mathbb{N}^+$ si ha che $b_{k + 1} \le b_{k}$, ossia **$b_{k}$ è una successione decrescente**;
> - **$\lim_{n \to +\infty} b_{n} = 0$**;
>
> allora la serie $\sum_{k = 0}^{\infty} a_{k}$ **converge**.

[DIMOSTRAZIONE: pag. 26 - 27]

Vediamo un esempio di applicazione del criterio di Leibniz, analizzando la seguente serie:
$$\sum_{k=1}^{\infty} \frac{(-1)^k}{k}$$
Si nota immediatamente che si tratta di una serie con termini di segno alterno, data la presenza di $(-1)^k$: procediamo, dunque, a verificare che rispetti le tre condizioni necessarie per applicare il criterio di Leibniz:
- $b_{k} = \frac{1}{k}$ è una successione di termini di segno positivo, dunque non negativo;
- $b_{k + 1} \le b_{k} \Longrightarrow \frac{1}{k + 1} \le \frac{1}{k}$ è vero per ogni $k$, quindi $b_{k}$ risulta essere una successione decrescente;
- per $n \rightarrow +\infty$, $b_{n} \rightarrow 0$.

Essendo soddisfatte tutte e tre le condizioni, possiamo affermare che la serie in questione converge.
___
### Criterio di convergenza assoluta

Nonostante il criterio di Leibniz venga applicato su serie a segno alterno, per poter essere utilizzato **è necessario che l'alternanza tra i segni sia regolare**, e che quindi il segno ad ogni termine (positivo, negativo, positivo, negativo, ecc. ecc.). Possono però esserci casi in cui quest'alternanza non sia regolare. Ad esempio, la seguente serie:
$$\sum_{k = 1}^{\infty} \frac{\sin k}{k^2}$$
presenta termini positivi per $0 \le k \le \pi$ e negativi per $\pi \le k \le 2\pi$. Dunque, in questo caso non è possibile applicare il criterio di Leibniz. In questi casi, si deve ricorrere al cosiddetto "**criterio di convergenza assoluta**":

> Data una successione $a_{k}$, si può affermare che:
> $$\sum_{k = 0}^{\infty} |a_{k}| \mbox{ converge } \Longrightarrow \space \sum_{k = 0}^{\infty}a_{k} \mbox{ converge}$$
> In tal caso, si dice che la serie **converge assolutamente**.

[DIMOSTRAZIONE: pag. 28 - 29]

Applichiamo il criterio di convergenza assoluta sulla serie mostrata precedentemente. Si ha che:
$$\sum_{k = 1}^{\infty} \left | \frac{\sin k}{k^2} \right | = \sum_{k = 1}^{\infty} \frac{\left |\sin k \right|}{k^2}$$
A questo punto, applichiamo il criterio del confronto diretto, dimostrando che la serie è limitata da una serie armonica generalizzata con $\alpha > 1$:
$$0 \le \sum_{k = 1}^{\infty} \frac{\left | \sin k \right |}{k^2} \le \sum_{k = 1}^{\infty} \frac{1}{k^2}$$
Essendo vera questa disuguaglianza, possiamo affermare che la serie $\sum_{k=1}^{\infty} \frac{\left | \sin k \right |}{k^2}$ converge, pertanto la serie iniziale converge assolutamente (e quindi anche normalmente).