Analizziamo un esempio. Supponiamo di voler comporre un panino, scegliendo tra:
- pane bianco, pane al sesamo, pane integrale;
- manzo, maiale, pesce; 
- ketchup, senape, maionese, salsa barbecue;

e di volere che tale panino contenga precisamente due salse diverse, senza dare importanza all’ordine in cui vengono inserite. Intuitivamente, è possibile applicare una [[Disposizioni e permutazioni |disposizione semplice]], e il risultato di questo procedimento sarà dunque:
$$4 • 3 = 12$$
Tuttavia, fare ciò terrà in considerazione anche coppie di stessi elementi ma di ordine diverso (ad esempio ketchup-maionese e maionese-ketchup), cosa che non vogliamo. Per eliminare le coppie simmetriche, dunque, occorrerà dividere il risultato per 2:
$$(4 • 3) / 2 = 6$$
Questo ragionamento, in maniera generalizzata, è conosciuto come "**regola del pastore**" ("*Per contare le pecore in un gregge, conta le zampe e dividi per 4*"). In termini insiemistici il numero delle salse nell’esempio corrisponde al concetto di sottoinsieme di 2 elementi scelti da un insieme di 4; il concetto di insieme formalizza proprio l’idea di una collezione di elementi distinti, non ripetuti e non ordinati.
___
Consideriamo un nuovo esempio: avendo l’insieme *A = {a, b, c, d}*, si vuole contare quanti sono i sottoinsiemi di 3 elementi. Logicamente, si ottiene in maniera immediata che sono 4: *{a, b, c}*, *{a, b, d}*, *{a, c, d}*, *{b, c, d}*. Ma se volessimo contarli, potremmo di nuovo partire con delle disposizioni semplici di ordine 3:
$$abc, acb, bac, bca, cab, cba$$
$$abd, adb, bad, bda, dab, dba$$
$$adc, acd, dac, dca, cad, cda$$
$$dbc, dcb, bdc, bcd, cdb, cbd$$
Si può osservare che il sottoinsieme *{a, b, c}* corrisponde alle 6 sequenze *abc*, *acb*, *bac*, *bca*, *cab*, *cba* formate con i suoi elementi, e analogamente per gli altri 3 sottoinsiemi. Dunque ogni sottoinsieme di 3 elementi corrisponde a 6 disposizioni semplici di lunghezza 3. Dato che sappiamo contare queste ultime, possiamo contare i sottoinsiemi, usando la regola del pastore. Nel nostro caso, ogni "pecora" (sottoinsieme di 3 elementi tra 6) ha 6 zampe (disposizioni semplici di lunghezza 3).

Si nota che è fondamentale che l’associazione sopra descritta tra sottoinsiemi di 3 elementi e disposizioni
semplici soddisfi le seguenti condizioni: 
1. a ogni sottoinsieme di 3 elementi viene associato lo stesso numero (in questo caso 6) di disposizioni semplici;
2. se due sottoinsiemi di 3 elementi sono distinti allora l’insieme delle disposizioni semplici associate al primo non ha elementi in comune con l’insieme delle disposizioni semplici associato al secondo;
3. l’associazione esaurisce l’insieme delle disposizioni semplici di ordine 3 su 4, ossia ogni disposizione semplice di ordine 3 sui 4 elementi *{a, b, c, d}*.

Queste condizioni ci permettono di contare quante sono le **combinazioni semplici** di ordine 3 su *{a, b, c, d}* se sappiamo contare quante sono le disposizioni semplici di ordine 3: ogni volta che contiamo (o togliamo) un insieme di 3 elementi scelti in *{a, b, c, d}* stiamo contando (o togliendo) 6 disposizioni semplici di ordine 3.

Per ottenere una formula generale dobbiamo chiederci cosa rappresenta, in questo caso, 6. Si vede facilmente che 6 è il numero delle [[Disposizioni e permutazioni |permutazioni]] di 3 elementi (*6 = 3!*) e che ogni sottoinsieme corrisponde a tante disposizioni semplici quante sono le permutazioni dei suoi elementi. 

Generalizzando, dunque, si può dire che, avendo un insieme finito *A*, formato da *n* elementi, una **combinazione** permette di sapere il numero di possibili scelte di *k* elementi distinti (con *k ≤ n*) senza dare importanza all’ordine in cui sono disposti. Dato l’insieme *A = a₁, a₂, ..., an*, per ottenere il numero di sottoinsiemi di *A* con *k* elementi, si fa:

![[comb.png]]

L'ultimo membro di questa equazione assume un nome proprio, ossia "**coefficiente binomiale**", e generalmente si legge come "n scegli k".
___
È possibile trovare un modo alternativo di contare i possibili sottoinsiemi di *k* elementi di un insieme *A* di *n* elementi (con *n* > *0*). Immaginiamo tale insieme *A* come un gregge di *n* pecore: si vogliono contare, quindi, tutti i possibili sotto-greggi di *k* pecore scelte nel gregge. Possiamo supporre che il gregge contenga una pecora nera, denotata con *p*; ovviamente, stabilito ciò, ogni sottoinsieme di *k* pecore scelte in *A* può essere solo di uno tra i seguenti due tipi:
1. tipo n°1 (gruppi tolleranti), cioè i gruppi che contengono la pecora nera;
2. tipo n°2 (gruppi intolleranti), cioè i gruppi che non contengono la pecora nera.

