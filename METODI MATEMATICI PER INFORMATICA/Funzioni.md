In informatica, una funzione è l’associazione di un *input* a un *output*. Entrambi possono essere di vario genere, ma comunque parliamo di funzione quando siamo sicuri che a un input in entrata corrisponderà esattamente un output in uscita. Partendo da ciò, possiamo arrivare a una prima definizione di "**funzione**", rudimentale ma sufficientemente generale:
> Una funzione è un'associazione tra elementi di un insieme X (detto **dominio**) ed elementi di un insieme Y (detto **codominio**), in modo tale che a ogni elemento del dominio venga associato un unico elemento del codominio. Denotiamo una funzione da un dominio X a un codominio Y come:
> $$f: X → Y$$

In questa definizione, *X* e *Y* sono due insiemi arbitrari, e ogni elemento *x* *∈* *X* viene associato (o "mappato") da *f* in un unico elemento *y ∈ Y*; affermato ciò, prende valore la dicitura:
$$f(x) = y$$
e si può dire che *y* è un'**immagine** di *x* via *f*, mentre *x* è una **pre-immagine** di *y* via *f*.

Si noti che secondo la definizione proposta, una funzione non è identificabile semplicemente come una regola di associazione di elementi di un insieme a elementi di un altro insieme. La specifica di una funzione contiene la specifica del suo dominio e del suo codominio; in questo senso, due funzioni possono differire anche se la regola che le definisce è la stessa. Si nota anche che se *f: X → Y* è una funzione, allora sono funzioni anche tutte le associazioni (definite esattamente come *f*) di elementi di *X* a elementi di *Z* per qualunque soprainsieme *Z* di *Y*; analogamente, sono funzioni tutte le associazioni (definite esattamente come *f*) di tipo *W → Y* per ogni sottoinsieme *W* di *X*.

Nella matematica moderna, è abituale identificare una funzione con un insieme che corrisponde a tutti i punti del suo grafico. In generale, una funzione viene definita nel modo seguente:
> Siano *X* e *Y* due insiemi qualunque, una funzione *f* con dominio *X* e codominio *Y* è un insieme di coppie ordinate di tipo *(x, y)* con *x ∈ X* e *y ∈ Y*, tale che per ogni *x ∈ X* esiste un unica *y* *∈ Y* tale che la coppia ordinata *(x, y) ∈ f*.

Dati due insiemi *A* e *B*, denotiamo con *A × B* l’insieme delle coppie ordinate di tipo *(a, b)* con *a ∈ A* e *b ∈ B*. Questo insieme viene detto il **prodotto cartesiano** di A per B. Tecnicamente, dunque, una funzione *f: X → Y* è un sottoinsieme del prodotto cartesiano *X × Y*.

La definizione insiemistica di funzione data sopra è anche detta "**estensionale**", in quanto una funzione è identificata con l’insieme delle coppie argomento/valore, e gli insiemi sono oggetti estensionali nel senso che due insiemi con la stessa estensione (cioè gli stessi elementi) sono considerati lo stesso insieme. Al concetto estensionale di funzione si contrappone quello "**intensionale**": la stessa funzione può essere ovviamente descritta da diverse regole di associazione o da diverse formule chiuse che danno luogo allo stesso insieme di coppie ordinate
argomento/valore. Analogamente esistono sempre infiniti programmi, sintatticamente distinti, che associano esattamente gli stessi *output* agli stessi *input*. Queste diverse regole e questi diversi programmi per la stessa funzione vengono considerati **intensionalmente differenti** ma **estensionalmente identici**.

[FUNZIONI A PIU' ARGOMENTI: DISPENSA 7]

Sia *f: X → Y*, e *A ⊆ X*, definiamo l’**immagine** di *A* sotto *f*, denotata con *f(A)*, come l’insieme di tutte le immagini sotto *f* di elementi di *A*, ossia l’insieme che contiene tutti e soli gli elementi che compaiono a secondo membro di una coppia in *f ↾A*: *f(A)* = {*y ∈ Y | ∃a ∈ A* t.c. *f(a) = y*}. In particolare, se *A = X*, *f(A) = f(X)* *=* {*y ∈ Y* | *∃x ∈ X* t.c. *f(x) = y*} è l’insieme che contiene tutti e soli i valori effettivamente assunti dalla funzione *f* sugli elementi del dominio *X*. In generale, si ha *f(X) ⊆ Y* ma non necessariamente si ha *f(X) = Y*.

Se *f: X → Y* e *A ⊆ X*, vale sempre *f(A) ⊆ f(X)*; per dimostrarlo, scriviamo le definizioni dei due insiemi:
> f(X) = {y ∈ Y | ∃x ∈ X t.c. f(x) = y}
> f(A) = {y ∈ Y | ∃a ∈ A t.c. f(a) = y}

Sia *y* arbitrario in *f(A)*. Per definizione *y ∈ Y* e per qualche *a ∈ A* abbiamo *f(a) = y*. Dato che *A ⊆ X*, vale che *y ∈ Y*, e per qualche *x ∈ X* abbiamo *f(x) = y*; dunque *y ∈ f(X)*.

Esistono diversi modi di **rappresentare una funzione** (in particolare una funzione con dominio finito) che risultano comodi e adatti in diverse situazioni:
1. **rappresentazione grafica**; una funzione da un dominio *X* a un codominio *Y* si può rappresentare graficamente su un piano cartesiano, numerando le ascisse con gli elementi del dominio e le ordinate con gli elementi del codominio, e segnando punti in *(x, y)* se *f(x) = y*; dal grafico si può facilmente giudicare se quella considerata è effettivamente una funzione: a ogni punto in ascissa deve corrispondere uno e un solo punto in ordinata;
2. **rappresentazione diagrammatica**; una funzione da un dominio finito *X* a un codominio finito *Y* si può rappresentare con un diagramma a frecce disegnando a sinistra tanti pallini quanti sono gli elementi di *X*, e a destra tanti pallini quanti sono gli elementi di *Y*, e mettendo una freccia da sinistra a destra tra ogni elemento di *X* e la sua immagine secondo *f*. Anche dal diagramma si può giudicare se quella considerata è una funzione: da ogni punto a sinistra deve uscire esattamente una freccia;
3. **rappresentazione tabulare**; una funzione può rappresentarsi in molti casi in forma tabulare, enumerando sulla prima riga gli elementi del dominio e sulla seconda riga i corrispondenti elementi del codominio; anche funzioni a dominio infinito possono rappresentarsi tabularmente, ma tale rappresentazione è sempre ambigua, perchè si può continuare in infiniti modi diversi mantenendo la proprietà di essere una funzione;
4. **rappresentazione algebrica**; una rappresentazione con formula è spesso conveniente, specie se si tratta di funzioni con dominio infinito; un caso particolare è una definizione per **ricorsione**, particolarmente adatta quando si tratta di funzioni aventi per dominio i numeri naturali.

[FUNZIONI E OPERATORI INSIEMISTICI: DISPENSA 7]