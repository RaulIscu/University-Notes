## Cos'è la notazione asintotica?

Per valutare l'efficienza di un algoritmo, in modo da poterlo confrontare con algoritmi diversi che risolvono lo stesso problema, si misura il **costo computazionale** dello stesso, espresso principalmente in due fattori:
- **tempo di esecuzione** dell'algoritmo;
- **spazio necessario** in memoria per l'esecuzione dell'algoritmo.

Per ora, concentriamoci sul primo di questi fattori. Il metodo principale per inquadrare il tempo di esecuzione di un algoritmo è la cosiddetta "**notazione asintotica**", che viene utilizzata per stimare **quanto aumenta il tempo di esecuzione dell'algoritmo al crescere della dimensione $n$ dell'input**, ossia, in parole povere, il "**tasso di crescita**" del tempo di esecuzione. In particolare, esistono **tre notazioni asintotiche** diverse:
- la **notazione $O$**, detta anche "**limite asintotico superiore**;
- la **notazione $\Omega$**, detta anche "**limite asintotico inferiore**";
- la **notazione $\Theta$**, detta anche "**limite asintotico stretto**".

Tale forma di valutazione dell'efficienza di un algoritmo ha maggiormente senso contestualmente a input sufficientemente grandi; è per questo che, in questo contesto, si parla di "**efficienza asintotica**" di un algoritmo.
___
## Notazione $O$

> Date due funzioni $f(n)$ e $g(n)$, entrambe non negative, si dice che:
> $$f(n) \text{ è in } O(g(n))\,\,\,\,\,\,\,\,\,\,\text{oppure}\,\,\,\,\,\,\,\,\,\,f(n)=O(g(n))$$
> se esistono due costanti $c$ e $n_{0}$ tali per cui vale che:
> $$0\le f(n)\le c\cdot g(n)\,\,\,\,\,\,\,\,\,\,\text{per ogni }n\ge n_{0}$$

In altre parole, potremmo dire che in $O(g(n))$ troveremo **tutte le funzioni "dominate" da $g(n)$**.

Per comprendere meglio questo concetto, vediamo un esempio. Supponiamo di avere una funzione $f(n)=3n+3$; possiamo affermare che tale funzione si trovi in $O(n^2)$, dato che è possibile trovare due valori $c$ e $n_{0}$ (ad esempio, $c=6$ e $n_{0}=1$) tali per cui valga che $c\cdot n^2\ge 3n+3$ per ogni $n\ge n_{0}$. In realtà, più precisamente, possiamo affermare che $f(n)$ si trovi anche in $O(n)$, dato che per gli stessi due valori $c$ e $n_{0}$ vale anche che $c\cdot n\ge 3n+3$ per ogni $n\ge n_{0}$.

Generalmente, vale la seguente regola:

> Data una funzione $f(n)$, esistono infinite funzioni $g(n)$ per cui vale che $f(n)$ si trova in $O(g(n))$.

##### Dimostrazione: un polinomio di grado $m$ è in $O(n^m)$

Sia $f(n)$ un generico polinomio di grado $m$, formalizzabile nel modo seguente:
$$f(n)=\sum_{i\,=\,0}^{m}a_{i}n^i$$
con $a_{m}>0$. Si osservi, preliminarmente, che per ogni $i$ si ha che:
- o $a_{i}\ge 0$ (ciò è vero a priori per $a_{m}$);
- o $a_{i}<0$.

Di conseguenza, si può affermare che:
$$\sum_{i\,=\,0}^{m}a_{i}n^{i}\,\,\le\,\,\sum_{i\,:\,a_{i}\,\ge\, 0}^{m}a_{i}n^{i}\,\,\le\,\, n^{m}\cdot\sum_{i\,:\,a_{i}\,\ge\, 0}^{m}a_{i}$$
Ponendo $c=\sum_{i\text{ t.c. }a_{i}\ge 0}^{m}a_{i}$, e considerando solo il primo e il terzo membro della disuguaglianza, si ottiene che $f(n)\le c\cdot n^{m}$ per ogni $n$, e dunque che $f(n)$ si trova in $O(n^{m})$, come volevasi dimostrare.

