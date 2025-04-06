### Cos'è la ricorsione

Finora sono stati trattati algoritmi basati prevalentemente su cicli iterativi, come il ciclo *for* o il ciclo *while*; spesso, tuttavia, algoritmi iterativi possono essere riformulati sfruttando la "**ricorsione**". Un algoritmo ricorsivo è un algoritmo che risolve un determinato problema riapplicando sé stesso su versioni via via più semplici dello stesso problema.

Per comprendere meglio questa tecnica, riformuliamo un algoritmo già visto in forma ricorsiva. L'algoritmo di [[Ricerca|ricerca binaria]] si presta particolarmente a questa riformulazione; i passaggi di una ricerca binaria ricorsiva sarebbero i seguenti:
- ispezionare l'elemento centrale dell'*array*;
- se l'elemento in questione è uguale all'elemento cercato v, restituire il suo indice;
- se l'elemento in questione è maggiore di v, ridurre l'*array* alla sua metà inferiore e rieseguire la ricerca binaria su di essa;
- se l'elemento in questione è minore di v, ridurre l'*array* alla sua metà superiore e rieseguire la ricerca binaria su di essa.

Le funzioni ricorsive, in realtà, sono più comuni di quanto si possa pensare. Le troviamo anche in matematica, dove un tipico esempio di ciò è il **fattoriale**:
$$n! = \begin{cases}n ⋅ (n - 1)! & \mbox{se } n > 0 \\ 1 & \mbox{se } n = 0 \end{cases}$$
Analizzando questo esempio, possiamo riconoscere *n = 0* come il "**caso base**" del problema, ossia il suo sotto-problema minimo, corrispondente dunque alla versione più semplice possibile del problema stesso.

All'interno della risoluzione di un problema ricorsivo, **la catena di ricorsione viene ripetuta finché non viene raggiunto il caso base del problema**. Per questo motivo, nella giusta costruzione di un algoritmo ricorsivo è necessario avere almeno un caso base al suo interno, in quanto la sua assenza causerebbe l'algoritmo a continuare all'infinito.

Arriviamo, quindi, alla seguente definizione di algoritmo ricorsivo:

> Un algoritmo è detto **ricorsivo** quando è espresso in termini di sé stesso. Un algoritmo ricorsivo ha le seguenti proprietà:
> - la soluzione del problema complessivo è costruita risolvendo ricorsivamente uno o più sotto-problemi di dimensione minore, e combinando le soluzioni ottenute;
> - la successione dei sotto-problemi deve sempre convergere ad un sotto-problema che costituisca il caso base, il quale termina la ricorsione.

___
### Esempi di ricorsione

Di seguito, sono esposti alcuni **esempi** (in pseudocodice) di **algoritmi ricorsivi**:

```
def fattoriale(n):
	if n == 0:
		return 1
	return n * fattoriale(n - 1)
```

```
def ricerca_sequenziale_ric(A, v, n = len(A) - 1):
	if A[n] == v:
		return n

	if n == 0:
		return -1
	return ricerca_sequenziale_ric(A, v, n - 1)
```

```
def ricerca_binaria_ric(A, v, i_min = 0, i_max = len(A)):
	if i_min > i_max:
		return -1

	m = (i_min + i_max) // 2

	if A[m] == v:
		return m
	elif A[m] > v:
		return ricerca_binaria_ric(A, v, i_min, m - 1)
	else:
		return ricerca_binaria_ric(A, v, m + 1, i_max)
```

___
### Iterazione vs. Ricorsione

Qualsiasi problema risolvibile con un algoritmo ricorsivo può essere risolto anche con un algoritmo iterativo. Viene allora da chiedersi perché si dovrebbe considerare l'opzione della ricorsione, e in quali contesti (se ce ne sono) questa risulti più vantaggiosa.

