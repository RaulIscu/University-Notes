Se *A* e *B* sono insiemi finiti, risulta abbastanza evidente che esiste una biezione tra *A* e *B* se e solo se i due insiemi hanno lo stesso numero di elementi. In questo caso, possiamo anche dire che gli insiemi *A* e *B* hanno la stessa **cardinalità**, e si scrive ***#(A) = #(B)***.

Partendo da questo ragionamento, si esplicitano in maniera generale i collegamenti tra iniettività, suriettività e biettività con la cardinalità di due insiemi:
- se esiste un'iniezione in *f: A → B*, allora *#(A) ≤ #(B)*;
- se esiste una suriezione in *f: A → B*, allora *#(A) ≥ #(B)*;
- se esiste una biezione in *f: A → B*, allora *#(A) = #(B)*.
___
In particolare, dall'ultimo degli assunti appena fatti, si ottiene il principio generale dell'**equicardinalità**:

> Siano *A* e *B* due insiemi; si dice che *A* e *B* hanno la stessa cardinalità se esiste una biezione tra *A* e *B*.

L'equicardinalità definisce una relazione tra due insiemi *A* e *B*, che sussiste se e solo se esiste una biezione tra i due insiemi. Tuttavia, non bisogna presupporre che questa relazione (*#(A) = #(B)*) sia una vera identità tra due oggetti *#(A)* e *#(B)*; possiamo però assicurarci che la relazione definita soddisfi alcune proprietà fondamentali dell’identità, dunque si comporta come un'identità.

Per ogni insieme *A*, esiste sempre una biezione tra *A* e sé stesso, dunque:

> Per ogni insieme *A*, vale che *#(A) = #(A)*.

Si dice, quindi, che la relazione di equicardinalità è **riflessiva**. Inoltre:

> Per ogni coppia di insiemi *A* e *B*, se vale che *#(A) = #(B)* allora vale anche che *#(B) = #(A)*.

Si noti che quest'implicazione non è scontata in base alle definizioni, in quanto *#(A) = #(B)* significa che esiste una biiezione in *f: A → B*, ma non necessariamente che esista anche in *h: B → A*; ciò può essere affermato con sicurezza in quanto ogni funzione biettiva è anche invertibile. Dunque, si dice che la relazione di equicardinalità e **simmetrica**: se *A* è in relazione con *B*, allora *B* è in relazione con *A*. Infine:

> Per gruppi di insiemi *A*, *B* e *C*, se vale che *#(A) = #(B)* e che *#(B) = #(C)*, allora vale anche che *#(A) = #(C)*.

Infatti, *#(A) = #(B)* significa che esiste una biezione *f: A → B*; *#(B) = #(C)* significa che esiste una biezione *g: B → C*; possiamo, quindi, concludere che *#(A) = #(C)*, ossia che esiste una biezione *h: A → C*, in quanto la composizione di biezioni è una biezione. Dunque, si dice che la relazione di equicardinalità è **transitiva**: se *A* è in relazione con *B* e *B* è in relazione con *C*, allora *A* è in relazione con *C*.