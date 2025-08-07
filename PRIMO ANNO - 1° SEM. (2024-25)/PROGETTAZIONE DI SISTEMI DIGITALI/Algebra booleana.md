## Cos'è un'equazione booleana?

A grandi linee, un'**equazione booleana** è un'equazione espressa in termini di variabili "**booleane**", ossia variabili binarie che possono essere **`True`** ($1$) o **`False`** ($0$). Per poter approfondire al meglio questo tipo di equazione, è opportuno innanzitutto imparare alcuni termini specifici:
- una variabile priva di negazioni si trova nella sua "forma vera", o "***true form***";
- il "**complemento**" di una variabile è il suo inverso;
- una variabile (o il suo complemento) viene definita anche come un "***literal***";
- l'*AND* di due o più literals viene anche detto "**prodotto**" o "**implicante**";
- l'*OR* di due o più literals viene anche detto "**somma**".

Avendo stabilito questo glossario, risulta ora cruciale stabilire una **gerarchia** dei vari operatori di un'equazione booleana. In una qualsiasi equazione booleana, l'ordine di precedenza dei tre operatori fondamentali è:
1. NOT
2. AND
3. OR

Per semplificare un'equazione booleana, utilizziamo gli assiomi e i teoremi dell'**algebra booleana**. In gran parte, essa funziona in maniera analoga all'algebra classica, se non in maniera ancora più semplice trattandosi solo di valori binari.
___
## Assiomi dell'algebra booleana

L'algebra booleana si basa su una serie di **assiomi**, ossia delle affermazioni che vengono assunte come vere a priori, essendo di fatto indimostrabili. A partire da questi assiomi, poi, si dimostreranno i vari teoremi. Gli assiomi dell'algebra booleana sono i seguenti:

![[axioms_boolean.png]]

