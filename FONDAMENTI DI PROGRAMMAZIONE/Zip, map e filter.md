La funzione ```zip(contenitore1, contenitore2, …)``` prende in input un gruppo di contenitori e restituisce delle tuple che contengono, a mano a mano, gli elementi nella posizione *i*-esima di questi contenitori. 

> NB: la sequenza di tuple che viene restituita ha lunghezza pari alla lunghezza minima tra i contenitori considerati (es: se il contenitore più piccolo preso in input ha 3 elementi, la funzione restituirà 3 tuple); vale lo stesso per la funzione `map`

Ad esempio:

```
L1 = [ 1, 2, 3, 4, 5, 6, 7 ]
S2 = 'abcdef'
L3 = ['A', 'B', 'C', 'D']

return list(zip(L1, S2, L3))
```

restituirà la seguente lista:

```
[(1, 'a', 'A'), (2, 'b', 'B'), (3, 'c', 'C'), (4, 'd', 'D')]
```

Nel caso in cui sia necessario trasformare una o più sequenze di valori in nuove sequenze, invece di utilizzare un ciclo ```for```, o anche di utilizzare la funzione ```zip```, è possibile utilizzare la funzione ```map(funzione, contenitore1, contenitore2, …)```, che consente di semplificare l’operazione inserendo semplicemente l’azione da compiere su ogni dato (o gruppo di dati). Ad esempio, considerando i contenitori dell’esempio precedente, eseguire il codice:

```
return map(funzione, L1, S2, L3)
```

produrrà un contenitore in cui ciascun elemento è ottenuto eseguendo funzione sull’elemento *i*-esimo di ciascun contenitore dato in input.

La funzione ```filter(selettore, contenitore)``` consente di filtrare gli elementi di un contenitore mediante la funzione selettore, assumendo che quest’ultima restituisca un valore ```True``` o ```False``` per ogni elemento in input. Consente, ovviamente, di semplificare notevolmente il codice, in quanto un ciclo ```for``` del tipo:

```
sottoinsieme = []
for elemento in contenitore:
	if selettore(elemento):
		sottoinsieme.append(elemento)
```
  
può essere scritto come:

```
sottoinsieme = filter(selettore, contenitore)
```