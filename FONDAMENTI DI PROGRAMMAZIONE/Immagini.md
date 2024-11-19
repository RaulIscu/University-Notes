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
In questo formato di matrice di *pixel*, se si vuole considerare un *pixel* in particolare si usa un comando del tipo **`img[y][x]`**, in cui `y` rappresenta la riga *y*-esima (dall'alto verso il basso), mentre `x` rappresenta il *pixel* della riga *y* che si trova nella colonna *x* (da sinistra verso destra).
___
