### Costo di un algoritmo

Finora, si è parlato in maniera generica e ipotetica di costo computazionale, sfruttando i concetti relativi alle [[Notazione asintotica|notazioni asintotiche]]. In questo capitolo, invece, si approfondirà il calcolo del **costo computazionale di un algoritmo** concreto, adottando il criterio della [[Criteri di misura del costo|misura di costo uniforme]].

Il costo computazionale di un algoritmo, inteso come funzione che ne rappresenta il tempo di esecuzione, è definito come **funzione monotona non decrescente** all'aumentare dell'*input*, poiché è ovvio che è impossibile che diminuisca il costo computazionale all'aumentare dell'*input*. Dunque, poiché il tempo di esecuzione di un algoritmo è strettamente connesso alla dimensione dei suoi *input*, è necessario prima di tutto identificare con precisione questo dato; ad esempio:
- in un algoritmo di **ordinamento**, la dimensione dell'*input* è data dal numero di dati da ordinare;
- in un algoritmo che lavora su una **matrice**, la dimensione dell'*input* è data dal numero di righe e dal numero di colonne (si avranno, quindi, due parametri);
- in un algoritmo che opera su **alberi**, la dimensione dell'*input* è data dal numero di nodi che compongono l'albero in questione.

Ovviamente esistono anche altri algoritmi che non rientrano in questa categorizzazione, per cui tale identificazione risulta meno scontata.

Essendo la notazione asintotica alla base del calcolo del costo computazionale di un algoritmo, il costo ottenuto potrà essere considerato valido solo **asintoticamente**, ossia considerando *input* tendenzialmente molto grandi. Esistono, infatti, algoritmi che per *input* relativamente piccoli hanno un comportamento diverso; è, dunque, opportuno, considerare solo *input* relativamente grandi per valutare la vera efficienza di un algoritmo.
___
### Costo delle istruzioni

È necessario, per calcolare il costo computazionale di un determinato algoritmo, valutare correttamente il costo delle singole **istruzioni**. Possiamo individuare tre categorie principali di istruzioni.

La prima è quella delle **istruzioni elementari**, ossia tutte le istruzioni con un tempo di esecuzione costante, che non dipende quindi dalla dimensione degli *input* (operazioni aritmetiche, lettura o scrittura di una variabile, valutazione di una condizione logica, stampa, ecc. ecc.); essendo il loro tempo di esecuzione costante, generalmente queste istruzioni hanno un costo computazionale di ***θ(1)***.

La seconda è quella dei **blocchi *if/else***, che hanno un costo pari alla **somma** del costo della **verifica della condizione** (solitamente pari a *θ(1)*) e di quello **massimo tra i costi complessivi del blocco *if* o del blocco *else***.

Infine, la terza è quella dei **blocchi iterativi**, che hanno un costo pari alla **somma effettiva** (dunque non asintotica) **dei costi di ciascuna iterazione**, compreso il costo della verifica della condizione; quindi, se tutte le iterazioni hanno lo stesso costo, il costo complessivo del blocco iterativo è pari al prodotto del costo di una singola iterazione per il numero di iterazioni. Inoltre, è importante ricordare che la condizione viene valutata una volta in più rispetto al numero di iterazioni, in quanto l'ultima valutazione, che darà esito negativo, sarà quella che terminerà il blocco.

Per avere un'idea del costo di un algoritmo, tendenzialmente si preferisce conoscere il **caso peggiore**. Tuttavia, per mantenere una maggiore precisione nella valutazione, si utilizzerà comunque la **notazione *θ***, e non la notazione *O*; nel caso in cui ciò non sia possibile, si approssimerà ricorrendo alla notazione *O* o alla notazione *Ω*.
___
### Esempio 1: calcolo del massimo di un *array*

Per comprendere al meglio i concetti appena esposti, di seguito si analizzano alcuni **esempi** di valutazione del costo di un algoritmo.

Il primo esempio è un algoritmo che ottiene il **valore massimo di un *array***. Lo pseudocodice è il seguente:

```
def trova_max(A):
	n = len(A)
	max = A[1]
	for i in range(1, n):
		if A[1] > max:
			max = A[i]
	return max
```

Per comodità, possiamo dividere l'algoritmo in tre blocchi:
- le istruzioni precedenti al blocco iterativo;
- il blocco iterativo;
- le istruzioni successive al blocco iterativo.

Per il primo blocco, si hanno due istruzioni elementari, e dunque il costo computazionale di ciascuna di esse è *θ(1)*, portando il costo del primo blocco a:
$$θ(1) + θ(1) = θ(1)$$
Per il secondo blocco, ossia il blocco iterativo del ciclo *for*, si hanno *n - 1* iterazioni, per cui il costo computazionale del blocco è:
$$(n - 1) ⋅ θ(1) + θ(1) = θ(n - 1) + θ(1) = θ(n) + θ(1) = θ(n)$$
Per il terzo blocco, si ha solamente l'istruzione di ritorno, che è un'istruzione elementare, per cui il costo computazionale del blocco è:
$$θ(1)$$
Una volta calcolato il costo di ognuno dei tre blocchi, è possibile sommare asintoticamente i loro costi parziali per ottenere il costo complessivo dell'algoritmo, che è pari a:
$$T(n) = θ(1) + θ(n) + θ(1) = θ(n)$$
___
### Esempio 2: somma dei primi *n* interi

