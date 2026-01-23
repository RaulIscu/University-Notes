Una delle mansioni più importanti di un OS all'interno di un calcolatore è una corretta **gestione della memoria**. Per ottenere ciò, l'OS deve puntare al compimento dei seguenti obiettivi:
- allocare correttamente memoria e risorse ai vari [[SO1_03 - Processi|processi]] e [[SO1_05 - Thread#Cos'è un thread?|thread]], **massimizzando l'utilizzo della memoria e il throughput del sistema**;
- garantire l'isolamento tra i vari processi, assicurando l'**indirizzabilità** e la **protezione tra processi**;
- fornire un'astrazione della memoria conveniente per l'utente, fornendo un'illusione di memoria illimitata tramite l'utilizzo di **memoria virtuale**.

Nei seguenti paragrafi, si approfondiranno i diversi modi in cui l'OS consegue questi obiettivi.

## Allocare memoria a processi e thread

##### Address binding

Partiamo dalle basi: quando un programmatore scrive un programma, e dunque del codice sorgente, **come fa il calcolatore ad eseguire tale programma?** Tipicamente, i programmi scritti da un utente fanno riferimento a dati e istruzioni specifici attraverso dei **nomi simbolici**, come `+`, `&&`, `count`, ecc. ecc.; per permettere l'esecuzione di un programma il cui codice contiene tali nomi, si dovrà:
1. **"tradurre" il codice sorgente in un file binario eseguibile**, che verrà conservato nella memoria a disco del calcolatore;
2. **caricare l'eseguibile nella memoria principale**, comunemente indicata come RAM.

Questi due passaggi fondamentali vengono eseguiti da diverse entità nel calcolatore: la traduzione da codice sorgente a file binario avviene grazie a **compilatori**, **assemblers** e **linkers** (nel caso di programmi scritti in linguaggi interpretati, la traduzione avviene invece quasi a runtime, ed è operata dall'interprete scelto); invece, il programma viene caricato in RAM dal **loader** dell'OS. 

Una volta ottenuto un eseguibile a partire da un programma, per poter **eseguire concretamente tale programma** la CPU dovrà ottenere ("**fetch**"), decodificare ("**decode**") ed eseguire ("**execute**") la serie di istruzioni contenuta al suo interno, e per fare ciò dovrà naturalmente accedere alla memoria. Inoltre, molte di queste istruzioni saranno istruzioni che richiederanno continue interazioni con la memoria, siano esse di **recupero** o di **scrittura di dati**, o anche entrambe in certi casi. Dato che per poter interagire con i chip della memoria si dovrà necessariamente far utilizzo di **indirizzi di memoria fisici**, sarà necessario **istanziare un qualche collegamento tra nomi simbolici contenuti nel programma e indirizzi fisici di memoria**. Ciò può avvenire attraverso la seguente scaletta:
1. **il nome simbolico**, ossia un riferimento simbolico alla memoria utilizzato all'interno del codice sorgente, **viene associato a un "indirizzo logico"**, ossia un indirizzo di memoria generato durante l'esecuzione del programma tramite la CPU;
2. **l'indirizzo logico viene poi convertito in un indirizzo fisico**, ossia un indirizzo di memoria effettivo, sul quale possono operare i chip della memoria e che conterrà il dato considerato.

Mentre il passaggio tra nome simbolico e indirizzo logico è relativamente semplice, quello tra indirizzo logico e indirizzo fisico, detto anche "**address binding**", non è così immediato. Innanzitutto, tale conversione può avvenire in $3$ momenti ben distinti:
- durante la **compilazione** del programma;
- durante il **caricamento** e l'**avvio** del programma;
- durante l'**esecuzione** del programma.

L'address binding che avviene **durante la compilazione** richiede che **si sappia l'indirizzo fisico di partenza del programma** considerato nella memoria. Se vale tale condizione, il compilatore potrà generare del cosiddetto "**codice assoluto**", e sostanzialmente **l'indirizzo fisico coinciderà con l'indirizzo logico**. Naturalmente, basandosi il tutto sull'indirizzo di memoria dove si trova il programma, se per qualche motivo esso cambia dopo la compilazione allora il programma dovrà essere ricompilato per assicurarne la corretta esecuzione.

L'address binding che avviene **durante il caricamento e l'avvio** avviene quando **non si è necessariamente a conoscenza**, durante la compilazione, **dell'indirizzo fisico di partenza del programma** considerato nella memoria. In questo caso, il compilatore genera del "**codice statico rilocalizzabile**", che si basa su indirizzi relativi all'ipotetico indirizzo di partenza $k$; sarà, in seguito, il loader dell'OS a determinare l'indirizzo fisico effettivo del programma (ossia $k$), e ad aggiustare gli indirizzi relativi generati dal compilatore in base a quest'ultimo (dunque, anche stavolta, **indirizzi logici e indirizzi fisici finiranno per coincidere**). Con questo approccio, se il programma dovesse per qualche motivo cambiare posizione in memoria dopo la compilazione, esso non dovrà necessariamente essere ricompilato, ma dovrà sicuramente essere riavviato dal loader.

L'address binding che avviene **durante l'esecuzione** avviene quando **è possibile che il programma venga spostato nella memoria principale durante l'esecuzione dello stesso**. In questo caso, il compilatore genera del "**codice dinamico rilocalizzabile**", che si basa su dei cosiddetti "**indirizzi virtuali**"; l'OS andrà poi ad associare volta per volta gli indirizzi virtuali a quelli fisici sfruttando una **Memory Management Unit**, o **MMU** in breve. Dunque, con questo approccio, **gli indirizzi logici** (o meglio, quelli virtuali) **non coincideranno con quelli fisici**. Quest'ultima soluzione è in realtà quella più flessibile e più frequentemente utilizzata nella maggior parte dei sistemi moderni.

Essendo gli indirizzi virtuali uno strumento così importante, è essenziale introdurre anche il concetto di **spazio di indirizzamento virtuale**, o **VAS** in breve, **di un processo**. Si assume, in generale, che il VAS di ogni processo abbia la medesima dimensione, che esso debba essere situato contiguamente nella memoria principale, e che la memoria principale debba essere molto più ampia della dimensione di un VAS.
___
##### Rilocazione di un processo

Quando si avvia l'esecuzione di un programma, sarà necessario **allocare il VAS di un processo all'interno della memoria principale**. Vediamo come avviene questa procedura.

Innanzitutto, dobbiamo fare delle premesse:
- si suppone sempre che **la parte di memoria occupata dall'OS si trovi all'inizio o alla fine della memoria**, e dunque occupi i più bassi o i più alti indirizzi di memoria;
- di conseguenza, si assume che qualsiasi indirizzo logico generato da un processo utente sia incluso nel range $[0,\,\text{memory\_size}-\text{os\_size}-1]$.

Tendenzialmente, quando un processo viene caricato nella memoria principale **il suo spazio di indirizzamento viene caricato in un segmento contiguo di memoria**. L'allocazione di uno spazio di memoria del genere a un processo, dunque sostanzialmente la traduzione degli indirizzi di memoria logici del programma in indirizzi fisici nella RAM, viene detta "**rilocazione**", e tale rilocazione può avvenire principalmente in due modi:
- **rilocazione statica**;
- **rilocazione dinamica**.

La **rilocazione statica** avviene al **caricamento del programma nella RAM**, in modo da poter essere eseguito. In parole povere, si ha un procedimento analogo all'[[SO1_07 - Gestione della memoria#Address binding|address binding]] in fase di caricamento che abbiamo visto nel paragrafo precedente: il loader "riscriverà" gli indirizzi logici del processo convertendoli in indirizzi fisici validi all'interno della RAM. Questo approccio presenta come **pregio** principale il **non avere bisogno di HW supplementare**, ma allo stesso tempo ha vari **difetti**: **non assicura una protezione dell'OS o di altri processi**; una volta caricato nella RAM, **il processo non potrà essere spostato nuovamente** dall'OS senza problemi; **non si assicura che lo spazio di indirizzamento del processo sia contiguo**.

Al contrario, la **rilocazione dinamica** è molto più all'avanguardia, seppur anche più complessa. Essa assicura la protezione degli spazi di memoria dedicati all'OS e ad altri processi, ma per essere implementata necessita di una componente di HW particolare, a cui abbiamo già accennato: la **Memory Management Unit**, o **MMU**. In questo caso, l'address binding effettivo avviene durante l'esecuzione del programma, con l'MMU che traduce dinamicamente i vari indirizzi logici (virtuali) in indirizzi fisici della RAM.
___
[12, slide 96 - 99 - 109/112 - 117 - 122 - 126 - 129 - 135 - 141 - 147 - 151 - 154 - 159 - 162/164 - 166/168 - 170 - 174 - 178 - 182 - 183]