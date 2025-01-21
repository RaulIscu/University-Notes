Il concetto di "**relazione di equivalenza**" si basa sul concetto matematico di identità. Infatti, mentre quest'ultimo gode delle seguenti proprietà:
1. per ogni *n* ∈ *N*, *n = n*;
2. per ogni *n, m* ∈ *N*, se *n = m* allora *m = n*;
3. per ogni *n, m, q* ∈ *N*, se *n = m* e *m = q* allora *n = q*;

una relazione *R* su un insieme *A* è una relazione di equivalenza se e solo se gode delle seguenti proprietà:
1. per ogni *a* ∈ *A*, *aRa*;
2. per ogni *a, b* ∈ *A*, se *aRb* allora *bRa*;
3. per ogni *a, b, c* ∈ *A*, se *aRb* e *bRc* allora *aRc*.

Insomma, una relazione *R* ⊆ *A × A* può dirsi una relazione di equivalenza se e solo se è riflessiva (punto 1), simmetrica (punto 2) e transitiva (punto 3). Ad esempio, sia *A* un insieme di studenti, e la relazione *aRb* tale per cui *a* e *b* hanno la stessa età: *R* è una relazione di equivalenza, perché uno studente ha ovviamente la stessa età di sé stesso, perché se lo studente *a* ha la stessa età dello studente *b* allora vale anche il contrario, e perché se *a* ha la stessa età di *b* e *b*, a sua volta, ha la stessa età di *c*, allora *a* avrà necessariamente la stessa età di *c*.

In generale, se definisco una relazione *R* su *A* come *aRb* se e solo se *a* e *b* hanno un certo valore assegnato identico, quello che ottengo è una relazione di equivalenza. Tuttavia, non tutte le relazioni di equivalenza si ottengono in questo modo: ad esempio, una relazione *aRb* tale per cui *a* è parente di *b* è anch'essa una relazione di equivalenza.
___
Se *R* è una relazione binaria su un insieme *A*, e *a* è un elemento di *A*, possiamo sempre considerare l’insieme degli elementi *b* ∈ *A* che sono in relazione *R* con *a*, ossia l’insieme {b ∈ B: *aRb*}; questo insieme viene detto "**vicinato**" di *a*. Per *R* arbitraria, il vicinato può essere anche vuoto. Se *R* è una relazione di
equivalenza, il vicinato di *a* viene chiamato "**classe di equivalenza**" e viene denotato con "**[a]*R***". Questo concetto presenta delle proprietà interessanti.

Consideriamo, ad esempio, gli interi *Z* e stabiliamo una relazione *aRb* se e solo se *a* e *b* hanno lo stesso resto nella divisione per 2. Notiamo subito che si tratta di una relazione di equivalenza, anche solo per il fatto che è una relazione che sussiste tra due elementi se e solo se presentano un certo valore assegnato identico. Dato che i possibili resti della divisione per 2 di un intero sono solo 0 e 1, è facile osservare che un arbitrario intero sarà necessariamente in relazione *R* o con 0 o con 1. Dunque, sia [p]*R*  la classe di equivalenza di *p* modulo *R*, si osserva che per ogni intero *p* si ha che *p* ∈ [0]*R* oppure p ∈ [1]*R*, a seconda che *p* sia pari o dispari; inoltre, si osserva che se *p* ∈ [0]*R*, allora [p]*R* = [0]*R* (ogni altro numero che ha lo stesso resto di *p* nella divisione per 2 ha anche lo stesso resto di 0), e la stessa cosa vale per [1]*R*. Dunque, presi due interi *p* e *q* a cui si applica la relazione *R*, le loro classi di equivalenza o coincidono oppure sono
completamente disgiunte, e la relazione *R* su *Z* determina soltanto due classi di equivalenza: [0]*R* e [1]*R*.

Generalizzando, si può affermare che **ogni relazione di equivalenza determina una partizione dell'insieme su cui è definita**, ossia una scomposizione di *A* come unione di suoi sottoinsiemi a due a due disgiunti. Perciò, sia *R* ⊆ *A × A* una relazione di equivalenza, per *a* ∈ *A* definiamo:
$$[a]_R = {b ∈ A: aRb}$$
detta classe di equivalenza di *a*. Valgono i seguenti punti:
1. per ogni *a* ∈ *A*, [a]*R* ≠ ∅;
2. per ogni *a, b* ∈ *A*, si ha che [a]*R* ∩ [b]*R* = ∅ oppure che [a]*R* = [b]*R*.

Una **partizione** di un insieme *A* è definita come una famiglia {*Ci*: *i* ∈ *I*} di insiemi non vuoti *Ci* ⊆ *A*, dove *I* è un insieme qualunque detto "insieme di indici", tali per cui:
1. per ogni *a* ∈ *A*, esiste un *i* ∈ *I* tale che *a* ∈ *Ci*;
2. per *i*, *j* ∈ *I*, se *i* ≠ *j* allora *Ci* ∩ *Cj* = ∅.

Si osserva che, dato che ogni *Ci* è un sottoinsieme di *A* per ipotesi, l'unione di tutti gli insiemi *Ci* sarà anch'essa un sottoinsieme di *A*; è anche vero, per il punto 1, che *A* è un sottoinsieme dell'unione di tutti gli insiemi *Ci* (tutti gli elementi di *A* appartengono a un qualche insieme *Ci*). Dunque, si può affermare che l'insieme *A* coincide con l'unione di tutti i suoi sottoinsiemi *Ci*, e dunque che una partizione di *A*, oltre ad essere mutualmente esclusiva, è necessariamente anche esaustiva.

Dai punti analizzati finora, segue che, sia {*Ci*: *i* ∈ *I*} una partizione di *A*, la relazione *R* ⊆ *A* × *A* definita ponendo *aRb* se e solo se esiste un *i* ∈ *I* tale che *a, b* ∈ *Ci* è una relazione di equivalenza su *A*. Si osserva, inoltre, che se *R* ⊆ *A × A* e *S* ⊆ *A × A* determinano le stesse classi di equivalenza, allora sono la stessa relazione.