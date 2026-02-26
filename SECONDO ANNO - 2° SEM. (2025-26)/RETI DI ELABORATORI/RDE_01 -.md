In questo corso, si approfondirà "**Internet**", o più informalmente la **rete**, tramite la quale i calcolatori possono comunicare: si approfondiranno le modalità in cui avviene lo scambio di dati tra due o più calcolatori, i concetti fondamentali delle reti di elaboratori, e i vari servizi e protocolli che ne definiscono il funzionamento.

## Cos'è Internet?

Spesso, con il termine "Internet" si indica una miriade di cose, a volte propriamente e a volte impropriamente. Ma **cos'è Internet** veramente?

##### Internet è una rete

Possiamo definire Internet in modo basilare come **una rete di dispositivi connessi tra loro**; ciascuno di questi dispositivi viene chiamato "**host**", o anche "**end system**". Per comprendere quanto, ormai, Internet sia diffuso e comune nel mondo, basti pensare che nel 2017 (ormai quasi 10 anni fa) si potevano contare almeno 18 miliardi di singoli dispositivi connessi a Internet, ed è logico pensare che il numero possa solo essere aumentato vertiginosamente. 

All'interno di una rete, gli host sono collegati tra loro attraverso una **complessa rete di "collegamenti di comunicazione" e di "switch di pacchetto"**. 

Nel concreto, i collegamenti di comunicazione sono i mezzi attraverso i quali vengono trasmessi effettivamente i dati tra i calcolatori della rete, e possono essere **fibre**, **cavi in rame**, **onde radio** o anche **satelliti**. Diversi collegamenti di comunicazione possono trasmettere dati a velocità diverse, e questa capacità propria del mezzo considerato viene tipicamente indicata con termini come "**transmission rate**", "**bandwidth**", "**bitrate**" e simili (approfondiremo questo concetto in seguito).

Quando un determinato host vuole inviare dei dati a un altro host della sua rete, l'host "mittente" andrà a **suddividere i dati in questione in blocchi**, ognuno abbinato a dei cosiddetti "**header bytes**" che forniscono informazioni sul significato del blocco di dati e su come ricomporre il tutto; ciascuno di questi blocchi, abbinato al suo header, viene detto "**pacchetto**", e rappresenta l'unità d'informazione principale che viene trasmessa nella rete. Una volta che l'host mittente avrà suddiviso i dati in pacchetti, essi verranno inviati nella rete e trasmessi fino all'host "destinatario", che ricomporrà i vari pacchetti per ottenere nuovamente i dati originali: è qui che entrano in gioco gli "**switch di pacchetto**", dispositivi il cui ruolo, all'interno della rete, è di **ricevere eventuali pacchetti in transito e inoltrarli all'esterno lungo la rete**, in modo che eventualmente essi arrivino a destinazione. Gli switch di pacchetto possono presentarsi in varie forme, ma due dei tipi più comuni sono i **routers** e i **link-layer switches**. La sequenza di collegamenti di comunicazione e di switch di pacchetto attraversata da un pacchetto per arrivare dall'host mittente all'host destinatario viene detta "**route**".
___
##### Come accedono a Internet i dispositivi?

Dunque, l'Internet è semplicemente un'enorme rete di dispositivi che rispetta le caratteristiche appena riassunte, o più precisamente una "**rete di reti**" del genere. Ma **come fanno gli host ad accedere a Internet**?

Ciò avviene grazie ai cosiddetti "**Internet Service Providers**", o in breve "**ISP**". Ci sono vari tipi di ISP, in base al contesto in cui vengono utilizzati, tra cui:
- ISP residenziali;
- ISP aziendali;
- ISP universitari;
- ISP che forniscono accesso a Internet in aeroporti, hotel, o altri spazi pubblici;
- ISP per dati mobili;

e così via. **Ogni ISP rappresenta**, di per sé, **un esempio di [[RDE_01 -#Internet è una rete|rete]]** costituita da collegamenti di comunicazione e switch di pacchetto, e può fornire vari tipi di accesso ai vari host che la compongono. Inoltre, essendo Internet una "macro-rete" unica, **anche i vari ISP dovranno essere connessi tra loro**: si avrà, così, una vasta gamma di ISP di "basso livello" collegati tra loro attraverso ISP di "alto livello" a copertura nazionale o internazionale; a loro volta, questi ISP di alto livello saranno connessi direttamente tra di loro (ad esempio, attraverso la fibra ottica), permettendo una comunicazione tra tutti i dispositivi.
___
##### Protocolli e standard

Tutti gli host di una rete, gli switch di pacchetto, e qualsiasi altro dispositivo sia connesso a Internet segue determinati **protocolli**, che definiscono come inviare e ricevere dati nell'Internet. In particolare, due dei protocolli più importanti utilizzati in questo ambito sono:
- il **Transmission Control Protocol**, o **TCP**;
- l'**Internet Protocol**, o **IP**.

In particolare, l'IP specifica il formato in cui devono essere inviati i [[RDE_01 -#Internet è una rete|pacchetti]] all'interno di una rete. Collettivamente, i protocolli principali che regolano il funzionamento di Internet sono conosciuti come **TCP/IP**. Data l'importanza dei protocolli, è fondamentale che ci siano delle **convenzioni su quali protocolli utilizzare e sul ruolo di ciascun protocollo**, in modo che possano essere creati più facilmente sistemi che possano comunicare tra loro: è necessario, dunque, definire degli "**standard**". Gli standard che regolano il funzionamento dell'Internet sono definiti dall'**Internet Engineering Task Force**, o **IETF** in breve, mentre i documenti che esprimono gli standard effettivi vengono chiamati "**Requests For Comments**", o **RFC**. Attualmente, esistono quasi 9000 RFC, che contribuiscono a definire protocolli fondamentali come il TCP, l'IP, o l'HTTP. 
___
##### Che servizi offre l'Internet?



[SLIDE: 01 - slide 31]
[LIBRO: pag. 35]
___


[recuperare lezioni del 23 febbraio e del 24 febbraio]

Ampiezza di banda: due concetti principali:
- caratterizzazione del canale o del sistema trasmissivo, l'intervallo di frequenze che un mezzo fisico consente di trasmettere senza danneggiare il segnale; maggiore è l'ampiezza di banda, maggiore è la quantità di informazione che può essere veicolato;
- quantità di bit al secondo che il mezzo di collegamento può trasmettere

il bitrate dipende sia dalla banda che dalla tecnica di trasmissione. 

THROUGHPUT: quanto velocemeente riusciamo a inviare dati CONCRETAMENTE tramite una rete, o numero di bit al secondo che passano attraverso un punto della rete. è simile al rate, ma...

...

I pacchetti si "accodano" nei buffer dei router (store and forward): nei router, i pacchetti si mettono in coda per essere mandati; supponendo che i pacchetti arrivino a velocità elevata e che il router non riesce a spedirli in modo sufficientemente veloce, a un certo punto il buffer si riempirebbe e ci sarebbe necessariamente una perdita di pacchetti (o i pacchetti nuovi in arrivo vengono ignorati, o vengono cestinati altri pacchetti già presenti nel buffer).

ritardi (latenze) del pacchetto:
- $d_{proc}$, processing delay, elaborazione del pacchetto, attesa che il pacchetto venga processato dal router;
- $d_{queue}$, queueing delay, ritardo di accodamento, attesa che il pacchetto venga trasmesso dal router; 
- $d_{trans}$, transmission delay, il tempo per modularlo sul "cavo";
- $d_{prop}$, propagation delay, il tempo che ci mette il pacchetto per essere propagato lungo il "cavo".

...

