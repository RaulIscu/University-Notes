Data una funzione *f: I → O*, in alcune situazioni siamo interessati a risalire da un elemento del codominio *O* a un elemento del dominio di cui esso è immagine. Se *x ∈ I* e *y ∈ O* sono tali che *f(x) = y*, abbiamo che *y* è immagine di *x*, e *x* pre-immagine di *y*. In generale, un elemento del codominio non ha necessariamente un'unica pre-immagine, anzi: possono esistere elementi del codominio senza alcuna pre-immagine, ma anche elementi del codominio con più di una pre-immagine.

La nozione di **funzione inversa** è piuttosto naturale nella pratica matematica; in generale, abbiamo la seguente definizione.
> Sia *f: X → Y* una funzione. Una funzione *g: Y → X* si dice l’inversa di *f* se e solo se *(g ◦ f)* è l’identità su *X*, e *(f ◦ g)* è l’identità su *Y*.

La funzione inversa di *f(x)* si denota con:
$$f(x)^-¹$$
Sappiamo già che l’esistenza di una *g* come nella definizione qui sopra equivale alla biettività di *f*; dunque una tale *g* non esiste per *f* arbitrarie. Una funzione *f: X → Y* è **invertibile** se esiste la funzione inversa.