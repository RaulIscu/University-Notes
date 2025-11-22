**Molte delle funzionalità di base dell'OS sono possibili grazie all'architettura dell'HW sottostante**: in base al supporto specifico del calcolatore, infatti, l'OS potrebbe avere alcune abilità piuttosto che altre, e alcuni aspetti della sua progettazione potrebbero essere semplificati o complicati.

In generale, possiamo identificare alcuni **servizi forniti dall'OS** che sono possibili, parzialmente o completamente, grazie al **supporto dell'HW**. Li riassumiamo nel seguente elenco:
- **protezione e sicurezza**;
- **system calls**;
- **gestione delle eccezioni**;
- **operazioni di I/O**;
- **scheduling**;
- **sincronizzazione**;
- **memoria virtuale**.

Nei capitoli seguenti, analizzeremo più nel dettaglio ciascuna delle righe di questa tabella.

## Protezione e sicurezza

Uno dei concetti più di base e, al contempo, più importanti nel funzionamento di un OS è quello delle "**istruzioni privilegiate**". Non tutte le istruzioni, infatti, hanno la stessa priorità nell'esecuzione, e alcune dovranno essere in grado di uscire dal normale flusso di esecuzione nella CPU, prendendo per certi versi il controllo.

Alcuni esempi di istruzioni del genere, solitamente, sono istruzioni che **mettono "in pausa" il sistema**, o che generano determinate "**interruzioni**" (le approfondiremo maggiormente in seguito). Essendo le istruzioni privilegiate più importanti e più impattanti sul funzionamento del calcolatore, generalmente **esse possono essere eseguite solo dall'OS**, e non direttamente dall'utente.

Un altro modo in cui viene garantita una maggiore sicurezza e protezione delle risorse del calcolatore è l'introduzione di una distinzione tra "**modalità utente**" e "**modalità kernel**". Possiamo vedere queste due modalità come due "stati" diversi del calcolatore durante l'esecuzione di istruzioni da parte della CPU:
- se il calcolatore si trova in modalità kernel, vengono sostanzialmente **sollevate tutte le restrizioni**, consentendo all'OS di eseguire qualsiasi istruzione (anche e soprattutto quelle privilegiate);
- se il calcolatore si trova in modalità utente, il calcolatore **presenta varie restrizioni all'utente**, in modo che esso non possa effettuare operazioni sensibili come accedere direttamente ai dispositivi di I/O, manipolare il contenuto della memoria principale, mettere in stallo il calcolatore o anche forzare il passaggio alla modalità kernel.

**La distinzione tra modalità kernel e modalità utente è implementata direttamente nell'HW**: ciò avviene grazie a un **bit di stato** conservato in un registro protetto della CPU (tendenzialmente, se tale bit è settato a $0$ ci si trova in modalità kernel, mentre se è settato a $1$ ci si trova in modalità utente).

In generale, in un qualsiasi calcolatore, l'HW deve supportare almeno la distinzione tra modalità kernel e modalità utente, ma spesso in calcolatori più moderni si sono adottate **soluzioni più complesse**, arrivando a progettare i cosiddetti "**anelli di protezione**". Infatti, aumentando i bit di stato da $1$ a $2$, diventa possibile contemplare un massimo di **4 livelli di "privilegio" diversi**, per una maggiore precisione nel controllo e nella protezione del sistema.

Fino ad adesso si è parlato di protezione e sicurezza soprattutto in relazione all'esecuzione di istruzioni, ma è importante anche la **protezione della memoria**. L'architettura sottostante di un calcolatore, infatti, deve permettere all'OS di **proteggere i programmi dell'utente uno dall'altro**, ma anche di **proteggere sé stesso dai programmi dell'utente**. La tecnica più semplice per implementare queste esigenze è avere **due registri specifici**, un "**registro base**" destinato a contenere **l'indirizzo di memoria di partenza del programma** e un "**registro limite**" destinato, invece, a contenere **l'ultimo indirizzo di memoria valido del programma**: all'inizio dell'esecuzione di un programma, l'OS carica i registri di base e di limite relativi ad esso, e durante l'esecuzione la CPU controllerà ogni indirizzo di memoria per verificare che si trovi nell'intervallo di memoria valido definito dai due registri.
___
## System calls, gestione delle eccezioni e operazioni di I/O

