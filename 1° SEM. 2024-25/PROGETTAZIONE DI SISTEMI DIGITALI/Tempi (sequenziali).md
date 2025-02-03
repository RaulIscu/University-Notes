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

Ci sono moltissime situazioni in cui può verificarsi del *clock skew*: i cavi che collegano *CLK* con i vari registri possono essere di lunghezze diverse; il *CLK* può essere coinvolto in logica combinatoria (come negli *[[Flip-flop|enabled flip-flop]]*) prima di arrivare ad alcuni ma non a tutti i registri; e così via. Ampliando sull'esempio analizzato finora, possiamo ipotizzare che il segnale *CLK* venga trasferito ai due registri mediante percorsi di lunghezza molto diversa:

![[clkskew_example.png]]

In questo modo, probabilmente il segnale arriverà all'*input* *CLK1* diverso tempo dopo essere arrivato a *CLK2*. Considerando questo fattore, il diagramma di tempo può essere rappresentato in maniera leggermente diversa:

![[clkskew_example1.png]]

in cui la linea più marcata indica il momento più tardivo in cui il segnale *CLK* potrebbe arrivare a uno dei registri, e le altre linee indicano che il segnale potrebbe arrivare fino a un tempo **t*skew*** prima di allora.

Torniamo, considerando il *clock skew*, ad analizzare il *setup time constraint* e l'*hold time constraint* del registro R2 del circuito. Partendo dal *setup time constraint*, nel peggiore dei casi R1 riceverà il segnale *CLK* il più tardi possibile, mentre R2 lo riceverà il prima possibile: una situazione del genere lascerebbe il minor tempo possibile a una qualsiasi informazione per essere trasmessa all'*output* del circuito. Vediamo un diagramma che ci permetta di visualizzare facilmente questa casistica:

![[clkskew_example2.png]]

L'informazione attraversa il registro R1 e il blocco di logica combinatoria, entrando nel nodo D2, e dovrà fare questo percorso e stabilizzarsi prima del *setup time* di R2. Possiamo, quindi, affermare che:
$$T_c ≥ tpcq + tpd + tsetup + tskew$$
ovvero:
$$tpd ≤ T_c - (tpcq + tsetup + tskew)$$

Consideriamo, ora, l'*hold time constraint*. Nel peggiore dei casi, R1 riceverà il segnale *CLK* il prima possibile, mentre R2 lo riceverà il più tardi possibile: una situazione del genere porterebbe una trasmissione molto più veloce dell'informazione, ma bisogna accertarsi che essa non arrivi a R2 prima del suo *hold time*. Vediamo un diagramma che ci permetta di visualizzare facilmente questa casistica:

![[clkskew_example3.png]]

Possiamo, quindi, affermare che:
$$tccq + tcd ≥ thold + tskew$$
ovvero:
$$tcd ≥ thold + tskew - tccq$$
In sostanza, abbiamo visto che il *clock skew* incrementa sia il *setup time* che l'*hold time* di un circuito, ponendo ancora maggiori limitazioni e richieste sull'efficienza della logica combinatoria.
___
Non è sempre possibile garantire che gli *input* di un circuito sequenziale sincrono siano stabili durante il suo *aperture time*, soprattutto se si lavora con circuiti i cui *input* provengono dal mondo esterno. 

Supponiamo, ad esempio, di avere un *flip-flop* il cui *input* *D* è controllato da un pulsante: se il pulsante è premuto, *D = 1*, altrimenti *D = 0*; a questo punto, supponiamo anche che il pulsante venga premuto in momenti casuali rispetto al *clock edge* del *flip-flop*, e analizziamo il comportamento del circuito nelle varie casistiche ottenute. Per fare ciò, lavoriamo su un diagramma di tempo:

![[metastability_example.png]]

Nel caso 1, il pulsante viene premuto molto tempo prima del *clock edge*, dunque il circuito funziona normalmente e *Q = 1*; nel caso 2, il pulsante viene premuto molto tempo dopo il *clock edge*, dunque il *flip-flop* non rileva la variazione dell'*input* e *Q = 0*; cosa succede, però, nel caso 3? Stavolta, il pulsante viene premuto in un momento compreso tra t*setup* prima e t*hold* dopo il *clock edge*: ciò viola una delle regole di base che abbiamo stabilito all'inizio di questa sezione.