I gruppi del primo tipo contengono la pecora nera *p* e altre *k − 1* pecore scelte tra le restanti *n − 1*; i gruppi del secondo tipo, invece, contengono *k* pecore scelte tra *n − 1* pecore (ossia tutte le pecore tranne la quella nera). La tipizzazione risulta essere esaustiva ed esclusiva, e i due casi sopra considerati sono, tecnicamente, una partizione in due parti dell’insieme dei sottoinsiemi di *k* elementi in *A*. Dunque, è possibile concludere che:

![[comb_pecoranera.png]]

Quest'identità permette di calcolare il valore di un coefficiente binomiale ricorsivamente usando valori più piccoli, sfruttando l'ipotetica esistenza di un "**elemento pecora nera**" nell'insieme di partenza.
___
Sfruttando il principio ricavato dalla risoluzione del [[Problema delle caramelle|problema delle caramelle]], è possibile definire un tipo particolare di combinazione, ossia la **combinazione con ripetizione**.

Consideriamo, ad esempio, l’insieme *A* = {a, b, c, d}. Si vogliono contare i modi di scegliere 6 elementi in *A* con possibili ripetizioni, senza dare importanza all’ordine. Una di queste scelte, per intenderci, potrebbe essere {a, a, c, c, c, d}. Chiamiamo "combinazione con ripetizione" di ordine *k* di *n* oggetti un raggruppamento di *k* oggetti scelti tra *n* con possibili ripetizioni, e denotiamo il loro numero con:

![[comb_ripetizione.png]]

Per sapere, in generale, a quanto ammonta questo valore, risulta utile impostare e analizzare una tabella come la seguente:

![[comb_ripetizione_tab.png]]

in cui gli elementi della prima riga (*a₁*, *a₂*, ecc. ecc.) sono gli *n* elementi dell'insieme di partenza, mentre gli elementi della seconda riga (*m₁*, *m₂*, ecc. ecc.) rappresentano il numero di volte che un certo elemento dell'insieme di partenza è incluso nel raggruppamento che si vuole fare. A conti fatti, dunque, si dovrà avere che *k* = *m₁ + m₂ + ... + mn*.

Ci si accorge abbastanza facilmente che tale equazione coincide con una tipica equazione di un problema di scrittura additiva, e dunque che il problema appena spiegato equivale a un problema di caramelle; insomma, il numero delle combinazioni con ripetizione di ordine *k* di *n* oggetti è esattamente uguale al numero di modi di distribuire *k* caramelle tra *n* bambini. Quindi, si ha che:

![[comb_ripetizione_formula.png]]
___
Le combinazioni sono uno strumento molto utile quando si lavora con gli **anagrammi**.

Se si considerano parole composte da lettere uniche (nessuna lettera della parola compare più di una volta al suo interno), il numero di possibili anagrammi di tali parole si può trovare applicando banalmente il [[Principio moltiplicativo|principio moltiplicativo]]: ad esempio, i possibili anagrammi della parola "padre" sono 5! = 120.

Tuttavia, la situazione si complica se si considerano parole che presentano al proprio interno lettere che si ripetono. Ad esempio, i possibili anagrammi della parola "nonna" non sono 5! = 120, perché nel contare i possibili anagrammi di una parola non si considerano copie della stessa lettera come lettere distinte. Occorre, quindi, applicare la regola del pastore, dividendo il risultato precedente per il numero di [[Disposizioni e permutazioni|permutazioni]] dell'insieme di lettere identiche presenti nella parola (in questo caso, tale insieme è {n₁, n₂, n₃}, e quindi occorre dividere per 3! = 6). Dunque, il numero di anagrammi della parola "nonna" è 5! / 3! = 20.

Si applica un ragionamento analogo se le lettere che si ripetono sono più di una; ad esempio, i possibili anagrammi della parola "nonno" sono (5! / 3!) / 2! = 5! / (3! × 2!) = 10, in quanto, ragionando gradualmente, si deve prima dividere il numero di anagrammi totali per le permutazioni delle 3 "n", e poi per le permutazioni delle 2 "o".

Insomma, se si vogliono formare gli anagrammi di una parola formata da *n* occorrenze di lettere, di cui *n₁* sono identiche, si hanno *n!* / *n₁!* possibilità; se ci sono *n₁* lettere identiche di un tipo e *n₂* di un altro tipo, si hanno *n!* / (*n₁!* × *n₂!*) possibilità; e così via. Generalizzando, gli anagrammi di una parola lunga *n* lettere, in cui compaiono *t* gruppi di *n₁*, *n₂*, ..., *nt* lettere ripetute, sono:

![[anagrammi_lettererip.png]]
