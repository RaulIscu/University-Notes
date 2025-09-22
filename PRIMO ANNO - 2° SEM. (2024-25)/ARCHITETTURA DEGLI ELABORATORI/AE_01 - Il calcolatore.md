## I tipi di calcolatore

Nonostante vari calcolatori diversi tra loro condividano pressoché le stesse componenti in termini di **hardware**, le soluzioni utilizzate per ciascuno di essi non sono mai identiche. A grandi linee, i calcolatori possono essere raggruppati in **tre macro-categorie** ben distinte, ossia:
- i **personal computer**, o **PC**;
- i **server**;
- i **calcolatori embedded**.

##### Personal Computer

I **personal computer**, o **PC**, rappresentano senz'altro la forma di calcolatore più conosciuta. Essi offrono delle buone prestazioni a un singolo utente ("personal" computer), mantenendo comunque un costo più o meno limitato; i PC vengono solitamente usati per eseguire software scritto da terze parti o per scrivere software in prima persona.
___
##### Server

I **server** rappresentano, sostanzialmente, un'evoluzione dei calcolatori di grandi dimensioni di un tempo, e nei giorni nostri di norma si può accedere ad essi solamente attraverso la **rete**. Nella maggior parte dei casi, sono orientati all'elaborazione di **grossi carichi di dati**, che si presentano sia come singole applicazioni complesse (come, ad esempio, avviene con applicazioni ingegneristiche o scientifiche) sia come tante piccole applicazioni (come, ad esempio, avviene in un server per il web).

Un server è realizzato con pressoché la stessa tecnologia di base di un [[AE_01 - Il calcolatore#Personal Computer|PC]], ma offre una **maggiore potenza di calcolo**, una **maggiore velocità di I/O** e una **maggiore memoria**. Inoltre, ricoprono un ampio spettro in termini di prestazioni e di costi: si può passare da server di fascia bassa composti da un paio di PC senza schermo né tastiera, fino a veri e propri supercomputer formati da centinaia di migliaia di processori e dotati di una memoria di vari terabyte.
___
##### Calcolatori embedded

I **calcolatori embedded** sono probabilmente i più numerosi dei tre, e coprono uno spettro ampissimo di applicazioni e prestazioni. All'interno di questa categoria, troviamo tutti quei processori e calcolatori progettati per eseguire una singola applicazione, o un'insieme di applicazioni collegate tra di loro, nel contesto di un'**integrazione diretta con l'hardware**, presentandosi all'utente come un sistema unico. Rientrano in questa descrizione i microprocessori delle automobili, i calcolatori presenti nelle televisioni, le reti di processori negli aerei moderni, e così via.

Generalmente, un'applicazione per un calcolatore embedded richiede **prestazioni limitate** e presenta dei **vincoli stringenti sul costo e sulla potenza** del dispositivo. Al tempo stesso, nella progettazione di un calcolatore embedded vi è una **tolleranza minima per i malfunzionamenti**, legata soprattutto al contatto diretto con l'esperienza dell'utente e alla possibilità di una grande responsabilità affidata al calcolatore stesso (si pensi, ad esempio, proprio ai processori di un aereo e alle conseguenze di un loro errore).
___
## Da cosa è composto un calcolatore?

L'hardware di qualsiasi calcolatore deve svolgere pressoché le stesse **funzioni di base**:
- **acquisire dati dall'esterno**, ossia ricevere input;
- **fornire dati all'esterno**, ossia restituire output;
- **elaborare i dati**;
- **memorizzare i risultati delle operazioni svolte**.

Innanzitutto, un calcolatore deve presentare le componenti chiave che si occupano delle prime due mansioni, ossia i **dispositivi di input** (microfono, tastiera, ecc. ecc.) e i **dispositivi di output** (altoparlanti, schermo, ecc. ecc.).

Poi, all'elaborazione dei dati sono destinate altre due componenti fondamentali: l'**unità di elaborazione dati**, detta anche "**datapath**", e l'**unità di controllo**, detta anche "**control unit**". Insieme, queste due componenti vengono spesso considerate come un unico blocco, che costituisce il **processore**, o **[[AE_05 - La CPU||CPU]]**, del calcolatore.

Infine, un calcolatore deve disporre di una **memoria**, dove tenere i programmi in esecuzione così come i dati su cui essi lavorano. Generalmente, la memoria di un calcolatore (tralasciando hard drive e memorie del genere) è costituita da chip di **DRAM**, o "**Dynamic Random Access Memory**", vantaggiose rispetto a memorie di tipo sequenziale per la capacità di accedere a qualsiasi punto della memoria nel medesimo tempo.

Dunque, queste sono le cinque componenti principali e fondamentali nella progettazione di un calcolatore.

##### Dispositivi di I/O


___
##### Memoria


___

