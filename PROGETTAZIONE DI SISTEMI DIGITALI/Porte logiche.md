Le **porte logiche** sono dei componenti basilari di un circuito logico, che prendono una o più variabili binarie come *input* e ne restituiscono un'altra come *output*.

Graficamente, le porte logiche sono rappresentate con dei simboli a cui sono collegati gli *input* (generalmente entranti dal lato sinistro o superiore) e l'*output* (generalmente uscente dal lato destro o inferiore); per indicare gli *input* si utilizzano in genere le lettere iniziali dell'alfabeto, mentre per gli *output* si utilizzano quelle finali. Inoltre, la relazione tra *input* e *output* di una porta logica può essere schematizzato in due modi:
- una tavola della verità, che presenta gli *input* sulla sinistra e i corrispettivi *output* sulla destra;
- un'equazione booleana, ossia un'espressione matematica costituita da variabili binarie.
___
Innanzitutto, analizziamo le porte logiche che accettano **un solo *input***.

Una porta logica ***NOT*** presenta un solo *input* e un solo *output*; il valore che verrà restituito come *output* sarà l'inverso di quello fornito in *input*. La rappresentazione grafica di una porta *NOT* è la seguente:
![[not.png]]
Un ***BUFFER*** presenta un solo *input* e un solo *output*; il valore che verrà restituito come *output* sarà uguale a quello fornito in *input*. La rappresentazione grafica di un *BUFFER* è la seguente:
![[buffer.png]]
Da un punto di vista logico, un *BUFFER* può sembrare sostanzialmente inutile, in quanto non porta alcuna variazione e si comporta come un qualsiasi cavo; nel concreto, però, esso trova un senso di esistenza nel compiere varie mansioni, principalmente svolgendo un ruolo di ripetitore, come trasportare grandi quantità di corrente a un motore o mandare rapidamente un certo *output* a varie porte logiche.

Dalla rappresentazione di entrambe queste porte logiche, si nota come esse varino solo per un pallino posto in corrispondenza dell'*output*: tale pallino si definisce generalmente "***bubble***", e se posto in corrispondenza di un *output* su qualsiasi porta logica, va a invertire l'*output* stesso.
___
Ora, analizziamo le porte logiche principali che accettano **più di un *input***.

Una porta logica ***AND*** presenta 2 *input* e un solo *output*; il valore che verrà restituito come *output* sarà `True` solo se entrambi gli *input* della porta logica sono anch'essi `True`. La rappresentazione grafica di una porta *AND* è la seguente:
![[and.png]]
L'equazione booleana di una porta *AND* può essere scritta in vari modi, tra cui:
- Y = AB;
- Y = A • B;
- Y = A ∩ B.

Una porta logica ***OR*** presenta 2 *input* e un solo *output*; il valore che verrà restituito come *output* sarà `True` se almeno uno degli *input* della porta logica è anch'esso `True`. La rappresentazione grafica di una porta *OR* è la seguente:
![[or.png]]
Oltre a Y = A + B, l'equazione booleana di una porta *OR* può prendere anche la forma Y = A ∪ B.
___
Partendo dalle porte *AND* e *OR*, si possono creare anche altre porte logiche "complesse", ossia:
- la porta *XOR*;
- la porta *NAND*;
- la porta *NOR*;
- la porta *XNOR*.

Una porta logica ***XOR*** (che sta per "*exclusive OR*") presenta 2 *input* e un solo *output*; il valore che verrà restituito come *output*, similmente alla porta *OR*, sarà `True` se uno degli *input* della porta logica è anch'esso `True`, ma, a differenza di quest'ultima, non se entrambi gli *input* saranno `True`. La rappresentazione grafica di una porta *XOR* è la seguente:
![[xor.png]]
Una porta logica ***NAND*** (che sta per "*NOT AND*") presenta 2 *input* e un solo *output*; il valore che verrà restituito come *output*, contrariamente alla porta *AND*, sarà sempre `True` a meno che entrambi gli *input* siano `True`. La rappresentazione grafica di una porta *NAND* è la seguente:
![[nand.png]]
Una porta logica ***NOR*** (che sta per "*NOT OR*") presenta 2 *input* e un solo *output*; il valore che verrà restituito come *output*, contrariamente alla porta *OR*, sarà `True` solo se entrambi gli *input* saranno `False`. La rappresentazione grafica di una porta *NOR* è la seguente:
![[nor.png]]
Una porta logica ***XNOR*** (che sta per "*exclusive NOR*") presenta 2 *input* e un solo *output*; il valore che verrà restituito come *output*, contrariamente alla porta *XOR*, sarà `True` solo se entrambi gli *input* saranno uguali (o entrambi `True` o entrambi `False`). Per questo motivo, una porta logica *XNOR* a due *input* viene anche detta "porta di equivalenza". La rappresentazione grafica di una porta *XNOR* è la seguente:
![[xnor.png]]
___
Molte delle porte logiche analizzate finora possono avere anche **più di 2 *input***; generalizzando, le principali e più comuni sono:
- la porta *AND*, che con un numero *N* di *input* restituirà come *output* un valore `True` solo se tutti gli *N* *input* saranno `True`;
- la porta *OR*, che con un numero *N* di *input* restituirà come *output* un valore `True` se almeno uno degli *N* *input* sarà `True`;
- la porta *NOR*, che con un numero *N* di *input* restituirà come *output* un valore `True` solo se tutti gli *N* *input* saranno `False`;
- la porta *NAND*, che con un numero *N* di *input* restituirà sempre come *output* un valore `True`, a meno che tutti gli *N* *input* siano `True`;
- la porta *XOR*;
- la porta *XNOR*.
