### Cosa sono le equazioni differenziali?

Solitamente, quando si parla di "equazioni", ci si riferisce a **equazioni algebriche** in cui viene richiesto di trovare uno o più valori che soddisfino una determinata uguaglianza. La seguente equazione:
$$x^2 + 3x - 1 = 0$$
è un perfetto esempio di questo tipo di equazione, per cui si potranno trovare due soluzioni $x_{1}$ e $x_{2}$.

Un'**equazione differenziale** è diversa da un'equazione algebrica, in quanto in un equazione differenziale non viene chiesto di trovare dei singoli valori di $x$, ma piuttosto delle **funzioni incognite** che possano soddisfare l'equazione. In particolare, un'equazione differenziale è un'equazione in cui uno dei membri contiene almeno una **derivata di qualsiasi ordine della funzione incognita**. 

> Un'**equazione differenziale ordinaria** (o **EDO**) è un'equazione in cui l'incognita è una funzione e uno dei termini dell'equazione è una derivata di qualsiasi ordine della funzione incognita stessa.
>
>L'ordine dell'equazione corrisponde all'ordine della derivata di ordine più alto presente nell'equazione stessa.

Per comprendere meglio di cosa si sta parlando, vediamo un esempio. Ponendo $f(x) = \cos x$, proviamo a risolvere la seguente equazione differenziale:
$$g'(x) = f(x)$$
Il problema posto, in realtà, non è altro che un modo alternativo per descrivere il problema del **trovare una primitiva di $f(x)$**, ossia in questo caso $g(x)$. Per risolvere il problema, dunque, possiamo integrare entrambi i lati dell'equazione:
$$\begin{align} g'(x) = f(x) \Longrightarrow g'(x) = \cos x &\Longrightarrow \int g'(x)\, dx = \int \cos(x)\, dx \\ &\Longrightarrow g(x) = \int \cos(x)\, dx \\ & \Longrightarrow g(x) = \sin(x) + c \end{align}$$
Si è ottenuto che $g(x) = \sin x + c$, con $c \in \mathbb{R}$. Poiché $c$ può essere una costante qualsiasi, tale equazione risulta avere infinite soluzioni.

Consideriamo, ad esempio, la seguente equazione differenziale ordinaria di secondo ordine:
$$y''(t) = 2$$
Poiché $y''(t)$ è una derivata di secondo ordine, per trovare la funzione incognita $y(t)$ è necessario integrare due volte entrambi i membri dell'equazione:
$$\begin{align} y''(t) = 2 &\Longrightarrow \iint y''(t)\, dt\, dt = \iint 2\, dt\, dt \\ &\Longrightarrow \int y'(t)\, dt = \int (2t + c_{1})\, dt \\ &\Longrightarrow y(t) = t^2 + c_{1}t + c_{2} \end{align}$$
con $c_{1}, c_{2} \in \mathbb{R}$. Poiché sia $c_{1}$ che $c_{2}$ possono essere qualsiasi costante, tale EDO ha infinite soluzioni dipendenti dai due parametri.

> Un'equazione differenziale di ordine $N$ ha infinite soluzioni dipendenti da $N$ parametri reali.

Per comodità, da adesso potrebbe essere omesso l'argomento della funzione $y(t)$ e delle sue derivate, limitandocisi eventualmente alle scritture $y$, $y'$, $y''$, ecc. ecc.
___
### Problema di Cauchy

