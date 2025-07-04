La **chiusura transitiva** è un'operazione che permette di "estendere" una relazione non-transitiva in modo da renderla transitiva. Se si vuole operare una chiusura transitiva, bisogna sempre trovare l'estensione più piccola possibile della relazione di partenza: per comprendere meglio tale concetto, vediamo un esempio.

Supponiamo di avere una relazione *R₁*, rappresentata nel seguente grafo con delle frecce bianche:

![[chiusuratrans_esempio.png]]

Si nota immediatamente che *R₁* non è transitiva: per esempio, valgono *aR₁b* e *bR₁c* ma non vale *aR₁c*; analogamente, valgono *bR₁c* e *cR₁e* ma non vale *bR₁e*. La relazione *R₂*, rappresentata nel grafo dalle frecce bianche e azzurre, è ottenuta cercando di rimediare ai due controesempi appena indicati, ma neanche questa relazione è transitiva: valgono, infatti, *aR₂c* e *cR₂e*, ma non ci sono frecce da *a* a *e*, e dunque non vale *aR₂e*. La relazione *R₃*, rappresentata dalla totalità delle frecce del grafo e ottenuta rimediando al controesempio portato per la relazione *R₂*, è finalmente transitiva.

Con *R₃*, dunque, abbiamo ottenuta un'**estensione** transitiva della relazione iniziale, nel senso che *R₁* ⊆ *R₃*. La relazione *R₃* è inoltre la più piccola relazione transitiva che estende *R₁* (in questi casi, con "più piccola" si può intendere sostanzialmente "ottenuta aggiungendo a *R₁* il minor numero di frecce"). Procediamo a definire generalmente l'operazione di chiusura transitiva:

>Si definisce "chiusura transitiva" di *R* la più piccola relazione transitiva che estende *R*, ossia la relazione *RT* tale per cui:
>  1. *R* ⊆ *RT*;
>  2. *RT* è transitiva;
>  3. se *S* estende *R* ed è transitiva allora *RT* ⊆ *S*.

Se escludiamo anche solo una coppia dalla chiusura transitiva *RT* di una relazione *R*, necessariamente violiamo o il fatto che la relazione estende *R* o il fatto che sia transitiva.

Nel caso di una relazione *R* su un insieme *A* finito, possiamo intendere “la più piccola” nel senso di "quella contenente il minor numero di coppie", ma questo
perde di senso se *A* è infinito. Il terzo punto della definizione rimedia proprio a questo problema, offrendo una definizione di “minima” o “più piccola” in termini di inclusione insiemistica, che vale sia per il caso finito che per il caso infinito. Questa condizione viene espressa richiedendo che ogni relazione che soddisfa le prime due condizioni (ossia estende *R* ed è transitiva) contenga la chiusura transitiva.
___
Vediamo un altro esempio: consideriamo *R* = {*(1, 2), (2, 3), (3, 4)*} sull'insieme *A* = {*1, 2, 3, 4*}. Dato che *(1, 2)* ∈ *R* e *(2, 3)* ∈ *R*, occorre aggiungere la coppia *(1, 3)*; inoltre, dato che *(2, 3)* ∈ *R* e *(3, 4)* ∈ *R*, occorre aggiungere la coppia *(2, 4)*. Si può chiamare *R⁺* la nuova relazione ottenuta, ma si nota che quest'ultima non è ancora transitiva: infatti, *(1, 3)* ∈ *R⁺* e *(3, 4)* ∈ *R⁺*, ma *(1, 4)* ∉ *R⁺*. Arriviamo, quindi, alla relazione *R⁺⁺*, che include le stesse coppie di *R⁺* ma anche *(1, 4)*, e si ottiene in questo modo una relazione transitiva, per tutti i possibili casi in cui si verifica la pre-condizione della definizione di transitività è vera anche la conclusione.

