Una funzione viene definita "**ricorsiva**" se, nel suo codice, richiama sé stessa.

Un problema ammette una soluzione con funzione ricorsiva se:
- è possibile rimpicciolire la sua dimensione (riduzione);
- esiste almeno un sotto-problema che ha una soluzione elementare (caso base);
- è sempre possibile, applicando ripetutamente la riduzione, arrivare ad uno dei casi base (convergenza);
- è possibile ottenere la soluzione del problema iniziale dalle soluzioni dei sotto-problemi (composizione).

Risolvere un problema ricorsivamente, dunque, richiede l'individuazione di un caso base, il confronto tra problemi di dimensioni diverse per capire come eseguire al meglio la riduzione, confrontarne le soluzioni per capire invece come calcolare al meglio la soluzione, e verificare che, eseguendo più volte la riduzione, si arrivi sempre al caso (o ai casi) base.

In generale, una funzione ricorsiva rispetta solitamente uno schema del tipo:
```
def risolvi_ricorsivamente(problema):
	if is_caso_base(problema):
		return soluzione nota
	else:
		sottoproblema = riduzione(problema)
		sottosoluzione = risolvi_ricorsivamente(sottoproblema)
		soluzione = composizione(sottosoluzione)
		return soluzione
```
___
Un esempio classico per capire meglio il concetto di "funzione ricorsiva" è il **fattoriale**: il fattoriale di un numero intero positivo *N* è costituito dal prodotto dei numeri che vanno da 1 a *N*. Per affrontare il problema in maniera ricorsiva, bisogna farsi le seguenti domande: 
- come ridurre il problema?
- quale soluzione semplice si conosce?
- come ottenere F(N) da F(N - 1)?
- il passo di riduzione converge al caso base? 

Per ridurre il problema, si diminuisce man mano *N* di 1, fino ad arrivare al caso base, ossia quello in cui *N* è uguale a 1 e dunque il fattoriale corrisponde a 1; si potrà, a questo punto, tornare man mano al problema iniziale moltiplicando per *N*. Di seguito, un esempio di programma ricorsivo che risolve il problema:
```
def fattoriale(N):
	if N == 1:
		return 1
	else:
		return N * fattoriale(N - 1)
```
___
[ESEMPIO: CONIGLI DI FIBONACCI]
___
[SIMULARE UN CICLO CON LA RICORSIONE]
___
[ESEMPIO: MCD DI INTERI POSITIVI]
___
[ESEMPIO: CONTROLLARE SE UNA LISTA O UNA STRINGA É PALINDROMA]