Tendenzialmente, si preferisce utilizzare la **ricorsione** quando è possibile formulare la soluzione di un problema in modo aderente alla natura del problema stesso, o banalmente quando la versione iterativa della soluzione è molto più complessa. Invece, conviene generalmente utilizzare l'**iterazione** quando essa risulta implementabile in maniera altrettanto semplice e chiara rispetto alla ricorsione, o quando è importante tener conto dell'efficienza dell'algoritmo.

L'ultimo punto è forse il più importante. Infatti, ogni algoritmo richiede, per essere eseguito, una determinata **quantità di memoria**, necessaria per:
- conservare il codice che ne definisce il funzionamento;
- passare i parametri in *input* e restituire valori in *output*;
- memorizzare i valori delle sue variabili locali.

Per natura di un algoritmo ricorsivo, che richiama sé stesso un elevato numero di volte, esso richiederà solitamente molta più memoria rispetto a un normale algoritmo iterativo. Quindi, a grandi linee, **si tende a preferire l'iterazione alla ricorsione**, a meno che il problema posto non sia risolvibile in maniera veloce e intuitiva con quest'ultima.
___
### Equazioni di ricorrenza

Nel calcolo del **[[Costo computazionale|costo computazionale]]**, gli algoritmi ricorsivi danno vita a funzioni matematiche anch'esse ricorsive; le funzioni matematiche che esprimono il costo computazionale di algoritmi ricorsivi vengono anche dette "**equazioni di ricorrenza**".

