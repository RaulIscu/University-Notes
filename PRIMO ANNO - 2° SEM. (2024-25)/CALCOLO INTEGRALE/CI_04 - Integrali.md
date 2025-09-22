### Cos'è un integrale?

> Data una funzione $f(x)$, un intervallo $[a, b]$ di tale funzione, l'**integrale** **di $f(x)$** nell'intervallo $[a, b]$ consiste nell'**area** (con segno) **della regione di piano sottesa al grafico** della funzione all'interno dell'intervallo $[a, b]$. Questa operazione viene indicata nel seguente modo:
> $$\int_{a}^{b} f(x)\,dx$$

Informalmente, l'area definita da un integrale del genere può essere definita come la regione di piano compresa tra il grafico di $f(x)$, l'asse $x$ del piano e le rette verticali $x = a$ e $x = b$. Per "**con segno**", invece, si intende che se l'integrale assumerà il segno della funzione $f(x)$ nell'intervallo considerato.

L'intervallo $[a, b]$ prende il nome di "**intervallo** (o **zona**) **di integrazione**"; la funzione $f(x)$, poi, viene detta "**funzione integranda**"; infine, la notazione $dx$ serve a indicare che si sta integrando rispetto alla variabile $x$.
___
### Come si calcola un integrale?

Ma come si può **calcolare un integrale**? Supponiamo di avere una funzione $f(x)$ e di volerne calcolare l'integrale nell'intervallo $[a, b]$; dunque, si vuole calcolare l'area evidenziata nel seguente grafico:

![[integral1.png]]

Tale figura, tuttavia, non corrisponde a un poligono o a una qualsiasi altra figura nota, e non è dunque possibile calcolarne l'area in maniera diretta. Per procedere, quindi, proviamo un approccio particolare, ossia **approssimare l'area sottesa come una somma delle aree di una serie di rettangoli**. Per cominciare ad applicare questo approccio, ipotizziamo di aggiungere al piano una retta $r(x) = M$:

![[integral2.png]]

Considerando il rettangolo che ha come base $(b - a)$ e come altezza $M$, possiamo affermare con certezza che tale rettangolo ha un'area maggiore di quella cercata. Si può affermare, poi, considerando un ipotetico rettangolo che ha come base $(b - a)$ e altezza $0$, che tale rettangolo a un'area (pari a $0$) minore di quella cercata. Formalmente, possiamo quindi affermare che:
$$0 \cdot (b - a) \le A \le M \cdot (b - a)$$
dove $A$ è proprio l'area che stiamo cercando.

Risulta evidente come la stima appena fatta sia in realtà molto inaccurata. Affinandola, possiamo considerare le due rette $r_{1}(x) = M = max(y_{a}, \space y_{b})$ e $r_{2}(x) = m = min(y_{a}, \space y_{b})$, ottenendo il seguente grafico:

![[integral3.png]]

Applicando lo stesso ragionamento precedente, possiamo affermare che:
$$m \cdot (b - a) \le A \le M \cdot (b - a)$$
Possiamo continuare ad aumentare la precisione della nostra stima, stavolta aumentando il numero di rettangoli creati. Ad esempio, sia $x_{1} = \frac{b - a}{2}$, possiamo scomporre l'intervallo $[a, b]$ iniziale in due intervalli di uguale ampiezza $[a, x_{1}]$ e $[x_{1}, b]$; per ognuno di questi sotto-intervalli, immaginiamo di aggiungere al due rette in maniera analoga agli approcci precedenti, e otterremmo il seguente grafico:

![[integral4.png]]

A questo punto, la stima dell'area diventa ancora più precisa:
$$m_{0} \cdot \frac{b - a}{2} + m_{1} \cdot \frac{b - a}{2} \le A \le M_{0} \cdot \frac{b - a}{2} + M_{1} \cdot \frac{b - a}{2} \space\space \Longrightarrow \space\space (m_{0} + m_{1}) \cdot \frac{b - a}{2} \le A \le (M_{0} + M_{1}) \cdot \frac{b - a}{2}$$
dove $m_{0} = min(a, \space x_{1})$, $m_{1} = min(x_{1}, \space b)$, $M_{0} = max(a, \space x_{1})$ e $M_{1} = max(x_{1}, \space b)$.

Volendo aumentare ancora la precisione della stima, raddoppiamo il numero dei rettangoli da 2 a 4. Si ottiene il seguente grafico:

![[integral5.png]]

Per cui si ottiene la seguente stima dell'area sottesa, ancora più precisa:
$$\frac{b - a}{4} \cdot (m_{0} + m_{1} + m_{2} + m_{3}) \le A \le \frac{b - a}{4} \cdot (M_{0} + M_{1} + M_{2} + M_{3})$$
Notiamo, a questo punto, che questa stima può essere riscritta utilizzando delle **serie**:
$$\frac{b - a}{2^2} \cdot \sum_{k = 0}^{2^2 - 1}m_{k} \le A \le \frac{b - a}{2^2} \cdot \sum_{k = 0}^{2^2 - 1}M_{k}$$
Ricordando che $m_{k}$ e $M_{k}$ corrispondono rispettivamente al minimo e al massimo del $k$-esimo intervallo, possiamo arrivare alla seguente **forma generalizzata**:
$$\frac{b - a}{2^n} \cdot \sum_{k = 0}^{2^n - 1}min_{[x_{k}, \space x_{k + 1}]}f(x) \le A \le \frac{b - a}{2^n} \cdot \sum_{k = 0}^{2^n - 1}max_{[x_{k}, \space x_{k + 1}]}f(x)$$
dove $n$ corrisponde al numero di suddivisioni dell'intervallo iniziale $[a, b]$, e ogni $x_{k}$ corrisponde dunque a $a + k \cdot \frac{b - a}{2^n}$.

Facciamo, ora, alcune osservazioni: notiamo, innanzitutto, che all'aumentare delle suddivisioni **la somma delle aree dei rettangoli "maggiori"**, che per comodità possiamo indicare come $\overline{S_{n}}$, **va a diminuire**; inoltre, allo stesso tempo **la somma delle aree dei rettangoli "minori"**, che per comodità possiamo indicare come $\underline{S_{n}}$, **va ad aumentare**.

A questo punto si ottiene logicamente che, suddividendo l'intervallo iniziale un numero infinito di volte (dunque, per $n \rightarrow +\infty$), l'errore nella stima si riduce a un valore infinitesimale. Si ha, quindi, che:
$$\lim_{n \to +\infty} \underline{S_{n}} = \lim_{n \to +\infty} \overline{S_{n}} = A$$
Si conclude, dunque, che per $n \rightarrow +\infty$ le somme $\underline{S_{n}}$ e $\overline{S_{n}}$ convergono al valore dell'area cercata $A$. Se $f(x)$ è una funzione su cui può essere applicato tale concetto, si dice che tale funzione è "**integrale secondo Riemann**".

> Sia $f: [a, b] \rightarrow \mathbb{R}$; si dice che $f$ è **integrabile secondo Riemann** se, dati i due limiti:
> $$\lim_{n \to +\infty} \frac{b - a}{2^n} \cdot \sum_{k = 0}^{2^n - 1}min_{[x_{k}, \space x_{k + 1}]}f(x) = \underline{S} \space \space \space \space \space \space \space \space \space \space \space \space \space \space \lim_{n \to +\infty} \frac{b - a}{2^n} \cdot \sum_{k = 0}^{2^n - 1}max_{[x_{k}, \space x_{k + 1}]}f(x) = \overline{S}$$
> si verifica che $\underline{S} = \overline{S}$.
___
### Proprietà degli integrali

