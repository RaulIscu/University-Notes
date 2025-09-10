## Gerarchia delle memorie

Fin dal principio dell'era dell'informatica, i programmatori hanno sempre agognato una memoria illimitata e al tempo stesso velocissima, che possa contenere tutti i dati che si desiderano e che possa permettere l'accesso ad essi in fretta. Naturalmente, una memoria che rispetti concretamente queste esigenze non esiste, ma ci sono varie tecniche che si possono utilizzare per creare una memoria che ci si avvicini il più possibile.

Una delle più importanti è il cosiddetto "**principio di località**". Così come uno studente, interessato a una determinata materia, non ha bisogno di dover consultare con la stessa probabilità tutti i libri di una biblioteca, così **un programma non deve accedere, con la stessa probabilità, a tutta la memoria a sua disposizione**. Di conseguenza, il principio di località afferma, in sostanza, che **un programma, in un certo istante di tempo, accede soltanto a una porzione relativamente piccola della memoria**. Questo principio può essere reinterpretato come l'unione di due sotto-principi, ossia:
- il principio di **località temporale**;
- il principio di **località spaziale**.

In particolare, il primo afferma che, **se si accede a una certa locazione di memoria, è probabile che vi si acceda di nuovo poco tempo dopo**; il secondo, invece, afferma che **se si accede a una certa locazione di memoria, è probabile che in seguito si acceda a locazioni vicine ad essa**. Questi principi emergono in modo spontaneo dalla struttura tipica dei programmi: ad esempio, all'interno di un ciclo, dati e istruzioni vengono ripetutamente letti dalla memoria, dimostrando un elevato livello di località temporale; inoltre, le istruzioni di un programma sono normalmente memorizzate in sequenza, portando in questo caso a una spiccata località spaziale.

