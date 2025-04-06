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
	n = len(A)                   # θ(1)
	max = A[1]                   # θ(1)

	for i in range(1, n):        # n - 1 iterazioni
		if A[i] > max:           # θ(1) per la verifica della condizione
			max = A[i]           # θ(1)

	return max                   # θ(1)
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
	somma = 0                        # θ(1)
	
	for i in range(1, n + 1):        # n iterazioni
		somma += i                   # θ(1)
		
	return somma                     # θ(1)
```

Seguendo gli stessi ragionamenti applicati nell'esempio precedente, arriviamo facilmente alla conclusione che il costo computazionale di questo algoritmo è:
$$T(n) = θ(1) + (n ⋅ θ(1) + θ(1)) + θ(1) = θ(n)$$
Notiamo, tuttavia, questa operazione è facilmente semplificabile ricordando la regola che permette di calcolare in maniera diretta la somma dei primi *n* interi:
$$\sum_{k=0}^{n} = \frac{n(n + 1)}{2}$$
È possibile, dunque, riscrivere l'algoritmo in maniera molto più ottimizzata:

```
def calcola_somma_2(n):
	somma = n * (n + 1) / 2        # θ(1)
	return somma                   # θ(1)
```

Il costo complessivo di questa nuova versione dell'algoritmo è molto minore:
$$T(n) = θ(1) + θ(1) = θ(1)$$
___
### Esempio 3: valutazione di un polinomio in un punto

Il terzo esempio è un algoritmo che **valuta un polinomio** espresso nella forma
$$\sum_{i = 0}^{n}a_i x^i$$
dove ogni *a* corrisponde ad un elemento di un *array* dato in *input* assieme al valore assunto dalla variabile *x*. Ad esempio, il polinomio *x² - 4x + 5* verrà espresso nell'*array* [5, -4, 1]. Lo pseudocodice di questo algoritmo è il seguente:

```
def calcola_polinomio_1(A, x):
	somma = 0                                 # θ(1)
	
	for i in range(len(A)):                   # len(A) iterazioni
		potenza = 1                           # θ(1)
		for j in range(i):                    # 0, 1, 2, ..., len(A) - 1 iterazioni
			potenza = x * potenza             # θ(1)
		somma = somma + A[i] * potenza        # θ(1)
	
	return somma                              # θ(1)
```

Qui la situazione è più complessa degli esempi precedenti, principalmente per la presenza di due cicli *for* annidati, in cui il contatore del secondo dipende da quello del primo. Ciò significa che il ciclo *for* interno verrà eseguito prima 0 volte, poi una volta, poi due volte e così via, finché il contatore del ciclo *for* esterno non raggiungerà *len(A)*. Questa casistica è perfettamente esprimibile tramite la seguente sommatoria:
$$\sum_{i = 0}^{n}θ(i)$$
Nell'ambito del calcolo della notazione asintotica, le sommatorie godono della proprietà per cui esse sono intercambiabili con la notazione utilizzata. Infatti, la sommatoria precedente è riscrivibile nel modo seguente:
$$\sum_{i = 0}^{n}θ(i) = θ(\sum_{i = 0}^{n}i) = θ(\frac{n(n + 1)}{2}) = θ(n²)$$
Dunque, il costo complessivo dell'algoritmo sarà:
$$T(n) = θ(1) + \sum_{i = 0}^{n}(θ(1) + θ(i) + θ(1)) + θ(1) = θ(1) + θ(n²) + θ(1) = θ(n²)$$
Tuttavia, è possibile ottimizzare questo algoritmo: infatti, piuttosto che ricalcolare la potenza ad ogni termine del polinomio, è possibile evitare completamente questa operazione ed eliminare anche il ciclo *for* annidato. Lo pseudocodice per l'algoritmo ottimizzato è il seguente:

```
def calcola_polinomio_2(A, x):
	somma = 0                                  # θ(1)
	
	for indice, numero in enumerate(A):        # len(A) iterazioni
		somma += numero * x ** indice          # θ(1)
	
	return somma                               # θ(1)
```

Il costo complessivo di questa versione dell'algoritmo è:
$$T(n) = θ(1) + n ⋅ θ(1) + θ(1) = θ(n)$$
___
### Esempio 4: analisi di caso migliore e caso peggiore

Il quarto esempio è un algoritmo che presenta esplicitamente un **caso migliore** e un **caso peggiore** relativamente agli *input*. Lo pseudocodice è il seguente:

```
def caso_migliore_peggiore(n):
	if n < 0:                 # θ(1) per la verifica della condizione
		n = -n                # θ(1)
	
	while n:                  # se n è pari, itera finché n = 0
		if n % 2 == 1:        # θ(1) per la verifica della condizione
			return 1          # θ(1)
		n -= 2                # θ(1)
	
	return 0                  # θ(1)
