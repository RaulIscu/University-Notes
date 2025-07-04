Supponiamo di voler contare, in un gruppo di 80 individui, tutte le possibili delegazioni formate da 4 individui ciascuna, tra cui bisogna scegliere anche un capogruppo. Per poter risolvere questo problema, tornano utili le [[Combinazioni|combinazioni]], nonché il [[Principio moltiplicativo|principio moltiplicativo]]; vediamo in che modo:
1. una possibile soluzione potrebbe essere scegliere i 4 membri della delegazione tra gli 80 individui, e in seguito scegliere un capogruppo all'interno della delegazione, ottenendo la seguente formula;

![[doppioconteggio_example1.png]]

2. in alternativa, si potrebbe scegliere un capogruppo tra gli 80 individui, e in seguito scegliere i restanti 3 membri della delegazione tra gli individui rimanenti, ottenendo la seguente formula;

![[doppioconteggio_example2.png]]

Entrambe le soluzioni appena presentate sono corrette ed equivalenti, quindi si può dedurre (e verificare, eventualmente, svolgendo i calcoli), che:

![[doppioconteggio_example3.png]]

Generalizzando, possiamo porre 80 = *n* e 4 = *m*, e si ottiene:

![[doppioconteggio_example4.png]]

Tuttavia, per poter affermare questa equivalenza, è necessario dimostrarla, e dunque dimostrare che l'equazione vale in generale per ogni *n* ≥ *m* > 0. Un modo per verificare ciò è mostrare che l’espressione al primo membro e quella al secondo membro dell'equazione contino la stessa quantità. Nel primo membro, si contano i modi di scegliere una delegazione di *m* membri tra *n* individui, e in essa un capogruppo (scegliendo, quindi, prima gli *m* membri e poi il capogruppo tra essi); ma anche nel secondo membro si conta la stessa cosa, cambiando solo l'ordine delle scelte (si sceglie prima un capogruppo tra gli *n* individui e poi gli altri *m - 1* membri tra gli *n - 1* individui rimanenti). Dunque, le due espressioni sono in realtà identiche per tutte le scelte delle variabili.

Questo metodo di dimostrare un'identità tra due formule, dimostrando che contano la stessa quantità, viene detta "**dimostrazione per doppio conteggio**".
___
[ULTERIORE GENERALIZZAZIONE: FINE DISPENSA 3]