Ripercorrendo quanto appena fatto, osserviamo che *R⁺* = *R* ∪ *(R ◦ R)*: infatti, per definizione, *R ◦ R* contiene tutte e sole le coppie *(a, c)* tali per cui esiste un *b* ∈ *A* tale che *(a, b)* ∈ *R* e *(b, c)* ∈ *R*. Analogamente, *R⁺⁺* = *R* ∪ *(R ◦ R)* ∪ *((R ◦ R) ◦ R)*: infatti, per definizione, infatti, *(x, y)* ∈ *(R ◦ R) ◦ R* se e solo se esiste *z* ∈ *A* tale che *(x, z)* ∈ *(R ◦ R)* e *(z, y)* ∈ *R*. In base all’esempio precedente, la chiusura transitiva di una relazione *R* si può ottenere estendendo *R* con le relazioni ottenute componendo *R* con se stessa. Denotiamo con *Rⁱ* la composta di *R* con sé stessa *i* volte (che possiamo chiamare "potenza di *R*"), ossia R ◦ R ◦ ... ◦ R (dove le parentesi sono omesse perché la composizione è associativa); il procedimento dell’esempio precedente ci suggerisce di definire la seguente successione di relazioni:
$$R_1 = R$$
$$R_2 = R ∪ (R ◦ R) = R_1 ∪ R^2$$
$$R_3 = R_2 ∪ (R ◦ R) ◦ R = R_2 ∪ R^2 ◦ R = R_2 ∪ R^3$$
La generica relazione *(i + 1)*-esima è dunque definita come:
$$R_i₊₁ = R_i ∪ R^i⁺¹$$
Consideriamo l’unione di tutte le *Ri* (o, equivalentemente, di tutte le *Rⁱ*), ponendo:

![[composizione_n-esima_r.png]]

*R∞* altro non è che l’unione infinita di *R* con tutte le sue potenze. Si ricorda che, per definizione di unione, una coppia *(x, y)* appartiene all’unione infinita *R∞*
se e solo se esiste un *n* ∈ *N* tale che *(x, y)* ∈ *Rn* (ossia se e solo se appartiene a uno dei termini dell’unione). Si può dimostrare che *R∞* così definita è la chiusura transitiva di *R*, ossia la più piccola relazione transitiva che estende *R*.
___
> Sia *R* una relazione su *A*, e siano *a, b* ∈ *A*. Con *l* ≥ *1*, diciamo che esiste un **percorso** di lunghezza *l* da *a* verso *b* se esistono elementi x₁, x₂, ..., x*l*₋₁ in *A* tali per cui vale:
> $$aRx₁Rx₂R...Rx_l₋₁Rb$$

Questo concetto è molto utile nel contesto della chiusura transitiva. Analizziamo un esempio: data una mappa di strade a senso unico che collegano città (avendo, dunque, una relazione *aRb* se e solo se c’è una strada che parte dalla città *a* e arriva alla città *b*), la chiusura transitiva contiene tutte e sole le coppie di città *(x, y)* tali che esiste un itinerario (o percorso) che porta da *x* a *y*.

Intuitivamente, dato he non abbiamo richiesto che gli elementi menzionati siano distinti, la definizione precedente definisce l’esistenza di un percorso di lunghezza al più *l* tra i punti *a* e *b*. La definizione, inoltre, è predisposta in modo da includere come caso particolare quello di due punti *a* e *b* tali per cui *aRb*: in questo caso, si può correttamente affermare che esiste un percorso di lunghezza 1 da *a* verso *b*, e la condizione "esistono x₁, x₂, ..., x*l*₋₁" è vera a vuoto.

Si osserva che esiste un percorso di lunghezza *i* tra *a* e *b* se e solo se *(a, b)* ∈ *Rⁱ*. Dunque l’unione *R¹* ∪ *R²* ∪ ... ∪ *Rⁱ* contiene tutte e sole le coppie *(a, b)* per cui esiste un percorso di lunghezza ≤ *i* da *a* a *b*.

