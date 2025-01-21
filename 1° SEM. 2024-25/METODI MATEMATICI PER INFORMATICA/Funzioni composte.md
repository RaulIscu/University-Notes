Comporre funzioni significa applicarle in sequenza; per esempio, comporre la funzione n → n + 1 alla funzione n → n² significa n → n + 1 → (n + 1)². Affinché questo sia possibile deve valere che l’*output* della prima funzione rientri tra i possibili argomenti della seconda (e dunque, che sia parte del dominio della seconda).
> Siano *f: X → Y* e *g: Y → Z* due funzioni; la funzione composta di *f* e *g* è la funzione *h: X → Z* definita ponendo:
> $$∀x ∈ X, h(x) = g(f(x))$$

La funzione composta considerata si denota anche con:
$$g ◦ f$$
In termini più espliciti, usando la definizione insiemistica di funzione, possiamo dare la seguente definizione equivalente.
> Siano *f: X → Y* e *g: Y → Z* due funzioni; si indica con *g ◦ f* l’insieme di tutte e sole le coppie ordinate *(x, z) ∈ X × Z* tali che ∃y ∈ Y tale per cui *(x, y) ∈ f* e *(y, z) ∈ g*.

Si noti che la definizione sopra è ben posta: ogni elemento di *X* ha un'immagine via *g ◦ f* perché ogni elemento di *X* ha un'immagine in *Y* via *f: X → Y* e ogni elemento di *Y* ha una immagine in *Z* via *g: Y → Z*.
___
Qui sopra abbiamo considerato le funzioni *s: N → N* definita come *s(n) = n + 1* e la funzione *q: N → N* definita come *q(n) = n²* e abbiamo descritto la loro composizione come la funzione risultante dall’applicazione prima di *s* e poi di *q*. Questa funzione si comporta così:
$$n → (n + 1)^2$$
Da questo esempio si vede facilmente che nelle composizioni l’ordine conta: se infatti componiamo *s* e *q* applicando prima *q* e poi *s* otteniamo una funzione diversa, che si comporta così:
$$n → n^2 + 1$$
In generale, **la composizione di funzioni** (laddove è definita) **non è commutativa in generale**.
___
Vediamo le proprietà di **iniettività**, **suriettività** e **biettività** in relazione alle composizioni di funzioni; siano *f: X → Y* e *g: Y → Z* due funzioni:
1. se *f* e *g* sono iniettive allora *g ◦ f* è iniettiva;
2. se *f* e *g* sono suriettive allora *g ◦ f* è suriettiva;
3. se *f* e *g* sono biettive allora *g ◦ f* è biettiva.

Dimostriamo il primo punto. Supponiamo che *f* e *g* siano entrambe iniettive; dobbiamo dimostrare che la composizione *g ◦ f* è iniettiva, e dunque che non esistono due elementi distinti del dominio *X* che hanno come immagine lo stesso elemento del codominio *Z*. Ragioniamo per assurdo: supponiamo che esista un elemento del codominio *z ∈ Z* tale che esistono due elementi del dominio *x*, *x'* *∈ X*, con *x ≠ x'*, che vengono entrambi mappati in *z* dalla funzione composta *g ◦ f*. Questo significa che:
$$(g ◦ f)(x) = (g ◦ f)(x')$$
che per definizione significa che:
$$g(f(x)) = g(f(x'))$$
Dato che *g* è iniettiva per ipotesi, se *g* mappa gli elementi f(x) e f(x′) del suo dominio *Y* nello stesso elemento del codominio *Z*, deve essere necessariamente *f(x) = f(x′)*. Dato che *f* è iniettiva per ipotesi, se *f* mappa gli elementi *x* e *x'* del suo dominio *X* nello stesso elemento del codominio *Y*, deve essere necessariamente *x = x'*. Ma questo contraddice l’ipotesi che *x* e *x'* siano distinti. Abbiamo così raggiunto una contraddizione, e dunque si è dimostrato che *g ◦ f* è iniettiva.

Dimostriamo il secondo punto, e quindi che ogni elemento del codominio *Z* è immagine via *g ◦ f* di almeno un elemento del dominio *X*. Scegliamo un arbitrario *z ∈ Z*. Dato che *g: Y → Z* è suriettiva per ipotesi, *∃y ∈ Y* tale che *g(y) = z*; sia *y₀* un tale *y*. Dato che *f: X → Y* è suriettiva per ipotesi, *∃x ∈ X* tale che *f(g(y₀)) = z*; sia *x₀* un tale *x*. Abbiamo dunque dimostrato che *∃x ∈ X* tale che *g(f(x)) = z*.

Il terzo punto viene immediatamente dimostrato a seguito delle prime due dimostrazioni.
___
