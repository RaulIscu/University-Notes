Come accennato nell'introduzione dei [[Circuiti sequenziali|circuiti sequenzial sincroni]], quando il *CLK* passa da 0 a 1, gli *output* potranno cominciare a cambiare dopo un tempo **t*ccq***, e dovranno essersi stabilizzati sul loro nuovo valore entro un tempo **t*pcq***. Questi due valori rappresentano rispettivamente il più piccolo *delay* possibile e il più grande *delay* possibile per il circuito in questione.

Per permettere al circuito di trasmettere correttamente il valore degli *input* agli *output*, gli *input* dovranno essersi stabilizzati almeno un tempo **t*setup*** (o ***setup time***) prima del *clock edge*, e dovranno rimanere stabili almeno per un tempo **t*hold*** (o ***hold time***) dopo il *clock edge*. La somma tra questi due tempi di un determinato circuito corrisponde al suo ***aperture time***, e rappresenta il tempo totale in cui è necessario che gli *input* rimangano stabili. Stabilendo queste restrizioni, possiamo garantire che il circuito con cui stiamo lavorando manipola e trasmette *input* solo ed esclusivamente quando essi non stanno cambiando.
___
Il **periodo di *CLK***, indicato con **T*c***, è il tempo che intercorre tra due *clock edge* consecutivi, ossia tra due *rising edge* consecutivi di un segnale *CLK* ciclico. Il reciproco di T*c*, ossia:
$$f_c = 1/T_c$$
rappresenta invece la **frequenza di *CLK***, misurata in **hertz** (**Hz**), o cicli al secondo. Mantenendo identiche tutte le altre caratteristiche di un circuito sequenziale, aumentarne la frequenza di *CLK* incrementa la quantità di lavoro che tale circuito può svolgere in una determinata unità di tempo.

Supponiamo di avere un circuito sequenziale sincrono arbitrario, come il seguente:

![[clkperiod_example.png]]

e di volerne calcolare il periodo di *CLK*. Analizzando il circuito, capiamo che al *clock edge* il [[Flip-flop|registro]] R1 produce gli *output* *Q1*, che vengono manipolati da un blocco di [[Circuiti combinatori|logica combinatoria]] che restituirà *D2*, segnali che diventeranno poi gli *input* del registro R2. Il diagramma di tempo che descrive questo funzionamento è il seguente:

![[clkperiod_example1.png]]

Da tale diagramma, è facile visualizzare come gli *output* delle varie componenti del circuito possono cominciare a variare dopo un determinato *contamination delay* (rappresentato dalle frecce grigie) e dovranno necessariamente essersi ristabilizzati dopo un determinato *propagation delay* (rappresentato dalle frecce arancioni).

Cominciamo a risolvere il nostro problema, analizzando innanzitutto i *propagation delay* del circuito, in relazione al *setup time* del registro R2:

![[clkperiod_example2.png]]

Notiamo che, per poter soddisfare un *setup time* sufficiente per R2, *D2* deve necessariamente stabilizzarsi prima del *setup time* relativo al prossimo *clock edge*. Possiamo quindi affermare che il periodo di *CLK* deve essere maggiore o uguale alla somma tra i vari *propagation delay* e il *setup time*:
$$T_c ≥ tpcq + tpd + tsetup$$
Solitamente, il *propagation delay* *CLK-to-Q* e il *setup time* di un *flip-flop* vengono forniti dal produttore dello stesso. Risulta utile, dunque, esplicitare nella disequazione appena ottenuta il *propagation delay* della logica combinatoria, che spesso è l'unica variabile sotto il controllo del progettista del circuito considerato:
$$tpd ≤ T_c - (tpcq + tsetup)$$
Il termine tra parentesi viene chiamato anche "***sequencing overhead***": idealmente, l'intero periodo di *CLK* T*c* sarebbe a disposizione per essere occupato da t*pd*, tuttavia questo tempo viene concretamente ridotto dal *sequencing overhead*. La disequazione appena vista, dunque, rappresenta il "*setup time constraint*", o "*max-delay constraint*", in quanto dipende dal *setup time* e limita il *propagation delay* della logica combinatoria del circuito. Se t*pd* è troppo grande, il segnale *D2* potrebbe non avere sufficiente tempo per stabilizzarsi prima che esso venga richiesto e utilizzato da R2; ciò porterebbe a un valore illegale o semplicemente sbagliato, che causerebbe un malfunzionamento del circuito. In caso si incorra in un problema del genere, si dovrà aumentare il periodo di *CLK* o riprogettare la logica combinatoria più efficientemente.

Il registro R2, oltre a un *setup time*, presenta ovviamente anche un *hold time*, e di conseguenza un "*hold time constraint*". Infatti, il suo *input* *D2* non deve cambiare prima di un tempo t*hold* dopo il *clock edge*. Per comprendere meglio la situazione, analizziamo i *contamination delay* del circuito, in relazione all'*hold time* di R2:

![[clkperiod_example3.png]]

Dal diagramma, notiamo che *D2* potrebbe cambiare a partire da un tempo (t*ccq* + t*cd*) dopo il *clock edge*; per assicurarci del buon funzionamento del circuito, dunque, bisogna porre che:
$$tccq + tcd ≥ thold$$
Anche in questo caso, t*ccq* e t*hold* sono valori solitamente forniti dal produttore del *flip-flop*, e si può quindi riscrivere la disequazione come:
$$tcd ≥ thold - tccq$$
fornendoci così l'*hold time constraint*, o "*min-delay constraint*", del registro R2. Visto che questa disequazione vale sempre, a prescindere dalla logica combinatoria coinvolta nel circuito, possiamo affermare che essa valga anche quando non vi è alcuna logica combinatoria, e dunque quando t*cd* = 0. In tal caso, si ottiene che:
$$thold ≤ tccq$$
ossia che un *flip-flop* affidabile deve necessariamente avere un *hold time* minore del suo *contamination delay*. Spesso, questi circuiti sono progettati in modo tale che t*hold* = 0, in modo da soddisfare sempre questa disequazione. In generale, tuttavia, questa restrizione è molto importante, ed è anche più difficile modificare un circuito in modo che la rispetti. Infatti, l'unica soluzione sarebbe aumentare il *contamination delay*, che implica riprogettare il circuito..

L'*hold time constraint* e il *setup time constraint* impongono un limite minimo e un limite massimo ai *delay* della logica combinatoria di un circuito sequenziale sincrono.
___
Finora, si è sempre supposto che il segnale *CLK* raggiunga tutti i registri di un circuito nello stesso momento; concretamente, però, questo è impossibile, e vi sarà sempre uno sbalzo (per quanto piccolo) tra i tempi di arrivo. Questo sbalzo viene chiamato "***clock skew***".

Ci sono moltissime situazioni in cui può verificarsi del *clock skew*: i cavi che collegano *CLK* con i vari registri possono essere di lunghezze diverse; il *CLK* può essere coinvolto in logica combinatoria (come negli *[[Flip-flop|enabled flip-flop]]*) prima di arrivare ad alcuni ma non a tutti i registri; e così via.

