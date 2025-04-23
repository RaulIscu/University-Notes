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
> $$\sum_{k = p}^{\infty} a_{k} \cdot (x - x_{0})^k = l$$
> In parole povere, l'intervallo di convergenza di una serie di potenze è **l'intervallo $X \subseteq \mathbb{R}$ per cui tale serie risulta essere convergente**.

Ad esempio, tornando alla serie geometrica, sappiamo che il suo intervallo di convergenza è l'intervallo $(-1, 1)$, in quanto per ogni $x \in (-1, 1)$ la serie geometrica converge al valore $\frac{1}{1 - x}$.

Data una serie di potenze avente come intervallo di convergenza l'insieme $X$, si avrà sempre che $x_{0} \in X$. In particolare, l'insieme $X$ risulta sempre essere un intervallo che ha come centro proprio il centro della serie $x_{0}$.

Le serie di potenze, inoltre, posseggono la seguente proprietà:

> Data la serie di potenze
> $$\sum_{k = p}^{\infty} a_{k} \cdot (x - x_{0})^k$$
> se la serie converge per un valore $x' \neq x_{0}$, allora la serie converge anche per ogni $x \in \mathbb{R}$ tale che $|x| < |x'|$, o in altre parole, per ogni $x \in (-x', x')$.

[DIMOSTRAZIONE: pag. 33]
___
### Raggio di convergenza

A questo punto, introduciamo il concetto di "**raggio di convergenza**":

> Data la serie di potenze
> $$\sum_{k = 0}^{\infty} a_{k} \cdot (x - x_{0})^k$$
> definiamo come **raggio di convergenza** $\rho$ della serie l'estremo superiore di tutti i valori $x \ge 0$ per cui la serie di potenze converge.

Dalla definizione appena data, segue che $\rho$ debba avere un valore non-negativo, incluso dunque nell'intervallo $[0, +\infty)$. Inoltre, ricordando che il centro della serie $x_{0}$ risulta sempre essere anche il centro del suo insieme di convergenza, possiamo affermare che:
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

Consideriamo una serie di potenze generica:
$$f(x) = \sum_{k = 0}^{\infty} a_{k}(x - x_{0})^k = a_{0} + a_{1}(x - x_{0}) + a_{2}(x - x_{0})^2 + \dots$$
Essendo una serie di potenze una funzione a tutti gli effetti, essa gode della proprietà della **derivabilità**: in particolare, se una funzione può essere espressa sotto forma di una somma infinita di termini, ne segue che la derivata di tale funzione possa essere espressa sotto forma di una somma infinita delle derivate di ogni termine originale.

Per derivare tale serie, notiamo che i vari termini della successione dei coefficienti siano delle semplici **costanti moltiplicative**, mentre per derivare i termine $(x - x_{0})^k$ bisognerà applicare la regola di **derivazione delle potenze**. Dunque, per la **derivata di primo ordine $f'(x)$** si ottiene che:
$$\begin{align} f'(x) &= \frac{d}{dx}(a_{0} + a_{1}(x - x_{0}) + a_{2}(x - x_{0})^2 + a_{3}(x - x_{0})^3 + \dots) \\ &= 0 + a_{1} + 2a_{2}(x - x_{0}) + 3a_{3}(x - x_{0})^2 + \dots \\ &= \sum_{k = 1}^{\infty}ka_{k} \cdot (x - x_{0})^{k - 1} \end{align}$$
Seguendo lo stesso procedimento, si può ricavare anche la **derivata di secondo ordine $f''(x)$**:
$$\begin{align} f''(x) = \frac{d}{dx}f'(x) &= \frac{d}{dx}(a_{1} + 2a_{2}(x - x_{0}) + 3a_{3}(x - x_{0})^2 + 4a_{4}(x - x_{0})^3 + \dots) \\ &= 0 + 2a_{2} + 6a_{3}(x - x_{0}) + 12a_{4}(x - x_{0})^2 + \dots \\ &= \sum_{k = 2}^{\infty} k(k - 1)a_{k} \cdot (x - x_{0})^{k - 2} \end{align}$$
A questo punto, è possibile ottenere una generalizzazione della **derivata di ordine $j$ di una serie di potenze**:
$$f^{(j)}(x) = \sum_{k = j}^{\infty} k(k - 1)(k - 2)\dots(k - j + 1)a_{k} \cdot (x - x_{0})^{k - j}$$
Rimane ora da analizzare l'**intervallo di convergenza** di questa derivazione generale di ordine $j$. Per poter fare ciò, effettuiamo un cambio di variabile ponendo $i = k - j$, in modo da poter ricondurre il tutto a una serie di potenze standard:
$$\begin{align} f^{(j)}(x) &= \sum_{k = j}^{\infty} k(k - 1)(k - 2)\dots(k - j + 1)a_{k} \cdot (x - x_{0})^{k - j} \\ &= \sum_{i = 0}^{\infty} (i + j)(i + j - 1)(i + j - 2)\dots(i + 1)a_{i + j} \cdot (x - x_{0})^i \end{align}$$
Notiamo subito che il centro della serie $x_{0}$ rimane invariato rispetto alla serie iniziale; invece, per quanto riguarda il centro di convergenza:
$$l = \lim_{i \to +\infty} \left| \frac{(i + j + 1)(i + j)(i + j - 1)\dots(i + 2)a_{i + j + 1}}{(i + j)(i + j - 1)(i + j - 2)\dots(i + 1)a_{i + j}} \right| = \lim_{i \to +\infty} \left| \frac{a_{i + j + 1}}{a_{i + j}}\right| = \lim_{n \to +\infty} \left| \frac{a_{n + 1}}{a_{n}} \right|$$
Ciò ci fa capire che il calcolo del raggio ci convergenza di una serie di potenze e quello della sua derivata di ordine $j$ sono perfettamente identici, dunque **l'intervallo di convergenza di una serie di potenze e della sua $j$-esima derivata sono equivalenti**. Possiamo formalizzare le informazioni ottenute nel modo seguente:

