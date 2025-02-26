Il concetto di **relazione** in matematica non è troppo diverso dal significato che si attribuisce generalmente a tale termine. Alcuni esempi di relazione potrebbero essere "*a* è padre di *b*" o "*n* è minore di *m*".

Volendo fare un confronto con le [[1° SEM. 2024-25/METODI MATEMATICI PER INFORMATICA/Funzioni|funzioni]], notiamo che sono due operazioni molto simili sotto alcuni punti di vista, ma le relazioni presentano due differenze fondamentali:
- una relazione non è sempre definita;
- una relazione può associare anche più "*output*" a un solo "*input*".
---
A livello insiemistico, il concetto di relazione può essere formalizzato nel modo seguente:

> Avendo due insiemi *A* e *B*, una **relazione** *R* tra (o su) *A* e *B* è un sottoinsieme del prodotto cartesiano *A* × *B*, ossia un insieme di coppie ordinate di tipo *(a, b)*, con *a* ∈ *A* e *b* ∈ *B*.

A livello simbolico, se *R* è una relazione tra *A* e *B*, con *a* ∈ *A* e *b* ∈ *B*, indichiamo tale relazione con:
$$R(a, b)$$ o anche:
$$aRb$$

Come accennato in precedenza, una relazione su due insiemi *A* e *B* si distingue da una funzione principalmente per due punti:
- possono esistere elementi *a* ∈ *A* che non sono in relazione con nessun elemento di *B*;
- possono esistere elementi *a* ∈ *A* che sono in relazione con più di un elemento di *B*.

Ad esempio, sia *A* l’insieme degli esseri umani e *B* l’insieme dei cani; la proprietà che vale di una coppia *(a, b)* ∈ *A × B* se e solo se “*a* è il padrone di *b*” è una relazione su *A* e *B*. Oppure, sia *A* l’insieme dei numeri naturali e *B* l’insieme dei numeri razionali; a proprietà che vale di una coppia *(a, b)* ∈ *A × B* se e solo se *0* ≤ *b* ≤ *a* è una relazione su *A* e *B*.

In particolare, possono esserci casi in cui **i due insiemi *A* e *B* sono uguali**, e dunque coincidono: infatti, se *R* ⊆ *A* × *A*, si afferma che *R* è una relazione su *A*. In realtà, qualsiasi relazione tra qualsiasi coppia di insiemi può essere vista come una relazione su un singolo insieme, questo perché se *R* ⊆ *A* × *B*, allora vale anche che *R* ⊆ *(A* ∪ *B)* × *(A* ∪ *B)*, e dunque *R* può essere considerata una relazione su *C* = *(A* ∪ *B)*.
___
Come per le funzioni, vi sono vari modi di **rappresentare una relazione**, tra cui:
- **grafi diretti**;
- **matrici**.

In un **grafo semplice diretto** (o **digrafo**), per rappresentare una relazione *R* tra *A* e *B* si rappresentano a sinistra gli elementi di *A* e a destra quelli di *B*; in seguito, si disegnano delle frecce, che vanno da un elemento di *A* a un elemento di *B* se e solo se *(a, b)* ∈ *R*. Ad esempio, avendo l'insieme *A* = {a, b, c, d, e} e l'insieme *B* = {1, 2, 3, 4, 5}, la relazione *R* = {*(a, 2), (a, 4), (b, 1), (b, 3), (c, 4), (d, 1), (d, 2), (d, 3)*} può essere rappresentata come:

![[grafodiretto_example.png]]

Nel caso di una relazione *R* su un singolo insieme *A*, possiamo disegnare una volta sola gli elementi di *A* e disegnare una freccia tra ogni coppia *(a₁, a₂)* di elementi di *A* per cui vale *(a₁, a₂)* ∈ *R*. In un grafo diretto, è possibile che una freccia parta e arrivi allo stesso valore, mentre non è mai possibile che due frecce distinte abbiano stessa origine e stessa destinazione.

Alternativamente, si può usare una **matrice**. Questa rappresentazione è particolarmente importante per il suo utilizzo nel rappresentare relazioni nei calcolatori elettronici, e ne permette una manipolazione abbastanza efficiente. Se *R* è una relazione tra *A* = {*a₁, a₂,* ecc. ecc.} e *B* = {*b₁, b₂,* ecc. ecc.}, la matrice di *R*, denotata M*R* è una matrice definita come segue:

![[matrixdef_relazioni.png]]

