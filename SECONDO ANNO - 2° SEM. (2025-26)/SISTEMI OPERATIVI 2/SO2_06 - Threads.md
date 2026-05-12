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

Alcuni **esempi importanti di implementazione del modello "da molti a 1"** sono la libreria "Green Threads" di Oracle, la libreria "GNU Portable Threads" e altre; invece, **tutti i maggiori OS moderni supportano i modelli "da 1 a 1" e "da molti a molti"**, in particolare con Linux, Windows e MacOS che tendono ad adottare il modello "da 1 a 1", mentre IRIX, HP-UX e Tru64 UNIX scelgono il modello "da molti a molti". In ogni caso, la scelta del modello "da 1 a 1" piuttosto che del modello "da molti a molti" dipende tipicamente dalla libreria di thread utilizzata, piuttosto che dall'OS specifico.
___
##### Vantaggi ed esempi del multi-threading

Il multi-threading rappresenta una tecnica proficua e consigliata, al giorno d'oggi, soprattutto perché ormai **la maggioranza dei calcolatori moderni permette vari meccanismi di parallelismo**: ad esempio, banalmente, la presenza di "**multiprocessori**", ossia di diverse CPU integrate sulla stessa scheda madre, e di **processori "multi-core"**, ossia composti da più unità integrate sullo stesso chip, permette di suddividere l'esecuzione in più flussi da mandare in esecuzione parallelamente; ancora, vari calcolatori supportano un meccanismo chiamato "**hyperthreading**", grazie al quale diversi flussi di esecuzione possono "detenere" un insieme di registri della CPU, e alternare la loro esecuzione sulle unità funzionali della stessa.

Naturalmente, implementare il multi-threading fornisce vari **vantaggi**, tra cui:
- **riduzione del tempo di risposta**, dato che la presenza di più threads di esecuzione permette a un'applicazione di non rimanere completamente bloccata in attesa di un certo dato o evento;
- **migliore condivisione delle risorse**, dato che tutti i threads di un'applicazione condividono le stesse risorse e la comunicazione tra tali threads è pressoché immediata;
- **maggiore efficienza**, dato che l'OS gestisce i threads in modo più efficiente rispetto ai processi (basti pensare che, in sistemi Linux, in media creare un thread richiede circa $\frac{1}{10}$ del tempo richiesto per creare un processo);
- **maggiore scalabilità**, dato che i thread possono sfruttare in modo implicito il parallelismo interno del calcolatore, e dunque permettere di creare programmi più complessi senza perdita di prestazioni.

Al giorno d'oggi, il multi-threading è una tecnica ampiamente utilizzata e diffusa. Si potrebbero trovare innumerevoli **esempi di applicazioni multi-thread**: si pensi, ad esempio, a un **browser**, che potrebbe prevedere i seguenti thread di esecuzione:
- un thread principale per il controllo dell'applicazione;
- un thread per l'interazione con l'utente;
- un thread per la visualizzazione delle pagine in formato HTML;
- un thread per la gestione dei trasferimenti di pagine e file dalla rete;
- un thread per l'esecuzione dei frammenti di codice integrati nelle pagine web;

e così via.
___
##### Librerie per threads

Generalmente, per realizzare un'applicazione multi-thread, il programmatore utilizza una **libreria di sistema**, che offre delle API che permettono la creazione e gestione dei threads. **Queste API non sono necessariamente correlate in modo diretto con la tipologia di thread utilizzata**, e possono ad esempio esistere diverse versioni di una libreria con API identiche ma riferite una a threads utente e l'altra a threads kernel (è questo il caso, ad esempio, per la libreria **`pthreads`**, o "**POSIX Threads**"). Ciononostante, **alcune librerie e relative API sono specifiche per un determinato OS o tipo di thread**, come accade ad esempio per la libreria per i thread **`Win32`**. Ancora, in altri casi, **la libreria è specifica di un certo linguaggio ad alto livello**: in questi contesti, l'uso della libreria è implicito e automatico (è il caso, ad esempio, della **libreria di thread di Java**).

Approfondendo la libreria **`pthreads`**, essa è definita dallo **standard POSIX**, che definisce le API della stessa ma non stabilisce in modo stretto quale debba essere la loro implementazione in un OS specifico. In Linux, ad esempio, sono coesistite **tre diverse implementazioni**:
- **`LinuxThreads`**, la prima delle tre, basata su un modello "[[SO2_06 - Threads#Implementazione di un'applicazione multi-thread|da 1 a 1]]" e non più supportata;
- **`NGPT`**, o "**Next Generation POSIX Threads**", sviluppata da IBM su un modello "da molti a molti", ma anch'essa non più supportata;
- **`NPTL`**, o "**Native POSIX Threads Library**", l'ultima implementazione nonché la più efficiente e più aderente allo standard, basata sul modello "da 1 a 1" e l'unica che è ancora attualmente in uso.
___
## Funzioni utili per gestire i threads

