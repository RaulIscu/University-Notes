In un programma, è possibile definire una variabile a cui viene assegnato via via un determinato valore da una sequenza di valori. Se si vogliono eseguire delle azioni su ciascun valore, conoscendo il numero di iterazioni da compiere, si utilizza un **ciclo ```for```**:
```
for elemento in sequenza:
	codice da eseguire per ciascun elemento della sequenza
```
Opzionalmente, si può aggiungere al blocco precedente anche un **```else```**:
```
else:
	codice eseguito se si è completato il ciclo normalmente (senza break)
```
L’istruzione ```break``` viene usata per uscire immediatamente dal ciclo, e continuare quindi con il codice dopo l’intero ciclo ```for```, al verificarsi di una determinata condizione. Un’altra istruzione utile nei blocchi for è ```continue```, che consente di saltare al prossimo elemento della sequenza considerata se il valore preso rispetta una determinata condizione. Un esempio di ciclo ```for``` che include anche queste istruzioni può essere il seguente:
```
for x in range(1, 11):
	if x == 8:
		break
	if x % 2 == 0:
		continue
	print(x)
else:
	print("li ho stampati tutti")
```
___
Nel caso in cui non si è a conoscenza del numero di iterazioni da compiere, conviene invece utilizzare un **ciclo ```while```**:
```
while condizioneTrue:
	codice da eseguire solo se condizioneTrue
```
Anche in questo caso, opzionalmente, si può aggiungere al ciclo precedente anche un ```else```:
```
else:
	codice da eseguire se si termina il ciclo (senza break)
```
Un esempio di ciclo ```while``` può essere il seguente:
```
x = 0
while x < 20:
	x += 1
	if x == 27:
		break
	if x % 2 == 0:
		continue
	print(x)
else:
	print("li ho stampati tutti")
```
