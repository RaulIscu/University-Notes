## Gerarchia delle memorie

Fin dal principio dell'era dell'informatica, i programmatori hanno sempre agognato una memoria illimitata e al tempo stresso velocissima, che possa contenere tutti i dati che si desiderano e che possa permettere l'accesso ad essi in fretta. Naturalmente, una memoria che rispetti concretamente queste esigenze non esiste, ma ci sono varie tecniche che si possono utilizzare per creare una memoria che ci si avvicini il più possibile.

La prima di queste tecniche che analizzeremo è il cosiddetto "**principio di località**". Così come uno studente, interessato a una determinata materia, non ha bisogno di dover consultare con la stessa probabilità tutti i libri di una biblioteca, così **un programma non deve accedere, con la stessa probabilità, a tutta la memoria a sua disposizione**. Di conseguenza, il principio di località afferma, in sostanza, che **un programma, in un certo istante di tempo, accede soltanto a una porzione relativamente piccola della memoria**. Questo principio può essere reinterpretato come l'unione di due sotto-principi, ossia:
- il principio di **località temporale**;
- il principio di **località spaziale**.

In particolare, il primo afferma che, **se si accede a una certa locazione di memoria, è probabile che vi si acceda di nuovo poco tempo dopo**; il secondo, invece, afferma che **se si accede a una certa locazione di memoria, è probabile che in seguito si acceda a locazioni vicine ad essa**. Questi principi emerge in modo spontaneo dalla struttura tipica dei programmi: ad esempio, all'interno di un ciclo, dati e istruzioni vengono ripetutamente letti dalla memoria, dimostrando un elevato livello di località temporale; inoltre, le istruzioni di un programma sono normalmente memorizzate in sequenza, portando in questo caso a una spiccata località spaziale.

