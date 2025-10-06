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

Infine abbiamo le **istruzioni iterative**, che comprendono i cicli `for` e i cicli `while`: il costo computazionale di queste istruzioni è pari alla somma dei **costi di ciascuna delle iterazioni dell'istruzione**, più il **costo di verifica della condizione**; nel caso in cui tutte le iterazioni abbiano lo stesso costo, allora il costo complessivo sarà ottenibile con il **prodotto del costo di una singola iterazione per il numero di iterazioni previste**. In entrambi i casi, è comunque fondamentale calcolare il numero di iterazioni che l'istruzione iterativa considerata dovrebbe svolgere. Bisogna ricordare, inoltre, che **la condizione che controlla l'istruzione iterativa verrà sempre valutata una volta in più rispetto al numero di iterazioni**, poiché l'ultima valutazione sarà sempre quella che porrà fine al ciclo.

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

Supponiamo di avere il seguente algoritmo, utilizzato per valutare il valore di un polinomio $\sum_{i=0}^{n}a_{i}x^{i}$, i cui coefficienti $a_{0},\,a_{1},\,\dots,\,a_{n}$ sono memorizzati in un array $A$, nel punto $x=c$:

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

