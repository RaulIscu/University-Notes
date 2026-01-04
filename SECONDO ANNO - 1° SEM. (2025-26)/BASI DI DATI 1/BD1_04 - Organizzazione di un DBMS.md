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



[21 - slide 8/12]
___