In una situazione del genere, l'*output* *Q* del *flip-flop* potrebbe assumere momentaneamente un voltaggio compreso tra 0 e il voltaggio massimo, valore che sarà inevitabilmente illegale. Questo stato viene definito "**stato metastabile**", e nonostante il circuito arriverà, prima o poi, ad avere un *output* accettabile corrispondente a 0 o a 1, il tempo che ci metterà per arrivarci (ossia il **tempo di risoluzione**) è sostanzialmente indefinito. Ogni circuito bistabile presenta uno stato metastabile.

Se l'*input* di un *flip-flop* varia in un momento casuale del ciclo di *CLK*, anche il tempo di risoluzione **t*res*** sarà sostanzialmente casuale; in particolare, se l'*input* varia al di fuori dell'*aperture time*, allora:
$$tres = tpcq$$
Tuttavia, il discorso si complica se l'*input* varia all'interno dell'*aperture time*, come nel caso 3 dell'esempio precedente; in questi casi, infatti, il tempo di risoluzione può essere molto più lungo. In parole povere, si può dimostrare che la probabilità che il tempo di risoluzione superi un'unità di tempo arbitraria *t* scende esponenzialmente rispetto all'incremento di *t* (per ogni *t* molto maggiore di t*pcq*): ciò significa che, se il circuito considerato entra uno stato metastabile, più si attende a lungo e più è probabile che questo risolva in un *output* accettabile.

