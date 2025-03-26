Cominciamo ad analizzare nel dettaglio le funzionalità di AWT partendo dall'elemento più basilare di qualsiasi interfaccia grafica: una **finestra**. Probabilmente le due classi più importanti legate alle finestre sono due, ossia **`Frame`** e **`Panel`**.

**`Frame`** incapsula una semplice finestra, e viene usata tipicamente per creare una finestra standard per applicazioni; **`Panel`**, invece, permette di creare dei "contenitori" in cui possono essere inserite altre componenti. Per comprendere meglio la funzionalità di queste due classi, è utile approfondire le gerarchie di classe relative ad esse: la classe `Frame` è una sottoclasse di `Window`, mentre quest'ultima e `Panel` sono a loro volta sottoclassi di `Container`; essa, infine, rappresenta una sottoclasse di `Component`.

Analizziamo queste classi partendo dalla cima della gerarchia:
- **`Component`** è una classe astratta che incapsula tutti gli attributi di un componente grafico: ad eccezione dei menù, infatti, tutti gli elementi di una UI che vengono visualizzati sullo schermo rappresentano delle istanze di sottoclassi di `Component`. All'interno di tale classe vengono definite centinaia di metodi, responsabili per gestire eventi (come *input* da mouse o tastiera), posizionare e ridimensionare finestre, ecc. ecc. Inoltre, un oggetto della classe `Component` conserva in memoria i colori relativi a sfondo e a primo piano, oltre che il *font* corrente.
- **`Container`**, sottoclasse di `Component`, aggiunge metodi che permettono ad altri oggetti di tipo `Component` di essere annidati al suo interno; del resto, essendo un `Container` un'istanza di `Component`, è possibile annidare dei `Container` all'interno di altri `Container`. Un oggetto di questa classe gestisce il posizionamento di qualsiasi componente contenuta al suo interno.
- **`Panel`**, sottoclasse di `Container`, rappresenta un *container* annidabile e visualizzabile sullo schermo, a cui possono essere aggiunti componenti mediante il metodo `add()`; inoltre, è possibile manipolare manualmente tali componenti tramite metodi come `setLocation()`, `setSize()`, `setPreferredSize()` o `setBounds()`.
- **`Window`**, anch'essa sottoclasse di `Container`, permette di creare una finestra *top-level*, ossia che non è contenuta in nessun altro oggetto, e si situa quindi direttamente al livello del *desktop*.
- **`Frame`**, sottoclasse di `Window`, è il tipo di finestra che verrà solitamente istanziata, poiché aggiunge un titolo, un menù, dei margini e degli angoli ridimensionabili agli oggetti appartenenti alla superclasse `Window`.

Non appartenente alla gerarchia, ma comunque importante, è la classe **`Canvas`**, sottoclasse di `Component`, che incapsula finestre vuote su cui è possibile disegnare.
___
Come accennato, tipicamente, lavorando con **finestre**, si istanzieranno oggetti di tipo **`Frame`**. Ci sono due tipi di **[[Classi|costruttori]]** di oggetti appartenenti a questa classe:

```
Frame();
Frame(String title);
```

Nel primo caso, viene creata una finestra di base che non possiede alcun titolo; nel secondo caso, invece, viene creata una finestra che ha come titolo la stringa *title* inserita come parametro del costruttore. Nel caso in cui si verifichi un tentativo di istanziamento di un `Frame` in un ambiente che non supporta interazione con l'utente, verrà lanciata una **`HeadlessException`**.

Le **dimensioni** di questa finestra non possono essere specificate al momento dell'inizializzazione, ma dovranno essere assegnate in seguito. Per fare ciò, si utilizza il metodo **`setSize(int newWidth, int newHeight)`**, che assegnerà alla finestra in questione la larghezza *newWidth* e l'altezza *newHeight*; in alternativa, è possibile utilizzare il metodo **`setSize(Dimension newSize)`**, che assegnerà alla finestra in questione larghezza e altezza tratti dai corrispondenti campi dell'oggetto *newSize* preso come parametro. Per ottenere le dimensioni di una finestra, sempre sottoforma di un oggetto della classe `Dimension`, si usa invece il metodo **`getSize()`**.

Dopo l'istanziamento di un oggetto di tipo `Frame`, esso non sarà automaticamente **visibile**. Per renderlo tale, si dovrà utilizzare il metodo:

```
setVisible(boolean);
```

