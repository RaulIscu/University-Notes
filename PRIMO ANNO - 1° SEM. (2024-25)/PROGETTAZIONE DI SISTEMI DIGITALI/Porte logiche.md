## Cos'è una porta logica?

Le **porte logiche** sono dei componenti basilari di un circuito logico, che prendono una o più variabili binarie come input e ne restituiscono un'altra come output. Rappresentano il fondamento di qualsiasi **[[Circuiti|circuito]]**, nonché un piccolo circuito a sé stante.

Graficamente, le porte logiche sono rappresentate con dei simboli a cui sono collegati gli input (generalmente entranti dal lato sinistro o superiore) e l'output (generalmente uscente dal lato destro o inferiore); per indicare gli input si utilizzano in genere le lettere iniziali dell'alfabeto, mentre per gli output si utilizzano quelle finali. Inoltre, la relazione tra input e output di una porta logica (come di un qualsiasi circuito) può essere schematizzato in due modi:
- una **tavola di verità**, che presenta gli input sulla sinistra e i corrispettivi output sulla destra;
- un'**[[Algebra booleana#Cos'è un'equazione booleana?|equazione booleana]]**, ossia un'espressione matematica costituita da variabili booleane.
___
## Porte logiche con un input: *NOT* e *BUFFER*

Innanzitutto, analizziamo le porte logiche che accettano **un solo input**, ossia:
- la porta ***NOT***;
- la porta ***BUFFER***.

Una porta logica ***NOT*** presenta un solo input e un solo output; il valore che verrà restituito come output sarà l'**inverso** di quello fornito in input. La rappresentazione grafica di una porta *NOT* è la seguente:

![[not.png]]

Un ***BUFFER*** presenta un solo input e un solo output; il valore che verrà restituito come output sarà **uguale** a quello fornito in input. La rappresentazione grafica di un *BUFFER* è la seguente:

![[buffer.png]]

Dalla rappresentazione di entrambe queste porte logiche, si nota come esse varino solo per un pallino posto in corrispondenza dell'output: tale pallino si definisce generalmente "**bubble**", e se posto in corrispondenza di un output su qualsiasi porta logica, va a invertire l'output stesso.
___
## Porte logiche a più input: *AND*, *OR*, *NAND*, *NOR*, *XOR* e *XNOR*

Ora, analizziamo le porte logiche che accettano **più di un input**, ossia:
- la porta ***AND***;
- la porta ***OR***;
- la porta ***NAND***;
- la porta ***NOR***;
- la porta ***XOR***;
- la porta ***XNOR***.

Una porta logica ***AND*** presenta $n$ input e un solo output; il valore che verrà restituito come output sarà **`True` solo se tutti gli input sono anch'essi `True`**. La rappresentazione grafica di una porta *AND* a 2 input è la seguente:

![[and.png]]

Una porta logica ***OR*** presenta $n$ input e un solo output; il valore che verrà restituito come output sarà **`True` se almeno uno degli input è anch'esso `True`**. La rappresentazione grafica di una porta *OR* a 2 input è la seguente:

![[or.png]]

Una porta logica ***NAND*** (che sta per "*NOT AND*") presenta $n$ input e un solo output; il valore che verrà restituito come output, contrariamente alla porta *AND*, sarà **sempre `True` a meno che tutti gli input siano `True`**. La rappresentazione grafica di una porta *NAND* a 2 input è la seguente:

![[nand.png]]

Una porta logica ***NOR*** (che sta per "*NOT OR*") presenta $n$ input e un solo output; il valore che verrà restituito come output, contrariamente alla porta *OR*, sarà **`True` solo se tutti gli input saranno `False`**. La rappresentazione grafica di una porta *NOR* a 2 input è la seguente:

![[nor.png]]

Una porta logica ***XOR*** (che sta per "*exclusive OR*") presenta $n$ input e un solo output; il valore che verrà restituito come output sarà **`True` se un numero dispari di input saranno anch'essi `True`**; nel caso in cui ci siano solo **2 input**, si può affermare che il valore restituito come output sarà **`True` solo se i due input saranno diversi tra loro**. La rappresentazione grafica di una porta *XOR* a 2 input è la seguente:

![[xor.png]]

Una porta logica ***XNOR*** (che sta per "*exclusive NOR*") presenta $n$ input e un solo output; il valore che verrà restituito come output sarà **`True` se un numero pari di input saranno anch'essi `True`**; nel caso in cui ci siano solo **2 input**, si può affermare che il valore restituito come output sarà **`True` solo se i due input saranno identici**. La rappresentazione grafica di una porta *XNOR* a 2 input è la seguente:

![[xnor.png]]
___