```

Analizziamo il comportamento del ciclo *while*: se *n* è dispari, la condizione `n % 2 == 1` restituirà `True`, eseguendo l'istruzione `return` e terminando istantaneamente il ciclo; se *n* è pari, allora a ogni iterazione del ciclo si sottrarrà 2 al numero, finché non si arriverà a 0 (condizione necessaria per terminare il ciclo). Dunque, la condizione necessaria a terminare il ciclo *while* è che:
$$n - 2k = 0, \mbox{dove } k \mbox{ è il numero di iterazioni}$$

Nel primo caso, il costo del ciclo sarà ***θ(1)***; nel secondo caso, invece, il costo sarà pari a ***θ(n)***, in quanto:
$$n - 2k = 0 \Rightarrow n = 2k \Rightarrow k = \frac{n}{2}$$
$$θ\left(\frac{n}{2} \right) = \frac{1}{2} ⋅ θ(n) = θ(n)$$

Possiamo quindi dire che il costo computazionale complessivo dell'algoritmo è il seguente:
$$T(n) = \begin{cases} θ(1), & \mbox{se }n\mbox{ è dispari (caso migliore)} \\ θ(n), & \mbox{se }n\mbox{ è pari (caso peggiore)}\end{cases}$$
___
### Esempio 5: iterazioni con radice

Il quinto esempio è un algoritmo in cui il numero di iterazioni di un suo ciclo corrisponde ad una **radice**. Lo pseudocodice è il seguente:

```
def iterazioni_radice(n):
	n = abs(n)              # θ(1)
	x, r = 0                # θ(1)
	
	while x * x < n:        # itera finché x² = n
		x += 1              # θ(1)
		r *= 3 * x          # θ(1)

	return r                # θ(1)
```

Analizziamo il comportamento del ciclo *while*: ad ogni iterazione di quest'ultimo, si aggiunge 1 ad *x*, finché il suo quadrato non sarà maggiore o uguale di *n*. Dunque, possiamo affermare che il ciclo terminerà quando:
$$k ⋅ k = n$$
Genericamente, il numero di iterazioni effettuate dal ciclo sarà:
$$k^2 = n \Rightarrow k = \sqrt{n}$$
Il costo computazionale complessivo dell'algoritmo sarà quindi pari a:
$$T(n) = θ(1) + \sqrt{n} ⋅ θ(1) + θ(1) = θ(\sqrt{n})$$
___
### Esempio 6: iterazioni logaritmiche

Il sesto esempio è un algoritmo in cui il numero di iterazioni di un suo ciclo corrisponde ad un **logaritmo**. Lo pseudocodice è il seguente:

```
def iterazioni_log(n):
	n = abs(n)            # θ(1)
	x, r = 0              # θ(1)

	while n > 1:          # itera finché n = 1
		r += 2            # θ(1)
		n = n // 3        # θ(1)

	return r              # θ(1)
```

Analizziamo il comportamento del ciclo *while*: ad ogni iterazione di quest'ultimo, *n* viene diviso per 3, finché il risultato di questa divisione non sarà minore o uguale a 1. Dunque, possiamo affermare che il ciclo terminerà quando:
$$\frac{n}{3^k} = 1$$
Genericamente, il numero di iterazioni effettuate dal ciclo sarà:
$$\frac{n}{3^k} = 1 \Rightarrow n = 3^k \Rightarrow k = log_3(n)$$
Il costo computazionale complessivo dell'algoritmo sarà quindi pari a:
$$T(n) = θ(1) + log_3(n) ⋅ θ(1) + θ(1) = θ(log(n))$$
___
### Esempio 7: iterazioni esponenziali

Il settimo esempio è un algoritmo in cui il numero di iterazioni di un suo ciclo comprende un **esponenziale**. Lo pseudocodice è il seguente:

```
def iterazioni_exp(n):
	n = abs(n)                # θ(1)
	x, t = 1                  # θ(1)

	for i in range(n):        # n iterazioni
		t *= 3                # θ(1)

	t -= 1                    # θ(1)

	while t >= x:             # itera finché t = x
		x += 2                # θ(1)
		t -= 2                # θ(1)

	return x                  # θ(1)
