Il concetto di [[Combinazioni|combinazione]] può essere applicato in una maniera particolare per alcuni problemi specifici, come il "**problema delle caramelle**".

Supponiamo di avere 7 caramelle, e di volerle distribuire tra 6 bambini: in quanti modi è possibile attuare questa distribuzione? Per poter analizzare e visualizzare più facilmente questo problema, stabiliamo una [[Dimostrazione per traduzione|buona traduzione]] per le possibili soluzioni. Ad esempio, la seguente distribuzione:

![[caramelle_example1.png]]

può essere rappresentata con una stringa composta da 7 pallini (che simboleggiano le caramelle) e 5 barrette verticali (che fungono da separatori tra 2 bambini), nel modo seguente:

![[caramelle_example2.png]]

Si può applicare lo stesso sistema per rappresentare una qualsiasi delle possibili distribuzioni di caramelle tra i 6 bambini. Ora, supponiamo di voler comunicare nella maniera più efficiente possibile questa specifica soluzione a qualcun'altro, presupponendo che esso sia a conoscenza della lunghezza della stringa e del numero totale di pallini e di barrette utilizzate. Dato che ognuna delle 12 posizioni della stringa può contenere soltanto una barretta oppure un pallino, è sufficiente comunicare la posizione dei 7 pallini oppure delle 5 barrette.

Scegliamo di comunicare la posizione delle 5 barrette: la soluzione, quindi, è completamente specificata da un sottoinsieme di 5 elementi in un insieme di 12 (le posizioni). Per esempio, la soluzione di sopra è rappresentata dall’insieme {3, 4, 6, 8, 9}, che indica la posizione delle barrette (contando le posizioni da sinistra a partire da 1). Le soluzioni sono tante quanti sono i sottoinsiemi di 5 elementi in un insieme di 12, ossia *C₁₂, ₅*.

Ora, scegliamo invece di comunicare la posizione dei 7 pallini: la soluzione, quindi, è completamente specificata da un sottoinsieme di 7 elementi in un insieme di 12. Per esempio, la soluzione di sopra è rappresentata dall’insieme {1, 2, 5, 7, 10, 11, 12}, che indica la posizione dei pallini. Le soluzioni sono tante quanti sono i sottoinsiemi di 7 elementi in un insieme di 12, ossia *C₁₂, ₇*.

Ovviamente, entrambe le soluzioni sono equivalenti e dunque *C₁₂, ₅* = *C₁₂, ₇* (in quanto *C₁₂, ₅* = *C₁₂, ₁₂₋₅*).

Generalizzando il tutto, se si vogliono distribuire *m* caramelle tra *t* bambini, il problema diventa contare le possibili stringhe formate da *m* pallini e *t − 1* barrette. Come visto sopra, basta contare o le posizioni delle barrette o quelle dei pallini: se si contano le posizioni dei pallini, si dovranno contare i sottoinsiemi di *m* elementi in un insieme di *m + t − 1* elementi; invece, se si contano le posizioni delle barrette, si dovranno contare i sottoinsiemi di *t − 1* elementi in un insieme di *m + t − 1* elementi. Essendo le due soluzioni equivalenti, si può affermare che il numero di modi di distribuire *m* caramelle tra *t* bambini è dato da:

![[caramelle.png]]
___
Trascendendo l'esempio delle caramelle, questo principio torna utile anche in altre casistiche, ad esempio nel trovare le "**scritture additive**" di un intero.

Generalmente, si definisce "scrittura additiva" di un intero la scrittura di un intero non negativo *m* come somma di *t* interi non negativi. Ad esempio, supponiamo di voler trovare il numero di modi per scrivere il numero 7 come somma di 6 interi non negativi; insomma, ci si sta chiedendo quante sono le possibili soluzioni dell'equazione:
$$x_1 + x_2 + x_3 + x_4 + x_5 + x_6 = 7$$
Intuitivamente, trovare il numero di soluzioni di quest'equazione equivale a trovare il numero di modi in cui si può "distribuire" il numero 7 in 6 interi non negativi. Si può utilizzare quindi lo stesso ragionamento spiegato in precedenza, dove 7 = *m* (numero di caramelle) e 6 = *t* (numero di bambini), e la soluzione sarà dunque data da *C₁₂, ₅*.

