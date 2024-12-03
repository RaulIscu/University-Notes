Spesso, in un programma, ci si trova a dover controllare se tutti gli elementi di un contenitore rispettano una certa condizione; per verificare ciò, potremmo scrivere un ciclo `for` del genere:
```
def controlla_tutti(contenitore):
	for elemento in contenitore:
		if not condizione(elemento):
			return False
	return True
```
In alternativa, per semplificare e velocizzare il tutto, si può utilizzare la funzione **`all(contenitore_TrueFalse)`**, che ritornerà `True` se tutti gli elementi del contenitore fornito saranno `True`. Questa funzione opera molto efficientemente se accoppiata con una funzione *[[Zip, map e filter|map]]*, che possa creare una lista di valori `True` o `False` applicando una condizione a un contenitore preesistente:
```
def controlla_tutti(contenitore):
	return all(map(condizione, contenitore))
```
In altri casi, invece, ci troviamo a voler controllare se almeno un elemento di un contenitore rispetta una certa condizione; per verificare ciò, potremmo scrivere un ciclo `for` del genere:
```
def esiste_uno(contenitore):
	for elemento in contenitore:
		if condizione(elemento):
			return True
	return False
```
In alternativa, per semplificare e velocizzare il tutto, si può utilizzare la funzione **`any(contenitore_TrueFalse)`**, che ritornerà `True` se almeno un elemento del contenitore fornito sarà `True`. Questa funzione opera molto efficientemente se accoppiata con una funzione *[[Zip, map e filter|map]]*, che possa creare una lista di valori `True` o `False` applicando una condizione a un contenitore preesistente:
```
def esiste_uno(contenitore):
	return any(map(condizione, contenitore ))
```