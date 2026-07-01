## Legge dei Grandi Numeri

In questo paragrafo, andiamo a riprendere il discorso iniziato parlando della **[[CDP_05 - Variabili aleatorie#Disuguaglianza di Chebyshev|disuguaglianza di Chebyshev]]**, e in particolare della sua applicazione sulla **media aritmetica $Y_{n}$ di $n$ variabili aleatorie incorrelate, con stesso [[CDP_05 - Variabili aleatorie#Valore atteso di una variabile aleatoria|valore atteso]] $\mu$ e stessa [[CDP_05 - Variabili aleatorie#Varianza e covarianza di variabili aleatorie|varianza]] $\sigma^{2}$**.

Innanzitutto, trattando ora con variabili aleatorie anche non a valori finiti, va specificato che **la disuguaglianza di Chebyshev vale anche per variabili aleatorie generali, a patto che abbiano valore atteso e varianza finiti**. Avendo stabilito ciò, riproponiamo per chiarezza la formulazione della disuguaglianza di Chebyshev:
$$\mathbb{P}(\{|X-\mu|>\epsilon\})\le \frac{\sigma^{2}}{\epsilon^{2}}$$
Con le stesse precauzioni, dunque che esistano e siano finiti il valore atteso $\mathbb{E}(X_{i})=\mu$ e la varianza $Var(X_{i})=\sigma^{2}$, possiamo dire la stessa cosa anche dell'applicazione della disuguaglianza sulla media aritmetica $Y_{n}$ di $n$ variabili aleatorie indipendenti $X_{1},\,X_{2},\,\dots,\,X_{n}$. Dunque, vale che:
$$\mathbb{P}(\{|Y_{n}-\mu|>\epsilon\})\le \frac{\sigma^{2}}{n\,\epsilon^{2}}$$
Cosa succederebbe, a questo punto, se considerassimo un numero $n$ molto grande, e dunque un numero molto grande di variabili aleatorie $X_{i}$? In parole povere, **all'aumentare di $n$, la probabilità che media aritmetica $Y_{n}$ e valore atteso $\mu$ differiscano diminuisce sempre di più**. Si può comprendere meglio questo concetto pensando a uno studente universitario che, col passare del tempo, fa sempre più esami: all'inizio, quando gli esami fatti saranno ancora pochi, ogni voto avrà un impatto notevole sulla media totale, ma all'aumentare degli esami la media diventerà sempre meno variabile, e un voto che si discosta dalla stessa non la impatterà più di tanto. Lo stesso, più o meno, vale per la media $Y_{n}$ e per le variabili $X_{i}$. In particolare, se consideriamo un numero $n$ tendente all'infinito, otteniamo la formulazione della "**Legge Debole dei Grandi Numeri**".

> Sia $\{X_{i},\,i\ge 1\}$ un insieme di variabili aleatorie indipendenti a due a due e identicamente distribuite, per le quali esistono e sono finiti valore atteso $\mathbb{E}(X_{i})=\mu$ e varianza $Var(X_{i})=\sigma^{2}$. Considerando la media aritmetica $Y_{n}=\frac{\sum_{i\,=\,1}^{n}X_{i}}{n}$, per ogni $\epsilon>0$ si ha che:
> $$\lim_{n\,\to\,\infty}\mathbb{P}(\{|Y_{n}-\mu|>\epsilon\})=0$$

La dimostrazione di questa equivalenza è pressoché banale, basta osservare che, per la disuguaglianza di Chebyshev, si ha:
$$0\,\le\,\mathbb{P}(\{|Y_{n}-\mu|>\epsilon\})\,\le\, \frac{\sigma^{2}}{n\,\epsilon^{2}}$$
e che, facendo tendere $n$ all'infinito in questa catena di disuguaglianze, otteniamo:
$$0\,\le\,\lim_{n\,\to\,\infty} \mathbb{P}(\{|Y_{n}-\mu|>\epsilon\})\,\le\,\lim_{n\,\to\,\infty} \frac{\sigma^{2}}{n\,\epsilon^{2}}$$
Possiamo facilmente calcolare il limite a destra, che risulterà in $0$, e dunque per il teorema del confronto abbiamo trovato che il membro centrale della disuguaglianza mostrata è anch'esso pari a $0$.

Per confermare la validità di questa legge, va fatta un'ulteriore precisazione: la possibilità di scegliere un numero $n$ molto grande, presuppone di avere uno spazio di probabilità sufficientemente grande, e nel caso della Legge Debole dei Grandi Numeri **tale spazio di probabilità dovrà essere infinito**.
___
## Teorema Centrale del Limite

Come abbiamo già detto in precedenza, la [[CDP_05 - Variabili aleatorie#Disuguaglianza di Chebyshev|disuguaglianza di Chebyshev]] permette di trovare delle limitazioni inferiori alle probabilità del tipo:
$$\mathbb{P}\left( \left\{\left| \frac{S_{n}}{n}-\mu\right|\le \epsilon \right\} \right)$$
Tuttavia, se si conoscesse la **funzione di distribuzione $F_{S_{n}}(x)$** della variabile aleatoria $S_{n}$, ossia la probabilità $\mathbb{P}(S_{n}\le x)$, tale probabilità si potrebbe calcolare in modo esatto, infatti:
$$\begin{align} \mathbb{P}\left( \left\{ \left| \frac{S_{n}}{n}-\mu \right| \le \epsilon \right\} \right) &=\mathbb{P}(n(\mu-\epsilon)\le S_{n}\le n(\mu+\epsilon))\\&= F_{S_{n}}(n(\mu+\epsilon)) -F_{S_{n}}(n(\mu-\epsilon)^{-})\\&=F_{S_{n}}(n(\mu+\epsilon))-F_{S_{n}}(n(\mu-\epsilon))+\mathbb{P}(\{S_{n}=n(\mu-\epsilon)\}) \end{align}$$
Naturalmente, però, trovare la distribuzione di somme $S_{n}$ con $n$ abbastanza alti diventa molto difficile, se non impossibile; dovremo quindi passare per vie alternative. Innanzitutto, osserviamo che calcolare **la funzione di distribuzione $F_{S_{n}}(x)$ equivale a calcolare la distribuzione di una trasformata di $S_{n}$**: infatti, dati due numeri reali $a_{n}$ e $b_{n}$, con $b_{n}>0$, possiamo affermare che:
$$\{S_{n}\le x\}=\left\{ \frac{S_{n}-a_{n}}{b_{n}}\le \frac{x-a_{n}}{b_{n}} \right\}$$
Ora, per quanto riguarda la scelta di $a_{n}$ e $b_{n}$, una scelta naturale che permette una notevole semplificazione è $a_{n}=\mathbb{E}(S_{n})$ e $b_{n}=\sqrt{Var(S_{n})}$, che portano alla **[[CDP_05 - Variabili aleatorie#Standardizzazione di una variabile aleatoria|standardizzazione]] della variabile aleatoria $S_{n}$**. In questo modo, per la disuguaglianza di Chebyshev, sappiamo che qualunque siano $n$ e $\alpha>0$ si ottiene:
$$\mathbb{P}\left( -\alpha\le \frac{S_{n}-\mathbb{E}(S_{n})}{\sqrt{Var(S_{n})}}\le\alpha \right)\ge 1 - \frac{1}{\alpha^{2}}$$
In particolare, è possibile dimostrare il seguente risultato:

> Considerando $n$ variabili aleatorie $X_{i}$, tutte indipendenti e con la stessa distribuzione, che ammettono dunque uno stesso valore atteso $\mu$ e una stessa varianza $\sigma^{2}$, e siano $\mu$ e $\sigma^{2}$ finiti (in particolare, $\sigma^{2}$ dovrà anche essere non nulla), allora sappiamo che $\mathbb{E}(S_{n})=n\mu$, e che $Var(S_{n})=n\sigma^{2}$, dunque:
> $$F_{S_{n}}(x)=\mathbb{P}(S_{n}\le x)=\mathbb{P}\left( \frac{S_{n}-n\mu}{\sqrt{n\sigma^{2}}}\le \frac{x-n\mu}{\sqrt{n\sigma^{2}}} \right)\simeq\Phi\left( \frac{x-n\mu}{\sqrt{n\sigma^{2}}} \right)$$
> dove $\Phi(x)$ è la **funzione di distribuzione di una variabile aleatoria gaussiana standard $\mathcal{N}(0,\,1)$**.

Tutto ciò ci porta, finalmente, alla formulazione del **Teorema Centrale del Limite**:

> Considerando $n$ variabili aleatorie $X_{i}$, tutte indipendenti e con la stessa distribuzione, che ammettono dunque uno stesso valore atteso $\mu$ e una stessa varianza $\sigma^{2}$, e siano $\mu$ e $\sigma^{2}$ finiti (in particolare, $\sigma^{2}$ dovrà anche essere non nulla), allora indicando con $S_{n}^{*}$ la standardizzazione della variabile $S_{n}$ ossia:
> $$S_{n}^{*}=\frac{S_{n}-\mathbb{E}(S_{n})}{\sqrt{Var(S_{n})}}=\frac{S_{n}-n\mu}{\sqrt{n\sigma^{2}}}$$
> e indicando on $F_{S_{n}^{*}}(x)$ la funzione di distribuzione di $S_{n}^{*}$, abbiamo che:
> $$\lim_{n\,\to\,\infty}F_{S_{n}^{*}}(x)=\lim_{n\,\to\,\infty}\mathbb{P}(S_{n}^{*}\le x)=\Phi(x)$$
> dove $\Phi$ è la funzione di distribuzione di una variabile aleatoria gaussiana standard. In altri termini, si può affermare che:
> $$\lim_{n\,\to\,\infty}\mathbb{P}\left( \frac{S_{n}-n\mu}{\sqrt{ n\sigma^{2}}}\le x\right)=\int_{-\infty}^{x} \frac{1}{\sqrt{2\pi}}\,e^{- \frac{y^{2}}{2}}dy$$

Si precisa che **per la validità del Teorema Centrale del Limite, è necessario che le variabili aleatorie $X_{i}$ siano completamente indipendenti** tra loro.

Ora, avendo esplicitato con chiarezza questo teorema, è facile notare che abbiamo trovato un modo semplice e immediato per calcolare le probabilità del tipo $\mathbb{P}\left( \left\{\left| \frac{S_{n}}{n}-\mu\right|\le \epsilon \right\} \right)$ che cercavamo a inizio paragrafo. Infatti, l'enunciato del teorema implica che:
$$\lim_{n\,\to\,\infty}\mathbb{P}\left( a\le \frac{S_{n}-n\mu}{\sqrt{ n\sigma^{2}}}\le b \right)=\Phi(b)-\Phi(a)$$
ossia che, per $n$ sufficientemente grandi ($n$, infatti, tende a infinito), la probabilità cercata può essere accuratamente approssimata con la sottrazione $\Phi(b)-\Phi(a)$; per poter applicare questo ragionamento, dunque, si dovrà standardizzare la variabile aleatoria $S_{n}$, modificando di conseguenza anche gli estremi della disuguaglianza in cui è coinvolta. Ora, indicando con $Y_{n}$ la media aritmetica $\frac{S_{n}}{n}$, notiamo che:
$$Y_{n}-\mu=\frac{S_{n}-n\mu}{n}$$
e, di conseguenza, che:
$$\frac{Y_{n}-\mu}{\sqrt{\frac{\sigma^{2}}{n}}}\,=\,\sqrt{\frac{n}{\sigma^{2}}}\,(Y_{n}-\mu)\,=\,\sqrt{\frac{n}{\sigma^{2}}}\, \frac{S_{n}-n\mu}{n}\,=\, \frac{\sqrt{n}}{\sqrt{\sigma^{2}}}\, \frac{S_{n}-n\mu}{n}\,=\, \frac{S_{n}-n\mu}{\sqrt{n\sigma^{2}}}$$
In altre parole, **la standardizzazione $Y_{n}^{*}$ della media aritmetica $Y_{n}$ equivale perfettamente alla standardizzazione della somma campionaria $S_{n}$**, il che vuol dire che anche lavorando con $Y_{n}$ sarà possibile applicare il Teorema Centrale del Limite in modo analogo.
___