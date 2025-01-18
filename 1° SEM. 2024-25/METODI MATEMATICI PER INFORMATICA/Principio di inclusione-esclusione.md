Il [[Principio additivo|principio additivo]], sostanzialmente, afferma che se gli elementi di un insieme sono di due tipi distinti e mutualmente esclusivi, allora il loro numero è la somma degli elementi del primo tipo e degli elementi del secondo tipo. Lo stesso principio, indirettamente, ci permette di contare insiemi definiti da proprietà disgiuntive (*A* o *B*), anche nel caso in cui queste proprietà non siano mutualmente esclusive.

Per comprendere meglio in che modo ciò avviene, consideriamo un esempio. Supponiamo di voler contare il numero di possibili targhe automobilistiche che contengono una P in prima posizione o una R in ultima posizione. Possiamo effettuare una partizione nel modo seguente:
- tipo *A*, composto dalle targhe che contengono una P in prima posizione;
- tipo *B*, composto dalle targhe che contengono una R in ultima posizione.

Il numero di elementi presenti nei due tipi è facilmente calcolabile mediante il [[Principio moltiplicativo|principio moltiplicativo]]; tuttavia, si può notare che i tipi della partizione non sono mutualmente esclusivi. Infatti, in *A* vengono contate una volta tutte le targhe che hanno P in prima posizione e non hanno R in ultima posizione (chiamiamo questo insieme *X*) e una volta tutte le targhe che hanno sia P in prima posizione che R in ultima posizione (chiamiamo questo insieme Y); invece, in *B* vengono contate una volta tutte le targhe che hanno R in ultima posizione e non hanno P in prima posizione (chiamiamo questo insieme *Z*) e una volta tutte
le targhe che hanno sia P in prima posizione che R in ultima posizione (insieme che coincide con *Y*). Gli elementi di *Y* sono contati esattamente due volte nella somma *A + B*: per ottenere la quantità corretta, bisogna dunque sottrarre il numero di elementi in *Y*, che corrisponde a (*A ∩ B*). L’insieme delle targhe con P in prima o R in ultima è dunque:
$$A + B − (A ∩ B)$$

È possibile generalizzare questo concetto, enunciando il "**principio di inclusione-esclusione**", che nella sua forma a due termini afferma che:
$$(A ∪ B) = A + B − (A ∩ B)$$

Si osserva facilmente che la forma del principio additivo, in cui i tipi *A* e *B* sono esclusivi, è un caso particolare della forma più generale, perché se i tipi sono esclusivi il termine (A ∩ B) è uguale a 0.
___
Possiamo applicare il principio di inclusione-esclusione a due termini ogni volta che dobbiamo contare l’unione tra due insiemi. Questo accade, per esempio, quando il problema è espresso direttamente in forma di disgiunzione, o mediante l’espressione "almeno".

Consideriamo, ad esempio, una classe con 24 studenti, sottoposti a due test di valutazione, supponendo che:
- 18 studenti superano il primo test;
- 15 studenti superano il secondo test;
- 12 studenti superano entrambi i test.

Si vuole contare il numero di studenti che superano almeno un test. Osserviamo subito che il costrutto "almeno" è parente stretto dell’oppure: in questo caso, infatti, "superare almeno un test" significa superare il primo test oppure superare il secondo test. Possiamo quindi applicare il principio additivo, con la seguente partizione:
- tipo *A*, composto dagli studenti che superano il primo test;
- tipo *B*, composto dagli studenti che superano il secondo test.

Nella somma *A + B*, ossia 18 + 15, stiamo contando esattamente due volte tutti e soli gli studenti che superano sia il primo che il secondo test, ossia gli studenti che sono simultaneamente di tipo *A* e di tipo *B*: bisogna dunque sottrarre questi studenti dalla somma. In questo caso, sappiamo esattamente che gli studenti che superano entrambi i test, ossia gli studenti appartenenti a *(A ∩ B)*, sono 12. Gli studenti di tipo A o di tipo B, ossia gli studenti che superano almeno un test, sono dunque:
$$18 + 15 − 12 = 21$$

Il principio di inclusione-esclusione risulta utile anche in altre situazioni, in cui il problema non è direttamente un problema disgiuntivo o di unione.

Supponiamo, ad esempio, di voler contare il numero di targhe che contengono almeno una T e almeno un 9. Una tipizzazione diretta risulta laboriosa, ed è più conveniente effettuare un [[Passaggio al complemento|passaggio al complemento]]: ci chiediamo, quindi, quante sono le targhe che non contengono una T o non contengono un 9? Per calcolare questa quantità, effettuiamo la seguente partizione:
- tipo *A*, ossia l'insieme delle targhe che non contengono una T;
- tipo *B*, ossia l'insieme delle targhe che non contengono un 9.

L’insieme *C* = *A ∪ B* è quello che ci interessa. Possiamo facilmente contare la cardinalità di *A* e di *B*:
$$A = 25^2 × 10^3 × 25^2$$
$$B= 26^2 × 9^3 × 26^2$$

