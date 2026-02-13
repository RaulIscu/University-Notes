Dopo aver approfondito il concetto di [[IAA_02 - Notazione asintotica#Cos'è la notazione asintotica?|notazione asintotica]] e aver capito come derivarla e semplificarla per varie funzioni, siamo pronti per capire come calcolare effettivamente il **costo computazionale** di un algoritmo.

Prima di procedere, facciamo alcune considerazioni. Innanzitutto, è ragionevole pensare che **il costo computazionale di un algoritmo**, inteso come la funzione che rappresenta il suo tempo di esecuzione, **sia una funzione monotona non decrescente della dimensione dell'input** di tale algoritmo (in parole povere, all'aumentare della dimensione dell'input il tempo di esecuzione o rimane pressoché costante o cresce). Capiamo, dunque, che per calcolare il costo computazionale di un algoritmo è necessario definire proprio la dimensione del suo input: in un [[IAA_06 - Algoritmi di ordinamento|algoritmo di ordinamento]], essa sarà il numero di elementi da ordinare; in un algoritmo che lavora su [[IAA_07 - Strutture dati#Alberi|alberi]], sarà il numero di nodi dell'albero in questione; e così via.

Inoltre, essendo la notazione asintotica il nostro strumento principale nel calcolo del costo computazionale, bisogna sempre tenere presente che **il costo computazionale ottenuto per un algoritmo è effettivamente valido solo asintoticamente**, cioè per input relativamente grandi.

Va sottolineato, inoltre, che **a volte il costo di un algoritmo non dipende solo dalla dimensione dell'input, ma anche dal valore esatto dello stesso**: in casi del genere, è opportuno suddividere lo studio del costo computazionale in termini di "**caso migliore**" e di "**caso peggiore**". A parità di dimensione dell'input, il caso peggiore corrisponde a quello in cui l'input assume valori tali per cui l'algoritmo deve eseguire il massimo numero di operazioni; viceversa, il caso migliore corrisponde all'input che permette all'algoritmo di eseguire il minimo numero di operazioni.

## Come calcolare il costo computazionale di un algoritmo?

Calcolare il costo computazionale di un algoritmo, nel suo complesso, implica il calcolare il **costo computazionale di ognuna delle sue istruzioni**, prevedere il **numero di volte che le istruzioni verranno eseguite** (ciò risulta importante soprattutto quando si trattano istruzioni iterative), e sommare i costi di ogni singola istruzione per ottenere il costo computazionale totale.

Possiamo suddividere le varie istruzioni di un algoritmo in più categorie, in base al loro costo computazionale o al metodo specifico utilizzato per calcolarlo:
- le **istruzioni elementari**;
- le **istruzioni condizionali**;
- le **istruzioni iterative**.

Partiamo dalle **istruzioni elementari**, che comprendono le operazioni aritmetiche, la lettura o scrittura di una variabile, la valutazione di una condizione logica, la stampa di un valore, ecc. ecc. Tutte queste istruzioni hanno un **costo computazionale costante**, dunque pari a **$\Theta(1)$**.

Passiamo, ora, alle **istruzioni condizionali**, ossia quelle che si trovano nella forma:

```
if (condizione):
	bloccoDiIstruzioni1
else:
	bloccoDiIstruzioni2
```

In questo caso, il costo computazionale sarà pari alla somma tra il **costo della verifica della condizione** (solitamente pari a $\Theta(1)$) e il **massimo dei costi dei due blocchi `bloccoDiIstruzioni1` e `bloccoDiIstruzioni2`**.

Infine abbiamo le **istruzioni iterative**, che comprendono i cicli `for` e i cicli `while`: il costo computazionale di queste istruzioni è pari alla **somma effettiva dei costi di ciascuna delle iterazioni dell'istruzione**, più il **costo di verifica della condizione**; nel caso in cui tutte le iterazioni abbiano lo stesso costo, allora il costo complessivo sarà ottenibile con il **prodotto del costo di una singola iterazione per il numero di iterazioni previste**. In entrambi i casi, è comunque fondamentale calcolare il numero di iterazioni che l'istruzione iterativa considerata dovrebbe svolgere. Bisogna ricordare, inoltre, che **la condizione che controlla l'istruzione iterativa verrà sempre valutata una volta in più rispetto al numero di iterazioni**, poiché l'ultima valutazione sarà sempre quella che porrà fine al ciclo.

##### Esempio n°1: ricerca del massimo in un array

Supponiamo di avere il seguente algoritmo, utilizzato per trovare il valore massimo tra $n$ valori all'interno di un array $A$ non ordinato, che si assume sia sempre non vuoto:

```
def trova_max(A):
	n = len(A)                 
	max = A[0]
	
	for i in range(1, n):
		if A[i] > max:
			max = A[i]
	
	return max
```

Analizziamo l'algoritmo istruzione per istruzione: le prime due rappresentano delle istruzioni elementari (scritture in variabili), e dunque entrambe presentano un costo computazionale di $\Theta(1)$; di seguito, troviamo un'istruzione iterativa, dove il costo di ogni iterazione è $\Theta(1)+\Theta(1)+\Theta(1)\,=\,\Theta(1)$, e che esegue $n-1$ iterazioni; infine, l'istruzione di ritorno è anch'essa un'istruzione elementare, e in quanto tale ha costo $\Theta(1)$.

A questo punto, detto $T(n)$ il costo computazionale complessivo dell'algoritmo `trova_max`, possiamo affermare che esso è pari a:
$$T(n)\,=\,\Theta(1)+[(n-1)\cdot \Theta(1)+\Theta(1)]+\Theta(1)\,=\,\Theta(n)$$
___
##### Esempio n°2: somma dei primi $n$ interi

Supponiamo di avere il seguente algoritmo, utilizzato per calcolare la somma dei primi $n$ interi positivi:

```
def calcola_somma(n):
	somma = 0
	
	for i in range(1, n + 1):
		somma += i
	
	return somma
```

Analizziamo l'algoritmo istruzione per istruzione: la prima è un'istruzione elementare, che dunque ha costo $\Theta(1)$; abbiamo poi un'istruzione iterativa, che esegue $n$ iterazioni dove ciascuna di esse ha costo $\Theta(1)+\Theta(1)=\Theta(1)$ (aumento del contatore e scrittura nella variabile `somma`); infine, l'istruzione di ritorno finale ha costo $\Theta(1)$, essendo anch'essa un'istruzione elementare.

A questo punto, detto $T(n)$ il costo computazionale complessivo dell'algoritmo `calcola_somma`, possiamo affermare che esso è pari a:
$$T(n)\,=\,\Theta(1)+[n\cdot \Theta(1)+\Theta(1)]+\Theta(1)\,=\,\Theta(n)$$
Seppur questa analisi sia corretta, notiamo che possiamo reinventare completamente tale algoritmo in modo da aumentarne l'efficienza. Infatti, sappiamo che la somma dei primi $n$ interi positivi può essere calcolata velocemente come $\frac{n(n+1)}{2}$; perciò, possiamo progettare un nuovo "algoritmo" `calcola_somma_new`:

```
def calcola_somma_new(n):
	somma = n * (n + 1) / 2
	return somma
```

Il costo computazionale $T(n)$ di questo nuovo algoritmo è $\Theta(1)$, rendendolo nettamente più efficiente del suo predecessore.
___
##### Esempio n°3: valutazione di un polinomio in un punto $c$

Supponiamo di avere il seguente algoritmo, utilizzato per valutare il valore di un polinomio $\sum_{i\,=\,0}^{n}a_{i}x^{i}$, i cui coefficienti $a_{0},\,a_{1},\,\dots,\,a_{n}$ sono memorizzati in un array $A$, nel punto $x=c$:

```
def calcola_polinomio(A, c):
	somma = 0
	
	for i in range(len(A)):
		potenza = 1
		
		for j in range(i):
			potenza *= c
			
		somma += A[i] * potenza
		
	return somma
```

Analizziamo l'algoritmo istruzione per istruzione: la prima è un'istruzione elementare con costo $\Theta(1)$; abbiamo poi la prima istruzione iterativa, che viene eseguita $n$ volte e dove ogni iterazione ha costo $\Theta(i)$, dato che il corpo del ciclo contiene un ulteriore ciclo annidato che viene eseguito $i$ volte, e che svolge operazioni elementari; infine, l'istruzione finale ha costo $\Theta(1)$.

A questo punto, detto $T(n)$ il costo computazionale complessivo dell'algoritmo `calcola_polinomio`, possiamo affermare che esso è pari a:
$$\begin{align} T(n)\,&=\,\Theta(1)+\left[\sum_{i\,=\,1}^{n}(\Theta(1)+\Theta(i)) + \Theta(1) \right]+\Theta(1)\,\\&=\,\Theta(1)+\left[\sum_{i\,=\,1}^{n}\Theta(1)+\sum_{i\,=\,1}^{n}\Theta(i) \right]+\Theta(1)\,\\&=\,\Theta(1)+\Theta(n)+\Theta(n^2)\,\\&=\Theta(n^{2}) \end{align}$$
Tuttavia, similmente all'[[IAA_03 - Costo computazionale#Esempio n°2 somma dei primi $n$ interi|esempio precedente]], notiamo che una riprogettazione dell'algoritmo considerato può portare a un notevole aumento della sua efficienza. In questo caso, come abbiamo visto, il punto più critico è il ciclo annidato al cuore dell'algoritmo, e possiamo fornire un'implementazione che lo elimina completamente:

```
def calcola_polinomio_new(A, c):
	somma = A[0]
	potenza = 1
	
	for i in range(1, len(A)):
		potenza *= c
		somma += A[i] * potenza
	
	return somma
```

In questa implementazione, abbiamo evitato di ricalcolare più volte il valore `potenza`, sfruttando i valori calcolati in precedenza e semplificando notevolmente l'algoritmo. Il costo computazionale di questa versione può essere calcolato molto facilmente ed è pari a $\Theta(n)$, molto minore al precedente costo di $\Theta(n^{2})$.
___
##### Esempio n°4: caso migliore e caso peggiore

Supponiamo di avere il seguente algoritmo, in cui si distingue chiaramente un caso migliore e un caso peggiore in termini di costo computazionale, in base all'input che viene dato all'algoritmo:

```
def es4(n):
	if (n < 0):
		n = -n
	
	while n:
		if (n % 2 == 1):
			return 1
		n -= 2
	
	return 0
```

Analizziamo l'algoritmo istruzione per istruzione: la prima è un'istruzione condizionale, dove la valutazione della condizione ha costo $\Theta(1)$, così come il codice contenuto al suo interno, il che porta il costo complessivo dell'istruzione condizionale a essere $\Theta(1)+\Theta(1)=\Theta(1)$. Arriviamo ora al ciclo `while`, ed è qui che si evidenzia la differenza tra caso migliore e caso peggiore:
- se $n$ è dispari, la condizione `n % 2 == 1` risulterà essere verificata (il resto della divisione tra un numero dispari e $2$ è sempre pari a $1$), dunque verrà immediatamente eseguita l'istruzione `return 1` e terminata l'esecuzione dell'algoritmo;
- se $n$ è pari, la condizione `n % 2 == 1` non sarà mai verificata, dunque si eseguiranno le varie iterazioni del ciclo `while`; per prevedere quante iterazioni del ciclo verranno eseguite, si predispone una tabella a $2$ righe, dove nella prima si tiene il conto di quante iterazioni si sono eseguite e nella seconda del valore di $n$, ossia del valore della variabile che "controlla" l'esecuzione del ciclo, a ogni iterazione:

![[costocomputazionale_esempio.png]]

Il ciclo verrà eseguito finché $n-2k=0$, dunque si potrà ottenere il numero $k$ di iterazioni risolvendo per $k$ tale equazione:
$$n-2k=0\,\,\,\Rightarrow\,\,\,n=2k\,\,\,\Rightarrow\,\,\,k=\frac{n}{2}$$
il che porta il costo del ciclo, nel caso peggiore, a essere pari a:
$$\Theta(1)\cdot \frac{n}{2}=\Theta(n)$$
Dunque, considerando tutto ciò che abbiamo detto, possiamo quantificare il costo computazionale dell'algoritmo considerato distinguendo i due casi:
$$T(n)=\begin{cases} \Theta(1)&\text{se }n\text{ è dispari}\\\Theta(n)&\text{se }n\text{ è pari} \end{cases}$$
___
##### Esempio n°5: numero di iterazioni con radice

Supponiamo di avere il seguente algoritmo:

```
def es5(n):
	n = abs(n)
	x = r = 0
	
	while (x * x < n):
		x += 1
		r *= 3 * x
	
	return r
```

Analizziamo l'algoritmo istruzione per istruzione: le prime istruzioni che troviamo sono tutte istruzioni elementari di costo $\Theta(1)$, dunque possiamo affermare che il blocco di codice precedente al ciclo `while` ha tale costo; lo stesso vale per l'istruzione di ritorno che troviamo al termine dell'algoritmo. Ora, pensiamo ad analizzare il ciclo `while`, che si comporta nel modo seguente:

![[costocomputazionale_esempio1.png]]

Il ciclo, in questo caso, itera finché è vero che $x^{2}<n$, dunque la condizione per la terminazione dello stesso è che $k^{2}=n$; da ciò, possiamo dedurre il numero $k$ di iterazioni che si prevede vengano eseguite:
$$k^{2}=n\,\,\,\Rightarrow\,\,\,k=\sqrt{ n }$$
Essendo il corpo del ciclo composto esclusivamente da istruzioni elementari, il costo complessivo del ciclo sarà pari a:
$$\Theta(1)\cdot \sqrt{ n }=\Theta(\sqrt{ n })$$
A questo punto, possiamo trovare il costo complessivo $T(n)$ dell'algoritmo:
$$T(n)\,=\,\Theta(1)+\Theta(\sqrt{ n })+\Theta(1)\,=\,\Theta(\sqrt{ n })$$
___
##### Esempio n°6: numero di iterazioni logaritmico

Supponiamo di avere il seguente algoritmo:

```
def es6(n):
	n = abs(n)
	x = r = 1
	
	while (n > 1):
		r += 2
		n = n // 3
	
	return r
```

Analizziamo l'algoritmo istruzione per istruzione: il primo blocco di istruzioni, quello precedente al ciclo, è composto interamente da istruzioni elementari, dunque avrà costo $\Theta(1)$; lo stesso vale per l'istruzione di ritorno con cui termina l'algoritmo. Passiamo, ora, ad analizzare il ciclo `while`, il cui comportamento può essere formalizzato nella seguente tabella:

![[costocomputazionale_esempio2.png]]

Notiamo che il ciclo continua a iterare finché $n>1$, dunque la condizione per la terminazione del ciclo è che $\frac{n}{3^{k}}=1$; da ciò possiamo trovare il numero $k$ di iterazioni che si prevede vengano eseguite:
$$\frac{n}{3^{k}}=1\,\,\,\Rightarrow\,\,\,n=3^{k}\,\,\,\Rightarrow\,\,\,k=\log_{3}(n)$$
A ogni iterazione, il ciclo esegue una serie di istruzioni elementari, per cui il costo complessivo di esecuzione del ciclo è:
$$\Theta(1)\cdot \log_{3}(n)=\Theta(\log n)$$
A questo punto, otteniamo il costo complessivo $T(n)$ dell'algoritmo:
$$T(n)\,=\,\Theta(1)+\Theta(\log n)+\Theta(1)\,=\,\Theta(\log n)$$
___
##### Esempio n°7: numero di iterazioni esponenziale

Supponiamo di avere il seguente algoritmo:

```
def es7(n):
	n = abs(n)
	x = t = 1
	
	for i in range(n):
		t = 3 * t
	
	t -= 1
	
	while (t >= x):
		x += 2
		t -= 2
		
	return x
```

Analizziamo l'algoritmo istruzione per istruzione: innanzitutto, individuiamo le varie istruzioni elementari, distribuite prima, in mezzo e dopo i due cicli, che hanno tutte costo $\Theta(1)$. Ora passiamo ad analizzare i cicli, partendo dal ciclo `for`: questo viene eseguito $n$ volte, e ogni iterazione ha costo costante pari a $\Theta(1)$, per cui il costo del ciclo in questione sarà:
$$\Theta(1)\cdot n=\Theta(n)$$
Inoltre, al termine del ciclo `for`, proprio grazie alla sua esecuzione, si avrà che $t=3^{n}$; prima di entrare nel ciclo `while`, poi, si esegue l'istruzione elementare `t -= 1`, il che porta il valore di $t$ all'entrata del ciclo `while` a essere $t=3^{n}-1$. Ora, il comportamento del ciclo `while` può essere formalizzato nel modo seguente:

![[costocomputazionale_esempio3.png]]

Il ciclo considerato viene eseguito finché $t\ge x$, dunque la condizione di terminazione del ciclo è che $3^{n}-(1+2k)=1+2k$, che possiamo sfruttare per ottenere il numero $k$ di iterazioni previste:
$$3^{n}-(1+2k)=1+2k\,\,\,\Rightarrow\,\,\,3^{n}-2=4k\,\,\,\Rightarrow\,\,\,k=\frac{3^{n}-2}{4}$$
Ora, all'interno di ogni iterazione del ciclo `while` vengono eseguite sempre $2$ istruzioni elementari, il che porta il costo di una singola iterazione ad essere pari a $\Theta(1)$; dunque il costo complessivo del ciclo è:
$$\Theta(1)\cdot \frac{3^{n}-2}{4}=\Theta(3^{n})$$
A questo punto, possiamo arrivare a calcolare il costo complessivo $T(n)$ dell'algoritmo:
$$T(n)\,=\,\Theta(1)+\Theta(n)+\Theta(1)+\Theta(3^{n})+\Theta(1)\,=\,\Theta(1)+\Theta(n)+\Theta(3^{n})\,=\,\Theta(3^{n})$$
___
##### Esempio n°8: costo pari a logaritmo di logaritmo

Supponiamo di avere il seguente algoritmo:

```
def es8(n):
	n = abs(n)
	p = 2
	
	while (n >= p):
		p = p * p
	
	return p
```

Analizziamo l'algoritmo istruzione per istruzione: notiamo subito che le prime due istruzioni, così come l'istruzione di ritorno finale, sono tutte istruzioni elementari di costo $\Theta(1)$. Rimane da analizzare il ciclo `while`, il cui comportamento viene riassunto nella seguente tabella:

![[costocomputazionale_esempio4.png]]

Il ciclo itera finché $n\ge p$, dunque la condizione di terminazione dello stesso è che $2^{2^{k}}=n$; possiamo sfruttare ciò per ottenere il numero $k$ di iterazioni che si prevede vengano eseguite:
$$2^{2^{k}}=n\,\,\,\Rightarrow\,\,\,2^{k}=\log_{2}(n)\,\,\,\Rightarrow\,\,\,k=\log_{2}(\log_{2}(n))$$
Essendo il corpo del ciclo costituito esclusivamente da un'istruzione elementare di costo $\Theta(1)$, il costo del ciclo sarà pari a:
$$\Theta(1)\cdot \log_{2}(\log_{2}(n))=\Theta(\log(\log n))$$
A questo punto, possiamo trovare il costo complessivo $T(n)$ dell'algoritmo considerato:
$$T(n)\,=\,\Theta(1)+\Theta(\log(\log n))+\Theta(1)\,=\,\Theta(\log(\log n))$$
___
##### Esempio n°9: cicli annidati

Supponiamo di avere il seguente algoritmo:

```
def es9(n):
	n = abs(n)
	i, j, t, s = 1
	
	while (i * i <= n):
		for j in range(t):
			s += 1
		
		i += 1
		t += 1
	
	return s
```

Analizziamo l'algoritmo istruzione per istruzione: le prime istruzioni, così come l'istruzione di ritorno finale, sono tutte istruzioni elementari di costo $\Theta(1)$. Passiamo, ora, al ciclo `while`, il cui comportamento può essere formalizzato nella seguente tabella:

![[costocomputazionale_esempio5.png]]

Il ciclo continua a iterare finché $i^{2}\le n$, dunque la condizione di terminazione del ciclo è che $(k+1)^{2}=n$. Possiamo sfruttare quanto detto per calcolare il numero $k$ di iterazioni previste per il ciclo in questione:
$$(k+1)^{2}=n\,\,\,\Rightarrow\,\,\,k+1=\sqrt{ n }\,\,\,\Rightarrow\,\,\,k=\sqrt{ n }-1$$
Notiamo, ora, che il corpo di codice del ciclo `while` contiene, oltre a due istruzioni elementari di costo $\Theta(1)$, anche un ciclo `for` annidato, che viene dunque eseguito $t$ volte per ogni iterazione del ciclo esterno; dato che il valore di $t$ aumenta di $1$ ad ogni iterazione del ciclo esterno, il numero totale di iterazioni eseguite dal ciclo sarà pari a:
$$\sum_{t\,=\,1}^{\sqrt{ n }\,-\,1}t=\frac{(\sqrt{ n }-1)\sqrt{ n }}{2}=\frac{n-\sqrt{ n }}{2}$$
Dunque, il costo complessivo del ciclo `while` esterno sarà dato da:
$$\Theta(1)\cdot \frac{n-\sqrt{ n }}{2}+\Theta(1)\cdot \sqrt{ n }-1=\Theta(n)+\Theta(\sqrt{ n })=\Theta(n)$$
A questo punto, possiamo ottenere il costo complessivo $T(n)$ dell'algoritmo:
$$T(n)\,=\,\Theta(1)+\Theta(n)+\Theta(1)\,=\,\Theta(n)$$
___
##### Esempio n°10

Supponiamo di avere il seguente algoritmo:

```
def es10(n):
	n = abs(n)
	s = n
	p = 2
	i, r = 1
	
	while (s >= 1):
		s = s // 5
		p += 2
		
	p = p * p
	
	while (i * i * i < n):
		for j in range(p):
			r += 1
		
		i += 1
	
	return r
```

Analizziamo l'algoritmo istruzione per istruzione: come al solito, notiamo prima di tutto le varie istruzioni elementari presenti (il blocco iniziale, l'istruzione compresa tra i due cicli `while`, e l'istruzione di ritorno finale), tutte aventi costo $\Theta(1)$. A questo punto, passiamo a considerare il primo ciclo `while`, il cui comportamento può essere riassunto nella seguente tabella:

![[costocomputazionale_esempio6.png]]

Il ciclo considerato viene eseguito finché vale che $s \ge 1$, e dunque la condizione di terminazione del ciclo è che $\frac{n}{5^{k}}=1$, condizione che possiamo utilizzare per calcolare il numero $k$ di iterazioni previste:
$$\frac{n}{5^{k}}=1\,\,\,\Rightarrow\,\,\,n=5^{k}\,\,\,\Rightarrow\,\,\,k=\log_{5}(n)$$
Ora, all'interno del ciclo considerato ci sono solo istruzioni elementari di costo $\Theta(1)$, dunque il costo complessivo del ciclo sarà pari a:
$$\Theta(1)\cdot \log_{5}(n)=\Theta(\log n)$$
Notiamo, del resto, che nel ciclo appena visto viene modificata la variabile $p$, che ci servirà in seguito, ed è dunque importante capire quale sarà il valore di $p$ una volta usciti dal ciclo: in ciascuna delle $\log_{5}(n)$ iterazioni, viene aggiunto $2$ a $p$, che ricordiamo essere inizializzato a $2$, dunque il valore di $p$ all'uscita del ciclo sarà $p=2+2\log_{5}(n)$; inoltre, subito dopo il ciclo appena considerato viene eseguita l'istruzione `p = p * p`, dunque all'entrata del ciclo successivo si avrà $p=(2+2\log_{5}(n))^{2}$. Passiamo, a questo punto, ad analizzare il comportamento del secondo ciclo `while`:

![[costocomputazionale_esempio7.png]]

Il ciclo considerato viene eseguito finché vale che $i^{3}<n$, e dunque la condizione di terminazione del ciclo è che $(k+1)^{3}=n$, condizione che possiamo utilizzare per calcolare il numero $k$ di iterazioni previste:
$$(k+1)^{3}=n\,\,\,\Rightarrow\,\,\,k+1=\sqrt[3]{ n }\,\,\,\Rightarrow\,\,\,k=\sqrt[3]{ n }-1$$
A questo punto, si noti che all'interno del ciclo `while` considerato si trova anche un ciclo `for` annidato, che viene eseguito $p=(2+2\log_{5}(n))^{2}$ volte per ciascuna iterazione del ciclo esterno, il che porta il numero di iterazioni di tale ciclo ad essere pari a:
$$(2+2\log_{5}(n))^{2}\cdot (\sqrt[3]{ n }-1)$$
Dunque, il costo complessivo del ciclo `while` esterno è pari a:
$$\begin{align}&\,\,\,\,\,\,\,\,\Theta(1)\cdot(2+2\log_{5}(n))^{2}\cdot(\sqrt[3]{ n }-1)+\Theta(1)\cdot(\sqrt[3]{ n }-1)\\&=\Theta(1)\cdot \Theta(\log^{2}n)\cdot(\sqrt[3]{ n }-1)+\Theta(\sqrt[3]{ n })\\&=\Theta(\sqrt[3]{ n }\cdot \log^{2}(n))+\Theta(\sqrt[3]{ n })\\&=\Theta(\sqrt[3]{ n }\cdot \log^{2}(n))\end{align}$$
A questo punto, possiamo finalmente ottenere il costo complessivo $T(n)$ dell'algoritmo:
$$T(n)\,=\,\Theta(1)+\Theta(\log n)+\Theta(1)+\Theta(\sqrt[3]{ n }\cdot \log^{2}n)+\Theta(1)\,=\,\Theta(\sqrt[3]{ n }\cdot \log^{2}n)$$
___