Se come parametro viene passato `true`, la finestra diventerà visibile, mentre se il parametro è `false`, la finestra rimarrà nascosta.

È possibile, poi, **modificare il titolo** della finestra, utilizzando il metodo:

```
setTitle(String newTitle);
```

che assegnerà alla finestra su cui viene invocato il titolo *newTitle*.

Sarà necessario, inoltre, inserire un modo per **chiudere la finestra** e rimuoverla dallo schermo. Se la finestra in questione non è la finestra *top-level* dell'applicazione, per fare ciò basterà utilizzare `setVisible(false)`; se, invece, si tratta della finestra principale, bisogna rilevare un evento di chiusura di tale finestra, implementando il metodo **`windowClosing()`** dell'interfaccia **`WindowListener`**.
___
**Visualizzare un *output* in una finestra** avviene generalmente tramite il metodo **`paint()`**, invocato dal sistema *run-time*. Questo metodo è definito nella classe `Component`, ed è sovrascritto nelle sottoclassi `Container` e `Window`; perciò, è invocabile da istanze della classe `Frame`. Il metodo `paint()` viene invocato in un'applicazione AWT ogni volta che il suo *output* va ridisegnato, che è una situazione che può avvenire in vari casi (sovrascrivere la finestra con altre finestre, minimizzare e poi riaprire la finestra, o anche banalmente quando la finestra viene visualizzata per la prima volta). Ciò implica che il programma debba avere un modo per conservare il suo *output*, così da poterlo rivisualizzare ogni volta che viene invocato `paint()`.

Cominciamo, quindi, a visualizzare qualcosa nella nostra finestra. Se volessimo, ad esempio, **visualizzare una stringa**, andremmo a utilizzare il metodo **`drawString()`**, membro della classe **`Graphics`**. Esso prende in *input* i seguenti parametri:

```
drawString(String messaggio, int x, int y);
```

dove *messaggio* è la stringa che verrà visualizzata, mentre *x* e *y* sono le coordinate (in termini di *pixel*) d'inizio della stringa. È importante ricordare che tale metodo non riconosce caratteri di accapo (`\n`); dunque, se si vuole avere più di una riga di testo, bisognerà farlo manualmente, invocando più volte il metodo e specificando ogni volta le coordinate opportune.

È possibile, poi, **modificare il colore dello sfondo e del primo piano** di una finestra. I metodi utilizzati per fare ciò sono i seguenti:

```
setBackground(Color newColor);
setForeground(Color newColor);
```

Entrambi questi metodi vengono definiti nella classe `Component`. Come si può vedere dal codice, questi metodi prendono un parametro di tipo **`Color`**, una classe che definisce varie costanti corrispondenti ai colori più frequenti e comuni, tra cui `Color.black`, `Color.white`, `Color.red`, e così via.

Esistono anche i metodi **`getBackground()`** e **`getForeground()`**, per ottenere il colore delle rispettive componenti di un `Frame` esistente (anche questi metodi vengono definiti nella classe `Component`).

Generalmente, un applicazione aggiorna l'*output* della sua finestra solo quando viene invocato il metodo `paint()`; viene dunque da chiedersi, come può il programma stesso provocare un aggiornamento, e richiamare dunque questo metodo, ogni volta che dovrà mostrare un nuovo *output*. Per fare ciò, si utilizzerà il metodo **`repaint()`**, definito in `Component`. La chiamata di questo metodo porterà a invocare il metodo `update()` (anch'esso definito nella stessa classe), che a sua volta richiamerà nuovamente il metodo `paint()`: perciò, per trasmettere un *output* a una finestra, sarà sufficiente conservare tale *output* e richiamare il metodo `repaint()`.

Il metodo `repaint()` presenta quattro versioni diverse:

```
repaint();
repaint(int x, int y, int width, int height);
repaint(long maxDelay);
repaint(long maxDelay, int x, int y, int width, int height);
```

La prima versione del metodo, nonché la più semplice, porta l'intera finestra a essere ridisegnata. La seconda, invece, specifica una regione precisa da ridisegnare, il cui angolo in alto a sinistra è definito dalle coordinate *x* e *y* mentre la larghezza e l'altezza della regione corrispondono rispettivamente a *width* e *height*; a volte, è preferibile questa versione alla prima, soprattutto in termini di efficienza e di costo computazionale.

