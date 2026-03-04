In questo corso, si approfondirà "**Internet**", o più informalmente la **rete**, tramite la quale i calcolatori possono comunicare: si approfondiranno le modalità in cui avviene lo scambio di dati tra due o più calcolatori, i concetti fondamentali delle reti di elaboratori, e i vari servizi e protocolli che ne definiscono il funzionamento.

## Cos'è Internet?

Spesso, con il termine "Internet" si indica una miriade di cose, a volte propriamente e a volte impropriamente. Ma **cos'è Internet** veramente?

##### Internet è una rete

Possiamo definire Internet in modo basilare come **una rete di dispositivi connessi tra loro**; ciascuno di questi dispositivi viene chiamato "**host**", o anche "**end system**". Per comprendere quanto, ormai, Internet sia diffuso e comune nel mondo, basti pensare che nel 2017 (ormai quasi 10 anni fa) si potevano contare almeno 18 miliardi di singoli dispositivi connessi a Internet, ed è logico pensare che il numero possa solo essere aumentato vertiginosamente. 

All'interno di una rete, gli end system sono collegati tra loro attraverso una **complessa rete di "collegamenti di comunicazione" e di "switch di pacchetto"**. 

Nel concreto, i collegamenti di comunicazione sono i mezzi attraverso i quali vengono trasmessi effettivamente i dati tra i calcolatori della rete, e possono essere **fibre**, **cavi in rame**, **onde radio** o anche **satelliti**. Diversi collegamenti di comunicazione possono trasmettere dati a velocità diverse, e questa capacità propria del mezzo considerato viene tipicamente indicata con termini come "**transmission rate**", "**bandwidth**", "**bitrate**" e simili (approfondiremo questo concetto in seguito).

Quando un determinato end system vuole inviare dei dati a un altro end system della sua rete, l'end system "mittente" andrà a **suddividere i dati in questione in blocchi**, ognuno abbinato a dei cosiddetti "**header bytes**" che forniscono informazioni sul significato del blocco di dati e su come ricomporre il tutto; ciascuno di questi blocchi, abbinato al suo header, viene detto "**pacchetto**", e rappresenta l'unità d'informazione principale che viene trasmessa nella rete. Una volta che l'end system mittente avrà suddiviso i dati in pacchetti, essi verranno inviati nella rete e trasmessi fino all'end system "destinatario", che ricomporrà i vari pacchetti per ottenere nuovamente i dati originali: è qui che entrano in gioco gli "**switch di pacchetto**", dispositivi il cui ruolo, all'interno della rete, è di **ricevere eventuali pacchetti in transito e inoltrarli all'esterno lungo la rete**, in modo che eventualmente essi arrivino a destinazione. Gli switch di pacchetto possono presentarsi in varie forme, ma due dei tipi più comuni sono i **routers** e i **link-layer switches**. La sequenza di collegamenti di comunicazione e di switch di pacchetto attraversata da un pacchetto per arrivare dall'end system mittente all'end system destinatario viene detta "**route**".
___
##### Come accedono a Internet i dispositivi?

Dunque, l'Internet è semplicemente un'enorme rete di dispositivi che rispetta le caratteristiche appena riassunte, o più precisamente una "**rete di reti**" del genere. Ma **come fanno gli end system ad accedere a Internet**?

Ciò avviene grazie ai cosiddetti "**Internet Service Providers**", o in breve "**ISP**". Ci sono vari tipi di ISP, in base al contesto in cui vengono utilizzati, tra cui:
- ISP residenziali;
- ISP aziendali;
- ISP universitari;
- ISP che forniscono accesso a Internet in aeroporti, hotel, o altri spazi pubblici;
- ISP per dati mobili;