Per comprendere meglio questo concetto, torniamo all'esempio del **fattoriale**. Il costo computazionale di tale algoritmo risulta essere:
$$ T = \begin{cases} T(n) = θ(1) + T(n - 1)& \mbox{se } n > 0 \\ T(0) = θ(1) & \mbox{se } n = 0 \end{cases}$$
La parte generica dell'equazione di ricorrenza che definisce *T(n)* contiene sempre almeno due addendi, di cui almeno uno contiene la parte ricorsiva (nell'esempio, *T(n - 1)*), mentre uno rappresenta il costo computazionale di ciò che viene eseguito fuori dalla parte ricorsiva (nell'esempio, *θ(1)*). Inoltre, così come per la definizione di algoritmi ricorsivi, anche l'equazione di ricorrenza deve necessariamente presentare un caso base (nell'esempio, *T(0)*).

Per sviluppare l'equazione di ricorrenza e quantificare più precisamente il costo computazionale di un algoritmo ricorsivo, si utilizzano diversi **metodi**:
- metodo **iterativo**;
- metodo di **sostituzione**;
- metodo dell'**albero**;
- metodo **principale**.
___
### Metodo iterativo

L'idea alla base del **metodo iterativo** è quella di sviluppare l'equazione di ricorrenza in modo da essere espressa come **somma di termini dipendenti dal caso generico e dal caso base**. Tuttavia, per l'elevato numero di calcoli da effettuare, esso risulta spesso inefficiente.

Consideriamo, ad esempio, la seguente equazione di ricorrenza:
$$T = \begin{cases} T(n) = θ(1) + T(n - 1) \\ T(1) = θ(1) \end{cases}$$
Proviamo a sviluppare il termine *T(n)* come somma dei suoi sotto-termini: se *T(n)* è definito come *θ(1) + T(n - 1)*, allora *T(n - 1)* sarà definito come *θ(1) + T(n - 2)*, e così via. Sviluppando *T(n)* in sotto-termini *k* volte, si ottiene:
$$T(n) = T(n - k) + \underbrace{θ(1) + θ(1) + \cdots + θ(1)}_{k \mbox{ volte}} = T(n - k) + k ⋅ θ(1)$$
Dopo un determinato numero di ricorsioni, però, l'equazione di ricorrenza raggiungerà il suo caso base, in questo caso *T(1)*. La catena, dunque, procederà finché *n - k = 1*, in modo che *T(n - k)* corrisponda a *T(1)*. Ne segue, dunque, che il numero di ricorsioni sarà:
$$k = n - 1$$
Una volta trovato *k*, basterà sostituirlo nell'equazione precedentemente trovata per calcolare il **costo computazionale generico** dell'algoritmo dell'esempio:
$$T(n) = T(n - k) + k ⋅ θ(1) = T(n - (n - 1)) + (n - 1) ⋅ θ(1) = T(1) + θ(n) = θ(1) + θ(n) = θ(n)$$

Vediamo un altro esempio, considerando la seguente equazione di ricorrenza:
$$T = \begin{cases} T(n) = T(\frac{n}{2}) + θ(1) \\ T(1) = θ(1) \end{cases}$$
Sviluppando *T(n)*, stavolta, si ottiene la seguente equazione generalizzata:
$$T(n) = T\left(\frac{n}{2^k} \right) + k ⋅ θ(1)$$
Sappiamo che il caso base è *T(1)*, che viene quindi raggiunto quando
$$\frac{n}{2^k} = 1$$
ossia quando il numero di ricorsioni è pari a:
$$k = log_2(n)$$
Risostituiamo *k* all'interno dell'equazione generalizzata, e facendo i calcoli si otterrà il costo computazionale generico dell'algoritmo:
$$T(n) = T\left(\frac{n}{2^k} \right) + k ⋅ θ(1) = T(1) + log_2(n) ⋅ θ(1) = θ(1) + θ(log_2(n)) = θ(log_2(n))$$
[casi particolari: pag. 58 - 59 - 60]
___
### Metodo di sostituzione

L'idea alla base del **metodo di sostituzione** consiste nell'**ipotizzare una soluzione per l'equazione di ricorrenza**, e dimostrare poi tale ipotesi tramite l'**induzione**. Lo svantaggio, piuttosto evidente, di tale metodo, è quello di poter procedere solo per tentativi.

Consideriamo, ad esempio, la seguente equazione di ricorrenza:
$$T = \begin{cases} T(n) = T(n - 1) + θ(1) \\ T(1) = θ(1) \end{cases}$$
Ipotizziamo la soluzione "*T(n) = O(n)*", ossia che *T(n) ≤ kn* per una certa costante *k*. 

[CONTINUO: pag. 60 - 61 - 62]
___
### Metodo dell'albero

Il **metodo dell'albero** costituisce semplicemente la **rappresentazione grafica del metodo iterativo**, rendendolo più semplice e chiaro rispetto alla sua controparte scritta.

Consideriamo, ad esempio, la seguente equazione di ricorrenza:
$$T = \begin{cases} T(n) = 2T(\frac{n}{2}) + θ(n^2) \\ T(1) = θ(1) \end{cases}$$
Utilizzando il metodo iterativo, la prima iterazione corrisponderebbe alla forma generica espressa nell'equazione di ricorrenza; la seconda corrisponderebbe a
$$T(n) = 2\left(2T\left(\frac{n}{2^2} \right) + θ\left(\left(\frac{n}{2} \right)^2 \right) \right) + θ(n^2) = 4T\left(\frac{n}{2^2}\right) + 2θ\left(\left(\frac{n}{2} \right)^2 \right) + θ(n^2)$$
e così via. La generalizzazione sfruttando il metodo iterativo risulta essere:
$$T(n) = 2^{k - 1}T\left(\frac{n}{2^k} \right) + \left(\sum_{i = 0}^{k} 2^i ⋅ θ\left(\left(\frac{n}{2^i} \right)^2 \right) \right) = 2^{k - 1}T\left(\frac{n}{2^k} \right) + \left(\sum_{i = 0}^{k - 1}θ\left(\frac{n^2}{2^i} \right) \right) = 2^{k - 1}T\left(\frac{n}{2^k} \right) + θ(n^2) ⋅ \sum_{i = 0}^{k - 1}\frac{1}{2^i}$$

Con il metodo dell'albero, la prima iterazione corrisponde a:

![[metodoalbero_example1.png]]

La seconda iterazione, invece, verrebbe rappresentata così:

![[metodoalbero_example2.png]]

e così via, fino ad arrivare a una generalizzazione del genere:

![[metodoalbero_example3.png]]