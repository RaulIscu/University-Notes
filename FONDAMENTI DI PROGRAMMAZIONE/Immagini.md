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
Si nota che nei codici analizzati finora si utilizzano funzioni specifiche, importate dalla libreria **`images`**; questa libreria non è predefinita di Python, ma creata *ad hoc* per lavorare sulle immagini nel corso. In generale, le funzioni di questa libreria sono:
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
___
[RUOTARE UN'IMMAGINE IN SENSO ANTIORARIO]
___
[DISEGNARE UNA LINEA]
___
[LEZIONE 12]
___
Molte operazioni che si possono fare su qualsiasi *editor* di foto possono essere eseguite anche su Python. In particolare, approfondiamo le seguenti operazioni:
- ritagliare;
- copiare una parte dell'immagine e incollarla su un'altra;
- aggiungere un bordo;
- applicare un filtro in toni di grigio;
- modificare la luminosità;
- modificare il contrasto;
- rendere il negativo di un'immagine;
- sfocare l'immagine.

Per **ritagliare un'immagine**, si distinguono due passaggi principali: prima si elimina un determinato numero di righe di *pixel* da sopra e sotto l'immagine, poi si toglie un determinato numero di colonne di *pixel* dall'immagine risultante. Per fare queste due operazioni, risulta fondamentale applicare lo *[[Generatori e contenitori|slicing]]*:
```
def crop_image(img, alto, basso, sx, dx):
	L, A = len(img[0]), len(img)
	if 0 <= alto < A and 0 <= basso <= A and 0 <= sx < L and 0 <= dx < L and alto + basso < A and sx + dx < L:
		if basso:
			nuova = img[alto: -basso]
		else:
			nuova = img[alto:]
		if dx:
			return [riga[sx: -dx] for riga in nuova]
		else:
			return [riga[sx:] for riga in nuova]
```
Per **copiare e incollare una parte dell'immagine su un'altra**, basterà effettuare un *crop* che isoli la parte di immagine che si vuole copiare, e sostituire la zona su cui si vuole copiare la parte considerata con quest'ultima con un [[Generatori e contenitori|assegnamento a slice]]:
```
def cut_paste_img(imgS, imgD, xs1, ys1, xs2, ys2, XD, YD):
	HS = len(imgS)
	WS = len(imgS[0])
	frammento = crop_image(imgS, ys1, HS - ys2, xs1, WS - xs2)
	larghezza = len(frammento[0])
	for indice, riga in enumerate(frammento):
		imgD[indice + YD][XD: XD + larghezza] = riga
```
Per **aggiungere un bordo** di un determinato colore a un'immagine, si possono utilizzare principalmente due metodi: 
- creare un'immagine più grande di quella di partenza, colorata del colore che si vuole avere per il bordo, e incollarci l'immagine iniziale; 
- aggiungere direttamente il bordo all'immagine iniziale, aggiungendo prima delle righe colorate all'inizio dell'immagine, aggiungendo poi i bordi destro e sinistro alle righe seguenti dell'immagine, e infine aggiungendo il bordo inferiore in maniera analoga a quello superiore.
Di seguito, un esempio di applicazione di entrambi i metodi:
```
def add_border1(img, spessore, colore):
	L, A = len(img[0]), len(img)
	nuova = crea_immagine(L+2*spessore, A+2*spessore, colore)
	cut_paste_img(img, nuova, 0, 0, L-1, A-1, spessore, spessore)
	return nuova

def add_border2(img, spessore, colore):
	L, A = len(img[0]), len(img)
	nuova = []
	nuova += [[colore] * (L+2*spessore) for i in range(spessore)]
	for riga in img:
		nuova.append([colore]*spessore + riga + [colore]*spessore)
	nuova += [[colore] * (L+2*spessore) for i in range(spessore)]
	return bordata
```
Per applicare un filtro in **toni di grigio**, si crea una copia dell'immagine di partenza in cui ogni *pixel* si sostituisce con il grigio che corrisponde alla luminosità media del *pixel* considerato:
```
def filtro_grigio(colore):
	media = round(sum(colore)/3)
	return media, media, media

def grey(img):
	grigia = copy.deepcopy(img)
	for y, riga in enumerate(img):
		for x, pixel in enumerate(riga):
			grigia[y][x] = filtro_grigio(pixel)
	return grigia
```
Per **modificare la luminosità** di un'immagine, sarà sufficiente moltiplicare i valori RGB di ogni *pixel* per un numero *k*, amplificando o riducendo in questo modo la luminosità di ogni *pixel*; per fare ciò, risulta fondamentale definire a priori una funzione che limiti i possibili valori RGB risultanti all'intervallo [0; 256):
```
def bound(canale):
	canale = round(canale)
	return min(max(canale, 0), 255)

def filtro_luminosita(colore, k):
	return (bound(colore[0]*k), bound(colore[1]*k), bound(colore[2]*k)

def luminosità(img, k):
	nuova = copy.deepcopy(img)
	for y, riga in enumerate(img):
		for x, colore in enumerate(riga):
			nuova[y][x] = filtro_luminosita(colore, k)
	return nuova
```
Modificare il contrasto di un'immagine significa, a grandi linee, che un *pixel* chiaro diventerà più chiaro e un *pixel* scuro diventerà più scuro: dunque, per **modificare il contrasto** di un'immagine, si dovranno allontanare i valori RGB di ogni *pixel* di un fattore *k* dal valore grigio 128. Per fare ciò, per ciascuna delle componenti RGB si dovrà sottrarre 128, moltiplicare il risultato per *k* e riaggiungere 128, assicurandosi che il valore finale sarà compreso nell'intervallo [0; 256):
```
def contrasta_canale(canale, k):
	differenza = canale - 128
	amplificato = differenza * k
	sommato = amplificato + 128
	return bound(sommato)

def filtro_contrasto(colore, k):
	return (contrasta_canale(colore[0], k), contrasta_canale(colore[1], k), contrasta_canale(colore[2], k))

def contrasto(img, k):
	nuova = copy.deepcopy(img)
	for y, riga in enumerate(img):
		for x, colore in enumerate(riga):
			nuova[y][x] = filtro_contrasto(colore, k)
	return nuova
```
Per **rendere il negativo** di un'immagine, bisogna trasformare ogni *pixel* nel suo inverso, calcolando dunque la luminosità inversa di ogni suo valore RGB, ossia 255 - R, 255 - G e 255 - B:
```
def filtro_negativo(colore):
	return (255 - componente for componente in colore)

def negativo(img):
	nuova = copy.deepcopy(img)
	for y, riga in enumerate(img):
		for x, colore in enumerate(riga):
			nuova[y][x] = filtro_negativo(colore)
	return nuova
```
Per **sfocare un'immagine**, si dovrà sostanzialmente fare una media dei colori fino a una distanza *k* del *pixel* considerato volta per volta:
```
def colore_medio(listaColori):
	N = len(listaColori)
	R, G, B = 0, 0, 0
	for r, g, b in listaColori:
		R += r
		G += g
		B += b
	return bound(R/N), bound(G/N), bound(B/N)

def vicini(img, W, H, x, y, k):
	vicinato = []
	for X in range(x - k, x + k + 1):
		for Y in range(y - k, y + k + 1):
			if 0 <= X < W and 0 <= Y < H:
				vicinato.append(img[Y][X])
	return vicinato

def blur(img, k):
	W = len(img[0])
	H = len(img)
	nuova = [riga.copy() for riga in img]
	for x in range(W):
		for y in range(H):
			vicinato = vicini(img, W, H, x, y, k)
			nuova[y][x] = colore_medio(vicinato)
	return nuova
```
