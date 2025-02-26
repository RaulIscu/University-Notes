Vari [[Circuiti sequenziali|circuiti sequenziali sincroni]] possono essere rappresentati sottoforma di ***FSM***, o ***finite state machines***, chiamate in questo modo in quanto un circuito con *i* registri può trovarsi in uno di un numero finito (più precisamente, 2*ⁱ*) di stati distinti.

Una *FSM* ha un numero *M* di *input*, un numero *N* di *output* e un numero *k* di "bit di stato". Oltre a ciò, include sempre un segnale *CLK* ed, eventualmente, un segnale di *RESET*. A livello minimo, un'implementazione di una *FSM* include due blocchi di logica combinatoria, indicati come "***next state logic***" e "***output logic***", e un [[Flip-flop|registro]] che conserva lo stato della macchina. In corrispondenza di ogni *clock edge*, la *FSM* avanza al suo *next state*, che viene ottenuto in base al suo *current state* e agli *input* attuali.

Si possono distinguere principalmente due categorie in cui si dividono le *FSM*:
- le "**macchine di Moore**", in cui gli *output* dipendono esclusivamente dal *current state* della macchina;
- le "**macchine di Mealy**", in cui gli *output* dipendono sia dal *current state* della macchina che dagli *input* attuali.

Per comprendere meglio la differenza tra queste due categorie, si possono confrontare le loro implementazioni. Vediamo, innanzitutto, un esempio generico di macchina di Moore:

![[moore.png]]

Ora, ecco un esempio generico di macchina di Mealy:

![[mealy.png]]
___
Introduciamo un esempio concreto per illustrare al meglio come progettare una *FSM* e la sua utilità.

Supponiamo di voler progettare il meccanismo che detta il funzionamento di un sistema di semafori in un incrocio tra due strade, che chiamaremo per comodità "Academic Avenue" e "Bravado Boulevard". Si possono, innanzitutto, installare due sensori del traffico, che indicheremo con T*a* e T*b*, rispettivamente su Academic Ave. e su Bravado Blvd., in modo che ognuno di questi sensori ritorni un valore *TRUE* se rileva delle persone e *FALSE* se invece non ne rileva. Si procede, a questo punto, a installare dei semafori, che indicheremo con L*a* e L*b*, che ricevono *input* che specificano se il semaforo in questione debba essere verde, giallo o rosso, in modo da controllare il traffico tra le due strade. Di seguito, una rappresentazione grafica della situazione:

![[fsm_example.png]]

Una *FSM* che controlli una situazione del genere dovrà quindi avere due *input* (T*a* e T*b*) e due *output* (L*a* e L*b*). Per questa situazione, supponiamo di inserire un *CLK* con un periodo di 5 secondi (il che vuol dire che passano 5 secondi tra ogni *clock edge*, non tra due variazioni di valore di *CLK*): dunque, ad ogni *clock edge*, i semafori sono in grado di cambiare in base ai dati rilevati dai sensori T*a* e T*b*. Per completezza, si può inserire anche un segnale di *RESET*, in modo da poter distinguere con certezza uno stato iniziale per la macchina. Possiamo riassumere questa *FSM* con la seguente simbologia:

![[fsm_example_symbol.png]]

A questo punto, bisogna creare un "**diagramma di transizione tra stati**" relativo a questa *FSM*, in modo da poter indicare tutti i possibili stati della macchina e il modo in avviene la transizione tra di essi. 