In alternativa, si può dimostrare la stessa proposizione procedendo per induzione sul grado $m$. Partiamo col caso base, in cui il grado del polinomio è $m=0$: in questo caso, abbiamo che:
$$f(n)=a_{0}\cdot n^{0}=a_{o}$$
Dunque, per $m=0$, $f(n)$ è una funzione costante e di conseguenza contenuta in $O(1)$, che coincide con $O(n^{0})$. Verificato il caso base, procediamo formulando la nostra ipotesi induttiva: affermiamo che il polinomio:
$$\sum_{i\,=\,0}^{k}a_{i}n^{i}$$
è in $O(n^{k})$ per ogni $k<m$, cioè che esiste una costante $c'$ tale per cui:
$$\sum_{i\,=\,0}^{k}a_{i}n^{i}\le c'\cdot n^{k}$$
e come passo induttivo vogliamo dimostrare che ciò valga anche per $k=m$, ossia che:
$$\sum_{i\,=\,0}^{m}a_{i}n^{i}\le c'\cdot n^{m}$$
Mettendo in evidenza l'ipotesi induttiva, vediamo che $f(n)$ può essere riscritto nel modo seguente:
$$f(n)=\sum_{i\,=\,0}^{m}a_{i}n^{i}=a_{m}n^{m}+\sum_{i\,=\,0}^{k}a_{i}n^{i}$$
e proprio per l'ipotesi induttiva sappiamo che la sommatoria che abbiamo appena evidenziato è minore o uguale di $c'\cdot n^{k}$; ciò ci permette di costruire la seguente catena di disuguaglianze:
$$a_{m}n^{m}+\sum_{i\,=\,0}^{k}a_{i}n^{i}\,\le\,a_{m}n^{m}+c'\cdot n^{k}\,\le\,a_{m}n^{m}+c'\cdot n^{m}$$
che è sicuramente valida dato che $k<m$ e, di conseguenza, $n^{k}<n^{m}$. Ora, riscrivendo $a_{m}n^{m}+c'\cdot n^{m}$ come $(a_{m}+c')\cdot n^{m}$, e ponendo $c''=a_{m}+c'$, possiamo isolare il primo e il terzo termine della disuguaglianza e ottenere:
$$f(n)\le c''\cdot n^{m}$$
Abbiamo così dimostrato che un generico polinomio di grado $m$ è in $O(n^{m})$.
___
##### Alcune osservazioni utili

> **Un logaritmo è dominato da una qualunque radice**, dunque vale che:
> $$\log^{a}(n)=O(\sqrt[b]{n})\,\,\,\,\,\,\,\,\,\,\text{per ogni }a,b\ge 1$$

> **Una radice è dominata da un qualunque polinomio**, dunque vale che:
> $$\sqrt[a]{n}=O(n^{b})\,\,\,\,\,\,\,\,\,\,\text{per ogni }a,b\ge 1$$

> **Un polinomio è dominato da un qualunque esponenziale**, dunque vale che:
> $$n^{a}=O(b^{n})\,\,\,\,\,\,\,\,\,\,\text{per ogni }a,b\ge 1$$

___
## Notazione $\Omega$

> Date due funzioni $f(n)$ e $g(n)$, entrambe non negative, si dice che:
> $$f(n)\text{ è in }\Omega(g(n))\,\,\,\,\,\,\,\,\,\,\text{oppure}\,\,\,\,\,\,\,\,\,\,f(n)=\Omega(g(n))$$
> se esistono due costanti $c$ e $n_{0}$ tali per cui vale che:
> $$f(n)\ge c\cdot g(n)\,\,\,\,\,\,\,\,\,\,\text{per ogni }n\ge n_{0}$$

In altre parole, potremmo dire che in $\Omega(g(n))$ troveremo **tutte le funzioni che "dominano" $g(n)$**.

Per comprendere meglio questo concetto, vediamo un esempio. Supponiamo di avere una funzione $f(n)=2n^{2}+3$; possiamo affermare che tale funzione si trovi in $\Omega(n)$, dato che è possibile trovare due valori $c$ e $n_{0}$ (ad esempio, $c=1$ e qualsiasi $n_{0}\in\mathbb{R}$) tali per cui valga che $2n^{2}+3\ge c \cdot n$ per ogni $n\ge n_{0}$. In realtà, più precisamente, possiamo affermare che $f(n)$ si trovi anche in $\Omega(n^2)$, dato che per gli stessi due valori $c$ e $n_{0}$ vale anche che $2n^2 + 3\ge c \cdot n^2$ per ogni $n \ge n_{0}$.