È importante notare che ogni assioma ha un assioma "duale" abbinato ad esso. Questo perché gli assiomi e i teoremi dell'algebra booleana obbediscono al principio della **dualità**: se in un assioma o teorema si sostituisce ogni $0$ con un $1$ e viceversa, nonché ogni *AND* con un *OR* e viceversa, l'affermazione risultante sarà comunque giusta. Il duale di un assioma si indica con il simbolo dell'assioma in questione seguito da un apostrofo (`'`).

Analizziamo singolarmente i vari assiomi:
- gli assiomi A1 e A1' stabiliscono la **caratteristica binaria** di una variabile;
- gli assiomi A2 e A2' definiscono la porta ***NOT***;
- gli assiomi da A3 ad A5 definiscono la porta ***AND***;
- gli assiomi da A3' ad A5' definiscono la porta ***OR***.
___
## Teoremi dell'algebra booleana

Avendo stabilito quali sono gli assiomi di base dell'algebra booleana, possiamo passare ai vari **teoremi**. Partiamo dai teoremi più semplici, ossia quelli che lavorano su **una sola variabile**:

![[theorems1_boolean.png]]

Analizziamo singolarmente i vari teoremi:
- il teorema T1 viene anche detto "**teorema dell'identità**", e afferma che un *AND* tra una variabile e $1$ risulta sempre nella variabile stessa (il suo duale, T1', afferma che un *OR* tra una variabile e $0$ risulta sempre nella variabile stessa);
- il teorema T2 viene anche detto "**teorema dell'annullamento**", e afferma che un *AND* tra una variabile e $0$ risulta sempre in $0$ (il suo duale, T2', afferma che un *OR* tra una variabile e $1$ risulta sempre in $1$); da tale teorema e dal suo duale, si evince che $0$ è "elemento nullo" per l'operazione *AND*, mentre $1$ lo è per l'operazione *OR*;
- il teorema T3 viene anche detto "**teorema dell'idempotenza**", e afferma che un *AND* tra una variabile e sé stessa è uguale alla variabile stessa (il suo duale, T3', afferma la stessa cosa ma con un *OR*);
- il teorema T4 viene anche detto "**teorema dell'involuzione**", e afferma che negare (o complementare) una variabile due volte ritorna la variabile iniziale;
- il teorema T5 viene anche detto "**teorema dei complementi**", e afferma un *AND* tra una variabile e il suo complemento risulta sempre in $0$ (il suo duale, T5', afferma che un *OR* tra una variabile e sé stessa risulta sempre in $1$).

Concretamente, tutti questi teoremi sono utili nel **semplificare un circuito** in qualche modo: T1 implica che se uno dei due input di una porta *AND* è sempre $1$, si può sostituire la porta *AND* con un nodo collegato all'altro input; T2 implica che se uno dei due input di una porta *AND* è sempre $0$, si può sostituire la porta *AND* con un nodo collegato allo $0$; T3 implica che se gli input di una porta *AND* corrispondono alla stessa variabile, si può sostituire la porta con un nodo; T4 implica che due *NOT* consecutivi si cancellano a vicenda, e risultano dunque trascurabili; T5 implica che se i due input di una porta *AND* sono uno il complemento dell'altro, si può sostituire la porta con un cavo collegato a uno $0$. Gli stessi ragionamenti, ovviamente, possono essere fatti anche per i duali di tali teoremi.

Ora, passiamo ai teoremi che lavorano su **più di una variabile**:

![[theorems2_boolean.png]]

Analizziamo singolarmente i vari teoremi:
- i teoremi T6 e T6' definiscono la **proprietà commutativa**, e, analogamente all'algebra classica, affermano che invertire gli input di un *AND* o di un *OR* non cambierà il risultato dell'operazione;
- i teoremi T7 e T7' definiscono la **proprietà associativa**, e, analogamente all'algebra classica, affermano che raggruppare in maniere diverse gli input di un *AND* o di un *OR* non cambierà il risultato dell'operazione;
- i teoremi T8 e T8' definiscono la **proprietà distributiva**; in questo caso, T8 funziona analogamente all'algebra classica (fare un *OR* tra due *AND* che presentano un input in comune equivale a fare un *AND* tra tale input e l'*OR* degli altri input), mentre T8' differisce dal funzionamento di quest'ultima (esso, infatti, afferma che fare un *AND* tra due *OR* che presentano un input in comune equivale a fare un *OR* tra tale input e l'*AND* degli altri input, ma nell'algebra classica la proprietà distributiva non si può applicare su una moltiplicazione tra somme, ossia il caso equivalente);
- i teoremi dal T9 al T11 (detti anche **primo teorema dell'assorbimento**, **secondo teorema dell'assorbimento** e **teorema del consenso**) sono utili per semplificare dei circuiti ridondanti ed eliminare componenti non necessarie.

Il primo teorema dell'assorbimento presenta un caso particolare, che può essere descritto in maniera generica come "fare un *OR* tra l'*AND* tra due input e il complemento di uno di quei due input equivale a fare l'*OR* tra quest'ultimo e l'altro input". Concretamente, questa forma può presentarsi come:
$$AB + \bar{A} = \bar{A} + B, \space \space \space \space \space A\bar{B} + \bar{A} = \bar{A} + \bar{B}, \space \space \space \space \space \bar{A}B + A = A + B, \space \space \space \space \space \bar{A}\bar{B} + A = A + \bar{B}$$
___
## Teorema di De Morgan

Il teorema T12, detto anche **teorema di De Morgan**, risulta forse il più importante e comune tra i teoremi a più variabili analizzati. Il teorema, sostanzialmente, afferma che il complemento di un *AND* di più input corrisponde all'*OR* tra i complementi dei singoli input considerati; il suo duale, invece, afferma la stessa cosa ma con un *OR* al posto dell'*AND* e viceversa.

Secondo il teorema di De Morgan, dunque, una porta *NAND* corrisponde a un *OR* con gli input negati, e viceversa una porta *NOR* corrisponde a un *AND* con gli input negati. Graficamente:

![[demorgan.png]]

Sapere ciò ci consente di semplificare dei circuiti sfruttando la tecnica che viene definita "***bubble pushing***", che segue le seguenti regole di base:
- operare un bubble pushing su una porta *OR* renderà tale porta un *AND*, e viceversa;
- operare un bubble pushing dall'output agli input di una porta logica negherà tutti gli input di tale porta logica;
- operare un bubble pushing dagli input all'output di una porta logica negherà l'output di tale porta logica.

Tale tecnica risulta utilissima nei circuiti CMOS, in quanto essi preferiscono generalmente porte *NAND* e *NOR* a porte *AND* e *OR*. Operare il bubble pushing permette, a partire da un circuito di *NAND* e *NOR*, di rendere più leggibile tale circuito, e di ottenere più facilmente un'equazione booleana che ne descriva il funzionamento. Per operare al meglio il bubble pushing su un circuito, oltre alle **regole** di base stabilite prima, conviene seguire anche le seguenti:
- cominciare dagli output del circuito e muoversi verso gli input;
- lavorando in questa direzione, disegnare ogni porta logica in modo da favorire la "semplificazione" di più bubble possibili (ad esempio, se la porta considerata ha una bubble su un input, conviene rappresentare la porta logica che fornisce tale input con una bubble sull'output, in modo che le due bubble si cancellino a vicenda).
___