> Data la serie di potenze
> $$f(x) = \sum_{k = 0}^{\infty} a_{k} \cdot (x - x_{0})^k$$
> avente intervallo di convergenza $X$, la serie è derivabile infinite volte in tale intervallo, e la sua $j$-esima derivata, equivalente a:
> $$f^{(j)}(x) = \sum_{k = j}^{\infty} k(k - 1)(k - 2)\dots(k - j + 1)a_{k} \cdot (x - x_{0})^{k - j}$$
> avrà sempre il medesimo intervallo di convergenza $X$.

Inoltre, se si vuole calcolare il valore della derivata $j$-esima di una serie di potenze con centro $x_{0}$ proprio nel punto $x_{0}$, esso sarà uguale a:
$$f^{(j)}(x_{0}) = j! \cdot a_{j}$$
___
### Serie di Taylor

> Siano $[a, b] \subseteq \mathbb{R}$, $f: [a, b] \rightarrow \mathbb{R}$ una determinata funzione e $x_{0} \in (a, b)$, definiamo "**polinomio di Taylor di ordine $n$ di $x$ centrato in $x_{0}$**", indicato come $T_{n}(x; x_{0})$, il polinomio:
> $$T_{n}(x; x_{0}) = f(x_{0}) + f'(x_{0})(x - x_{0}) + \frac{f''(x_{0})}{2}(x - x_{0})^2 + \frac{f'''(x_{0})}{6}(x - x_{0})^3 + \dots + \frac{f^{(n)}(x_{0})}{n!}(x - x_{0})^k$$
> dove $f^{(n)}$ indica la derivata di ordine $n$ della funzione $f$.

Volendo esprimere questo polinomio in forma contratta, lo si potrebbe fare con la seguente sommatoria:
$$T_{n}(x; x_{0}) = \sum_{k = 0}^{n} \frac{f^{(k)}(x_{0})}{k!}(x - x_{0})^k$$
Il **polinomio di Taylor** risulta fondamentale per lo studio di funzioni più complesse. Infatti, il teorema di Taylor afferma che, al crescere dell'ordine $n$ del polinomio, l'approssimazione tra la funzione $f(x)$ e il polinomio $T_{n}(x; x_{0})$ tende ad essere trascurabile per valori di $x$ molto vicini al centro $x_{0}$. In altre parole, per valori vicini al centro $x_{0}$, **è possibile approssimare una funzione tramite un suo polinomio di Taylor di ordine sufficientemente alto**.

Formalmente, l'enunciato del **teorema di Taylor** è il seguente:

> Siano $[a, b] \subseteq \mathbb{R}$, $f: [a, b] \rightarrow \mathbb{R}$ una determinata funzione e $x_{0} \in (a, b)$, esiste sempre una funzione $R_{n}(x)$ detta "**resto infinitesimale**" per cui si ha che:
> $$f(x) = T_{n}(x; x_{0}) + R_{n}(x; x_{0})$$
> Inoltre, si ha che:
> $$\lim_{x \to x_{0}} \frac{R_{n}(x; x_{0})}{(x - x_{0})^n} = 0$$

Esistono vari modi per rappresentare il resto infinitesimale introdotto dal teorema di Taylor: in questo corso, verrà utilizzato il cosiddetto "**resto di Lagrange**", che assume la seguente forma:
$$R_{n}(x; x_{0}) = \frac{f^{(n + 1)}(\xi)}{(n + 1)!}(x - x_{0})^{n + 1}$$
con $\xi \in (x, x_{0})$.

