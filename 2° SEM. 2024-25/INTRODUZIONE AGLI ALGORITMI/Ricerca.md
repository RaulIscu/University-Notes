Uno dei problemi più ricorrenti e importanti in ambito informatico è quello della **ricerca** di un dato specifico in un insieme di altri dati (numeri, stringhe, o qualsiasi altro elemento).

Possiamo formalizzare questo problema descrivendo gli *input* e gli *output* di una possibile soluzione:
1. come ***input*** si riceverà un *array* A di *n* elementi, e un valore v;
2. come ***output***, invece, si otterrà un indice *i* tale che A[i] = v, oppure un determinato valore `None` se il valore v non è presente nell'*array*.

Analizziamo delle possibili implementazioni di algoritmi che risolvono questo problema.
___
Un primo approccio consiste nella cosiddetta **ricerca sequenziale**. Si tratta dell'algoritmo più semplice utilizzabile, e consiste nei seguenti passaggi:
- ispezionare gli elementi dell'*array* uno alla volta;
- confrontare ciascun elemento con v;
- restituire il risultato, interrompendo il procedimento nell'eventualità in cui si trova v.

Di seguito, vediamo dello pseudocodice che implementa quest'algoritmo di ricerca sequenziale:

```
def RicercaSequenziale1(A, v):
	i = 0
	
	while (i < len(A) and A[i] ≠ v):
		i += 1
	
	if i < len(A):
		return i
	else:
		return -1

def RicercaSequenziale2(A, v):
	for i in range(len(A)):
		if A[i] == v:
			return i
	
	return -1
```

L'algoritmo di ricerca sequenziale presenta, nel caso migliore (ossia quello in cui *v* viene trovato subito come primo elemento dell'*array* considerato), un costo computazionale pari a **θ(1)**; nel caso peggiore (ossia quello in cui *v* non è contenuto nell'*array*), esso avrà invece un costo pari a **θ(n)**, dove *n* è la lunghezza dell'*array* considerato.

Non potendo trovare una stima del costo computazionale che sia valida per tutti i casi, potremo dire che in generale il costo computazionale di questo algoritmo è un **O(n)**, per evidenziare il fatto che ci sono *input* per cui questo costo viene raggiunto ma anche *input* per cui il costo effettivo è minore.

[COSTO MEDIO]
___
Si può, alternativamente, applicare una **ricerca binaria** (o **ricerca dicotomica**). Questo algoritmo necessita, come premessa per poter funzionare in maniera affidabile, che l'*array* su cui si sta lavorando sia ordinato; si può riassumere nei seguenti passaggi:
- ispezionare l'elemento centrale della sequenza, e se esso corrisponde a v si può terminare qui;
- se l'elemento non corrisponde a v, nel caso in cui v sia più piccolo dell'elemento trovato si ripete il primo passaggio lavorando solo sulla metà inferiore dell'*array*, altrimenti si lavora nella metà superiore.

Di seguito, vediamo dello pseudocodice che implementa quest'algoritmo di ricerca binaria:

```
def RicercaBinaria(A, v):
	a, b = 0, len(A) - 1
	m = (a + b) // 2
	
	while A[m] != v:
		if A[m] > v:
			b = m - 1
		else:
			a = m + 1
		
		if a > b:
			return -1
		
		m = (a + b)//2

	return m
```

Analizzando il funzionamento dell'algoritmo, osserviamo che ad ogni iterazione viene dimezzato il numero di elementi su cui proseguire l'indagine: questo è l'aspetto principale che rende la ricerca binaria molto più efficiente di quella sequenziale. Grazie a ciò, infatti, il numero di iterazioni cresce, parallelamente alla lunghezza *n* dell'*array* considerato, come *log n*.

Dunque, l'algoritmo di ricerca binaria presenta, nel caso migliore (ossia quello in cui *v* viene trovato subito come primo elemento dell'*array* considerato), un costo computazionale pari a **θ(1)**; nel caso peggiore (ossia quello in cui *v* non è contenuto nell'*array*), esso avrà invece un costo pari a **θ(log n)**, dove *n* è la lunghezza dell'*array* considerato.

[COSTO MEDIO]