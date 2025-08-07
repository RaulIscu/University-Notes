## Cos'è il sistema binario?

In informatica, qualsiasi dato viene rappresentato usando i **bit**, componenti elementari rappresentati da cifre tra $0$ e $1$. Generalmente, un numero è espresso in “base 10”, o in un sistema decimale. Ad esempio: 
$$5374_{10} = (5 \cdot 10^3) + (3 \cdot 10^2) + (7 \cdot 10^1) + (4 \cdot 10^0)$$
Nell’informatica e nell’elettronica, invece, si utilizza il **sistema binario**, dunque in "base 2"; il meccanismo rimane lo stesso, con la differenza dell’utilizzo esclusivo di $0$ e $1$, ad esempio: 
$$1101_{2} = (1 \cdot 2^3) + (1 \cdot 2^2) + (0 \cdot 2^1) + (1 \cdot 2^0) = 13_{10}$$
Operando in un sistema binario, è utile nonché molto importante avere dimestichezza con le varie **potenze di base $2$**. Tra le più importanti, troviamo **$2^8 = 256$**, che rappresenta un valore degno di nota in quanto le sequenze di bit vengono spesso spezzate e considerate separatamente per semplificare vari processi, e in genere tali sequenze vengono spezzate in "**byte**", ossia gruppi di **8 bit** ciascuno, che possono quindi rappresentare 256 combinazioni diverse. Un’altra potenza utile è sicuramente **$2^{10} = 1024 \simeq 10^3$**, da tenere a mente per calcolare più efficientemente potenze di base $2$ con apice elevato.
___
## Numeri binari segnati: segno/grandezza e complemento a due

Per poter considerare sia numeri positivi che numeri negativi in un sistema binario, si dovranno utilizzare dei sistemi particolari, i più diffusi e importanti dei quali sono il sistema del **segno e grandezza** e quello del **complemento a due** (o **$Ca2$**).

In un sistema **segno/grandezza**, un numero binario composto da $N$ bit presenterà il suo segno nel *msb* (*most significant bit*), e il suo valore assoluto nei restanti $N - 1$ bit. Se il bit del segno sarà uguale a $0$, il numero considerato sarà positivo; viceversa, se il bit del segno sarà uguale a $1$, il numero considerato sarà negativo. Ad esempio:
$$5_{10} = 0101_{2}$$
dove il *msb*, ossia $0$, indica che si tratta di un numero positivo, mentre i restanti bit, ossia $101$, rappresentano il valore assoluto, pari a $5$. Sfortunatamente, il sistema segno/grandezza presenta varie imperfezioni: ad esempio, non è possibile effettuare un'ordinaria [[Addizione tra binari|addizione tra binari]] scritti in tale sistema; inoltre, vi è una rappresentazione distinta per $+0$ e per $-0$.

Per venir meno a questi problemi, è stato ideato il sistema del **complemento a due**. In un numero binario scritto in complemento a due, il *msb* ha valore negativo invece che positivo. Ad esempio:
$$-2_{10} = 1110_{2}$$
dove il *msb* vale $-8$ invece che $8$, e dunque si ha $- 8 + 4 + 2 = -2$. Questo sistema mantiene, di fatto, la proprietà del *msb* per cui esso indichi anche il segno del numero considerato, analogamente al sistema segno/grandezza. Inoltre, risolve i problemi dell'addizione e dello $0$, permettendo un'addizione ordinaria tra binari rappresentati in tale sistema e fornendo una rappresentazione univoca per lo $0$.

È possibile **invertire il segno** di un numero binario scritto in complemento a due in maniera molto comoda e immediata; per fare ciò, si dovrà semplicemente:
1. invertire tutti i bit del numero considerato;
2. aggiungere $1$ al *lsb* (*least significant bit*).

