Nell'informatica, ci sono alcune categorie di problemi che sono più rilevanti di altre, soprattutto per la loro frequenza e per il loro riscontro anche in situazioni reali. Una di queste categorie è quella dei problemi di "**ricerca**", che naturalmente consistono nel **cercare un elemento specifico all'interno di un insieme di elementi**.

Più formalmente, tale problema può essere descritto in forma di **input e output di un algoritmo**:
- come **input**, si avrà un array $A$ contenente $n$ elementi, tra cui figurerà l'elemento cercato $v$;
- come **output**, si otterrà l'elemento $v$, oppure un indice $i$ tale che `A[i] = v`, o ancora un valore `None` o $-1$ se l'elemento desiderato non è contenuto nell'array.

Vari approcci alla ricerca sono possibili dal punto di vista algoritmico: in questo capitolo, analizzeremo due dei principali metodi di ricerca, ossia la "**ricerca sequenziale**" e la "**ricerca binaria**".
## Ricerca sequenziale

Un primo approccio, il più basilare e intuitivo, consiste nella cosiddetta "**ricerca sequenziale**". Tale soluzione si basa sull'**ispezionare gli elementi dell'array uno alla volta, confrontando ciascuno di essi con l'elemento cercato $v$**, e restituire il risultato della ricerca, che sarà l'indice $i$ dell'elemento all'interno dell'array se esso viene trovato, o $-1$ se l'elemento $v$ non viene trovato all'interno dell'array.

Una possibile implementazione di un algoritmo di ricerca sequenziale è il seguente:

```
def ricerca_sequenziale(A, v):
	i = 0
	
	while i < len(A) and A[i] != v:
		i += 1
	
	if i < len(A):
		return i
	else:
		return -1
```

Un'implementazione alternativa, più semplice a livello di codice, può essere la seguente:

```
def ricerca_sequenziale_1(A, v):
	for i in range(len(A)):
		if A[i] == v:
			return i
	
	return -1
```

Passando al **costo computazionale** dell'algoritmo, non possiamo effettuare una stima accurata che valga per qualsiasi caso generale, dato che il costo dipende dai valori particolari contenuti nell'array $A$. È possibile, però, distinguere un caso migliore e un caso peggiore:
- nel **caso migliore** (quando l'elemento $v$ desiderato è il primo elemento dell'array), il costo computazionale è pari a $\Theta(1)$;
- nel **caso peggiore** (quando l'elemento $v$ desiderato non è contenuto nell'array), il costo computazionale è pari a $\Theta(n)$.

Non avendo trovato una stima del costo computazionale valida per tutti i casi, **in generale** si può affermare che **il costo computazionale dell'algoritmo è in $O(n)$**, per evidenziare che ci sono possibili input in cui il costo indicato viene raggiunto, ma anche altri input per cui il costo è minore. 

In contesti del genere, in cui c'è una distinzione tra caso migliore e peggiore, si può comunque **fornire un'approssimazione per il valore stretto del costo computazionale**, ma per fare ciò è necessario stimare il **numero medio di iterazioni**. Sappiamo che $v$ può apparire in una qualsiasi delle posizioni dell'array con la stessa probabilità, dunque si ha che:
$$\mathbb{P}(v\text{ si trovi in }i\text{-esima posizione}) = \frac{1}{n}$$
Di conseguenza, il numero medio di iterazioni è dato da:
$$\frac{1}{n}\cdot \sum_{i\,=\,1}^{n}i\,=\,\frac{1}{n}\cdot \frac{n(n+1)}{2} = \frac{n+1}{2}$$
Dunque, è ragionevole pensare che il costo computazionale medio dell'algoritmo di ricerca sequenziale fornito sia $\Theta(n)$.

Avendo chiarito il concetto di ricerca sequenziale, è opportuno fare una piccola precisazione riguardante l'operatore `in` in linguaggi come Python, che viene utilizzato proprio per sapere se un determinato valore si trova all'interno di un certo insieme di valori: seppur la scrittura condensata possa far pensare che si tratta di un'[[IAA_03 - Costo computazionale#Come calcolare il costo computazionale di un algoritmo?|istruzione elementare]], dunque di costo $\Theta(1)$, in realtà tale operatore è un'abbreviazione di una ricerca sequenziale dell'elemento considerato nell'insieme di elementi in questione, e ha dunque un costo medio pari a $\Theta(n)$.
___
## Ricerca binaria

