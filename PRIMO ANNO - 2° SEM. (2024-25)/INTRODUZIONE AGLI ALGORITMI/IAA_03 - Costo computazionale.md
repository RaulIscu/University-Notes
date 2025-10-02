Dopo aver approfondito il concetto di [[IAA_02 - Notazione asintotica#Cos'è la notazione asintotica?|notazione asintotica]] e aver capito come derivarla e semplificarla per varie funzioni, siamo pronti per capire come calcolare effettivamente il **costo computazionale** di un algoritmo.

Prima di procedere, facciamo alcune considerazioni. Innanzitutto, è ragionevole pensare che **il costo computazionale di un algoritmo**, inteso come la funzione che rappresenta il suo tempo di esecuzione, **sia una funzione monotona non decrescente della dimensione dell'input** di tale algoritmo (in parole povere, all'aumentare della dimensione dell'input il tempo di esecuzione o rimane pressoché costante o cresce). Capiamo, dunque, che per calcolare il costo computazionale di un algoritmo è necessario definire proprio la dimensione del suo input: in un [[IAA_06 - Algoritmi di ordinamento|algoritmo di ordinamento]], essa sarà il numero di elementi da ordinare; in un algoritmo che lavora su [[IAA_07 - Strutture dati#Alberi|alberi]], sarà il numero di nodi dell'albero in questione; e così via.

Inoltre, essendo la notazione asintotica il nostro strumento principale nel calcolo del costo computazionale, bisogna sempre tenere presente che **il costo computazionale ottenuto per un algoritmo è effettivamente valido solo asintoticamente**, cioè per input relativamente grandi.

Va sottolineato, inoltre, che **a volte il costo di un algoritmo non dipende solo dalla dimensione dell'input, ma anche dal valore esatto dello stesso**: in casi del genere, è opportuno suddividere lo studio del costo computazionale in termini di "**caso migliore**" e di "**caso peggiore**". A parità di dimensione dell'input, il caso peggiore corrisponde a quello in cui l'input assume valori tali per cui l'algoritmo deve eseguire il massimo numero di operazioni; viceversa, il caso migliore corrisponde all'input che permette all'algoritmo di eseguire il minimo numero di operazioni.

## Come calcolare il costo computazionale di un algoritmo?

Calcolare il costo computazionale di un algoritmo, nel suo complesso, implica il calcolare il **costo computazionale di ognuna delle sue istruzioni**, prevedere il **numero di volte che le istruzioni verranno eseguite** (ciò risulta importante soprattutto quando si trattano istruzioni iterative), e sommare i costi di ogni singola istruzione per ottenere il costo computazionale totale.

Possiamo suddividere le varie istruzioni di un algoritmo in più categorie, in base al loro costo computazionale o al metodo specifico utilizzato per calcolarlo:
- le **istruzioni elementari**;
- le **istruzioni condizionali**;
- le **istruzioni iterative**.

Partiamo dalle **istruzioni elementari**, che comprendono le operazioni aritmetiche, la lettura o scrittura di una variabile, la valutazione di una condizione logica, la stampa di un valore, ecc. ecc. Tutte queste istruzioni hanno un **costo computazionale costante**, dunque pari a **$\theta(1)$**.

Passiamo, ora, alle **istruzioni condizionali**, ossia quelle che si trovano nella forma:

```
if (condizione):
	bloccoDiIstruzioni1
else:
	bloccoDiIstruzioni2
```

In questo caso, il costo computazionale sarà pari alla somma tra il **costo della verifica della condizione** (solitamente pari a $\theta(1)$) e il **massimo dei costi dei due blocchi `bloccoDiIstruzioni1` e `bloccoDiIstruzioni2`**.

Infine abbiamo le **istruzioni iterative**, che comprendono i cicli `for` e i cicli `while`: il costo computazionale di queste istruzioni è pari alla somma dei **costi massimi di ciascuna delle iterazioni dell'istruzione**, più il **costo di verifica della condizione**; nel caso in cui tutte le iterazioni abbiano lo stesso costo massimo, allora il costo complessivo sarà ottenibile con il **prodotto del costo massimo di una singola iterazione per il numero di iterazioni previste**. In entrambi i casi, è comunque fondamentale calcolare il numero di iterazioni che l'istruzione iterativa considerata dovrebbe svolgere. Bisogna ricordare, inoltre, che **la condizione che controlla l'istruzione iterativa verrà sempre valutata una volta in più rispetto al numero di iterazioni**, poiché l'ultima valutazione sarà sempre quella che porrà fine al ciclo.

##### Esempio n°1: ricerca del massimo in un array

[dispensa notazione asintotica: pag. 20]
___
##### Esempio n°2: somma dei primi $n$ interi

[dispensa notazione asintotica: pag. 23]
___
##### Esempio n°3: valutazione di un polinomio in un punto $c$

[dispensa notazione asintotica: pag. 24]
___