Ad esempio:
$$2_{10} = 0010_{2}$$
$$-2_{10} = 1101_{2} + 1 = 1110_{2}$$
Come già accennato, l'**addizione binaria** funziona regolarmente per i numeri scritti in complemento a due, a patto però che si elimini l'eventuale bit di riporto del *msb* (o l'eventuale bit del risultato che eccede il numero di bit degli addendi). Per **sottrarre**, invece, due numeri in complemento a due, sarà sufficiente sommare il primo con l'inverso del secondo o viceversa. Invece, per **estendere un numero** scritto in complemento a due **a un numero maggiore di bit**, si dovranno aggiungere a sinistra del numero in questione tante copie del *msb* iniziale quanti sono i bit che si vogliono aggiungere al numero.
___
## Numeri binari razionali: fixed point, floating point e IEEE 754

Anche i sistemi appena visti, però, non sono sufficienti a coprire qualsiasi numero possibile: abbiamo considerato, infatti, solo numeri interi, tralasciando completamente numeri dotati di parti frazionarie. Per rappresentare quest'ultimi, esistono principalmente due sistemi: il "***fixed point***" e il "***floating point***".

Un numero frazionario scritto in ***fixed point*** presenta, come suggerisce il nome, un punto binario "fisso", che separa la parte intera da quella frazionaria; il numero di bit conferito a ciascuna di queste due parti del numero viene convenzionalmente stabilito a priori, e per questo il punto in sé viene spesso omesso. Per quanto riguarda la rappresentazione concreta della parte frazionaria, si segue lo stesso ragionamento applicato per dei numeri binari basilari: si moltiplica, dunque, il bit in questione per la potenza di $2$ avente come esponente la posizione del bit, con la particolarità che la parte frazionaria avrà posizioni negative, partendo da $-1$ per i decimi. Ad esempio:
$$6.75_{10} = 0110.1100_{2} = 01101100 = 2^2 + 2^1 + 2^{-1} + 2^{-2}$$
Infatti, $2^{-1} = 0.5$ e $2^{-2} = 0.25$, dunque la somma sarà uguale a $4 + 2 + 0.5 + 0.25 = 6.75$.

È possibile stabilire un **algoritmo** affidabile per convertire numeri frazionari decimali nei loro corrispettivi binari:
1. separare la parte intera da quella frazionaria;
2. convertire la parte intera in binario;
3. moltiplicare la parte frazionaria (che possiamo chiamare $p$) per $2$; se, in seguito a ciò, si ha che $p < 1$, allora la cifra da scrivere sarà $0$, altrimenti si scriva $1$ e si consideri $p = p - 1$;
4. se $p \neq 0$, tornare al passaggio $n°3$, altrimenti finire.

Invece, per rappresentare un numero binario in un sistema ***floating point***, si applica una metodologia che per certi versi rispecchia quella della notazione scientifica per i numeri decimali: infatti, le principali componenti di un numero scritto in questo modo sono il **segno** del numero, la sua **mantissa**, e la base e l'**esponente** della potenza per cui essa è moltiplicata. Nel sistema binario, comunemente, si scrive un numero in *floating point* utilizzando **32 bit**, suddivisi nel modo seguente:
- il primo bit rappresenta il **segno** del numero ($0$ = positivo, $1$ = negativo);
- i successivi 8 bit rappresentano l'**esponente** della potenza (si dà per scontato che la base della potenza sia sempre $2$, trattandosi di un numero binario);
- i restanti 23 bit rappresentano la **mantissa** del numero.

Per comprendere meglio, vediamo un esempio. Supponiamo di voler convertire il numero decimale $228$ in binario usando una rappresentazione *floating point*; innanzitutto, lo si converte in un numero binario di base:
$$228_{10} = 11100100_{2}$$
A questo punto, analogamente alla notazione scientifica, si porta il *floating point* a destra del *msb*, e si moltiplica il tutto per una potenza di $2$ avente come esponente la posizione del *msb* (in questo caso, $7$):
$$11100100 = 1.11001 \cdot 2^7$$
Ora, si potrà costruire una prima rappresentazione del numero in 32 bit:
$$0 \space | \space 00000111 \space | \space 1110010000000000000000$$
dove il primo bit rappresenta il fatto che il numero sia positivo, i successivi 8 l'esponente della potenza di $2$, e i restanti 23 bit la mantissa che viene moltiplicata per la potenza in questione. Si noti che, in realtà, il primo bit della mantissa sarà sempre $1$, dunque lo si può omettere (per la regola dell'***implicit leading 1***):
$$0 \space | \space 00000111 \space | \space 1100100000000000000000$$
In questo modo, la mantissa conserverà esclusivamente la parte frazionaria del numero binario precedentemente scritto in notazione scientifica. Infine, per poter avere la possibilità di esponenti negativi, è opportuno rendere l'esponente un ***biased exponent***, sommandolo appunto con un ***bias***, che per una rappresentazione in 32 bit è uguale a $127_{10}$, o $01111111_{2}$. L'esponente risultante sarà $134_{10}$, ossia $10000110_{2}$, e se si vorrà ricavare nuovamente l'esponente effettivo basterà sottrarre il *bias*:
$$0 \space | \space 10000110 \space | \space 1100100000000000000000$$
Quella appena vista è la rappresentazione nello standard **IEEE 754** in 32 bit di un numero binario. Ovviamente, essa rimane uguale anche per numeri che dispongono di parte frazionaria e negativi. Analizziamo dunque un altro esempio, e convertiamo in binario secondo lo standard IEEE 754 il numero $-58.25_{10}$. Anche in questo caso, si comincia convertendolo in un numero binario di base (trascurando, momentaneamente, il segno), e trasformandolo in seguito in "notazione scientifica":
$$58.25_{10} = 111010.01_{2} = 1.1101001 \cdot 2^5$$
A questo punto, si rappresenta il numero con i canonici 32 bit: il primo sarà 1, rappresentando il segno negativo del numero originale; i successivi 8 corrisponderanno al numero $132_{10}$, dato dalla somma dell'esponente $5$ con il *bias* $127$; infine, i 23 bit rimanenti saranno dati dalla parte frazionaria della mantissa. Il risultato sarà:
$$1 \space | \space 10000100 \space | \space 11010010000000000000000$$
La rappresentazione IEEE 754 di un numero binario presenta alcuni casi particolari, tra cui:

![[ieee754_specialcases.png]]

Inoltre, è importante sapere che vi sono delle variazioni di questo tipo di rappresentazioni, in base alla **precisione** con cui si vogliono rappresentare i numeri:
- ***single-precision***;
- ***half-precision***;
- ***double-precision***.

La rappresentazione ***single-precision*** è quella utilizzata finora, dotata di **32 bit** in cui il primo rappresenta il segno, i seguenti 8 l'esponente della potenza di $2$ e i rimanenti 23 la mantissa; per questa modalità, il *bias* corrisponde sempre a $127_{10}$. In questo formato, il minimo numero positivo rappresentabile ammonta a circa $1.1 \cdot 10^{-38}$, mentre il numero massimo rappresentabile ammonta a circa $3.4 \cdot 10^{38}$.

La rappresentazione ***half-precision***, invece, è dotata di **16 bit** in cui il primo rappresenta il segno, i seguenti 5 l'esponente della potenza di $2$ e i rimanenti 10 la mantissa; per questa modalità, il *bias* corrisponde sempre a $15_{10}$. In questo formato, il minimo numero positivo rappresentabile ammonta a circa $6.1 \cdot 10^{-5}$, mentre il numero massimo rappresentabile ammonta a $65504_{10}$.

La rappresentazione ***double-precision***, infine, è dotata di **64 bit** in cui il primo rappresenta il segno, i seguenti 11 l'esponente della potenza di $2$ e i rimanenti 52 la mantissa; per questa modalità, il *bias* corrisponde sempre a $1023_{10}$. In questo formato, il minimo numero positivo rappresentabile ammonta a circa $2.2 \cdot 10^{-308}$, mentre il numero massimo rappresentabile ammonta a circa $1.79 \cdot 10^{308}$.
___
## Addizioni tra binari

L'**addizione tra binari** funziona in modo sostanzialmente analogo all'addizione tra decimali. I numeri vengono sempre messi in colonna, con le singole cifre nelle colonne corrispondenti, e, nell'addizione di ogni singola colonna, se si ottiene un numero che supera il massimo numero contenibile in una singola cifra si riporta nella colonna successiva. La differenza più sostanziale sta proprio nell'approccio a quest'ultimo punto: mentre nell'addizione tra decimali una singola cifra può rappresentare al massimo $9$, e quindi qualsiasi numero superiore a $9$ presenterà una cifra nella colonna delle decine e, dunque, un riporto, nell'addizione tra binari una singola cifra può rappresentare al massimo $1$, e quindi qualsiasi numero superiore a $1$ presenterà un riporto.

Vediamo un esempio, sommando i binari $1011_{2}$ e $0011_{2}$:

![[binaryaddition.png]]

In questo caso, la somma che avviene nella prima colonna avrà come risultato $10_{2}$, ossia $2_{10}$, dunque si segna $0$ e si riporta $1$; nella seconda colonna, la somma avrà come risultato $11_{2}$, ossia $3_{10}$, dunque si segna $1$ e si riporta $1$; e così via.

In un'addizione tra binari arbitraria, compiuta manualmente, si può tranquillamente sforare il numero di bit dei binari iniziali senza conseguenze; in un sistema digitale, tuttavia, ciò può creare problemi, in quanto il sistema opererà su un numero fisso di bit (pari a quello dei binari iniziali), e ignorerà qualsiasi bit in posizioni superiori a quelle considerate. Quando ciò avviene, si verifica un cosiddetto "***overflow***"; l'avvenire di un *overflow* può essere accertato controllando se vi è un riporto a partire dal *msb* (*most significant bit*).