Le ultime due versioni hanno parametri strutturati in maniera simile ai primi due, ma con l'aggiunta del parametro *maxDelay*, ossia il tempo massimo (in millisecondi) che è concesso che passi tra la chiamata del metodo `repaint()` e la corrispondente chiamata di `update()`; questo perché `repaint()`, di default, fa una richiesta di ridisegnamento che non viene necessariamente eseguita subito, soprattutto su *hardware* più lenti. In alcuni contesti, dunque, è necessario stabilire un limite all'ammontare di *delay* con cui la finestra su cui si sta lavorando viene aggiornata.
___
Tutti gli *output* che vengono visualizzati in una finestra devono passare per un ***graphics context***, oggetto incapsulato all'interno della classe `Graphics`; tendenzialmente, un oggetto di questo tipo viene o passato come parametro a metodi come `paint()` o `update()`, oppure può essere ottenuto mediante il metodo **`getGraphics()`**, definito all'interno di `Component`.

La classe **`Graphics`**, tra le altre cose, definisce vari metodi che permettono di disegnare linee, cerchi, archi, e molto altro, sia con il solo contorno sia riempiti. Nel caso in cui una figura disegnata in questo modo risulti andare oltre i bordi della finestra in cui si sta lavorando, essa verrà automaticamente clippata.

Per disegnare una **linea**, si utilizza il seguente metodo:

```
drawLine(int startX, int startY, int endX, int endY);
```

dove *startX* e *startY* sono le coordinate del punto di partenza, mentre *endX* ed *endY* sono le coordinate del punto di arrivo della linea.

Per disegnare un **rettangolo**, si utilizzano i seguenti metodi:

```
drawRect(int x, int y, int width, int height);
fillRect(int x, int y, int width, int height);
```

dove *x* e *y* indicano le coordinate dell'angolo in alto a sinistra del rettangolo, mentre *width* e *height* rappresentano rispettivamente la larghezza e l'altezza di quest'ultimo. Il primo metodo viene utilizzato per disegnare solo un contorno, mentre il secondo permette di avere un rettangolo pieno.

Per disegnare un **rettangolo dagli angoli arrotondati**, si utilizzano i seguenti metodi:

```
drawRoundRect(int x, int y, int width, int height, int xDiam, int yDiam);
fillRoundRect(int x, int y, int width, int height, int xDiam, int yDiam);
```

Questi metodi risultano analoghi a quelli relativi a rettangoli normali, con l'aggiunta dei parametri *xDiam* e *yDiam*, che rappresentano rispettivamente il diametro dell'arco arrotondante sull'asse x e quello dell'arco sull'asse y.

Per disegnare un'**ellisse**, si utilizzano i seguenti metodi:

```
drawOval(int x, int y, int width, int height);
fillOval(int x, int y, int width, int height);
```

L'ellisse desiderata verrà disegnata come iscritta nel rettangolo avente l'angolo in alto a sinistra posto nel punto (*x*, *y*), larghezza pari a *width* e altezza pari a *height*. Se si vuole disegnare un **cerchio**, sarà sufficiente specificare un quadrato come figura all'interno della quale iscrivere l'ellisse.

Per disegnare un **arco**, si utilizzano i seguenti metodi:

```
drawArc(int x, int y, int width, int height, int startAngle, int sweepAngle);
fillArc(int x, int y, int width, int height, int startAngle, int sweepAngle);
```

Anche in questo caso, l'arco viene teoricamente iscritto in un rettangolo avente l'angolo in alto a sinistra posto nel punto (*x*, y), larghezza pari a *width* e altezza pari a *height*; inoltre, l'arco viene disegnato a partire da *startAngle* per la distanza angolare specificata da *sweepAngle*. Entrambi questi ultimi due parametri sono espressi in gradi, e 0 gradi corrispondono all'orizzontale; inoltre, se *sweepAngle* ha segno positivo, l'arco viene disegnato in senso antiorario, mentre se *sweepAngle* ha segno negativo, l'arco viene disegnato in senso orario.

Per disegnare dei **poligoni** con un numero arbitrario di vertici, si utilizzano i seguenti metodi:

```
drawPolygon(int[] x, int[] y, int numPoints);
fillPolygon(int[] x, int[] y, int numPoints);
```

I vertici del poligono hanno coordinate specificate dalle coppie di interi in stessi indici degli *array* *x* e *y*, mentre il numero di vertici del poligono va specificato in *numPoints*.

[pag. 1265]