Si vuole valutare l'efficienza di un algoritmo in odo tale da poterlo confrontare con algoritmi diversi che risolvono lo stesso problema. Per fare ciò, si valuta il costo computazionale di ciascun algoritmo. 

In matematica la notazione asintotica permette di confrontare il tasso di crescita (ossia il suo "comportametno asintotico") di una funzione nei confronti di un'altra.

[diverse notazioni asintotiche]

Una notazione asisntotica di un algorirtmo ha senso quando la dimensione dell'input è sufficientemente grande, generalmente per n che tende a infinito; per questo si parla di "efficienza asintotica" degli algoritmi.
___
La notazione O ("o-grande")
Date due fuzioni f(n) e g(n) positive, si dice che f(n) è in O(g(n)) se esisotno due costanti c e n0 tali che 0 < f(n) < c x g(n) per ogni n > n0.

Ad esempio, f(n) = 3n + 3. f(n) è in O(n²) in quanto, posto c = 6 si ha che cn² > 3n è 3 per ogni n > 1. Seguendo lo stesso ragionamento, f(n) è anche in O(n). 

[COMPLETA APPUNTI]