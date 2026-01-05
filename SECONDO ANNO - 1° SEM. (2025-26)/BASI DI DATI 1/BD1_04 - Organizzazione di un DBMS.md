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

Nello strato fisico, dunque, si trovano tutti quegli strumenti e componenti che si occupano della **gestione della memoria** concreta, dunque dei dati contenuti nel database (qui troviamo il gestore di memoria, vari buffer, metodi di accesso, ecc. ecc.). Possiamo schematizzare la struttura di questo blocco del DBMS nel modo seguente:

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



[21 - slide 13]
___