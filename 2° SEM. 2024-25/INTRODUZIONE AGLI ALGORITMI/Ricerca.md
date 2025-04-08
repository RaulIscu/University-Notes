### Il problema della ricerca

Nell'ambito dell'informatica, esistono alcune tipologie di problemi particolarmente ricorrenti. In particolare, uno di essi riguarda la **ricerca di un elemento in un insieme di elementi**, come numeri, stringhe o altro. In questo tipo di problemi, si individuano principalmente due componenti:
- l'***input***, che consiste in un *array* A di *n* elementi e in un valore v da cercare al suo interno;
- l'***output***, che consiste nell'indice corrispondente alla posizione dell'elemento v all'interno dell'*array* A (se l'elemento è presente), oppure in `Null` o -1 (se l'elemento non è presente).
___
### Ricerca sequenziale

Uno degli approcci più intuitivi per risolvere il problema della ricerca è l'algoritmo della **ricerca sequenziale**. Questo algoritmo segue i seguenti passaggi:
- l'*array* A preso in *input* viene analizzato elemento per elemento;
- ogni elemento dell'*array* viene confrontato con il valore v; se l'elemento analizzato coincide con v viene restituito l'indice di tale elemento, altrimenti si procede al prossimo elemento;
- se anche nessun elemento dell'*array* coincide con v, viene restituito -1 per indicare che l'elemento cercato non è presente nell'*array*.

Di seguito, un esempio di pseudocodice che implementa questo algoritmo:

```
def ricerca_sequenziale(A, v):
	i = 1
	
	while i < len(A) and A[i] ≠ v:        # eseguito massimo n volte
		i += 1
	
	if i < len(A):
		return i
	else:
		return -1
```

Senza bisogno di un'analisi approfondita, ci si rende conto che nel **caso migliore** (ossia quello in cui l'elemento non solo è presente nell'*array*, ma si trova alla prima posizione) tale algoritmo ha un [[Costo computazionale|costo computazionale]] pari a ***θ(1)***. Invece, nel **caso peggiore** (ossia quello in cui l'elemento non è presente nell'*array*), tale algoritmo ha un costo computazionale di ***θ(n)***.

Poiché caso peggiore e caso migliore presentano costi computazionali differenti, non è possibile trovare una stima del costo valida per casi generici. Diremo quindi che il costo computazionale dell'algoritmo è in *O(n)*, per evidenziare il fatto che ci sono *input* in cui questo costo viene raggiunto, ma anche *input* per cui il costo è minore.

In questi casi, è necessaria una **stima del costo medio** dell'algoritmo, ossia del costo che è più probabile avere. Per ottenerla, ipotizziamo di avere un *array* A contenente *n* elementi, al cui interno ogni posizione ha la stessa probabilità di contenere il valore v; in queste condizioni, è possibile affermare che la probabilità che v sia in *k*-esima posizione è:
$$P = \frac{1}{n}$$
Applicando tale probabilità al numero di iterazioni, si ottiene:
$$P ⋅ \sum_{k = 0}^{n}k = \frac{1}{n} ⋅ \frac{n(n + 1)}{2} = \frac{n + 1}{2}$$
Il risultato ottenuto corrisponde, così, al numero medio di iterazioni del ciclo. Esso si trova in *θ(n)*, quindi il caso medio si avvicina più al caso peggiore che al caso migliore.
___
### Ricerca binaria

Alternativamente, è possibile utilizzare un algoritmo di **ricerca binaria**, più efficiente ma che richiede una condizione per poter essere applicata: l'*array* su cui è operata la ricerca deve essere ordinato. L'algoritmo può essere riassunto nei seguenti passaggi:
- viene ispezionato l'elemento centrale *m* dell'*array* A: se corrisponde all'elemento v, si restituisce immediatamente l'indice di *m*; se v < *m*, si procederà al prossimo passaggio considerando solo la prima metà dell'*array*; se v > *m*, si procederà al prossimo passaggio considerando solo la seconda metà dell'*array*;
- viene ripetuto il primo passaggio, finché la lista non sarà ridotta a un solo elemento, e se l'unico elemento rimasto corrisponde a v viene ritornato l'indice trovato, altrimenti l'elemento v non si trova nell'*array* e si ritorna -1.

Di seguito, un esempio di pseudocodice che implementa questo algoritmo:

```
def ricerca_binaria(A, v):
	a = 0                    # primo indice di A
	b = len(A) - 1           # ultimo indice di A
	m = (a + b) // 2         # indice a metà di A

	while A[m] != v:
		if A[m] > v:
			b = m - 1        # si analizza la metà inferiore
		else:
			a = m + 1        # si analizza la metà superiore

		if a > b:            # si verifica solo se v non è in A
			return -1

		m = (a + b) // 2

	return m
```

Per ottenere il costo computazionale di questo algoritmo, analizziamo il ciclo *while*: supponendo che l'elemento v venga trovato alla *k*-esima iterazione del ciclo, a ogni iterazione la nuova "lunghezza" di A, o meglio della sezione analizzata di A, è pari a
$$\frac{n}{2^k}$$
dove *k* è il numero dell'iterazione corrente, mentre *n* è la lunghezza dell'*array* (come specificato a inizio capitolo). Nel caso peggiore, ossia quello in cui rimane solo v nell'*array* analizzato, tale valore sarà uguale a 1. Si ha:
$$\frac{n}{2^k} = 1 \Rightarrow n = 2^k \Rightarrow k = log_2(n)$$
Dunque, nel caso peggiore si avranno *log₂n* iterazioni; questa informazione ci permette di ottenere il **costo computazionale del caso peggiore**, che sarà pari a:
$$T(n)_{peggiore} = θ(1) + (log_2(n) ⋅ θ(1)) + θ(1) = θ(log(n))$$
Il **costo computazionale del caso migliore** (ossia il caso in cui si trova v al primissimo passaggio dell'algoritmo), invece, è pari a ***θ(1)***.

Anche in questo caso, come per la ricerca sequenziale, caso peggiore e caso migliore hanno costi computazionali non corrispondenti, ed è dunque opportuno calcolare il **costo medio** di questo algoritmo. Per comodità, assumiamo dei presupposti:
- supponiamo che il numero di elementi dell'*array* sia una potenza di 2;
- supponiamo che v sia presente nell'*array*;
- supponiamo che tutte le posizioni dell'*array* abbiano la stessa probabilità di contenere v.

Alla prima iterazione dell'algoritmo, c'è un'unica posizione raggiungibile, ossia quella centrale; alla seconda iterazione, ce ne sono 2, ossia quella centrale della metà inferiore e quella centrale della metà superiore; alla terza iterazione, ce ne sono 4; e così via. Dunque, le posizioni raggiungibili alla *k*-esima iterazione sono:
$$n(k) = 2^{k - 1}$$
Avendo assunto che ogni posizione abbia la stessa probabilità di contenere il valore v, la probabilità relativa a ogni posizione è:
$$\frac{n(k)}{n} = \frac{2^{k - 1}}{n}$$
Di conseguenza, il numero medio di iterazioni dell'algoritmo di ricerca binaria è:
$$\sum_{k = 0}^{log(n)}\left(k ⋅ \frac{2^{k - 1}}{n} \right) = \frac{1}{n} ⋅  \sum_{k = 0}^{log(n)}(k ⋅ 2^{k - 1}) = \frac{(log(n) - 1)2^{log(n)} + 1}{n} = log(n) - 1 + \frac{1}{n} = θ(log(n))$$