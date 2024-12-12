Per semplificare un'equazione booleana, utilizziamo gli assiomi e i teoremi dell'**algebra booleana**. In gran parte, essa funziona in maniera analoga all'algebra classica, se non in maniera ancora più semplice trattandosi solo di valori binari (1 o 0).
___
L'algebra booleana si basa su una serie di **assiomi**, ossia delle affermazioni che vengono assunte come vere a priori, essendo di fatto indimostrabili. A partire da questi assiomi, poi, si dimostreranno i vari teoremi.

Gli assiomi dell'algebra booleana sono i seguenti:

![[axioms_boolean.png]]

È importante notare che ogni assioma ha un assioma "duale" abbinato ad esso. Questo perché gli assiomi e i teoremi dell'algebra booleana obbediscono al principio della **dualità**; dunque, se in un assioma o teorema si sostituisce ogni 0 con un 1 e viceversa, nonché ogni *AND* con un *OR* e viceversa, l'affermazione risultante sarà comunque giusta. Il duale di un assioma si indica con il simbolo di un assioma seguito da un apostrofo (`'`).

Analizziamo singolarmente i vari assiomi:
- gli assiomi A1 e A1' stabiliscono la caratteristica binaria di una variabile;
- gli assiomi A2 e A2' definiscono la porta *NOT*;
- gli assiomi da A3 ad A5 definiscono la porta *AND*;
- gli assiomi da A3' ad A5' definiscono la porta *OR*.
___
Avendo stabilito quali sono gli assiomi di base dell'algebra booleana, possiamo passare ai vari **teoremi**.

Partiamo dai teoremi più semplici, ossia quelli che lavorano su **una sola variabile**:

![[theorems1_boolean.png]]

Analizziamo singolarmente i vari teoremi:
- il teorema T1 viene anche detto "**teorema dell'identità**", e afferma che un *AND* tra una variabile e 1 risulta nella variabile stessa (il suo duale, T1', afferma che un *OR* tra una variabile e 0 risulta sempre nella variabile stessa);
- il teorema T2 viene anche detto "**teorema dell'annullamento**", e afferma che un *AND* tra una variabile e 0 risulta 0 (il suo duale, T2', afferma che un *OR* tra una variabile e 1 risulta 1); da tale teorema e dal suo duale, si evince che 0 è "elemento nullo" per l'operazione *AND*, mentre 1 lo è per l'operazione *OR*;
- il teorema T3 viene anche detto "**teorema dell'idempotenza**", e afferma che un *AND* tra una variabile e sé stessa è uguale alla variabile stessa (il suo duale, T3', afferma la stessa cosa ma con un *OR*);
- il teorema T4 viene anche detto "**teorema dell'involuzione**", e afferma che negare (o complementare) una variabile due volte ritorna la variabile iniziale;
- il teorema T5 viene anche detto "**teorema dei complementi**", e afferma un *AND* tra una variabile e il suo complemento risulta 0 (il suo duale, T5', afferma che un *OR* tra una variabile e sé stessa risulta 1).

Concretamente, tutti questi teoremi sono utili nel **semplificare un circuito** in qualche modo: T1 implica che se uno dei due *input* di una porta *AND* è sempre 1, si può sostituire la porta *AND* con un nodo collegato all'altro *input*; T2 implica che se uno dei due *input* di una porta *AND* è sempre 0, si può sostituire la porta *AND* con un nodo collegato allo 0; T3 implica che se gli *input* di una porta *AND* corrispondono alla stessa variabile, si può sostituire la porta con un nodo; T4 implica che due *NOT* consecutivi si cancellano a vicenda, e risultano dunque trascurabili; T5 implica che se i due *input* di una porta *AND* sono uno il complemento dell'altro, si può sostituire la porta con un cavo collegato a uno 0. Gli stessi ragionamenti, ovviamente, possono essere fatti anche per i duali di tali teoremi.
___
Ora, passiamo ai teoremi che lavorano su **più di una variabile**:

![[theorems2_boolean.png]]

Analizziamo singolarmente i vari teoremi:
- i teoremi T6 e T6' definiscono la **proprietà commutativa**, e, analogamente all'algebra classica, affermano che invertire gli *input* di un *AND* o di un *OR* non cambierà il risultato dell'operazione;
- i teoremi T7 e T7' definiscono la **proprietà associativa**, e, analogamente all'algebra classica, affermano che raggruppare in maniere diverse gli *input* di un *AND* o di un *OR* non cambierà il risultato dell'operazione;
- i teoremi T8 e T8' definiscono la **proprietà distributiva**; in questo caso, T8 funziona analogamente all'algebra classica (fare un *OR* tra due *AND* che presentano un *input* in comune equivale a fare un *AND* tra tale *input* e l'*OR* degli altri *input*), mentre T8' differisce dal funzionamento di quest'ultima (esso, infatti, afferma che fare un *AND* tra due *OR* che presentano un *input* in comune equivale a fare un *OR* tra tale *input* e l'*AND* degli altri *input*, ma nell'algebra classica la proprietà distributiva non si può applicare su una moltiplicazione tra somme, ossia il caso equivalente);
- i teoremi dal T9 al T11 sono utili per semplificare dei circuiti ridondanti ed eliminare componenti non necessarie.

Il teorema T12, detto anche **teorema di De Morgan**, risulta forse il più importante e comune tra i teoremi a più variabili analizzati. Il teorema, sostanzialmente, afferma che il complemento di un *AND* di più termini corrisponde all'*OR* tra i complementi dei singoli termini considerati; il suo duale, invece, afferma la stessa cosa ma con un *OR* al posto dell'*AND* e viceversa.

Secondo il teorema di De Morgan, dunque, una porta NAND corrisponde a un *OR* con gli *input* negati, e viceversa una porta *NOR* corrisponde a un *AND* con gli *input* negati. Graficamente:

![[demorgan.png]]

Sapere ciò ci consente di semplificare dei circuiti sfruttando la tecnica che viene definita "***bubble pushing***", che segue le seguenti regole di base:
- operare un *bubble pushing* su una porta *OR* renderà tale porta un *AND*, e viceversa;
- operare un *bubble pushing* dall'*output* agli *input* di una porta logica negherà tutti gli *input* di tale porta logica;
- operare un *bubble pushing* dagli *input* all'*output* di una porta logica negherà l'*output* di tale porta logica.
