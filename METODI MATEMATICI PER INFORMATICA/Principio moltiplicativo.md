Il **principio moltiplicativo** risulta utile nel contare in quanti modi possibili si può scegliere un elemento per categoria avendo *n* categorie di elementi. 

Ad esempio, supponiamo di doverci vestire e di dover scegliere uno tra 3 pantaloni, una tra 2 magliette e un paio tra 3 paia di scarpe. In questo contesto, abbiamo quindi 3 scelte di pantaloni, e per ognuna di queste 2 scelte di magliette, e ancora per ognuna di queste 3 scelte di scarpe. Il numero totale di combinazioni possibili sarà:

> *3 ∙ 2 ∙ 3 = 18*

Generalizzando, se si deve scegliere un numero *n* di elementi, avendo *a1* scelte per il primo, *a2* scelte per il secondo, e così via fino ad avere *an* scelte, si ottiene che le possibili combinazioni sono:

![[panini.png]]

Analizziamo, ora, un esempio diverso: supponiamo di avere 8 atleti che corrono in una gara, e di voler sapere quanti podii diversi si possono ottenere da quest'ultima. A logica, diremo che al primo posto potremo avere 8 diversi atleti, per ognuno di questi poi si potranno avere 7 atleti al secondo posto (in quanto uno degli 8 atleti è già giunto all'arrivo), e ancora per ognuno di questi 6 atleti diversi potranno occupare il terzo posto. I possibili podii sono dunque:

> *8 ∙ 7 ∙ 6 = 336*

Generalizzando, se si considera l'insieme A = {*a1*, *a2*, ..., *an*}, formato da *n* elementi, il numero di sequenze ordinate di lunghezza *k* di elementi di A senza ripetizioni (dette anche **disposizioni semplici di ordine *k* di *n* elementi**) è dato da:

  ![[disp_senza_rip.png]]
Considerando lo stesso insieme A, il numero di sequenze ordinate di lunghezza k di elementi di A con possibili ripetizioni (dette anche **disposizioni con ripetizioni di ordine k di n elementi**) è invece dato da:

![[disp_con_rip.jpg]]

Nel caso in cui *n = k*, il problema diventa trovare il numero di modi per riordinare gli *n* elementi considerati in una sequenza; si tratta, dunque, di una **permutazione**, la cui soluzione si ottiene come:
![[perm.png]]