Una dimostrazione rigorosa dell’osservazione precedente si può ottenere per induzione matematica, dimostrando che l’equivalenza è vera per ogni possibile *l* ∈ {1, 2, 3, ...}. Limitiamoci a qualche osservazione:
- per *l* = 1 stiamo dicendo che *R₁* (ossia *R*) contiene tutte e sole le coppie *(a, b)* ∈ *A × A* per cui esiste un percorso di lunghezza 1 da *a* verso *b*. Queste sono tutte le coppie *(a, b)* ∈ *R*, dunque l’identità è verificata.
- per *l* = 2 stiamo dicendo che *R₂* contiene tutte e sole le coppie in *R ◦ R*, ossia le coppie *(x, y)* tali per cui esiste *z* ∈ *A* tale che valgano *xRz* e *zRy*. Dunque esiste un percorso di lunghezza 2 da *x* verso *y*: *xRzRy*. Viceversa se esiste un percorso di lunghezza 2 da *x* verso *y* allora la coppia *(x, y)* è in *R ◦ R* (per definizione di composizione).
- per *l* = 3 stiamo dicendo che *R₃* contiene tutte e sole le coppie in *(R ◦ R) ◦ R*, ossia le coppie *(x, y)* tali per cui esiste *z* ∈ *A* tale che *(x, z)* ∈ *R ◦ R* e *(z, y)* ∈ *R*. Per quanto visto sopra, *(x, z)* ∈ *R ◦ R* equivale all’esistenza di un percorso di lunghezza 2 da *x* verso *z*, e *(z, y)* ∈ *R* equivale all’esistenza di un percorso di lunghezza 1 da *z* verso *y*: dunque, esiste un percorso di lunghezza 3 da *x* verso *z*.

Si ottiene, dunque, che *R∞* coincide con l’insieme delle coppie *(a, b)* per cui, per qualche *l*, esiste un percorso di lunghezza *l* tra *a* e *b*. Quest'identità è molto utile, perché in molti casi è più semplice e intuitivo ragionare in termini di percorsi che non in termini di iterazione della composizione di *R* con se stessa. Per esempio, in termini di percorsi è evidente il concetto di transitività: se esiste un percorso da *a* verso *b* e un percorso da *b* verso *c*, di certo esiste un percorso da *a* verso *c*.
___
Dimostriamo, appoggiandoci alla nozione di percorso, che ***R∞* è la chiusura transitiva di *R***.

Si tratta di dimostrare che *R∞* soddisfa le tre condizioni che definiscono la chiusura transitiva *RT*, ossia:
1. *R∞* estende *R*;
2. *R∞* è transitiva;
3. *R∞* è la più piccola relazione transitiva che estende *R*.

Il punto 1 viene dimostrato immediatamente in quanto *R* = *R₁*, che è necessariamente contenuta in *R∞*.

Per il punto 2, siano *(a, b)* ∈ *R∞* e *(b, c)* ∈ *R∞*: per l’equivalenza tra appartenenza a una composizone *Rⁱ* ed esistenza di un percorso di lunghezza *i*, *(a, b)* ∈ *R∞* equivale a dire che esiste un percorso (di una qualche lunghezza *i*) da *a* verso *b*; analogamente, *(b, c)* ∈ *R∞* equivale a dire che esiste un percorso (di una qualche lunghezza *j*) da *b* verso *c*. Dunque esiste un percorso (di lunghezza *i* + *j*) tra *a* e *c*: si ottiene, così, che *(a, c)* ∈ *R∞*. Abbiamo così dimostrato che *R∞* è transitiva.

Per il punto 3, ci limitiamo a considerazioni intuitive (in quanto una dimostrazione rigorosa richiede l’induzione). Per dimostrare che *R∞* è la più piccola relazione transitiva che estende *R*, si considera una relazione arbitraria *S* ⊆ *A × A* transitiva che estende *R*, e si dimostra che necesariamente deve includere
*R∞*, ossia *R∞* ⊆ *S*. Osserviamo che, dato che *R* ⊆ *S*, tutte le frecce di *R* sono frecce anche di *S*, e dunque se esiste un percorso da *a* verso *b* in *R* quello è anche un percorso da *a* verso *b* in *S*. In termini insiemistici, questo significa che, per ogni *i*, *Rⁱ* ⊆ *Sⁱ*, e questo implica a sua volta che *R∞* ⊆ *S∞*. D’altra parte, è facile convincersi che, dato che *S* è transitiva, comporre *S* con sé stessa non porta fuori da *S*, e dunque vale anche che *S∞* ⊆ *S*. Si ottiene, così, che *R∞* ⊆ *S∞* ⊆ *S*, e dunque che *R∞* ⊆ *S*.
___
Se pensiamo di voler calcolare RT, l’unione infinita delle iterazioni di *R* non è molto conveniente da trovare. Consideriamo, però, cosa accade nel caso di una relazione *R* su un insieme finito.