Una qualsiasi funzione $f(x)$ **continua** o **monotona** (dunque, anche monotona discontinua o continua non monotona) nell'intervallo $[a, b]$ è **integrabile nell'intervallo $[a, b]$**.

Tenendo a mente la definizione geometrica di integrale, dunque del fatto che corrisponda all'area sottesa a una funzione in un intervallo specifico, possiamo formulare alcune **proprietà degli integrali**, tra cui:
- **linearità** di un integrale;
- **additività** di un integrale;
- **invertibilità dell'intervallo di integrazione** di un integrale;
- **differenza** tra integrali.

> La proprietà della **linearità** di un integrale afferma che, date due funzioni $f$ e $g$ integrabili nell'intervallo $[a, b]$, la funzione $h(x) = \alpha f(x) + \beta g(x)$ è integrabile nello stesso intervallo, e il suo integrale equivale alla somma dell'integrale di $\alpha f(x)$ e di $\beta g(x)$ in tale intervallo:
> $$\int_{a}^{b} [\alpha f(x) + \beta g(x)]\,dx = \alpha \int_{a}^{b}f(x)\,dx + \beta \int_{a}^{b} g(x)\, dx$$

> La proprietà dell'**additività** di un integrale afferma che, sia $[a, b] = [a, c] \cup [c, b]$, dove $c \in [a, b]$, e sia $f$ una funzione integrabile in $[a, c]$ e in $[c, b]$, allora $f$ sarà integrabile anche in $[a, b]$ e il suo integrale in tale intervallo equivale alla somma tra l'integrale in $[a, c]$ e quello in $[c, b]$:
> $$\int_{a}^{b} f(x)\, dx = \int_{a}^{c} f(x)\, dx + \int_{c}^{b} f(x)\, dx$$

Quest'ultima proprietà ci permette di fare delle assunzioni aggiuntive, ad esempio in relazione alla definizione di **funzione integrabile** che è stata fornita a inizio paragrafo: supponendo, infatti, di avere una funzione non integrabile, e dunque discontinua e non monotona, in un intervallo $[a, b]$, per calcolarne l'integrale in tale intervallo sarà sufficiente **scomporre l'integrale in vari integrali su sotto-intervalli** dell'intervallo iniziale, in modo da avere un frammento di funzione monotono o continuo in ognuno di questi sotto-intervalli. Possiamo, quindi, affermare che:

> Una funzione $f$ è **integrabile** in un intervallo $[a, b]$ se all'interno di tale intervallo:
> - è **monotona** e **limitata**;
> - è **continua**;
> - presenta un **numero finito di cambi di monotonia**;
> - presenta un **numero finito di discontinuità**.

Inoltre, sempre la proprietà dell'additività ci permette di calcolare integrali in cui la funzione non assume valori strettamente positivi nell'intervallo considerato. Ad esempio, avendo una funzione come la seguente:

![[integral_negative.png]]

l'integrale in $[a, b]$ può essere comodamente spezzato nella somma tra l'integrale calcolato in $[a, c]$ e quello calcolato in $[c, b]$. Tuttavia, assumendo la funzione valori negativi in $[a, c]$, anche il risultato di tale integrale sarà negativo; dunque, per ottenere l'**area assoluta** sottesa al grafico nell'intervallo $[a, b]$, bisognerà invertire il segno dell'integrale in $[a, c]$, in modo da ottenere la somma effettiva tra le due aree:
$$\int_{a}^{b} f(x)\, dx = - \int_{a}^{c} f(x)\, dx + \int_{c}^{b} f(x)\, dx$$
> Se una funzione $f$ assume valori negativi $\forall x \in [x_{1}, \space x_{2}]$ e viene integrata in tale intervallo, allora è necessario **negare il risultato** dell'integrale.

Finora si sono analizzati solo casi di integrali su intervalli $[a, b]$ dove effettivamente si ha che $a < b$; ma cosa succederebbe se invece $a > b$? A livello quantitativo, il risultato non varierà, in quanto l'area sottesa rimane identica, tuttavia cambierà il segno del risultato. Infatti:

> La proprietà dell'**invertibilità dell'intervallo di integrazione** di un integrale afferma che, sia $f$ una funzione integrabile in $[a, b]$ dove $a < b$, allora vale che:
> $$\int_{a}^{b} f(x)\, dx = - \int_{b}^{a} f(x)\, dx$$

È possibile, infine, calcolare un integrale mediante la differenza tra due altri integrali.

> La proprietà della **differenza** tra integrali afferma che, sia $[a, b]$ un intervallo e sia $c \in [a, b]$, se $f$ è una funzione integrabile in $[a, b]$ allora l'integrale di $f$ in $[c, b]$ è esprimibile come:
> $$\int_{c}^{b} f(x)\, dx = \int_{a}^{b} f(x)\, dx - \int_{a}^{c} f(x)\, dx$$

Se l'intervallo di integrazione coincide con un punto $a$, allora il valore dell'integrale sarà sempre $0$, qualsiasi sia la funzione integranda:
$$\int_{a}^{a} f(x)\, dx = 0$$
___
### Teorema fondamentale del calcolo integrale

Supponiamo di voler calcolare l'integrale di $f(x) = x$ nell'intervallo $[t, t + h]$. Per fare ciò, possiamo sfruttare una differenza tra integrali, affermando che:
$$\int_{t}^{t + h} x\, dx = \int_{0}^{t + h}x\, dx - \int_{0}^{t} x\, dx$$
Essendo le aree relative a tali integrali dei triangoli, si possono facilmente calcolare:
$$\int_{0}^{t + h}x\, dx - \int_{0}^{t} x\, dx = \frac{(t + h) \cdot (t + h)}{2} - \frac{t \cdot t}{2} = \frac{(t + h)^2}{2} - \frac{t^2}{2}$$
Tali aree sono valide per qualsiasi valore di $t$, e per questo è possibile effettuare una generalizzazione e trovare una **funzione ausiliaria $F(x)$** corrispondente a qualsiasi integrale di $f(x) = x$ in un intervallo $[0, t]$:
$$F(t) = \int_{0}^{t}x\, dx = \frac{t^2}{2}$$
Avendo trovato questa funzione, si può riscrivere l'integrale iniziale come:
$$\int_{t}^{t + h}x\, dx = F(t + h) - F(t) = \frac{(t + h)^2}{2} - \frac{t^2}{2}$$
A questo punto, chiediamoci quale sia la derivata di tale funzione $F(t)$, in modo da sapere quanto il suo valore cambi al variare del suo argomento. Calcolando il limite per $h \rightarrow 0$ del suo rapporto incrementale, si ottiene che:
$$F'(x) = \lim_{h \to 0} \frac{F(t + h) - F(t)}{h} = \lim_{h \to 0} \frac{\frac{(t + h)^2}{2} - \frac{t^2}{2}}{h} = \lim_{h \to 0} \frac{2th + h^2}{2h} = t$$
Notiamo, dunque, che **la derivata di $F(x)$ corrisponde esattamente al valore di $t$**. In altre parole, la derivata della funzione ausiliaria in $t$ corrisponde esattamente al valore della funzione originale in $t$.