La conoscenza di questi principi viene sfruttata per **strutturare la memoria di un [[AE01 - Il calcolatore#Da cosa è composto un calcolatore?|calcolatore]] in forma gerarchica**, rispettando quella che viene chiamata "**gerarchia delle memorie**".

La **gerarchia delle memorie** consiste in un insieme di **livelli di memoria**, ciascuno caratterizzato da una **diversa velocità di accesso** e una **diversa dimensione**. A parità di capacità, le memorie più veloci hanno tendenzialmente un costo più elevato per singolo bit rispetto a quelle più lente, dunque di solito sono più piccole. **La memoria più veloce e piccola è posta più vicino al processore**, mentre quella più lenta e grande è quella più "lontana" dallo stesso. Di conseguenza, anche i dati stessi sono organizzati in modo gerarchico: la totalità dei dati a disposizione si trova nel livello più basso della memoria, e tutti i livelli superiori contengono un sottoinsieme dei dati presenti nel livello sottostante.

Seppur una gerarchia delle memorie possa essere composta da più livelli, **i dati possono essere trasferiti solo tra due livelli vicini**: di conseguenza, poniamo la nostra attenzione su **due soli livelli di memoria**. Quello superiore, più vicino al processore, è naturalmente più piccolo e veloce dell'inferiore, più lontano dal processore. La **più piccola quantità di informazione che può essere presente o assente** su questa sotto-gerarchia a due livelli è denominata "**blocco**".

Se il dato richiesto dal processore è contenuto in uno dei blocchi presenti nel livello superiore, si dice che **la richiesta ha avuto successo**, e questo evento si denota con il termine "**hit**"; se, invece, il dato non viene trovato nel livello superiore della gerarchia, **la richiesta fallisce**, e questo evento si denota con il termine "**miss**". In quest'ultimo caso, per trovare il blocco contenente il dato cercato si dovrà accedere al livello inferiore della gerarchia delle memorie. Possiamo definire come "**hit rate**", o "**frequenza di hit**", la **frazione degli accessi alla memoria che hanno successo**, ossia in cui il dato richiesto viene trovato nel livello superiore della gerarchia considerata; spesso, l'hit rate viene utilizzato come **indice delle prestazioni delle gerarchie delle memorie**. Definiamo, poi, anche una "**miss rate**", o "**frequenza di miss**", che è semplicemente pari a $1 - hit\,\,rate$, e rappresenta la **frazione degli accessi alla memoria che falliscono**.

Poiché il motivo principale della scelta di adottare una gerarchia delle memorie è l'**aumento di prestazioni**, possiamo dedurre che un aspetto importantissimo sia la **velocità di accesso alla memoria**. In particolare, il "**tempo di hit**" è il tempo di accesso al livello superiore della gerarchia, e comprende anche il tempo necessario a stabilire se il tentativo si risolve in un successo (hit) o in un fallimento (miss); in caso di miss, la "**penalità di miss**" consiste nel tempo necessario a sostituire un blocco del livello superiore con un nuovo blocco, caricato dal livello inferiore della gerarchia, e a trasferire i dati contenuti in tale blocco al processore. Siccome il livello superiore è più piccolo e veloce, tendenzialmente **il tempo di hit sarò molto minore al tempo necessario per accedere al livello inferiore nella gerarchia**, tempo che rappresenta la componente più importante della penalità di miss.
___
## Tecnologie delle memorie

Al giorno d'oggi, vengono utilizzate principalmente **quattro tecnologie** per costruire delle memorie e, di conseguenza, una [[AE06 - La memoria#Gerarchia delle memorie|gerarchia delle memorie]]. 

Due di queste tecnologie sono la **DRAM**, o "**Dynamic Random Access Memory**", e la **SRAM**, o "**Static Random Access Memory**". Mentre la prima è la principale tecnologia utilizzata nelle **memorie RAM** dei calcolatori, la seconda è quella che va a comporre i livelli di memoria più vicini al processore, come la **[[AE06 - La memoria#La cache|cache]]**. Generalmente, **la DRAM ha un costo più basso per bit della SRAM, ma anche un accesso decisamente più lento**. La principale causa della differenza di costo è il fatto che le memorie DRAM utilizzano meno transistor per ogni bit da memorizzare, e riescono così a raggiungere una capacità superiore a parità di materiali utilizzati. La terza tecnologia di cui andremo a parlare è la **memoria flash**, che viene principalmente utilizzata nei **dispositivi mobili**. Infine, abbiamo i **dischi magnetici**, che vanno a comporre le memorie più capienti e dall'accesso più lento della gerarchia.

Per un'idea più completa delle prestazioni e dei costi di queste tecnologie, possiamo fare riferimento alla seguente tabella, che fornisce una media di questi valori nell'anno 2020:

![[costi_tempi_memorie_tabella.png]]

A questo punto, andiamo ad approfondire più nel dettaglio ciascuna delle tecnologie appena nominate.

##### SRAM

Le **memorie SRAM** sono, sostanzialmente, dei **circuiti integrati** organizzati come **vettori di memoria**; di solito, essi hanno **una sola porta d'accesso**, che può fornire sia la lettura che la scrittura dei dati della memoria. Le SRAM forniscono lo **stesso tempo di accesso per tutti i dati**.

In una SRAM, si utilizzano **da 6 a 8 transistor per bit**, in modo da evitare il più possibile interferenze o disturbi al momento della lettura. Inoltre, hanno bisogno di ricevere una **potenza minima**, in modo da mantenere la carica anche quando si trovano in stand-by.

In passato, la maggior parte dei PC e dei server utilizzava diversi chip di SRAM per diversi livelli di cache; ad oggi, tuttavia, le cache di tutti i livelli sono integrate nel processore, sostanzialmente eliminando il mercato delle SRAM singole.
___
##### DRAM

In una memoria [[AE06 - La memoria#SRAM|SRAM]], o RAM statica, il dato rimane memorizzato per tutto il tempo in cui l'alimentazione è attiva. Un comportamento diverso si ha in una **memoria DRAM**, o **RAM dinamica**, in cui il dato viene memorizzato come **carica in un condensatore**, e in cui di conseguenza **un solo transistor è sufficiente** per leggere o sovrascrivere il dato. 

L'utilizzo di un solo transistor per bit di dato memorizzato contribuisce a una **maggiore densità** e a un **costo minore** rispetto alle SRAM; tuttavia, l'utilizzo di un condensatore per memorizzare un bit rende tale memoria più "**volatile**", e rende necessario un **"refresh" periodico** della stessa. Per refreshare, o rinfrescare, una cella di memoria, occorre semplicemente **leggerne il contenuto e riscriverlo**. La carica, però, può essere mantenuta per pochi millisecondi, per cui rinfrescare i bit di una DRAM costantemente ed uno ad uno ruberebbe tempo all'accesso ai dati memorizzati in essa: per questo motivo, le DRAM utilizzano un'**architettura a due livelli**, che consente di **rinfrescare un'intera "riga" di memoria insieme**, mediante un ciclo di lettura seguito immediatamente da un ciclo di riscrittura. Per comprendere meglio la struttura di una DRAM, possiamo osservare la seguente rappresentazione:

![[struttura_dram.png]]

Una memoria DRAM moderna è organizzata in **banchi**, e ciascuno di essi è formato da una **serie di righe**. Inviando un "**comando di precaricamento**", si può aprire o chiudere un banco in particolare; per avviare, invece, il trasferimento del contenuto di una riga del banco in un buffer, si utilizza un "**comando di attivazione**". Una volta che il contenuto di una riga sarà trasferito nel buffer, si potrà accedere ai dati specificando gli indirizzi successivi di gruppi di bit, qualsiasi sia l'ampiezza della DRAM, oppure specificando l'indirizzo di partenza e l'intenzione di accedere all'intero buffer (funzionamento, per certi versi, analogo a quello delle SRAM). Questo approccio migliora significativamente il tempo di accesso.

Per migliorare ulteriormente l'interfaccia tra processori e DRAM, a quest'ultime è stato aggiunto un segnale di **clock**, motivo per cui un nome più appropriato per indicarle sarebbe "**DRAM sincrone**" o "**Synchronous DRAM**", in breve **SDRAM**. Il vantaggio di avere un clock integrato nella memoria sta nell'**eliminazione del tempo necessario a sincronizzare memoria e processore**.

Concretamente, il principale aumento di velocità delle SDRAM è dovuto alla possibilità di **trasferire gruppi di bit adiacenti a raffica**, o "**in burst**", senza la necessità di specificare ulteriori indirizzi di memoria. Questa modalità di trasferimento viene anche chiamata "**DDR**", o "**Double Data Rate**", nome che indica in particolare che il trasferimento dei dati avviene **sia sul positive-edge sia sul negative-edge del clock**, ottenendo così il doppio della larghezza di banda prevista inizialmente. La versione più recente di questa tecnologia è la **DDR4**: ad esempio, una DRAM di tipo DDR4-3200 può effettuare **3200 milioni di trasferimenti di dati al secondo**, che corrisponde a una frequenza di clock di **1600 MHz**.

Per sostenere una tale larghezza di banda, bisogna implementare alcune migliorie nell'organizzazione interna della DRAM. Ad esempio, invece di un unico buffer di riga, ogni banco dispone del proprio buffer, in modo che una DRAM possa leggere o scrivere da diversi banchi simultaneamente.
___
##### Memoria flash

Le **memorie flash**, che fanno parte delle memorie "**EEPROM**" (Electrically Erasable Programmable Read-Only Memory), sono un tipo di memoria cancellabile elettricamente e programmabile.

A differenza dei [[AE06 - La memoria#Disco magnetico|dischi]] e delle [[AE06 - La memoria#DRAM|DRAM]], **i bit delle memorie flash si deteriorano dopo un certo numero di scritture**. Per far fronte a questa limitazione, la maggior parte dei dispositivi che utilizzano memorie flash contiene un **controllore**, che distribuisce le scritture dai blocchi di memoria scritti più di frequente su blocchi scritti meno frequentemente, con una tecnica chiamata "**livellamento dell'usura**", o "**wear leveling**". Seppur utilizzare questo approccio vada a diminuire le prestazioni teoriche di una memoria flash, essa risulta pressoché necessaria per allungarne il ciclo di vita, e in certi casi anche utile dato che un controllore può identificare eventuale celle di memoria malfunzionanti.
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

Nella [[AE06 - La memoria#Gerarchia delle memorie|gerarchia delle memorie]] del primo calcolatore commerciale che implementava qualcosa del genere, il livello di memoria che si trova **tra il processore e la memoria principale** (dunque, quello più piccolo e più veloce) era detto "**cache**"; similmente, le memorie utilizzate nelle varie implementazioni di processore approfondite nel capitolo sulle [[AE05 - La CPU|CPU]] possono essere sostituite da **memorie cache**. 

Ad oggi, seppur la definizione appena fornita rimane la più utilizzata, questo termine viene talvolta esteso ad indicare sistemi di memoria gestiti in modo tale da ottenere i massimi benefici dalla località degli accessi.

##### Come funziona una cache?

In poche parole, una cache rappresenta **una memoria piccola e veloce, che si interfaccia direttamente con il processore, e in cui vengono memorizzati i dati più usati o più recentemente usati**. A livello simbolico, possiamo rappresentare una cache con il seguente schema:

![[cache_semp.png]]

Come possiamo vedere, la cache contiene vari dati ($X_{1}$, $X_{2}$, $X_{3}$, ecc. ecc.), che sono quelli utilizzati più di recente, ciascuno memorizzato in una delle sue $n$ **linee** (una singola linea può contenere più parole di dati). Supponiamo, ora, che il processore richieda una certa parola $X_{n}$: se il blocco di memoria corrispondente è presente nella cache, il dato viene caricato da essa e la richiesta di dati risulta in una **[[AE06 - La memoria#Gerarchia delle memorie|hit]]**; se, invece, il blocco non è presente attualmente nella cache, la richiesta di dati risulterà in una **[[AE06 - La memoria#Gerarchia delle memorie|miss]]**, e la parola $X_{n}$ verrà **prelevata dal livello inferiore di memoria** e **trasferita nella cache**. Nel nostro esempio, il dato non era presente nella cache, dunque in seguito alla richiesta lo schema della cache diventa più simile al seguente:

![[cache_semp1.png]]

Viene spontaneo, a questo punto, farsi alcune domande. Ad esempio, come si fa a sapere se un dato è presente nella cache? Oppure, supponendo che questo dato sia effettivamente contenuto in essa, come si fa a trovarlo? Per certi versi, le risposte a queste due domande sono collegate.

Supponiamo che **ogni parola della memoria possa essere scritta in una sola linea della cache**: il modo più semplice per rendere possibile ciò è associare una sola linea della cache a ogni parola della memoria, definendo una **corrispondenza tra i vari indirizzi di memoria e la loro linea della cache**. Adottando questo approccio, ammesso che la parola cercata si trovi effettivamente nella cache, sapremo dove trovarla. Quest'organizzazione della cache è detta "**a mappatura diretta**", o "**direct mapped cache**". Per questo tipo di cache, questa corrispondenza tra indirizzi di memoria e linee è di solito molto semplice: quasi tutte le cache a mappatura diretta, per trovare la **linea che corrisponde a un dato indirizzo della memoria principale**, utilizzano la seguente operazione (le doppie barre `//` indicano l'operazione di **modulo**, ossia il resto della divisione tra i due operandi):
$$\text{indirizzo del blocco in memoria } // \,\,\text{numero di linee nella cache}$$
Se il numero di linee della cache è una **potenza di 2**, allora l'indirizzamento può essere eseguito semplicemente considerando **i $\log_{2}\text{(numero di linee della cache)}$ bit meno significativi dell'indirizzo di memoria**. Per comprendere meglio come avvenga questa procedura, vediamo un esempio:

![[cache_mappatura_diretta_esempio.png]]

Nell'immagine, troviamo una **cache da 8 linee**, dove ovviamente si ha che $8 = 2^3$. Ciò vuol dire che, per indirizzare la memoria nella cache, sarà sufficiente considerare i $\log_{2}8 = 3$ bit meno significativi di tale indirizzo: sostanzialmente, **i bit meno significativi dell'indirizzo vengono utilizzati come indice della linea a cui sono mappati**. Vediamo, ad esempio, che il blocco con indirizzo $00001$ viene mappato alla linea $001$ della cache, mentre il blocco con indirizzo $01101$ viene mappato alla linea $101$ della cache, e così via.

Ora, però, sorge un altro dubbio: dato che ogni elemento della cache può contenere dati provenienti da diversi punti della memoria, come è possibile capire se il dato presente nella cache corrisponde alla parola desiderata? In altre parole, come facciamo a sapere se la parola desiderata si trova nella cache oppure no?

È possibile risolvere questo problema aggiungendo alla cache un **campo di bit**, denominato "**tag**" o "**etichetta**". I tag contengono, sostanzialmente, **la parte superiore dell'indirizzo della parola in questione nella memoria principale**, e in particolare i bit dell'indirizzo che non sono stati utilizzati per mapparlo alla cache (inserire anche quest'ultimi risulterebbe ridondante). Tornando all'esempio precedente, dunque, nel tag di ogni parola occorrerebbe memorizzare solo i 2 bit più significativi, dato che i 3 bit inferiori sono stati utilizzati nella mappatura. Oltre al tag, è necessario prevedere anche un metodo per capire **quando una linea della cache non contiene informazioni valide**: ad esempio, non appena un processore viene avviato, la sua cache è naturalmente vuota e dunque i valori contenuti al suo interno sono privi di significato. Comunemente, si aggiunge un **bit di validità**, o "**valid bit**", che se impostato a $1$ indica che il corrispondente elemento di cache contiene dati validi; nel caso in cui il bit di validità fosse $0$, la richiesta di lettura dell'elemento in questione non può avere successo.

Supponiamo di avere una memoria cache di 8 linee inizialmente vuota, e di effettuare una **sequenza arbitraria di nove richieste di dati**. Nella seguente tabella, possiamo vedere l'esito e le locazioni di memoria di ciascuna di queste richieste:

![[cache_richieste_dati_esempio_tabella.png]]

Dato che la cache dispone di 8 linee, per la mappatura si utilizzano i 3 bit meno significativi dell'indirizzo in memoria (indicato nella seconda colonna). Notiamo che, essendo la cache inizialmente vuota, i primi due accessi costituiscono delle **[[AE06 - La memoria#Gerarchia delle memorie|miss]]**: in particolare, a partire dallo stato iniziale della cache vuota:

![[cache_richieste_dati_esempio_tabella1.png]]

dopo la prima miss la parola desiderata viene caricata dal livello inferiore di memoria nell'elemento della cache ad indice $110$:

![[cache_richieste_dati_esempio_tabella2.png]]

Si noti che la colonna indicata con $V$ è quella dei bit di validità, dove $N$ indica che l'elemento non è valido e $S$ indica che lo è. Subito dopo, avviene una seconda miss, che porta al caricamento di una parola nell'elemento della cache ad indice $010$:

![[cache_richieste_dati_esempio_tabella3.png]]

Dopo queste due miss, le due richieste successive sono risultano in **hit**, dato che richiedono proprio i dati che sono stati caricati nella cache in seguito alle due richieste precedenti: perciò, non avvengono modifiche nell'assetto della cache. Per quanto riguarda la quinta e sesta richiesta, entrambe risultano in **miss**, dato che entrambe cercano di accedere ad elementi vuoti della cache; in particolare, la miss della quinta richiesta porterà al caricamento di una parola nell'elemento della cache ad indice $000$:

![[cache_richieste_dati_esempio_tabella4.png]]

La miss della sesta richiesta, invece, porterà al caricamento di una parola nell'elemento della cache ad indice $011$:

![[cache_richieste_dati_esempio_tabella5.png]]

La settima richiesta di dati fa riferimento al dato che è stato caricato nella quinta, dunque risulta in una **hit**. Lo stesso non si può dire dell'ottava, che risulta in una **miss**; in particolare, in questo caso l'indirizzo del dato da caricare è mappato a una linea della cache dov'è già presente un dato (l'elemento $010$), quindi si dovrà procedere alla sostituzione di quest'ultimo col dato appena richiesto:

![[cache_richieste_dati_esempio_tabella6.png]]

Infine, l'ultima richiesta di dati fa riferimento allo stesso blocco richiesto dalla settima, dunque risulta in una **hit**.

Come possiamo vedere anche dall'esempio appena analizzato, l'indice di una linea della cache, congiunto al contenuto del campo tag, specifica in maniera univoca l'indirizzo della memoria principale associato al dato memorizzato in tale linea. Poiché le parole sono allineate a multipli di 4 byte, e gli indirizzi sono riferiti ai singoli byte, **i due bit meno significativi dell'indirizzo specificano in realtà i byte all'interno di una stessa parola**; in questo contesto, selezionando una parola all'interno di una linea della cache è possibile ignorare i 2 bit meno significativi del suo indirizzo.
___
##### Cache con linee da più di una parola

Gli esempi forniti finora, così come le spiegazioni relative a tali esempi, supponevano delle cache semplici, in cui la dimensione di una singola linea corrispondeva a una parola, o 4 byte. Normalmente, tuttavia, **una linea di cache è costituita da più parole**. In questo contesto più realistico, il numero complessivo di bit necessari per realizzare una cache è funzione della **dimensione della cache** e della **dimensione degli indirizzi di memoria**; supponiamo, ad esempio, di avere la seguente situazione:
- indirizzi di memoria a **$32$ bit**;
- **cache a mappatura diretta**;
- dimensione della cache di **$2^{n}$ linee**, per cui vengono utilizzati $n$ bit per indicizzarle;
- dimensione di una singola linea della cache di **$2^{m}$ parole**, ossia di **$2^{m + 2}$ byte**, per cui vengono utilizzati $m$ bit per individuare una singola parola all'interno di una linea, e altri $2$ bit per individuare un byte all'interno di una parola.

In un contesto del genere, la dimensione del campo tag di una linea di cache è pari a:
$$32 - (n + m + 2)$$
ossia il numero di bit dell'indirizzo di memoria, a cui vengono sottratti gli $n$ bit dell'indice della linea, gli $m$ bit dell'indice della parola all'interno della linea, e i $2$ bit dell'indice del byte all'interno della parola. Il numero totale di bit contenuti in una cache a mappatura diretta, quindi, è pari a
$$2^{n} \cdot (\text{dimensione della linea} + \text{dimensione del tag} + \text{bit di validità})$$
Considerando che la dimensione della linea è di $2^{m}$ parole, dunque di $2^{m+5} = 2^{m} \cdot 32$ bit, che la dimensione del tag è $32 - (n + m + 2)$, e che naturalmente il bit di validità è costituito da un singolo bit, possiamo riscrivere la formula come:
$$\begin{align} 2^{n} \cdot (\text{dimensione della linea} + \text{dimensione del tag} + \text{bit di validità}) &= 2^n \cdot [(2^{m} \cdot 32) + (32 - n - m - 2) + 1] \\ &= 2^{n} \cdot (2^{m} \cdot 32 + 31 - n - m) \end{align}$$
Sebbene questa sia la dimensione reale della cache, per convenzione spesso si escludono dal calcolo i bit del campo tag e il bit di validità, considerando dunque **solo la dimensione dei dati effettivi**.

A questo punto, però, **mappare la memoria in una cache con linee da più di una parola** risulta leggermente più complesso. Supponiamo, ad esempio, di avere una cache con **64 linee da 4 parole** (o 16 byte) **ciascuna**, e di voler sapere a quale linea della cache venga mappato il dato all'indirizzo di memoria $1200$, espresso in byte. Facciamo appello all'operazione introdotta nel [[AE06 - La memoria#Come funziona una cache?|paragrafo precedente]], ossia
$$\text{(indirizzo del blocco in memoria) } \text{modulo} \,\text{(numero di linee nella cache)}$$
per trovare l'indice della linea di cache corrispondente. L'indirizzo del blocco si ottiene dividendo l'indirizzo del dato in questione per il numero di byte di un blocco:
$$\frac{1200}{16} = 75$$
Se volessimo, poi, sapere l'**offset** del dato all'interno del blocco, ossia l'indice del byte all'interno del blocco considerato, dovremmo effettuare un'operazione di modulo tra gli stessi operandi:
$$1200\,\,\text{modulo}\,\,16 = 0$$
Dunque, il byte desiderato è il primo byte della prima parola del blocco. A questo punto, avendo l'indirizzo in memoria del blocco a cui appartiene il dato richiesto, così come il numero di linee della cache, possiamo conoscere l'indice della linea a cui tale dato verrà mappato applicando proprio la formula ricordata poco fa:
$$75\,\,\text{modulo}\,\,64 = 11$$
In generale, **linee di dimensioni maggiori sfruttano maggiormente la [[AE06 - La memoria#Gerarchia delle memorie|località spaziale]]**, e dunque **diminuiscono la frequenza di miss**; tuttavia, **quest'ultima può tornare a crescere se la dimensione delle linee diventa troppo grande rispetto alla dimensione totale della cache**, dato che ciò porterebbe a un numero molto piccolo di blocchi memorizzabili al suo interno, e di conseguenza a una maggiore "competizione" per occupare questi pochi posti. Ciò porterebbe, in buona parte dei casi, alla sostituzione di un dato nella cache con uno nuovo prima ancora che sia stato utilizzato il precedente.

Un problema ancora più grave, sempre associato all'aumento della dimensione delle linee, è la **crescita della penalità di miss**: essa, infatti, è determinata dal tempo necessario a prelevare un blocco dal livello inferiore della gerarchia e a scriverlo nella cache, e questo tempo a sua volta è costituito principalmente dal tempo di trasferimento del blocco. Naturalmente, maggiori sono le dimensioni del blocco, maggiore sarà questo tempo. All'aumento delle dimensioni di un singolo blocco, dunque, tendenzialmente **l'aumento della penalità di miss ha un impatto maggiore della diminuzione della frequenza di miss**, senza contare il fatto che aumentando eccessivamente le dimensioni del blocco si ha anche un aumento di tale frequenza; tutti questi fattori portano a una **diminuzione delle prestazioni della cache**.
___
##### Come gestire le miss della cache?

Al termine del [[AE06 - La memoria#Cache con blocchi di più di una parola|paragrafo precedente]], si è stabilito che l'aumento delle dimensioni di una linea, se gestito male, può portare a una diminuzione delle prestazioni della cache dovuta soprattutto alle **miss**. Ma **in che modo**, in un [[AE05 - La CPU|processore]], **la control unit gestisce le miss all'interno della cache?**

Quello che deve fare la control unit, sostanzialmente, è **riconoscere il fallimento di una richiesta di dati**, e provvedere a **risolverlo prelevando dati dalla memoria principale o da una cache di livello inferiore**. Invece, se la richiesta di dati ha successo (hit), il processore continuerà l'elaborazione utilizzando il dato richiesto senza intoppi o interruzioni. Per quanto riguarda la gestione delle hit, non ci sarà bisogno di cambiamenti importanti nell'implementazione della control unit; la **gestione delle miss**, invece, richiede un'**unità di controllo separata**, che lavori a stretto contatto con il processore e che si occupi dell'**accesso alla memoria principale** e del **"rifornimento" della cache**. Per risolvere una miss, ottenendo il dato effettivamente richiesto, sarà necessario introdurre uno **stallo nella [[AE05 - La CPU#Pipeline|pipeline]]**, bloccando il contenuto dei registri per tutto il tempo necessario a caricare i dati dalla memoria principale. 

Vediamo, in particolare, come vengono gestite le **miss sulle istruzioni** (gli stessi meccanismi possono essere estesi anche per gestire le miss sui dati). Nel caso in cui l'accesso a un'istruzione si traduca in una miss, il contenuto di tale blocco sarà non valido; dunque, si dovrà eseguire un'**operazione di lettura nel livello inferiore di memoria**, in modo da caricare l'istruzione corretta nella cache. Dal momento che il PC viene incrementato di $4$ nel primo ciclo di clock di esecuzione, l'**indirizzo dell'istruzione** che ha generato la miss sarà pari a $PC - 4$. Ottenuto quindi questo indirizzo, sarà possibile leggere l'istruzione corrispondente dalla memoria principale, operazione che però impiegherà più cicli di clock; terminata l'attesa, **la parola contenente l'istruzione desiderata verrà scritta nella cache**.

Riassumiamo, dunque, i passi principali da seguire quando si verifica una miss nella cache delle istruzioni:
- inviare il valore originale del PC alla memoria principale;
- far eseguire alla memoria principale un'operazione di lettura, e attendere che essa venga completata;
- scrivere la parola trovata nella posizione opportuna della linea di cache, aggiornare il campo tag e impostare a $1$ il bit di validità;
- far ripartire l'esecuzione dell'istruzione dall'inizio, ripetendo lo stadio IF che stavolta troverà l'istruzione corretta all'interno della cache.

Le operazioni svolte nel caso di una miss nella **cache dei dati** sono essenzialmente identiche.
___
##### Come gestire la scrittura nella cache?

Supponiamo che venga eseguita un'istruzione `sw` che scriva un determinato dato solamente nella cache di dati, senza modificare la memoria principale. Si creerebbe un problema dato che, al termine della scrittura, **la memoria principale avrebbe un contenuto diverso da quello della cache** all'indirizzo di memoria indicato: si dice, dunque, che cache e memoria sono "**incoerenti**". Ma **come si può mantenere la coerenza tra queste due memorie?**

La soluzione più semplice a questa problematica consiste nello **scrivere sempre il dato in questione in entrambe le memorie**: questo approccio viene chiamato "**write-through**". Tuttavia, seppur funzionante, il write-through risulta essere particolarmente **inefficiente**. Ciò è dovuto proprio alla scrittura di dati in memoria, dato che scrivere una parola nella memoria principale potrebbe richiedere **almeno $100$ cicli di clock del processore**, rallentando considerevolmente l'esecuzione. Per ovviare a tale inefficienza, si può utilizzare una sorta di "memoria tampone", chiamata "**buffer di scrittura**". Il buffer di scrittura si occupa di **memorizzare i dati in attesa di scrittura in memoria**: in questo modo, dopo la scrittura di un dato nella cache e conseguentemente nel buffer di scrittura, all'interno del processore si potrà continuare con l'esecuzione e, una volta completata la scrittura del dato nella memoria principale, il corrispondente spazio nel buffer verrà liberato. Adottando questa soluzione, uno **stallo dell'esecuzione** risulterà **necessario solo quando il buffer sarà pieno e il processore dovrà eseguire un'operazione di scrittura**.

Un metodo alternativo al write-through è, invece, il cosiddetto "**write-back**": in questo schema, quando si verifica una scrittura **il dato viene scritto solamente nella cache**, e il blocco modificato viene **salvato nel livello di memoria inferiore solo quando deve necessariamente essere rimpiazzato**. Si tratta di una soluzione che può portare a un miglioramento delle prestazioni, ma che è anche più complessa da implementare rispetto al write-through.
___
##### Misurare le prestazioni della cache

Il **tempo di CPU**, nel suo complesso, può essere diviso nel tempo speso per l'**esecuzione di un programma** e in quello trascorso in **attesa di risposta dal sistema di memoria**. Di solito, si suppone che il costo degli accessi alla cache che risultano in hit rientri nei cicli di clock della normale esecuzione, dunque si ottiene che il tempo di CPU è dato dalla seguente formula:
$$\text{Tempo di CPU} = (\text{Cicli di esecuzione} + \text{Cicli di stallo della memoria}) \cdot \text{Durata di un ciclo di clock}$$

Semplificando, possiamo assumere che nella maggior parte dei casi **i cicli di stallo della memoria sono dovuti principalmente alle miss della cache**. In particolare, essi possono essere definiti come la somma degli stalli provocati dalle **letture** e di quelli provocati dalle **scritture**:
$$\text{Cicli di stallo della memoria} = \text{Cicli di stallo in lettura} + \text{Cicli di stallo in scrittura}$$
Per quanto riguarda i **cicli di stallo in lettura**, essi possono essere quantificati in funzione del numero di letture compiute in un programma, della frequenza di miss in lettura del processore in questione, e della penalità di miss in lettura:
$$\text{Cicli di stallo in lettura} = \text{Letture} \cdot \text{Frequenza di miss in lettura} \cdot \text{Penalità di miss in lettura}$$
Invece, per i **cicli di stallo in scrittura** (in un sistema write-through) vanno considerati sia i regolari miss di scrittura, sia gli stalli dovuti alla saturazione del buffer di scrittura. In questo caso, dunque, la formula diventa:
$$\text{Cicli di stallo in scrittura} = (\text{Scritture} \cdot \text{Frequenza di miss in scrittura} \cdot \text{Penalità di miss in scrittura}) + \text{N° di stalli del buffer di scrittura}$$

Dato che gli **stalli dovuti al buffer di scrittura** dipendono non solo dalla frequenza delle scritture, ma anche da quanto esse sono ravvicinate nel tempo, non è possibile fornire una semplice equazione generale per calcolare il numero di questi stalli. Fortunatamente, però, in un sistema di memoria dotato di buffer di scrittura progettato bene, questi stalli dovrebbero essere molto rari, e perciò **trascurabili**; un sistema dove ciò non avviene può essere considerato mal progettato, e avrebbe beneficiato di una maggiore profondità del buffer di scrittura oppure di un approccio write-back.

In molte cache di tipo write-through, **le penalità di miss in lettura e in scrittura sono uguali**, ed entrambe corrispondono al **tempo richiesto per prelevare un blocco dalla memoria principale**. Supponendo che gli stalli provocati dal buffer di scrittura siano trascurabili, è possibile dunque semplificare le equazioni fornite in precedenza, arrivando a una nuova formulazione per il numero di cicli di stallo della memoria:
$$\begin{align} \text{Cicli di stallo della memoria} &= \text{Accessi alla memoria} \cdot \text{Frequenza di miss} \cdot \text{Penalità di miss} \\ &= \text{N° di miss} \cdot \text{Penalità di miss} \end{align}$$

Proviamo ad applicare concretamente le formule appena ricavate per determinare le prestazioni di una cache. Supponiamo di avere un processore che disponga di una cache istruzione e di una cache dati, tali per cui la prima ha una frequenza di miss del $2\%$, mentre la seconda del $4\%$; si supponga, poi, che il processore abbia idealmente (ossia quando non si verificano stalli dovuti alla memoria) un CPI di 2, e che in generale la penalità di miss sia pari a $100$ cicli di clock. Infine, si supponga che la percentuale delle istruzioni di accesso alla memoria sul totale delle istruzioni sia del $36\%$. Cominciamo ricavano il numero di cicli di stallo spesi per gestire le miss delle istruzioni:
$$\text{Cicli di stallo per le istruzioni} = I \cdot 2\% \cdot 100 = 2 \cdot I$$
Posto che $I$ sia pari al numero totale di istruzioni, abbiamo che in media l'accesso alla cache istruzioni causa **2 cicli di clock di stallo per istruzione**. Passiamo ora ai cicli di stallo spesi per gestire le miss dei dati:
$$\text{Cicli di stallo per i dati} = I \cdot 36\% \cdot 4\% \cdot 100 = 1.44 \cdot I$$
In questo caso, otteniamo che in media l'accesso alla cache dati causa **1.44 cicli di clock di stallo per istruzione**. A questo punto, possiamo affermare che il numero totale di **cicli di clock di stallo dovuti alla memoria** è di **3.44 cicli per istruzione**; di conseguenza, il CPI totale è pari a $2 + 3.44 = 5.44$. Notiamo, dunque, che se il processore fosse dotato di una cache ideale, le sue prestazioni sarebbero quasi **3 volte migliori**.

Che cosa succederebbe, però, se **rendessimo il processore più veloce lasciando invariato il sistema di memoria**? In questo caso, secondo la legge di Amdahl, **la quantità di tempo spesa negli stalli della memoria aumenterà in relazione al tempo totale**, diventando ancora di più la parte preponderante dello stesso. Un risultato molto simile si otterrebbe aumentando la frequenza di clock senza modificare, anche in questo caso, il sistema di memoria.

Tutte le formule e gli esempi visti in precedenza in questo paragrafo sono basati sull'ipotesi che il **tempo di hit** non sia un fattore significativo nel calcolo delle prestazioni di una cache; tuttavia, se il tempo di hit aumentasse, farebbe lo stesso anche il tempo totale richiesto per accedere a una parola del sistema di memoria, facendo verosimilmente crescere anche la durata di un ciclo di clock. Per tenere conto del fatto che il tempo di accesso ai dati influenza le prestazioni sia in caso di hit che di miss, i progettisti utilizzano a volte l'**AMAT** ("**Average Memory Access Time**") per esaminare e confrontare cache diverse. Questo tempo è dato dalla seguente formula:
$$AMAT = \text{Durata di una hit} + (\text{Frequenza di miss} \cdot \text{Penalità di miss})$$

Un altro fattore impattante sulle prestazioni di una cache è la sua **dimensione**. **Una cache più grande**, infatti, **avrà bisogno di un tempo di accesso maggiore**.
___
##### Cache fully-associative

Finora, da quando abbiamo cominciato ad analizzare nel dettaglio il [[AE06 - La memoria#Come funziona una cache?|funzionamento di una cache]], abbiamo utilizzato uno schema "**a mappatura diretta**", detto anche "**direct mapping**", in cui esiste una mappatura diretta tra indirizzi della memoria principale e singole linee della cache. Questo approccio, però, non è l'unico per determinare la posizione di un blocco di dati, e alcune alternative possono portare a una **riduzione della frequenza di miss**.

Se una cache a mappatura diretta prevede che ogni indirizzo di memoria sia mappato a una determinata linea della cache, la prima alternativa che andremo ad approfondire, ossia la **cache "completamente associativa"**, o "**fully-associative**", fa l'esatto opposto. Una memoria cache di questo tipo permette che **un blocco di dati della memoria principale possa essere scritto in una qualsiasi linea della cache**. Per trovare un certo blocco di dati in una cache di questo tipo, la ricerca deve essere effettuata su tutte le linee della stessa, e per rendere più efficace tale ricerca essa viene svolta **in parallelo** utilizzando un **comparatore** per ogni blocco della cache. Seppur questa soluzione fornisca **massima flessibilità**, per farla funzionare è necessario **hardware più complesso e più costoso**.
___
##### Cache set-associative

Vi è un'ulteriore alternativa, un approccio intermedio tra mappatura diretta e [[AE06 - La memoria#Cache fully-associative|associatività completa]], ossia la cosiddetta **cache "set-associative"**. In una cache set-associative, **ogni blocco della memoria principale può essere scritto in un numero prefissato** (almeno 2) **di posizioni alternative**; in particolare, una cache set-associative con $n$ possibili scelte di posizione è chiamata "**set-associative a $n$ vie**", dunque una cache set-associative a $n$ vie è costituita da un certo numero di **insiemi**, o **set**, ciascuno dei quali raccoglie al suo interno **$n$ linee** provenienti ciascuna da una via diversa. In questo contesto, ogni blocco della memoria principale viene mappato a un unico set della cache, individuato dal campo **indice**, e potrà essere scritto in una qualsiasi delle linee costituenti il set.

Come abbiamo già visto, la linea di destinazione nella cache di un blocco di dati della memoria principale in una cache a mappatura diretta si ottiene con la seguente formula:
$$(\text{numero del blocco in memoria})\,\,\text{modulo}\,\,(\text{numero di linee nella cache})$$
Invece, in una cache set-associative, per sapere **il set di destinazione di un blocco di dati della memoria principale** la formula diventa:
$$\text{(numero del blocco in memoria)}\,\,\text{modulo}\,\,\text{(numero di set nella cache)}$$
In questo caso, dato che il blocco di dati può essere scritto in una qualsiasi delle linee del suo set, la ricerca deve essere effettuata analizzando il campo tag di tutte le linee del set.

Di seguito, un insieme di esempi di cache set-associative con **diversi gradi di associatività**, dove essa aumenta all'aumentare delle vie (notiamo che una cache a mappatura diretta può essere interpretata come una cache set-associative a una via, mentre una cache fully-associative può essere interpretata come una cache set-associative con un solo set):

![[cache_setassociative_esempi.png]]

Il principale **vantaggio dell'aumento del grado di associatività** è, in genere, una **diminuzione della frequenza di miss**; parallelamente, però, all'aumentare dell'associatività vi è anche uno **svantaggio**, ossia il **potenziale aumento del tempo di hit**.

Per comprendere meglio come il grado di associatività influenza la frequenza di miss, vediamo un **esempio**. Consideriamo **tre cache** di piccole dimensioni, ciascuna costituita da **4 linee da una parola** ciascuna: in particolare, la prima cache è **fully-associative**, la seconda è **set-associative a 2 vie** e la terza è **a mappatura diretta**. A questo punto, supponiamo di voler determinare il **numero di miss** nelle tre casistiche quando vengono richiesti i blocchi di memoria con la seguente sequenza di indirizzi: $0, 8, 0, 6, 8$.

Partiamo dall'ultima cache, quella **a mappatura diretta**. Determiniamo, innanzitutto, a quali linee della cache corrispondano i diversi indirizzi dell'esempio:

![[cache_associatività_esempio.png]]

A questo punto, vediamo cosa succede in risposta a ciascuna richiesta della sequenza, e schematizziamo il tutto in una tabella (le linee non valide sono vuote, e i dati appena scritti nella cache sono indicati in arancione):

![[cache_associatività_esempio1.png]]

Come si può notare, la cache a mappatura diretta genera **5 miss su 5 richieste di dati**: la **1°** richiede un dato da una linea non valida, ossia la prima; la **2°** richiede un dato diverso da quello già contenuto nella prima linea; la **3°** ha lo stesso comportamento della 2°; la **4°**, come la 1°, richiede un dato da una linea non valida, ossia la terza; infine, la **5°** ha nuovamente lo stesso comportamento della 2°.

Vediamo ora come si comporta la cache **set-associative**. Come detto in precedenza, si tratta di una cache set-associative a 2 vie, dunque formata da 2 set di 2 linee ciascuno. Determiniamo, innanzitutto, a quali set della cache (e quindi, a quali linee) corrispondano i diversi indirizzi dell'esempio:

![[cache_associatività_esempio2.png]]

Ora, dato che in caso di miss si può scegliere quale linea del set sostituire, è necessario stabilire una modalità di sostituzione: solitamente, le cache set-associative sostituiscono il blocco di dati contenuto nella linea aggiornata meno di recente. A questo punto, utilizzando questa modalità, vediamo cosa succede in risposta a ciascuna richiesta della sequenza, e schematizziamo nuovamente il tutto in una tabella:

![[cache_associatività_esempio3.png]]

Come si può notare, la cache set-associative a 2 vie genera **4 miss su 5 richieste di dati**: la **1°** richiede un dato da un set con solo linee non valide; la **2°** richiede un dato non presente nel set considerato; la **3°** richiede un dato effettivamente presente nel set considerato, e ha dunque successo; la **4°** richiede un dato non presente nel set considerato, dunque va a sostituire il blocco di dati della linea utilizzata meno di recente con quello richiesto; infine, la **5°** ha lo stesso comportamento della 4°.

Infine, analizziamo il comportamento della cache **fully-associative**. Dato che un qualsiasi blocco di dati della memoria può essere scritto in qualsiasi linea della cache, non sarà necessario alcun indirizzamento. A questo punto, vediamo cosa succede in risposta a ciascuna richiesta della sequenza, e schematizziamo ancora una volta il tutto in una tabella:

![[cache_associatività_esempio4.png]]

Come si può notare, la cache fully-associative genera **3 miss su 5 richieste di dati**: la **1°** richiede un dato non presente nella cache; la **2°** ha lo stesso comportamento della **1°**; la **3°** richiede un dato effettivamente presente nella cache, e ha dunque successo; la **4°** ha nuovamente lo stesso comportamento della 1°; infine, la **5°** ha successo.

Delle tre cache analizzate, quella fully-associative ha generato il minor numero di miss, cioè 3, che era anche il miglior risultato ottenibile (vengono richiesti dati da 3 indirizzi di blocco di memoria diversi); è confermata, così, la regola per cui **all'aumentare del grado di associatività tende a diminuire la frequenza di miss**. Per comprendere veramente quanto ciò sia vero anche in contesti reali, di seguito si riporta una tabella recante le frequenze di miss in una cache di dati con associatività variabile da 1 a 8 vie, grande $64\text{ KiB}$ ($1\text{ KiB} = 1024\text{ byte}$) e dotata di linee da 16 parole ciascuna:

![[cache_associatività_esempio5.png]]

Ora passiamo ad analizzare aspetti più concreti di una cache set-associative, ad esempio **come viene trovato un blocco di dati al suo interno**. Proprio come in una cache a mappatura diretta, ogni blocco di dati scritto nella cache è abbinato a un campo tag, che permette di individuarne l'indirizzo in relazione alla memoria principale; in particolare, un indirizzo di memoria in cache set-associative o a mappatura diretta rispecchia la seguente struttura:

![[cache_setassociative_indirizzo.png]]

Il campo **tag** viene controllato per verificare se corrisponde a quello dell'indirizzo del dato o dell'istruzione richiesta dal processore. Il contenuto del campo **indice**, invece, serve a selezionare e indicare il set che può contenere l'elemento cercato. Infine, il campo **offset di blocco** rappresenta la posizione del dato desiderato all'interno del blocco di dati. 

Oltre a questo indirizzo, nella cache vanno ovviamente memorizzati anche i dati effettivi. Riassumiamo, quindi, la struttura di una cache e come calcolarne le dimensioni: una cache set-associative a $n$ vie contiene **$S$ set**, ciascuno dei quali composto da **$n$ linee**, contenenti **blocchi di dati da $m$ word**; la dimensione effettiva di ogni linea è data dalla somma di:
- un **bit di validità**;
- il **tag**;
- l'**indice**;
- l'**offset di blocco**;
- il **blocco di dati** in sé.

Per calcolare i bit necessari per l'**indice** (che rappresenta l'indice del set all'interno del quale ci si trova) basterà calcolare il valore: $$\log_{2}S$$Per calcolare i bit necessari per l'**offset di blocco** (che rappresenta la posizione del dato in questione prima tra le word del blocco, poi tra i byte della word), invece, si calcolerà il valore: $$\log_{2}(m \cdot 4) = \log_{2}(m) + 2$$La dimensione del **tag**, di conseguenza, supponendo di avere una memoria con indirizzi da 32 bit, sarà pari a: $$32 - \text{n° di bit dell'indice} - \text{n° di bit dell'offset}$$Per quanto riguarda il **blocco di dati** effettivo, esso avrà dimensioni pari a:
$$m \cdot 32$$
Il contenuto del campo tag viene esaminato **in parallelo** per tutti i blocchi dell'insieme selezionato, dato che una ricerca sequenziale richiederebbe un tempo molto maggiore. Supponendo di mantenere costante la dimensione totale della cache, abbiamo visto che **al crescere dell'associatività aumenta il numero di linee di un singolo set**, e di conseguenza anche **il numero di confronti da effetturare in parallelo per trovare il dato richiesto**: ogni volta che raddoppia il grado di associatività, raddoppia anche il numero di linee all'interno di un singolo set, mentre viene dimezzato il numero di quest'ultimi. Analogamente, ogni incremento dell'associatività di un fattore 2 fa diminuire di 1 bit la dimensione del campo indice, e aumentare di 1 bit quella del campo tag: perciò, in una cache fully-associative, in cui è presente un solo set e quindi tutte le linee vanno esaminate in parallelo, il campo indice non esiste più e la ricerca viene condotta su tutta la cache.

In una cache a mappatura diretta, si richiede **un unico comparatore**, dato che il dato cercato può trovarsi in una sola posizione. Invece, in una cache set-associative a $n$ vie, saranno necessari **$n$ comparatori**, oltre a un **multiplexer con $n$ ingressi e un'uscita** richiesto per scegliere uno dei quattro possibili blocchi di dati da restituire. Dunque, l'accesso alla cache avviene innanzitutto tramite l'**indice**, in modo da individuare il set appropriato, e in seguito esaminando in parallelo i **tag** dei vari dati contenuti nelle linee di tale set. Possiamo visualizzare meglio questo meccanismo con la seguente rappresentazione:

![[cache_setassociative_circuito.png]]

Capiamo, adesso, **come scegliere il blocco di dati da sostituire** quando si verifica una miss. Infatti, se in una cache a mappatura diretta questa scelta poteva avere un unico risultato, in una cache set-associative **tutti i blocchi del set considerato sono possibili candidati per la sostituzione**. 

Comunemente, si utilizza un approccio detto **LRU**, o "**Least Recently Used**": il blocco sostituito è quello rimasto inutilizzato più a lungo (è lo stesso approccio che si è utilizzato nello scorso esempio). A livello rudimentale, si può implementare questa soluzione associando ad ogni linea di un set un **bit `Used`**, che viene impostato a $1$ quando si accede a tale linea e che viene reimpostato a $0$ dopo un certo intervallo di tempo.

Un'altra alternativa è l'approccio detto **LFU**, o "**Least Frequently Used**": in questo caso, il blocco sostituito è quello meno utilizzato. Per implementare questa soluzione, si potrebbe associare un **contatore** a ciascuna linea ed aggiornarlo ad ogni accesso; fare ciò, tuttavia, richiede hardware più complesso.

Ancora, si potrebbe semplicemente **sostituire un blocco "casuale"**, o magari sostituire i blocchi **in sequenza**.
___
##### Cache multilivello

L'utilizzo delle cache, naturalmente, porta come vantaggio primario di **ridurre il gap tra l'elevata frequenza di clock del processore e il molto più lento accesso alla memoria principale**. Spesso, per migliorare ancora di più questa situazione, un processore può supportare un **livello di cache aggiuntivo**. Di solito, questo secondo livello di cache si trova sullo stesso chip del processore, e viene utilizzato quando si verifica una miss all'interno della cache primaria: se il secondo livello di cache contiene il dato desiderato, allora **la penalità di miss sarà essenzialmente pari al tempo di accesso ad esso**; se, invece, il dato desiderato non è contenuto neanche nel secondo livello, è inevitabile l'accesso alla memoria principale e una **penalità di miss elevata**. Una cache divisa in più "livelli", come quella ipotizzata finora, viene detta "**cache multilivello**".

Per comprendere meglio come implementare una cache multilivello possa migliorare le prestazioni di un processore, vediamo un esempio. Supponiamo di disporre di un processore con frequenza di clock pari a 4 GHz e con un CPI di $1$ (se non si considerano le miss); supponiamo poi che il tempo di accesso alla memoria principale, che comprende tutto il tempo richiesto per gestire la miss corrispondente, sia di $100\,\,ns$, e che la frequenza di miss della cache sia pari al $2\%$ delle istruzioni. La penalità di miss per la memoria principale sarà pari a:
$$\frac{100\,\,ns}{0.25\,\,\frac{ns}{\text{ciclo di clock}}} = 400 \text{ cicli di clock}$$
Dunque, il numero medio di cicli di stallo per istruzione è pari a:
$$400 \cdot 2\% = 8$$
il che porta il CPI totale a:
$$\text{CPI totale = CPI di base + n° di cicli di stallo per istruzione = 1 + 8 = 9}$$
Supponiamo, ora, di introdurre anche una cache secondaria, con tempo di accesso pari a $5\,\,ns$ sia in caso di hit che di miss, e grande a sufficienza da ridurre la frequenza di miss della memoria principale allo $0.5\%$. La penalità di miss per la cache secondaria sarà pari a:
$$\frac{5\,\,ns}{0.25 \frac{ns}{\text{ciclo di clock}}} = 20 \text{ cicli di clock}$$
Se la miss viene risolta dalla cache secondaria, questo tempo costituisce la penalità di miss totale; invece, se la miss richiede anche l'accesso alla memoria principale, il tempo totale di miss sarà dato dalla somma del tempo di accesso alla cache secondaria e di quello alla memoria principale. Dunque, il nuovo CPI totale sarà dato da:
$$\begin{align} \text{CPI totale} &= \text{CPI di base} + \text{n° di stalli primari per istruzione} + \text{n° di stalli secondari per istruzione} \\ &= 1 + (20 \cdot 2\%) + (400 \cdot 0.5\%) \\ &= 1 + 0.4 + 2 = 3.4 \end{align}$$
Notiamo, dunque, che **l'introduzione di una cache multilivello ha portato a un miglioramento significativo delle prestazioni**, arrivando quasi a triplicare la velocità d'esecuzione del processore.

Le considerazioni da fare in fase di progettazione sono molto diverse per la cache primaria e per la cache secondaria: in particolare, una cache a due livelli permette di progettare la **cache primaria** focalizzandosi sulla **minimizzazione del tempo di hit**, in modo da ottenere un periodo di clock più breve oppure un numero minore di stadi di [[AE05 - La CPU#Pipeline|pipeline]], e di progettare la **cache secondaria** focalizzandosi sulla **frequenza di miss**, per ridurre la penalità dovuta ai lunghi tempi di accesso alla memoria principale.
___
## Memoria virtuale

Nel [[AE06 - La memoria#La cache|capitolo precedente]], abbiamo visto come le memorie cache forniscano un accesso veloce a una porzione di dati e istruzioni contenuti nella memoria principale, e in particolar modo a quei dati utilizzati più di recente o più frequentemente. Allo stesso modo, **anche la memoria principale può fungere da "cache" per la memoria di massa**, secondo una tecnica chiamata "**memoria virtuale**".

Ci sono principalmente due motivazioni che giustificano l'utilizzo di questa tecnica:
- favorire una **gestione efficiente e sicura della memoria** in corrispondenza dell'esecuzione di più programmi e processi;
- **estendere**, almeno apparentemente, **i limiti** posti dalla cache e dalla memoria principale **in termini di quantità di dati**.

In parole povere, la memoria virtuale si occupa di gestire automaticamente i due livelli della [[AE06 - La memoria#Gerarchia delle memorie|gerarchia]] costituiti dalla **memoria principale**, chiamata anche "**memoria fisica**" per distinguerla da quella virtuale, e dalla **memoria di massa**.

I concetti che stanno alla base della memoria virtuale sono simili a quelli della cache. Un **blocco della memoria virtuale** viene definito "**pagina**", di conseguenza le **miss di una memoria virtuale** sono dette "**page fault**". Sostanzialmente, quando si utilizza la memoria virtuale, il processore genera **indirizzi virtuali**, che vengono poi tradotti da una combinazione di hardware e software in **indirizzi fisici**, che possono essere utilizzati per accedere alla vera posizione dei dati. Possiamo visualizzare questo procedimento con la seguente rappresentazione:

![[memoria_virtuale.png]]

Come si può vedere, mentre il processore genera indirizzi virtuali l'accesso effettivo alla memoria viene svolto attraverso indirizzi fisici; inoltre, sia la memoria virtuale che la memoria fisica sono suddivise in pagine, in modo tale che una pagina virtuale venga mappata su una pagina fisica. È possibile, naturalmente, che una pagina virtuale non sia presente nella memoria principale, e in tal caso essa dovrà trovarsi nel disco. Le pagine fisiche, poi, possono essere condivise facendo in modo che due indirizzi virtuali puntino allo stesso indirizzo fisico: in questo modo, ad esempio, due diversi programmi potranno condividere dati o codice.

Questo processo di mappatura tra memoria virtuale e fisica prende il nome di "**traduzione dell'indirizzo**", o anche "**mappatura dell'indirizzo**". 
___
[pag. 392... - 19, slide 15/17 - 19, slide 22 - 20, slide 12]