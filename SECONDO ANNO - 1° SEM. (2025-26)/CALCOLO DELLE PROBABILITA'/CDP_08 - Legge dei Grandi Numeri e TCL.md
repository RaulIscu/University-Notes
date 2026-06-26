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



[pag. 249/255]
___