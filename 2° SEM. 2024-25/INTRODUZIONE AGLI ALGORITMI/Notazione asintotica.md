Per poter valutare l’efficienza di un algoritmo, così da confrontarlo con altri che risolvono lo stesso problema, bisogna essere in grado di valutarne il **costo computazionale**, ovvero il suo tempo di esecuzione e le sue necessità in termini di memoria (salvo ove diversamente specificato, la grandezza che verrà valutata maggiormente nel corso è il tempo di esecuzione dell’algoritmo). 

In generale, questa valutazione è complicata e contiene spesso dettagli trascurabili, per cui ci piacerebbe limitarci a dare una visione più astratta, e valutare solo quello che informalmente possiamo chiamare “**tasso di crescita**”, cioè la velocità con cui il tempo di esecuzione cresce all’aumentare della dimensione dell’*input*. Poiché per piccole dimensioni dell’*input* il tempo usato è comunque poco, tale valutazione è più interessante quando la dimensione dell’*input* è sufficientemente grande, per questo si parla di "**efficienza asintotica**" degli algoritmi.

Inoltre, siccome la velocità dello specifico calcolatore usato influisce solo per una costante moltiplicativa, vogliamo descrivere un modello che riesca a prescindere da essa. Infine, essendo il tempo di esecuzione una quantità necessariamente positiva, assumeremo in generale che tutte le funzioni coinvolte siano asintoticamente non negative.

Ci sono varie forme di notazione asintotica, principalmente tre:
- la **notazione *O***, o "limite asintotico superiore";
- la **notazione *Ω***, o "limite asintotico inferiore";
- la **notazione *θ***, o "limite asintotico stretto".
___
Partiamo dalla **notazione *O***. Date due funzioni *f(n)* e *g(n)*, entrambe positive, si dice che "***f(n)* è un *O(g(n))***" se esistono due costanti *c* e *n₀* tali che, per ogni *n ≥ n₀*, vale che:
$$0 ≤ f(n) ≤ c g(n)$$
Graficamente, deve valere ciò:

![[notazioneO.png]]

Ad esempio, avendo *f(n) = 3n + 3*, si può affermare che *f(n) = O(n²)*, in quanto esistono *c* (ad esempio *c* = 6) e *n₀* (ad esempio *n₀ = 1*) tali che venga rispettata la condizione stabilita in precedenza (infatti, *6n² ≥ 3n + 3* per ogni *n ≥ 1*). Tra l'altro, per gli stessi valori, possiamo affermare anche che *f(n) = O(n)* per la stessa coppia di valori. È facile convincersi che, data una funzione *f(n)*, esistono infinite funzioni *g(n)* per cui *f(n)* risulta un *O(g(n))*.
___
Parliamo, ora, della **notazione *Ω***. Date due funzioni *f(n)* e *g(n)*, entrambe positive, si dice che "***f(n)* è un *Ω(g(n))***" se esistono due costanti *c* e *n₀* tali che, per ogni *n ≥ n₀*, vale che:
$$f(n) ≥ c g(n)$$
Graficamente, deve valere ciò:

![[notazioneΩ.png]]

Ad esempio, avendo *f(n) = 2n² + 3*, si può affermare che *f(n) = Ω(n)*, in quanto esistono *c* (ad esempio *c = 1*) e *n₀* (in questo caso, qualunque valore) tali che venga rispettata la condizione stabilita in precedenza (infatti, *2n² + 3 ≥ n* per ogni *n ∈ R*). Tra l'altro, per *c ≤ 2* e per ogni *n ∈ R*, possiamo affermare anche che *f(n) = Ω(n²)*.

