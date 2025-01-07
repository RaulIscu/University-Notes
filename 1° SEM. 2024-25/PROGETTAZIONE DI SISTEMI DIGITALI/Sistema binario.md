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
Anche i sistemi appena visti, però, non sono sufficienti a coprire qualsiasi numero possibile: abbiamo considerato, infatti, solo numeri interi, tralasciando completamente numeri dotati di parti decimali, ossia frazioni. Per rappresentare quest'ultime, esistono principalmente due sistemi: il "***fixed point***" e il "***floating point***".

Un numero frazionario scritto in ***fixed point*** presenta, come suggerisce il nome, un punto binario "fisso", che separa la parte intera da quella frazionaria; il numero di bit conferito a ciascuna di queste due parti del numero viene convenzionalmente stabilito a priori, e per questo il punto in sé viene spesso omesso. Per quanto riguarda la rappresentazione concreta della parte frazionaria, si segue lo stesso ragionamento applicato per dei numeri binari basilari: si moltiplica, dunque, il bit in questione (1 o 0) per la potenza di 2 avente come esponente la posizione del bit, con la particolarità che la parte frazionaria avrà posizioni negative, partendo da -1 per i decimi. Ad esempio:
$$6.75₁₀ = 0110.1100₂ = 01101100 = 2² + 2¹ + 2^-¹ + 2^-²$$
Infatti, *2^-1 = 0.5* e *2^-2 = 0.25*, dunque la somma sarà uguale a *4 + 2 + 0.5 + 0.25 = 6.75*.

È possibile stabilire un algoritmo affidabile per convertire numeri frazionari decimali nei loro corrispettivi binari:
1. separare la parte intera da quella frazionaria;
2. convertire la parte intera in binario;
3. per la parte frazionaria (p), moltiplicarla per 2; se p<1 la cifra da scrivere sarà 0, altrimenti si scriva 1 e p = p - 1;
4. se p ≠ 0, tornare al passaggio n°3, altrimenti finire.

Invece, per rappresentare un numero binario in un sistema ***floating point***, si applica una metodologia che per certi versi rispecchia quella della notazione scientifica per i numeri decimali: infatti, le principali componenti di un numero scritto in questo modo sono il **segno** del numero, la sua **mantissa**, e la base e l'**esponente** della potenza per cui essa è moltiplicata.

Nel sistema binario, in genere, si scrive un numero in *floating point* utilizzando **32 bit**, suddivisi nel modo seguente:
- il primo bit rappresenta il segno del numero (0 = positivo, 1 = negativo);
- i successivi 8 bit rappresentano l'esponente della potenza (si dà per scontato che la base sia sempre 2, trattandosi di un numero binario);
- i restanti 23 bit rappresentano la mantissa del numero.

Per comprendere meglio, vediamo un esempio. Supponiamo di voler convertire il numero decimale 228 in binario usando una rappresentazione *floating point*; innanzitutto, lo si converte in un numero binario di base:
$$228₁₀ = 11100100₂$$
A questo punto, analogamente alla notazione scientifica, si porta il *floating point* a destra dell'*msb*, e si moltiplica il tutto per una potenza di 2 avente come esponente la posizione dell'*msb* (in questo caso, 7):
$$11100100 = 1.11001 × 2⁷$$
Ora, si potrà costruire il numero completo in 32 bit:
$$0|00000111|1110010000000000000000$$
dove il primo bit rappresenta il fatto che il numero sia positivo, i successivi 8 l'esponente della potenza di 2, ossia 7, e i restanti 23 bit la mantissa che viene moltiplicata per la potenza in questione. Si noti che, in realtà, il primo bit della mantissa sarà sempre 1, dunque lo si può omettere (***implicit leading 1***):
$$0|00000111|1100100000000000000000$$
In questo modo, la mantissa conserverà esclusivamente la parte frazionaria del numero binario precedentemente scritto in notazione scientifica. Infine, per potere avere la possibilità di esponenti negativi, è opportuno rendere l'esponente un ***biased exponent***, sommandolo appunto con un ***bias***, che per una rappresentazione in 32 bit è 127, o 01111111 in binario. L'esponente risultante sarà 134, ossia 10000110, e per ricavare l'esponente effettivo basterà sottrarre il *bias*:
$$0|10000110|1100100000000000000000$$
Quella appena vista è la rappresentazione nello standard **IEEE 754** in 32 bit *floating point* di un numero binario. Ovviamente, essa rimane uguale anche per numeri che dispongono di parte frazionaria e negativi. Analizziamo dunque un altro esempio, e convertiamo in binario secondo lo standard IEEE 754 il numero decimale -58.25. Anche in questo caso, si comincia convertendolo in un numero binario di base (trascurando, momentaneamente, il segno), e trasformandolo in seguito in "notazione scientifica":
$$58.25₁₀ = 111010.01₂ = 1.1101001 × 2^5$$
A questo punto, si rappresenta il numero con i canonici 32 bit: il primo sarà 1, rappresentando il segno negativo del numero originale; i successivi 8 corrisponderanno al numero 132, dato dalla somma dell'esponente 5 con il *bias* 127; infine, i 23 bit rimanenti saranno dati dalla parte frazionaria della mantissa. Il risultato sarà:
$$1|10000100|11010010000000000000000$$
___
La rappresentazione IEEE 754 in *floating point* di un numero binario presenta alcuni casi particolari, tra cui:

![[ieee754_specialcases.png]]

Inoltre, è importante sapere che vi sono delle variazioni di questo tipo di rappresentazioni, in base alla **precisione** e al *range* con cui si vogliono rappresentare i numeri:
- ***single-precision***;
- ***half-precision***;
- ***double-precision***.

La rappresentazione ***single-precision*** è quella utilizzata finora, dotata di 32 bit in cui il primo rappresenta il segno, i seguenti 8 l'esponente della potenza di 2 e i rimanenti 23 la mantissa. Per questa modalità, il *bias* corrisponde sempre a 127.

La rappresentazione ***half-precision***, invece, è dotata di 16 bit in cui il primo rappresenta il segno, i seguenti 5 l'esponente della potenza di 2 e i rimanenti 10 la mantissa. Per questa modalità, il *bias* corrisponde sempre a 15.

La rappresentazione ***double-precision***, infine, è dotata di 64 bit in cui il primo rappresenta il segno, i seguenti 11 l'esponente della potenza di 2 e i rimanenti 52 la mantissa. Per questa modalità, il *bias* corrisponde sempre a 1023.