> Sia $f(x)$ una funzione integrabile in $[0, t]$, tale per cui:
> $$F(t) = \int_{0}^{t} f(x)\, dx$$
> Si ha che $F'(t) = f(t)$. Dunque, si può informalmente affermare che **l'integrale è l'operazione matematica inversa della derivata**.

Tornando all'esempio iniziale, con $f(x) = x$, notiamo infatti che la funzione $F(x)$ corrisponde a una funzione la cui derivata coincide proprio con $f(x)$.

Tale teorema fondamentale ci permette di calcolare con facilità il valore di un qualsiasi integrale di una funzione $f(x)$ in un certo intervallo, limitando il calcolo al **trovare il valore assunto dalla corrispettiva funzione $F(x)$ negli estremi dell'intervallo di integrazione**. Per comodità, in seguito si utilizzeranno le seguenti notazioni nei calcoli di un integrale:
$$\int_{a}^{b} f(x)\, dx = F(x) \, \, |_{a}^{b} = F(b) - F(a)$$
___
### Integrali indefiniti e funzioni primitive

La funzione $F(x)$ definita dal [[CI_04 - Integrali#Teorema fondamentale del calcolo integrale|teorema fondamentale del calcolo integrale]] viene detta "**primitiva di $f(x)$**" e, per ogni funzione $f(x)$, ne esistono **infinite**: infatti, se $F(x)$ è una primitiva di $f(x)$ allora una qualsiasi funzione $G(x) = F(x) + c$, per qualsiasi costante $c \in \mathbb{R}$, è anch'essa una primitiva di $f(x)$.

> Sia $f(x)$ una funzione integrabile, allora esistono **infinite funzioni primitive $G(x)$**, tali per cui $G'(x) = f(x)$, con $G(x) = F(x) + c$ per ogni $c \in \mathbb{R}$.

In generale, se una funzione è continua nell'intervallo di integrazione $[a, b]$, ciò vuol dire che esiste almeno una primitiva valida per quell'intervallo.

Inoltre, nel paragrafo precedente si è visto come si possa considerare l'integrazione come l'operazione matematicamente inversa alla derivazione. In particolare, possiamo fare una differenza tra due tipi principali di integrale:
- l'**integrale definito**, ossia quello usato finora, che viene utilizzato per calcolare l'area sottesa a una funzione in un determinato intervallo definito;
- l'**integrale indefinito**, che viene utilizzato come operazione inversa alla derivazione su una determinata funzione.

> Si definisce "**integrale indefinito**" l'operazione inversa alla derivazione di una funzione $f(x)$, che consiste nel trovare la primitiva $F(x)$ di tale funzione:
> $$\int f(x)\, dx = F(x) + c$$
___
### Integrali immediati

Di seguito, i principali **integrali immediati**:
- l'integrale di $x^\alpha$ (con $\alpha \neq -1$), è pari a:
$$\int x^\alpha\, dx = \frac{x^{\alpha + 1}}{\alpha + 1} + c$$
- l'integrale di $x^{-1}$, ossia di $\frac{1}{x}$, è pari a:
$$\int x^{-1}\, dx = \int \frac{1}{x}\, dx = \ln|x| + c$$
- l'integrale di $e^x$ è pari a:
$$\int e^x\, dx = e^x + c$$
- l'integrale di $e^{\alpha x}$ è pari a:
$$\int e^{\alpha x}\, dx = \frac{e^{\alpha x}}{\alpha} + c$$
- l'integrale di $\cos(\alpha x)$ è pari a:
$$\int \cos(\alpha x)\, dx = \frac{\sin(\alpha x)}{\alpha} + c$$
- l'integrale di $\sin(\alpha x)$ è pari a:
$$\int \sin(\alpha x)\, dx = - \frac{\cos(\alpha x)}{\alpha} + c$$
- l'integrale di $\frac{1}{\cos^2x}$ è pari a:
$$\int \frac{1}{\cos^2x}\, dx = \tan x + c$$
- l'integrale di $\frac{1}{1 + x^2}$ è pari a:
$$\int \frac{1}{1 + x^2}\, dx = \arctan x + c$$
- l'integrale di $\alpha$ è pari a:
$$\int \alpha\, dx = \alpha x + c$$
- l'integrale di $\alpha^x$ è pari a:
$$\int \alpha^x\, dx = \frac{\alpha^x}{\ln \alpha} + c$$
- l'integrale di $\frac{1}{\alpha x + \beta}$ è pari a:
$$\int \frac{1}{\alpha x + \beta}\, dx = \frac{\ln |\alpha x + \beta|}{\alpha} + c$$
- l'integrale di $e^{\alpha x} \cdot \cos(\beta x)$ è pari a:
$$\int e^{\alpha x} \cdot \cos(\beta x)\, dx = \frac{e^{\alpha x}(\alpha \cos(\beta x) + \beta \sin(\beta x))}{\beta^2 + \alpha^2} + c$$
- l'integrale di $e^{\alpha x} \cdot \sin(\beta x)$ è pari a:
$$\int e^{\alpha x} \cdot \sin(\beta x)\, dx = \frac{e^{\alpha x}(\alpha \sin(\beta x) - \beta \cos(\beta x))}{\beta^2 + \alpha^2} + c$$
___
### Integrali immediati di funzioni composte

Per le **funzioni composte** di tipo $f(g(x))$, sappiamo che $F'(g(x)) = f(g(x)) \cdot g'(x)$, e dunque possiamo affermare che :
$$\int f(g(x)) \cdot g'(x)\, dx = F(g(x)) + c$$
Da questo principio, possiamo generalizzare alcuni integrali immediati nei loro corrispettivi con funzioni composte. Ad esempio:
- l'integrale di $g'(x) \cdot \cos g(x)$ è pari a:
$$\int g'(x) \cdot \cos g(x)\, dx = \sin g(x) + c$$
- l'integrale di $g'(x) \cdot \sin g(x)$ è pari a:
$$\int g'(x) \cdot \sin g(x)\, dx = - \cos g(x) + c$$
- l'integrale di $g'(x) \cdot e^{g(x)}$ è pari a:
$$\int g'(x) \cdot e^{g(x)}\, dx = e^{g(x)} + c$$
- l'integrale di $g'(x) \cdot g(x)^\alpha$ (con $\alpha \neq -1$) è pari a:
$$\int g'(x) \cdot g(x)^\alpha\, dx = \frac{g(x)^{\alpha + 1}}{\alpha + 1} + c$$
- l'integrale di $g'(x) \cdot g(x)^{-1}$, ossia di $\frac{g'(x)}{g(x)}$, è pari a:
$$\int \frac{g'(x)}{g(x)}\, dx = \ln |g(x)| + c$$
___
### Integrazione per sostituzione

Un metodo per calcolare gli integrali di funzioni per cui non è possibile applicare immediatamente gli [[CI_04 - Integrali#Integrali immediati|integrali immediati]] è la cosiddetta "**integrazione per sostituzione**". Per comprendere questo procedimento, consideriamo il seguente esempio:
$$\int_{1}^{4}e^{3x}\, dx$$
Notiamo come tale integrale risulti essere simile all'integrale di $e^x$, la cui primitiva sappiamo essere $F(x) = e^x$. Per semplificare il calcolo dell'integrale, è possibile effettuare una **sostituzione di variabile** per ricondurci a tale integrale immediato.

È importante ricordare, quando si risolve un integrale mediante l'integrazione per sostituzione, che si deve **sostituire ogni singolo riferimento alla variabile originale** presente nell'integrale, inclusi gli estremi dell'intervallo di integrazione e la variabile di integrazione. Nel nostro caso, possiamo effettuare i seguenti passaggi:
- poniamo $y = 3x$, in modo da trasformare $e^{3x}$ in $e^y$;
- stabilito tale valore per la nuova variabile $y$, quando $x = 1$ si ha che $y = 3$, mentre quando $x = 4$ si ha che $y = 12$, quindi l'intervallo di integrazione precedente $[1, 4]$ va sostituito col nuovo intervallo $[3, 12]$;
- per modificare, infine, la variabile di integrazione, sfruttiamo l'equazione generica $dy \cdot y' = dx \cdot f'(x)$, dove $f(x)$ rappresenta ciò che si sta sostituendo mediante $y$, e dunque si ha che:
$$dy \cdot y' = (3x)' \cdot dx \, \, \, \Longrightarrow \, \, \, dy = 3\, dx \, \, \, \Longrightarrow \, \, \, dx = \frac{dy}{3}$$
A questo punto, possiamo riscrivere l'integrale iniziale in funzione della nuova variabile $y$:
$$\int_{1}^{4}e^{3x}\, dx = \int_{3}^{12} e^y\, \frac{dy}{3} = \frac{1}{3} \int_{3}^{12} e^y\, dy$$
A questo punto, essendoci ricondotti a un integrale immediato, possiamo facilmente calcolare il tutto:
$$\frac{1}{3}\int_{3}^{12} e^y\, dy = \frac{1}{3} \cdot e^y\, |_{3}^{12} = \frac{1}{3} \cdot e^{3x}\, |_{1}^{4} = \frac{e^{12} - e^3}{3}$$
___
### Integrazione per parti

Un metodo per calcolare integrali più complessi è quello della cosiddetta "**integrazione per parti**". Per applicare l'integrazione per parti, ricordiamo l'equazione che descrive la **derivazione di un prodotto di due funzioni $f(x)$ e $g(x)$**:
$$[f(x) \cdot g(x)]' = f'(x)g(x) + f(x)g'(x)$$
Avendo quest'uguaglianza, possiamo integrare entrambi i membri:
$$\int [f(x) \cdot g(x)]'\, dx = \int f'(x)g(x) + f(x)g'(x)\, dx$$
A questo punto, notiamo che nel primo membro dell'equazione si effettua l'integrazione di una derivazione: essendo queste operazioni matematicamente inverse, si "annullano" e restituiscono il prodotto originale tra le due funzioni:
$$\begin{align} \int [f(x) \cdot g(x)]'\, dx = \int f'(x)g(x) + f(x)g'(x)\, dx \, \, \, &\Longrightarrow \, \, \, f(x) \cdot g(x) = \int f'(x)g(x) + f(x)g'(x)\, dx \\ &\Longrightarrow \, \, \, f(x) \cdot g(x) = \int f'(x)g(x)\, dx + \int f(x)g'(x)\, dx \\ &\Longrightarrow \int f'(x)g(x)\, dx = f(x) \cdot g(x) - \int f(x)g'(x)\, dx \end{align}$$
> Se il prodotto tra funzioni $f'(x)g(x)$ è integrabile, allora si ha che:
> $$\int f'(x)g(x)\, dx = f(x) \cdot g(x) - \int f(x)g'(x)\, dx$$

Per comprendere meglio come applicare questo metodo, consideriamo il seguente esempio:
$$\int x^3e^{x^2}\, dx$$
Inizialmente, proviamo ad applicare l'[[CI_04 - Integrali#Integrazione per sostituzione|integrazione per sostituzione]], ponendo $y = x^2$ e di conseguenza $\frac{dy}{2} = x\,dx$:
$$\int x^3e^{x^2}\, dx = \int x^2 \cdot e^{x^2} \cdot x\, dx = \int ye^y\, \frac{dy}{2} = \frac{1}{2} \int ye^y\, dy$$
Notiamo che non è bastato questo metodo per ricondurci a un integrale immediato, tuttavia ha sicuramente reso più semplice l'integrale di partenza. A questo punto, applichiamo l'integrazione per parti.

Per fare ciò, bisogna individuare all'interno dell'integrale le funzioni che svolgeranno i ruoli di $f'(x)$ e di $g(x)$: in questo caso, scegliamo $f'(x) = e^y$ e $g(x) = y$. Tramite integrazione, si ottiene quindi che $f(x) = e^y$, mentre tramite derivazione si ottiene che $g'(x) = 1$. Procediamo, ora, applicando la formula dell'integrazione per parti:
$$\frac{1}{2} \int ye^y\, dy = \frac{1}{2} \left(ye^y - \int e^y\, dy \right) = \frac{ye^y - e^y}{2} + c = \frac{x^2e^{x^2} - e^{x^2}}{2} + c$$
L'integrazione per parti è uno strumento molto potente per il calcolo di integrali più complessi, ma presenta una certa difficoltà nella scelta iniziale di $f'(x)$ e di $g(x)$: se non si individuano queste due funzioni in maniera efficiente, infatti, si andrà solo a complicare il tutto e l'integrazione per parti non porterà effettivamente a niente (ad esempio, se nell'integrale precedente si fossero scelte $f'(x) = y$ e $g(x) = e^y$ l'integrale sarebbe diventato ancora più complesso).
___
### Integrazione di $P_{n}(x) \cdot e^x$

Consideriamo il seguente integrale:
$$\int P_{n}(x) \cdot e^x\, dx$$
dove $P_{n}(x)$ è un polinomio di grado $n$. Applicando la formula della derivazione di un prodotto tra funzioni, sappiamo che per un qualsiasi polinomio $Q_{n}(x)$ si ha che:
$$[Q_{n}(x) \cdot e^x]' = Q'_{n}(x)e^x + Q_{n}(x)e^x = e^x(Q'_{n}(x) + Q_{n}(x))$$
Possiamo porre, a questo punto, il polinomio $P_{n}(x)$ come pari alla somma di polinomi appena ottenuta ($P_{n}(x) = Q'_{n}(x) + Q_{n}(x)$). Posta questa condizione, si può affermare che:
$$\int P_{n}(x) \cdot e^x\, dx = \int [Q_{n}(x) \cdot e^x]'\, dx = Q_{n}(x) \cdot e^x + c$$
Avendo queste uguaglianze, è possibile ricavare $Q_{n}(x)$ risolvendo un **sistema di equazioni**. Per comprendere meglio questo procedimento, consideriamo il seguente esempio:
$$\int (x^3 - 3x^2 + 8x - 11)e^x\, dx$$
In questo caso, si ha che $P_{3}(x) = x^3 - 3x^2 + 8x - 11$, e quindi che:
$$x^3 - 3x^2 + 8x - 11 = Q_{3}(x) + Q'_{3}(x)$$
Essendo $Q_{3}(x)$ un generico polinomio di terzo grado, esso è rappresentabile come $Q_{3}(x) = \alpha x^3 + \beta x^2 + \gamma x + \delta$. Ne segue, quindi, che $Q'_{3}(x) = 3\alpha x^2 + 2\beta x + \gamma$. A questo punto, è possibile riscrivere l'equazione appena esplicitata come:
$$\begin{align} x^3 - 3x^2 + 8x - 11 &= Q_{3}(x) + Q'_{3}(x) \\ &=  (\alpha x^3 + \beta x^2 + \gamma x + \delta) +  (3\alpha x^2 + 2\beta x + \gamma) \\ &= \alpha x^3 + (3\alpha + \beta)x^2 + (2\beta + \gamma)x + \gamma + \delta \end{align}$$
Ora, confrontando membro a membro i termini aventi il medesimo grado, otterremo un sistema di equazioni che ci permetterà di trovare il valore dei vari coefficienti, in modo da poterli inserire nel polinomio generico $Q_{3}(x)$ e trovare quindi la soluzione dell'integrale:
$$\begin{cases} x^3 = \alpha x^3 \\ -3x^2 = (3\alpha + \beta)x^2 \\ 8x = (2\beta + \gamma)x \\ -11 = \gamma + \delta \end{cases} \, \, \, \, \, \Longrightarrow \, \, \, \, \, \begin{cases} \alpha = 1 \\ \beta = -6 \\ \gamma = 20 \\ \delta = -31 \end{cases}$$
Di conseguenza, il polinomio $Q_{3}(x)$ sarà:
$$Q_{3}(x) = x^3 - 6x^2 + 20x - 31$$
e quindi concludiamo che:
$$\int (x^3 - 3x^2 + 8x - 11)e^x\, dx = (x^3 - 6x^2 + 20x - 31)e^x + c$$

> Per risolvere un integrale del tipo:
> $$\int P_{n}(x) \cdot e^x\, dx$$
> - porre $P_{n}(x) = Q_{n}(x) + Q'_{n}(x)$;
> - individuare $n$, e in base ad esso riscrivere $Q_{n}(x)$ come polinomio generico di grado $n$ e $Q'_{n}(x)$ come derivata di tale polinomio;
> - confrontare membro a membro i termini dell'equazione aventi medesimo grado in un sistema di equazioni;
> - ricavare i coefficienti del polinomio $Q_{n}(x)$ e sostituirli al suo interno;
> - la soluzione dell'integrale iniziale sarà $Q_{n}(x) \cdot e^x + c$.
___
### Integrazione di $\sin^kx$ e di $\cos^kx$

In generale:

> Avendo un integrale di uno dei seguenti tipi:
> $$\int \sin^kx\, dx \, \, \, \, \, \, \, \, \, \, \, \, \, \, \, \, \, \, \, \, \int \cos^kx\, dx$$
> dove $k$ è una qualsiasi costante intera e positiva:
> - se $k$ è **dispari**, è consigliato risolvere l'integrale utilizzando l'**integrazione per sostituzione**;
> - se $k$ è **pari**, è consigliato risolvere l'integrale utilizzando l'**integrazione per parti**.

Vediamo alcuni esempi per comprendere meglio questo approccio. Consideriamo il seguente integrale, in cui $k$ è **dispari**:
$$\int \sin^5x\, dx$$
Possiamo riscrivere l'integrale come:
$$\int \sin^5x\, dx = \int \sin^4x \cdot \sin x\, dx = \int (\sin^2x)^2 \cdot \sin x\, dx$$
Ricordando l'identità trigonometrica fondamentale, ossia $\sin^2x + \cos^2x = 1$, è possibile riscrivere nuovamente l'integrale come:
$$\int (\sin^2x)^2 \cdot \sin x\, dx = \int (1 - \cos^2x)^2 \cdot \sin x\, dx$$
A questo punto, possiamo applicare l'**integrazione per sostituzione**, ponendo $y = \cos x$ e, di conseguenza, $dy = -\sin x\, dx$. Sostituendo il tutto all'interno del nostro integrale, si ottiene che:
$$\int (1 - \cos^2x)^2 \cdot \sin x\, dx = - \int (1 - y^2)^2\, dy = - \int (1 - 2y^2 + y^4)\, dy$$
In questo modo, abbiamo ricondotto l'integrale iniziale all'integrale di un polinomio, molto semplice da risolvere scomponendo l'integrale in una somma di integrali:
$$\begin{align} - \int (1 - 2y^2 + y^4)\, dy &= - \left(\int 1\, dy - \int 2y^2\, dy + \int y^4\, dy \right) \\ &= - \left( y - \frac{2}{3}y^3 + \frac{1}{5}y^5 \right) + c \\ &= -y + \frac{2}{3}y^3 - \frac{1}{5}y^5 + c \\ &= -\cos x + \frac{2}{3} \cos^3x - \frac{1}{5}\cos^5x + c \end{align}$$
Ora, consideriamo un nuovo esempio, stavolta in cui $k$ è **pari**:
$$\int \sin^4x\, dx$$
Possiamo riscrivere l'integrale come:
$$\int \sin^4x\, dx = \int \sin^3x \cdot \sin x\, dx$$
A questo punto, possiamo applicare l'**integrazione per parti**, ponendo $f'(x) = \sin x$ e $g(x) = \sin^3x$, e ottenendo di conseguenza che $f(x) = - \cos x$ e che $g'(x) = 3\sin^2x\cos x$:
$$\int \sin^3x \cdot \sin x\, dx = - \cos x\sin^3x + 3 \int \cos^2x\sin^2x\, dx$$
Ricordando l'identità trigonometrica fondamentale, possiamo riscrivere l'integrale come:
$$\begin{align} \int \sin^4x\, dx &= - \cos x\sin^3x + 3 \int \cos^2x\sin^2x\, dx \\ &= -\cos x \sin^3x + 3 \int (1 - \sin^2x)\sin^2x\, dx \\ &= - \cos x\sin^3x + 3 \int \sin^2x\, dx - 3\int \sin^4x\, dx \end{align}$$
Notiamo a questo punto che l'integrazione per parti ha portato in realtà al ritorno all'integrale iniziale: tuttavia, proprio perché ciò che abbiamo ottenuto coincide con quest'ultimo, possiamo spostare il termine appena trovato al primo membro, e ottenere così una formulazione dell'integrale iniziale che risulta effettivamente semplificata:
$$\int \sin^4x\, dx = - \cos z \sin^3x + 3 \int \sin^2x\, dx - 3 \int \sin^4x\, dx \, \, \, \Longrightarrow \, \, \, \int \sin^4x\, dx = \frac{1}{4} \left(-\cos x \sin^3x + 3 \int \sin^2x\, dx \right)$$
A questo punto, si potrà semplificare anche l'integrale di $\sin^2x$ in modo perfettamente analogo al procedimento compiuto finora, arrivando alla soluzione:
$$\frac{1}{4} \left(-\cos x \sin^3x + 3 \int \sin^2x\, dx \right) = \frac{-2\sin^3x \cos x - 3\sin x \cos x + 3x}{8}$$
___
### Integrazione di funzioni razionali

L'integrazione di **funzioni razionali**, ossia la risoluzione di integrali del tipo:
$$\int \frac{P(x)}{Q(x)}\, dx$$
dove $P(x)$ e $Q(x)$ sono due polinomi generici in $x$ (principalmente di grado $0$, $1$ o $2$), risulta essere relativamente articolata e complessa, e prevede diversi approcci in base alla forma che assumono i due polinomi.

Il primo caso che analizzeremo è quello in cui il polinomio $P(x)$ è una **costante**, mentre il polinomio $Q(x)$ è un **polinomio di 1° grado**. In queste condizioni, l'integrale si presenta nella seguente forma:
$$\int \frac{\beta}{\gamma x + \delta}\, dx$$
In questo caso, per risolvere l'integrale si può portare fuori la costante moltiplicativa $\beta$, e applicare quindi l'[[CI_04 - Integrali#Integrazione per sostituzione|integrazione per sostituzione]], ponendo $y = \gamma x + \delta$ e, di conseguenza, $\frac{dy}{\gamma} = dx$:
$$\int \frac{\beta}{\gamma x + \delta}\, dx = \beta \int \frac{1}{\gamma x + \delta}\, dx = \beta \int \frac{1}{y}\, \frac{dy}{\gamma} = \frac{\beta}{\gamma} \int \frac{1}{y}\, dy$$
Ci siamo ricondotti, così, a un [[CI_04 - Integrali#Integrali immediati|integrale immediato]], che possiamo facilmente risolvere:
$$\frac{\beta}{\gamma} \int \frac{1}{y}\, dy = \frac{\beta}{\gamma}\, \ln |y| = \frac{\beta}{\gamma}\, \ln(|\gamma x + \delta|)$$
Concludiamo, così, che:
> $$\int \frac{\beta}{\gamma x + \delta}\, dx = \frac{\beta}{\gamma}\, \ln (|\gamma x + \delta|)$$

Il secondo caso che analizzeremo è quello in cui il polinomio $P(x)$ è una **costante**, mentre il polinomio $Q(x)$ è un **quadrato**. In queste condizioni, l'integrale si presenta nella seguente forma:
$$\int \frac{\beta}{f(x)^2}\, dx$$
In questo caso, per risolvere l'integrale si può portare fuori la costante moltiplicativa $\beta$, e riformulare l'integrale per favorire l'applicazione di un [[CI_04 - Integrali#Integrali immediati di funzioni composte|integrale immediato di funzione composta]]:
$$\int \frac{\beta}{f(x)^2}\, dx = \beta \int \frac{1}{f(x)^2}\, dx = \beta \int f(x)^{-2}\, dx$$
Per poter applicare quest'ultimo, è importante far figurare $f'(x)$, moltiplicando e dividendo per le costanti opportune. Quindi:
$$\beta \int f(x)^{-2}\, dx = \frac{\beta}{f'(x)} \int f'(x) \cdot f(x)^{-2}\, dx = \frac{\beta}{f'(x)} \cdot \frac{f(x)^{-1}}{-1} + c$$
Concludiamo, così, che:
> $$\int \frac{\beta}{f(x)^2}\, dx = - \frac{\beta}{f'(x) \cdot f(x)} + c$$

Il terzo caso che analizzeremo è quello in cui il polinomio $P(x)$ è un **polinomio di 1° grado**, mentre il polinomio $Q(x)$ è un **polinomio di 2° grado con $\Delta < 0$**. In queste condizioni, l'integrale si presenta nella seguente forma:
$$\int \frac{\alpha x + \beta}{\gamma x^2 + \delta x + \epsilon}\, dx \, \, \, \, \, \, \, \, \, \, \text{con } \Delta = \delta^2 - 4\gamma \epsilon < 0$$
In questo caso, per risolvere l'integrale l'obiettivo diventa effettuare delle varie "riformulazioni" dell'integrale (suddividerlo in somma di più integrali, moltiplicare e dividere per costanti, sommare e sottrarre costanti per isolare quadrati, ecc. ecc.) in modo da ricondursi a integrali del tipo $\int \frac{f'(x)}{1 + f(x)^2}dx$ o del tipo $\int \frac{f'(x)}{f(x)}dx$.

> Se l'integrale da risolvere non rientra in nessuno di questi casi particolari, si andrà ad utilizzare un quarto procedimento più generico, composto dai seguenti passaggi:
> - se il grado di $P(x)$ è maggiore o uguale al grado di $Q(x)$, effettuare una **divisione polinomiale di $P(x)$ per $Q(x)$**;
> - **fattorizzare $Q(x)$**, ossia scomporlo in un prodotto di fattori di 1° o di 2° grado non ulteriormente scomponibili (per farlo, alcuni metodi utili possono essere la scomposizione di Ruffini, la regola somma-prodotto, o anche direttamente la risoluzione dell'equazione associata);
> - **scomporre** la frazione ottenuta in dei cosiddetti "**fratti semplici**";
> - **integrare i fratti semplici** ottenuti.

Per comprendere meglio come funziona questo procedimento, consideriamo come esempio il seguente integrale:
$$\int \frac{x^3 - 3x -1}{x^2 - x - 2}\, dx$$
Notiamo subito che il grado di $P(x)$ è maggiore del grado di $Q(x)$, quindi dovremo effettuare la divisione tra $P(x)$ e $Q(x)$. Essa darà come risultato il polinomio $x + 1$ e come resto $1$, dunque potremo riscrivere l'integrale come:
$$\begin{align} \int \frac{x^3 - 3x -1}{x^2 - x - 2}\, dx &= \int \frac{(x^2 - x - 2)(x + 1) + 1}{x^2 - x - 2}\, dx \\ &= \int \frac{(x^2 - x - 2)(x + 1)}{x^2 - x - 2} + \frac{1}{x^2 - x - 2}\, dx \\ &= \int x + 1 + \frac{1}{x^2 - x - 2}\, dx \end{align}$$
A questo punto, passiamo al secondo passaggio, ossia alla fattorizzazione di $Q(x)$. Utilizziamo, per questo esempio, la regola somma-prodotto, e cerchiamo quindi due numeri il cui prodotto sia uguale a $-2$ e la cui somma sia uguale a $-1$: due numeri che rispettano queste condizioni sono $-2$ e $1$, quindi possiamo riscrivere $Q(x)$ come:
$$\int x + 1 + \frac{1}{x^2 - x - 2}\, dx = \int x + 1 + \frac{1}{(x - 2)(x + 1)}\, dx$$
Passiamo, quindi, al terzo passaggio, ossia alla scomposizione della frazione ottenuta nei cosiddetti "fratti semplici". In questo caso, vogliamo effettuare la seguente scomposizione:
$$\frac{1}{(x - 2)(x + 1)} = \frac{A}{x - 2} + \frac{B}{x + 1} = \frac{(Ax + A) + (Bx - 2B)}{(x - 2)(x + 1)} = \frac{(A + B)x + (A - 2B)}{(x - 2)(x + 1)}$$
e trovare quindi due costanti $A$ e $B$ per cui sia vera tale uguaglianza. Similmente al metodo che si è utilizzato per l'integrazione di $P_{n}(x) \cdot e^x$, per ottenere il valore di $A$ e $B$ si dovrà risolvere un sistema di equazioni in cui ogni membro è un'uguaglianza tra i coefficienti dei termini di medesimo grado della frazione di partenza e di quella ottenuta. In questo caso:
$$\begin{cases} 0 = A + B \\ 1 = A - 2B \end{cases} \, \, \, \, \, \Rightarrow \, \, \, \, \, \begin{cases} A = -B \\ 1 = -3B \end{cases} \, \, \, \, \, \Rightarrow \, \, \, \, \, \begin{cases} A = \frac{1}{3} \\ B = -\frac{1}{3} \end{cases}$$
Avendo trovato dei valori di $A$ e di $B$ per cui viene rispettata l'uguaglianza iniziale, possiamo quindi affermare che:
$$\frac{1}{(x - 2)(x + 1)} = \left(\frac{1}{3} \cdot \frac{1}{x - 2} \right) - \left(\frac{1}{3} \cdot \frac{1}{x + 1} \right)$$
Sostituendo nell'integrale, si ottiene che:
$$\int x + 1 + \frac{1}{(x - 2)(x + 1)}\, dx = \int x + 1 + \frac{1}{3} \cdot \frac{1}{x - 2} - \frac{1}{3} \cdot \frac{1}{x + 1}\, dx$$
Infine, ci rimane solo l'ultimo passaggio, ossia suddividere l'integrale in somma di più integrali e risolvere ognuno di essi:
$$\begin{align} \int x + 1 + \frac{1}{3} \cdot \frac{1}{x - 2} - \frac{1}{3} \cdot \frac{1}{x + 1}\, dx &= \int x\, dx + \int 1\, dx + \frac{1}{3} \int \frac{1}{x - 2}\,dx - \frac{1}{3} \int \frac{1}{x + 1}\, dx \\ &= \frac{x^2}{2} + x + \frac{1}{3}(\ln |x - 2|) - \frac{1}{3}(\ln |x + 1|) + c \\ &= \frac{x^2}{2} + x + \frac{1}{3}\ln \left|\frac{x - 2}{x + 1} \right| + c \end{align}$$
L'esempio che abbiamo appena visto era abbastanza elementare, dato che permetteva una completa fattorizzazione di $Q(x)$ in termini di 1° grado. Ma cosa succederebbe se avessimo, in seguito alla fattorizzazione, termini di **2° grado** non ulteriormente scomponibili? Per scoprirlo, consideriamo un nuovo esempio:
$$\int \frac{1}{x^3 + x}\, dx$$
Procediamo con i medesimi passaggi dell'esempio precedente. Prima di tutto, confrontiamo il grado di $P(x)$ e di $Q(x)$: il primo ha grado minore del secondo, dunque si può omettere il primo passaggio. A questo punto, andiamo a fattorizzare $Q(x)$ raccogliendo la $x$:
$$\int \frac{1}{x^3 + x}\, dx = \int \frac{1}{x(x^2 + 1)}\, dx$$
Il termine $x^2 + 1$ non è ulteriormente scomponibile, dunque si dovrà procedere al terzo passaggio con questi termini. In questo caso, la scomposizione in fratti semplici subisce una leggera variazione: per la frazione con denominatore $x$ vale il medesimo approccio usato in precedenza, essendo di 1° grado, ma per la frazione con denominatore $x^2 + 1$ si inserirà come numeratore un **polinomio generico di 1° grado**:
$$\frac{1}{x(x^2 + 1)} = \frac{A}{x} + \frac{Bx + C}{x^2 + 1} = \frac{Ax^2 + A + Bx^2 + Cx}{x(x^2 + 1)} = \frac{(A + B)x^2 + Cx + A}{x(x^2 + 1)}$$
A questo punto, impostiamo il sistema di equazioni per trovare i vari coefficienti:
$$\begin{cases} 0 = A + B \\ 0 = C \\ 1 = A \end{cases} \, \, \, \, \, \Rightarrow \, \, \, \, \, \begin{cases} A = 1 \\ B = -1 \\ C = 0 \end{cases}$$
Si ha, di conseguenza, che:
$$\int \frac{1}{x(x^2 + 1)}\, dx = \int \frac{1}{x}\, dx - \int \frac{x}{x^2 + 1}\, dx$$
Il primo dei due integrali ottenuti è immediato, mentre possiamo riformulare il secondo, moltiplicando e dividendo per $2$, in un integrale del tipo $\int \frac{f'(x)}{f(x)} dx$:
$$\begin{align} \int \frac{1}{x}\, dx - \int \frac{x}{x^2 + 1}\, dx &= \ln |x| - \frac{1}{2}\int \frac{2x}{x^2 + 1}\, dx \\ &= \ln |x| - \frac{1}{2} \ln |x^2 + 1| + c \\ &= \ln |x| - \ln \sqrt{x^2 + 1} + c \\ &= \ln \left|\frac{x}{\sqrt{x^2 + 1}} \right| + c \end{align}$$
Un altro caso particolare è quello in cui, nella fattorizzazione di $Q(x)$, si incappi in un quadrato. Ad esempio, consideriamo il seguente integrale:
$$\int \frac{x + 1}{x^3 + 2x^2 + x}\, dx$$
Anche in questo esempio, si può omettere il primo passaggio in quanto il grado di $P(x)$ è minore del grado di $Q(x)$. Passiamo, quindi, alla fattorizzazione di quest'ultimo:
$$\int \frac{x + 1}{x^3 + 2x^2 + x}\, dx = \int \frac{x + 1}{x(x - 1)^2}\, dx$$
Ora, nella scomposizione in fratti semplici, il quadrato va gestito in maniera peculiare: invece di considerare il termine $(x - 1)^2$ in un'unica frazione, si andranno a creare due frazioni, la prima che per denominatore avrà solo il polinomio privo di esponente, ossia $x - 1$, la seconda che invece avrà per denominatore il quadrato stesso. Per quanto riguarda i numeratori, entrambi saranno costanti generiche:
$$\frac{x + 1}{x(x - 1)^2} = \frac{A}{x} + \frac{B}{x - 1} + \frac{C}{(x - 1)^2} = \frac{(A + B)x^2 + (C - 2A - B)x + A}{x(x - 1)^2}$$
In generale, per un termine generico $f(x)^n$, si dovranno creare $n$ frazioni che avranno per denominatore $f(x)$ con grado crescente, da $1$ a $n$, e per numeratore ognuna una costante generica. Superato questo punto, procediamo normalmente ad impostare un sistema di equazioni per ricavare il valore dei coefficienti:
$$\begin{cases} 0 = A + B \\ 1 = C - 2A - B \\ 1 = A \end{cases} \, \, \, \, \, \Rightarrow \, \, \, \, \, \begin{cases} A = 1 \\ B = -1 \\ C = 2 \end{cases}$$
Si ha, di conseguenza, che:
$$\begin{align} \int \frac{x + 1}{x(x - 1)^2}\, dx &= \int \frac{1}{x}\, dx - \int \frac{1}{x - 1}\, dx + 2 \int \frac{1}{(x - 1)^2}\, dx \\ &= \ln|x| - \ln|x - 1| + 2\,  \frac{(x - 1)^{-1}}{-1} + c \\ &= \ln|x| - \ln|x - 1| - \frac{2}{x - 1} + c \\ &= \ln \left|\frac{x}{x - 1} \right| - \frac{2}{x - 1} + c \end{align}$$
___
### Studio di funzioni definite tramite integrali

[pag. 87 - 88 - 89]
___
### Integrali impropri

> Un "**integrale improprio**", detto anche "integrale generalizzato", è un integrale in cui la funzione integranda, l'intervallo di integrazione o entrambi sono **illimitati**.

Vediamo, innanzitutto, cosa succede se **la funzione integranda è illimitata**. Supponiamo di avere una funzione continua $f(x)$, e di considerarla su un intervallo $[a, b)$ per cui essa risulti illimitata a sinistra di $b$ (quindi, si avrebbe che $\lim_{x \to b^-} f(x) = \pm \infty$). In questo caso, se volessimo integrare $f(x)$ nell'intervallo $[a, b]$, si risulterebbe in un integrale improprio della seguente forma:
$$\int_{a}^{b} f(x)\, dx = \lim_{\epsilon \to 0} \int_{a}^{b - \epsilon}f(x)\, dx$$
dove $\epsilon$ è una quantità piccola arbitraria. L'idea, dunque, è di **risolvere prima un integrale "proprio"**, ossia in cui sia l'intervallo di integrazione che la funzione integranda in tale intervallo sono limitati, nell'intervallo $[a, b - \epsilon]$, e poi di far tendere il valore di $\epsilon$ a 0 in modo da ottenere il risultato effettivo dell'integrale che si stava cercando.

Lo stesso discorso vale per l'altro estremo di integrazione $a$. Supponendo che la funzione $f(x)$ risulti illimitata a destra di $a$ (quindi, si avrebbe che $\lim_{x \to a^+} f(x) = \pm \infty$), l'integrazione di tale funzione risulterebbe nel seguente integrale improprio:
$$\int_{a}^{b} f(x)\, dx = \lim_{\epsilon \to 0} \int_{a + \epsilon}^{b} f(x)\, dx$$
> In un integrale definito, se la **funzione integranda $f(x)$** risulta essere **illimitata** in prossimità di uno o entrambi gli estremi dell'intervallo di integrazione $[a, b]$, allora la risoluzione di tale integrale sarà data da uno dei seguenti integrali impropri:
> $$\lim_{\epsilon \to 0} \int_{a}^{b - \epsilon} f(x)\, dx \, \, \, \, \, \, \, \, \, \, \, \, \, \, \, \, \, \, \, \, \lim_{\epsilon \to 0} \int_{a + \epsilon}^{b} f(x)\, dx \, \, \, \, \, \, \, \, \, \, \, \, \, \, \, \, \, \, \, \, \lim_{\epsilon \to 0} \int_{a + \epsilon}^{b - \epsilon} f(x)\, dx$$
> in base a in prossimità a quali estremi la funzione risulti essere illimitata. A seconda del risultato del limite, si ha che:
> - se il limite **esiste ed è finito**, allora si dice che l'integrale **converge** e che $f(x)$ è "**integrabile in senso improprio**";
> - se il limite **esiste ed è pari a $\pm \infty$**, allora si dice che l'integrale **diverge**;
> - se il limite **non esiste**, allora si dice che l'integrale è **indeterminato**.

Vediamo, ora, cosa succede se **l'intervallo di integrazione è illimitato**. Supponiamo di voler integrare una funzione continua $f(x)$, e di volerla integrare sull'intervallo illimitato $[a, +\infty)$. In questo caso, si dovrebbe andare a risolvere il seguente integrale improprio:
$$\int_{a}^{+\infty} f(x)\, dx = \lim_{M \to +\infty} \int_{a}^{M} f(x)\, dx$$
Per quanto riguarda la risoluzione concreta di tale integrale, si sfrutta lo stesso procedimento esplicitato prima, che contempla prima il calcolo dell'integrale proprio e poi lo svolgimento del limite. Inoltre, anche in questo caso il discorso non cambia se l'intervallo è illimitato nell'altro senso, ossia avendo $(-\infty, b]$. Infatti:
$$\int_{-\infty}^{b} f(x)\, dx = \lim_{M \to -\infty} \int_{M}^{b} f(x)\, dx$$
> In un integrale definito, se l'**intervallo di integrazione** risulta essere **illimitato** in un verso, allora la risoluzione di tale integrale sarà data da uno dei seguenti integrali impropri:
> $$\lim_{M \to +\infty} \int_{a}^{M} f(x)\, dx \, \, \, \, \, \, \, \, \, \, \, \, \, \, \, \, \, \, \, \, \lim_{M \to -\infty} \int_{M}^{b} f(x)\, dx$$
> in base a quale degli estremi dell'intervallo di integrazione sia pari a $\infty$. A seconda del risultato del limite, valgono le stesse distinzioni fatte per gli integrali impropri con funzione integranda illimitata.
>
> Nel caso in cui l'intervallo di integrazione risulti essere **illimitato in entrambi i versi**, ossia $(-\infty, +\infty)$, conviene scegliere un determinato valore di "separazione" ed applicare la proprietà dell'[[CI_04 - Integrali#Proprietà degli integrali|additività di un integrale]]:
> $$\int_{-\infty}^{+\infty} f(x)\, dx = \int_{-\infty}^{a} f(x)\, dx + \int_{a}^{+\infty} f(x)\, dx$$

Ma come risolvere un integrale in cui **sia l'intervallo di integrazione sia la funzione integranda sono illimitati**? Similmente all'approccio utilizzato per l'integrazione in un intervallo illimitato in entrambi i versi, conviene sfruttare l'additività dell'integrale e ricondursi a una somma di integrali in cui ognuno di essi presenta una sola "particolarità", sia essa un estremo di integrazione divergente o un estremo di integrazione in prossimità del quale è la funzione integranda a divergere.

Potrebbe essere utile, a questo punto, approfondire dei **criteri di convergenza** per gli integrali impropri, per capire se uno di essi converge o meno senza doverlo necessariamente risolvere, processo spesso tedioso o molto più difficile. I criteri di convergenza che analizzeremo sono i seguenti:
- criterio del **confronto**;
- criterio del **confronto asintotico**.

> Il **criterio del confronto** afferma che, siano $f(x)$ e $g(x)$ due funzioni continue, tali per cui $0 \le f(x) \le g(x)$ nell'intervallo $[a, +\infty)$, allora:
> $$\text{se } \int_{a}^{+\infty}g(x)\, dx \text{ converge, allora anche } \int_{a}^{+\infty} f(x)\, dx \text{ converge}$$$$\text{se } \int_{a}^{+\infty}f(x)\, dx \text{ diverge, allora anche } \int_{a}^{+\infty} g(x)\, dx \text{ diverge}$$

> Il **criterio del confronto asintotico** afferma che, siano $f(x)$ e $g(x)$ due funzioni continue, tali per cui $f(x) \sim g(x)$ per $x \to +\infty$, ossia tali per cui $\lim_{x \to +\infty}f(x) = \lim_{x \to +\infty}g(x)$, allora:
> $$\int_{a}^{+\infty}f(x)\, dx \text{ converge/diverge a } +\infty \iff \int_{a}^{+\infty}g(x)\, dx \text{ converge/diverge a } +\infty$$

Di seguito, infine, il comportamento di alcuni **integrali impropri "notevoli"**. Il seguente integrale improprio:
$$\int_{a}^{+\infty} \frac{1}{x^\alpha}\, dx$$
per $a > 0$:
- se $\alpha > 1$, **converge**;
- se $\alpha \le 1$, **diverge a $+\infty$**.

Il seguente integrale improprio:
$$\int_{a}^{+\infty} \frac{1}{x^\alpha \ln^\beta x}\, dx$$
per $a > 1$:
- se $\alpha > 1$, oppure se $\alpha = 1$ e $\beta > 1$, **converge**;
- se $\alpha < 1$, oppure se $\alpha = 1$ e $\beta \le 1$, **diverge a $+\infty$**.

Il seguente integrale improprio:
$$\int_{a}^{b} \frac{1}{(x - a)^\alpha}\, dx$$
- se $\alpha < 1$, **converge**;
- se $\alpha \ge 1$, **diverge**.
___
### Criteri di convergenza degli integrali

[pag. 95 - 96 - 97]
___