Oltre alla [[IAA_04 - Ricerca#Ricerca sequenziale|ricerca sequenziale]], possiamo trovare altri algoritmi molto più efficienti, come la "**ricerca binaria**". Il meccanismo della ricerca binaria è riassumibile come segue: **ispezionare l'elemento centrale dell'array**; se si tratta dell'elemento desiderato $v$, restituirlo e fermarsi, altrimenti si distinguono due casi:
- se **l'elemento desiderato è più piccolo di quello trovato**, allora si ripete lo stesso procedimento nella metà inferiore della sequenza;
- se **l'elemento desiderato è più grande di quello trovato**, allora si ripete lo stesso procedimento nella metà superiore della sequenza.

Va ricordato che, per l'opportuno funzionamento della ricerca binaria, **l'array di elementi su cui lavora deve necessariamente essere ordinato**.

Una possibile implementazione di un algoritmo di ricerca binaria è il seguente:

```
def ricerca_binaria(A, v):
	a = 0
	b = len(A) - 1
	m = (a + b) // 2
	
	while A[m] != v:
		if (A[m] > v):
			b = m - 1
		else:
			a = m + 1
		
		if a > b:
			return -1
		
		m = (a + b) // 2
	
	return m
```

Passando al **costo computazionale** dell'algoritmo, anche in questo caso non possiamo effettuare una stima accurata che valga per qualsiasi caso generale, dato che il costo dipende dai valori particolari contenuti nell'array $A$. È possibile, però, distinguere un caso migliore e un caso peggiore:
- nel **caso migliore** (quando l'elemento $v$ desiderato è trovato alla prima iterazione, dunque si trova precisamente a metà dell'array), il costo computazionale è pari a $\Theta(1)$;
- nel **caso peggiore** (quando l'elemento $v$ desiderato non è contenuto nell'array), il costo computazionale è pari a $\Theta(\log n)$.

Notiamo che vi è un significativo miglioramento di prestazioni rispetto all'algoritmo di ricerca sequenziale: informalmente, ciò avviene perché **ad ogni iterazione si dimezza il numero di elementi su cui lavorare**; più formalmente, abbiamo che all'$i$-esima iterazione la dimensione dell'input è $\frac{n}{2^{i}}$. Dunque, indicando con $n$ il numero di elementi dell'array, abbiamo che il numero di iterazioni cresce seguendo l'andamento di $\log n$.

Non avendo trovato una stima del costo computazionale valida per tutti i casi, **in generale** si può affermare che **il costo computazionale dell'algoritmo è in $O(\log n)$**, per evidenziare che ci sono possibili input in cui il costo indicato viene raggiunto, ma anche altri input per cui il costo è minore. 

Per fornire un'**approssimazione per il valore stretto del costo computazionale**, stimiamo il **numero medio di iterazioni**. Poniamo innanzitutto delle assunzioni: si assume che il numero di elementi dell'array è una potenza di 2 (si pone per semplicità di calcolo, non va a modificare sostanzialmente il risultato finale), che l'elemento cercato $v$ sia presente nella sequenza e che tutte le posizioni all'interno dell'array sono equiprobabili. A questo punto, chiediamoci quante posizioni possono essere controllate alla $i$-esima iterazione dell'algoritmo:
- con 1 iterazione, si può raggiungere una sola posizione;
- con 2 iterazioni, si possono raggiungere 2 posizioni;
- con 3 iterazioni, si possono raggiungere 4 posizioni;

e così via. In generale, la ricerca binaria esegue $i$ iterazioni solo se $v$ si trova in una delle $2^{i - 1}$ posizioni raggiungibili con tale numero di iterazioni; la probabilità che l'elemento $v$ si trovi in una delle $2^{i -1}$ posizioni è $\frac{2^{i-1}}{n}$, perciò possiamo affermare che il numero medio di iterazioni è dato da:
$$\sum_{i\,=\,1}^{\log n}i\cdot \frac{2^{i-1}}{n}\,=\,\frac{1}{n}\cdot \sum_{i\,=\,1}^{\log n}(i\cdot 2^{i-1})$$
Sapendo che $\sum_{i=1}^{k}i\cdot 2^{i-1}\,=\, (k-1)2^{k} + 1$, sostituendo $k = \log n$ troviamo che:
$$\frac{1}{n}((\log n-1)2^{\log n}+1\,=\,\log n - 1 + \frac{1}{n}$$
Dunque, abbiamo che **il numero medio di iterazioni si discosta per meno di un'iterazione dal numero massimo di iterazioni**.
___