Un ***multiplexer*** (detto anche ***mux***) è un componente di logica combinatoria. Sostanzialmente, il suo scopo è quello di scegliere un *output* tra diversi possibili *input*, in base a un valore di "***select***", chiamato anche "segnale di controllo".
___
La forma più basilare di *multiplexer* è il cosiddetto "**2:1 *multiplexer***", che presenta due *input* (*D₀* e *D₁*), un valore di *select* (*S*) e un valore di *output* (*Y*). Di seguito, la rappresentazione grafica di un 2:1 *multiplexer* generico e la sua tavola di verità:
![[mux.png]]
Come si può notare dalla tavola di verità, quando il valore *S* sarà uguale a 0, l'*output* corrisponderà all'*input* *D₀*, mentre quando *S* sarà uguale a 1, l'*output* corrisponderà all'*input* *D₁*.

Un 2:1 *multiplexer* può essere costruito con un circuito in forma SOP, o anche utilizzando dei *tristate buffer*, come si può vedere di seguito:

![[mux_sop.png]]
![[mux_tristate.png]]
___
Esistono anche *multiplexer* più grandi, che presentano dunque un maggior numero di *input*. Ad esempio, un **4:1 *multiplexer*** presenta 4 *input* (*D₀*, *D₁*, *D₂* e *D₃*), due valori di *select* (*S₀* e *S₁*) e un valore di *output* (Y). Di seguito, la rappresentazione grafica di un 4:1 *multiplexer* generico:

![[mux4.png]]

Oltre a essere costruibile mediante circuiti in forma SOP o contenenti *tristate buffers*, un *multiplexer* con più di due *input* come il 4:1 *multiplexer* può essere costruito anche utilizzando molteplici 2:1 *multiplexer*:

![[mux4_with_mux2.png]]

Si incontreranno, probabilmente, anche *multiplexer* più complessi, come l'8:1 *multiplexer*, il 16:1 *multiplexer* e così via. In generale, sarà utile ricordare che un *mux* potrà avere 2ⁱ *input* e un numero di valori *select* pari a log₂*i*.