Le [[SO1_02 - OS e HW#Protezione e sicurezza|istruzioni privilegiate]] non possono essere eseguite in modalità utente in maniera diretta, ma programmi che vengono eseguiti in modalità utente possono chiedere all'OS di entrare in modalità kernel, eseguire certe istruzioni privilegiate, o in generale di effettuare alcune operazioni specifiche (ad esempio, scrivere dati in un file, inviare dati nella rete, ecc. ecc.): queste richieste vengono chiamate "**system calls**".

Queste "system calls" rientrano nella categoria di quelle che vengono definite "**trap**", ossia **qualsiasi evento che provoca il calcolatore a entrare in modalità kernel**. All'interno di questa categoria, troviamo principalmente tre tipi di eventi:
- le **system calls**, appunto, che vengono dette anche "**software traps**" in quanto consistono in richieste sincrone di un servizio fornito dall'OS e inizializzate da un qualche SW in esecuzione;
- le "**eccezioni**", dette anche "**faults**", che consistono in risposte sincrone a eventi eccezionali o inaspettati avvenuti durante l'esecuzione di un qualche SW (ad esempio istruzioni non definite, falle nella protezione, miss nella memoria, ecc. ecc.);
- le "**interrupt**", che consistono in eventi asincroni e inizializzati dall'HW (ad esempio il completamento di un'operazione I/O, un timer, ecc. ecc.).

### Categorie di system call

In genere, una qualsiasi system call appartiene a una delle seguenti categorie in base alla mansione che svolge o al servizio che richiede:
- **controllo dei processi**;
- **gestione dei file**;
- **gestione dei dispositivi**;
- **"manutenzione" delle informazioni**;
- **comunicazioni**.

##### Controllo dei processi

Nella prima categoria, quella del **controllo dei processi**, rientrano tutte le system call che:
- creano, caricano, eseguono o terminano processi;
- ottengono o modificano attributi relativi a un determinato processo;
- impongono uno stallo per un determinato lasso di tempo o in vista dell'avvenimento di un certo evento; 
- allocano o liberano memoria. 
___
##### Gestione dei file

Nella seconda categoria, quella della **gestione dei file**, rientrano le system call che:
- creano, cancellano, aprono, chiudono, leggono o scrivono uno o più file;
- ottengono o modificano attributi relativi a un determinato file. 

Si tratta, in realtà, di operazioni che sono spesso supportate non solo per i file veri e propri, ma anche per le directory.
___
##### Gestione dei dispositivi

Nella terza categoria, quella della **gestione dei dispositivi**, rientrano le system call che:
- richiedono o rilasciano un determinato dispositivo;
- leggono o scrivono dati all'interno di un determinato dispositivo;
- ottengono o modificano attributi relativi a un determinato dispositivo;
- gestiscono il collegamento e scollegamento concreto di un dispositivo al calcolatore. 

Ricordiamo che, quando si parla di "dispositivi", si intendono sia dispositivi fisici (come un hard disk) che dispositivi virtuali o "astratti" (come blocchi di memoria RAM). In alcune architetture, i dispositivi di questo tipo vengono rappresentati nel file system come una sorta di "file speciali".
___
##### Manutenzione delle informazioni

Nella quarta categoria, quella della **"manutenzione" delle informazioni**, rientrano le system call che:
- ottengono o modificano l'orario o la data memorizzata dal sistema;
- ottengono o modificano altri dati di sistema o attributi di vari processi, file o dispositivi. 

In questa categoria rientrano anche system call che vengono utilizzate in fase di "debugging", che vanno a mettere in pausa l'esecuzione di un programma ad ogni istruzione e a tracciare i risultati delle varie operazioni svolte.
___
##### Comunicazioni

Nella quinta categoria, quella delle **comunicazioni**, rientrano le system call che:
- creano o eliminano connessioni;
- inviano o ricevono messaggi;
- trasferiscono informazioni di stato;
- gestiscono la connessione e la disconnessione ad altri dispositivi remoti.

Tipicamente, qualsiasi forma di comunicazione in questo contesto rientra in uno di due "modelli":
- **scambio di messaggi**;
- **condivisione di memoria**.

Nel modello di scambio di messaggi, l'obiettivo è supportare system calls che possano identificare un processo remoto o un host con cui comunicare, stabilire una connessione tra i due processi, avviare o chiudere la connessione quando necessario, trasmettere messaggi sfruttando tale connessione e ricevere eventuali messaggi in arrivo. Si tratta di un modello di comunicazione relativamente semplice, soprattutto per la comunicazione tra calcolatori general-purpose, oltre che appropriata soprattutto per quantità piccole di dati.

Nel modello di condivisione di memoria, invece, l'obiettivo è più che altro creare della memoria condivisa tra più processi e thread, accedere a tale memoria quando necessario, fornire meccanismi di protezione che limitino gli accessi simultanei a tale memoria ed effettuare un'allocazione dinamica della stessa in base alle esigenze. In questo caso, si ha un modello più complesso ma anche più veloce, appropriato soprattutto per quantità più grandi di dati, e ideali quando i processi considerati vanno a effettuare più letture che scritture.
___
### Flusso di una system call

Concretamente, quando un programma in esecuzione vuole richiedere un servizio all'OS tramite una system call, non va ad eseguire direttamente tale system call, ma utilizza una forma di **API come ponte tra programma e system call**, che provoca la transizione [[SO1_02 - OS e HW#Protezione e sicurezza|da modalità utente a modalità kernel]] e, attraverso una cosiddetta "**system call interface**" e sfruttando una tabella relativa alle varie system call possibili, va a richiedere all'OS il servizio desiderato.

Di conseguenza, possiamo riassumere il **flusso** di una system call con il seguente schema, che mostra quello che succede chiamando la funzione `read()` in C:

![[syscall_anatomy_example.png]]

Capiamo, dallo schema, che al chiamante non interessa l'implementazione interna della system call, e la maggior parte dei dettagli sono infatti occultati dall'API: il chiamante, per poter richiedere la system call con successo, deve sapere esclusivamente i **parametri di input** e l'**output previsto**. Per comprendere più nel dettaglio come viene richiesta la system call, facciamo riferimento alla seguente immagine in cui viene nuovamente schematizzato l'esempio precedente:

![[syscall_anatomy_example1.png]]

Per chiamare la funzione `read()`, bisogna richiedere una specifica system call all'OS identificata univocamente da un certo numero **`$sys_read`**, che perciò viene memorizzato nel **registro `%eax`**. A quel punto, viene eseguita una **[[SO1_02 - OS e HW#System calls, gestione delle eccezioni e operazioni di I/O|trap]]** che porta alla **transizione del sistema a modalità kernel**, e grazie al suo numero identificativo (`0x80`) andando nella **IVT** (Interrupt Vector Table) l'OS sa che si vuole eseguire una system call. Ora, la system call specifica che si vuole eseguire viene individuata andando a riprendere il valore contenuto nel registro `%eax` e recuperando, all'interno della **tabella delle system call**, quella corrispondente al servizio richiesto (in questo esempio, **`sys_read()`**).

Come detto poco fa, l'esecuzione di una trap porta alla transizione da modalità utente a modalità kernel: per gestire questa transizione si dispone del cosiddetto "**system call handler**", le cui responsabilità sono le seguenti:
- **salvare lo stato del sistema** prima della transizione in registri appositi;
- **individuare ed eseguire la routine corretta** per la trap eseguita (nel nostro esempio, ciò corrisponde a cercare la system call appropriata nella tabella delle system call ed eseguirla);
- **ripristinare lo stato del sistema in modalità utente** una volta che la routine ha terminato di essere eseguita.

Spesso, quando viene richiesta una system call, per la sua esecuzione sono necessari più dati oltre al semplice identificatore: in questi contesti, è necessario avere un modo per **passare dei parametri all'OS**. Ci sono principalmente **3 modi** per farlo:
- memorizzare i parametri in **registri dedicati** (tale soluzione può risultare problematica nel momento in cui il numero di parametri supera quello dei registri allocati);
- memorizzare i parametri in un **blocco di dati** o in una **tabella** conservata in una zona specifica di memoria, passando quindi all'OS solo l'indirizzo di memoria dove si trovano tali parametri;
- far inserire al programma i parametri nello **stack**, e in seguito farli rilasciare dall'OS (seppur funzionante, si tratta di una soluzione più complessa soprattutto per la diversità tra i vari indirizzi di memoria).
___
## Scheduling e sincronizzazione

Per facilitare lo **scheduling** e la **sincronizzazione** tra i vari processi eseguiti in un calcolatore, una delle soluzioni più importanti è l'implementazione di un **timer**, concretamente rappresentato da un **clock a livello di HW**; in sistemi che permettono di eseguire più processi "contemporaneamente", il timer viene utilizzato per permettere alla CPU di non essere monopolizzata da un processo unico e di concentrarsi, volta per volta, sull'esecuzione di un programma diverso. Tipicamente, il timer genera un [[SO1_02 - OS e HW#System calls, gestione delle eccezioni e operazioni di I/O|interrupt]] a intervalli di tempo regolari, e in corrispondenza di ciascuno di questi interrupt il "**CPU scheduler**" prende il controllo e decide, volta per volta, su quale processo direzionare la CPU.

Tali interrupt, tuttavia, potrebbero interferire con l'esecuzione di alcuni processi: per evitare questa problematica, l'OS deve essere in grado di sincronizzare le attività dei vari processi, siano essi cooperanti o concorrenti, e perciò l'HW deve essere progettato in maniera tale che assicuri che **piccole sequenze di istruzioni contigue vengano eseguite atomicamente**. Ciò implica che:
- gli interrupt non possano avvenire durante l'esecuzione di queste sequenze;
- alcune istruzioni importanti vengano eseguite sempre.
___
## Memoria virtuale

La **memoria virtuale** consiste in un'**astrazione della memoria principale** effettiva, concretamente contenuta nel calcolatore. Si tratta di un espediente per dare l'**illusione**, ai vari processi e dunque indirettamente anche all'utente, **che la memoria del calcolatore sia uno spazio contiguo**, o che sia più capiente di quello che effettivamente è. Permette, inoltre, di **eseguire programmi non completamente caricati nella memoria principale**, premettendo però che essi siano completamente "caricati" nella memoria virtuale.

La memoria virtuale viene implementata sia a livello di **HW** che a livello di **SW**:
- a livello di HW, si dispone di una **MMU** (**Memory Management Unit**), responsabile della traduzione di indirizzi di memoria virtuali in indirizzi fisici, e viceversa;
- a livello di SW, l'OS è responsabile della gestione degli indirizzi di memoria virtuali.

Tipicamente, la memoria virtuale è divisa in "**pagine**", o "**pages**", blocchi di memoria tutti della stessa grandezza (in maniera analoga alla memoria fisica); le pagine di memoria virtuale che non sono caricate nella memoria principale sono contenute nella memoria a disco.

Vediamo più nel dettaglio la **MMU**. Quest'unità si occupa di abbinare indirizzi virtuali a indirizzi di memoria fisici basandosi su una "**page table**", gestita dall'OS. Al tempo stesso, per velocizzare gli accessi a blocchi di memoria frequentemente utilizzati o vicini tra loro, dispone di una forma di cache chiamata "**Translation Look-aside Buffer**", o **TLB** in breve.
___