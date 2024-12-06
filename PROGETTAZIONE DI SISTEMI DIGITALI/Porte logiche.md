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
[PORTE LOGICHE A 2 O PIU' INPUT: AND E OR]


___
[PORTE LOGICHE A 2 O PIU' INPUT: XOR, NAND, NOR E XNOR]
___
[PORTE LOGICHE A PIU' DI DUE INPUT: AND, OR, XOR, NAND, NOR E XNOR]
___
