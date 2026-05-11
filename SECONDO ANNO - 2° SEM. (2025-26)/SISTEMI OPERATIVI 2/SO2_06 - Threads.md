## Le applicazioni multi-thread

In un'applicazione tradizionale, il programmatore definisce tendenzialmente un **unico flusso di esecuzione delle istruzioni**: durante l'esecuzione del programma, la CPU eseguirà istruzioni nella sequenza dettata dalla logica del programma stesso, seguendo però un'unica "strada" nel farlo; quando, poi, il flusso di esecuzione arriva ad eseguire una chiamata `exit()`, l'esecuzione viene terminata.

In alternativa, però, è possibile anche creare delle cosiddette "**applicazioni multi-thread**", in cui il programmatore definisce **diversi flussi di esecuzione** (detti "**threads**"), tali per cui ciascuno di essi condivide le strutture dati principali dell'applicazione, ma procede in modo concorrente e indipendente dagli altri flussi. In questo contesto, l'applicazione termina la propria esecuzione solamente quando **tutti i threads vengono terminati**.

##### Processi e threads

Prima di proseguire, è opportuno effettuare un approfondimento sui **threads**, in particolare facendo un **confronto tra processi e threads**.

Come abbiamo detto [[SO2_03 - Processi#Cos'è un processo?|in precedenza]], un processo rappresenta in poche parole un'istanza di un programma in esecuzione. Ora, in una tipica applicazione mono-thread, tutto il necessario per l'esecuzione della stessa (codice, strutture dati, file aperti, contenuto dei registri della CPU, ecc. ecc.) è semplicemente contenuto in tale processo. In un'applicazione multi-thread, invece, **lo spazio di memoria del processo è in buona parte condiviso tra i suoi thread**: in particolare, tipicamente le risorse comuni sono:
- **codice** del programma in esecuzione;
- **strutture dati**;
- **file aperti**;

mentre altre risorse come il contenuto dei **registri della CPU** e dello **stack** sono **proprie di ogni thread**. Insomma, la differenza principale tra un'applicazione single-thread e una multi-thread sta nel fatto che **il processo della seconda è "suddiviso" tra più thread**, che contribuiscono tutti all'esecuzione dello stesso programma ma che lo fanno seguendo diversi flussi di esecuzione e svolgendo compiti diversi.

Possiamo riassumere le **principali differenze tra processi e threads** nella seguente tabella:

| Processi                                                                                                   | Threads                                                                                                   |
| ---------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| Istanze di un programma in esecuzione                                                                      | Componenti di un processo e più piccola unità di esecuzione                                               |
| Context switching richiede interazione con l'OS                                                            | Context switching non richiede interazione con l'OS                                                       |
| Ogni processo ha il suo spazio di memoria                                                                  | Utilizzano la memoria del processo a cui appartengono                                                     |
| Richiedono più risorse di sistema                                                                          | Richiedono meno risorse di sistema                                                                        |
| Relativamente difficili da creare                                                                          | Facili da creare                                                                                          |
| Comunicazione tra processi abbastanza lenta, in quanto ogni processo ha un differente indirizzo di memoria | Comunicazione tra thread più veloce, in quanto i thread condividono lo stesso indirizzo e area di memoria |
| Ogni processo viene eseguito in modo indipendente                                                          | Ogni thread può leggere, scrivere o modificare dati di altri thread                                       |
___
##### Implementazione di un'applicazione multi-thread

Per poter **implementare un'applicazione multi-thread**, si deve pensare principalmente a due livelli:
- **livello utente**;
- **livello kernel**.

In particolare, ciò avviene perché i threads vengono generalmente categorizzati in:
- **thread utente**, che rappresentano i vari flussi logici di esecuzione del programma;
- **thread kernel**, che rappresentano i thread effettivamente visibili dall'OS, e di conseguenza i servizi e le strutture dati che il kernel utilizza per gestirli.

Si specifica, per chiarezza, che la distinzione tra thread utente e thread kernel non ha niente a che fare con la distinzione di privilegi di esecuzione tra User Mode e Kernel Mode. In sintesi, un thread kernel è **l'unità più piccola che l'OS può mandare in esecuzione** su un processore, mentre un thread utente è invece un'**illusione di parallelismo creata all'interno dell'applicazione**.

Dunque, una specifica implementazione è caratterizzata principalmente dalla **relazione e comunicazione tra thread utente e thread kernel**, che può seguire diversi modelli, tra cui:
- modello "**da molti a 1**";
- modello "**da 1 a 1**";
- modello "**da molti a molti**".

Il **modello "da molti a 1"** impone che **a più thread utente corrisponda un unico thread kernel**. Il kernel, naturalmente, non è coinvolto nella gestione dei flussi di esecuzione dell'applicazione, e dunque dei vari thread utente, ma **è l'applicazione stessa a gestire autonomamente l'esecuzione dei thread utente**, organizzando i vari flussi di esecuzione e salvando e ripristinando all'occorrenza stacks e contenuti dei registri della CPU. In un'applicazione che segue questo modello, formalizzabile nel seguente schema:

![[modello_moltia1.png]]

**se un thread utente esegue una chiamata di sistema bloccante, l'intero processo** (e quindi anche tutti gli altri thread utente) **viene bloccato**. Ciò avviene perché se uno dei thread utente effettua tale chiamata l'OS dovrà necessariamente bloccare il thread kernel (che è l'unico thread visibile all'OS), ma essendo tutti i thread utente mappati al medesimo thread kernel ciò porterà al bloccaggio totale del processo. In questo modello, è di fatto **impossibile sfruttare il parallelismo supportato dal calcolatore**, ad esempio se quest'ultimo dispone di più core o più processori, dato che comunque a essere eseguito sarà un unico thread kernel. Tale implementazione è detta anche "**multi-threading a livello utente**".

**Il modello "da 1 a 1"** impone che **ciascun thread utente corrisponda a un singolo thread kernel**. **Il kernel**, stavolta, **è coinvolto nella gestione dei flussi di esecuzione dell'applicazione**, dato che ciascuno di essi, e dunque ciascun thread utente, è mappato a un diverso thread kernel, perfettamente visibile all'OS; in questo contesto, **l'applicazione utilizza le API definite in librerie di sistema** per creare e distruggere thread utente, ma anche per gestire la comunicazione e la sincronizzazione tra gli stessi. In un'applicazione che segue questo modello, formalizzabile nel seguente schema:

![[modello_da1a1.png]]

**se un thread utente esegue una chiamata di sistema bloccante, gli altri thread possono continuare la loro esecuzione senza problemi**. In questo modello, per giunta, **viene sfruttato il parallelismo supportato dal calcolatore**. Tale implementazione è detta anche "**multi-threading a livello kernel**".

Infine, il **modello "da molti a molti"** impone che **un numero $n_{u}$ di thread utente corrisponda a un numero $n_{k}$ di thread kernel**, con $n_{k}\le n_{u}$. Il kernel è coinvolto nella gestione dei thread kernel, ma non gestisce i thread utente; l'applicazione, invece, tramite API va a definire il numero di thread kernel, crea e distrugge thread utente e mappa i secondi ai primi. Si tratta, sostanzialmente, di un **ibrido tra i modelli "da 1 a 1" e "da molti a 1"**, formalizzabile nel seguente schema:

![[modello_damoltiamolti.png]]

[SLIDES: 16, pag. 16]
___
##### Vantaggi del multi-threading

[SLIDES: 16, pag. 5/7]
___
##### Librerie per threads

[SLIDES: 16, pag. 17 - 18]
___
## Funzioni utili per gestire i threads

[SLIDES: 16, pag. 20/32]
___