e così via. **Ogni ISP rappresenta**, di per sé, **un esempio di [[RDE_01 - Introduzione#Internet è una rete|rete]]** costituita da collegamenti di comunicazione e switch di pacchetto, e può fornire vari tipi di accesso ai vari end system che la compongono. Inoltre, essendo Internet una "macro-rete" unica, **anche i vari ISP dovranno essere connessi tra loro**: si avrà, così, una vasta gamma di ISP di "basso livello" collegati tra loro attraverso ISP di "alto livello" a copertura nazionale o internazionale; a loro volta, questi ISP di alto livello saranno connessi direttamente tra di loro (ad esempio, attraverso la fibra ottica), permettendo una comunicazione tra tutti i dispositivi.
___
##### Protocolli e standard

Tutti gli end system di una rete, gli switch di pacchetto, e qualsiasi altro dispositivo sia connesso a Internet segue determinati **protocolli**, che definiscono come inviare e ricevere dati nell'Internet. In particolare, due dei protocolli più importanti utilizzati in questo ambito sono:
- il **Transmission Control Protocol**, o **TCP**;
- l'**Internet Protocol**, o **IP**.

Ad esempio, l'IP specifica il formato in cui devono essere inviati i [[RDE_01 - Introduzione#Internet è una rete|pacchetti]] all'interno di una rete. Collettivamente, i protocolli principali che regolano il funzionamento di Internet sono conosciuti come **TCP/IP**. Data l'importanza dei protocolli, è fondamentale che ci siano delle **convenzioni su quali protocolli utilizzare e sul ruolo di ciascun protocollo**, in modo che possano essere creati più facilmente sistemi che possano comunicare tra loro: è necessario, dunque, definire degli "**standard**". Gli standard che regolano il funzionamento dell'Internet sono definiti dall'**Internet Engineering Task Force**, o **IETF** in breve, mentre i documenti che esprimono gli standard effettivi vengono chiamati "**Requests For Comments**", o **RFC**. Attualmente, esistono quasi 9000 RFC, che contribuiscono a definire protocolli fondamentali come il TCP, l'IP, o l'HTTP.

Ma più nel dettaglio, **cos'è un protocollo?** Per comprendere ciò, può aiutare fare dei paralleli con la comunicazione tra noi esseri umani. Se pensiamo, ad esempio, a una tipica conversazione tra due persone in cui una delle due chiede l'orario all'altra, possiamo già immaginarci a grandi linee cosa si diranno: prima uno scambio di saluti, poi la persona interessata chiederà l'ora all'altra, e quest'ultima risponderà fornendo proprio l'orario richiesto, se avrà modo di saperlo. Implicitamente, tutte queste parti della conversazione ci comunicano singolarmente dei messaggi o delle intenzioni: ad esempio, generalmente quando si dà un saluto cordiale a un'altra persona ci si aspetta che quest'ultima risponda analogamente; in seguito, se si riceve effettivamente una risposta "favorevole", è come se questa fosse un'indicazione del fatto che si può procedere a chiedere l'orario senza problemi, mentre una risposta scortese o infastidita ci segnala che forse è meglio lasciare stare e interrompere il tentativo di conversazione. Il punto è che **ci sono messaggi specifici che si possono mandare, e specifici comportamenti con cui si può reagire in base alla risposta che si riceve**. Questa definizione generale può essere applicata anche ai protocolli utilizzati nel networking.

Risulta evidente, sia nell'analogia umana che nel caso effettivo, che **le entità comunicanti devono seguire lo stesso protocollo per conseguire con successo un obiettivo**: se, ad esempio, una persona è educata mentre l'altra no, oppure se una delle due persone non è, per qualche motivo, a conoscenza del concetto di tempo, ci sarà molta più difficoltà nel comunicare e ottenere le informazioni desiderate.

**Un protocollo di networking**, dunque, **risulta essere del tutto analogo ai "protocolli" utilizzati nella comunicazione umana**, con la differenza che a comunicare non sono esseri umani, ma componenti di hardware e software di determinati dispositivi. **Qualsiasi attività avvenga su Internet viene regolamentata da un qualche protocollo**: per esempio, ci sono protocolli implementati a livello di hardware per gestire il flusso di informazioni tra due calcolatori fisicamente collegati; possiamo trovare anche protocolli che gestiscono la velocità e la modalità di trasmissione dei pacchetti tra due dispositivi; ancora, nei router ci sono protocolli che determinano il modo in cui si decide la route di un pacchetto da mittente a destinatario. Considerato quanto detto finora in questo paragrafo, possiamo fornire una **definizione generale di protocollo** nel mondo del networking:

> Un protocollo definisce il formato e l'ordinamento dei messaggi scambiati tra due o più entità comunicanti, così come le azioni compiute in risposta alla ricezione o all'invio di un messaggio, o a un qualsiasi altro evento.
___
##### Che servizi offre l'Internet?

Finora, abbiamo descritto Internet in termini delle sue componenti; tuttavia, è anche possibile descriverlo da un'altra angolazione, ossia in base ai **servizi che offre**. Principalmente, **Internet fornisce un'infrastruttura dove possono funzionare varie applicazioni**: oltre ad applicazioni più tradizionali come l'utilizzo di e-mail o i browser, in questo gruppo troviamo anche le applicazioni utilizzate nei dispositivi mobili, i videogiochi, le piattaforme di streaming multimediali, le app di messaggistica, e così via. Questo genere di applicazioni viene detto "**applicazioni distribuite**" (**distributed applications**), dato che coinvolge più end system della rete. Per chiarezza, si specifica che **le applicazioni distribuite vengono concretamente eseguite solo sugli end system e non sugli switch di pacchetto**, infatti questi ultimi si limitano a facilitare la comunicazione tra end system e non hanno informazioni o facoltà sul funzionamento delle applicazioni particolari.

Essendo le applicazioni distribuite utilizzate su più end system, che devono scambiarsi dati continuamente, **l'Internet può essere visto anche come un'interfaccia per la comunicazione tra applicazioni distribuite** (in questo contesto, si dice anche che Internet funge da "**socket interface**"). Mediante Internet, un programma in esecuzione su un end system potrà chiedere di trasmettere dati a uno specifico programma in esecuzione su un altro end system della stessa rete; per permettere questo scambio di dati tra programmi e applicazioni, Internet specifica un particolare insieme di regole, che approfondiremo in seguito.
___
## Periferia e nucleo di rete

Una qualsiasi [[RDE_01 - Introduzione#Internet è una rete|rete di dispositivi]] può essere "separata" in due parti principali:
- la "**periferia**", detta anche "**network edge**";
- il "**nucleo**", detto anche "**network core**".

##### Periferia della rete

Nella **periferia della rete** troviamo ciò con cui siamo più familiari: computer, smartphone, e vari altri dispositivi che utilizziamo quotidianamente. 

Ricordando quanto detto qualche paragrafo fa, questi dispositivi all'interno di una rete prendono il nome di "**end systems**": in questo contesto, si comprende che questa terminologia viene utilizzata perché i dispositivi in questione formano appunto la periferia, dunque le zone esterne (la "fine") della rete. Allo stesso modo, i dispositivi considerati vengono chiamati anche "**hosts**" perché eseguono (ospitano) le varie [[RDE_01 - Introduzione#Che servizi offre l'Internet?|applicazioni]]. Tendenzialmente, gli hosts di una rete vengono divisi in **due macro-categorie**:
- **clients**;
- **servers**.

Informalmente, i dispositivi client sono spesso computer, smartphone, PC, e tutti quegli altri dispositivi che **"ricevono" dei servizi ed eseguono applicazioni utente**; invece, i dispositivi server sono generalmente macchine più potenti e ad elevate prestazioni, il cui scopo è **conservare e distribuire dati**, così come **eseguire programmi che forniscono servizi ad applicazioni utente** eseguite sui dispositivi client.

Per poter comunicare tra di loro, i vari end systems di una rete devono essere collegati ad essa attraverso una "**rete di accesso**", ossia la sotto-rete che connette fisicamente un end system al primo router (detto anche "router periferico") sulla route verso un altro end system. In base al contesto, si distinguono **diversi tipi di reti di accesso**, tra cui:
- reti di accesso **residenziali**;
- reti di accesso **istituzionali** o **aziendali**;
- reti di accesso **mobile**.

Nel 2020, uno studio ha mostrato che più dell'80% delle residenze europee e statunitensi avevano un accesso stabile a Internet. Al giorno d'oggi, le due principali forme di **reti di accesso residenziali** sono:
- la "**digital subscriber line**", o **DSL** in breve;
- l'**accesso via cavo**.

Nel caso della prima, spesso la DSL di una residenza è gestita dallo stesso operatore che fornisce a tale residenza l'accesso alla linea telefonica: perciò, parlando di DSL, **spesso la compagnia telefonica del cliente è anche il suo [[RDE_01 - Introduzione#Come accedono a Internet i dispositivi?|ISP]]**. Per permettere al cliente l'accesso ad Internet, il modem della DSL sfrutta la linea telefonica esistente per trasmettere dati a un "**DSL access multiplexer**", o **DSLAM** in breve, tipicamente situato nella sede centrale della compagnia telefonica; per fare ciò, il modem riceve i dati digitali e li converte in segnali analogici ad alta frequenza, segnali che verranno poi trasmessi lungo la linea telefonica fino al DSLAM, che procederà a riconvertirli in segnali digitali e a inoltrarli lungo la rete. Ci si potrebbe chiedere, a questo punto, **come si fa a distinguere tra segnali telefonici e dati da trasmettere su Internet**, dato che entrambi sono mandati utilizzando la linea telefonica. Il segreto sta nella **frequenza** dei diversi tipi di segnale, dato che:
- un **segnale telefonico ordinario** si trova solitamente in una banda di frequenza **tra 0 e 4 kHz**;
- un **segnale di rete in upstream** (quando si manda qualcosa nella rete) si trova solitamente in una banda di frequenza **tra 4 e 50 kHz**;
- un **segnale di rete in downstream** (quando si scarica qualcosa dalla rete) si trova solitamente in una banda di frequenza **tra 50 kHz e 1 MHz**.

Dal lato del ricevente, per assicurare una corretta separazione dei segnali in arrivo al modem DSL, generalmente si dispone anche di uno "**splitter**", che gestisce proprio tale differenziazione e inoltra al modem solamente i dati di rete.

Gli standard DSL definiscono molteplici "**transmission rates**", ossia in parole povere molteplici velocità massime a cui possono essere trasmessi dati: ad esempio, per la trasmissione di dati in **upstream** si usano spesso transmission rates di **3.5 Mbps** o di **16 Mbps**, mentre per la trasmissione di dati in **downstream** di **24 Mbps** o di **52 Mbps**. Dato che le transmission rates dei dati in upstream e in downstream sono diverse, si dice che **la rete di accesso è asimmetrica**.

In generale, ci sono vari fattori possibili per cui una determinata transmission rate può non essere sempre raggiunta: ad esempio, la compagnia telefonica potrebbe offrire un servizio "a livelli" in cui avere una maggiore velocità richiede un pagamento maggiore; in molti casi, poi, la transmission rate è limitata anche dalla distanza tra la residenza e la sede centrale della compagnia, e dunque il DSLAM, dato che una rete di accesso di tipo DSL è solitamente progettata per funzionare bene nel raggio di 5-10 miglia dalla sede centrale della compagnia telefonica.

Mentre la DSL sfrutta la linea telefonica, la **connessione via cavo** utilizza l'**infrastruttura della compagnia di televisione via cavo** per trasmettere dati. In questo caso, dunque, **la compagnia della TV via cavo del cliente sarà anche il suo ISP**.  

[SLIDES: 02... slide 9 - 10, 16 - 17, 19]
[LIBRO: pag. 44]
___
## 

[recuperare lezioni del 23 febbraio, del 24 febbraio e del 2 marzo]

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

