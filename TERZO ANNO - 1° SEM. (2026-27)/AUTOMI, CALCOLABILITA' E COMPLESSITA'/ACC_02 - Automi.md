Per poter affrontare nel dettaglio la teoria della computazione, partiamo dal modellare ciò su cui tale computazione avviene, ossia un computer. Naturalmente, analizzare teoricamente un computer effettivo risulterebbe fin troppo complesso, dunque in questi contesti si preferisce utilizzare dei cosiddetti "**modelli di computazione**". Un modello di computazione rappresenta, sostanzialmente, un'astrazione di un calcolatore, che può essere accurata in alcuni aspetti e meno in altri; per questo motivo, durante questo corso si vedranno diversi modelli di computazione, a seconda delle caratteristiche su cui ci si vorrà concentrare.

Il primo modello di computazione che andremo ad analizzare, il più semplice, è il cosiddetto "**automa finito**", chiamato anche "**macchina a stati finiti**".

## Cos'è un automa finito?

Un **automa finito** può essere utilizzato per **modellare un semplice computer** con una **quantità estremamente limitata di memoria**. 

Per comprendere al meglio questo concetto, vediamo un **esempio concreto** prima di arrivare alla definizione formale: supponiamo, ad esempio, di avere a che fare con il **sistema di controllo di una porta automatica di sola entrata**. Il suo compito è di aprirsi quando rileva una persona che sta per attraversarne la soglia, e di rimanere aperta abbastanza da permettere a tale persona di arrivare dall'altra parte. Per svolgere queste due mansioni, saranno necessari due sensori, per cui possiamo schematizzare questo esempio nel modo seguente:

![[automa_esempio.png]]

Ora, naturalmente il sistema che stiamo considerando può trovarsi solamente in uno di **due stati**: **`OPEN`** quando la porta è aperta, e **`CLOSED`** quando la porta è chiusa. Invece, per quanto riguarda i possibili **input** del sistema, ossia ciò che viene rilevato dai due sensori, essi sono 4: **`FRONT`** quando è rilevata una persona dal sensore anteriore, **`REAR`** quando è rilevata dal sensore posteriore, **`BOTH`** quando è rilevata da entrambi, e **`NEITHER`** quando nessuno dei due sensori rileva nulla. Il sistema di controllo **passa da uno stato all'altro in base all'input che riceve e allo stato in cui si trova quando lo riceve**: ad esempio, se si trova nello stato `CLOSED` e riceve input `NEITHER` o `REAR` rimane in tale stato; invece, se riceve l'input `FRONT`, la porta si apre e il sistema passa nello stato `OPEN`; se, poi, nello stato `OPEN` si riceve l'input `NEITHER`, la porta si chiuderà e si passerà allo stato `CLOSED`; e così via. Queste transizioni possono essere riassunte in quella che chiamiamo "**tabella delle transizioni di stato**", che riassume e schematizza tutti i possibili comportamenti del sistema in base a stato e input. Ad esempio, per l'esempio appena visto, una possibile tabella delle transizioni di stato è la seguente:

![[automa_esempio1.png]]

Ancora, tale sistema può essere formalizzato in modo più chiaro e immediato con un "**diagramma di stato**", come il seguente:

![[automa_esempio2.png]]

In base alle premesse appena fatte, se ad esempio il sistema ricevesse la sequenza di input `FRONT`-`REAR`-`NEITHER`-`FRONT`-`BOTH`-`NEITHER`-`REAR`-`NEITHER`, esso passerebbe attraverso la sequenza di stati `CLOSED`-`OPEN`-`OPEN`-`CLOSED`-`OPEN`-`OPEN`-`CLOSED`-`CLOSED`-`CLOSED`.

Ora, a partire da questo esempio, vediamo di generalizzare e di arrivare eventualmente a una definizione di automa finito. Prendiamo un altro automa generico, chiamato $M_{1}$ e definito dal seguente diagramma di stato:

![[automa_esempio3.png]]

