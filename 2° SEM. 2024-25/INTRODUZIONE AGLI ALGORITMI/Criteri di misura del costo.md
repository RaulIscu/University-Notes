Supponiamo di avere una parola di memoria di dimensione *i*: se è soddisfatta l’ipotesi che ogni dato in *input* ha dimensioni minori di 2*ⁱ*, ciascuna operazione elementare sui dati del problema verrà eseguita in un tempo costante. In tal caso, si parla di "**misura di costo uniforme**". 

Tale criterio, però, risulta essere più un'idealizzazione e non è sempre realistico, in quanto è perfettamente possibile che un dato del problema sia più grande, e per memorizzarlo si dovranno quindi usare più parole di memoria. Di conseguenza, anche le operazioni elementari su di esso dovranno essere reiterate per tutte le parole di memoria che lo contengono, e quindi richiederanno un tempo che non è più costante.

Converrà utilizzare, quindi, il criterio di "**misura di costo logaritmico**", che risulta essere perfettamente realistico e risolve il problema sopra esposto, assumendo che il costo delle operazioni elementari sia una funzione della dimensione degli operandi (ossia dei dati). Poiché il numero di *bit* necessari per memorizzare un valore *n* è proporzionale a *log₂n*, si parla di misura di costo logaritmico. Essa però implica rilevanti complicazioni nei calcoli dell’efficienza di un algoritmo, per cui non verrà approfondita in questo corso.
___
Analizziamo informalmente un semplicissimo algoritmo di esempio, applicando entrambi i criteri al fine di evidenziarne le differenze. L’algoritmo consiste di un ciclo, reiterato *i* volte, che calcola il valore 2*ⁱ*:

```
def potenza_di_2(i): 
	x = 1 
	for n in range(i):
		x = x * 2
	return x
```

Si vede facilmente che, con la misura di costo uniforme, il tempo di esecuzione totale è proporzionale ad *i*, poiché si tratta di un ciclo eseguito *i* volte in cui, ad ogni iterazione, si compiono due operazioni (l'incremento del contatore e il calcolo del nuovo valore). 

Con la misura di costo logaritmico le cose diventano subito più complicate perché sia l’incremento di *i* che il raddoppio di *x* non hanno più costo costante. In particolare, per ogni singola iterazione, il costo complessivo è dato da:
- *log₂x* = *log₂2ⁱ* = *i* per il calcolo del nuovo valore di *x*;
- *log₂i*, per l’incremento del contatore.

Dunque, il costo totale diventa:

![[mc_logaritmico1.png]]

Ora, considerando che:

![[mc_logaritmico2.png]]
![[mc_logaritmico3.png]]

si ottiene che il tempo di esecuzione totale è proporzionale a *i²*.

Concludiamo osservando che, per semplicità, abbiamo sottinteso che l’*input* fosse un intero strettamente positivo. Nel seguito, assumeremo sempre che l’*input* sia corretto (cioè esattamente come ce lo aspettiamo), evitando così la gestione degli errori (che, seppur rilevante, esula dagli obiettivi di questo corso).