In altre parole, le righe della matrice corrispondono agli elementi di *A*, mentre le colonne agli elementi di *B*, e nella cella *(i, j)* scriviamo 1 se sussiste la relazione *R* tra *ai* e *bj* e 0 se non sussiste. I valori 1 e 0 indicano, dunque, il valore di verità di *R(ai, bj)*. Supponiamo ad esempio, di avere una relazione su *A* = {1, 2, 3, 4}, definita come *R* = {*(1, 2), (2, 4), (3, 2), (4, 2), (4, 4)*}; la matrice risultante sarà la seguente:

![[matrix_relazioni.png]]

___
Come per le funzioni, anche per le relazioni può essere utile approfondire il concetto di **inversione**. Tornando all'esempio "*a* è padre di *b*", l'inversa di tale relazione sarebbe "*b* è figlio di *a*". Possiamo definire questo concetto a livello insiemistico:

> Se *R* ⊆ *A* × *B*, denotiamo con *R⁻¹* la relazione inversa di *R*, ossia il sottoinsieme di *B* × *A* definito come:
> $$R⁻¹ = {(b, a): (a, b) ∈ R}$$

Ad esempio, con *A* = {2, 3, 4} e *B* = {2, 6, 8}, sia *R* la relazione {*(2, 2), (2, 6), (2, 8), (3, 6), (4, 8)*}; per calcolare l’inversa di *R* partendo dalla sua elencazione insiemistica basta invertire le coppie. Dunque, *R⁻¹* = {*(2, 2), (6, 2), (8, 2), (6, 3), (8, 4)*}. 

In un grafo diretto, per rappresentare l'inversa di una relazione basterà invertire la direzione di tutte le frecce presenti; in una matrice, invece, occorrerà operare una "**trasposizione**", ossia trasformare la matrice di partenza *M* in una nuova matrice *M'* in modo che le colonne di *M'* corrispondano alle righe di *M*. Ad esempio:

![[matrix_inversion.png]]

Come si può facilmente notare, la prima colonna della matrice inversa corrisponde alla prima riga di quella iniziale, la seconda colonna alla seconda riga, e così via. La matrice costruita in questo modo viene detta "matrice trasposta" di *M*. Questo fatto risulta utile nella pratica informatica, per poter calcolare l’inversa di una relazione salvata come una matrice binaria.

Possono esserci dei casi in cui invertire una relazione porterà alla stessa relazione di partenza; ad esempio, l'inversa della relazione "*a* è fratello di *b*" è "*b* è fratello di *a*", che risulta di fatto equivalente alla prima. Una relazione che gode di questa proprietà viene detta **simmetrica**. Più formalmente:

> Una relazione *R* ⊆ *A × A* è simmetrica se, per ogni *a₁, a₂* ∈ *A*, vale che *(a₁, a₂)* ∈ *R* se e solo se *(a₂, a₁)* ∈ *R*.

Si può affermare, dunque, che se una relazione *R* ⊆ *A × A* è simmetrica se e solo se *R* = *R⁻¹*.
___
Come per le funzioni, anche per le relazioni può essere utile approfondire il concetto di **composizione**. Avendo la relazione *aRb* tale per cui "*a* è padre di *b*", e la relazione *bSc* tale per cui "*b* è marito di *c*, la relazione composta tra *R* e *S* è la relazione *T* tale per cui "*a* è suocero di *c*". Risulta evidente che per comporre due relazioni *R* e *S* occorre che *R* sia una relazione tra *A* e *B*, e che *S* sia una relazione tra *B* e *C*. Possiamo definire questo concetto a livello insiemistico:

> Se *R* ⊆ *A × B* e *S* ⊆ *B × C*, la relazione composta (o composizione) di *R* e *S* è la relazione tra *A* e *C* che sussiste tra *a* ∈ *A* e *c* ∈ *C* se e solo se esiste un
*b* ∈ *B* tale per cui valgano *aRb* e *bSc*. La relazione composta viene denotata come: 
$$S ◦ R$$

È possibile comporre una relazione con sé stessa: quando ciò avviene, si parla di "**iterazione**". Ad esempio, la composta della relazione P “*a* e padre di *b*” con sé stessa corrisponde alla relazione “*a* è nonno di *b*”. Se si opera tale composizione di nuovo, ottenendo *P ◦ (P ◦ P)*, si arriva alla relazione “*a* è bisnonno di *b*”.

