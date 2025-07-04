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

Vediamo, ora, le **EDO lineari omogenee del secondo ordine**, e in particolare quelle a coefficienti reali costanti, ossia equazioni differenziali che assumono genericamente la seguente forma:
$$ay'' + by' + cy = 0$$
Per questo tipo di equazioni, l'insieme delle soluzioni di una determinata equazione consiste in uno "**spazio vettoriale**" di dimensione 2: in parole povere, ciò vuol dire che:
- trovata una soluzione $y$, anche $Ay$ (per ogni $A \in \mathbb{R}$) sarà una soluzione; 
- trovate due soluzioni $y_{1}$ e $y_{2}$, anche la somma $y = Ay_{1} + By_{2}$ sarà una soluzione.

Generalmente, l'obiettivo è trovare queste due soluzioni qualsiasi $y_{1}$ e $y_{2}$, e impostare la **soluzione generica** dell'equazione.

> Per risolvere un'**EDO lineare omogenea del secondo ordine** a coefficienti reali costanti, ossia un'equazione differenziale del tipo:
> $$ay'' + by' + cy = 0$$
> si dovrà:
> - **risolvere l'equazione caratteristica** $a\lambda^2 + b\lambda + c = 0$, trovando così due soluzioni $\lambda_{1}$ e $\lambda_{2}$;
> - **ricavare due soluzioni $y_{1}$ e $y_{2}$** in base ai valori di $\lambda_{1}$ e $\lambda_{2}$:
> 	- se si avranno **due soluzioni reali e distinte** ($\Delta > 0$), ossia $\lambda_{1} \neq \lambda_{2}$, allora le basi dello spazio delle soluzioni saranno $y_{1} = e^{\lambda_{1}t}$ e $y_{2} = e^{\lambda_{2}t}$, e dunque la soluzione generica sarà $y(t) = Ae^{\lambda_{1}t} + Be^{\lambda_{2}t}$;
> 	- se si avranno **due soluzioni reali e coincidenti** ($\Delta = 0$), ossia $\lambda_{1} = \lambda_{2}$, allora le basi dello spazio delle soluzioni saranno $y_{1} = e^{\lambda t}$ e $y_{2} = te^{\lambda t}$, e dunque la soluzione generica sarà $y(t) = Ae^{\lambda t} + Bte^{\lambda t}$;
> 	- se si avranno **due soluzioni complesse e distinte** ($\Delta < 0$), ossia $\lambda_{1} = \alpha + \beta i$ e $\lambda_{2} = \alpha - \beta i$, allora le basi dello spazio delle soluzioni saranno $y_{1} = e^{\alpha t} \cdot \cos \beta t$ e $y_{2} = e^{\alpha t} \cdot \sin \beta t$, e dunque la soluzione generica sarà $y(t) = Ae^{\alpha t} \cdot \cos \beta t + Be^{\alpha t} \cdot \sin \beta t$.
> - eventualmente, **ricavare i coefficienti $A$ e $B$** se ci si trova in un [[Equazioni differenziali#Problema di Cauchy|problema di Cauchy]].

Per comprendere meglio come applicare questo metodo, proviamo ad analizzare il seguente esempio:
$$\begin{cases} y'' + 2y' + 2y = 0 \\ y(0) = 1 \\ y'(0) = 1 \end{cases}$$
L'equazione caratteristica associata all'equazione differenziale presente nel problema di Cauchy è:
$$\lambda^2 + 2\lambda + 2 = 0$$
Andando a risolvere quest'equazione per trovare $\lambda_{1}$ e $\lambda_{2}$, si ottiene che:
$$\lambda_{1,\, 2} = \frac{-2 \pm \sqrt{4 - 4(1)(2)}}{2} = \frac{-2 \pm 2\sqrt{-1}}{2} = \frac{2(-1 \pm i)}{2} = -1 \pm i$$
Avendo, quindi, che $\lambda_{1} = -1 + i$ e che $\lambda_{2} = -1 - i$, riconosciamo di trovarci nel terzo caso, con $\alpha = -1$ e $\beta = 1$. Dunque, si ha che:
$$y_{1} = e^{-t} \cdot \cos t, \, \, \, y_{2} = e^{-t} \cdot \sin t \, \, \, \, \, \Longrightarrow \, \, \, \, \, y(t) = Ae^{-t} \cdot \cos t + Be^{-t} \cdot \sin t$$
A questo punto, trovandoci in un problema di Cauchy, sarà possibile ricavare i coefficienti $A$ e $B$ per trovare una soluzione unica. Per fare ciò, a partire dalla soluzione generica appena trovata, ricaviamone la derivata $y'(t)$:
$$\begin{align} y(t) = Ae^{-t} \cdot \cos t + Be^{-t} \cdot \sin t \, \, \, &\Longrightarrow \, \, \, y'(t) = A(-e^{-t} \cdot \cos t - e^{-t} \cdot \sin t) + B(-e^{-t} \cdot \sin t + e^{-t} \cdot \cos t) \\ &\Longrightarrow \, \, \, y'(t) = -Ae^{-t} \cdot \cos t - Ae^{-t} \cdot \sin t - Be^{-t} \cdot \sin t + Be^{-t} \cdot \cos t \\ &\Longrightarrow \, \, \, y'(t) = e^{-t}(- A\sin t - A\cos t - B\sin t + B\cos t) \end{align}$$
A questo punto, possiamo impostare un sistema di equazioni per trovare i coefficienti $A$ e $B$:
$$\begin{cases} y(0) = 1 \\ y'(0) = 1 \end{cases}\, \, \, \, \, \Longrightarrow \, \, \, \, \, \begin{cases} Ae^{0} \cdot \cos 0 + Be^{0} \cdot \sin 0 = 1 \\ e^{0}(- A\sin 0 - A \cos 0 - B \sin 0 + B \cos 0) = 1 \end{cases}\, \, \, \, \, \Longrightarrow \, \, \, \, \, \begin{cases} A = 1 \\ - A + B = 1 \end{cases}\, \, \, \, \, \Longrightarrow \, \, \, \, \, \begin{cases} A = 1 \\ B = 2 \end{cases}$$
L'unica soluzione del problema di Cauchy, dunque, è la seguente:
$$y(t) = e^{-t} \cdot \cos t + 2e^{-t} \cdot \sin t = e^{-t}(\cos t + 2 \sin t)$$
___
### Equazioni differenziali lineari non omogenee del secondo ordine

Analizziamo, infine, le **EDO lineari non omogenee del secondo ordine**, ossia quelle equazioni differenziali che si presentano nella seguente forma:
$$ay'' + by' + cy = f(t)$$
> Per risolvere un'**EDO lineare non omogenea del secondo ordine**, ossia un'equazione differenziale del tipo:
> $$ay'' + by' + cy = f(t)$$
> si dovrà:
> - **determinare la soluzione generica $y_{o}(t) = Ay_{1} + By_{2}$ dell'equazione omogenea associata** (ossia, la stessa equazione differenziale ma con $f(t) = 0$);
> - a partire dalle soluzioni $y_{1}$ e $y_{2}$ trovate, bisogna **ricavare una soluzione particolare della forma $y_{p}(t) = A(t)y_{1} + B(t)y_{2}$**, con $A(t)$ e $B(t)$ che potranno essere trovate risolvendo il seguente sistema di equazioni;
> $$\begin{cases} A'(t)y_{1} + B'(t)y_{2} = 0 \\ A'(t)y_{1}' + B'(t)y_{2}' = f(t) \end{cases}$$
> - trovata anche la soluzione particolare $y_{p}(t)$, la soluzione generica dell'equazione iniziale sarà $y(t) = y_{o}(t) + y_{p}(t)$.

Per comprendere meglio come applicare questo metodo, proviamo ad analizzare il seguente esempio:
$$y'' - 2y' + y = \frac{e^x}{x^4}$$
Prima di tutto, andiamo a ricavare $y_{o}(t)$, ossia la soluzione generica dell'equazione omogenea associata. Per fare ciò, risolviamo la seguente equazione:
$$\lambda^2 - 2\lambda + 1 = 0\, \, \, \, \, \Longrightarrow \, \, \, \, \, \lambda_{1} = \lambda_{2} = 1$$
Ci troviamo nel caso in cui le due soluzioni $\lambda_{1}$ e $\lambda_{2}$ sono uguali, dunque le basi dello spazio delle soluzioni saranno $y_{1} = e^{t}$ e $y_{2} = te^{t}$, portando alla seguente soluzione generica $y_{o}(t)$:
$$\begin{cases} y_{1} = e^{t} \\ y_{2} = te^{t} \end{cases}\, \, \, \Rightarrow \, \, \, y_{o}(t) = Ae^{t} + Bte^{t}$$
Ora, possiamo trovare la soluzione particolare $y_{p}(t)$. Per fare ciò, impostiamo il sistema di equazioni che ci permetterà di ottenere $A(t)$ e $B(t)$:
$$\begin{cases} A'(t)e^{t} + B'(t)te^{t} = 0 \\ A'(t)e^{t} + B'(t)(e^{t} + te^{t}) = \frac{e^{t}}{t^4} \end{cases}\, \, \, \Rightarrow \, \, \, \begin{cases} A'(t) = -\frac{B'(t)te^{t}}{e^{t}} \\ A'(t)e^{t} + B'(t)e^{t} + B'(t)te^{t} = \frac{e^{t}}{t^4} \end{cases}\, \, \, \Rightarrow \, \, \, \begin{cases} A'(t) = -B'(t)t \\ -B'(t)te^{t} + B'(t)e^{t} + B'(t)te^{t} = \frac{e^{t}}{t^4} \end{cases}\, \, \, \Rightarrow \, \, \, \begin{cases} A'(t) = -B'(t)t \\ B'(t)e^{t} = \frac{e^{t}}{t^4} \end{cases}\, \, \, \Rightarrow \, \, \, \begin{cases} A'(t) = -\frac{1}{t^3} \\ B'(t) = \frac{1}{t^4} \end{cases}$$
Avendo trovato $A'(t)$ e $B'(t)$, trovare $A(t)$ e $B(t)$ consiste semplicemente nell'integrare le funzioni appena trovate:
$$A(t) = - \int \frac{1}{t^3}\, dt = - \int t^{-3}\, dt = \frac{1}{2t^2}\, \, \, \, \, \, \, \, \, \, B(t) = \int \frac{1}{t^4}\, dt = \int t^{-4}\, dt = -\frac{1}{3t^3}$$
A questo punto, ricaviamo la soluzione particolare $y_{p}(t)$:
$$y_{p}(t) = A(t)y_{1} + B(t)y_{2} = \frac{1}{2t^2}e^{t} - \frac{1}{3t^3}te^{t} = \frac{e^t}{2t^2} - \frac{e^{t}}{3t^2} = \frac{e^t}{6t^2}$$
Infine, arriviamo alla soluzione generica dell'equazione differenziale che volevamo risolvere, ossia $y(t) = y_{o}(t) + y_{p}(t)$:
$$y(t) = Ae^{t} + Bte^{t} + \frac{e^{t}}{6t^2}$$
