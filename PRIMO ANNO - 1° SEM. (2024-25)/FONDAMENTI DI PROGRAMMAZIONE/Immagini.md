Le **immagini** sono, a livello fondamentale, delle griglie di "***pixel***" (**pic**ture **el**ement) colorati, disposti in varie forme e combinazioni. 
___
Analizzando le immagini sotto questo punto di vista, si può affermare che ad ogni posizione, definita da coordinate (*x*, *y*), di un'immagine si troverà un *pixel* di un determinato colore. Questi colori possono essere distinti e codificati in vario modo; quello più comune e diffuso è il **modello** ***RGB***, che, come suggerisce il nome, si basa principalmente su tre componenti:
- **R**, ossia la luminosità del colore **rosso**;
- **G**, ossia la luminosità del colore **verde**;
- **B**, ossia la luminosità del colore **blu**.
Ciascuno di questi valori viene, in genere, codificato in un *byte* (8 *bit*), e può quindi essere rappresentato da un numero che va **da 0 a 256**. Essendo un *pixel* costituito dalla combinazione dei tre elementi *RGB*, esso occuperà 3 *byte* (o 24 *bit*), e potrà visualizzare uno tra circa 16 milioni di colori diversi. 

Nell'analisi del modello *RGB*, i casi particolari più lampanti sono il bianco, rappresentato dal massimo della luminosità per tutti e 3 i parametri (`255, 255, 255`), e il nero, rappresentato invece dal minimo della luminosità per tutti e 3 i parametri (`0, 0, 0`).
___
Abbiamo stabilito che una qualsiasi immagine può essere interpretata come una griglia (o **matrice**) di *pixel*; per semplicità, dunque, in un programma un'immagine può essere rappresentata come una [[Generatori e contenitori|lista]] di liste di triple (tuple con 3 elementi). Ad esempio, se volessimo rappresentare la bandiera italiana, il programma corrispondente sarebbe il seguente:
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