In entrambe le notazioni esposte finora, per ogni funzione *f(n)* è possibile trovare più funzioni *g(n)*; in effetti, *O(g(n))* e *Ω(g(n))* sono insiemi di funzioni, e dire ”*f(n)* è un *O(g(n))*” oppure ”*f(n) = O(g(n))*” ha il significato di ”*f(n) ∈ O(g(n))*”. Tuttavia, poiché i limiti asintotici ci servono per stimare con la maggior precisione possibile il costo computazionale di un algoritmo, vorremmo trovare la funzione *g(n)* che più si avvicina a *f(n)*. Perciò cerchiamo **la più piccola funzione *g(n)* per determinare O e la più grande funzione *g(n)* per determinare *Ω***. La definizione che segue formalizza questo concetto intuitivo.
___
Date due funzioni *f(n)* e *g(n)*, entrambe positive, si dice che "***f(n)* è un *θ(g(n))***" se esistono tre costanti *c₁*, *c₂* e *n₀* tali che, per ogni *n ≥ n₀*, vale che:
$$c_1g(n) ≤ f(n) ≤ c_2g(n)$$
In altre parole, *f(n) = θ(g(n))* se è contemporaneamente *O(g(n))* e *Ω(g(n))*. Graficamente, deve valere ciò:

![[notazioneθ.png]]

Ad esempio, avendo *f(n) = 3n + 3*, si può affermare che *f(n) = θ(n)*, in quanto esistono *c₁* (ad esempio, *c₁ = 3*), *c₂* (ad esempio, *c₂ = 4*) e *n₀* (ad esempio, *n₀ = 3*) tali che venga rispettata la condizione stabilita in precedenza (infatti, *3n ≤ 3n + 3 ≤ 4n* per ogni *n ≥ 3*).
___
Per semplificare il calcolo del costo computazionale asintotico degli algoritmi, si possono sfruttare delle semplici regole di **algebra sulla notazione asintotica**.

Vediamo, innanzitutto, delle proprietà relative alle **costanti moltiplicative**:
- per ogni *k > 0* e per ogni *f(n) ≥ 0*, se *f(n)* è un *O(g(n))*, allora anche *k ∙ f(n)* è un *O(g(n))*;
- per ogni *k > 0* e per ogni *f(n) ≥ 0*, se *f(n)* è un *Ω(g(n))*, allora anche *k ∙ f(n)* è un *Ω(g(n))*;
- per ogni *k > 0* e per ogni *f(n) ≥ 0*, se *f(n)* è un *θ(g(n))*, allora anche *k ∙ f(n)* è un *θ(g(n))*.

Informalmente, queste tre regole si possono riassumere tenendo a mente che **le costanti moltiplicative sono trascurabili nel calcolo delle notazioni asintotiche**. Questa regola generale, tuttavia, vale sempre tranne quando tali costanti moltiplicative si trovano negli esponenti.

Passiamo, ora, a delle proprietà relative alla **commutatività della somma**:
- per ogni *f(n), d(n) > 0*, se *f(n)* è un *O(g(n))* e *d(n)* è un *O(h(n))*, allora *f(n) + d(n)* è un *O(g(n) + h(n))* = O(max(g(n),h(n)));
- per ogni *f(n), d(n) > 0*, se *f(n)* è un *Ω(g(n))* e *d(n)* è un *Ω(h(n))*, allora *f(n) + d(n)* è un *Ω(g(n) + h(n))* = Ω(max(g(n),h(n)));
- per ogni *f(n), d(n) > 0*, se *f(n)* è un *θ(g(n))* e *d(n*) è un *θ(h(n))*, allora *f(n) + d(n)* è un *θ(g(n) + h(n))* = θ(max(g(n),h(n))).

Informalmente, queste tre regole si possono riassumere tenendo a mente che **le notazioni asintotiche commutano con l’operazione della somma**.

Infine, analizziamo le proprietà relative alla **commutatività del prodotto**:
- per ogni *f(n), d(n) > 0*, se *f(n)* è un *O(g(n))* e *d(n)* è un *O(h(n))*, allora *f(n)d(n)* è un *O(g(n)h(n))*;
- per ogni *f(n), d(n) > 0*, se *f(n)* è un *Ω(g(n))* e *d(n)* è un *Ω(h(n))*, allora *f(n)d(n)* è un *Ω(g(n)h(n))*;
- per ogni *f(n), d(n) > 0*, se *f(n)* è un *θ(g(n))* e *d(n*) è un *θ(h(n))*, allora *f(n)d(n)* è un *θ(g(n)h(n))*.

Informalmente, queste tre regole si possono riformulare dicendo che **le notazioni asintotiche commutano con l’operazione del prodotto**.



