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
-  **grafi diretti**;
- **matrici**.

In un **grafo semplice diretto** (o **digrafo**), per rappresentare una relazione *R* tra *A* e *B* si rappresentano a sinistra gli elementi di *A* e a destra quelli di *B*; in seguito, si disegnano delle frecce, che vanno da un elemento di *A* a un elemento di *B* se e solo se *(a, b)* ∈ *R*. Ad esempio, avendo l'insieme *A* = {*a, b, c, d, e*} e l'insieme *B* = {*1, 2, 3, 4, 5*}, la relazione *R* = {*(a, 2), (a, 4), (b, 1), (b, 3), (c, 4), (d, 1), (d, 2), (d, 3)*} può essere rappresentata come:

![[grafodiretto_example.png]]

Nel caso di una relazione *R* su un singolo insieme *A*, possiamo disegnare una volta sola gli elementi di *A* e disegnare una freccia tra ogni coppia *(a₁, a₂)* di elementi di *A* per cui vale *(a₁, a₂)* ∈ *R*. In un grafo diretto, è possibile che una freccia parta e arrivi allo stesso valore, mentre non è mai possibile che due frecce distinte abbiano stessa origine e stessa destinazione.

[DISPENSA 11]

___