Partiamo dallo stato "iniziale", ossia quello che si ha quando si resetta la macchina mediante il segnale *RESET*: scegliamo che questo stato restituisca come *output* i semafori L*a* verdi e i semafori L*b* rossi. A questo punto, si avvia il ciclo del *CLK*, e ogni 5 secondi i sensori T*a* e T*b* controlleranno la situazione. A partire dallo stato iniziale (indichiamo questo stato con **S0**), finché continua ad esserci traffico su Academic Ave., ed esso continua ad essere rilevato da T*a*, lo stato resta invariato. Invece, quando T*a* smetterà di rilevare traffico sulla sua strada, L*a* diventerà giallo per i successivi 5 secondi (indichiamo questo stato con **S1**); non appena questi 5 secondi saranno passati, e si arriverà al prossimo *clock edge*, L*a* diventerà rosso mentre L*b* diventerà verde (indichiamo questo stato con **S2**). Analogamente, finché continua ad esserci traffico su Bravado Blvd., ed esso continua ad essere rilevato da T*b*, lo stato resta invariato. Invece, quanto T*b* smetterà di rilevare traffico sulla sua strada, L*b* diventerà giallo per i successivi 5 secondi (indichiamo questo stato con **S3**); non appena questi 5 secondi saranno passati, e si arriverà al prossimo *clock edge*, L*b* diventerà rosso mentre L*a* diventerà verde, tornando così a S0. Dunque, la *FSM* potrà oscillare tra 4 possibili stati, e il risultante diagramma di transizione è il seguente:

![[fsm_example_std.png]]

In generale, in un diagramma di transizione tra stati, i vari cerchi rappresentano i vari possibili stati in cui può trovarsi l'*FSM*, mentre gli archi che collegano due stati rappresentano le transizioni tra di essi (l'arco di *RESET*, proveniente dal nulla, sta a indicare che la macchina entra nello stato S0 ogni qualvolta essa venga resettata, indifferentemente dallo stato in cui si trovava precedentemente). Se un singolo stato presenta più di un arco uscente da esso, ognuno di questi verrà associato all'*input* che provoca quella transizione in particolare; al contrario, se un singolo stato presenta un solo arco uscente da esso, tale transizione avviene a prescindere dal valore degli *input*. Gli *output* dell'*FSM* in uno stato ben preciso sono appuntati all'interno dello stato in questione.

A partire dal diagramma, poi, si può ottenere una "**tabella di transizione tra stati**", che indichi, per ogni *current state* S e combinazione di *input*, quale dovrebbe essere il *next state* S'. Analogamente alle tabelle di verità della [[Circuiti combinatori|logica combinatoria]], anche in una tabella di transizione tra stati si potranno inserire dei *don't care* (*X*) in corrispondenza a determinati *input* quando questi non influenzano il *next state*. Per il nostro esempio, si ottiene la seguente tabella:

![[fsm_example_table.png]]

A questo punto, è importante che gli stati e i possibili *output* vengano assegnati a delle "**codifiche**", in modo da uscire dal piano astratto in cui abbiamo progettato l'*FSM* finora e cominciare a progettare l'effettivo circuito che determinerà il suo funzionamento. Per il nostro esempio, possiamo codificare stati e *output* nel modo seguente:

![[fsm_example_encodings.png]]

Combinando la tabella creata inizialmente con le codifiche che abbiamo assegnato ai vari stati, è possibile ottenere una nuova tabella di transizione tra stati, che diventa ora una vera e propria tavola di verità per il *next state* della nostra *FSM*, che definisce quest'ultimo in funzione del *current state* e degli *input*:

![[fsm_example_encodedtable.png]]

A partire da questa tabella, è facile ottenere delle equazioni booleane (ad esempio in forma SOP) per i bit che codificano il *next state*:
$$s'_1 = S_1'S_0 + S_1S_0'T_B' + S_1S_0'T_B = S_1 ⊕S_0$$
$$s'_0 = S_1'S_0'T_A' + S_1S_0'T_B'$$
È possibile, a questo punto, creare anche una tabella per gli *output* codificati in corrispondenza allo stato in cui si verificano:

![[fsm_example_outputtable.png]]

Si possono ricavare, anche qui, delle equazioni booleane per i bit che codificano gli *output*:
$$L_A₁ = S_1$$
$$L_A₀ = S_1'S_0$$
$$L_B₁ = S_1'$$
$$L_B₀ = S_1S_0$$
A questo punto, avendo tutti i dati necessari impostati nel migliore dei modi, sarà possibile progettare concretamente una macchina di Moore per il sistema considerato (si è scelta una macchina di Moore in quanto gli *output* dipendono solo dal *current state* della macchina).

