In informatica, qualsiasi dato viene rappresentato usando i ***bit***, componenti elementari rappresentati da cifre tra ***0*** e ***1***.

Generalmente, un numero è espresso in “base 10”, o in un sistema decimale. Ad esempio: 
$$5374₁₀ = (5 × 10^3) + (3 × 10^2) + (7 × 10^1) + (4 × 10^0)$$
Nell’informatica e nell’elettronica, invece, si utilizza il **sistema binario**, dunque in "base 2"; il meccanismo rimane lo stesso, con la differenza dell’utilizzo esclusivo di 1 e 0, ad esempio: 
$$1101₂ = (1 × 2^3) + (1 × 2^2) + (0 × 2^1) + (1 × 2^0) = 13₁₀$$
Operando in un sistema binario, è utile nonché molto importante avere dimestichezza con le varie potenze di base 2. Tra le più importanti, troviamo **2⁸ = 256**, che rappresenta un valore degno di nota in quanto le sequenze di *bit* vengono spesso spezzate e considerate separatamente per semplificare vari processi, e in genere tali sequenze vengono spezzate in ***byte*** composti da 8 bit ciascuno, che possono quindi rappresentare 256 combinazioni diverse. Un’altra potenza utile è sicuramente  **2¹⁰ = 1024 ≃10³**, da tenere a mente per calcolare più efficientemente potenze di base 2 con apice elevato.
___
Gli esempi di numeri binari visti finora riguardano esclusivamente numeri positivi. Per poter considerare sia numeri positivi che numeri negativi in un sistema binario, si dovranno utilizzare dei sistemi particolari, i più diffusi e importanti dei quali sono il sistema del **segno e grandezza** e quello del **complemento a due**.

In un sistema **segno/grandezza**, un numero binario composto da *N* bit presenterà il suo segno nel *msb* (*most significant bit*), e il suo valore assoluto nei restanti *N - 1* bit. Se il bit del segno sarà uguale a 0, il numero considerato sarà positivo; viceversa, se il bit del segno sarà uguale a 1, il numero considerato sarà negativo. Ad esempio:
$$5₁₀ = 0101₂$$
dove l'*msb*, ossia 0, indica che si tratta di un numero positivo, mentre i restanti bit, ossia 101, rappresentano il valore assoluto, pari a 5.

Sfortunatamente, il sistema segno/grandezza presenta varie imperfezioni: ad esempio, non è possibile effettuare un'ordinaria [[Addizione tra binari|addizione tra binari]] scritti in tale sistema; inoltre, in tale sistema vi è una rappresentazione distinta per +0 e -0.

Per venir meno a questi problemi, è stato ideato il sistema del **complemento a due**. In un numero binario scritto in complemento a due, l'*msb* ha valore negativo invece che positivo. Ad esempio:
$$-2₁₀ = 1110₂$$
dove l'*msb* vale -8 invece che 8, e dunque si ha -8 + 4 + 2 = -2.

Questo sistema mantiene, di fatto, la proprietà dell'*msb* per cui esso indichi anche il segno del numero considerato, analogamente al sistema segno/grandezza. Inoltre, risolve i problemi dell'addizione e dello 0, permettendo un'addizione ordinaria tra binari rappresentati in tale sistema e fornendo una rappresentazione univoca per lo 0.

È possibile **invertire il segno** di un numero binario scritto in complemento a due; per fare ciò, si dovrà semplicemente:
1. invertire tutti i bit del numero considerato;
2. aggiungere 1 al *lsb* (*least significant bit*).

Ad esempio:
$$2₁₀ = 0010₂$$
$$-2₁₀ = 1101₂ + 1 = 1110₂$$
Come già accennato, l'addizione binaria funziona regolarmente per i numeri scritti in complemento a due, a patto però che si elimini l'eventuale bit di riporto dell'*msb* (o l'eventuale bit del risultato che eccede il numero di bit degli addendi). Per sottrarre, invece, due numeri in complemento a due, sarà sufficiente sommare il primo con l'inverso del secondo o viceversa.

Per estendere un numero scritto in complemento a due a un numero maggiore di bit, si dovranno aggiungere a sinistra del numero in questione tante copie dell'*msb* iniziale quanti sono i bit che si vogliono aggiungere al numero.
___
