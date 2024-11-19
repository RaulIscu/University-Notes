Le **immagini** sono, a livello fondamentale, delle griglie di "***pixel***" (**pic**ture **el**ement) colorati, disposti in varie forme e combinazioni. 
___
Analizzando le immagini sotto questo punto di vista, si può affermare che ad ogni posizione, definita da coordinate (*x*, *y*), di un'immagine si troverà un *pixel* di un determinato colore. Questi colori possono essere distinti e codificati in vario modo; quello più comune e diffuso è il **modello** ***RGB***, che, come suggerisce il nome, si basa principalmente su tre componenti:
- **R**, ossia la luminosità del colore **rosso**;
- **G**, ossia la luminosità del colore **verde**;
- **B**, ossia la luminosità del colore **blu**.
Ciascuno di questi valori viene, in genere, codificato in un *byte* (8 *bit*), e può quindi essere rappresentato da un numero che va **da 0 a 256**. Essendo un *pixel* costituito dalla combinazione dei tre elementi *RGB*, esso occuperà 3 *byte* (o 24 *bit*), e potrà visualizzare uno tra circa 16 milioni di colori diversi. 

Nell'analisi del modello *RGB*, i casi particolari più lampanti sono il bianco, rappresentato dal massimo della luminosità per tutti e 3 i parametri (`255, 255, 255`), e il nero, rappresentato invece dal minimo della luminosità per tutti e 3 i parametri (`0, 0, 0`).
___
Abbiamo stabilito che una qualsiasi immagine può essere interpretata come una griglia (o **matrice**) di *pixel*; per semplicità, dunque, in un programma un'immagine può venir rappresentata come una [[Generatori e contenitori|lista]] di liste di triple (tuple con 3 elementi). Ad esempio, se volessimo rappresentare la bandiera italiana, il programma corrispondente sarebbe il seguente:
```
import images
img = [
		[(0,255,0), (0,255,0), (0,255,0), (255,255,255), (255,255,255), (255,255,255), (255,0,0), (255,0,0), (255,0,0)],
		[(0,255,0), (0,255,0), (0,255,0), (255,255,255), (255,255,255), (255,255,255), (255,0,0), (255,0,0), (255,0,0)],
		[(0,255,0), (0,255,0), (0,255,0), (255,255,255), (255,255,255), (255,255,255), (255,0,0), (255,0,0), (255,0,0)],
		[(0,255,0), (0,255,0), (0,255,0), (255,255,255), (255,255,255), (255,255,255), (255,0,0), (255,0,0), (255,0,0)],
		[(0,255,0), (0,255,0), (0,255,0), (255,255,255), (255,255,255), (255,255,255), (255,0,0), (255,0,0), (255,0,0)],
		[(0,255,0), (0,255,0), (0,255,0), (255,255,255), (255,255,255), (255,255,255), (255,0,0), (255,0,0), (255,0,0)],
		[(0,255,0), (0,255,0), (0,255,0), (255,255,255), (255,255,255), (255,255,255), (255,0,0), (255,0,0), (255,0,0)],
		[(0,255,0), (0,255,0), (0,255,0), (255,255,255), (255,255,255), (255,255,255), (255,0,0), (255,0,0), (255,0,0)],
		[(0,255,0), (0,255,0), (0,255,0), (255,255,255), (255,255,255), (255,255,255), (255,0,0), (255,0,0), (255,0,0)],
		[(0,255,0), (0,255,0), (0,255,0), (255,255,255), (255,255,255), (255,255,255), (255,0,0), (255,0,0), (255,0,0)],
		[(0,255,0), (0,255,0), (0,255,0), (255,255,255), (255,255,255), (255,255,255), (255,0,0), (255,0,0), (255,0,0)],
]

images.visd(img)
```
In questo formato di matrice di *pixel*, se si vuole considerare o manipolare un *pixel* in particolare si usa un comando del tipo **`img[y][x]`**, in cui `y` rappresenta la riga *y*-esima (dall'alto verso il basso), mentre `x` rappresenta il *pixel* della riga *y* che si trova nella colonna *x* (da sinistra verso destra).
___
Per creare un'immagine di base, partendo da zero, si possono utilizzare due metodi alternativi; il primo sfrutta le *list comprehension*, mentre il secondo no:
```
def crea_immagine1(larghezza, altezza, colore):
	return [[colore] * larghezza for i in range(altezza)]

def crea_immagine2(larghezza, altezza, colore):
	img = []
	for y in range(altezza):
		riga = []
		for x in range(larghezza):
			riga.append(colore)
		img.append(riga)
	return img
```
Invece, per caricare un'immagine dalla memoria, si utilizza un codice del genere:
```
import images
img3 = images.load('3cime.png')
```
Infine, se si vuole salvare un'immagine su cui si è lavorato:
```
import images
img3[40][30:250] = [(255,0,0)] * 220
images.save(img3, '3cime-2.png')
```
Si nota che nei codici analizzati finora si utilizzano funzioni specifiche, importate dalla libreria **`images`**; questa libreria non è predefinita di Python, ma creata *ad hoc* per lavorare sulle immagini nel corso. In generale, le funzioni principali di questa libreria sono:
- **`images.visd(immagine)`**, che permette di visualizzare un'immagine presa come argomento;
- **`images.load(filename)`**, che permette di caricare nel programma un'immagine salvata in memoria;
- **`images.save(immagine, filename)`**, che permette di salvare in memoria un'immagine su cui si è lavorato nel programma.
___
Essendo un'immagine una matrice di *pixel*, si può facilmente manipolare un *pixel* specifico di questa matrice specificandone le coordinate e il colore che si vuole assegnare al *pixel* considerato:
```
def draw_pixel(img, x, y, colore):
	A, L = len(img), len(img[0])
	x = int(round(x))
	y = int(round(y))
	if 0 <= x < L and 0 <= y < A:
		img[y][x] = colore

draw_pixel(img3, 20, 2000, red)
```
Ciò che fa il blocco di codice all'interno della definizione di `draw_pixel()` è ricavare altezza e larghezza dell'immagine considerata, arrotondare eventuali valori `float` inseriti come coordinate del *pixel*, e modificare quest'ultimo solo se esso è effettivamente presente all'interno dell'immagine.