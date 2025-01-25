Se *A* e *B* sono insiemi finiti, risulta abbastanza evidente che esiste una biezione tra *A* e *B* se e solo se i due insiemi hanno lo stesso numero di elementi. In questo caso, possiamo anche dire che gli insiemi *A* e *B* hanno la stessa **cardinalità**, e si scrive:
$$#(A) = #(B)$$
Partendo da questo ragionamento, si esplicitano in maniera generale i collegamenti tra iniettività, suriettività e biettività con la cardinalità di due insiemi:
- se esiste un'iniezione in *f: A → B*, allora *#(A) ≤ #(B)*;
- se esiste una suriezione in *f: A → B*, allora *#(A) ≥ #(B)*;
- se esiste una biezione in *f: A → B*, allora *#(A) = #(B)*.
___
In particolare, dall'ultimo degli assunti appena fatti, si ottiene il principio generale dell'**equicardinalità**:
> Siano *A* e *B* due insiemi; si dice che *A* e *B* hanno la stessa cardinalità se esiste una biezione tra *A* e *B*.

L'equicardinalità definisce una relazione tra due insiemi *A* e *B*, che sussiste se e solo se esiste una biezione tra i due insiemi. Tuttavia, non bisogna presupporre che questa relazione (*#(A) = #(B)*) sia una vera identità tra due oggetti *#(A)* e *#(B)*; possiamo però assicurarci che la relazione definita soddisfi alcune proprietà fondamentali dell’identità, dunque si comporta come un'identità.

Per ogni insieme *A* vale *#(A) = #(A)*, perché esiste sempre una biezione tra A e A: si dice che la relazione di equicardinalità è **riflessiva**. Per insiemi *A*, *B* se vale che *#(A) = #(B)*, allora vale anche che *#(B) = #(A)*; si noti che quest'implicazione non è scontata in base alle definizioni, in quanto *#(A) = #(B)* significa che esiste una biiezione in *f: A → B*, ma non necessariamente che esista anche in *h: B → A*. Ciò può essere affermato con sicurezza in quanto ogni funzione biettiva è anche invertibile. Dunque, si dice che la relazione di equicardinalità e **simmetrica**: se *A* è in relazione con *B*, allora *B* è in relazione con *A*.

Per insiemi *A*, *B*, *C*, se vale *#(A) = #(B)* e *#(B) = #(C)* allora vale *#(A) = #(C)*: *#(A) = #(B)* significa che esiste una biiezione *f: A → B*; *#(B) = #(C)* significa che esiste una biezione *g: B → C*; possiamo, quindi, concludere che *#(A) = #(C)*, ossia che esiste una biezione *h: A → C*, in quanto la composizione di biezioni è una biezione. Dunque, si dice che la relazione di equicardinalità è **transitiva**: se *A* è in relazione con *B* e *B* è in relazione con *C*, allora *A* è in relazione con *C*.
___
Cosa accade se si generalizzano queste idee a insiemi arbitrari, in particolare a insiemi infiniti? L’idea, dovuta al matematico Georg Cantor (1845-1918), è una delle idee più rivoluzionarie della matematica dell’800, e ha avuto grande impatto sulle scienze matematiche dei secoli successivi.

Risulta facile dimostrare che esiste una biezione tra *N = {1, 2, 3, 4, ...}* e *P = {2, 4, 6, 8, ...}*. La funzione *f: N → P* tale che *f(n) = 2n* è una biezione; si può, dunque, scrivere che *#(N) = #(P)*. Si osservi che *P* è un sottoinsieme proprio di *N*, ossia è un sottoinsieme di *N* ma non coincide con esso (anzi, *P* possiede più o meno la metà degli elementi di *N*); eppure, secondo la nostra definizione, i due insiemi hanno la stessa cardinalità, ossia lo stesso numero di elementi. Questa proprietà di N può essere scelta come definizione di **insieme infinito**, in una trattazione assiomatica rigorosa (e così è stato fatto dai matematici di fine XIX secolo).