A questo punto, per avere la cardinalità corretta dell’unione tra *A* e *B*, bisogna sottrarre alla somma tra le cardinalità di *A* e di *B* la cardinalità della loro intersezione, ossia dell'insieme delle targhe che non contengono né una T né un 9, che corrisponde a:
$$A ∩ B = 25^2 × 9^3 × 25^2$$
Dunque, il complemento che stiamo contando ha un numero di elementi pari a:
$$(25^2 × 10^3 × 25^2) + (26^2 × 9^3 × 26^2) − (25^2 × 9^3 × 25^2)$$
e la soluzione dell’esercizio si ottiene sottraendo questa quantità dal numero totale di targhe.
___
Precedentemente, è stato esplicitato il principio di inclusione-esclusione a due termini, che rappresenta ovviamente il caso più basilare di applicazione di tale principio. Consideriamo, adesso, un caso in cui i dati sono divisi in 3 tipi, ad esempio una classe di studenti sottoposti a tre test di valutazione: Combinatoria (*C*), Induzione (*I*) e Logica (*L*). I risultati dei test sono i seguenti:
- 12 studenti superano I;
- 5 studenti superano L;
- 8 studenti superano C;
- 2 studenti superano sia I che L;
- 6 studenti superano sia I che C;
- 3 studenti superano sia L che C;
- 1 studente supera sia I che L che C.

Si osserva che, come sopra, i dati vanno di norma interpretati così: il numero degli studenti che supera I conta quelli che superano solo I, quelli che superano I e anche L, quelli che superano I e anche C, e quelli che superano tutti e tre i test; si possono fare dei ragionamenti analoghi anche per gli altri test. Volendo sapere quanti studenti hanno superato almeno un test, possiamo cominciare dalla seguente partizione:
- tipo *I*, ossia gli studenti che superano Induzione;
- tipo *L*, ossia gli studenti che superano Logica;
- tipo *C*, ossia gli studenti che superano Combinatoria.

Possiamo vedere il problema, anche in questo caso, come un problema di unione: denotiamo, quindi, con (*I ∪ L ∪ C*) l’insieme degli studenti che sono in *I* o in *C* o in *L*. Considerando la somma delle cardinalità dei tre tipi, si nota che si stanno contando due volte gli studenti che superano almeno due esami: infatti, ragionando per coppie di tipi, in *I* si contano quelli che superano solo *I* e anche quelli che superano *I* e *L*, mentre in *L* si contano quelli che superano
solo *L* ma anche quelli che superano *I* e *L*, e bisogna dunque sottrarre una volta quest'ultima quantità; inoltre, accade la stessa cosa se consideriamo gli studenti che superano *L* e *C*, che sono contati una volta in *L* e una in *C*; e si procede analogamente per gli studenti che superano *I* e *C*, contati una volta in *I* e una volta in *C*. Si ottiene, così, che andranno sottratte le quantità *#(I ∩ L)*, *#(I ∩ C)* e *#(L ∩ C)*.

Tuttavia, il risultato va ancora aggiustato: in ciascuno dei primi tre addendi abbiamo infatti contato una volta gli studenti che superano tutti e tre i test, ma questi ultimi sono stati anche sottratti in ciascuno dei tre sottraendi. Ad esempio, in *#(I ∩ C)* contiamo gli studenti che superano solo *I* e *C* ma anche quelli superano tutti e tre i test, e la stessa cosa vale per *#(I ∩ L)* e per *#(L ∩ C)*. Risulta, quindi, che andrà aggiunta la quantità *#(I ∩ C ∩ L)*. Otteniamo così che:
$$(I ∪ L ∪ C) = I + L + C − (I ∩ L) − (I ∩ C) − (L ∩ C) + (I ∩ C ∩ L)$$
Generalizzando tale ragionamento, otteniamo la formula del **principio di inclusione-esclusione a tre termini**:
$$(A ∪ B ∪ C) = A + B + C − (A ∩ B) − (A ∩ C) − (B ∩ C) + (A ∩ B ∩ C)$$
___
Seguendo ragionamenti analoghi a quelli precedenti, è possibile arrivare a una formulazione generica del principio di inclusione-esclusione, valida per qualsiasi numero *n* di termini. Si nota, infatti, analizzando i casi precedenti, che per ottenere la cardinalità dell'unione tra un numero di insiemi si devono:
1. sommare le cardinalità dei singoli;
2. sottrarre le cardinalità delle intersezioni a due a due;
3. sommare le cardinalità delle intersezioni a tre a tre;
4. sottrarre le cardinalità delle intersezioni a quattro a quattro;
5. ...

Tale procedimento può essere rappresentato matematicamente con la seguente formula:

![[pie_n_elementi.png]]

in cui la prima sommatoria indica la somma delle cardinalità dei singoli, la seconda indica la somma di tutte le possibili intersezioni a due elementi (si legge come "la somma per ogni scelta di *i₁* e *i₂* che variano tra 1 e *n* tali per cui *i₁* < *i₂* delle intersezioni tra *Ai₁* e *Ai₂*"), e così via. Il termine *(−1)ⁱ⁻¹* non è che un
"trucchetto" per scrivere uniformemente il segno dell’ultimo termine della formula, che è un meno se *n* è pari e un più se *n* è dispari.