```

Analizziamo il comportamento dei cicli presenti, partendo dal ciclo *for*: questo ciclo viene eseguito *n* volte, e ad ogni iterazione *t* (inizializzato ad 1) viene moltiplicato per 3, portando ad avere, alla fine del ciclo, che:
$$t = 3^n$$
Invece, per quanto riguarda il ciclo *while*, ad ogni iterazione si aggiunge 2 ad *x* e si sottrae 2 a *t*, finché *t* non sarà minore o uguale a *x*. Dunque, possiamo affermare che il ciclo terminerà quando:
$$3^n - 1 - 2k = 1 + 2k$$
Genericamente, il numero di iterazioni effettuate dal ciclo sarà:
$$3^n - 1 - 2k = 1 + 2k \Rightarrow 3^n - 2 = 4k \Rightarrow k = \frac{3^n - 2}{4}$$
Il costo computazionale complessivo dell'algoritmo sarà quindi pari a:
$$T(n) = θ(1) + n ⋅ θ(1) + \frac{3^n - 2}{4} ⋅ θ(1) + θ(1) = θ(n) + θ(3^n) = θ(3^n)$$
___
### Esempio 8: iterazioni con logaritmi di logaritmi

L'ottavo esempio è un algoritmo in cui il numero di iterazioni di un suo ciclo comprende un **logaritmo di logaritmo**. Lo pseudocodice è il seguente:

```
def iterazioni_loglog(n):
	n = abs(n)           # θ(1)
	p = 2                # θ(1)

	while n >= p:        # itera finché n = p
		p *= p           # θ(1)

	return p             # θ(1)
```

Analizziamo il comportamento del ciclo *while*: ad ogni iterazione, *p* (che viene inizializzato a 2) viene moltiplicato per sé stesso, finché *n* non sarà minore o uguale a *p*. Dunque, possiamo affermare che il ciclo terminerà quando:
$$2^{2^k} = n$$
Genericamente, il numero di iterazioni effettuate dal ciclo sarà:
$$2^{2^k} = n \Rightarrow 2^k = log_2(n) \Rightarrow k = log_2(log_2(n))$$
Il costo computazionale complessivo dell'algoritmo sarà quindi pari a:
$$T(n) = θ(1) + log_2(log_2(n)) ⋅ θ(1) + θ(1) = θ(log(log(n)))$$
___
### Esempio 9: cicli *while* e *for* annidati

Il nono esempio è un algoritmo il cui pseudocodice presenta dei **cicli *while* e *for* annidati**. Lo pseudocodice è il seguente:

```
def while_for_annidati(n):
	n = abs(n)                    # θ(1)
	s = n                         # θ(1)
	p = 2                         # θ(1)
	i, r = 1                      # θ(1)

	while s >= 1:                 # itera finché s = 1
		s = s // 5                # θ(1)
		p += 2                    # θ(1)

	p *= p                        # θ(1)

	while i * i * i < n:          # itera finché i³ = n
		for j in range(p):        # (2 + 2log₅(n))² iterazioni
			r += 1                # θ(1)
		i += 1                    # θ(1)

	return r                      # θ(1)
```

Analizziamo il comportamento del primo ciclo *while*: ad ogni iterazione, *s* (inizializzata come *n*) viene divisa interamente per 5, mentre il valore di *p* (inizializzata come 2) viene incrementato di 2, finché *s* non sarà minore o uguale a 1. Dunque, possiamo affermare che il ciclo terminerà quando:
$$\frac{n}{5^k} = 1$$
Genericamente, il numero di iterazioni effettuate dal primo ciclo *while* sarà:
$$\frac{n}{5^k} = 1 \Rightarrow n = 5^k \Rightarrow k = log_5(n)$$
È utile analizzare anche il comportamento di *p* nel ciclo appena visto: ad ogni iterazione dello stesso, essa viene incrementata di 2, dunque possiamo affermare che alla fine del ciclo, e in seguito all'istruzione `p *= p`, si avrà che:
$$p = (2 + 2log_5(n))^2$$
Invece, per quanto riguarda il secondo ciclo *while*, ad ogni iterazione viene eseguito il ciclo *for* annidato, e viene incrementata di 1 *i* (inizializzata come 1). Dunque, possiamo affermare che il ciclo terminerà quando:
$$(k + 1)^3 = n$$
Genericamente, il numero di iterazioni effettuate dal secondo ciclo *while* sarà:
$$(k + 1)^3 = n \Rightarrow k + 1 = \sqrt[3]{n} \Rightarrow k = \sqrt[3]{n} - 1$$
Infine, analizzando il ciclo *for* annidato all'interno del secondo ciclo *while*, si evince subito che esso viene eseguito *p* volte ad ogni iterazione del ciclo *while*. Dunque, il numero totale di iterazioni effettuate dal ciclo *for* sarà:
$$k = (\sqrt[3]{n} - 1)(2 + 2log_5(n))^2$$
Il costo computazionale complessivo dell'algoritmo sarà quindi pari a:
$$T(n) = θ(1) + log_5(n) ⋅ θ(1) + (\sqrt[3]{n} - 1)((2 + 2log_5(n))^2 ⋅ θ(1) + θ(1)) + θ(1)  = θ(1) + θ(log(n)) + (\sqrt[3]{n} - 1)(θ(log^2(n)) + θ(1)) + θ(1)$$
$$= θ(1) + θ(log(n)) + θ(\sqrt[3]{n} ⋅ log^2(n)) + θ(\sqrt[3]{n}) = θ(\sqrt[3]{n} ⋅ log^2(n))$$