Per comprendere meglio come funziona la composizione tra relazioni, analizziamo un esempio concreto. Supponiamo di avere due relazioni *R* ed *S*, tali per cui *R* = {*(a, b), (b, b), (b, d), (c, a), (d, a)*} e *S* = {*(a, d), (a, b), (b, c), (d, b)*}. La composta *(S ◦ R)* si può “calcolare” partendo dal primo elemento di R, ossia *(a, b)*, e cercando in *S* una qualsiasi coppia che inizi con il secondo elemento della coppia (in questo caso, b), ossia una qualsiasi coppia di tipo *(b, x)* per qualche *x* ∈ *C*; per ogni coppia di questo tipo, sappiamo che *(a, x)* si trova nella relazione composta *(S ◦ R)*. Operando tale procedimento per tutte le coppie considerate, si otterrà che:
$$(S ◦ R) = {(a, c), (b, c), (b, b), (c, d), (c, b), (d, b), (d, d)}$$
[COMPOSIZIONE TRAMITE PRODOTTO MATRICIALE: DISPENSA 11]
___
> Una relazione *R* ⊆ *A × A* è detta "**transitiva**" se vale che, per ogni *a, b, c* ∈ *A*, se valgono *aRb* e *bRc* allora vale anche *aRc*.

Ad esempio, la relazione "*a* è padre di *b*" non è transitiva, perché dire che "*a* è padre di *b*" e che "*b* è padre di *c*" non equivale a dire che "*a* è padre di *c*"; tuttavia, una relazione del tipo "*n* è minore di *m*" è invece transitiva, in quanto se "*n* è minore di *m*" e "*m* è minore di *o*", allora necessariamente vale che "*n* è minore di *o*".

Si noti che la definizione di transitività è espressa con un quantificatore universale ("*per ogni a, b, c ∈ A*"), seguito da un condizionale (*se... allora...*). Questa definizione non richiede che una relazione *R* soddisfi sia *aRb* che *bRc* per ogni *a, b, c* ∈ *A*; richiede, invece, che, se valgono sia *aRb* che *bRc*, allora deve
valere anche *aRc*. In altre parole, una coppia *(a, b)* di una relazione *R* tale per cui non esiste nessuna coppia di forma *(b, x)* in *R* non ha nessun effetto sulla transitività o meno di *R*.

La definizione generale data a inizio paragrafo lascia, in realtà, spazio per alcuni casi particolari.

Supponiamo ad esempio, di avere *A* = {1, 2, 3, 4, 5}, e di avere la relazione *R* = {*⊘*}. Per quanto possa sembrare contro-intuitivo, *R* rappresenta una relazione transitiva su A. Infatti, la definizione di transività prevede che per ogni scelta di *a, b, c* ∈ *A* (dunque, non necessariamente distinti), se valgono *aRb* e *bRc* allora vale anche *aRc*. Se non si dà mai una configurazione di tipo *aRb* e *bRc* per qualche *a, b, c* ∈ *A*, la pre-condizione della definizione di transitività non è mai verificata, e quindi l’implicazione è vera, o meglio, "**vera a vuoto**".

Prendiamo sempre *A* = {1, 2, 3, 4, 5}, e consideriamo stavolta la relazione *R* = {*(1, 2), (3, 4), (1, 5)*}. Anche in questo caso si tratta di una relazione transitiva. Infatti, non vi è alcuna possibilità di configurazioni di tipo *aRbRc*, e dunque la pre-condizione è vera a vuoto.

Consideriamo, infine, sullo stesso insieme *A* = {1, 2, 3, 4, 5}, la relazione *R* = {*(1, 1), (2, 2), (3, 3), (4, 4)*}. Anche in questo caso si tratta di una relazione transitiva: infatti, per ogni configurazione di tipo *aRbRc*, si ha anche *aRc*. Le uniche configurazioni di questo tipo sono *1R1R1*, *2R2R2*, *3R3R3* e *4R4R4*. In tutti i casi, la
post-condizione dell’implicazione che definisce la transività è verificata: *1R1*, *2R2*, *3R3* e *4R4*.

A questo punto, può essere utile approfondire le condizioni che portano alla negazione della transitività di una relazione *R*. Procedendo passo passo, si ottiene che *R* non è transitiva se e solo se:
- non è vero che per ogni *a, b, c* ∈ *A*, se *aRb* e *bRc* allora *aRc*;
- c’è almeno una scelta di *a, b, c* ∈ *A* tali per cui non è vero che se *aRb* e *bRc* allora *aRc*;
- c’è almeno una scelta di *a, b, c* ∈ *A* tali per cui valgono *aRb* e *bRc* ma non *aRc*.

Ad esempio, la relazione *R* = {*(1, 2), (1, 3), (2, 2), (2, 5), (5, 2), (3, 4)*} su *A* = {1, 2, 3, 4, 5} non è transitiva: per dimostrarlo, sarà sufficiente esibire una scelta di *a*, *b*, *c* tali per cui *(a, b)* ∈ *R* e *(b, c)* ∈ *R* ma *(a, c)* ∉ *R*. Una scelta di questo tipo è, per esempio, a = 1, b = 3, c = 4.