Per comprendere meglio i concetti appena introdotti, applichiamoli su un esempio, considerando la funzione $f(x) = e^{\sin x}$ e supponendo di volerla approssimare intorno al centro $x_{0} = \pi$. Il polinomio di Taylor di ordine $1$ centrato in $\pi$ è pari a:
$$\begin{align} T_{1}(x; \pi) &= f(\pi) + f'(\pi)(x - \pi) \\ &= e^{\sin \pi} + \cos(\pi) e^{\sin \pi}(x - \pi) \\ &= 1 - (x - \pi) \end{align}$$
Essendo l'ordine scelto relativamente basso, anche l'approssimazione non è molto accurata (infatti, graficamente si nota che essa risulta "corretta" solo per il centro $\pi$). Vediamo, però, cosa succede se si aumenta l'ordine del polinomio, passando all'ordine $2$:
$$\begin{align} T_{2}(x; \pi) &= f(\pi) + f'(\pi)(x - \pi) + \frac{f''(\pi)}{2}(x - \pi)^2 \\ &= e^{\sin \pi} + \cos(\pi)e^{\sin \pi}(x - \pi) + \frac{(\cos^2\pi - \sin \pi)e^{\sin \pi}}{2}(x - \pi)^2 \\ &= 1 - (x - \pi) + \frac{1}{2}(x - \pi)^2 \end{align}$$
Ora l'intorno di approssimazione è aumentato, e aumenterà ogni volta che si aumenterà l'ordine del polinomio di Taylor. Proprio per questo motivo, **se l'ordine del polinomio tende all'infinito**, il resto infinitesimale diventerà insignificante e sostanzialmente **la funzione andrà a coincidere con il suo polinomio di Taylor**.

Notiamo, infatti, che:
$$\begin{align} \lim_{n \to +\infty} f(x) &= \lim_{n \to +\infty} \left(T_{n}(x; x_{0}) + R_{n}(x; x_{0}) \right) \\ &=  \lim_{n \to +\infty} \left( \sum_{k = 0}^{n} \frac{f^{(k)}(x_{0})}{k!}(x - x_{0})^k + \frac{f^{(n + 1)}(\xi)}{(n + 1)!}(x - x_{0})^{n + 1}\right) \\ &= \sum_{k = 0}^{\infty} \frac{f^{(k)}(x_{0})}{k!}(x - x_{0})^k \end{align}$$
Dunque, estendendo l'ordine a $+\infty$, si ottiene che la funzione $f(x)$ coincide esattamente con una serie, la quale viene detta "**serie di Taylor**"; si nota, tra l'altro, che una serie di Taylor non è altro che una **serie di potenze**, e dunque tale convergenza al valore della funzione si verifica solo ed esclusivamente all'interno del raggio di convergenza della serie stessa.

Formalmente:

> Siano $[a, b] \subseteq \mathbb{R}$, $f: [a, b] \rightarrow \mathbb{R}$ una determinata funzione e $x_{0} \in (a, b)$, definiamo come **serie di Taylor di $f$ di centro $x_{0}$** il polinomio di Taylor di ordine $+\infty$ associato alla funzione $f$. 
> 
> In particolare, per ogni $x \in [x_{0} - \rho, x_{0} + \rho]$, dove $\rho$ è il raggio di convergenza di tale serie, si ha che:
> $$f(x) = \sum_{k = 0}^{\infty} \frac{f^{(k)}(x_{0})}{k!}(x - x_{0})^k$$

[ESEMPI: pag. 41 - 42 - 43]
___
### Espansioni di Taylor notevoli

Di seguito, si elencano le **espansioni di Taylor più comuni**, assieme al loro intervallo di convergenza.

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
Conoscere tali espansioni notevoli è utile non solo per analizzare le funzioni ad esse associate, ma anche per semplificare l'analisi di altre **funzioni composte, in parte, da quest'ultime**. Ad esempio, applicando l'espansione notevole di $e^x$, è facile trovare quella di $xe^x$:
$$xe^x = x\sum_{k = 0}^{\infty} \frac{x^k}{k!} = \sum_{k = 0}^{\infty} \frac{x^{k + 1}}{k!}$$
Inoltre, è opportuno ricordare che le serie di Taylor non sono altro che serie di potenze; dunque, se necessario, è possibile sfruttare **cambi di variabile** (a patto che essi siano permessi dall'intervallo di convergenza) per ottenere le **espansioni di funzioni composte**. Ad esempio, ponendo $x^2 = y$:
$$\cos(x^2) = \cos y = \sum_{k = 0}^{\infty} \frac{(-1)^ky^{2k}}{(2k)!} = \sum_{k = 0}^{\infty} \frac{(-1)^k(x^2)^{2k}}{(2k)!} = \sum_{k = 0}^{\infty} \frac{(-1)^kx^{4k}}{(2k)!}$$
___