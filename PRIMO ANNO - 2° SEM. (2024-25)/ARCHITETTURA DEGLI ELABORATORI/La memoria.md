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

Una memoria DRAM moderna è organizzata in **banchi**, e ciascuno di essi è formato da una **serie di righe**. Inviando un "**comando di precaricamento**", si può aprire o chiudere un banco in particolare; per avviare, invece, il trasferimento del contenuto di una riga del banco in un buffer, si utilizza un "**comando di attivazione**". Una volta che il contenuto di una riga sarà trasferito nel buffer, si potrà accedere ai dati specificando gli indirizzi successivi di gruppi di bit, qualsiasi sia l'ampiezza della DRAM, oppure specificando l'indirizzo di partenza e l'intenzione di accedere all'intero buffer (funzionamento, per certi versi, analogo a quello delle SRAM).



[pag. 344 - 345 - 346]
___
##### Memoria flash

[pag. 346]
___
##### Disco magnetico

[pag. 346 - 347 - 348]
___

[pag. 344... 18, slide 4]