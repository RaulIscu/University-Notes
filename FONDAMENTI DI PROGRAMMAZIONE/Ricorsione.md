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
Analizziamo un altro esempio di problema risolvibile ricorsivamente, ossia **trovare il massimo comun divisore** (MCD) tra due interi positivi *x* e *y*: si dovrà trovare, quindi, un numero *M* (più grande possibile) tale che *x = Mk*, così come *y = Mj*, con *k, j ≥ 1*.

Cerchiamo un caso base da cui partire per la risoluzione. Un buon approccio potrebbe essere il caso in cui *x = y*, che quindi porta a *j = k = 1* e a *M = x*. Inoltre, possiamo sottrarre il numero minore dal numero maggiore, ottenendo così un terzo numero *z = x - y = M(k - j)*; da questa uguaglianza, si evince che il numero *z* (più piccolo di *x*) ha lo stesso MCD di *x* e *y*, cioè proprio *M*. Facendo un'operazione del genere ciclicamente, otterrò man mano una riduzione della somma *k + j*, fino ad arrivare a *j = k = 1*, e dunque proprio al caso base. A questo punto, una volta trovato *M*, si avrà per ricomposizione la soluzione di ciascun caso più grande.

Tale ragionamento può essere programmato nel modo seguente:
```
def MCD(x, y):
	if x == y:
		return x
	else:
		if x > y:
			z = x - y
			return MCD(z, y)
		else:
			z = y - x
			return MCD(z, x)
```
___
Un ulteriore esempio di problema potenzialmente ricorsivo è **controllare se una stringa o una lista sia palindroma**. Tale problema può essere facilmente risolto anche in maniera iterativa, metodo che però risulta abbastanza inefficiente (viene creata una nuova stringa in memoria, e si confrontano più elementi del necessario).

Per un approccio ricorsivo, troviamo innanzitutto un caso base: in questo caso, si arriva in maniera immediata al caso in cui la sequenza di elementi sia lunga 0 o 1, in quanto in questi casi essa sia sempre palindroma. A questo punto, passando ad altri casi, si controllerà se il primo e l'ultimo elemento della sequenza siano uguali: se essi non lo sono, si potrà subito affermare che la sequenza considerata non è palindroma (potenzialmente si può usare quest'osservazione come ulteriore caso base); se invece lo sono, si potranno eliminare questi due elementi e ripetere l'operazione con primo e ultimo elemento della nuova sequenza. Così facendo, si arriverà eventualmente al caso base iniziale, e si potrà risolvere il problema.

Tale ragionamento può essere programmato nel modo seguente:
```
def palindroma(sequenza):
	if len(sequenza) < 2:
		return True
	if sequenza[0] != sequenza[-1]:
		return False
	else:
		return palindroma(sequenza[1: -1])
```
Notiamo, tuttavia, che un codice del genere risulta inefficiente per lo stesso motivo che rendeva inefficiente una generica soluzione iterativa, ossia la creazione di nuove sequenze (o, in questo caso, sottosequenze): si può ottimizzare questa soluzione ricorrendo a degli indici di inizio e di fine e non creando ulteriori sottosequenze, nel modo seguente:
```
def palindroma2(sequenza, inizio, fine):
	if inizio >= fine:
		return True
	if sequenza[inizio] != sequenza[fine]:
		return False
	else:
		return palindroma2(sequenza, inizio + 1, fine - 1)
```
___
Un esempio più "concreto" di ricorsione può essere l'**esplorazione di un albero di *directory***, in cui supponiamo di voler cercare tutti i *file* di testo e le loro dimensioni (inserendo *path* del *file* e le sue dimensioni in un dizionario).

Nell'analisi di una *directory*, risulta che il caso base sia quello in cui tale *directory* contenga solo *file*, mentre l'eventualità di ulteriori sotto-*directory* rappresenta il caso ricorsivo. A forza di esaminare sotto-*directory*, si arriverà necessariamente a un caso in cui essa contenga proprio solo *file*, arrivando così al caso base precedentemente specificato; da lì, si potrà risalire alla *directory* iniziale.

Per esaminare *directory* e *file* conviene utilizzare la libreria **`os`**, e i suoi metodi, tra cui:
- **`os.listdir(path)`**, che fornisce i nomi di tutti gli elementi trovati in una determinata *directory* (se l'argomento `path` viene omesso si analizza la *directory* corrente);
- **`os.path.isdir(path)`**, che ritorna `True` o `False` a seconda se il *path* dato in argomento indica una *directory* esistente;
- **`os.path.getsize(path)`**, che restituisce un intero che rappresenta le dimensioni in *byte* del *path* dato in argomento.

Tale ragionamento può essere programmato nel modo seguente:
```
def cerca_file_sizes(directory):
	risultato = {}
	for nome in os.listdir(directory):
		if nome[0] in '_.': 
			continue
		fullname = directory + '/' + nome
		if os.path.isdir(fullname):
			trovati = cerca_file_sizes(fullname)
			risultato.update(trovati)
		elif nome.endswith('.txt'):
			size = os.path.getsize(fullname)
			risultato[fullname] = size
	return risultato
```
___
