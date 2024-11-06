Consideriamo il seguente quesito, simile all'esempio trattato parlando del [[Principio additivo]]: 
> quante targhe automobilistiche contengono almeno una P?

Potremmo provare a procedere usando proprio il principio additivo. Consideriamo, quindi, i seguenti tipi, a seconda della posizione di una P nella targa:
1. Categoria n°1, o *A*, ossia le targhe con P in prima posizione;
2. Categoria n°2, o *B*, ossia le targhe con P in seconda posizione;
3. Categoria n°3, o *C*, ossia le targhe con P in terza posizione;
4. Categoria n°4, o *D*, ossia le targhe con P in quarta posizione.

Bisogna, però, chiedersi: questa tipizzazione rispetta i vincoli di applicabilità del principio additivo? Prima di tutto chiariamo meglio i tipi. A una prima lettura potremmo interpretare la categorizzazione come le targhe con una sola P e quella P in posizione 1, 2, 3 o 4. In realtà, tuttavia, si intendono le targhe con una P in 1, 2, 3, o 4 posizione ma non escludiamo che vi siano altre P. Si vede facilmente che i tipi sono esaustivi, ma non sono esclusivi: dunque, risulta difficile (se non impossibile), applicare il principio additivo in questo caso.

Una soluzione alternativa potrebbe essere contare la quantità desiderata contando quante targhe non soddisfano il vincolo, e sottraendo il loro numero dal totale delle targhe possibili. In questo caso, il vincolo è: contenere almeno una P; dunque, le targhe che non lo soddisfano sono quelle che non contengono nessuna P. Il loro numero si conta facilmente con il principio moltiplicativo: 
$$25^2 × 10^3 × 25^2$$
Il totale delle targhe è anch'esso facilmente calcolabile: 
$$26^2 ×10^3 ×26^2$$
Dunque il risultato richiesto diventa:
$$(26^2 × 10^3 × 26^2) − (25^2 × 10^3 × 25^2)$$
La soluzione trovata in questo modo viene detta soluzione per **passaggio al complemento**. Si può osservare che altro non è che un caso particolare del principio additivo. Equivale infatti a dividere tutte le targhe possibili (insieme *A*) in due tipi: quelle che soddisfano il vincolo (chiamiamolo insieme *V*) e quelle che non lo soddisfano (chiamiamolo insieme *non V*). Si vede facilmente che abbiamo così definito una partizione in 2 parti di A. Dunque per il principio additivo:

> ***A = V + non V***  →  ***V = A - non V***

In termini insiemistici l’insieme che abbiamo chiamato *non V* viene detto il "**complemento di *V***" in *A* e viene denotato con ***A\V*** (l’insieme degli elementi di *A* che non appartengono a *V*). La sua definizione ufficiale è la seguente: se *V* ⊆ *A*, il complemento di *V* in *A* è *A\V* = {a | a ∈ A, a ∉ V }. Ogni sottoinsieme *V* di un insieme *A* determina una partizione di *A* in due parti: *V* stesso e il suo complemento *A\V*.