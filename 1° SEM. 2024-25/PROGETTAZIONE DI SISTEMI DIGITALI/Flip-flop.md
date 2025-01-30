In questa sezione, analizzeremo principalmente quattro tipi di ***flip-flop*** o di componenti derivate da essi:
1. il ***D flip-flop***;
2. il **registro**;
3. l'***enabled flip-flop***;
4. il ***resettable flip-flop***.
___
Un ***D flip-flop*** consiste, sostanzialmente, in due *[[Latch|D latch]]* collegati, controllati da *CLK* complementari. I due *latch* utilizzati vengono chiamati rispettivamente L1 e L2, e il nodo che li collega viene generalmente indicato con N1. Graficamente, un *D flip-flop* viene rappresentato con il diagramma seguente:

![[d_flipflop.png]]

e può essere riassunto in maniera compatta con il simbolo seguente:

![[d_flipflop_symbol.png]]

Ancora, se l'*output* *Q'* è trascurabile, la simbologia può essere ancora più condensata:

![[d_flipflop_symbolcondensed.png]]

In un *D flip-flop*, il *latch* L1 (ossia, generalmente, quello collegato all'*input* *D*) viene detto "*master*", mentre il *latch* L2 (ossia, generalmente, quello il cui *input* è collegato al nodo N1) viene detto "*slave*".

Quando *CLK = 0*, il *master* è trasparente e lo *slave* è opaco: dunque, l'*input* *D* viene propagato al nodo N1 attraverso il *latch* L1; quando *CLK = 1*, il *master* è opaco e lo *slave* è trasparente: dunque, il valore propagato al nodo N1 viene propagato all'*output* *Q*, mentre N1 "perde il collegamento" con l'*input* *D*. Questo meccanismo implica che il valore assunto da *D* immediatamente prima del passaggio di *CLK* da 0 a 1 viene trasmesso a *Q* immediatamente dopo tale passaggio; invece, in qualsiasi altro momento, *Q* mantiene il suo valore precedente.

Si può riassumere il funzionamento appena spiegato affermando che **un *D flip-flop* trasmette *D* a *Q* durante il *rising edge* di *CLK*, e mantiene il suo stato precedente in qualsiasi altro momento**. 

Il *rising edge* di *CLK*, per comodità, viene spesso detto semplicemente "*clock edge*". Il *D flip-flop* in sè, inoltre, può essere chiamato anche "*master-slave flip-flop*", "*edge-triggered flip-flop*" o "*positive edge-triggered flip-flop*".
___
Un **registro** a *N* bit consiste in un gruppo di *N* *flip-flop* che condividono lo stesso segnale *CLK*, in modo tale che tutti i bit di *output* del registro vengano aggiornati sempre nello stesso momento. Di seguito, ad esempio, il diagramma di un registro a 4 bit:

![[register_example.png]]

Vediamo, inoltre, che tale rappresentazione può essere compattata nella seguente:

![[register_example_symbol.png]]
___
Un ***enabled flip-flop*** consiste nell'unione tra un classico *D flip-flop* e un nuovo *input* chiamato *ENABLE* (o *EN*), che determina se l'informazione fornita dall'*input* *D* viene o meno trasmessa attraverso il circuito durante il *clock edge*: dunque, quando *EN* = 1, l'*enabled flip-flop* si comporta come un normalissimo *D flip-flop*, mentre quando *EN = 0*, il circuito ignora completamente il valore di *CLK* e mantiene il suo stato precedente. Un *enabled flip-flop* può essere implementato in vari modi, tra cui:

![[enabled_flipflop.png]]

È possibile riassumere una qualsiasi di queste implementazioni con il seguente simbolo:

![[enabled_flipflop_symbol.png]]

Potrebbe tornare utile precisare che, nella seconda possibile implementazione, si deve fare attenzione a non variare il valore di *EN* nel momento in cui *CLK = 1*, in quanto fare ciò potrebbe causare un *glitch*. È saggio, generalmente, evitare di implementare logica che coinvolga il segnale *CLK*, in quanto potrebbe spesso portare a problematiche del genere e quasi sicuramente a errori di tempo.
___
Un ***resettable flip-flop*** è simile a un *enabled flip-flop*, nel senso che anch'esso aggiunge un nuovo *input* a un *D flip-flop* di partenza; in questo caso, però, l'*input* in questione è *RESET*, ed esso si trova a stretto contatto con *D* piuttosto che con *CLK*. Infatti, quando *RESET = 0*, il circuito si comporta come un normalissimo *D flip-flop*; quando, invece, *RESET = 1*, il circuito ignora il valore di *D* e l'*output* *Q* viene forzato a 0. Graficamente, un *resettable flip-flop* può essere implementato nel modo seguente:

![[resettable_flipflop.png]]

e condensato mediante la seguente simbologia:

![[resettable_flipflop_symbols.png]]

Circuiti del genere possono venire categorizzati in:
- **sincroni**, che possono essere resettati solo in concomitanza con il *clock edge*;
- **asincroni**, che si resettano non appena *RESET = 1*, indipendentemente dal valore di *CLK*.

In particolare, l'implementazione fornita prima mostra un *resettable flip-flop* sincrono.