Innanzitutto, per conservare lo stato della macchina, si implementa un registro a 2 bit, che ogni *clock edge* trasmette il *next state* S' al *current state* S; inoltre, tale registro è anche dotato di un segnale di *RESET*. A questo punto, si procede a ideare il blocco della *next state logic*, basato sulle equazioni booleane che definiscono il *next state*; infine, si crea anche il blocco dell'*output logic*, basato invece sulle equazioni booleane che definiscono gli *output*. Seguendo questi passaggi, il circuito completo, e dunque l'*FSM*, può essere implementato nel modo seguente:

![[fsm_example_implementation.png]]

Possiamo analizzare un diagramma di tempo, che include le forme d'onda di *CLK*, *RESET*, T*a* e T*b*, L*a* e L*b*, il *next state* S' e il *current state* S, per vedere concretamente come l'*FSM* entra nei vari stati:

![[fsm_example_timing.png]]
___
Nell'esempio precedente, le **codifiche** dei vari stati dell'*FSM* sono state scelte in maniera arbitraria, e ovviamente una scelta diversa in questo passaggio avrebbe determinato un circuito diverso. Risulta quindi naturale chiedersi quale sia la codifica che consente di avere il minor numero di porte logiche, o il *delay* minore, all'interno del circuito.

In generale, non è possibile stabilire delle regole universali che permettano di ottenere sempre la codifica più efficiente; tuttavia, spesso si può preferire una codifica piuttosto che un'altra analizzando al meglio la tabella degli stati, cercando di fare in modo che **stati o *output* collegati condividano il maggior numero di bit possibile**.

Una decisione importante da prendere nella codifica degli stati è la scelta tra due tipi di codifica:
- la **codifica binaria**;
- la **codifica *one-hot***.

Utilizzando la codifica binaria, come nell'esempio precedente, ogni stato è rappresentato da un numero binario; sfruttando questo sistema, per un sistema con *k* stati sono sufficienti log₂*k* bit di stato.

Utilizzando, invece, la codifica *one-hot*, ogni stato viene associato a un singolo bit di stato (viene chiamata *one-hot* proprio perché un solo bit alla volta può essere "hot", o 1). Ad esempio, un'*FSM* dotata di 3 stati codificati *one-hot* presenterà le codifiche 001, 010 e 100.

In una codifica *one-hot*, ogni bit, naturalmente, viene conservato in un singolo *flip-flop*, dunque tendenzialmente essa richiede un maggior numero di *flip-flop* rispetto alla codifica binaria. Allo stesso tempo, però, spesso utilizzare una codifica *one-hot* semplifica i blocchi di *next state logic* e di *output logic*. Quindi, scegliere l'una o l'altra dipenderà sempre dalla *FSM* con cui si sta lavorando in quel momento.

Relativamente alla codifica *one-hot*, è possibile anche scegliere una sua variante, ossia la codifica ***one-cold***: come suggerisce il nome, essa funziona in maniera analoga alla *one-hot* con la differenza che un solo bit alla volta può essere "cold", o 0.
___
L'esempio che abbiamo utilizzato prima per rappresentare il funzionamento delle *FSM* ha portato alla creazione di una macchina di Moore, in cui gli *output* dipendono esclusivamente dallo stato della macchina; per questo motivo, essi potevano facilmente essere appuntati all'interno dello stato nel quale si verificavano.

Il discorso cambia quando si trattano le **macchine di Mealy**, ossia delle *FSM* in cui gli *output* non dipendono solo dallo stato ma anche dagli *input* correnti. Per questa particolarità, nei diagrammi di transizione tra stati delle macchine di Mealy gli *output* non vengono appuntati all'interno degli stati, ma sull'arco che indica la transizione tra di essi, abbinati agli *input* che li provocano.

Un esempio di diagramma di transizione tra stati di una macchina di Mealy può essere il seguente:

![[mealy_example_std.png]]