> Un "**problema di Cauchy**" è un particolare tipo di problema matematico in cui, data un'equazione differenziale di ordine $N$ e una quantità $N$ di condizioni iniziali sufficienti, si è in grado di ricondurre tale problema a un'unica soluzione. Si dovrà avere, quindi, che:
> $$(c) = \begin{cases} \mbox{EDO di ordine } N \mbox{ per l'incognita } y(t) \\ N \mbox{ condizioni iniziali} \end{cases}$$
> dove $(c)$ è l'unica soluzione del problema.

Dunque, risolvere un problema di Cauchy significa trovare, tra le infinite soluzioni dell'EDO fornita, quella che soddisfa anche le $N$ condizioni iniziali. Per capire come procedere, analizziamo un esempio abbastanza basilare:
$$\begin{cases} y'(t) = -e^{-t} \\ y(0) = 3 \end{cases}$$
Come prima cosa, andiamo a trovare la soluzione dell'equazione differenziale al primo membro del sistema, risolvendola come abbiamo fatto nel paragrafo precedente:
$$\begin{align} y'(t) = -e^{-t} &\Longrightarrow \int y'(t)\, dt = \int -e^{-t}\, dt \\ &\Longrightarrow y(t) = e^{-t} + c \end{align}$$
A questo punto, per trovare il parametro $c$, e passare così dalla situazione generale delle infinite soluzioni alla unica soluzione che stiamo cercando, sfruttiamo la condizione iniziale fornita al secondo membro del sistema, sostituendo $t = 0$ e, di conseguenza, $y(0) = 3$:
$$\begin{align} y(t) = e^{-t} + c &\Longrightarrow y(0) = e^{0} + c \\ &\Longrightarrow 3 = 1 + c \\ &\Longrightarrow c = 2\end{align}$$
Avendo trovato il valore di $c$, possiamo affermare che la soluzione di questo problema di Cauchy è la funzione $y = e^{-t} + 2$. Proviamo, ora, ad analizzare un esempio un po' più complesso, che introduce una EDO di secondo ordine e, di conseguenza, due condizioni iniziali:
$$\begin{cases} y''(t) = t \\ y(0) = 1 \\ y'(0) = 4 \end{cases}$$
Procediamo in maniera sostanzialmente analoga: partiamo trovando l'insieme delle soluzioni generali dell'EDO:
$$\begin{align} y''(t) = t &\Longrightarrow \int y''(t)\, dt = \int t\, dt \\ &\Longrightarrow y'(t) = \frac{t^2}{2} + c_{1} \\ &\Longrightarrow \int y'(t)\, dt = \int \left( \frac{t^2}{2} + c_{1} \right)\, dt \\ &\Longrightarrow    y(t) = \frac{t^3}{6} + c_{1}t + c_{2} \end{align}$$
A questo punto, per trovare i parametri $c_{1}$ e $c_{2}$, sfruttiamo le due condizioni iniziali fornite dal problema. Sostituendo la prima (ossia $t = 0$ e $y(0) = 1$) all'interno della soluzione generica trovata per $y(t)$, si ha che:
$$\begin{align} y(t) = \frac{t^3}{6} + c_{1}t + c_{2} &\Longrightarrow y(0) = \frac{0^3}{6} + c_{1} \cdot 0 + c_{2} \\ &\Longrightarrow 1 = 0 + 0 + c_{2} \\ &\Longrightarrow c_{2} = 1\end{align}$$
Invece, sostituendo la seconda (ossia $t = 0$ e $y'(0) = 4$) all'interno della soluzione generica trovata per $y'(t)$, si ha che:
$$\begin{align} y'(t) = \frac{t^2}{2} + c_{1} &\Longrightarrow y'(0) = \frac{0^2}{2} + c_{1} \\ &\Longrightarrow 4 = 0 + c_{1} \\ &\Longrightarrow c_{1} = 4 \end{align}$$
Avendo trovato i valori di $c_{1}$ e $c_{2}$, possiamo affermare che la soluzione di questo problema di Cauchy è la funzione $y = \frac{t^3}{6} + 4t + 1$.

È importante tenere a mente che, per essere risolvibile, un problema di Cauchy deve essere "**ben formulato**", e deve dunque avere necessariamente **tante condizioni iniziali quanti sono i parametri $c$ da determinare**; inoltre, per essere tale, le condizioni iniziali del problema di Cauchy devono **fissare dei valori** per la funzione incognita e per le eventuali derivate **in uno stesso punto**.
___
### Equazioni differenziali a variabili separabili

Un'**equazione differenziale a variabili separabili** è un'equazione differenziale del primo ordine che si può ricondurre alla seguente forma generale:
$$y' = f(y) \cdot a(t)$$
dove $f(y)$ è una funzione della funzione $y(t)$, mentre $a(t)$ è una qualsiasi funzione di $t$. Ad esempio, i seguenti sono esempi di equazioni differenziali a variabili separabili:
$$y' = y \cdot \ln t \space \space \space \space \space \space \space \space (f(y) = y, \space \space a(t) = \ln t)$$
$$y' = e^t \cdot y \ln y \space \space \space \space \space \space \space \space (f(y) = y \ln y, \space \space a(t) = e^t)$$
> Per risolvere un'**equazione differenziale a variabili separabili**, bisogna:
>- **separare le variabili** in funzione di $t$ (ossia $a(t)$) da quelle in funzione di $y$ (ossia $y'$ e $f(y)$);
>- **integrare ciascun membro** rispetto alla variabile da cui dipende;
>- **ricavare $y(t)$**.

Analizziamo un esempio per comprendere meglio come applicare questo procedimento, provando a risolvere la seguente equazione differenziale:
$$y' = y^2 \cdot \ln t \Longrightarrow \frac{dy}{dt} = y^2 \cdot \ln t$$
dove si è sostituito $y' = \frac{dy}{dt}$, scrittura equivalente ma più comoda in questo tipo di equazione differenziale. A questo punto, procediamo a separare le variabili:
$$\frac{dy}{dt} = y^2 \cdot \ln t \Longrightarrow \frac{dy}{y^2} = dt \ln t$$
A questo punto, possiamo effettuare il secondo passaggio del procedimento, ossia integrare ciascun membro dell'equazione:
$$\frac{dy}{y^2} = dt \ln t \Longrightarrow \int \frac{1}{y^2}\, dy = \int \ln t\, dt$$
Risolvendo questi integrali, si ottiene che:
$$\begin{align} \int \frac{1}{y^2}\, dy = \int \ln t\, dt &\Longrightarrow -\frac{1}{y} = t \ln t - t + c \\ &\Longrightarrow y = - \frac{1}{t \ln t - t + c} \end{align}$$
L'insieme delle soluzioni di questa equazione differenziale è quindi l'insieme di funzioni $y(t) = - \frac{1}{t \ln t - t + c}$, con $c \in \mathbb{R}$. Vediamo un altro esempio, andando a risolvere un'equazione del genere inserita all'interno di un problema di Cauchy:
$$\begin{cases} y' = e^y \cdot \sin t \\ y\left( \frac{\pi}{2} \right) = 1 \end{cases}$$
Andiamo quindi a risolvere l'equazione differenziale che si presenta al primo membro del sistema. Partiamo separando le variabili:
$$\begin{align} y' = e^y \cdot \sin t &\Longrightarrow \frac{dy}{dt} = e^y \cdot \sin t \\ &\Longrightarrow \frac{dy}{e^y} = dt \cdot \sin t \\ &\Longrightarrow e^{-y} \cdot dy = \sin t \cdot dt \end{align}$$
A questo punto, integriamo i due membri dell'equazione:
$$\begin{align} e^{-y} \cdot dy = \sin t \cdot dt &\Longrightarrow \int e^{-y}\, dy = \int \sin t\, dt \\ &\Longrightarrow -e^{-y} = - \cos t + c \\ &\Longrightarrow e^{-y} = \cos t - c \\ &\Longrightarrow y = - \ln(\cos t - c) \end{align}$$
Avendo trovato l'insieme di funzioni che soddisfa l'equazione differenziale, resta solo da trovare il valore del parametro $c$ che soddisfa il problema di Cauchy che si sta risolvendo:
$$\begin{align} y(t) = -\ln(\cos t - c) &\Longrightarrow y\left( \frac{\pi}{2} \right) = -\ln\left( \cos\left( \frac{\pi}{2} \right) - c \right) \\ &\Longrightarrow 1 = -\ln(-c) \\ &\Longrightarrow \ln (-c) = -1 \\ &\Longrightarrow c = -\frac{1}{e} \end{align}$$
Si ottiene, così, che la soluzione del problema di Cauchy è la funzione $y(t) = -\ln\left( \cos t + \frac{1}{e} \right)$.

Nella risoluzione di un'equazione differenziale a variabili separabili, è importante ricordare una particolarità: spesso per tali equazioni sono ammesse **soluzioni costanti**, che potrebbero non emergere dalla risoluzione canonica dell'equazione. In generale, vale la seguente regola:

> Data un'equazione differenziale del tipo:
> $$y' = f(y) \cdot a(t)$$
> se esiste un valore costante $y_{0} \in \mathbb{R}$ tale per cui $f(y_{0}) = 0$, allora si ha che anche $y(t) = y_{0}$ è una soluzione dell'equazione differenziale in questione.

Ad esempio, nel primo esempio analizzato in questo paragrafo, troviamo che $y_{0} = 0$ è un valore che annulla $f(y)$, quindi alle soluzioni trovate canonicamente va aggiunta la soluzione $y(t) = 0$, che non sarebbe stata trovata altrimenti. Nel secondo esempio, invece, non ci sono valori costanti che annullino $f(y)$ (la funzione $e^y$ non può mai essere pari a $0$), quindi non sono presenti soluzioni costanti per tale equazione. 
___
### Equazioni differenziali lineari omogenee del primo ordine

Un'**equazione differenziale lineare del primo ordine** è un'equazione differenziale che assume la seguente forma generale:
$$y' + a(t) \cdot y = b(t)$$
dove $a(t)$ e $b(t)$ sono due funzioni di $t$. Ad esempio, i seguenti sono esempi di equazioni differenziali lineari del primo ordine:
$$y' - t \cdot y = 2t \space \space \space \space \space \space \space \space (a(t) = -t, \space \space b(t) = 2t)$$
$$y' + \frac{y}{t} = 4t^2 \space \space \space \space \space \space \space \space \left( a(t) = \frac{1}{t}, \space \space b(t) = 4t^2 \right)$$
Se $a(t) = 0$, si ricade in quella che potremmo definire un'equazione differenziale "**elementare**", simile a quelle analizzate nel primo paragrafo. Invece, se $b(t) = 0$, si ricade in quella che potremmo definire un'equazione differenziale lineare "**omogenea**". In questo paragrafo, in particolare, ci si limiterà all'analisi di equazioni lineari omogenee, dunque del tipo:
$$y' = a(t) \cdot y$$
Il caso più basilare di questo tipo di equazione è quando il termine $a(t)$ sia uguale a una costante $\lambda \in \mathbb{R}$:

> Data un'equazione differenziale del tipo
> $$y(t)' = \lambda y(t)$$
> con $\lambda \in \mathbb{R}$, si ottiene che:
> $$y(t) = e^{\lambda t + c}$$

In generale, invece, possiamo affermare che:

> Data un'equazione differenziale lineare di primo ordine, ossia un'equazione del tipo:
> $$y' = a(t) \cdot y$$
> la sua soluzione sarà:
> $$y(t) = C \cdot e^{A(t)}$$
> dove $C$ è una qualsiasi costante appartenente ai reali, mentre $A(t)$ è la primitiva di $a(t)$, ossia una funzione tale per cui $A'(t) = a(t)$ (per semplicità, è possibile omettere il parametro reale $c$ che si dovrebbe solitamente sommare alla primitiva).
___
### Equazioni differenziali lineari non omogenee del primo ordine

In questo paragrafo, si analizzeranno quelle EDO lineari in cui $a(t) \ne 0$ e $b(t) \ne 0$, ossia che non sono né elementari né omogenee.

Per risolvere questo tipo di equazione, uno dei metodi migliori è quello che viene spesso definito "**metodo del fattore integrante**", che prevede una serie di passaggi.

> Per risolvere un'**equazione differenziale lineare del primo ordine** del tipo
> $$y' + a(t) \cdot y = b(t)$$
> utilizzando il metodo del **fattore integrante**, si deve seguire il seguente procedimento:
> - **trovare una primitiva di $a(t)$** (per semplicità, è possibile omettere il parametro reale $c$ che si dovrebbe solitamente sommare alla primitiva);
> - **moltiplicare entrambi i membri dell'equazione per $e^{A(t)}$**, in modo da rendere il primo membro dell'equazione una derivata di $y \cdot e^{A(t)}$;
> - **integrare entrambi i membri** rispetto alla variabile $t$;
> - **esplicitare $y(t)$** moltiplicando entrambi i membri per $e^{-A(t)}$.
>
> La soluzione ottenuta con questo procedimento dovrebbe rispettare la seguente forma generalizzata:
> $$y(t) = e^{-A(t)} \left(\int b(t)e^{A(t)}\, dt \right)$$

Per comprendere meglio come applicare questo metodo, proviamo ad analizzare il seguente esempio:
$$y' - t \cdot y = 2t$$
dove $a(t) = -t$ e $b(t) = 2t$. Cominciamo trovando una primitiva $A(t)$ di $a(t)$, andando quindi ad integrare $a(t)$:
$$A(t) = \int -t\, dt = -\frac{t^2}{2}$$
A questo punto, procediamo al secondo passaggio andando a moltiplicare entrambi i membri dell'equazione iniziale per $e^{A(t)} = e^{- \frac{t^2}{2}}$:
$$y' \cdot e^{- \frac{t^2}{2}} - t \cdot y \cdot e^{- \frac{t^2}{2}} = 2t \cdot e^{- \frac{t^2}{2}}$$
Ora, integriamo entrambi i membri dell'equazione ottenuta:
$$\begin{align} y' \cdot e^{- \frac{t^2}{2}} - t \cdot y \cdot e^{- \frac{t^2}{2}} = 2t \cdot e^{- \frac{t^2}{2}} &\Longrightarrow \left[ y \cdot e^{- \frac{t^2}{2}} \right]' = 2t \cdot e^{- \frac{t^2}{2}} \\ &\Longrightarrow y \cdot e^{- \frac{t^2}{2}} = \int 2t \cdot e^{- \frac{t^2}{2}}\, dt \\ &\Longrightarrow y \cdot e^{- \frac{t^2}{2}} = -2e^{- \frac{t^2}{2}} + c \end{align}$$
Infine, andiamo ad esplicitare la funzione incognita moltiplicando entrambi i membri per $e^{-A(t)} = e^{\frac{t^2}{2}}$:
$$\begin{align} y \cdot e^{- \frac{t^2}{2}} = -2e^{- \frac{t^2}{2}} + c &\Longrightarrow y \cdot e^{- \frac{t^2}{2}}e^{\frac{t^2}{2}} = -2e^{- \frac{t^2}{2}}e^{\frac{t^2}{2}} + c\cdot e^{\frac{t^2}{2}} \\ &\Longrightarrow y = -2 + c \cdot e^{\frac{t^2}{2}} \end{align}$$
___
### Equazioni differenziali lineari omogenee del secondo ordine

[pag. 118 - 119 - 120 - 121 - 122]
___
### Equazioni differenziali lineari non omogenee del secondo ordine

[pag. 123 - 124 - 125 - 126 - 127 - 128 - 129]