for righe in img[1:-1]:
	righe[34] = colore
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
[RUOTARE UN'IMMAGINE IN SENSO ANTIORARIO E ORARIO]
___
Disegnare una **linea** di *pixel* orizzontale o verticale su un'immagine di partenza è abbastanza immediato: la prima si può facilmente ottenere con un'assegnamento a *slice*, mentre la seconda modificando *pixel* dello stesso indice in varie righe consecutive di *pixel*.

Il discorso si complica quando si vuole creare una generica **linea diagonale**. Per fare ciò, tornerà utile ricordare l'equazione generica di una retta, e ragionare scandendo il cateto più lungo del triangolo rettangolo immaginario di cui la linea diagonale che vogliamo disegnare è ipotenusa. Presupponendo di avere le coordinate del *pixel* di inizio e del *pixel* di termine della linea che si vuole disegnare, si dovranno calcolare le lunghezze dei due cateti del triangolo immaginario, e confrontarle; a questo punto, in base a quale cateto (orizzontale `dx` o verticale `dy`) sarà più lungo, si calcolerà il coefficiente angolare della retta che si vuole disegnare e lo si utilizzerà, insieme all'equazione generica della retta passante per un punto, per disegnare uno ad uno i *pixel*:
```
def draw_line(img, x1, y1, x2, y2, colore):
	dx = x2 - x1
	dy = y2 - y1
	if abs(dx) >= abs(dy):
		if x1 > x2:
			x1, y1, x2, y2 = x2, y2, x1, y1
			dx *= -1
			dy *= -1
		m = dy/dx
		for x in range(x1, x2 + 1):
			y = m * (x - x1) + y1
			draw_pixel(img, x, y, colore)
	else:
		if y1 > y2:
			x1, y1, x2, y2 = x2, y2, x1, y1
			dx *= -1
			dy *= -1
		m = dx/dy
		for y in range(y1, y2 + 1):
			x = m * (y - y1) + x1
			draw_pixel(img, x, y, colore)
```
___
Distinguiamo vari casi possibili di disegno di un **rettangolo** su un'immagine, partendo dai più facili. Probabilmente, il caso più basilare sarà il disegno di un **rettangolo vuoto e privo di inclinazione**, ossia con lati che sono orizzontali e verticali: per fare ciò, si può semplicemente implementare 4 volte la funzione generica `draw_line()` appena definita, o in alternativa colorare manualmente i singoli *pixel* del perimetro del rettangolo. Supponendo che i *pixel* siano forniti nell'ordine giusto, le due modalità di disegno portano alle seguenti funzioni:
```
def draw_empty_rectangle(img, x1, y1, x2, y2, colore):
	draw_line(img, x1, y1, x2, y1, colore)
	draw_line(img, x1, y2, x2, y2, colore)
	draw_line(img, x1, y1, x1, y2, colore)
	draw_line(img, x2, y1, x2, y2, colore)

def draw_empty_rectangle2(img, x1, y1, x2, y2, colore):
	for x in range(x1, x2 + 1):
		draw_pixel(img, x, y1, colore)
		draw_pixel(img, x, y2, colore)
	for y in range(y1, y2+1):
		draw_pixel(img, x1, y, colore)
		draw_pixel(img, x2, y, colore)
```
Nel caso in cui il **rettangolo** che vogliamo disegnare sia sempre **privo di inclinazione**, ma **pieno**, l'operazione diventa in realtà ancora più semplice, in quanto basterà programmare due cicli annidati, che vanno quindi a colorare tutti i *pixel* appartenenti al rettangolo che si vuole disegnare:
```
def draw_rectangle(img, x1, y1, x2, y2, colore):
	for x in range(x1, x2 + 1):
		for y in range(y1, y2 + 1):
			draw_pixel(img, x, y, colore)
```
[DISEGNARE UN RETTANGOLO INCLINATO] 
___
É possibile disegnare anche figure curve. Vediamo, ad esempio, l'**ellisse**: essa è definita come una figura dotata di due fuochi, per cui la somma delle distanze di ogni suo punto dai due fuochi è costante. Da ciò, si ricava che se la somma delle distanze dai due fuochi di un punto è minore di questa costante, il punto si trova all'interno dell'ellisse; viceversa, se la somma delle distanze dai due fuochi di un punto è maggiore, questo si trova all'esterno dell'ellisse.

Si può sfruttare la proprietà appena esplicitata per disegnare in maniera facile un'**ellisse piena**: per fare ciò, conoscendo le coordinate dei due fuochi, basterà infatti controllare ogni *pixel* dell'immagine, calcolandone la distanza dai due fuochi, e se quest'ultima risulterà minore di *D = 2a* (dove *a* è il semiasse maggiore dell'ellisse), colorare il *pixel* considerato:
```
from math import dist

def draw_ellisse(img, x1, y1, x2, y2, D, colore):
	larghezza = len(img[0])
	altezza = len(img)
	for x in range(larghezza):
		for y in range(altezza):
			D1 = dist((x, y), (x1, y1))
			D2 = dist((x, y), (x2, y2))
			if D1 + D2 <= D:
				img[y][x] = colore
```
Nel caso in cui si volesse, invece, disegnare un'**ellisse vuota**, si dovranno colorare esclusivamente i *pixel* che distano all'incirca D dai due fuochi: per ogni *pixel* dell'immagine, dunque, si dovrà controllare che:
$$|D1+D2-D| < 1$$
In alternativa, se si vuole essere precisi, si può diminuire il valore di errore a valori più piccoli di 1, senza però esagerare. Nell'esempio seguente si utilizza il valore 0.6:
```
def draw_ellisse_vuota(img, x1, y1, x2, y2, D, colore):
	larghezza = len(img[0])
	altezza = len(img)
	for x in range(larghezza):
		for y in range(altezza):
			D1 = dist((x, y), (x1, y1))
			D2 = dist((x, y), (x2, y2))
			if abs((D1 + D2) - D) < .6:
				img[y][x] = colore
```
Vediamo ora il **cerchio**, figura che non è altro che un caso particolare di ellisse, in cui i due fuochi coincidono e in cui, dunque, la somma delle distanze di un punto del cerchio dai due fuochi rappresenta il diametro del cerchio stesso. Si potranno, dunque, implementare le funzioni utilizzate per disegnare le ellissi:
```
def draw_circle(img, x, y, r, colore):
	draw_ellisse(img, x, y, x, y, 2*r, colore)

def draw_circle_vuoto(img, x, y, r, colore):
	draw_ellisse_vuota(img, x, y, x, y, 2*r, colore)
```
In generale, per disegnare una qualsiasi curva generica (parabola, iperbole, ecc. ecc.), si potrà arrivare a un procedimento sottoforma di codice conoscendone semplicemente le proprietà principali.
___
Molte operazioni che si possono fare su qualsiasi *editor* di foto possono essere eseguite anche su Python. In particolare, approfondiamo le seguenti operazioni:
- ritagliare;
- copiare una parte dell'immagine e incollarla su un'altra;
- aggiungere un bordo;
- applicare un filtro in toni di grigio;
- modificare la luminosità;
- modificare il contrasto;
- rendere il negativo di un'immagine;
- sfocare l'immagine;
- inserire del rumore.

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
Per **inserire del rumore** in un'immagine, si potrà aggiungere del colore in maniera casuale a ciascun *pixel*; per fare ciò, basterà considerare ogni singolo *pixel* dell'immagine, e aggiungere, per ognuno dei canali RGB del *pixel*, un valore casuale nel range *[-k; k]*, assicurandosi che il risultato sia incluso nell'intervallo compreso tra 0 e 255:
```
from random import randint

def filtro_rumore_casuale(colore, k):
	return tuple(bound(C + randint(-k, k)) for C in colore)

def rumore(img, k):
	nuova = copy.deepcopy(img)
	for y, riga in enumerate(img):
		for x, colore in enumerate(riga):
			nuova[y][x] = filtro_rumore_casuale(colore, k)
	return nuova
```
___