In vari casi, implementare una macchina di Mealy risulta essere più vantaggioso rispetto a una macchina di Moore, in quanto generalmente, per lo stesso funzionamento, una macchina di Mealy presenta meno stati. È possibile notarlo immediatamente implementando lo stesso funzionamento illustrato dal diagramma precedente con una macchina di Moore, che presenterà 3 stati invece di 2:

![[mealy_example_moorestd.png]]

Inoltre, notiamo che, per questo esempio, la macchina di Mealy è più conveniente anche rispetto al numero di porte logiche utilizzate nell'implementazione dei circuiti. Di seguito il confronto tra la macchina di Moore (a) e la macchina di Mealy (b):

![[mealymoore_compare.png]]
___
Progettare un'*FSM* complessa risulta più facile se si riesce a suddividerla in macchine più semplici, in modo che l'*output* di alcune diventi l'*input* di altre. Questo procedimento viene chiamato anche "**fattorizzazione**" di una *FSM*.

Vediamo un esempio di fattorizzazione ampliando l'esempio iniziale. Supponiamo, a partire dalla stessa situazione a cui eravamo rimasti, di voler aggiungere una "modalità parata" al sistema di semafori, che quando attivata mantenga verdi i semafori su Bravado Blvd. (L*b*) e rossi quelli su Academic Ave. (L*a*), in modo da lasciar fluire senza problemi la parata su Bravado Blvd. fino al suo termine.

Per aggiungere questa funzionalità, occorrerà considerare due nuovi *input*, uno che faccia entrare il sistema in modalità parata (chiameremo *P* questo *input*), e un altro che faccia tornare il sistema al suo normale funzionamento (chiameremo *R* questo *input*). Dunque, quando il sistema entra in modalità parata, la macchina procede nella sua sequenza normale finché le luci L*b* non diventano verdi, e rimane in questo stato finché il sistema non esce dalla modalità parata.

È possibile implementare il tutto in una sola *FSM* più grande e complessa, come la seguente:

![[fsm_factoring_example.png]]

che, per quanto funzionante, risulta notevolmente più contorta e difficile da progettare e analizzare. In alternativa, è possibile operare una fattorizzazione in due *FSM* più semplici; fare ciò risulterà in circuiti con meno porte logiche, in un minor numero di stati da considerare, e generalmente in un sistema molto più intuitivo. Per il nostro esempio, una soluzione che coinvolge una fattorizzazione può essere la seguente:

![[fsm_factoring_example1.png]]
___
Se si vuole ottenere il diagramma di transizione tra stati di una *FSM* a partire dal circuito che detta il suo funzionamento, converrà seguire i seguenti passaggi:
1. analizzare il circuito, individuando i vari *input*, *output* e bit di stato;
2. ottenere equazioni booleane relative al *next state* e agli *output*;
3. creare delle tabelle per *next state* e *output*, e semplificare la tabella di stati per eliminare stati irraggiungibili;
4. codificare ogni stato valido e ogni *output*, e assegnare dei nomi con cui riscrivere le tabelle;
5. disegnare il diagramma di transizione tra stati della *FSM*.

Oltre a questi passaggi, può essere utile riassumere il funzionamento dell'*FSM* a parole, specificando cosa essa debba fare e in corrispondenza a quali eventi, in modo da avere un quadro più chiaro di come procedere.
___
In generale, invece, possiamo delineare un percorso di passaggi da attraversare quando si vuole **progettare una qualsiasi *FSM***. Questi passaggi sono:
6. identificare gli *input* e gli *output* della macchina;
7. abbozzare un diagramma di transizione tra stati;
8. se si vuole implementare una macchina di Moore, creare una tabella di transizione tra stati e una tabella per gli *output*; se si vuole implementare una macchina di Mealy, creare una tabella combinata per stati e *output*;
9. codificare stati e *output* della macchina;
10. ottenere equazioni booleane relative al *next state* e agli *output*;
11. progettare e implementare il circuito che detterà il funzionamento dell'*FSM*.