Generalmente, vale la seguente regola:

> Data una funzione $f(n)$, esistono infinite funzioni $g(n)$ per cui vale che $f(n)$ si trova in $O(g(n))$.

##### Dimostrazione: un polinomio di grado $m$ è in $\Omega(n^{m})$

In modo analogo a quanto visto per il [[IAA_02 - Notazione asintotica#Notazione $O$|limite asintotico superiore]], si può dimostrare che, considerato un generico polinomio di grado $m$, scritto come:
$$f(n)=\sum_{i\,=\,0}^{m}a_{i}n^{i}$$
esso si trova in $\Omega(n^{m})$, e dunque domina la funzione $n^{m}$.
___
##### Alcune osservazioni utili

> **Una radice domina qualunque logaritmo**, dunque vale che:
> $$\sqrt[b]{n}=\Omega(\log^{a}(n))\,\,\,\,\,\,\,\,\,\,\text{per ogni }a,b\ge 1$$

> **Un polinomio domina qualunque radice**, dunque vale che:
> $$n^{b}=\Omega(\sqrt[a]{n})\,\,\,\,\,\,\,\,\,\,\text{per ogni }a,b\ge 1$$

> **Un esponenziale domina qualunque polinomio**, dunque vale che:
> $$b^{n}=\Omega(n^{a})\,\,\,\,\,\,\,\,\,\,\text{per ogni }a,b\ge 1$$

In termini più generali, considerando le osservazioni fatte finora parlando di notazione $O$ e notazione $\Omega$, possiamo formulare la seguente **scala di ordini di grandezza delle successioni numeriche**:
$$1\,≺\,\log^{a}(n)\,≺\, \sqrt[b]{n}\,≺\,n^{c}\,≺\,d^{n}\,≺\,n!\,≺\,n^{n}$$
___
## Notazione $\Theta$

Poiché i limiti asintotici servono per stimare con la maggiore precisione possibile il costo computazionale di un algoritmo, in generale si dovrebbe cercare di trovare:
- **la più piccola funzione $g(n)$** per determinare il **[[IAA_02 - Notazione asintotica#Notazione $O$|limite asintotico superiore]]** (la notazione $O$);
- **la più grande funzione $g(n)$** per determinare il **[[IAA_02 - Notazione asintotica#Notazione $ Omega$|limite asintotico inferiore]]** (la notazione $\Omega$).

Il limite asintotico più preciso possibile è una sorta di combinazione dei due precedentemente visti, e prende il nome di "**limite asintotico stretto**", indicato con la **notazione $\Theta$**.

>Date due funzioni $f(n)$ e $g(n)$, entrambe non negative, si dice che:
> $$f(n)\text{ è in }\Theta(g(n))\,\,\,\,\,\,\,\,\,\,\text{oppure}\,\,\,\,\,\,\,\,\,\,f(n)=\Theta(g(n))$$
> se esistono tre costanti $c_{1}$, $c_{2}$ e $n_{0}$ tali per cui vale che:
> $$c_{1}\cdot g(n)\le f(n)\le c_{2}\cdot g(n)\,\,\,\,\,\,\,\,\,\,\text{per ogni }n\ge n_{0}$$

In altre parole, potremmo dire che in $\Theta(g(n))$ troveremo **tutte le funzioni che "si comportano" analogamente a $g(n)$**. In $\Theta(g(n))$, si trovano **tutte le funzioni che appartengono sia a $O(g(n))$ che a $\Omega(g(n))$**.

Per comprendere meglio questo concetto, vediamo un esempio. Supponiamo di avere una funzione $f(n)=3n+3$; possiamo affermare che tale funzione si trovi in $\Theta(n)$, dato che è possibile trovare tre valori $c_{1}$, $c_{2}$ e $n_{0}$ (ad esempio, $c_{1}=1$, $c_{2} = 4$ e $n_{0}=3$) tali per cui valga che $c_{1}\cdot n\le 3n+3\le c_{2}\cdot n$ per ogni $n\ge n_{0}$.

##### Dimostrazione: un polinomio di grado $m$ è in $\Theta(n^{m})$

Dato che abbiamo già dimostrato che $n^{m}$ costituisce sia il [[IAA_02 - Notazione asintotica#Dimostrazione un polinomio di grado $m$ è in $O(n m)$|limite asintotico superiore]] che il [[IAA_02 - Notazione asintotica#Dimostrazione un polinomio di grado $m$ è in $ Omega(n {m})$|limite asintotico inferiore]] per un polinomio generico di grado $m$, possiamo affermare che tale polinomio si trovi anche in $\Theta(n^{m})$.
___
## Calcolo della notazione asintotica tramite limiti

Per calcolare i limiti asintotici di una funzione, è possibile sfruttare dei **limiti**: infatti, possiamo individuare principalmente tre regole, una relativa a ciascuna delle notazioni viste finora.

> Se si ha che:
> $$\lim_{n\, \to\, +\infty} \frac{f(n)}{g(n)} = k\,\,\,\,\,\,\,\,\,\,\text{con }k>0$$
> allora possiamo affermare che **$f(n)=\Theta(g(n))$**.

> Se si ha che:
> $$\lim_{n\, \to\, +\infty} \frac{f(n)}{g(n)} = +\infty$$
> allora possiamo affermare che $f(n)=\Omega(g(n))$ e che $f(n)\neq \Theta(g(n))$.

> Se si ha che:
> $$\lim_{n\, \to\, +\infty} \frac{f(n)}{g(n)} = 0$$
> allora possiamo affermare che $f(n)=O(g(n))$ e che $f(n)\neq \Theta(g(n))$.

Se il limite non esiste, il metodo in questione non porterà a conclusioni rilevanti e si dovrà, quindi, procedere diversamente.
___
## Algebra della notazione asintotica

Per semplificare il calcolo del costo computazionale degli algoritmi, si possono sfruttare alcune semplici regole che vanno a formare quella che potremmo definire "**algebra della notazione asintotica**". Nei seguenti paragrafi, si approfondiranno tali regole associandole anche a vari esempi.

##### Costanti moltiplicative

> Per ogni $k > 0$, se $f(n)$ è in $O(g(n))$ allora lo sarà anche $k\cdot f(n)$.

> Per ogni $k > 0$, se $f(n)$ è in $\Omega(g(n))$ allora lo sarà anche $k\cdot f(n)$.

> Per ogni $k > 0$, se $f(n)$ è in $\Theta(g(n))$ allora lo sarà anche $k\cdot f(n)$.

Informalmente, queste tre regole esprimono il fatto che, nel calcolo della notazione asintotica, **le costanti moltiplicative possono essere ignorate** (solo, però, se non si trovano all'esponente).

Possiamo **dimostrare la prima regola** (e, di conseguenza, anche le altre due) abbastanza semplicemente. Affermando che $f(n)$ è in $O(g(n))$, stiamo affermando che esistono due costanti $c$ e $n_{0}$ tali per cui vale che: $$f(n)\le c\cdot g(n)\,\,\,\,\,\,\,\,\,\,\text{per ogni }n\ge n_{0}$$Di conseguenza, possiamo affermare che lo stesso vale anche moltiplicando entrambi i membri per una certa costante $k$: $$k\cdot f(n)\le k\cdot c \cdot g(n)$$Prendendo $k\cdot c$ come nuova costante $c'$, e mantenendo lo stesso $n_{0}$, si ottiene che $k \cdot f(n)\le c'\cdot g(n)$ per ogni $n\ge n_{0}$, il che vuol dire che anche $k\cdot f(n)$ è in $O(g(n))$, come volevasi dimostrare.

Vediamo un esempio per comprendere meglio come applicare queste regole. Supponiamo di voler trovare il limite asintotico stretto per $f(n)=3n^{2}$: applicando la terza delle tre regole appena esposte, sappiamo che essa avrà lo stesso limite asintotico stretto della funzione $n^{2}$, e mediante un [[IAA_02 - Notazione asintotica#Calcolo della notazione asintotica tramite limiti|limite]] banale possiamo verificare che $f(n)=\Theta(n^{2})$.

Passiamo ad un altro esempio. Supponiamo di voler trovare il limite asintotico stretto per $f(n)=2^{n+1}$: possiamo riscrivere $2^{n+1}$ come $2\cdot 2^{n}$, evidenziando la presenza di una costante moltiplicativa che possiamo quindi ignorare; dunque, possiamo affermare che $f(n)=\Theta(2^{n})$.
___
##### Commutatività della somma

> Per ogni $f(n),\,d(n) > 0$, se $f(n)=O(g(n))$ e $d(n)=O(h(n))$ allora si ha che $f(n)+d(n)$ è in $O(g(n)+h(n))=O(max(g(n),\,h(n)))$.

> Per ogni $f(n),\,d(n) > 0$, se $f(n)=\Omega(g(n))$ e $d(n)=\Omega(h(n))$ allora si ha che $f(n)+d(n)$ è in $\Omega(g(n)+h(n))=\Omega(max(g(n),\,h(n)))$.

> Per ogni $f(n),\,d(n) > 0$, se $f(n)=\Theta(g(n))$ e $d(n)=\Theta(h(n))$ allora si ha che $f(n)+d(n)$ è in $\Theta(g(n)+h(n))=\Theta(max(g(n),\,h(n)))$.

Informalmente, queste tre regole esprimono il fatto che, nel calcolo della notazione asintotica, **data una funzione $p(n)=f(n)+g(n)$ qualsiasi suo limite asintotico è uguale al massimo tra i limiti asintotici di $f(n)$ e $g(n)$**.

Possiamo **dimostrare la prima regola** (e, di conseguenza, anche le altre due) abbastanza semplicemente. Affermando che $f(n) = O(g(n))$ e che $d(n)=O(h(n))$, stiamo affermando che esistono quattro costanti $c$, $c'$, $n_{0}$ e $n_{0}'$ tali per cui vale che: $$f(n)\le c\cdot g(n)\,\,\,\,\,\,\,\,\,\,\text{per ogni }n\ge n_{0}$$e che:$$d(n)\le c'\cdot h(n)\,\,\,\,\,\,\,\,\,\,\text{per ogni }n\ge n_{0}'$$Di conseguenza, possiamo affermare che per ogni $n\ge max(n_{0},\,n_{0}')$ la somma $f(n)+d(n)$ è necessariamente minore o uguale della somma $c\cdot g(n)+c'\cdot h(n)$, e quest'ultima è a sua volta sicuramente minore o uguale di $max(c,\,c')\cdot (g(n)+h(n))$:$$f(n)+d(n)\,\,\le\,\,c\cdot g(n)+c'\cdot h(n)\,\,\le\,\,max(c,\,c')\cdot(g(n)+h(n))$$Abbiamo dunque dimostrato che $f(n)+d(n)=O(g(n)+h(n))$. Infine, possiamo costruire la seguente disuguaglianza:
$$max(c,\,c')\cdot(g(n)+h(n))\,\le\,2\,max(c,\,c')\cdot max(g(n),\,h(n))$$
che ci permette di dimostrare che $O(g(n)+h(n))=O(max(g(n),\,h(n)))$.

Vediamo un esempio per comprendere meglio come applicare queste regole. Supponiamo di voler trovare il limite asintotico stretto per $f(n)=3n+4n^{4}$: per quanto riguarda il primo monomio, applicando prima la regola delle [[IAA_02 - Notazione asintotica#Costanti moltiplicative|costanti moltiplicative]] e poi un [[IAA_02 - Notazione asintotica#Calcolo della notazione asintotica tramite limiti|limite]], troviamo che è in $\Theta(n)$; per il secondo, seguendo lo stesso procedimento, si ottiene che è in $\Theta(n^{4})$; a questo punto, abbiamo che $f(n)=\Theta(n)+\Theta(n^{4})$. Applicando la terza delle regole appena esposte, si ottiene che $\Theta(n)+\Theta(n^{4})=\Theta(max(n,\,n^{4}))=\Theta(n^{4})$.
___
##### Commutatività del prodotto

> Per ogni $f(n),\,d(n)>0$, se $f(n) = O(g(n))$ e $d(n)=O(h(n))$ allora si ha che $f(n)\cdot d(n)$ è in $O(f(n)\cdot g(n))$.

> Per ogni $f(n),\,d(n)>0$, se $f(n) = \Omega(g(n))$ e $d(n)=\Omega(h(n))$ allora si ha che $f(n)\cdot d(n)$ è in $\Omega(f(n)\cdot g(n))$.

> Per ogni $f(n),\,d(n)>0$, se $f(n) = \Theta(g(n))$ e $d(n)=\Theta(h(n))$ allora si ha che $f(n)\cdot d(n)$ è in $\Theta(f(n)\cdot g(n))$.

Informalmente, queste tre regole esprimono il fatto che, nel calcolo della notazione asintotica, **data una funzione $p(n)=f(n)\cdot g(n)$ qualsiasi suo limite asintotico è uguale al prodotto tra i limiti asintotici di $f(n)$ e $g(n)$**.

Possiamo **dimostrare la prima regola** (e, di conseguenza, anche le altre due) abbastanza semplicemente. Affermando che $f(n) = O(g(n))$ e che $d(n)=O(h(n))$, stiamo affermando che esistono quattro costanti $c$, $c'$, $n_{0}$ e $n_{0}'$ tali per cui vale che: $$f(n)\le c\cdot g(n)\,\,\,\,\,\,\,\,\,\,\text{per ogni }n\ge n_{0}$$e che: $$d(n)\le c'\cdot h(n)\,\,\,\,\,\,\,\,\,\,\text{per ogni }n\ge n_{0}'$$Di conseguenza, possiamo effettuare una moltiplicazione membro a membro, e garantire che per ogni $n\ge max(n_{0},\,n_{0}')$ vale che: $$f(n)\cdot d(n)\,\,\le\,\,c\cdot c'\cdot g(n)\cdot h(n)$$Prendendo $c\cdot c'$ come nuova costante $c''$, e mantenendo lo stesso $n_{0}$, si ottiene che $f(n) \cdot d(n)\le c''\cdot g(n)\cdot h(n)$ per ogni $n\ge n_{0}$, il che vuol dire che $f(n)\cdot d(n)$ è in $O(g(n)\cdot h(n))$, come volevasi dimostrare.

Vediamo un esempio per comprendere meglio come applicare queste regole. Supponiamo di voler trovare il limite asintotico stretto per $f(n)=3n\cdot 2^{n}+4n^{4}$: per quanto riguarda il primo addendo, si ha che $3n=\Theta (n)$ e che $2^{n}=\Theta(2^{n})$, e applicando la terza delle regole appena esposte si ottiene che $\Theta (n)\cdot \Theta(2^{n})=\Theta(n\cdot 2^{n})$; per il secondo, si trova subito che $4n^{4}=\Theta(n^{4})$; a questo punto, abbiamo che $f(n)=\Theta(n\cdot 2^{n})+\Theta(n^{4})$. Sappiamo che un esponenziale domina sempre un polinomio, dunque applicando la terza delle regole sulla [[IAA_02 - Notazione asintotica#Commutatività della somma|commutatività della somma]] si ottiene che $\Theta(n\cdot 2^{n})+\Theta(n^{4})=\Theta(n\cdot 2^{n})$.
___
##### Sommatorie notevoli

> $$\sum_{i\,=\,0}^{n}i\,=\,\frac{n(n+1)}{2}\,=\,\Theta(n^{2})$$

Più in generale, vale che:

> $$\sum_{i\,=\,0}^{n}i^{c}\,=\,\Theta(n^{c+1})\,\,\,\,\,\,\,\,\,\,\text{per ogni }c\ge 1$$



> $$\sum_{i\,=\,0}^{n}2^{i}\,=\,2^{n+1}-1\,=\,\Theta(2^{n})$$

Più in generale, vale che:

> $$\sum_{i\,=\,0}^{n}c^{i}\,=\,\frac{c^{n+1}-1}{c-1}\,=\,\Theta(c^{n})\,\,\,\,\,\,\,\,\,\,\text{per ogni }c>1$$



> $$\sum_{i\,=\,0}^{n}(i\cdot 2^{i})\,=\,(n-1)2^{n+1}+2\,=\,\Theta(n\cdot 2^{n})$$

Più in generale, vale che:

> $$\sum_{i\,=\,0}^{n}(i\cdot c^{i})\,=\, \frac{n\cdot c^{n+1}}{c-1}-\frac{c^{n+1}-1}{(c-1)^2} \,=\,\Theta(n\cdot c^{n})\,\,\,\,\,\,\,\,\,\,\text{per ogni }c>1$$



> $$\sum_{i\,=\,1}^{n}\log i\,=\,\log n!\,=\,\Theta(n\,\log n)$$

Più in generale, vale che:

> $$\sum_{i\,=\,1}^{n}\log^{c}i\,=\,\Theta(n\,\log^{c}i)\,\,\,\,\,\,\,\,\,\,\text{per ogni }c>1$$



> $$\sum_{i\,=\,1}^{n} \frac{1}{i}=\Theta(\log n)$$
___