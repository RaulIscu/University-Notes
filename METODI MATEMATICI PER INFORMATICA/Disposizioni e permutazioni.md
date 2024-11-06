Analizziamo un esempio: supponiamo di avere 8 atleti che corrono in una gara, e di voler sapere quanti podii diversi si possono ottenere da quest'ultima. A logica, diremo che al primo posto potremo avere 8 diversi atleti, per ognuno di questi poi si potranno avere 7 atleti al secondo posto (in quanto uno degli 8 atleti è già giunto all'arrivo), e ancora per ognuno di questi 6 atleti diversi potranno occupare il terzo posto. I possibili podii sono dunque:

> *8 ∙ 7 ∙ 6 = 336*

Generalizzando, applicando il principio moltiplicativo, se si considera l'insieme A = {*a1*, *a2*, ..., *an*}, formato da *n* elementi, il numero di sequenze ordinate di lunghezza *k* di elementi di A senza ripetizioni (dette anche **disposizioni semplici di ordine *k* di *n* elementi**) è dato da:

![[disp_senza_rip.png]]

Nel caso in cui *n = k*, il problema diventa trovare il numero di modi per riordinare gli *n* elementi considerati in una sequenza; si tratta, dunque, di una **permutazione**, la cui soluzione si ottiene come:
![[perm.png]]
Considerando lo stesso insieme A, il numero di sequenze ordinate di lunghezza k di elementi di A con possibili ripetizioni (dette anche **disposizioni con ripetizioni di ordine k di n elementi**) è invece dato da:

![[disp_con_rip.jpg]]