Continuando a prendere come riferimento la [[SO2_06 - Threads#Librerie per threads|libreria per thread]] **`pthreads`**, in questo paragrafo andremo ad approfondire alcune **funzioni di libreria utili per gestire i threads**. In particolare, considereremo funzioni utilizzate per:
- **[[SO2_06 - Threads#Creazione di un nuovo thread|creare un thread]]**;
- **[[SO2_06 - Threads#Terminazione di un thread|terminare un thread]]**;
- **[[SO2_06 - Threads#Attesa della terminazione di un thread|far attendere la terminazione di un altro thread]]**;
- **[[SO2_06 - Threads#Terminazione di un processo multi-thread|terminare un processo multi-thread]]**;
- **accedere e modificare gli [[SO2_06 - Threads#Attributi di un thread|attributi di un thread]]**.

Si ricordi che, in generale, per lavorare con `pthreads` all'interno di un programma C si dovrà **includere l'header file `pthread.h`**. Inoltre, per poter **compilare un programma che utilizza `pthread.h`**, sarà necessario **aggiungere l'opzione `-pthread`** al comando `gcc`, nel modo seguente:

```
gcc program.c -o program.o -pthread
```

##### Creazione di un nuovo thread

Per **creare un nuovo thread** all'interno del processo considerato, la libreria `pthreads` offre la funzione:

```
int pthread_create(pthread_t *ptid, const pthread_attr_t *pattr, void *start(void *), void *arg)
```

Approfondiamo nel dettaglio ciascuno dei **parametri** di questa funzione:
- **`pthread_t *ptid`** consiste in un **[[SO2_04 - C#Puntatori|puntatore]] a una variabile di tipo `pthread_t`**, che in caso di successo della chiamata a `pthread_create` andrà a contenere l'ID del nuovo thread creato, chiamato "**TID**" o "**Thread ID**";
- **`const pthread_attr_t *pattr`** consiste in un **puntatore a una struttura `pthread_attr_t`**, che permette eventualmente di specificare alcuni attributi specifici per il thread che si sta creando (rivedremo questo concetto [[SO2_06 - Threads#Attributi di un thread|in seguito]]), e che può essere passato come `NULL` o `0` per fare in modo che il thread abbia degli attributi predefiniti;
- **`void *start(void *)`** consiste nella **funzione che verrà inizialmente eseguita dal thread**, il cui identificatore naturalmente è `start`;
- **`void *arg`** consiste in un **puntatore passato come argomento a `start`** (l'argomento è unico, dunque se si vogliono passare più dati converrà creare una [[SO2_04 - C#Strutture|struttura]] e passare un puntatore ad essa); se non servono argomenti, tale parametro avrà valore `NULL`.

Il **valore di ritorno** della funzione `pthread_create` è **`0` in caso di successo**, o un **codice numerico positivo in caso di errore**, con tale codice che rappresenta l'errore specifico in cui ha incappato la funzione.

Di seguito, si fornisce un **esempio di utilizzo** di `pthread_create`:

```
#include <pthread.h>
#include <stdio.h>
#include <stdlib.h>

void *stampa_messaggio(void *arg) 
{
    char *messaggio = (char *)arg;
    printf("Il thread dice: %s\n", messaggio);
    
    pthread_exit(NULL);
}

int main() 
{
    pthread_t mio_tid; 
    char *testo = "Ciao dal nuovo thread!";
    int risultato;

    risultato = pthread_create(&mio_tid, NULL, stampa_messaggio, (void *)testo);

    if (risultato != 0) 
    {
        printf("Errore nella creazione del thread\n");
        return 1;
    }

    pthread_join(mio_tid, NULL); 

    printf("Il thread ha terminato, il main chiude.\n");
    return 0;
}
```
___
##### Terminazione di un thread

Per **terminare l'esecuzione di un thread**, si utilizza la funzione:

```
void pthread_exit(void *value_ptr)
```

dove **`value_ptr`** consiste in un **[[SO2_04 - C#Puntatori|puntatore]] generico che rappresenta il "risultato" del thread**. Il thread che viene terminato è proprio il thread che chiama la funzione `pthread_exit`, dunque `value_ptr` sarà ciò che il thread restituirà ad eventuali altri thread dello stesso processo che lo stavano "aspettando" (se il thread non deve restituire nulla di utile, si può passare `NULL` a tale funzione); una cosa importantissima da ricordare, in questo contesto, è di **non restituire mai un puntatore a una variabile locale alla funzione del thread**, dato che alla terminazione del thread il suo stack viene distrutto, e con esso qualsiasi variabile locale interna ad esso. 

Nonostante sia buona pratica **inserire** sempre **una chiamata a `pthread_exit`** al termine del corpo della funzione `start` di un thread, **non è sempre necessario**: infatti, se `start` giunge al termine naturalmente, tale funzione viene invocata implicitamente dall'OS, e se la funzione esegue un'istruzione `return` l'OS prende il valore ritornato e lo utilizza come `value_ptr` della chiamata implicita a `pthread_exit`.

Nel momento in cui **il thread che esegue `pthread_exit` è l'ultimo thread in esecuzione di un processo**, ciò porta alla **terminazione dell'intero processo**, che effettua una chiamata implicita a `exit(0)`.

Di seguito, si fornisce un **esempio di utilizzo** di `pthread_exit`:

```
#include <pthread.h>
#include <stdio.h>
#include <stdlib.h>

void *calcola_risultato(void *arg) 
{
    int numero = *(int *)arg;
    
    // Allocare memoria nell'Heap, così che non venga distrutta quando il thread muore
    int *risultato = malloc(sizeof(int)); 
    *risultato = numero * 10;
    
    printf("Thread: sto restituendo %d...\n", *risultato);
    
    pthread_exit((void *)risultato); 
}

int main() {
    pthread_t tid;
    int input = 5;
    void *risultato_thread;

    pthread_create(&tid, NULL, calcola_risultato, &input);

    pthread_join(tid, &eredita_dal_thread); 

    int *valore_letto = (int *)eredita_dal_thread;
    printf("Il thread ha terminato con successo, restituendo: %d\n", *valore_letto);
    
    // Pulire la memoria allocata dal thread defunto
    free(valore_letto); 

    return 0;
}
```
___
##### Attesa della terminazione di un thread

Lo strumento fondamentale per la **sincronizzazione tra thread** è la funzione **`pthread_join`**, il cui scopo principale è **far attendere al thread chiamante il termine dell'esecuzione di un altro thread**. La sinossi completa della funzione è:

```
int pthread_join(pthread_t tid, void *pret)
```

dove **`tid`** è il **TID del thread che si desidera attendere** (per intenderci, quello ottenuto dalla chiamata a `pthread_create`), mentre **`pret`** è un **puntatore alla variabile che riceverà il valore restituito dal thread terminato** (per intenderci, se il thread che termina esegue `pthread_exit(val)`, `pret` dovrà essere un puntatore a `val`). Nel caso in cui non ci interessi recuperare il valore di ritorno del thread che si sta aspettando, possiamo passare come parametro `pret` il valore nullo `NULL`.

Il **valore di ritorno** della funzione `pthread_join`, analogamente a `pthread_create`, è **`0` in caso di successo** e un **codice numerico positivo in caso di errore** (ad esempio, se si prova a fare un join su un thread non esistente).

Naturalmente, per natura di questa funzione, **`pthread_join` rappresenta una chiamata bloccante**, nel senso che l'esecuzione del thread chiamante viene a tutti gli effetti sospesa, finché il thread indicato da `tid` non termina la sua esecuzione. Oltre a ciò, però, `pthread_join` può avere anche altri scopi, primo su tutti la **pulizia della memoria**: infatti, quando un thread termina, è possibile che le sue risorse (ad esempio, il suo stack) rimanga in memoria se nessun altro thread stava "aspettando" la sua fine; dunque, in questo contesto, effettuare una chiamata a `pthread_join` relativa a tale thread garantisce che tali risorse vengano effettivamente eliminate, liberando memoria.

Di seguito, si fornisce un **esempio di utilizzo** di `pthread_join`:

```
#include <pthread.h>
#include <stdio.h>
#include <stdlib.h>

void *funzione_worker(void *arg) 
{
    int *v = malloc(sizeof(int));
    *v = 42;
    printf("Thread: Calcolo completato.\n");
    pthread_exit(v);
}

int main() 
{
    pthread_t tid;
    void *status;

    pthread_create(&tid, NULL, funzione_worker, NULL);

    printf("Main: In attesa del thread...\n");
    
    // Il main si blocca qui finché il thread non finisce
    pthread_join(tid, &status); 

    int *risultato = (int *)status;
    printf("Main: Thread terminato. Il risultato è %d\n", *risultato);

    free(risultato); // Pulizia della memoria allocata dal thread
    return 0;
}
```
___
##### Terminazione di un processo multi-thread



[SLIDES: 16, pag. 24 - 25]
___
##### Attributi di un thread

[SLIDES: 16, pag. 26/28]
___