Il secondo esempio è un algoritmo che, dato un numero *n*, ottiene la **somma dei primi *n* interi a partire da 0**. Lo pseudocodice è il seguente:

```
def calcola_somma_1(n):
	somma = 0
	for i in range(1, n + 1):
		somma += i
	return somma
```

Seguendo gli stessi ragionamenti applicati nell'esempio precedente, arriviamo facilmente alla conclusione che il costo computazionale di questo algoritmo è:
$$T(n) = θ(1) + (n ⋅ θ(1) + θ(1)) + θ(1) = θ(n)$$
Notiamo, tuttavia, questa operazione è facilmente semplificabile ricordando la regola che permette di calcolare in maniera diretta la somma dei primi *n* interi:
$$\sum_{k=0}^{n} = \frac{n(n + 1)}{2}$$
È possibile, dunque, riscrivere l'algoritmo in maniera molto più ottimizzata:

```
def calcola_somma_2(n):
	somma = n * (n + 1) / 2
	return somma
```

Il costo complessivo di questa nuova versione dell'algoritmo è molto minore:
$$T(n) = θ(1) + θ(1) = θ(1)$$
___
### Esempio 3: valutazione di un polinomio in un punto

Il terzo esempio è un algoritmo che **valuta un polinomio** espresso nella forma
$$\sum_{k = 0}^{n}a_i x^i$$
dove ogni *a* corrisponde ad un elemento di un *array* dato in *input* assieme al valore assunto dalla variabile *x*. Ad esempio, il polinomio *x² - 4x + 5* verrà espresso nell'*array* [5, -4, 1]. Lo pseudocodice di questo algoritmo è il seguente:

```
def calcola_polinomio_1(A, x):
	somma = 0
	for i in range(len(A)):
		potenza = 1
		for j in range(i):
			potenza = x * potenza
		somma = somma + A[i] * potenza
	return somma
```

Qui la situazione è più complessa degli esempi precedenti, principalmente per la presenza di due cicli *for* annidati, in cui il contatore del secondo dipende da quello del primo. Ciò significa che il ciclo *for* interno verrà eseguito prima 0 volte, poi una volta, poi due volte e così via, finché il contatore del ciclo *for* esterno non raggiungerà *len(A)*. Questa casistica è perfettamente esprimibile tramite la seguente sommatoria:
$$\sum_{i = 0}^{n}θ(i)$$
Nell'ambito del calcolo della notazione asintotica, le sommatorie godono della proprietà per cui esse sono intercambiabili con la notazione utilizzata. Infatti, la sommatoria precedente è riscrivibile nel modo seguente:
$$\sum_{i = 0}^{n}θ(i) = θ(\sum_{i = 0}^{n}i) = θ(\frac{n(n + 1)}{2}) = θ(n²)$$
Dunque, il costo complessivo dell'algoritmo sarà:
$$T(n) = θ(1) + \sum_{i = 0}^{n}(θ(1) + θ(i) + θ(1)) + θ(1) = θ(1) + θ(n²) + θ(1) = θ(n²)$$
Tuttavia, è possibile ottimizzare questo algoritmo: infatti, piuttosto che ricalcolare la potenza ad ogni termine del polinomio, è possibile conservare la potenza calcolata per il termine precedente, evitando il ciclo *for* annidato. Lo pseudocodice per l'algoritmo ottimizzato è il seguente:

```
def calcola_polinomio_2(A, x):
	somma = 0
	potenza = 1
	for i in range(len(a)):
		potenza = x * potenza
		somma = somma + A[i] * potenza
	return somma
```

Il costo complessivo di questa versione dell'algoritmo è:
$$T(n) = θ(1) + n ⋅ θ(1) + θ(1) = θ(n)$$
___
### Esempio 4: Analisi di caso migliore e caso peggiore

Il quarto esempio è un algoritmo che presenta esplicitamente un **caso migliore** e un **caso peggiore** relativamente agli *input*. Lo pseudocodice è il seguente:

```
def caso_migliore_peggiore(n):
	if n < 0:
		n = -n
	while n:
		if n % 2 == 1:
			return 1
		n -= 2
	return 0
```

Analizziamo il comportamento del ciclo *while*:
- se *n* è dispari, la condizione `n % 2 == 1` restituirà `True`, eseguendo l'istruzione `return` e terminando istantaneamente il ciclo;
- se *n* è pari, allora a ogni iterazione del ciclo si sottrarrà 2 al numero, finché non si arriverà a 0 (condizione necessaria per terminare il ciclo).

Nel primo caso, il costo del ciclo sarà *θ(1)*; nel secondo caso, invece, il costo sarà pari a *θ(n)*. Possiamo quindi dire che il costo computazionale complessivo dell'algoritmo è il seguente:
$$T(n) = \begin{cases} θ(1), & \mbox{se }n\mbox{ è dispari (caso migliore)} \\ θ(n), & \mbox{se }n\mbox{ è pari (caso peggiore)}\end{cases}$$
___