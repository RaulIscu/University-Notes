## Cos'è un algoritmo ricorsivo?

Nel capitolo precedente si è approfondito il problema della [[IAA_04 - Ricerca|ricerca]], e in particolare uno degli algoritmi analizzati è quello della [[IAA_04 - Ricerca#Ricerca binaria|ricerca binaria]]: l'implementazione proposta in precedenza è perfettamente iterativa, ma è possibile implementare lo stesso algoritmo anche utilizzando la "**ricorsione**". Avendo un array $A$ e l'elemento cercato $v$, in parole povere possiamo effettuare la ricerca binaria anche seguendo i seguenti passaggi:
- se $A$ è vuoto, l'elemento $v$ non è sicuramente contenuto al suo interno, quindi restituire subito $-1$;
- ispezionare l'elemento centrale dell'array $A$, e se corrisponde a $v$ restituire il suo indice;
- se l'elemento considerato non è quello cercato, confrontarlo con quest'ultimo per vedere se è minore o maggiore;
- se $v$ è minore dell'elemento considerato, eseguire nuovamente lo stesso algoritmo sulla metà inferiore di $A$; invece, se $v$ è più grande dell'elemento considerato, farlo sulla metà superiore.

L'aspetto fondamentale di questo approccio, che lo differenzia dalla soluzione precedente, è il concetto di **un algoritmo che "riapplica" sé stesso su un sottoproblema**, ossia una versione più semplice del problema iniziale: è questa, sostanzialmente, la definizione di "**algoritmo ricorsivo**".

> Un algoritmo è detto "**ricorsivo**" quando è espresso in termini di sé stesso.

Per poter essere ben formulato, un algoritmo ricorsivo deve necessariamente presentare alcune **proprietà**:
- la soluzione del problema iniziale deve essere costruita risolvendo, in modo ricorsivo, **uno o più sottoproblemi di dimensione minore**, e **combinando poi queste soluzioni**;
- la successione dei sottoproblemi, che saranno man mano più piccoli e semplici, deve sempre convergere a un sottoproblema che definiamo "**caso base**", o anche "**condizione di terminazione**", il cui risultato è noto e che termina la ricorsione.

La presenza di un caso base risulta essere fondamentale per il buon funzionamento di un algoritmo ricorsivo: infatti, in sua assenza, l'esecuzione dell'algoritmo genererà una catena infinita di chiamate ricorsive, che non avrà termine e non porterà ad alcuna soluzione. Del resto, **è possibile prevedere anche più di un caso base**, finché ci si assicuri che almeno uno dei casi base previsti verrà sempre incontrato.

In generale, **qualsiasi problema risolvibile con un algoritmo ricorsivo può essere risolto anche con un algoritmo iterativo**. È dunque legittimo chiedersi: quando conviene utilizzare l'una o l'altra soluzione? In linea di massima, si possono seguire queste regole:
- si preferisce un **algoritmo ricorsivo** quando la formulazione del problema è prettamente ricorsiva, o quando la soluzione iterativa risulta molto più complessa o non evidente da implementare;
- si preferisce un **algoritmo iterativo** quando la soluzione iterativa risulta essere semplice e chiara quanto (o più di) quella ricorsiva, o quando si attribuisce maggiore importanza all'efficienza dell'algoritmo.

Soffermiamoci in particolare su quest'ultimo punto: **generalmente, un algoritmo ricorsivo ha maggiori esigenze in termini di memoria rispetto a quelli iterativi**. Infatti, ad ogni chiamata ricorsiva servirà della memoria aggiuntiva per ricaricare il codice, per i vari parametri e per le variabili locali. Un algoritmo ricorsivo mal progettato esaurisce con estrema rapidità la memoria disponibile, e può addirittura risultare in una sua terminazione forzata.

Un classico esempio di algoritmo ricorsivo molto impegnativo a livello computazionale e di utilizzo della memoria è quello utilizzato per il calcolo dell'$n$-esimo numero di Fibonacci:

```
def fibonacci(n):
	if n <= 1:
		return n
	
	return (fibonacci(n - 1) + fibonacci(n - 2))
```

Come è facile notare, in questo caso ogni iterazione dell'algoritmo genera addirittura altre due chiamate ricorsive, portando a un'articolazione più complessa delle chiamate e a una crescita pressoché esponenziale del tempo di esecuzione e dell'utilizzo della memoria. Per questo problema, seppur a livello di codice l'algoritmo risulta essere molto semplice, converrà implementare una soluzione iterativa come la seguente:

```
def fibonacci_iter(n):
	if n <= 1:
		return n
	
	fib_prec_prec = 0
	fib_prec = 1
	
	for i in range(2, n + 1):
		fib_prec_prec, fib_prec = fib_prec, fib_prec_prec + fib_prec
	
	return fib_prec
```

Questa implementazione ha costo computazionale pari a $\Theta(n)$ e costo in termini di spazio pari a $\Theta(1)$, risultando molto più vantaggioso della sua controparte ricorsiva.

##### Esempio n°1: calcolo del fattoriale di un intero $n$

Un esempio classico di algoritmo ricorsivo è quello utilizzato per calcolare il **fattoriale di un intero $n$**. Assumendo che $n$ sia un numero intero non negativo, una soluzione iterativa del problema potrebbe essere la seguente:

```
def fattoriale_iter(n):
	res = 1
	
	for i in range(1, n + 1):
		res *= i
	
	return res
```

Come si può facilmente notare, in nessun punto del suo corpo tale algoritmo "riapplica" sé stesso, infatti si tratta di un algoritmo non ricorsivo. Una soluzione alternativa, che implementa la ricorsione, è la seguente:

```
def fattoriale_ric(n):
	if (n == 0):
		return 1
	
	return n * fattoriale_ric(n - 1)
```

In questo caso, vediamo che l'algoritmo "riapplica" sé stesso per risolvere il problema. Entrambe le proprietà fondamentali di un algoritmo ricorsivo vengono rispettate: la soluzione del problema iniziale viene ottenuta risolvendo una successione di sottoproblemi via via più semplici (il numero $n$ viene diminuito di $1$ ad ogni iterazione), e tale successione converge a un caso base (se $n=0$, il risultato del fattoriale è $1$).
___
##### Esempio n°2: ricerca sequenziale ricorsiva di un elemento $v$

È possibile fornire una soluzione ricorsiva anche per il problema della **[[IAA_04 - Ricerca#Ricerca sequenziale|ricerca sequenziale]]**, affrontato nel capitolo precedente. Ponendo `n = len(A) - 1`:

```
def ricerca_sequenziale_ric(A, v, n):
	if A[n] == v:
		return n
	
	if n == 0:
		return -1
	else:
		return ricerca_sequenziale_ric(A, v, n - 1)
```

Anche in questo caso, possiamo trovare un caso base (se l'elemento considerato corrisponde a $v$, restituire tale elemento). Nel caso in cui l'iterazione attuale non rientri nel caso base, si riapplica lo stesso algoritmo andando ad analizzare l'elemento precedente nell'array $A$, finché non si esauriranno gli elementi dello stesso.
___
##### Esempio n°3: ricerca binaria ricorsiva di un elemento $v$

L'algoritmo di ricerca binaria si presta molto a un'implementazione ricorsiva. Ponendo `i_min = 0` e `i_max = len(A)`:

```
def ricerca_binaria_ric(A, v, i_min, i_max):
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

Troviamo un caso base anche in questo algoritmo (se l'elemento considerato corrisponde a $v$, restituire tale elemento). Nel caso in cui l'iterazione attuale non rientri in nessuno dei due casi base, si riapplica lo stesso algoritmo andando ad analizzare l'una o l'altra metà dell'array $A$ preso in input.
___
## Equazioni di ricorrenza

Torniamo a parlare dell'algoritmo utilizzato per calcolare l'$n$-esimo numero di Fibonacci, visto nel [[IAA_05 - Ricorsione#Cos'è un algoritmo ricorsivo?|paragrafo precedente]], e in particolare della sua versione ricorsiva:

```
def fibonacci(n):
	if n <= 1:
		return n
	
	return (fibonacci(n - 1) + fibonacci(n - 2))
```

Abbiamo già stabilito che eseguire questo algoritmo risulta molto dispendioso, sia a livello di tempo di esecuzione che di memoria occupata, al crescere di $n$. Ma come possiamo **calcolare il costo computazionale di un algoritmo ricorsivo**? 

Proviamo a farlo utilizzando la metodologia che abbiamo usato per gli [[IAA_03 - Costo computazionale#Come calcolare il costo computazionale di un algoritmo?|algoritmi iterativi]] visti in precedenza: la prima istruzione incontrata è un'istruzione condizionale, che avrà costo $\Theta(1)$ (in particolare, $\Theta(1)$ per la valutazione della condizione e $\Theta(1)$ per il suo corpo); l'istruzione di ritorno, invece, è più particolare, in quanto risulta avere costo $T(n -1) +T(n - 2)$, dove $T(n)$ rappresenta il costo computazionale complessivo dell'algoritmo. Provando a sviluppare questa espressione, si nota che, come l'algoritmo considerato, anche la funzione di costo riferita ad esso è ricorsiva. È possibile, dunque, ottenere una stima accurata del costo computazionale di un algoritmo ricorsivo?

Ciò è possibile utilizzando le cosiddette "**equazioni di ricorrenza**", delle funzioni matematiche che esprimono chiaramente il costo di un algoritmo ricorsivo. Un'equazione di ricorrenza ben formulata contiene, tra le sue parti, il costo dell'algoritmo in corrispondenza dei suoi **casi base**, insieme al costo dell'algoritmo nel **caso generale**. In particolare, la parte generale dell'equazione di ricorrenza, quindi quella che definisce $T(n)$, **deve essere costituita dalla somma di almeno due addendi, di cui almeno uno contiene la parte ricorsiva mentre l'altro rappresenta il costo di tutto ciò che viene eseguito fuori dalla chiamata ricorsiva**.

Per comprendere al meglio come utilizzare le equazioni di ricorrenza, vediamo un esempio. Consideriamo nuovamente la versione ricorsiva dell'algoritmo di calcolo di un fattoriale:

```
def fattoriale(n):
	if n == 0:
		return 1
	
	return n * fattoriale(n - 1)
```

Come sappiamo, questo algoritmo presenta un caso base, che corrisponde al caso in cui il numero $n$ è pari a $0$: in quel caso il costo computazionale è pari a $\Theta(1)$. In generale, invece, viene eseguito l'algoritmo nella sua interezza, che vediamo avere costo $\Theta(1) + T(n - 1)$. Dunque, possiamo formalizzare l'equazione di ricorrenza dell'algoritmo considerato nel modo seguente:
$$\begin{cases} T(0) = \Theta(1) \\ T(n) = \Theta(1) + T(n - 1) \end{cases}$$
Tuttavia, nel concreto questa formalizzazione chiarifica solo la situazione in cui ci si trova, ma non fornisce uno strumento per calcolare effettivamente il costo computazionale. Per fare ciò, si dovrà **"risolvere" l'equazione di ricorrenza ottenuta**, e questo può essere fatto utilizzando uno di **4 metodi**:
- il **[[IAA_05 - Ricorsione#Metodo iterativo|metodo iterativo]]**;
- il **[[IAA_05 - Ricorsione#Metodo di sostituzione|metodo di sostituzione]]**;
- il **[[IAA_05 - Ricorsione#Metodo dell'albero|metodo dell'albero]]**;
- il **[[IAA_05 - Ricorsione#Metodo principale|metodo principale]]**, detto anche "**master theorem**".
___
## Metodo iterativo

Per risolvere un'equazione di ricorrenza utilizzando il **metodo iterativo**, quello che si deve fare è **sviluppare l'[[IAA_05 - Ricorsione#Equazioni di ricorrenza|equazione di ricorrenza]] ed esprimerla come somma di termini dipendenti da $n$ e dal caso base**. Si tratta di un metodo basato soprattutto sui calcoli algebrici, più meccanico e dispendioso di altri.

##### Esempio n°1

Per comprendere meglio il funzionamento di questo metodo, consideriamo la seguente equazione di ricorrenza:
$$\begin{cases} T(1)=\Theta(1)\\T(n)=\Theta(1)+T(n-1) \end{cases}$$
Sviluppando ripetutamente l'addendo rappresentante la parte ricorsiva dell'algoritmo nel secondo membro dell'equazione, si ottiene:
$$\begin{align} T(n)&=\Theta(1)+\underline{T(n-1)}\\&=\Theta(1)+\Theta(1)+\underline{T(n-2)}\\&=\Theta(1)+\Theta(1)+\Theta(1)+\underline{T(n-3)}\\&\dots \\&= k\cdot \Theta(1)\,+\,T(n-k)\end{align}$$
Abbiamo dunque generalizzato il costo computazionale $T(n)$ ipotizzando un numero $k$ di chiamate ricorsive; come sappiamo, però, dopo un determinato numero di ricorsioni l'equazione di ricorrenza convergerà al suo caso base, che nel nostro esempio è $T(1)$, dunque possiamo affermare che la catena di ricorsione continua finché $n-k=1$, da cui segue che:
$$n-k=1\,\,\,\Rightarrow\,\,\,k=n-1$$
Trovato, dunque, il numero $k$ di chiamate ricorsive che vengono eseguite in funzione di $n$, ci basterà sostituire $k$ nella generalizzazione trovata poco fa per trovare il costo computazionale generico dell'algoritmo:
$$\begin{align} T(n)&=k\cdot \Theta(1)+T(n-k)\\&=(n-1)\,\Theta(1) +T(n-(n-1))\\&=\Theta(n)+T(1)\\&=\Theta(n)+\Theta(1)\\&=\Theta(n)\end{align}$$
___
##### Esempio n°2: ricerca binaria ricorsiva

Vediamo un altro esempio, applicando il metodo iterativo all'equazione di ricorrenza che descrive il [[IAA_03 - Costo computazionale|costo computazionale]] dell'algoritmo ricorsivo di [[IAA_04 - Ricerca#Ricerca binaria|ricerca binaria]]:
$$\begin{cases} T(0)=\Theta(1)\\T(1)=\Theta(1)\\T(n)=\Theta(1)+T\left( \frac{n}{2} \right) \end{cases}$$
Sviluppando ripetutamente l'addendo rappresentante la parte ricorsiva dell'algoritmo nel secondo membro dell'equazione, si ottiene:
$$\begin{align} T(n)&=\Theta(1)+\underline{T\left( \frac{n}{2} \right)}\\&=\Theta(1)+\Theta(1)+\underline{T\left( \frac{n}{4} \right)}\\&=\Theta(1)+\Theta(1)+\Theta(1)+T\left( \frac{n}{8} \right)\\&\dots \end{align}$$
Generalizzando, abbiamo che il costo computazionale dell'algoritmo è esprimibile come:
$$T(n)=k\cdot \Theta(1)+T\left( \frac{n}{2^{k}} \right)$$
dove $k$ è il numero di chiamate ricorsive effettuate. Ora, dato che i casi base si trovano quando $n = 0$ e quando $n=1$, sappiamo che la ricorsione terminerà quando $\frac{n}{2^{k}}=1$, e ciò avviene quando il numero di chiamate ricorsive è:
$$\frac{n}{2^{k}}=1\,\,\,\Rightarrow\,\,\,n=2^{k}\,\,\,\Rightarrow\,\,\,k=\log_{2}(n)$$Dunque, possiamo riscrivere il costo computazionale complessivo $T(n)$ come:
$$T(n) = \log n \cdot \Theta(1)+\Theta(1)=\Theta(\log n)$$
___
##### Esempio n°3: calcolo dei numeri di Fibonacci

Vediamo un terzo esempio, applicando il metodo iterativo all'equazione di ricorrenza che descrive il costo computazionale dell'algoritmo ricorsivo del calcolo dei numeri di Fibonacci:
$$\begin{cases} T(0)=\Theta(1)\\T(1)=\Theta(1)\\T(n)=\Theta(1)+T(n-1)+T(n-2) \end{cases}$$
In questo caso, sviluppare l'addendo rappresentante la parte ricorsiva dell'algoritmo, come abbiamo fatto per gli esempi precedenti, risulta molto più difficile e per niente pratico. Tuttavia, anche se non conviene applicare il metodo iterativo direttamente, possiamo fare due considerazioni:
- $T(n)\le \Theta(1)+2T(n-1)$, e questa disuguaglianza ci permette di derivare un **[[IAA_02 - Notazione asintotica#Notazione $O$|limite asintotico superiore]]**;
- $T(n)\ge \Theta(1)+2T(n-2)$, e questa disuguaglianza ci permette di derivare un **[[IAA_02 - Notazione asintotica#Notazione $ Omega$|limite asintotico inferiore]]**.

Partiamo dalla prima delle due considerazioni. Applicando il metodo iterativo su di essa, si ha che:
$$\begin{align} T(n)&\le\Theta(1)+\underline{2T(n-1)}\\&\le\Theta(1)+2\cdot\Theta(1)+\underline{4T(n-2)}\\&\le\Theta(1)+2\cdot\Theta(1)+4\cdot\Theta(1)+\underline{8T(n-3)}\\&\dots \end{align}$$
Generalizzando:
$$T(n)\le\sum_{i\,=\,0}^{k\,-\,1}(2^{i}\cdot \Theta(1))+2^{k}\cdot T(n-k)$$
dove $k$ è il numero di chiamate ricorsive effettuate. Ora, dato che i casi base si trovano quando $n = 0$ e quando $n=1$, sappiamo che la ricorsione terminerà quando $n-k=1$, e ciò avviene quando il numero di chiamate ricorsive è $k = n-1$. Dunque, possiamo riscrivere la disuguaglianza appena ottenuta come:
$$\begin{align} T(n)&\le\sum_{i\,=\,0}^{n\,-\,2}(2^{i}\cdot \Theta(1))+2^{n-1}\cdot \Theta(1)\\&\le(2^{n-1}-1)\cdot\Theta(1)+2^{n-1}\cdot \Theta(1)\\&\le (2^{n}-1)\cdot \Theta(1)\end{align}$$
Da questa disuguaglianza, ricaviamo infine che:
$$T(n)=O(2^{n})$$
Passiamo, ora, alla seconda delle due considerazioni. Applicando il metodo iterativo su di essa, si ha che:
$$\begin{align} T(n)&\ge \Theta(1)+\underline{2T(n-2)}\\&\ge \Theta(1)+2\cdot \Theta(1)+\underline{4T(n-4)}\\&\ge \Theta(1)+2\cdot \Theta(1)+4\cdot \Theta(1)+\underline{8T(n-6)}\\&\dots \end{align}$$
Generalizzando:
$$T(n)\ge\sum_{i\,=\,0}^{k\,-\,1}(2^{i}\cdot \Theta(1)) + 2^{k}\cdot T(n-2k)$$
dove $k$ è il numero di chiamate ricorsive effettuate. Ora, dato che i casi base si trovano quando $n = 0$ e quando $n = 1$, sappiamo che la ricorsione terminerà quando $n - 2k = 0$ se $n$ è pari o quando $n - 2k = 1$ se $n$ è dispari; per semplicità, assumiamo che in generale valga il primo caso (il comportamento asintotico resta invariato nei due casi), e quindi che la ricorsione termini quando il numero di chiamate ricorsive è $k=\frac{n}{2}$. Dunque, possiamo riscrivere la disuguaglianza appena ottenuta come:
$$\begin{align} T(n)&\ge\sum_{i\,=\,0}^{\frac{n}{2}\,-\,1}(2^{i}\cdot \Theta(1))+2^{\frac{n}{2}}\cdot \Theta(1)\\&\ge (2^{\frac{n}{2}}-1)\cdot\Theta(1)+2^{\frac{n}{2}}\cdot \Theta(1)\\&\ge (2\cdot 2^{\frac{n}{2}}-1)\cdot\Theta(1) \end{align}$$
Da questa disuguaglianza, ricaviamo infine che:
$$T(n)=\Omega (2^{\frac{n}{2}})=\Omega(\sqrt{ 2^{n} })$$
Pur non essendo riusciti a trovare un limite asintotico stretto ben preciso per l'algoritmo considerato, possiamo comunque concludere con sicurezza che il calcolo dei numeri di Fibonacci mediante la ricorsione richiede un tempo esponenziale in funzione di $n$.
___
## Metodo di sostituzione

Per risolvere un'equazione di ricorrenza utilizzando il **metodo di sostituzione**, quello che si deve fare è sostanzialmente **ipotizzare una soluzione** e **verificare la sua correttezza per induzione**. Si tratta di un metodo spesso ostico da utilizzare, la cui difficoltà maggiore risiede proprio nel dover trovare la funzione più vicina alla vera soluzione; in effetti, questo metodo è sconsigliato nella pratica e viene utilizzato soprattutto nelle dimostrazioni.

Per comprendere meglio il funzionamento di questo metodo, applichiamolo nuovamente alla seguente equazione di ricorrenza:
$$\begin{cases} T(1)=\Theta(1)\\T(n)=\Theta(1)+T(n-1) \end{cases}$$
Per risolvere l'equazione, ipotizziamo la soluzione $T(n) = cn$, dove $c$ è una certa costante moltiplicativa. Sostituendo questa ipotesi nella parte generale dell'equazione si ottiene $T(n)=c(n-1)+\Theta(1)$, che risulta effettivamente essere equivalente a $cn$; la stessa equivalenza vale, naturalmente, anche per il caso base.

Un problema che sorge, però, è che non è detto che le due costanti "nascoste" dalla notazione asintotica $\Theta(1)$ siano le stesse, mentre noi vogliamo verificare una soluzione esatta e non asintotica: è necessario, dunque, **eliminare le notazioni asintotiche dall'equazione**. È possibile trasformare l'equazione di ricorrenza, senza cambiarne il significato, nella seguente:
$$\begin{cases} T(1) = d\\T(n)=c+T(n-1) \end{cases}$$
dove $c$ e $d$ sono due costanti positive fissate. A questo punto, ipotizziamo che $T(n)=O(n)$, ossia che valga che $T(n)\le kn$ per una certa costante $k$ non meglio determinata. Per verificare la nostra affermazione, procediamo per induzione su $n$: innanzitutto, nel caso base si ha che $T(1)\le k\cdot 1$, e dunque che $T(1)\le k$, disuguaglianza che è verificata se e solo se $d\le k$; ora, passiamo a formulare la nostra ipotesi induttiva e affermiamo che:
$$T(r)\le kr$$
per ogni $r<n$, volendo dimostrare con il passo induttivo che ciò valga anche per $n$. Sappiamo che $T(n)=T(n-1)+c$, dunque sostituendo nella nostra ipotesi iniziale si ha che:
$$T(n-1)+c\le kn$$
e per la nostra ipotesi induttiva sappiamo anche che $T(r)\le kr$ per ogni $r<n$, dunque anche per $r=n-1$, il che ci porta a riscrivere la disuguaglianza come:
$$k(n-1)+c\le kn\,\,\,\Rightarrow\,\,\,kn-k+c\le kn\,\,\,\Rightarrow\,\,\,-k+c\le 0\,\,\,\Rightarrow\,\,\,c\le k$$
Siamo arrivati, così, alla conclusione che la nostra ipotesi è vera se e solo se viene rispettata anche la disuguaglianza $c\le k$. Dato che, banalmente, esiste sicuramente un valore $k$ tale che $c\le k$ e che $d\le k$, possiamo concludere che abbiamo verificato la nostra ipotesi iniziale, ossia che $T(n)=O(n)$.

In modo del tutto analogo, proviamo a dimostrare che $T(n)=\Omega(n)$, ossia che $T(n)\ge hn$ per una certa costante $h$ non meglio determinata. Procedendo nuovamente per induzione su $n$, pensiamo prima al caso base: si ha $T(1)\ge h$, e poiché sappiamo dall'equazione di ricorrenza che $T(1)=d$, tale disuguaglianza è verificata se e solo se vale anche che $d\ge h$. Ora, passiamo a formulare l'ipotesi induttiva, affermando che:
$$T(r)\ge hr$$
per ogni $r<n$, volendo dimostrare con il passo induttivo che ciò valga anche per $n$. Sappiamo che $T(n)=T(n-1)+c$, dunque sostituendo nella nostra ipotesi iniziale si ha che:
$$T(n-1)+c\ge hn$$
e per l'ipotesi induttiva:
$$h(n-1)+c\ge hn\,\,\,\Rightarrow\,\,\,hn-h+c\ge hn\,\,\,\Rightarrow\,\,\,-h+c\ge 0\,\,\,\Rightarrow\,\,\,c\ge h$$
Dunque la nostra ipotesi iniziale è vera se e solo se vale sia che $d\ge h$ sia che $c \ge h$. Dato che, banalmente, esiste sicuramente un valore $h$ che rispetta queste condizioni, possiamo concludere che abbiamo verificato che $T(n)=\Omega(n)$. Inoltre, avendo verificato sia che $T(n)=O(n)$, sia che $T(n)=\Omega(n)$, di conseguenza si è dimostrato che $T(n)=\Theta(n)$.

È importante sottolineare che questo metodo va utilizzato con cautela, dato che si sarebbero potute formulare ipotesi meno accurate che avrebbero portato a risultati poco utili o fuorvianti: ad esempio, per l'equazione di ricorrenza appena analizzata, avremmo potuto dimostrare che $T(n)=O(n^{2})$ o che $T(n)=O(2^{n})$, e parallelamente che $T(n)=\Omega(\sqrt{ n })$ o che $T(n)=\Omega(\log n)$.
___
## Metodo dell'albero

Per risolvere un'equazione di ricorrenza utilizzando il **metodo dell'albero**, quello che si deve fare è **costruire un "albero di ricorrenza" dell'algoritmo considerato**, in modo da rappresentare graficamente lo sviluppo del suo costo computazionale e valutare, così, quest'ultimo con più facilità.

Prima di procedere, è opportuno fare una piccola parentesi sul concetto di "**albero**", che verrà poi trattato più approfonditamente nel capitolo sulle [[IAA_07 - Strutture dati#Alberi|strutture dati]]. Informalmente, un cosiddetto "**albero binario**" è costituito da un insieme di **nodi**, all'interno del quale vi si trova un nodo particolare detto "**radice**", da cui si sviluppano gli altri; **ogni nodo è collegato al più ad altri due nodi**, con quest'ultimi che vengono definiti "**figli**", mentre il nodo da cui derivano è definito "**padre**"; **ogni nodo può essere figlio di un solo padre**, ossia può derivare solo da un nodo. In generale, se all'interno di un albero ogni nodo può avere al più $m$ figli, allora l'albero verrà detto "**albero $m$-ario**".

Visivamente, si può organizzare un albero partendo dalla radice, e ponendo ciascun nodo più in basso di suo padre: in questo modo, tutti i nodi diventano naturalmente organizzati in **livelli**, numerati in ordine crescente a partire dalla radice (dunque, di norma, la radice si trova al livello $0$). Definiamo come **"altezza" di un albero** la **lunghezza del più lungo cammino dalla radice ad una foglia** (vengono detti "**foglie**" i nodi che non hanno figli); si noti, dunque, che un albero di altezza $h$ dispone di $h+1$ livelli, di norma numerati da $0$ ad $h$.

Un albero nel quale tutti i livelli contengono il massimo numero possibile di nodi è detto "**albero completo**". Avendo un albero binario completo di altezza $h$, sono facilmente derivabili alcune considerazioni:
- il **numero di nodi al livello $i$** è $2^{i}$, dunque **il numero delle foglie dell'albero** è $2^{h}$;
- il **numero di nodi interni**, ossia di tutti i nodi dell'albero che non sono foglie, è pari a $\sum_{i\,=\,0}^{h\,-\,1}2^{i}=\frac{2^{h}\,-\,1}{2\,-\,1}=2^{h}-1$;
- il **numero totale di nodi** dell'albero è pari alla somma del numero di foglie e di nodi interni, dunque $2^{h}+2^{h}-1=2^{h+1}-1$.

Proviamo, con le informazioni fornite finora, a **stimare l'altezza di un albero binario completo contenente $n$ nodi**: poiché l'albero è completo, sappiamo che il numero di nodi $n$ è pari a:
$$n\,=\,2^{h+1}-1$$
dove $h$ è l'altezza dell'albero. Di conseguenza, possiamo affermare che:
$$\log(n+1)\,=\,\log(2^{h+1})\,=\,h+1$$
da cui si deriva che:
$$h\,=\,\log(n+1)-1\,=\,\log(n+1)-\log(2)\,=\,\log\left( \frac{n+1}{2} \right)$$
Possiamo facilmente generalizzare tutte le osservazioni e i calcoli visti finora, facendoli valere per qualsiasi albero $m$-ario completo con $m>2$, dunque:
- il **numero di nodi al livello $i$** è $m^{i}$, dunque **il numero delle foglie dell'albero** è $m^{h}$;
- il **numero di nodi interni**, ossia di tutti i nodi dell'albero che non sono foglie, è pari a $\sum_{i\,=\,0}^{h\,-\,1}m^{i}=\frac{m^{h}\,-1}{m\,-\,1}$;
- il **numero totale di nodi** dell'albero è pari alla somma del numero di foglie e di nodi interni, dunque $m^{h}+\frac{m^{h}\,-\,1}{m\,-\,1}=\frac{m^{h+1}\,-\,1}{m\,-\,1}$;
- avendo $n$ nodi, l'**altezza** dell'albero è pari a $\Theta(\log_{m}n)$.

A questo punto, torniamo a parlare del metodo dell'albero. **Ogni nodo dell'albero di ricorrenza corrisponderà alla soluzione di un problema di una certa dimensione**; esso riporta il costo della ricombinazione delle soluzioni parziali, e **ha tanti figli quanti sono i sottoproblemi** in cui il problema relativo al nodo stesso è scomposto ricorsivamente.

##### Esempio

Per comprendere meglio il funzionamento di questo metodo, applichiamolo alla seguente equazione di ricorrenza:
$$\begin{cases} T(1)=\Theta(1)\\T(n)=2T\left( \frac{n}{2} \right)+\Theta(n^{2}) \end{cases}$$
Per iniziare a costruire l'albero di ricorrenza, partiamo dalla radice e dai suoi figli, che corrispondono sostanzialmente alla prima iterazione dell'algoritmo:

![[metodo_albero_esempio.png]]

In questo albero, sulla radice si trova il costo computazionale della prima iterazione della parte non ricorsiva dell'algoritmo (in questo caso, $\Theta(n^{2})$), e i due figli rappresentano le due chiamate ricorsive effettuate, che lavoreranno su un sottoproblema di dimensione minore (in questo caso, $\frac{n}{2}$ per entrambe le chiamate). In seguito, per proseguire con la creazione dell'albero, si ripeterà a oltranza lo stesso procedimento su ciascuno dei figli, fino ad arrivare alle foglie, che corrispondono ai casi base e, perciò, non hanno figli. L'albero di ricorrenza ottenuto dovrebbe svilupparsi in qualcosa del genere:

![[metodo_albero_esempio1.png]]

Una volta completato l'albero, **il costo computazionale è dato dalla somma dei costi di tutti i livelli** di cui è costituito. Si noti che, concretamente, **il metodo dell'albero necessita degli stessi identici calcoli algebrici utilizzati per il [[IAA_05 - Ricorsione#Metodo iterativo|metodo iterativo]]**. Nel nostro esempio:
$$\begin{align} &\text{livello 0: } \Theta(n^{2})\\&\text{livello 1: }\, 2\cdot \Theta\left( \left( \frac{n}{2} \right)^{2} \right) \,=\, \Theta\left( \frac{n^{2}}{4} + \frac{n^{2}}{4} \right)\,=\, \Theta\left( \frac{n^{2}}{2} \right) \\&\text{livello 2: }\, 4\cdot \Theta\left( \left( \frac{n}{4} \right)^{2} \right) \,=\, \Theta\left( \frac{n^{2}}{16}+\frac{n^{2}}{16}+\frac{n^{2}}{16}+\frac{n^{2}}{16} \right) \,=\, \Theta\left( \frac{n^{2}}{4} \right) \\&\dots\\&\text{livello }i\text{: }\,2^{i}\cdot \Theta\left( \left( \frac{n}{2^{i}} \right)^{2} \right)\,=\,\Theta\left( \frac{n^{2}}{2^{i}} \right) \end{align}$$
e la catena di chiamate ricorsive continuerà finché $\frac{n}{2^{k}}=1$, che corrisponde al caso base dell'equazione di ricorrenza. Sfruttando questa condizione, possiamo esplicitare il numero massimo $k$ di livelli per l'albero di ricorrenza:
$$\frac{n}{2^{k}}=1\,\,\,\Rightarrow\,\,\,n = 2^{k}\,\,\,\Rightarrow\,\,\,k=\log n$$
Dunque, ricordando il modo per calcolare il numero di nodi di un albero $m$-ario completo, otteniamo che il costo totale è dato da:
$$\sum_{i\,=\,0}^{\log n}\Theta\left( \frac{n^{2}}{2^{i}} \right)=n^{2}\,\sum_{i\,=\,0}^{\log n}\Theta\left( \frac{1}{2^{i}} \right)=n^{2}\cdot \Theta(1)=\Theta(n^{2})$$
___
## Metodo principale

Per risolvere un'equazione di ricorrenza utilizzando il **metodo principale**, basterà **applicare una formula fissata**. Si tratta di un metodo molto vantaggioso, dato che fornisce una soluzione meccanica e "fissa", ma allo stesso tempo l'utilizzo di questo approccio è limitato esclusivamente alle equazioni di ricorrenza che si presentano nella forma:
$$\begin{cases} T(1)=\Theta(1)\\T(n)=a\cdot T\left( \frac{n}{b} \right)+f(n) \end{cases}$$
dove $a$ e $b$ sono due costanti positive con $a\ge 1$ e $b > 1$, mentre $f(n)$ è una qualsiasi funzione asintoticamente positiva. Il metodo principale è derivato dal cosiddetto "**teorema principale**", o "**master theorem**", il cui enunciato è il seguente:

> Dati $a \ge 1$, $b > 1$, una funzione asintoticamente positiva $f(n)$ e un'equazione di ricorrenza nella forma:
> $$\begin{cases} T(1)=\Theta(1)\\T(n)=a\cdot T\left( \frac{n}{b} \right)+f(n) \end{cases}$$
> valgono le seguenti considerazioni:
> - se esiste una qualche costante $\epsilon > 0$ tale per cui vale che $f(n)=O(n^{\log_{b}a-\epsilon})$, allora $T(n)=\Theta(n^{\log_{b}a})$;
> - se vale che $f(n)=\Theta(n^{\log_{b}a})$, allora $T(n)=\Theta(n^{\log_{b}a}\cdot \log n)$;
> - se esiste una qualche costante $\epsilon > 0$ tale per cui vale che $f(n)=\Omega(n^{\log_{b}a+\epsilon})$, e una costante $c<1$ tale per cui $a\cdot f\left( \frac{n}{b} \right)\le c\cdot f(n)$ per $n$ sufficientemente grandi, allora $T(n)=\Theta(f(n))$.

Informalmente, in ciascuno dei tre casi dell'enunciato appena esposto **vengono confrontati tra loro $f(n)$ e $n^{\log_{b}a}$**, e il teorema ci fa notare che il costo computazionale complessivo dell'algoritmo "dipende" proprio dalla relazione tra i due. Infatti:
- se **il maggiore** dei due **è $n^{\log_{b}a}$**, come avviene nel **primo caso**, allora il costo complessivo sarà $\Theta(n^{\log_{b}a})$;
- se **si comportano ugualmente**, come avviene nel **secondo caso**, allora il costo complessivo sarà $\Theta(n^{\log_{b}a}\cdot \log n)$;
- se **il maggiore** dei due **è $f(n)$**, come avviene nel **terzo caso**, e si verifica anche una condizione aggiuntiva, allora il costo complessivo sarà $\Theta(f(n))$.

Si ricordi che, in questo contesto, "maggiore" va inteso asintoticamente e può essere interpretato come "**maggiore polinomialmente**": in altre parole, $f(n)$ e $n^{\log_{b}a}$ devono essere uno maggiore dell'altro di un fattore $n^{\epsilon}$ per qualche $\epsilon>0$. Questa precisazione porta alla presenza di alcune "**zone grigie**" in cui il metodo principale risulta non applicabile, seppur l'equazione di ricorrenza rispetti la struttura desiderata: queste "zone grigie" si presentano **quando $f(n)$ è più piccola o più grande di $n^{\log_{b}a}$, ma non polinomialmente**.

##### Esempi

Per comprendere meglio come applicare questo metodo, vediamo alcuni **esempi** (essendo, per definizione, i casi base corrispondenti sempre a $T(1)=\Theta(1)$, ed essendo ininfluenti all'applicazione del metodo, essi verranno omessi).

Supponiamo di avere la seguente equazione di ricorrenza:
$$T(n)=9T\left( \frac{n}{3} \right)+\Theta(n)$$
Abbiamo $a=9$ e $b=3$, il che porta a ottenere $n^{\log_{b}a}=n^{\log_{3}9}=n^{2}$; oltre a ciò, si ha che $f(n)=\Theta(n)$. Scegliendo ad esempio $\epsilon=1$, otteniamo che $f(n)=\Theta(n^{2-\epsilon})=\Theta(n)$, perciò riconosciamo che ci troviamo nel primo caso, e dunque $T(n)=\Theta(n^{\log_{b}a})=\Theta(n^{2})$.

Analizziamo, ora, la seguente equazione di ricorrenza:
$$T(n)=T\left( \frac{2}{3}n \right)+\Theta(1)$$
Abbiamo $a=1$ e $b=\frac{3}{2}$, il che porta a ottenere $n^{\log_{b}a}=n^{\log_{\frac{3}{2}}1}=n^{0}=1$; oltre a ciò, si ha che $f(n)=\Theta(1)$. Notiamo subito che $f(n)=\Theta(n^{\log_{b}a})=\Theta(1)$, perciò riconosciamo che ci troviamo nel secondo caso, e dunque $T(n)=\Theta(n^{\log_{b}a}\cdot \log n)=\Theta(\log n)$.

Di seguito, consideriamo la seguente equazione di ricorrenza:
$$T(n)=3T\left( \frac{n}{4} \right)+\Theta(n\,\log n)$$
Abbiamo $a=3$ e $b=4$, il che porta a ottenere $n^{\log_{b}a}=n^{\log_{4}3}\approx n^{0.7}$; oltre a ciò, si ha che $f(n)=\Theta(n\,\log n)$. Scegliendo ad esempio $\epsilon=0.2$, otteniamo che $f(n)=\Omega(n^{\log_{b}a+\epsilon})$, perciò riconosciamo che ci troviamo nel terzo caso. Per poter confermare la validità della soluzione, dimostriamo anche che $a\cdot f\left( \frac{n}{b} \right)\le c \cdot f(n)$, ossia che $3\cdot \frac{n}{4}\,\log\left( \frac{n}{4} \right)\le c\cdot n\,\log n$, per qualche $c<1$. Ponendo, ad esempio, $n=\frac{3}{4}$, si verifica la disuguaglianza: dunque $T(n)=\Theta(n\,\log n)$.

Concludiamo con un'ultima equazione di ricorrenza:
$$T(n)=2T\left( \frac{n}{2} \right)+\Theta(n\,\log n)$$
Abbiamo $a=2$ e $b=2$, il che porta a ottenere $n^{\log_{b}a}=n^{\log_{2}2}=n$; oltre a ciò, si ha che $f(n)=\Theta(n\,\log n)$. Ora, mentre $f(n)$ è asintoticamente più grande di $n$, non si può dire che sia polinomialmente maggiore, dunque non riusciamo a inquadrarci in nessuno dei tre casi, e ciò rende impossibile l'applicazione del metodo principale.

[Dimostrazione del Master Theorem: DISPENSE, pag. 22/26]
___