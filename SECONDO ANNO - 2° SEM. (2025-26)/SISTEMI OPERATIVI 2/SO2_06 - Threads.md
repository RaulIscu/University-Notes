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

Come abbiamo accennato [[SO2_06 - Threads#Creazione di un nuovo thread|in precedenza]], **un thread è dotato di determinati attributi**, che permettono di personalizzare il suo comportamento. Ciò avviene attraverso un oggetto di tipo **`pthread_attr_t`**, che consiste essenzialmente in una **[[SO2_04 - C#Strutture|struttura]] contenente le varie opzioni di configurazione** del thread (è quella che viene specificata quando si chiama la funzione `pthread_create`, e che contiene attributi predefiniti se al parametro corrispondente di tale funzione si passa `NULL`).

Per poter **assegnare attributi specifici a un nuovo thread**, si dovranno seguire dei passaggi ben precisi:
1. **dichiarare un oggetto di tipo `pthread_attr_t`**;
2. **inizializzare l'insieme di attributi** con una chiamata alla funzione **`pthread_attr_init`**;
3. **modificare i singoli attributi** del thread con funzioni più specifiche (le vedremo in seguito);
4. **assegnare l'insieme di attributi creato a un nuovo thread**, passando un puntatore agli attributi come parametro a `pthread_create`;
5. una volta che il thread in questione è stato creato, **l'oggetto di tipo `pthread_attr_t`** non serve più, dunque **andrà eliminato** con una chiamata alla funzione **`pthread_attr_destroy`**.

Vediamo più nel dettaglio le due funzioni appena citate, ossia **`pthread_attr_init`** e **`pthread_attr_destroy`**. La sinossi completa della prima è:

```
int pthread_attr_init(pthread_attr_t *attr)
```

Come accennato, tale funzione serve per **inizializzare un oggetto di tipo `pthread_attr_t`, popolandolo con gli attributi predefiniti** dell'OS del calcolatore su cui si sta lavorando. L'unico parametro che riceve tale funzione è **`attr`**, ossia un **[[SO2_04 - C#Puntatori|puntatore]] all'oggetto da inizializzare**; per quanto riguarda il **valore di ritorno**, invece, in caso di successo verrà restituito `0`, altrimenti si restituirà un codice numerico specifico per l'errore che si è incontrato. Abbiamo, poi, la funzione:

```
int pthread_attr_destroy(pthread_attr_t *attr)
```

che viene utilizzata per **distruggere un oggetto di tipo `pthread_attr_t`**, in modo da liberare la memoria allocata ad esso durante la sua inizializzazione. Anche in questo caso, l'unico parametro che riceve la funzione è **`attr`**, ossia un **puntatore all'oggetto da distruggere**; per quanto riguarda il valore di ritorno, valgono le stesse considerazioni fatte per `pthread_attr_init`.

Ora, avendo chiarito come inizializzare e distruggere gli oggetti-attributi di un thread, andiamo a vedere più nel dettaglio quali sono effettivamente gli **attributi di un thread**. In particolare, approfondiremo principalmente i seguenti attributi:
- **`detachstate`**;
- **`scope`**;
- **`stackaddr`**;
- **`stacksize`**;
- **`schedpolicy`**;
- **`inheritsched`**;
- **`priority`**.

L'attributo **`detachstate`** definisce **cosa succede alle risorse del thread nell'istante in cui termina la sua esecuzione**. Il **valore predefinito** di tale attributo è **`PTHREAD_CREATE_JOINABLE`**, che impone al thread di **preservare il suo stato di uscita e le sue risorse dopo la terminazione**, in attesa che un altro thread faccia una chiamata a `pthread_join` su tale thread; in alternativa, è possibile assegnare anche il valore **`PTHREAD_CREATE_DETACHED`**, che impone al thread di **rilasciare istantaneamente la memoria e le risorse utilizzate al termine dell'esecuzione**.

L'attributo **`scope`** definisce **con chi compete il thread per risorse e tempo di esecuzione sulla CPU**. Tipicamente, in Linux il **valore predefinito** di tale attributo è **`PTHREAD_SCOPE_SYSTEM`**, che fa in modo che **il thread competa alla pari con tutti i thread di tutti i processi attivi** nel calcolatore; in alternativa, è possibile assegnare anche **`PTHREAD_SCOPE_PROCESS`**, che fa in modo che **il thread competa solo con gli altri thread appartenenti al suo stesso processo**.

L'attributo **`stackaddr`** permette di specificare l'**indirizzo in memoria dello stack del thread**. Si tratta di un attributo molto delicato, tipicamente settato a **`NULL`**, il che significa che è l'OS a decidere dove allocare lo stack; modificare l'attributo `stackaddr` è un'operazione avanzata e raramente necessaria.

L'attributo **`stacksize`** permette di specificare la **dimensione dello stack del thread**. Il valore predefinito è tipicamente **1 MB** o **2 MB**, a seconda dell'architettura; in certi contesti, però, è opportuno modificare tale dimensione, ad esempio per diminuirla quando si prevede la creazione di un grande numero di thread, o per aumentarla quando si prevede che il thread considerato debba effettuare ricorsioni profonde o allocare array statici di grandi dimensioni.

L'attributo **`schedpolicy`** definisce **quale algoritmo di scheduling utilizzare per gestire il thread**. Il **valore predefinito** di tale attributo è tipicamente **`SCHED_OTHER`**, che impone un approccio trovato in molti sistemi (tra cui sistemi Solaris) in cui **un thread viene eseguito finché non viene interrotto da un thread con priorità più alta**, oppure **finché non si blocca volontariamente**. In alternativa, è possibile assegnare altre politiche di scheduling real-time, come:
- **`SCHED_FIFO`**, con la quale un thread "monopolizza" la CPU finché non decide da solo di fermarsi;
- **`SCHED_RR`**, con la quale un thread viene costantemente alternato con altri thread real-time seguendo un modello Round Robin.

L'attributo **`inheritsched`** specifica **se il nuovo thread eredita o meno la priorità e lo scheduling del thread padre**. Il **valore predefinito** di tale attributo è **`PTHREAD_INHERIT_SCHED`**, con il quale **il nuovo thread eredita priorità e politiche di scheduling del thread padre** (in questo caso, eventuali valori inseriti negli attributi `schedpolicy` e `priority` del thread figlio vengono ignorati); in alternativa, assegnando a questo attributo il valore **`PTHREAD_EXPLICIT_SCHED`**, si fa in modo che **il nuovo thread non erediti priorità e politiche di scheduling dal thread padre**, facendo invece riferimento a quelle assegnate ad esso stesso. 

L'attributo **`priority`** rappresenta, concretamente, la **priorità assoluta del thread**. Tale valore è contenuto in una **[[SO2_04 - C#Strutture|struttura]] `sched_param`**, nel campo **`int sched_priority`** della stessa, e i valori che può assumere dipendono sia dall'OS con cui si sta lavorando, sia dalla politica di scheduling scelta per il thread considerato: in particolare, se si sceglie una politica di default come `SCHED_OTHER`, la `sched_priority` è tipicamente impostata a **0**, mentre per politiche real-time come `SCHED_FIFO` o `SCHED_RR` il range tipico va **da 1** (priorità minima) **a 99** (priorità massima.

Per poter **leggere e modificare singoli attributi di un thread**, è prevista un'ampia famiglia di funzioni. Innanzitutto, per **ottenere gli attributi di un thread già attivo** si utilizza la funzione:

```
int pthread_getattr_np(pthread_t thread, pthread_attr_t *attr)
```

dove **`thread`** è il **TID del thread da cui ottenere gli attributi**, e **`attr`** è un **puntatore all'oggetto di tipo `pthread_attr_t` che ospiterà una copia degli attributi correnti di `thread`**. Una volta ottenuti gli attributi nel loro complesso, sarà possibile **ottenere singoli attributi dall'oggetto `pthread_attr_t`** tramite una serie di funzioni "getter", tra cui:
- **`pthread_attr_getdetachstate(const pthread_attr_t *attr, int *ds)`**, che ottiene l'attributo `detachstate` dell'oggetto `attr` e lo scrive nella variabile a cui punta `ds`;
- **`pthread_attr_getscope(const pthread_attr_t *attr, int *s)`**, che ottiene l'attributo `scope` dell'oggetto `attr` e lo scrive nella variabile a cui punta `s`;
- **`pthread_attr_getstacksize(const pthread_attr_t *attr, size_t *ss)`**, che ottiene l'attributo `stacksize` dell'oggetto `attr` (corrispondente ai byte di memoria che si vogliono allocare allo stack) e lo scrive nella variabile a cui punta `ss`;
- **`pthread_attr_getstack(const pthread_attr_t *attr, void sa, size_t *ss)`**, che ottiene sia l'attributo `stackaddr` dell'oggetto `attr`, scrivendolo nel puntatore `sa`, sia l'attributo `stacksize` (sempre espresso in byte), scrivendolo nella variabile a cui punta `ss`;
- **`pthread_attr_getschedpolicy(const pthread_attr_t *attr, int *sp)`**, che ottiene l'attributo `schedpolicy` dell'oggetto `attr` e lo scrive nella variabile a cui punta `sp`;
- **`pthread_attr_getinheritsched(const pthread_attr_t *attr, int *is)`**, che ottiene l'attributo `inheritsched` dell'oggetto `attr` e lo scrive nella variabile a cui punta `is`;
- **`pthread_attr_getschedparam(const pthread_attr_t *attr, struct sched_param *p)`**, che ottiene l'attributo `sched_param` dell'oggetto `attr` e lo scrive nella variabile a cui punta `p`.

Vediamo, poi, le funzioni utilizzate per **modificare gli attributi di un oggetto di tipo `pthread_attr_t`**:
- **`pthread_attr_setdetachstate(pthread_attr_t *attr, int ds)`**, che modifica l'attributo `detachstate` dell'oggetto `attr` e gli assegna il valore `ds`;
- **`pthread_attr_setscope(pthread_attr_t *attr, int s)`**, che modifica l'attributo `scope` dell'oggetto `attr` e gli assegna il valore `s`;
- **`pthread_attr_setstackaddr(pthread_attr_t *attr, void *sa)`**, che modifica l'attributo `stackaddr` dell'oggetto `attr` e gli assegna il valore `sa`;
- **`pthread_attr_setstacksize(pthread_attr_t *attr, size_t ss)`**, che modifica l'attributo `stacksize` dell'oggetto `attr` e gli assegna il valore `ss`, corrispondente ai byte di memoria che si vogliono allocare allo stack;
- **`pthread_attr_setstack(pthread_attr_t *attr, void *sa, size_t ss)`**, che modifica sia l'attributo `stackaddr` dell'oggetto `attr`, assegnandogli il valore `sa`, sia l'attributo `stacksize`, assegnandogli il valore `ss` (sempre espresso in byte);
- **`pthread_attr_setschedpolicy(pthread_attr_t *attr, int sp)`**, che modifica l'attributo `schedpolicy` dell'oggetto `attr` e gli assegna il valore `sp`;
- **`pthread_attr_setinheritsched(pthread_attr_t *attr, int is)`**, che modifica l'attributo `inheritsched` dell'oggetto `attr` e gli assegna il valore `is`;
- **`pthread_attr_setschedparam(pthread_attr_t *attr, const struct sched_param *p)`**, che modifica l'attributo `sched_param` dell'oggetto `attr` e gli assegna il valore `p`.
___
## Implementazione dei thread in Linux

[SLIDES: 16, pag. 30/32]
___
## Sincronizzazione tra threads

Come abbiamo visto finora, i threads possono essere uno strumento molto potente e comodo, ma **l'esistenza di più flussi di esecuzione concorrenti è anche fonte di molte complicazioni**: infatti, in un'applicazione multi-thread, **ogni thread rappresenta un flusso di esecuzione a sé stante, che si trova** a tutti gli effetti **"in competizione" con gli altri flussi** (rappresentati dagli altri thread); **ogni processo**, del resto, **può essere interrotto da un altro processo** in pressoché qualsiasi momento; infine, se il sistema su cui si lavora dispone di più di un processore, quasi sicuramente **diversi processi saranno in esecuzione contemporaneamente**. In questo contesto, è importantissimo parlare di **"sincronizzazione" tra threads**, in modo da assicurare l'esecuzione corretta di ciascuno di essi senza che si corrompano a vicenda o finiscano a manifestare comportamenti non previsti.

##### Race condition

Parlando di sincronizzazione tra threads, è importante pensare soprattutto al mantenere una **coerenza nelle strutture dati**, in modo che ciascun thread possa lavorare con dati che rappresentino accuratamente lo stato della sua esecuzione. Questa coerenza deve manifestarsi su due livelli diversi:
- una coerenza nelle **strutture dati private** di ciascun thread;
- una coerenza nelle **strutture dati condivise** tra più thread.

Se la prima è sostanzialmente garantita a priori grazie al meccanismo del "**context switch**", lo stesso non si può dire della seconda. Dunque, se due o più flussi di esecuzione condividono una determinata struttura dati, la loro concorrenza può determinare uno stato di tale struttura non coerente con la logica di ciascuno dei flussi: questo tipo di situazioni viene detto "**race condition**", e sono naturalmente situazioni da evitare il più possibile, soprattutto per la loro **natura non-deterministica**, nel senso che **lo stato finale della struttura dati dipende imprevedibilmente dall'ordine in cui i thread vengono eseguiti dal processore**.

Un esempio tipico di race condition basilare può essere il seguente: supponiamo di avere due thread `#1` e `#2`, che condividono una variabile `counter` e il cui codice è, per il thread `#1`:

```
for ( ; ; )
{
	crea_risorsa();
	counter = counter + 1;
}
```

e per il thread `#2`:

```
while (counter > 0)
{
	counter = counter - 1;
	consuma_risorsa();
}
```

In questo caso, la race condition è causata proprio dal comportamento della variabile `counter`, unico dato condiviso tra i due threads. In particolare, sono l'incremento e il decremento di `counter` a causare problemi, dato che non si tratta di cosiddette "**operazioni atomiche**", ossia **operazioni indivisibili che vengono eseguite per intero senza interruzioni**, ma piuttosto da operazioni divisibili in tre passi:
1. lettura del valore dalla memoria principale in un registro;
2. incremento (o decremento) del registro;
3. scrittura del valore dal registro alla memoria principale.

Ciò vuol dire che, ad esempio, potrebbe succedere la seguente successione di eventi (si suppone che `counter` parta da un valore pari a 2):
- nell'istante di tempo $t = 1$, il thread `#1` comincia l'esecuzione dell'istruzione `counter = counter + 1`, dunque carica in un registro $R_{0}$ il valore `counter` dalla memoria principale, e nell'istante seguente $t=2$ incrementa il registro $R_{0}$ di 1 (ora, $R_{0}$ conterrà il valore 3);
- nell'istante di tempo $t=3$, il thread `#2` interrompe l'esecuzione di `#1`, ed esegue a sua volta l'istruzione `counter = counter - 1`, procedendo dunque a caricare `counter` dalla memoria principale (dato che il thread `#1` non ha ancora scritto il nuovo valore di `counter` in memoria, esso sarà ancora pari a 2) in un registro $R_{1}$, a decrementare il registro $R_{1}$ di 1 nell'istante $t=4$ (ora, $R_{1}$ conterrà il valore 1), e a riscrivere il valore di $R_{1}$ nella variabile `counter` in memoria nell'istante $t=5$;
- a questo punto, nell'istante di tempo $t=6$, il controllo tornerà al thread `#1`, che scriverà il valore contenuto nel registro $R_{0}$ (ossia, 3) nella variabile `counter` in memoria principale, che però era stata precedentemente settata a 1 dal thread `#2`.

Insomma, è perfettamente possibile che si crei una situazione di incertezza, in cui l'ordine di esecuzione dei thread cambia drasticamente il risultato finale, e produce effetti incoerenti per almeno uno dei threads coinvolti.
___
##### Semafori e Mutex

In generale, una **sequenza di istruzioni di un flusso di esecuzione che accede a una struttura dati condivisa**, e quindi che **deve essere eseguita "atomicamente"**, ovvero senza la possibilità di essere interrotta da altri thread, viene detta "**regione critica**" (si specifica, per chiarezza, che seppur una regione critica debba essere eseguita "atomicamente", essa non è di per sé un'istruzione atomica). Il metodo più facile e comune per **proteggere una regione critica**, dunque per assicurarsi che essa venga effettivamente eseguita atomicamente, è il cosiddetto "semaforo".

Il concetto di "**semaforo**", contestualmente alla sincronizzazione tra threads, è stato inventato da E. W. Dijkstra negli anni '60, e si basa su una premessa molto semplice: in parole povere, esso consiste in un **contatore che indica il numero di copie disponibili di una certa risorsa**. Per comprendere meglio, si può pensare a un'analogia con i parcheggi per automobili: spesso, all'ingresso di tali parcheggi, c'è un tabellone che indica quanti posti sono attualmente liberi, e naturalmente se non ci sono posti liberi sarà impossibile entrare nel parcheggio; in questo contesto, si pensi al semaforo come al tabellone dell'esempio, che mostra ai threads quante copie della risorsa condivisa sono disponibili, e non permette il "passaggio" se attualmente sono tutte occupate. Il semaforo viene interamente gestito solo tramite **due operazioni atomiche**:
- **`wait`**, che **se invocata da un thread pone quest'ultimo in attesa che il contatore del semaforo diventi positivo** (dunque, che si liberi una risorsa), e appena lo diventa **procede a decrementarlo di 1** (appena si libera una risorsa, il thread in attesa va subito ad occuparla);
- **`signal`**, che **se invocata da un thread incrementa il contatore del semaforo di 1** (dunque, segnalando di aver appena terminato di utilizzare una risorsa).

In genere, **il contatore di un semaforo viene inizializzato con un valore $n > 0$**. In particolare, in base al valore $n$ effettivamente assegnato a tale contatore, si possono distinguere principalmente **due tipi di semafori**:
- il classico "**semaforo contatore**", in cui si ha $n>1$ e con cui, dunque, possono essere acquisite $n$ risorse in modo concorrente;
- il "**semaforo binario**", detto anche "**Mutex**" (da "Mutual Exclusion"), in cui si ha $n=1$ e con cui, dunque, può essere acquisita la risorsa da un solo flusso di esecuzione alla volta.
___
##### Mutex in POSIX

Approfondiamo, a questo punto, il secondo dei due, ossia il Mutex. Essi sono **implementati nello standard POSIX**, e possono essere dunque utilizzati con la **libreria `pthreads`** con cui abbiamo lavorato finora. In POSIX, il Mutex è implementato con il tipo di dato **`pthread_mutex_t`**, che contiene al suo interno:
- lo **stato** del Mutex ("aperto", dunque disponibile ad essere acquisito, o "chiuso", dunque già occupato da un altro thread);
- il **TID del thread attualmente in possesso del Mutex**;
- la **coda di threads in attesa** che la risorsa protetta dal Mutex si liberi.

Ogni entità di tipo `pthread_mutex_t`, dunque ogni Mutex, avrà poi un suo **insieme di attributi**, contenuti in una **[[SO2_04 - C#Strutture|struttura]] di tipo `pthread_mutexattr_t`**. Senza scendere troppo nei dettagli, tale struttura definisce principalmente il **comportamento del Mutex quando un thread cerca di effettuare un'operazione `lock`** (ossia cerca di acquisirlo) **o un'operazione `unlock`** (ossia cerca di liberarlo) **più volte consecutivamente**. Tali comportamenti determinano di quale dei seguenti tre tipi sarà il Mutex:
- **`fast`**, ossia un Mutex che, nell'eventualità in cui un thread esegua una `lock` due volte prima di aver eseguito un'`unlock`, **blocca il thread, con l'alto rischio di causare stalli** (non controlla, sostanzialmente, se il thread ad avere eseguito le due `lock` è lo stesso), mentre se un thread esegue un'`unlock` sul Mutex che deteneva esso **viene rilasciato immediatamente** (se, invece, un thread prova a sbloccare un Mutex che non era mai stato bloccato da tale thread, si potrebbero incorrere in crash o comportamenti imprevedibili);
- **`recursive`**, ossia un Mutex che, nell'eventualità in cui un thread esegua una `lock` due volte prima di aver eseguito un'`unlock`, **incrementa nuovamente un contatore che indica il numero di `lock` eseguite**, come se aggiungesse un ulteriore "lucchetto" alla medesima risorsa, senza bloccare il thread considerato, mentre se un thread esegue un'`unlock` sul Mutex che deteneva quest'ultimo non viene rilasciato immediatamente, ma **viene decrementato il contatore di `lock` eseguite**, e il Mutex sarà considerato effettivamente libero solamente quando tale contatore tornerà a 0 (come suggerisce il nome, questo tipo di Mutex torna utile quando si implementano funzioni ricorsive);
- **`error-checking`**, ossia un Mutex che, nell'eventualità in cui un thread esegua una `lock` due volte prima di aver eseguito un'`unlock`, **il thread non viene bloccato, ma viene restituito un codice di errore specifico** (si approfondiranno i codici di errore tra poco), e analogamente se un thread esegue un'`unlock` su un Mutex che non gli appartiene viene restituito un ulteriore codice di errore.

Per lavorare con Mutex nello standard POSIX, faremo riferimento principalmente alle seguenti **funzioni**:
- **`pthread_mutex_init`**;
- **`pthread_mutex_lock`**;
- **`pthread_mutex_trylock`**;
- **`pthread_mutex_unlock`**;
- **`pthread_mutex_destroy`**.

La funzione **`pthread_mutex_init`**, la cui sinossi completa è:

```
int pthread_mutex_init(pthread_mutex_t *mutex, const pthread_mutexattr_t *attr)
```

serve a **inizializzare il Mutex indicato dal puntatore `mutex`**, ponendolo inizialmente in uno stato "aperto" e **assegnandogli gli attributi indicati dal puntatore `attr`**; se il secondo puntatore, ossia `attr`, è uguale al valore nullo `NULL`, al Mutex da inizializzare sarà assegnato di default il tipo `fast`.

La funzione **`pthread_mutex_lock`**, la cui sinossi completa è:

```
int pthread_mutex_lock(pthread_mutex_t *mutex)
```

serve a **tentare di acquisire il Mutex indicato dal puntatore `mutex`**. Se quest'ultimo è libero, il thread lo acquisisce, ne diventa il proprietario e la chiamata alla funzione ritorna subito; invece, se il Mutex considerato è già occupato, il thread chiamante viene subito sospeso, e rimarrà tale finché il proprietario corrente del Mutex non lo rilascerà.

La funzione **`pthread_mutex_trylock`**, la cui sinossi completa è:

```
int pthread_mutex_trylock(pthread_mutex_t *mutex)
```

ha uno scopo pressoché identico a quello di `pthread_mutex_lock`, ossia **tentare di acquisire il Mutex indicato dal puntatore `mutex`**, ma con una fondamentale differenza: **se il Mutex `mutex` è già occupato, il thread chiamante non viene sospeso**, e quest'ultimo può dunque svolgere altri compiti in attesa che il Mutex venga rilasciato (supponendo, ovviamente, che il programmatore l'abbia previsto).

La funzione **`pthread_mutex_unlock`**, la cui sinossi completa è:

```
int pthread_mutex_unlock(pthread_mutex_t *mutex)
```

serve a **rilasciare il Mutex indicato dal puntatore `mutex`**. È importante ricordare che **un Mutex può essere sbloccato solamente dal thread che lo deteneva**, e che se un thread diverso da esso prova a rilasciarlo si verificherà un comportamento indefinito (o un errore esplicito, se il Mutex considerato è di tipo `error-checking`). Una volta che il Mutex viene rilasciato, **l'OS va a "risvegliare" uno degli eventuali thread che stavano attendendo questo evento** in seguito a una chiamata a `pthread_mutex_lock`, permettendogli così di acquisire il Mutex.

La funzione **`pthread_mutex_destroy`**, la cui sinossi completa è:

```
int pthread_mutex_destroy(pthread_mutex_t *mutex)
```

serve a **distruggere il Mutex indicato dal puntatore `mutex`**, liberando le risorse ad esso associate. Si tenga a mente che **si può distruggere un Mutex solamente se sbloccato e se nessun altro thread sta attendendo di poterlo acquisire**, in caso contrario la funzione `pthread_mutex_destroy` fallisce.

Tutte le funzioni appena analizzate **restituiscono `0` in caso di successo** e un **codice di errore diverso da `0` altrimenti**, ad eccezione di `pthread_mutex_init`, che restituisce sempre `0`. In particolare, possiamo approfondire i diversi **codici di errore** restituiti da tali funzioni in base a cosa è andato storto nella loro esecuzione:
- la funzione **`pthread_mutex_lock`** restituisce **`EINVAL`** se **il Mutex non è stato correttamente inizializzato**, oppure restituisce **`EDEADLK`** se **il Mutex è già acquisito dal thread chiamante** (quest'ultimo codice di errore viene restituito esplicitamente solo se il Mutex considerato è di tipo `error-checking`);
- la funzione **`pthread_mutex_trylock`** restituisce **`EINVAL`** se **il Mutex non è stato correttamente inizializzato**, oppure restituisce **`EBUSY`** se **il Mutex non è libero al momento della chiamata**;
- la funzione **`pthread_mutex_unlock`** restituisce **`EINVAL`** se **il Mutex non è stato correttamente inizializzato**, oppure restituisce **`EPERM`** se **il thread chiamante non è il proprietario del Mutex** (quest'ultimo codice di errore viene restituito esplicitamente solo se il Mutex considerato è di tipo `error-checking`);
- la funzione **`pthread_mutex_destroy`** restituisce **`EBUSY`** se **il Mutex non è libero al momento della chiamata**.

Ora che si hanno ben chiare le caratteristiche dei Mutex nello standard POSIX, così come le funzioni utilizzate per gestirli, è opportuno capire **come utilizzare concretamente i Mutex**. In generale, la prima cosa che conviene fare è **inizializzare il Mutex**, tramite una chiamata a `pthread_mutex_init`; in seguito, una volta creata la risorsa condivisa che si vuole proteggere con il Mutex creato, **qualsiasi accesso o modifica a tale risorsa dovrebbe essere "delimitata" da una chiamata `pthread_mutex_lock`** (o `pthread_mutex_trylock`, a seconda delle esigenze) **e una chiamata `pthread_mutex_unlock`**; infine, una volta certi che il Mutex considerato non serve più, lo si può **distruggere con una chiamata a `pthread_mutex_destroy`**.
___
##### Barriere

Un altro meccanismo di sincronizzazione tra threads, forse meno comune dei [[SO2_06 - Threads#Semafori e Mutex|semafori]] e dei [[SO2_06 - Threads#Mutex in POSIX|Mutex]] ma ugualmente importante, è costituito dalle cosiddette "**barriere**". A differenza dei semafori e dei Mutex, il cui ruolo è più che altro quello di proteggere risorse evitando che vengano "contaminate" da altri threads, le barriere vengono utilizzate per **coordinare l'esecuzione dei threads**, facendo in modo che **essi proseguano il loro flusso di esecuzione solo se tutti i threads hanno raggiunto un certo risultato**, che rappresenterà concretamente la "barriera" di cui stiamo parlando.

Nello standard POSIX, le barriere sono implementate tramite il **tipo di dato `pthread_barrier_t`**, che al suo interno contiene vari dati, tra cui:
- un "**target count**", ossia il numero di thread che devono raggiungere la barriera per fare in modo che essa "si apra", e dunque lasci proseguire a tali threads la loro esecuzione;
- un "**current count**", ossia il numero di thread attualmente in attesa di fronte alla barriera, che viene incrementato ogni volta che un nuovo thread giunge alla barriera stessa (si controlla costantemente se il current count è diventato uguale al target count, e solo in tal caso la barriera viene aperta).

Inoltre, come per i Mutex, ogni entità di tipo `pthread_barrier_t`, dunque ogni barriera, avrà poi un suo **insieme di attributi**, contenuti in una **[[SO2_04 - C#Strutture|struttura]] di tipo `pthread_barrierattr_t`**. Lo scopo principale degli attributi di una barriera è gestire il cosiddetto "**ambito di condivisione**", caratteristica che può essere modificata attraverso la seguente funzione:

```
int pthread_barrierattr_pshared(pthread_barrierattr_t *attr, int pshared)
```

Tale funzione prende come parametri **`attr`**, ossia un **puntatore all'oggetto `pthread_barrierattr_t` da modificare**, e **`pshared`**, ossia un **valore intero che determina l'ambito di condivisione della barriera**. In particolare, quest'ultimo parametro prevede solamente due possibili "modalità":
- **`PTHREAD_PROCESS_PRIVATE`** (modalità di default), che se settata fa in modo che **la barriera sia accessibile solo ai thread creati all'interno dello stesso processo che l'ha inizializzata**;
- **`PTHREAD_PROCESS_SHARED`**, che se settata fa in modo che **la barriera sia accessibile a qualsiasi thread, anche appartenenti a processi diversi**.
  
Utilizzare la seconda modalità, tuttavia, prevede un grado maggiore di attenzione e di sovrastruttura, dato che si dovrà creare la barriera da condividere in un'area di memoria speciale, che non sia di esclusiva proprietà del [[SO2_03 - Processi#Cos'è un processo?|processo]] che l'ha generata.

Per lavorare con barriere nello standard POSIX, faremo riferimento principalmente alle seguenti **funzioni**:
- **`pthread_barrier_init`**;
- **`pthread_barrier_wait`**;
- **`pthread_barrier_destroy`**.

La funzione **`pthread_barrier_init`**, la cui sinossi completa è:

```
int pthread_barrier_init(pthread_barrier_t *restrict barrier, const pthread_barrierattr_t *restrict attr, unsigned int count)
```

serve a **inizializzare la barriera indicata dal puntatore `barrier`, assegnandogli gli attributi indicati dal puntatore `attr`**; in particolare, se il puntatore `attr` è uguale al valore nullo `NULL`, alla barriera da inizializzare saranno assegnati attributi di default (primo su tutti, la modalità di condivisione `PTHREAD_PROCESS_PRIVATE`). Il terzo parametro, ossia l'intero senza segno **`count`**, rappresenta il **target count della barriera da inizializzare**, ossia il numero di thread che devono raggiungere la barriera affinché essa "si apra" (bisogna fare attenzione al valore da assegnare a `count`, dato che se si imposta tale parametro a un valore più alto del numero di threads effettivamente previsti, è praticamente certa l'eventualità di uno stallo).

La funzione **`pthread_barrier_wait`**, la cui sinossi completa è:

```
int pthread_barrier_wait(pthread_barrier_t *barrier)
```

serve a **far attendere il thread chiamante "di fronte" alla barriera `barrier`, in attesa che essa si apra**. Non appena un thread effettua una chiamata a tale funzione, la sua esecuzione viene sospesa, e i thread "addormentati" di fronte alla barriera vengono risvegliati contemporaneamente non appena si raggiunge il target count della stessa. Al risveglio dei thread, la funzione **restituisce `0` per quasi tutti i thread**, tranne che per uno scelto in modo casuale, a cui viene restituita la **costante speciale `PTHREAD_BARRIER_SERIAL_THREAD`**: tale costante torna utile in contesti in cui, tra una fase di esecuzione e l'altra, è necessaria un'operazione di pulizia o di unione dei dati ottenuti, operazione che deve essere svolta da un solo thread, e il thread in questione sarà proprio quello a cui è stata restituita la costante speciale. 

La funzione **`pthread_barrier_destroy`**, la cui sinossi completa è:

```
int pthread_barrier_destroy(pthread_barrier_t *barrier)
```

serve a **distruggere la barriera indicata dal puntatore `barrier`**, liberando le risorse ad essa associate. Si tenga a mente che **si può distruggere una barriera solamente se nessun thread sta attendendo che essa venga aperta**, in caso contrario la funzione `pthread_mutex_destroy` fallisce o porta a comportamenti indefiniti.
___
##### Condizioni

L'ultimo meccanismo di sincronizzazione dei threads che andremo a vedere è costituito dalle "**condizioni**", dette anche "**condition variables**". La specialità delle condizioni è il **sospendere l'esecuzione di un thread finché non diventa vera una determinata condizione su un dato condiviso**; in parole povere, serve a far aspettare l'avvenimento di un determinato evento a un thread.

Si tratta di un meccanismo fondamentale, e **sempre associato ai [[SO2_06 - Threads#Semafori e Mutex|Mutex]]**. Per capire meglio il perché, vediamo un semplice esempio. Supponiamo che un thread debba attendere che una variabile globale assuma il valore `1`; per fare ciò senza l'utilizzo di condizioni, si dovrebbe implementare una soluzione mediante un ciclo, che tipicamente assume la seguente forma generale:

```
pthread_mutex_lock(&mutex);

while (risorsa != 1)
{
	pthread_mutex_unlock(&mutex);
	// Attendi un po', poi riprova...
	pthread_mutex_lock(&mutex);
}
```

Un approccio del genere viene chiamato "**busy waiting**", ed è da evitare soprattutto per una questione di prestazioni: seppur non faccia concretamente nulla, il ciclo viene attivamente eseguito sul processore, mantenendolo occupato, e ciò rallenterà inevitabilmente l'esecuzione di altri threads o processi. Al tempo stesso, l'associazione tra Mutex e condizioni è necessaria per **evitare [[SO2_06 - Threads#Race condition|race conditions]] su una condizione** (potrebbe succedere, ad esempio, che un thread debba mettersi in attesa di una condizione e che un altro thread invii un segnale alla medesima condizione, sbloccandola, prima che il primo thread si sia effettivamente messo in attesa).

[tipo pthread_cond_t e pthread_condattr_t]

Per lavorare con condizioni nello standard POSIX, faremo riferimento principalmente alle seguenti **funzioni**:
- **`pthread_cond_init`**;
- **`pthread_cond_signal`**;
- **`pthread_cond_broadcast`**;
- **`pthread_cond_wait`**;
- **`pthread_cond_timedwait`**;
- **`pthread_cond_destroy`**.

La funzione **`pthread_cond_init`**, la cui sinossi completa è:

```
int pthread_cond_init(pthread_cond_t *cond, pthread_condattr_t *attr)
```



La funzione **`pthread_cond_signal`**, la cui sinossi completa è:

```
int pthread_cond_signal(pthread_cond_t *cond)
```



La funzione **`pthread_cond_broadcast`**, la cui sinossi completa è:

```
int pthread_cond_broadcast(pthread_cond_t *cond)
```



La funzione **`pthread_cond_wait`**, la cui sinossi completa è:

```
int pthread_cond_wait(pthread_cond_t *cond, pthread_mutex_t *mutex)
```



La funzione **`pthread_cond_timedwait`**, la cui sinossi completa è:

```
int pthread_cond_timedwait(pthread_cond_t *cond, pthread_mutex_t *mutex, const struct timespec *abstime)
```



La funzione **`pthread_cond_destroy`**, la cui sinossi completa è:

```
int pthread_cond_destroy(pthread_cond_t *cond)
```



[SLIDES: 17, pag. 18 - 19]
___