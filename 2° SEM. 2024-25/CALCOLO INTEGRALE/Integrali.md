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
> $$\int_{a}^{b} [\alpha f(x) + \beta g(x)]\,dx = \alpha \int_{a}^{b}f(x)\,dx + \int_{a}^{b} g(x)\, dx$$

> La proprietà dell'**additività** di un integrale afferma che, sia $[a, b] = [a, c] \cup [c, b]$, dove $c \in [a, b]$, e sia $f$ una funzione integrabile in $[a, c]$ e in $[c, b]$, allora $f$ sarà integrabile anche in $[a, b]$ e il suo integrale in tale intervallo equivale alla somma tra l'integrale in $[a, c]$ e quello in $[c, b]$:
> $$\int_{a}^{b} f(x)\, dx = \int_{a}^{c} f(x)\, dx + \int_{c}^{b} f(x)\, dx$$

Quest'ultima proprietà ci permette di fare delle assunzioni aggiuntive, ad esempio in relazione alla definizione di **funzione integrabile** che è stata fornita a inizio paragrafo: supponendo, infatti, di avere una funzione non integrabile, e dunque discontinua e non monotona, in un intervallo $[a, b]$, per calcolarne l'integrale in tale intervallo sarà sufficiente **scomporre l'integrale in vari integrali su sotto-intervalli** dell'intervallo iniziale, in modo da avere un frammento di funzione monotono o continuo in ognuno di questi sotto-intervalli. Possiamo, quindi, affermare che:

> Una funzione $f$ è **integrabile** in un intervallo $[a, b]$ se all'interno di tale intervallo presenta un **numero finito di cambi di monotonia** e un **numero finito di discontinuità**.

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

La funzione $F(x)$ definita dal [[Integrali#Teorema fondamentale del calcolo integrale|teorema fondamentale del calcolo integrale]] viene detta "**primitiva di $f(x)$**" e, per ogni funzione $f(x)$, ne esistono **infinite**: infatti, se $F(x)$ è una primitiva di $f(x)$ allora una qualsiasi funzione $G(x) = F(x) + c$, per qualsiasi costante $c \in \mathbb{R}$, è anch'essa una primitiva di $f(x)$.

> Sia $f(x)$ una funzione integrabile, allora esistono **infinite funzioni primitive $G(x)$**, tali per cui $G'(x) = f(x)$, con $G(x) = F(x) + c$ per ogni $c \in \mathbb{R}$.

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
$$\int e^{\alpha x}\, dx = \frac{e^{\alpha x}}{x} + c$$
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
- l'integrale di $\frac{f'(x)}{f(x)}$, indipendentemente dalla funzione $f(x)$, è pari a:
$$\int \frac{f'(x)}{f(x)}\, dx = \ln(|f(x)|) + c$$
- l'integrale di $e^{\alpha x} \cdot \cos(\beta x)$ è pari a:
$$\int e^{\alpha x} \cdot \cos(\beta x)\, dx = \frac{e^{\alpha x}(\alpha \cos(\beta x) + \beta \sin(\beta x))}{\beta^2 + \alpha^2} + c$$
- l'integrale di $e^{\alpha x} \cdot \sin(\beta x)$ è pari a:
$$\int e^{\alpha x} \cdot \sin(\beta x) = \frac{e^{\alpha x}(\alpha \sin(\beta x) - \beta \cos(\beta x))}{\beta^2 + \alpha^2} + c$$
___
### Integrazione per sostituzione

Un metodo per calcolare gli integrali di funzioni per cui non è possibile applicare immediatamente gli [[Integrali#Integrali immediati|integrali immediati]] è la cosiddetta "**integrazione per sostituzione**". Per comprendere questo procedimento, consideriamo il seguente esempio:
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

[pag. 69 - 70 - 71 - 72]
___
### Integrazione di $P_{n}(x) \cdot e^x$

[pag. 77 - 78 - 79]
___
### Integrazione di $\sin^k(x)$ e di $\cos^k(x)$

[pag. 79 - 80 - 81]
___
### Integrazione di funzioni razionali

[pag. 81 - 82 - 83 - 84 - 85 - 86]
___
### Studio di funzioni definite tramite integrali

[pag. 87 - 88 - 89]
___
### Integrali impropri

[pag. 90 - 91 - 92 - 93 - 94]
___
### Criteri di convergenza degli integrali

[pag. 95 - 96 - 97]
___