I 3 nodi del diagramma sono detti "**stati**", e in questo esempio sono etichettati come $q_{1}$, $q_{2}$ e $q_{3}$. Tra questi, possiamo identificare $q_{1}$ come lo "**stato iniziale**" dell'automa, dato che presenta un arco entrante in esso ma non uscente da altri stati; al tempo stesso, possiamo identificare $q_{2}$ come lo "**stato accettante**", o "**stato finale**", dell'automa, dato che presenta un contorno doppio. Formalmente, infine, gli archi tra i vari stati si dicono "**transizioni**", e i valori annessi a ciascuna transizione sono i **valori di input** che provocano tale transizione.

In generale, **un automa finito prende in input una sequenza di simboli**, simboli che devono far parte di un **alfabeto $\Sigma$** (in questo esempio, l'alfabeto è $\Sigma=\{0,\,1\}$), e tali simboli vengono **letti uno alla volta, da sinistra verso destra**. Sono proprio tali simboli che, come nell'esempio della porta automatica, determinano le transizioni di stato dell'automa considerato. Ad esempio, se l'automa $M_{1}$ riceve in input la sequenza `1101`, avvengono le seguenti transizioni:
1. l'automa parte dallo stato iniziale $q_{1}$;
2. l'automa legge `1`, dunque effettua la transizione allo stato $q_{2}$;
3. l'automa legge `1`, dunque rimane nello stato $q_{2}$;
4. l'automa legge `0`, dunque effettua la transizione allo stato $q_{3}$;
5. l'automa legge `1`, dunque effettua la transizione allo stato $q_{2}$.

Ora, **tipicamente un automa produce un output**; in questo esempio, per semplicità, supponiamo che gli output possibili siano solamente due, `True` e `False`. L'output restituito dall'automa **dipende esclusivamente dall'ultimo simbolo letto in input**: se l'ultimo simbolo di input porta l'automa a trovarsi in uno stato finale, allora l'automa restituirà `True`, altrimenti restituirà `False`. Elaborando, ad esempio, sempre l'input `1101`, l'automa $M_{1}$ restituirà `True`, dato che al termine dell'elaborazione si troverà nello stato $q_{2}$. Un'analisi più approfondita dell'automa $M_{1}$ permette di mostrare che esso accetterà qualsiasi sequenza che termina con $1$, o anche qualsiasi sequenza che termina con un numero pari di $0$ dopo l'ultimo $1$.

Forniamo, a questo punto, una **definizione formale di automa finito**:

> Un **automa finito**, o "**DFA**" (Deterministic Finite-State Automaton), è una tupla $(Q,\,\Sigma,\,\delta,\,q_{0},\,F)$, dove:
> - **$Q$** è un insieme finito chiamato "**insieme degli stati**";
> - **$\Sigma$** è un insieme finito chiamato "**alfabeto**";
> - **$\delta:Q\times\Sigma\to Q$** è una "**funzione di transizione**";
> - **$q_{0}\in Q$** è lo **stato iniziale**;
> - **$F\subseteq Q$** è l'**insieme degli stati accettanti**.

Da questa definizione formale, possiamo anche capire meglio il comportamento di un automa finito in eventuali casi limite: ad esempio, porre $F=\emptyset$ è tranquillamente consentito, il che implica che **un automa finito può non avere stati accettanti**. Chiariamo, a questo punto, anche il concetto di "funzione di transizione", non analizzato concretamente finora: la funzione $\delta$ associa a una tupla costituita da uno stato e un simbolo un nuovo stato, dunque in parole povere **definisce le transizioni dell'automa finito considerato**, specificando esattamente uno stato successivo per ogni possibile combinazione di uno stato e un simbolo di input.

##### Linguaggi

Indicando con $\Sigma^{*}$ l'insieme di tutte le possibili sequenze di lunghezza $k\in\mathbb{N}$ di caratteri contenuti nell'alfabeto $\Sigma$, possiamo dire che **a ogni automa finito corrisponde un "linguaggio" $L\subseteq \Sigma^{*}$**. Ma cos'è un linguaggio? Informalmente, possiamo vedere un linguaggio come l'**insieme di tutte le sequenze di simboli accettate dall'automa $M$ considerato**; indicando con $A$ tale insieme, scriviamo che:
$$L(M)=A$$
In questo contesto, si dice che "**$M$ riconosce $A$**", oppure che "**$M$ accetta $A$**". Nel caso in cui un determinato automa non accetti alcuna sequenza in input, esso riconoscerà comunque un linguaggio $L$, semplicemente con $L(M)=\emptyset$.
___
##### Esempi di automi finiti

Riprendiamo l'automa visto in precedenza, $M_{1}$, che ricordiamo essere definito da tale diagramma di stato:

![[automa_esempio4 1.png]]

Cerchiamo di formalizzare $M_{1}$ sulla base della definizione appena data. Costruiamo dunque la tupla $(Q,\,\Sigma,\,\delta,\,q_{0},\,F)$:
- $Q$ è l'insieme degli stati di $M_{1}$, dunque sarà $\{q_{1},\,q_{2},\,q_{3}\}$;
- $\Sigma$ è l'alfabeto della sequenza presa in input, dunque sarà $\{0,\,1\}$;
- $\delta$ è una funzione definibile, in questo esempio, dalla seguente tabella:

|         | 0       | 1       |
| ------- | ------- | ------- |
| $q_{1}$ | $q_{1}$ | $q_{2}$ |
| $q_{2}$ | $q_{3}$ | $q_{2}$ |
| $q_{3}$ | $q_{2}$ | $q_{2}$ |

- lo stato iniziale di $M_{1}$ è $q_{1}$;
- l'insieme $F$ è costituito da un solo stato, ossia $\{q_{2}\}$.

Per quanto riguarda il linguaggio riconosciuto da $M_{1}$, esso è:
$$L(M_{1})=\{w\,|\,w\text{ contiene almeno un } 1\text{ e un numero pari di } 0\text{ segue l'ultimo }1\}$$

Andiamo avanti, e vediamo un nuovo esempio $M_{2}$ di automa finito, identificato dal seguente diagramma:

![[automa_esempio4 1.png]]

In questo caso, abbiamo:
- $Q=\{q_{1},\,q_{2}\}$;
- $\Sigma=\{0,\,1\}$;
- $\delta$ è definita dalla seguente tabella:

|         | 0       | 1       |
| ------- | ------- | ------- |
| $q_{1}$ | $q_{1}$ | $q_{2}$ |
| $q_{2}$ | $q_{1}$ | $q_{2}$ |

- lo stato iniziale è $q_{1}$;
- $F=\{q_{2}\}$.

In questo caso, provando vari input, è facile convincersi che $M_{2}$ accetta tutte le sequenze di simboli che terminano con un $1$, il che vuol dire che:
$$L(M_{2})=\{w\,|\,w\text{ termina con un }1\}$$

Passiamo a un altro esempio, con l'automa finito $M_{3}$:

![[automa_esempio5.png]]

Notiamo subito, ad occhio, che $M_{3}$ è quasi identico a $M_{2}$, con la sola eccezione che $F=\{q_{1}\}$, dunque troviamo un caso particolare in cui lo stato iniziale è anche lo stato finale dell'automa. Data questa particolarità, possiamo subito affermare con certezza che $M_{3}$ accetta la stringa vuota $\epsilon$. Oltre a ciò, si può osservare che $M_{3}$ accetta tutte le sequenze che terminano con uno $0$, dunque abbiamo che:
$$L(M_{3})=\{w\,|\,w\text{ è la stringa vuota }\epsilon\text{ oppure termina con uno 0}\}$$

Vediamo un ultimo esempio, con l'automa $M_{4}$:

![[automa_esempio6.png]]

In questo caso, si ha $Q=\{q_{0},\,q_{1},\,q_{2}\}$ e $\Sigma=\{(RESET),\,0,\,1,\,2\}$, con $q_{0}$ come stato iniziale e stato accettante. Seppur possa sembrare particolarmente complessa rispetto agli esempi visti finora, si tratta di un automa che svolge una mansione molto semplice: conserva al suo interno la somma parziale dei simboli che legge in input, modulo $3$ (se $M_{4}$ si trova in $q_{0}$ tale somma vale $0$, se si trova in $q_{1}$ tale somma vale $1$, e così via), e ogni volta che riceve il simbolo $(RESET)$ riporta il conto a $0$. Con questo chiarimento, diventa palese che $M_{4}$ accetta tutte le sequenze che risultano in una somma pari a $0\text{ mod }3$, ossia in una somma che è multipla di $3$.
___
#####  

[pag. 34]
___