Finora, ci siamo concentrati sulle varie caratteristiche del [[BD1_01 - Modello relazionale#Cos'è il modello relazionale?|modello relazionale]], sui vincoli che possiamo porre al suo interno, e su come creare dei database strutturati correttamente. All'inizio del corso, abbiamo accennato al fatto che i database vengono generalmente gestiti attraverso dei **DBMS**, o **Database Management System**, ma **cos'è concretamente un DBMS**?

Un DBMS completo e ben strutturato è, in realtà, un connubio di **più parti che lavorano in sincrono**, e che si occupano di varie mansioni, tra cui:
- un **gestore di memoria**;
- un **processore di query relazionali**;
- un **gestore delle comunicazioni con il client**;
- un **gestore dei processi**;
- vari **strumenti di utilità**.

Momentaneamente, andremo a focalizzarci soprattutto sul funzionamento delle prime due componenti elencate, ossia quelle che vengono anche definite rispettivamente "**strato fisico**" e "**strato logico**". 

[nello strato logico, invece, ci si concentra sulla **lettura**, **elaborazione**, **ottimizzazione** ed **esecuzione delle query**. ]

## Strato fisico

Nello strato fisico si trovano tutti quegli strumenti e componenti che si occupano della **gestione della memoria** concreta, dunque dei dati contenuti nel database (qui troviamo il gestore di memoria, vari buffer, metodi di accesso, ecc. ecc.). Possiamo schematizzare la struttura di questo blocco del DBMS nel modo seguente:

![[stratofisico_struttura.png]]

Per approfondire il funzionamento e la struttura dello strato fisico, partiamo dalla base, cioè dall'**hardware di memoria**, utilizzato per conservare i dati. Quando si parla di memoria, un concetto fondamentale da conoscere è quello di "**gerarchia delle memorie**", ossia della struttura gerarchica in cui tipicamente si distribuiscono i vari livelli di memoria contenuti in un computer. Nell'ipotetica piramide formata da quest'ultimi:
- la **cima** è composta da **memorie più veloci**, ma anche **costose** e **piccole**;
- il **fondo** è composto da **memorie più lente**, ma anche **meno costose** e **più grandi**.

Le memorie più veloci vanno a comporre quella che possiamo definire "**memoria primaria**", o anche "**memoria volatile**", e in ordine crescente di grandezza qui troviamo tipicamente i **registri della CPU**, le **cache** (piccole memorie direttamente collegate alla CPU, che operano quasi alla sua stessa velocità), la **memoria principale** (chip di RAM, più lenti della cache ma anche molto più capienti, che fungono da ponte tra le memorie a disco e la CPU). Quelle più lente, invece, compongono la cosiddetta "**memoria secondaria**", o anche "**memoria persistente**", e qui troviamo tipicamente **HDD** (Hard Disk Drive), **SSD** (Solid State Drive) o altre memorie fisiche ad alta capienza. Ricontestualizzando il tutto nell'ambito di un database, la memoria primaria sarà destinata a contenere **buffer del database** e **codice da eseguire relativo ad applicazioni e altre componenti del DBMS**, mentre la memoria secondaria conterrà **i file del database**.

##### Hard Disk Drives

Facciamo un approfondimento sugli **Hard Disk Drives**, o **HDD** in breve. Si tratta di dispositivi di memoria direttamente accessibili, o di **DASD** in breve, e per contenere i dati sfruttano dei **dischi circolari coperti da particelle magnetiche**, che sono **fissati su un perno che ruota**, quando l'HDD viene utilizzato, **a una velocità costante**; per leggere e scrivere dati su questi dischi, nell'HDD sono presenti anche delle **testine posizionate all'apice di alcuni bracci**, che all'occorrenza vengono messe a contatto con i dischi. A loro volta, i bracci sono fissati a un cosiddetto **attuatore**, che permette di muoverli avanti o indietro per accedere a parti diverse di memoria. È possibile schematizzare la struttura appena descritta nel modo seguente:

![[hdd_struttura.png]]

Ma **quanto tempo ci vuole per leggere o scrivere dei dati con un HDD**? Seguendo la struttura che abbiamo visto, deduciamo che la lettura o scrittura di qualsiasi dato implica innanzitutto il **corretto posizionamento dell'attuatore**, in modo da allineare le testine con la traccia desiderata del disco, e il tempo utilizzato per ottenere ciò viene detto "**seek time**"; a questo punto, si dovrà aspettare che **il settore desiderato del disco ruoti fino ad arrivare sotto la testina**, e questo ulteriore ritardo viene invece denominato "**rotation delay**"; inoltre, c'è anche da considerare un "**transfer time**", che dipende dalla **grandezza del blocco di memoria considerato**, dalla **densità delle particelle magnetiche** che ricoprono i dischi e dalla **velocità di rotazione dei dischi**. Tutti i tempi citati finora contribuiscono al cosiddetto "**service time**", che costituisce dunque il tempo di "risposta" di un HDD quando si vuole leggere o scrivere qualcosa, ma il tempo di risposta effettivo (il "**response time**"), è in realtà dato dalla somma tra il service time e il "**queueing time**", ossia il ritardo dovuto allo scheduling delle varie operazioni che il calcolatore dovrà svolgere.

Considerando la sequenza di operazioni svolte dall'HDD, possiamo stimare approssimativamente con delle formule matematiche il **tempo necessario per leggere o scrivere blocchi di memoria**; per fare ciò, distinguiamo però tra due tipi di accessi, ossia:
- **RBA**, o **Random Block Access**;
- **SBA**, o **Sequential Block Access**.

La principale differenza tra i due sta nella diversa posizione delle testine, e dunque nel seek time: infatti, un RBA è un accesso a un blocco generico di memoria dove si assume che le testine debbano effettivamente spostarsi per raggiungerlo, e dunque tiene conto del seek time; al contrario, un SBA è un accesso sequenziale a blocchi di memoria contigui, dunque si assume che le testine siano già posizionate sulla traccia giusta e perciò il seek time non viene più considerato.

Indichiamo il tempo necessario per un RBA con $T_{RBA}$, e quello necessario per un SBA con $T_{SBA}$, e questi due valori potranno essere ottenuti con le seguenti formule:
$$T_{RBA}=\text{seek time}+\frac{ROT}{2}+\frac{BS}{TR}\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,T_{SBA}=\frac{ROT}{2}+\frac{BS}{TR}$$
dove con $ROT$ si intende il **tempo di rotazione** di un disco, con $BS$ la **grandezza del blocco di memoria** e con $TR$ il "**transfer rate**", ossia l'ammontare di memoria trasferito per unità di tempo.
___
##### Da concetti logici a blocchi di dati fisici

Naturalmente, lavorando con [[BD1_04 - Organizzazione di un DBMS#Hard Disk Drives|HDD]] o, in generale, con qualsiasi dispositivo di memoria, l'obiettivo è di **organizzare i dati e l'hardware in modo da minimizzare il più possibile qualsiasi ritardo nella lettura o scrittura**, e per quanto riguarda i dispositivi di memoria analizzati nel paragrafo precedente queste minimizzazioni possono essere effettuate soprattutto sul **seek time** e, parzialmente, sul **rotation delay**; oltre a ciò, si desidera anche **minimizzare il numero di RBA**, dato che naturalmente impiegano più tempo ad essere effettuati rispetto agli SBA.

Per poter pensare a queste problematiche, un creatore di basi di dati fisiche deve pensare ai modi più ottimali per **trasformare concetti e modelli logici di dato in strutture dati fisiche**, in modo da ottenere il miglior bilancio possibile tra una **lettura e scrittura efficiente** in termini di tempo e un **utilizzo intelligente dello spazio di memoria**. Per questo obiettivo, un'organizzazione adiacente al [[BD1_01 - Modello relazionale|modello relazionale]] su cui ci siamo soffermati finora nel corso risulta molto utile. Per capire come questi concetti possano essere collegati, vediamo la seguente tabella, dove ogni colonna rappresenta uno dei "passaggi" di questa trasformazione, e ciascuna riga un certo tipo di dato:

| Modello astratto                       | Modello logico-relazionale          | Modello fisico                                                      |
| -------------------------------------- | ----------------------------------- | ------------------------------------------------------------------- |
| Attributo e tipo di attributo          | Valore (cella) e nome della colonna | Dato (bit o caratteri rappresentanti un determinato valore)         |
| Singola entità                         | Riga o tupla                        | Collezione di dati, che rappresenta tutti gli attributi dell'entità |
| Insieme delle entità dello stesso tipo | Tabella o relazione                 | File o blocco di dati                                               |
| Insieme di tipi di entità              | Insieme di tabelle o relazioni      | Database                                                            |

A livello fisico, come anticipato dalla tabella, **un database consiste in un insieme di file**; ogni file, a sua volta, può essere visto come una **collezione di "pagine" di dimensione fissa**; ogni pagina, al suo interno, conterrà **diverse entità**, ciascuna corrispondente a una [[BD1_01 - Modello relazionale#Domini, tuple e relazioni|tupla]] per intenderci; infine, ciascuna tupla sarà composta da **un certo numero di campi**, di dimensione fissa o variabile, che rappresentano gli [[BD1_01 - Modello relazionale#Attributi|attributi]] della tupla.
___
## File

È chiaro, dunque, che il fulcro di un database sono i **file**, che costituiscono la sovrastruttura principale in cui sono organizzati i dati contenuti al suo interno.

Ma **come sono organizzati internamente i file**? Ci sono varie modalità alternative per distribuire i dati all'interno di un file, e di conseguenza in base ad esse ci sono diversi **tipi di file**, tra cui:
- **heap file**;
- **sequential file**;
- **random file**;
- **indexed sequential file**.

Analizziamo ciascuna di queste strutture più nel dettaglio. 

##### Heap file

Si tratta di un'**organizzazione basilare e comune**, dove **nuove entità sono aggiunte al termine del file**, e dove **non è presente una relazione tra attributi dell'entità e la loro posizione in memoria**. Evidentemente, basandoci su queste caratteristiche, l'unico modo per trovare un'entità ben precisa all'interno di un heap file è la **ricerca lineare**, ossia scorrere ciascuna delle entità del file una dopo l'altra finché non verrà trovata quella che corrisponde alla chiave di ricerca; quest'ultima, del resto, diventa ancora più inefficiente nel momento in cui tale chiave non è univoca all'interno del file, dato che ciò richiede che tutto il file venga interrogato in modo da assicurarsi di trovare tutte le entità al suo interno che corrispondono alla chiave di ricerca. Data la natura del file, per un file con $NBLK$ blocchi si dovranno controllare una media di $\frac{NBLK}{2}$ entità per trovare quella desiderata.
___
##### Sequential file

Passiamo, ora, al **sequential file**. Pur rimanendo molto semplice, è un passo avanti rispetto all'[[BD1_04 - Organizzazione di un DBMS#Heap file|heap file]]: in questo caso, **le entità vengono memorizzate in ordine crescente o decrescente rispetto alla loro chiave di ricerca**. Si tratta di un piccolo cambiamento, ma che permette di aumentare l'efficienza in vari contesti: innanzitutto, supponendo che si vogliano recuperare **più entità contigue in ordine**, la struttura del sequential file permetterebbe di **effettuare una ricerca lineare esclusivamente con degli [[BD1_04 - Organizzazione di un DBMS#Hard Disk Drives|SBA]]**, che sappiamo essere più efficienti degli RBA; al tempo stesso, pur rimanendo la ricerca lineare una scelta possibile, per trovare una determinata entità sarà possibile effettuare una **ricerca binaria**, che porterà inevitabilmente a un'esecuzione di un numero molto minore di accessi, in media $\log_{2}NBLK$ (ciononostante, precisiamo che gli accessi in questione sarebbero prevalentemente degli RBA, dato che l'algoritmo di ricerca binaria prevede di spostarsi da un punto all'altro dell'insieme di entità).

Per comprendere quanto quest'ultimo approccio risulti essere più efficiente, vediamo un esempio: supponiamo di avere un sequential file contenente $NR=30\,000$ entità, dove una singola entità avrà dimensione $RS=100$ byte, e con la dimensione di un singolo blocco di memoria pari a $BS=2048$ byte; possiamo ottenere il numero $BF$ di entità contenute in un blocco dividendo la dimensione di un blocco di memoria per la dimensione di un'entità ($BF=\frac{BS}{RS}=\frac{2048}{100}\approx 20$), e in seguito il numero $NBLK$ di blocchi del file dividendo il numero di entità per il valore appena trovato ($NBLK=\frac{NR}{BF}=\frac{30\,000}{20}=1500$). A questo punto, possiamo stimare il numero di accessi a blocchi di memoria che ci si aspetta debbano essere eseguiti per trovare un'entità generica all'interno del file. Come abbiamo detto, la ricerca lineare necessita in media $\frac{NBLK}{2}$ accessi e, in un sequential file, sarebbero tutti accessi a blocchi di memoria contigui, dunque ci si aspettano: $$\frac{1500}{2}\text{ SBA} = 750 \text{ SBA}$$Se utilizzassimo, invece, la ricerca binaria, allora impiegheremmo in media:
$$\log_{2}1500\text{ RBA}\approx 11\text{ RBA}$$

Tuttavia, il sequential file è **meno efficiente** dell'heap file su un aspetto, ossia l'**aggiornamento dei dati contenuti al suo interno**: per ovviare a questa inefficienza, spesso si preferisce aggiungere, rimuovere o modificare entità in gruppi.
___
##### Random file

[21 - slide 24/31]
___
##### Indexed sequential file

[21 - slide 32/37]
___