Nella progettazione di un circuito sequenziale sincrono, uno degli obiettivi principali è minimizzare la possibilità del circuito di entrare in uno stato metastabile. Uno dei metodi più comuni per ottenere questo scopo è far passare qualsiasi *input* asincrono (come quello considerato nell'esempio precedente) attraverso dei "sincronizzatori".

Un **sincronizzatore** è un dispositivo che riceve un *input* asincrono *D* e un segnale *CLK*; esso produce un *output Q* entro un intervallo limitato di tempo, ed è altamente probabile che tale *output* corrisponda a un valore accettabile. Se *D* rimane stabile durante l'*aperture time*, allora non ci sono problemi e *Q* può tranquillamente assumere il valore di *D*; se, invece, *D* varia durante l'*aperture time*, *Q* dovrebbe assumere un valore che sia o 0 o 1, ma evitare a tutti i costi di risultare in uno stato metastabile. Compattamente, un sincronizzatore viene rappresentato con la seguente simbologia:

![[sync_symbol.png]]

Un sincronizzatore può essere costruito in vari modi. È possibile, ad esempio, implementare un sincronizzatore utilizzando due *flip-flop*, come si può vedere di seguito:

![[sync_example.png]]

In questo esempio, F1 trasmette il valore di *D* al *clock edge*, e se *D* varia in quel momento, l'*output* che viaggia su D2 potrebbe essere metastabile. Se il periodo di *CLK* è sufficientemente lungo, il segnale su D2 risolverà, con alta probabilità, in un valore accettabile prima della fine del periodo stesso, e dunque prima che esso venga trasmesso a F2.

Si dice che un sincronizzatore "fallisce" se *Q* diventa metastabile. Questo succede nel caso in cui il segnale su D2 non risolve in un valore accettabile in tempo, e dunque nel caso in cui:
$$tres > T_c - tsetup$$
___
Analizzando un circuito, possiamo chiamare "***token***" un gruppo di *input* che vengono processati per produrre un gruppo di *output*. La **latenza** di un circuito è il tempo che impiega un determinato *token* per percorrere completamente il circuito considerato; chiamiamo, invece, "***throughput***" il numero di *token* che può essere completamente processato in una determinata unità di tempo. Per comodità, si può pensare a queste due grandezze come alla coppia di grandezze periodo-frequenza.

Il *throughput* di un circuito può essere migliorato, e dunque aumentato, processando un maggior numero di *token* contemporaneamente. Questo processo viene chiamato "**parallelismo**", e viene praticato principalmente in due modi:
- **parallelismo spaziale**;
- **parallelismo temporale**.

Per attuare il parallelismo spaziale, si dispongono più copie dello stesso circuito o segmento di circuito, in modo da poter svolgere un maggior numero di compiti contemporaneamente. Per attuare il parallelismo temporale, invece, si divide un determinato compito in più sotto-compiti, in un procedimento simile a una catena di montaggio: in questo modo, seppur ogni singolo compito dovrà comunque passare per ogni sezione del circuito, ognuna di esse lavorerà su un compito diverso in un momento arbitrario, così che concretamente più compiti possano essere svolti allo stesso momento. Il parallelismo temporale viene anche chiamato "***pipelining***".

Supponiamo di avere un compito con latenza *L*. Un circuito che risolve tale compito senza implementare alcun tipo di parallelismo avrà un *throughput* di *1/L*; invece, un circuito che risolve tale compito implementando il parallelismo spaziale, e utilizzando quindi *N* copie di sé stesso per fare ciò, avrà un *throughput* di *N/L*; infine, un circuito che risolve tale compito implementando il parallelismo temporale, e dunque idealmente suddividendo il compito in *N* parti di egual lunghezza, avrà anch'esso un *throughput* di *N/L*, utilizzando però una sola copia del circuito.

Seppur il parallelismo temporale sembri essere innegabilmente la scelta migliore, trovare *N* sotto-compiti di egual lunghezza non è sempre facile, o addirittura possibile. Nel caso in cui i sotto-compiti abbiano lunghezza diversa, e il più lungo abbia latenza *L₁*, allora il *throughput* del circuito sarà pari a *1/L₁*. 

L'aspetto più attrattivo del *pipelining*, concretamente, è proprio la possibilità di velocizzare un circuito senza duplicarne i componenti. Di solito, ciò avviene inserendo dei registri tra i vari blocchi di logica combinatoria del circuito, in modo da dividere quest'ultimo in varie sezioni che potranno lavorare sotto un segnale di *CLK* più veloce. Nel fare ciò, i registri sono importanti proprio perché non permettono a un *token* coinvolto in una determinata sezione di raggiungere e corrompere un *token* coinvolto nella sezione successiva.

Vediamo un esempio di applicazione del *pipelining*. Di seguito, un circuito che non presenta alcun tipo di parallelismo:

![[pipeline_example.png]]

Nel circuito considerato troviamo 4 blocchi di logica combinatoria, racchiusi tra 2 registri. La *[[Tempi (combinatori)|critical path]]* passa attraverso i blocchi 2, 3 e 4, e assumendo che il registro abbia t*pcq* = 0.3 ns e t*setup* = 0.2 ns, possiamo affermare che il periodo di *CLK* più efficiente possibile prevenendo possibili errori è T*c* = 9.5 ns. Il circuito ha quindi una latenza di 9.5 ns, e un *throughput* di 1/9.5 ns = 105 MHz.

Applicando un primo livello di *pipelining*, possiamo inserire un registro tra i blocchi di logica combinatoria 3 e 4, per ottenere il circuito seguente:

![[pipeline_example1.png]]

In questo caso, la prima sezione del circuito avrà una latenza di 5.5 ns, mentre la seconda di 4.5 ns. Ciò vuol dire che il periodo di *CLK* potrà essere diminuito a T*c* = 5.5 ns senza incorrere in problematiche di alcun tipo. La latenza totale del circuito sarà ora maggiore, ossia 11 ns (due cicli di *CLK*), ma il *throughput* è stato aumentato con successo, ammontando ora a 1/5.5 ns = 182 MHz.

Si può aumentare ancora di più l'efficienza di questo circuito, inserendo un registro a 2 bit prima del blocco di logica combinatoria 3, ottenendo il circuito seguente:

![[pipeline_example2.png]]

Ora, la sezione con latenza maggiore è l'ultima, con una latenza di 4.5 ns. Ciò vuol dire che il periodo di *CLK* potrà essere diminuito nuovamente, stavolta a T*c* = 4.5 ns. La latenza totale del circuito aumenterà ancora, arrivando ora a 13.5 ns (tre cicli di *CLK*), ma il *throughput* risulta ancora maggiore, ammontando a 1/4.5 ns = 222 MHz. Applicando il *pipelining*, si è così più che raddoppiata l'efficienza di questo circuito.

Il parallelismo temporale, seppur molto potente, non può essere applicato sempre. Bisogna, infatti, assicurarsi che non vi siano "**dipendenze**" tra le varie sezioni di un circuito: se una sezione, per svolgere il suo compito, ha bisogno del risultato di un compito precedente, il compito in questione non può cominciare fino a quando quello precedente non sarà terminato.
