In questa sezione, analizzeremo principalmente due tipi di ***latch***:
1. l'***SR latch***;
2. il ***D latch***.
___
L'***SR latch*** è composto da due porte *NOR* *cross-coupled*. Tale circuito presenta due *input* (S e R, che stanno per *set* e *reset* e danno il nome al *latch*) e due *output* (Q e il suo complemento). Graficamente, un esempio generico di *SR latch* è il seguente:

![[sr_latch.png]]

Per comprendere meglio il circuito, consideriamo le 4 casistiche possibili in base agli *input* S e R:
- se **R = 1** e **S = 0**, N1 riceve almeno un *input* *TRUE*, quindi produce un *output* Q = 0 che viene preso in *input* da N2; quest'ultimo, ricevendo due *input* *FALSE* produrrà un *output* Q' = 1;
- se **R = 0** e **S = 1**, N2 riceve almeno un *input* *TRUE*, quindi produce un *output* Q' = 0 che viene preso in *input* da N2; quest'ultimo, ricevendo due *input* *FALSE* produrrà un *output* Q = 1;
- se **R = 1** e **S = 1**, sia N1 che N2 ricevono almeno un *input* *TRUE*, quindi entrambi gli *output* Q e Q' saranno uguali a 0;
- se **R = 0** e **S = 0**, ci troviamo apparentemente bloccati, in quanto sia Q che Q' rimangono incerti; tuttavia, sappiamo che l'*output* Q deve risultare o 0 o 1, dunque possiamo ricavare il funzionamento del circuito distinguendo questi due sotto-casi:
	1. se Q = 0, N2 produrrà come *output* Q' = 1, che porterà N1 a restituire invece come *output* Q = 0, rispettando le condizioni iniziali;
	2. se Q = 1, N2 produrrà come *output* Q' = 0, che porterà N1 a restituire invece come *output* Q = 1, rispettando le condizioni iniziali.

I due sotto-casi del quarto e ultimo caso possono essere riassunti supponendo che Q abbia un qualsiasi valore noto precedente a quello corrente. Possiamo chiamare questo valore Q*prev*, ed esso rappresenterà semplicemente la variabile di stato del *latch*. Dunque, in "assenza" di *input*, ossia quando S e R sono uguali a 0, il circuito ricorda il suo stato precedente, dato da Q*prev*, e rimane in esso.

Possiamo riassumere i casi analizzati in una tavola di verità, che ci aiuterà a spiegare meglio il funzionamento dell'*SR latch*:

![[sr_latch_truth.png]]

Ripensando al significato delle lettere S e R, comprendiamo che "settare" un valore vuol dire renderlo *TRUE*, mentre "resettarlo" vuol dire riportarlo a *FALSE*. Sapendo ciò, notiamo che se R = 1 l'*output* Q sarà uguale a 0 (*FALSE*), mentre se S = 1 e R = 0, l'*output* Q sarà uguale a 1 (*TRUE*); il caso in cui entrambi gli *input* S e R sono uguali a 1, in realtà, non ha concretamente senso, in quanto implica che il circuito in questione venga settato e resettato allo stesso tempo; se, invece, nessun *input* viene attivato, il *latch* ricorda il suo stato precedente, e si attiene ad esso.

Solitamente, un *SR latch* viene costruito con le porte *NOR* che abbiamo visto, ma esso può potenzialmente essere costruito in vari altri modi. In generale, qualsiasi circuito che rispetti la tavola di verità appena analizzata può essere definito *SR latch*, e graficamente rappresentato con il seguente simbolo:

![[sr_latch_symbol.png]]

___
L'*SR latch* risulta non ottimale in molte situazioni, proprio per il fatto che il circuito si comporta in maniera anomala nel caso in cui sia *S* che *R* sono attivi; inoltre, ciascuno dei due *input* determina non solo quale sarà lo stato del circuito, ma anche quando questo andrà a cambiare, mentre solitamente è più comodo che queste due incognite vengano risolte separatamente.

È per compensare a questi problemi che viene introdotto il "***D latch***", dove *D* sta per "*Data*". Anche questo circuito presenta due *input*, ossia *D* (che controlla lo stato del *latch*) e *CLK*, che sta per "*clock*" (che controlla quando lo stato del *latch* va a cambiare). Graficamente, un generico *D latch* può essere implementato nel modo seguente:

![[d_latch.png]]

Per comprendere meglio il circuito, consideriamo le casistiche possibili in base agli *input* *D* e *CLK*:
- se ***CLK = 0***, allora *S* = *R* = *0* indipendentemente dal valore di *D*;
- se ***CLK = 1*** e ***D = 1***, allora *S = 1* e *R = 0*;
- se ***CLK = 1*** e ***D = 0***, allora *S* = *0* e *R* = *1*.

Possiamo riassumere i casi analizzati in una tavola di verità, che ci aiuterà a spiegare meglio il funzionamento del *D latch*:

![[d_latch_truth.png]]

Avendo i valori di *S* e *R*, naturalmente, gli *output* Q e Q' verranno determinati in base alla tavola di verità dell'*SR latch*. Si nota, dunque, che se *CLK = 0*, *Q = Qprev* (il circuito, dunque, ricorderà il suo valore precedente); invece, se *CLK = 1*, *Q = D*. Mediante questo meccanismo, il *D latch* evita il caso anomalo dell'attivazione contemporanea di *S* e *R*.

Insomma, in un *D latch*, **l'*input* *CLK* è quello che determina quando l'informazione** (*D*) **entra nel circuito**: per questo, quando *CLK = 1*, il circuito viene detto "**trasparente**", in quanto si comporta come un *[[Porte logiche|BUFFER]]* e trasmette come *output* il valore di *D*; quando, invece, *CLK = 0*, il circuito viene detto "**opaco**", in quanto non lascia passare l'informazione *D* e l'*output* mantiene il suo valore precedente.

In generale, qualsiasi circuito che rispetti la tavola di verità appena analizzata può essere definito *D latch*, e graficamente rappresentato con il seguente simbolo:

![[d_latch_symbol.png]]