La conoscenza di questi principi viene sfruttata per **strutturare la memoria di un [[Il calcolatore#Da cosa è composto un calcolatore?|calcolatore]] in forma gerarchica**, rispettando quella che viene chiamata "**gerarchia delle memorie**".

La **gerarchia delle memorie** consiste in un insieme di **livelli di memoria**, ciascuno caratterizzato da una **diversa velocità di accesso** e una **diversa dimensione**. A parità di capacità, le memorie più veloci hanno tendenzialmente un costo più elevato per singolo bit rispetto a quelle più lente, dunque di solito sono più piccole. **La memoria più veloce e piccola è posta più vicino al processore**, mentre quella più lenta e grande è quella più "lontana" dallo stesso. Di conseguenza, anche i dati stessi sono organizzati in modo gerarchico: la totalità dei dati a disposizione si trova nel livello più basso della memoria, e tutti i livelli superiori contengono un sottoinsieme dei dati presenti nel livello sottostante.

Seppur una gerarchia delle memorie possa essere composta da più livelli, **i dati possono essere trasferiti solo tra due livelli vicini**: di conseguenza, poniamo la nostra attenzione su **due soli livelli di memoria**. Quello superiore, più vicino al processore, è naturalmente più piccolo e veloce dell'inferiore, più lontano dal processore. La **più piccola quantità di informazione che può essere presente o assente** su questa sotto-gerarchia a due livelli è denominata "**blocco**", o anche "**linea**".

Se il dato richiesto dal processore è contenuto in uno dei blocchi presenti nel livello superiore, si dice che **la richiesta ha avuto successo**, e questo evento si denota con il termine "**hit**"; se, invece, il dato non viene trovato nel livello superiore della gerarchia, **la richiesta fallisce**, e questo evento si denota con il termine "**miss**". In quest'ultimo caso, per trovare il blocco contenente il dato cercato si dovrà accedere al livello inferiore della gerarchia delle memorie. Possiamo definire come "**hit rate**", o "**frequenza di hit**", la **frazione degli accessi alla memoria che hanno successo**, ossia in cui il dato richiesto viene trovato nel livello superiore della gerarchia considerata; spesso, l'hit rate viene utilizzato come **indice delle prestazioni delle gerarchie delle memorie**. Definiamo, poi, anche una "**miss rate**", o "**frequenza di miss**", che è semplicemente pari a $1 - hit\,\,rate$, e rappresenta la **frazione degli accessi alla memoria che falliscono**.

Poiché il motivo principale della scelta di adottare una gerarchia delle memorie è l'**aumento di prestazioni**, possiamo dedurre che un aspetto importantissimo sia la **velocità di accesso alla memoria**. In particolare, il "**tempo di hit**" è il tempo di accesso al livello superiore della gerarchia, e comprende anche il tempo necessario a stabilire se il tentativo si risolve in un successo (hit) o in un fallimento (miss); in caso di miss, la "**penalità di miss**" consiste nel tempo necessario a sostituire un blocco del livello superiore con un nuovo blocco, caricato dal livello inferiore della gerarchia, e a trasferire i dati contenuti in tale blocco al processore. Siccome il livello superiore è più piccolo e veloce, tendenzialmente **il tempo di hit sarò molto minore al tempo necessario per accedere al livello inferiore nella gerarchia**, tempo che rappresenta la componente più importante della penalità di miss.
___
## Tecnologie delle memorie

Al giorno d'oggi, vengono utilizzate principalmente **quattro tecnologie** per costruire delle memorie e, di conseguenza, una [[La memoria#Gerarchia delle memorie|gerarchia delle memorie]]. 

Due di queste tecnologie sono la **DRAM**, o "**Dynamic Random Access Memory**", e la **SRAM**, o "**Static Random Access Memory**". Mentre la prima è la principale tecnologia utilizzata nelle **memorie RAM** dei calcolatori, la seconda è quella che va a comporre i livelli di memoria più vicini al processore, come la **cache**. Generalmente, **la DRAM ha un costo più basso per bit della SRAM, ma anche un accesso decisamente più lento**. La principale causa della differenza di costo è il fatto che le memorie DRAM utilizzano meno transistor per ogni bit da memorizzare, e riescono così a raggiungere una capacità superiore a parità di materiali utilizzati. 

La terza tecnologia di cui andremo a parlare è la **memoria flash**, che viene principalmente utilizzata nei **dispositivi mobili**. Infine, abbiamo i **dischi magnetici**, che vanno a comporre le memorie più capienti e dall'accesso più lento della gerarchia.

Per un'idea più completa delle prestazioni e dei costi di queste tecnologie, possiamo fare riferimento alla seguente tabella, che fornisce una media di questi valori nell'anno 2020:

![[costi_tempi_memorie_tabella.png]]

A questo punto, andiamo ad approfondire più nel dettaglio ciascuna delle tecnologie appena nominate.

##### SRAM

Le **memorie SRAM** sono, sostanzialmente, dei **circuiti integrati** organizzati come **vettori di memoria**; di solito, essi hanno **una sola porta d'accesso**, che può fornire sia la lettura che la scrittura dei dati della memoria. Le SRAM forniscono lo **stesso tempo di accesso per tutti i dati**.

In una SRAM, si utilizzano **da 6 a 8 transistor per bit**, in modo da evitare il più possibile interferenze o disturbi al momento della lettura. Inoltre, hanno bisogno di ricevere una **potenza minima**, in modo da mantenere la carica anche quando si trovano in stand-by.

In passato, la maggior parte dei PC e dei server utilizzava diversi chip di SRAM per diversi livelli di cache; ad oggi, tuttavia, le cache di tutti i livelli sono integrate nel processore, sostanzialmente eliminando il mercato delle SRAM singole.
___
##### DRAM

In una memoria [[La memoria#SRAM|SRAM]], o RAM statica, il dato rimane memorizzato per tutto il tempo in cui l'alimentazione è attiva. Un comportamento diverso si ha in una **memoria DRAM**, o **RAM dinamica**, in cui il dato viene memorizzato come **carica in un condensatore**, e in cui di conseguenza **un solo transistor è sufficiente** per leggere o sovrascrivere il dato. 

L'utilizzo di un solo transistor per bit di dato memorizzato contribuisce a una **maggiore densità** e a un **costo minore** rispetto alle SRAM; tuttavia, l'utilizzo di un condensatore per memorizzare un bit rende tale memoria più "**volatile**", e rende necessario un **"refresh" periodico** della stessa. Per refreshare, o rinfrescare, una cella di memoria, occorre semplicemente **leggerne il contenuto e riscriverlo**. La carica, però, può essere mantenuta per pochi millisecondi, per cui rinfrescare i bit di una DRAM costantemente ed uno ad uno ruberebbe tempo all'accesso ai dati memorizzati in essa: per questo motivo, le DRAM utilizzano un'**architettura a due livelli**, che consente di **rinfrescare un'intera "riga" di memoria insieme**, mediante un ciclo di lettura seguito immediatamente da un ciclo di riscrittura. Per comprendere meglio la struttura di una DRAM, possiamo osservare la seguente rappresentazione:

![[struttura_dram.png]]

Una memoria DRAM moderna è organizzata in **banchi**, e ciascuno di essi è formato da una **serie di righe**. Inviando un "**comando di precaricamento**", si può aprire o chiudere un banco in particolare; per avviare, invece, il trasferimento del contenuto di una riga del banco in un buffer, si utilizza un "**comando di attivazione**". Una volta che il contenuto di una riga sarà trasferito nel buffer, si potrà accedere ai dati specificando gli indirizzi successivi di gruppi di bit, qualsiasi sia l'ampiezza della DRAM, oppure specificando l'indirizzo di partenza e l'intenzione di accedere all'intero buffer (funzionamento, per certi versi, analogo a quello delle SRAM). Questo approccio migliora significativamente il tempo di accesso.

Per migliorare ulteriormente l'interfaccia tra processori e DRAM, a quest'ultime è stato aggiunto un segnale di **clock**, motivo per cui un nome più appropriato per indicarle sarebbe "**DRAM sincrone**" o "**Synchronous DRAM**", in breve **SDRAM**. Il vantaggio di avere un clock integrato nella memoria sta nell'**eliminazione del tempo necessario a sincronizzare memoria e processore**.

Concretamente, il principale aumento di velocità delle SDRAM è dovuto alla possibilità di **trasferire gruppi di bit adiacenti a raffica**, o "**in burst**", senza la necessità di specificare ulteriori indirizzi di memoria. Questa modalità di trasferimento viene anche chiamata "**DDR**", o "**Double Data Rate**", nome che indica in particolare che il trasferimento dei dati avviene **sia sul positive-edge sia sul negative-edge del clock**, ottenendo così il doppio della larghezza di banda prevista inizialmente. La versione più recente di questa tecnologia è la **DDR4**: ad esempio, una DRAM di tipo DDR4-3200 può effettuare **3200 milioni di trasferimenti di dati al secondo**, che corrisponde a una frequenza di clock di **1600 MHz**.

Per sostenere una tale larghezza di banda, bisogna implementare alcune migliorie nell'organizzazione interna della DRAM. Ad esempio, invece di un unico buffer di riga, ogni banco dispone del proprio buffer, in modo che una DRAM possa leggere o scrivere da diversi banchi simultaneamente.
___
##### Memoria flash

Le **memorie flash**, che fanno parte delle memorie "**EEPROM**" (Electrically Erasable Programmable Read-Only Memory), sono un tipo di memoria cancellabile elettricamente e programmabile.

A differenza dei [[La memoria#Disco magnetico|dischi]] e delle [[La memoria#DRAM|DRAM]], **i bit delle memorie flash si deteriorano dopo un certo numero di scritture**. Per far fronte a questa limitazione, la maggior parte dei dispositivi che utilizzano memorie flash contiene un **controllore**, che distribuisce le scritture dai blocchi di memoria scritti più di frequente su blocchi scritti meno frequentemente, con una tecnica chiamata "**livellamento dell'usura**", o "**wear leveling**". Seppur utilizzare questo approccio vada a diminuire le prestazioni teoriche di una memoria flash, essa risulta pressoché necessaria per allungarne il ciclo di vita, e in certi casi anche utile dato che un controllore può identificare eventuale celle di memoria malfunzionanti.
___
##### Disco magnetico

Una **memoria a disco magnetico** è costituita da un gruppo di **dischi**, detti anche **piatti**, che ruotano a una velocità compresa **tra i $5400$ e i $15000$ giri al minuto**. Ciascun disco è ricoperto su entrambe le facce da un materiale magnetico e registrabile, simile a quello delle videocassette o delle audiocassette; per leggere e scrivere dati su questi dischi, poco al di sopra di entrambe le superfici di ogni disco è posizionato un **braccio mobile**, che presenta all'estremità una "**testina di lettura/scrittura**", ossia una piccola bobina elettromagnetica. Per prevenire disturbi dall'esterno, l'intera unità è sigillata.

Le superfici di ogni disco sono divise in cerchi concentrici chiamati "**tracce**", che sono tipicamente decine di migliaia per lato di un disco; ogni traccia, a sua volta, è divisa in migliaia di "**settori**", che rappresentano l'effettiva **unità di memorizzazione delle informazioni**. Ogni settore ha, tipicamente, una dimensione compresa **tra $512$ e $4096$ byte**. Una tipica sequenza di informazioni registrata sul materiale magnetico è costituita da:
- numero del settore;
- spazio vuoto di separazione;
- informazioni memorizzate nel settore in questione (incluso il codice di correzione degli errori);
- spazio vuoto di separazione;
- numero del settore successivo;

e così via.

Le testine di lettura/scrittura sono collegate assieme e si muovono congiuntamente, così che **ogni testina si trova in corrispondenza della stessa traccia su tutte le superfici**; per riferirsi alle tracce dei diversi dischi che si trovano sotto le testine in un certo istante di tempo, si utilizza il termine "**cilindro**".

Per **accedere ai dati**, il primo passo è l'operazione di "**ricerca**", o "**seek**", che consiste nel posizionare la testina sulla traccia giusta. Il tempo necessario per spostare la testina sopra la traccia desiderata è chiamato **tempo di ricerca**, e tipicamente per una determinata memoria a disco magnetico viene riportato il tempo di ricerca minimo, quello massimo e quello medio: mentre i primi due risultano essere facili da misurare, quello medio è influenzato da molte variabili, e risulta quindi più "aperto a interpretazioni".

Una volta che la testina ha raggiunto la traccia desiderata, deve aspettare che il settore giusto passi sotto di essa: questo tempo di attesa viene detto **latenza di rotazione**, o **ritardo di rotazione**. Naturalmente, il valore medio di questa latenza corrisponde a mezzo giro del disco; avendo stabilito che i dischi magnetici ruotano a velocità comprese tra $5400$ e $15000$ giri al minuto, la latenza di rotazione media nel peggiore dei casi è:
$$\frac{0.5\,\, \text{rotazioni}}{5400\,\, \text{GPM}} = 0.0056\,\,\text{secondi} = 5.6\,\,\text{ms}$$

L'ultima componente importante del tempo di accesso al disco è il **tempo di trasferimento**, ossia il tempo impiegato per trasferire un blocco di bit; questo tempo dipende dalla dimensione del settore, dalla velocità di rotazione e dalla densità di memorizzazione delle tracce. Nel 2020, le velocità di trasferimento dei dati erano tipicamente comprese **tra i $150$ e i $250$ MB/s**.
___
## La cache

Nella [[La memoria#Gerarchia delle memorie|gerarchia delle memorie]] del primo calcolatore commerciale che implementava qualcosa del genere, il livello di memoria che si trova **tra il processore e la memoria principale** (dunque, quello più piccolo e più veloce) era detto "**cache**"; similmente, le memorie utilizzate nelle varie implementazioni di processore approfondite nel capitolo sulle [[La CPU|CPU]] possono essere sostituite da **memorie cache**. 

Ad oggi, seppur la definizione appena fornita rimane la più utilizzata, questo termine viene talvolta esteso ad indicare sistemi di memoria gestiti in modo tale da ottenere i massimi benefici dalla località degli accessi.

##### Come funziona una cache?

In poche parole, una cache rappresenta **una memoria piccola e veloce, che si interfaccia direttamente con il processore, e in cui vengono memorizzati i dati più usati o più recentemente usati**. A livello simbolico, possiamo rappresentare una cache con il seguente schema:

![[cache_semp.png]]

Come possiamo vedere, la cache contiene vari dati ($X_{1}$, $X_{2}$, $X_{3}$, ecc. ecc.), che sono quelli utilizzati più di recente, ciascuno memorizzato in una delle sue $n$ **linee** (una singola linea può contenere più parole di dati). Supponiamo, ora, che il processore richieda una certa parola $X_{n}$: se il blocco di memoria corrispondente è presente nella cache, il dato viene caricato da essa e la richiesta di dati risulta in una **[[La memoria#Gerarchia delle memorie|hit]]**; se, invece, il blocco non è presente attualmente nella cache, la richiesta di dati risulterà in una **[[La memoria#Gerarchia delle memorie|miss]]**, e la parola $X_{n}$ verrà **prelevata dal livello inferiore di memoria** e **trasferita nella cache**. Nel nostro esempio, il dato non era presente nella cache, dunque in seguito alla richiesta lo schema della cache diventa più simile al seguente:

![[cache_semp1.png]]

Viene spontaneo, a questo punto, farsi alcune domande. Ad esempio, come si fa a sapere se un dato è presente nella cache? Oppure, supponendo che questo dato sia effettivamente contenuto in essa, come si fa a trovarlo? Per certi versi, le risposte a queste due domande sono collegate.

Supponiamo che **ogni parola della memoria possa essere scritta in una sola posizione nella cache**: il modo più semplice per rendere possibile ciò è associare una sola locazione della cache a ogni parola della memoria, definendo una **corrispondenza tra i vari indirizzi di memoria e la loro locazione nella cache**. Adottando questo approccio, ammesso che la parola cercata si trovi effettivamente nella cache, sapremo dove trovarla. Quest'organizzazione della cache è detta "**a mappatura diretta**", o "**direct mapped cache**". Per questo tipo di cache, questa corrispondenza tra indirizzi di memoria e locazioni nella cache è di solito molto semplice: quasi tutte le cache a mappatura diretta, per trovare il **blocco che corrisponde a un dato indirizzo della memoria principale**, utilizzano la seguente operazione:
$$\text{indirizzo del blocco in memoria } // \,\,\text{numero di blocchi nella cache}$$
Se il numero di blocchi della cache è una **potenza di 2**, allora l'indirizzamento può essere eseguito semplicemente considerando **i $\log_{2}\text{(numero di blocchi della cache)}$ bit meno significativi dell'indirizzo di memoria**. Per comprendere meglio come avvenga questa procedura, vediamo un esempio:

![[cache_mappatura_diretta_esempio.png]]

Nell'immagine, troviamo una **cache da 8 blocchi**, dove ovviamente si ha che $8 = 2^3$. Ciò vuol dire che, per indirizzare la memoria nella cache, sarà sufficiente considerare i $\log_{2}8 = 3$ bit meno significativi di tale indirizzo: sostanzialmente, **i bit meno significativi dell'indirizzo vengono utilizzati come indice del blocco della cache a cui sono mappati**. Vediamo, ad esempio, che il blocco con indirizzo $00001$ viene mappato al blocco $001$ della cache, mentre il blocco con indirizzo $01101$ viene mappato al blocco $101$ della cache, e così via.

Ora, però, sorge un altro dubbio: dato che ogni elemento della cache può contenere dati provenienti da diversi punti della memoria, come è possibile capire se il dato presente nella cache corrisponde alla parola desiderata? In altre parole, come facciamo a sapere se la parola desiderata si trova nella cache oppure no?

È possibile risolvere questo problema aggiungendo alla cache un **campo di bit**, denominato "**tag**" o "**etichetta**". I tag contengono, sostanzialmente, **la parte superiore dell'indirizzo della parola in questione nella memoria principale**, e in particolare i bit dell'indirizzo che non sono stati utilizzati per mapparlo alla cache (inserire anche quest'ultimi risulterebbe ridondante). Tornando all'esempio precedente, dunque, nel tag di ogni parola occorrerebbe memorizzare solo i 2 bit più significativi, dato che i 3 bit inferiori sono stati utilizzati nella mappatura. Oltre al tag, è necessario prevedere anche un metodo per capire **quando un blocco della cache non contiene informazioni valide**: ad esempio, non appena un processore viene avviato, la sua cache è naturalmente vuota e dunque i valori contenuti al suo interno sono privi di significato. Comunemente, si aggiunge un **bit di validità**, o "**valid bit**", che se impostato a $1$ indica che il corrispondente elemento di cache contiene dati validi; nel caso in cui il bit di validità fosse $0$, la richiesta di lettura dell'elemento in questione non può avere successo.
___
##### Accesso alla cache

Supponiamo di avere una memoria cache di 8 blocchi inizialmente vuota, e di effettuare una **sequenza arbitraria di nove richieste di dati**. Nella seguente tabella, possiamo vedere l'esito e le locazioni di memoria di ciascuna di queste richieste:

![[cache_richieste_dati_esempio_tabella.png]]

Dato che la cache dispone di 8 blocchi, per la mappatura si utilizzano i 3 bit meno significativi dell'indirizzo in memoria (indicato nella seconda colonna). Notiamo che, essendo la cache inizialmente vuota, i primi due accessi costituiscono delle **[[La memoria#Gerarchia delle memorie|miss]]**: in particolare, a partire dallo stato iniziale della cache vuota:

![[cache_richieste_dati_esempio_tabella1.png]]

dopo la prima miss la parola desiderata viene caricata dal livello inferiore di memoria nell'elemento della cache ad indice $110$:

![[cache_richieste_dati_esempio_tabella2.png]]

Si noti che la colonna indicata con $V$ è quella dei bit di validità, dove $N$ indica che l'elemento non è valido e $S$ indica che lo è. Subito dopo, avviene una seconda miss, che porta al caricamento di una parola nell'elemento della cache ad indice $010$:

![[cache_richieste_dati_esempio_tabella3.png]]

Dopo queste due miss, le due richieste successive sono risultano in **hit**, dato che richiedono proprio i dati che sono stati caricati nella cache in seguito alle due richieste precedenti: perciò, non avvengono modifiche nell'assetto della cache. Per quanto riguarda la quinta e sesta richiesta, entrambe risultano in **miss**, dato che entrambe cercano di accedere ad elementi vuoti della cache; in particolare, la miss della quinta richiesta porterà al caricamento di una parola nell'elemento della cache ad indice $000$:

![[cache_richieste_dati_esempio_tabella4.png]]

La miss della sesta richiesta, invece, porterà al caricamento di una parola nell'elemento della cache ad indice $011$:

![[cache_richieste_dati_esempio_tabella5.png]]

La settima richiesta di dati fa riferimento al dato che è stato caricato nella quinta, dunque risulta in una **hit**. Lo stesso non si può dire dell'ottava, che risulta in una **miss**; in particolare, in questo caso l'indirizzo del dato da caricare è mappato a un blocco della cache dov'è già presente un dato (il blocco $010$), 
___

[pag. 352... 18, slide 16]