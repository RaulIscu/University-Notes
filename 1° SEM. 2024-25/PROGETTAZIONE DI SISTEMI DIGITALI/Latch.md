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

Possiamo riassumere i casi analizzati finora in una tavola di verità, che ci aiuterà a spiegare meglio il funzionamento dell'*SR latch*:

![[sr_latch_truth.png]]

Ripensando al significato delle lettere S e R, comprendiamo che "settare" un valore vuol dire renderlo *TRUE*, mentre "resettarlo" vuol dire riportarlo a *FALSE*. Sapendo ciò, notiamo che se R = 1 l'*output* Q sarà uguale a 0 (*FALSE*), mentre se S = 1 e R = 0, l'*output* Q sarà uguale a 1 (*TRUE*); il caso in cui entrambi gli *input* S e R sono uguali a 1, in realtà, non ha concretamente senso, in quanto implica che il circuito in questione venga settato e resettato allo stesso tempo; se, invece, nessun *input* viene attivato, il *latch* ricorda il suo stato precedente, e si attiene ad esso.

Solitamente, un *SR latch* viene costruito con le porte *NOR* che abbiamo visto, ma esso può potenzialmente essere costruito in vari altri modi. In generale, qualsiasi circuito che rispetti la tavola di verità appena analizzata può essere definito *SR latch*, e graficamente rappresentato con il seguente simbolo:

![[sr_latch_symbol.png]]

___

