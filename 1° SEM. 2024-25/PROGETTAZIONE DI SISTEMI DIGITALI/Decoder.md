Un ***decoder*** è un componente di logica combinatoria. Sostanzialmente, il suo scopo è quello di scegliere esattamente un *output* tra diversi possibili *output* possibile, in base alla combinazione di *input* che riceve; per questa esclusività degli *output*, essi vengono definiti "*one-hot*", in quanto solo uno di loro è "attivo" in qualsiasi momento.

In generale, un *decoder* può avere un numero *i* di *input* e un numero *2ⁱ* di *output*.
___
Una delle forme più basilari e comuni di *decoder* è il ***2:4 decoder***, che presenta due *input* (*A₀* e *A₁*) e 4 *output* (*Y₀*, *Y₁*, *Y₂* e *Y₃*). Di seguito, la rappresentazione grafica di un 2:4 *decoder* generico e la sua tavola di verità:

![[decoder.png]]

Similmente ai *[[Multiplexer|multiplexer]]*, anche i *decoder* possono essere costruiti mediante un circuito in forma SOP, o meglio utilizzando delle porte *AND*. Generalmente, per un *i:2ⁱ* *decoder*, saranno necessarie *2ⁱ* porte *AND* con *i* *input*, con ogni porta che riceverà la *true form* o il complemento di ciascun *input* presente; si può notare, dunque, che ogni *output* in un *decoder* rappresenta un singolo mintermine degli *input*. Graficamente, un 2:4 *decoder* equivale al seguente circuito:

![[decoder_and.png]]