I problemi di scrittura additiva di un intero ammettono molte variazioni, in base ai vincoli aggiuntivi che si possono imporre sul valore delle variabili.

Ad esempio, consideriamo ora la seguente equazione:
$$x_1 + x_2 + x_3 + x_4 + x_5 = 10$$
Si vuole sapere quante sono le possibili soluzioni intere e positive della stessa. La variazione qui sta nella positività stretta dei valori, che esclude quindi la presenza di zeri: tornando al ragionamento delle caramelle, il problema equivale a distribuire 10 caramelle a 5 bambini dandone almeno una a ciascuno. 

Un modo intelligente di affrontare il problema può essere ridurlo a un problema privo del vincolo aggiuntivo. Per fare ciò, si inizia distribuendo a priori una caramella a ciascun bambino, soddisfacendo subito il vincolo; così facendo, restano da assegnare 10 − 5 = 5 caramelle tra i 5 bambini, ma stavolta senza il vincolo di dare almeno una caramella a ciascuno. La soluzione al problema così posto è dunque *C₉, ₄*. 

Generalizzando, la soluzione a questo tipo di problema è:

![[caramelle_almenouna.png]]

Analizziamo ancora un altro esempio, più complesso. Si suppone di avere 11 caramelle, e di volerle distribuire tra 3 bambini, in modo che nessuno ne riceva più di 4: in quanti modi si può compiere tale operazione? Quello che il problema chiede, sottoforma di una scrittura additiva, è il numero di soluzioni dell'equazione:
$$x_1 + x_2 + x_3 = 11$$
con il vincolo di avere x₁, x₂, x₃ ≤ 4.

Conviene, in questo caso, non contare gli oggetti con la proprietà *P* richiesta, ma piuttosto effettuare un [[Passaggio al complemento|passaggio al complemento]] e trovare invece quelli che rientrano nell'insieme "non *P*", formato quindi dalle soluzioni in cui almeno un bambino ha più di 4 caramelle. Per ottenere la cardinalità di questo insieme, impostiamo un problema di unione, effettuando una partizione dell'insieme non-*P* nei seguenti 3 tipi:
- tipo *A*, ossia le soluzioni in cui il primo bambino ha più di 4 caramelle;
- tipo *B*, ossia le soluzioni in cui il secondo bambino ha più di 4 caramelle;
- tipo *C*, ossia le soluzioni in cui il terzo bambino ha più di 4 caramelle.

La risposta cercata è data dall'unione *A* ∪ *B* ∪ *C*, che può essere ottenuta applicando il [[Principio di inclusione-esclusione|principio di inclusione-esclusione]] a tre termini, per cui:
$$(A ∪ B ∪ C) = A + B + C − (A ∩ B) − (A ∩ C) − (B ∩ C) + (A ∩ B ∩ C)$$
Vediamo come calcolare i vari termini dell'operazione:
- per contare le cardinalità di *A*, *B* e *C*, si suppone di dare a priori 5 caramelle a uno dei bambini (a seconda di quale insieme si sta contando), e in seguito si contano i modi di distribuire le restanti 6 caramelle tra i 3 bambini, senza ulteriori vincoli;
- per contare le cardinalità di *A ∩ B*, *A ∩ C* e *B ∩ C*, si suppone di dare a priori 5 caramelle a due dei bambini (a seconda di quale insieme si sta contando), e in seguito si contano i modi di distribuire la restante caramella tra i 3 bambini;
- la cardinalità di *A ∩ B ∩ C* è pari a 0, in quanto per poter dare 5 o più caramelle a tutti e 3 i bambini si dovrebbero avere almeno 15 caramelle.

Svolgendo i calcoli, si ottiene che la cardinalità di non-*P* è quindi:

![[caramelle_example3.png]]

Per ottenere la soluzione al problema iniziale, si sottrae la quantità appena trovata al numero totale di soluzioni possibili per il problema privo di vincoli, dato da *C₁₁₊₃₋₁, ₃₋₁* = *C₁₃, ₂* = 78. Dunque, le soluzioni che rispettano la proprietà *P* sono 78 - 75 = 3.

Il metodo sopra illustrato può essere generalizzato per qualsiasi problema su soluzioni di equazioni additive con un vincolo sul valore massimo delle variabili.