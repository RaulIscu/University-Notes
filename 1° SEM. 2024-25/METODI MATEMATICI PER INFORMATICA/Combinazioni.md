Analizziamo un esempio: supponiamo di voler comporre un panino, scegliendo tra:
- pane bianco, pane al sesamo, pane integrale;
- manzo, maiale, pesce; 
- ketchup, senape, maionese, salsa barbecue;
e di volere che tale panino contenga precisamente due salse diverse, senza dare importanza all’ordine in cui vengono inserite. Intuitivamente, è possibile applicare una [[Disposizioni e permutazioni |disposizione semplice]], e il risultato di questo procedimento sarà dunque:
$$4 • 3 = 12$$
Tuttavia, fare ciò terrà in considerazione anche coppie di stessi elementi ma di ordine diverso (ad esempio ketchup-maionese e maionese-ketchup), cosa che non vogliamo. Per eliminare le coppie simmetriche, dunque, occorrerà dividere il risultato per 2:
$$(4 • 3) / 2 = 6$$
Questo ragionamento, in maniera generalizzata, è conosciuto come "**regola del pastore**" (*Per contare le pecore in un gregge, conta le zampe e dividi per 4*). In termini insiemistici il numero delle salse nell’esempio corrisponde al concetto di sottoinsieme di 2 elementi scelti da un insieme di 4; il concetto di insieme formalizza proprio l’idea di una collezione di elementi distinti, non ripetuti e non ordinati.

Consideriamo un nuovo esempio: avendo l’insieme *A = {a, b, c, d}*, si vuole contare quanti sono i sottoinsiemi di 3 elementi. Logicamente, si ottiene in maniera immediata che sono 4: *{a, b, c}*, *{a, b, d}*, *{a, c, d}*, *{b, c, d}*. Ma se volessimo contarli, potremmo di nuovo partire con delle disposizioni semplici di ordine 3:
$$abc, acb, bac, bca, cab, cba$$
$$abd, adb, bad, bda, dab, dba$$
$$adc, acd, dac, dca, cad, cda$$
$$dbc, dcb, bdc, bcd, cdb, cbd$$
Si può osservare che il sottoinsieme *{a, b, c}* corrisponde alle 6 sequenze *abc*, *acb*, *bac*, *cab*, *cba* formate con i suoi elementi, e analogamente per gli altri 3 sottoinsiemi. Dunque ogni sottoinsieme di 3 elementi corrisponde a 6 disposizioni semplici di lunghezza 3. Dato che sappiamo contare queste ultime, possiamo contare i sottoinsiemi, usando la regola del pastore. Nel nostro caso, ogni "pecora" (sottoinsieme di 3 elementi tra 6) ha 6 zampe (disposizioni semplici di lunghezza 3). Si nota che è fondamentale che l’associazione sopra descritta tra sottoinsiemi di 3 elementi e disposizioni
semplici soddisfi le seguenti condizioni: 
1. a ogni sottoinsieme di 3 elementi viene associato lo stesso numero (in questo caso 6) di disposizioni semplici;
2. se due sottoinsiemi di 3 elementi sono distinti allora l’insieme delle disposizioni semplici associate al primo non ha elementi in comune con l’insieme delle disposizioni semplici associato al secondo;
3. l’associazione esaurisce l’insieme delle disposizioni semplici di ordine 3 su 4, ossia ogni disposizione semplice di ordine 3 sui 4 elementi *{a, b, c, d}*.
Queste condizioni ci permettono di contare quante sono le **combinazioni semplici** di ordine 3 su *{a, b, c, d}* se sappiamo contare quante sono le disposizioni semplici di ordine 3: ogni volta che contiamo (o togliamo) un insieme di 3 elementi scelti in *{a, b, c, d}* stiamo contando (o togliendo) 6 disposizioni semplici di ordine 3.

Per ottenere una formula generale dobbiamo chiederci cosa rappresenta, in questo caso, 6. Si vede facilmente che 6 è il numero delle [[Disposizioni e permutazioni |permutazioni]] di 3 elementi (*6 = 3!*) e che ogni sottoinsieme corrisponde a tante disposizioni semplici quante sono le permutazioni dei suoi elementi. 

Generalizzando, dunque, si può dire che, avendo un insieme finito *A*, formato da *n* elementi, una **combinazione** permette di sapere il numero di possibili scelte di *k* elementi distinti (con *k ≤ n*) senza dare importanza all’ordine in cui sono disposti. Dato l’insieme *A = a₁, a₂, ..., an*, per ottenere il numero di sottoinsiemi di *A* con *k* elementi, si fa:

![[comb.png]]

L'ultimo membro di questa equazione assume un nome proprio, ossia "**coefficiente binomiale**", e generalmente si legge come "n scegli k".

Supponiamo, ora, di voler sapere quante sono le possibili delegazioni formate di 4 studenti tra 80, tra cui un capogruppo. Questo quesito ha sostanzialmente due possibili soluzioni:
1. scelgo i 4 membri della delegazione e tra essi un capogruppo (4 scelte di un capogruppo), e dunque si ha:
$$C₈₀,₄ × 4$$
2. scelgo 1 capogruppo tra gli 80 membri totali (80 scelte) e poi scelgo i rimanenti 3 membri della delegazione, e dunque si ha:
$$80 × C₇₉,₃$$

Entrambe le soluzioni sono corrette, e possono quindi essere eguagliate; si ha quindi che:

![[comb_num1.png]]
![[comb_num2.png]]

L'equazione generalizzata appena ottenuta si può riscrivere in maniera totalmente combinatoria, e in seguito ancora generalizzata:

![[comb_num3.png]]
![[comb_num4.png]]

[CONTINUO: DISPENSA 4]