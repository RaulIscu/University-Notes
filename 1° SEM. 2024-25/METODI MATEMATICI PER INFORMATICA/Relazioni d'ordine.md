Una "**relazione d’ordine**" è una relazione che gode di alcune proprietà fondamentali della relazione di ordine numerico sui naturali. Consideriamo, ad esempio, la relazione di ordine numerico "*≤*" su *N*: ovviamente, gode delle seguenti proprietà:
1. per ogni *n* ∈ *N*, *n* ≤ *n*;
2. per ogni *n, m* ∈ *N*, se *n ≤ m* e *m ≤ n* allora *m = n*;
3. per ogni *n, m, q* ∈ *N*, se *n* ≤ *m* e *m* ≤ *q* allora *n* ≤ *q*;
4. per ogni *n, m* ∈ *N*, o *n ≤ m* oppure *m ≤ n*.

La definizione di **relazione d’ordine totale** è modellata esattamente su queste quattro proprietà. Quindi, una relazione *R* su un insieme *A* è una relazione d'ordine totale se e solo se gode delle seguenti proprietà:
1. per ogni *a* ∈ *A*, vale *aRa*;
2. per ogni *a, b* ∈ *A*, se *aRb* e *bRa* allora *a = b*;
3. per ogni *a, b, c* ∈ *A*, se *aRb* e *bRc* allora *aRc*;
4. per ogni *a, b* ∈ *A* vale *a ≤ b* oppure *b ≤ a*.

Insomma, una relazione *R* ⊆ *A × A* è una relazione di ordine totale (o "ordine lineare") se e solo se è riflessiva (punto 1), antisimmetrica (punto 2), transitiva (punto 3) e totale (punto 4). La nozione generalizza l’idea fondamentale di un **ordine lineare**, ossia i cui elementi possono essere disegnati su una linea in ordine di precedenza, e siano tutti confrontabili tra loro.

La definizione di "**relazione d'ordine parziale**", invece, gode di tutte le proprietà di quella di ordine totale tranne per l'ultima, ossia proprio la totalità. Dunque, una relazione *R* ⊆ *A × A* che gode delle proprietà di riflessività, antisimmetria e transitività viene detta "**ordine parziale**" su *A*.

Siamo soliti, in realtà, usare relazioni che permettono di stabilire un ordine di precedenza tra elementi ma che non soddisfano la proprietà di totalità. Consideriamo, per esempio, l’inclusione insiemistica "⊆": essa è riflessiva (per ogni insieme *X*, *X* ⊆ *X*), antisimmetrica (per ogni coppia di insiemi *X* e *Y*, se *X* ⊆ *Y* e *Y* ⊆ *X* allora *X = Y*) e transitiva (per ogni tripla di insiemi *X*, *Y* e *Z*, se *X* ⊆ *Y* e *Y* ⊆ *Z* allora *X* ⊆ *Z*); non è, però, totale, in quanto non è vero che, presi due insiemi arbitrari *X* e *Y*, valga sempre *X* ⊆ *Y* oppure *Y* ⊆ *X*. Dunque, la relazione di inclusione insiemistica non è un ordine totale sugli insiemi, ma piuttosto un ordine parziale.
___
Gli ordini totali permettono di confrontare gli elementi di un insieme finito in modo del tutto lineare, partendo dal minimo e procedendo seguendo l’ordine.; questo risulta comodo anche dal punto di vista informatico o algoritmico. Gli ordini parziali, invece, sono più complicati perché rendono necessario seguire i diversi “percorsi” ramificati che collegano i punti. Risulta, dunque, interessante osservare che è sempre possibile **estendere un ordine parziale a un ordine totale** sullo stesso insieme.

Sia A = {*a₁*, *a₂*, ..., *an*} un insieme finito ordinato da una relazione *R* di ordine parziale: allora, esiste una relazione *R∗* ⊆ *A × A* che è un ordine totale ed estende *R*, ossia per ogni *a, b* ∈ *A*, se *aRb* allora *aR∗b*.

Per dimostrare questo teorema, sarà sufficiente dimostrare che, sia *R* ⊆ *A × A* una relazione di ordine parziale, e siano *a, b* ∈ *A* due elementi incomparabili
relativamente a *R* (ossia tali che *(a, b)* ∉ *R* e *(b, a)* ∉ *R*), esiste una relazione *R′* ⊆ *A × A* tale che:
1. *R* ⊆ *R′*;
2. *(a, b)* ∈ *R′*.

[DIMOSTRAZIONE: FINE DISPENSA 13]