In questo capitolo, si introdurranno **alcune keyword utili** in determinati contesti, che permettono di compattare la sintassi di alcuni costrutti o magari di velocizzare determinati procedimenti. Approfondiremo le seguenti keyword:
- **`all`**;
- **`any`**;
- **`filter`**;
- **`map`**;
- **`zip`**.

## `all`

Spesso, in un programma, ci si trova a voler **controllare se tutti gli elementi di un [[FDP_06 - Generatori e strutture dati#Strutture dati|contenitore]] rispettano una certa condizione**; per verificare ciò, un primo approccio potrebbe essere scrivere un ciclo `for` del genere:

```
for el in cont:
	if not cond:
		return False
return True
```

In alternativa, per semplificare il tutto, si può utilizzare la funzione **`all(cont)`**, che **restituirà `True` se tutti gli elementi del contenitore `cont` saranno `True`**. Concretamente, tale funzione può rivelarsi molto efficiente se accoppiata con una funzione **`map`**, che possa creare una lista di [[FDP_05 - Tipi#I booleani `bool`|valori booleani]] applicando una condizione a un contenitore preesistente:

```
return all(map(cond, cont))
```
___
## `any`

In altri casi, invece, ci troviamo a voler **controllare se almeno un elemento di un contenitore rispetta una certa condizione**; per verificare ciò, anche in questo caso si potrebbe utilizzare un ciclo `for`, come il seguente:

```
for el in cont:
	if cond:
		return True
return False
```

In alternativa, per semplificare il tutto, si può utilizzare la funzione **`any(cont)`**, che **restituirà `True` se almeno un elemento del contenitore `cont` sarà `True`**. Come per quella analizzata nel [[FDP_11 - Altre keyword utili#`all`|paragrafo precedente]], anche tale funzione può rivelarsi molto efficiente se accoppiata con una funzione **`map`**, che possa creare una lista di valori booleani applicando una condizione a un contenitore preesistente:

```
return any(map(cond, cont))
```
___
## `filter`

La funzione **`filter(select, cont)`** consente di **filtrare gli elementi del contenitore `cont` in base alla funzione `select`**, assumendo che quest’ultima restituisca un valore booleano per ogni elemento preso in input. Permette, ovviamente, di semplificare notevolmente il codice; ad esempio, un ciclo `for` del tipo:

```
result = []
for el in cont:
	if select(el):
		result.append(el)
```

può essere scritto come:

```
result = filter(select, cont)
```
___
## `map`

La funzione **`map(func, cont1, cont2, …)`** consente di **eseguire la funzione `func` su ognuno degli elementi dei contenitori `cont1, cont2, …`** (in caso vengano specificati più contenitori, la funzione `func` dovrà prendere in input tanti argomenti quanti sono i contenitori considerati). Considerando tre contenitori `l1`, `s2` e `l3` (possono essere anche di tipi diversi), eseguire il codice:

```
return map(func, l1, s2, l3)
```

restituirà una lista contenente gli output delle varie chiamate a `func`, che a ogni chiamata prende in input l'elemento $i$-esimo dei tre contenitori. La lista risultante avrà lunghezza pari alla lunghezza del contenitore più piccolo preso in input, ed eventuali elementi "in eccesso" verranno ignorati.
___
## `zip`

La funzione **`zip(cont1, cont2, …)`** prende in input un certo numero di contenitori `cont1, cont2, …` e restituisce **una lista di tuple, ciascuna di lunghezza pari al numero di contenitori e contenente gli elementi $i$-esimi dei contenitori in questione**. La lista di tuple contiene tante tuple quant'è il numero di elementi contenuti nel contenitore più piccolo preso in input, ed eventuali elementi "in eccesso" verranno ignorati. Per comprendere meglio, vediamo un esempio; supponiamo di avere nuovamente tre contenitori `l1`, `s2` e `l3` (possono essere anche di tipi diversi), e di eseguire il codice seguente:

```
l1 = [ 1, 2, 3, 4, 5, 6, 7 ]
s2 = 'abcdef'
l3 = ['A', 'B', 'C', 'D']

return list(zip(l1, s2, l3))
```

L'istruzione di `return` restituirà la seguente lista:

```
[(1, 'a', 'A'), (2, 'b', 'B'), (3, 'c', 'C'), (4, 'd', 'D')]
```
___