L'addizione tra numeri binari in *[[Sistema binario#Numeri binari razionali fixed point, floating point e IEEE 754|floating point]]* risulta meno immediata. Si dovrà seguire, infatti, il seguente algoritmo:
1. estrarre i bit relativi al segno e all'esponente dai numeri, e preporre un 1 alle mantisse (l'*implicit leading 1*);
2. comparare gli esponenti dei due numeri;
3. se gli esponenti dei due numeri sono diversi, "[[Sistema binario#Moltiplicazioni tra binari|shiftare]]" la mantissa del numero con esponente minore verso destra di un numero di bit pari alla differenza tra i due esponenti;
4. sommare le due mantisse;
5. se necessario, normalizzare la mantissa risultante (portare il *floating point* alla sua posizione canonica e modificare di conseguenza l'esponente);
6. se la parte frazionaria eccede i bit massimi della precisione che si sta utilizzando, arrotondarla;
7. riassemblare il tutto in un numero binario rappresentato in *floating point*.

Per comprendere meglio i vari passaggi, analizziamo un esempio. Sommiamo i numeri $1.5_{10}$ e $3.25_{10}$; innanzitutto, convertiamoli in binario rappresentandoli in *floating point*:
$$1.5_{10} = 0 \space | \space 01111111 \space | \space 10000000000000000000000$$
$$3.25_{10} = 0 \space | \space 10000000 \space | \space 10100000000000000000000$$
Si tratta di numeri entrambi positivi, con esponenti rispettivamente $127_{10}$ e $128_{10}$, e le cui mantisse complete risultano essere $1.1$ e $1.101$. L'esponente del primo numero risulta essere di un'unità più piccolo rispetto a quello del secondo, quindi la mantissa del primo numero va shiftata verso destra di un bit ($1.1 \gg 1 = 0.11$). A questo punto, si può procedere alla somma delle due mantisse $0.11$ e $1.101$, incolonnandole in maniera tale da far coincidere i punti binari di entrambi i numeri; il risultato sarà $10.011 \cdot 2^1$, che dovrà essere normalizzato:
$$10.011 \cdot 2^1 = 1.0011 \cdot 2^2$$
Non sarà necessario arrotondare la parte frazionaria, in quanto il suo numero di bit è abbondantemente inferiore a 23. A questo punto possiamo procedere a riassemblare il numero binario risultante:
$$0 \space | \space 10000001 \space | \space 00110000000000000000000$$
___
## Moltiplicazioni tra binari

Le **moltiplicazioni tra binari** funzionano in maniera analoga alle moltiplicazioni tra numeri decimali. Dopo aver appropriatamente incolonnato i numeri da moltiplicare, si procede al calcolo dei vari "prodotti parziali", ottenuti moltiplicando il moltiplicando per ogni singola cifra del moltiplicatore; come per i numeri decimali, ognuno di questi prodotti parziali andrà poi appuntato spostato a sinistra di una cifra (in questo caso, di un bit) rispetto a quello precedente. Una volta trovati tutti i prodotti parziali ed essersi assicurati di averli incolonnati accuratamente, si può procedere alla loro somma. 

Di seguito, per esempio, la moltiplicazione tra i numeri $5_{10}$, ossia $0101_{2}$, e $7_{10}$, ossia $0111_{2}$:

![[binarymult.png]]

Un tipo particolare di moltiplicazione, ma anche di divisione, viene eseguito mediante l'utilizzo di "**shifters**", che consentono di moltiplicare o dividere un numero binario per una determinata potenza di $2$. Infatti:
- shiftare un numero binario verso **sinistra** di $N$ bit vuol dire **moltiplicarlo** per la potenza di $2$ con esponente $N$;
- shiftare un numero binario verso **destra** di $N$ bit vuol dire **dividerlo** per la potenza di $2$ con esponente $N$.

Gli shifters sono "**$\gg$**" per le divisioni e "**$\ll$**" per le moltiplicazioni. Vediamo degli esempi che coinvolgono numeri binari rappresentati in [[Sistema binario#Numeri binari segnati segno/grandezza e complemento a due|complemento a due]]:
$$11101_{2} \ll 2 = 10100_{2}$$
$$10000_{2} \gg 2 = 11100_{2}$$
La moltiplicazione tra numeri binari in *[[Sistema binario#Numeri binari razionali fixed point, floating point e IEEE 754|floating point]]* risulta meno immediata. Si dovrà seguire, infatti, il seguente algoritmo:
1. estrarre gli esponenti dei due numeri e sommarli;
2. moltiplicare le mantisse tra di loro;
3. se necessario, normalizzare il risultato;
4. riassemblare il numero binario risultante.
___