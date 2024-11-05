I valori booleani possono essere combinati con **operatori logici** come ```and```, ```or``` e ```not```:
- ```and``` restituirà un valore ```True``` solo se tutti i valori booleani considerati risultano ```True```;
- ```or``` restituirà un valore ```True``` anche con solo un valore ```True```; 
- ```not``` rovescia il valore booleano considerato (restituirà ```False``` se il valore è ```True``` e viceversa).
Questi tre operatori vanno considerati con un preciso ordine di precedenza, ossia ```not``` ⇒ ```and``` ⇒ ```or```.

La combinazione di condizioni vero/falso serve a indicare al programma comportamenti diversi a seconda del risultato della condizione. Per scegliere di eseguire parti diverse di codice in situazioni diverse, vengono utilizzate istruzioni come **```if```**, **```elif```** ed **```else```**:

```
if condizione1:
	istruzioni eseguite se condizione1 = True
elif condizione2:
	istruzioni eseguite se condizione1 = False e condizione2 = True
else:
	istruzioni eseguite se condizione1, condizione2 = False
```

Un collegamento interessante tra tipi di dati interessa **numeri e valori booleani**: infatti, tutti i numeri interi (a esclusione dello 0) sono considerati ```True``` (ad esempio: ```bool(1)``` ⇒ ```True```, ```bool(0)``` ⇒ ```False```); un ragionamento simile vale anche per i numeri con la virgola, per cui tutti i numeri con la virgola (a esclusione di 0.0) sono considerati ```True```.

I valori booleani sono fondamentali nelle **espressioni condizionate**, espressioni che, a seconda di una condizione specifica, possono assumere due valori diversi. Possono essere interpretata come un “compattamento” di una funzione ```if```/```else```; infatti, invece di scrivere:

```
if condizione:
	A = valore_se_True
else:
	A = valore_se_False
```

è possibile scrivere:

```
A = valore_se_True if condizione else valore_se_False
```

Questa tecnica consente di semplificare il codice, rendendolo più compatto è comprensibile.