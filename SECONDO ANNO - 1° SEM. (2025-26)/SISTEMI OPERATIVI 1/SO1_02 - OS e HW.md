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

[slide 19]

In generale, in un qualsiasi calcolatore, l'HW deve supportare almeno la distinzione tra modalità kernel e modalità utente, ma spesso in calcolatori più moderni si sono adottate **soluzioni più complesse**, arrivando a progettare i cosiddetti "**anelli di protezione**". Infatti, aumentando i bit di stato da $1$ a $2$, diventa possibile contemplare un massimo di **4 livelli di "privilegio" diversi**, per una maggiore precisione nel controllo e nella protezione del sistema.

Fino ad adesso si è parlato di protezione e sicurezza soprattutto in relazione all'esecuzione di istruzioni, ma è importante anche la **protezione della memoria**. L'architettura sottostante di un calcolatore, infatti, deve permettere all'OS di **proteggere i programmi dell'utente uno dall'altro**, ma anche di **proteggere sé stesso dai programmi dell'utente**. La tecnica più semplice per implementare queste esigenze è avere **due registri specifici**, un "**registro base**" destinato a contenere **l'indirizzo di memoria di partenza del programma** e un "**registro limite**" destinato, invece, a contenere **l'ultimo indirizzo di memoria valido del programma**: all'inizio dell'esecuzione di un programma, l'OS carica i registri di base e di limite relativi ad esso, e durante l'esecuzione la CPU controllerà ogni indirizzo di memoria per verificare che si trovi nell'intervallo di memoria valido definito dai due registri.
___
## System calls, gestione delle eccezioni e operazioni di I/O

Le [[SO1_02 - OS e HW#Protezione e sicurezza|istruzioni privilegiate]] non possono essere eseguite in modalità utente in maniera diretta, ma programmi che vengono eseguiti in modalità utente possono chiedere all'OS di entrare in modalità kernel, eseguire certe istruzioni privilegiate, o in generale di effettuare alcune operazioni specifiche (ad esempio, scrivere dati in un file, inviare dati nella rete, ecc. ecc.): queste richieste vengono chiamate "**system calls**".

Queste "system calls" rientrano nella categoria di quelle che vengono definite "**trap**", ossia **qualsiasi evento che provoca il calcolatore a entrare in modalità kernel**. All'interno di questa categoria, troviamo principalmente tre tipi di eventi:
- le **system calls**, appunto, che vengono dette anche "**software traps**" in quanto consistono in richieste sincrone di un servizio fornito dall'OS e inizializzate da un qualche SW in esecuzione;
- le "**eccezioni**", dette anche "**faults**", che consistono in risposte sincrone a eventi eccezionali o inaspettati avvenuti durante l'esecuzione di un qualche SW (ad esempio istruzioni non definite, falle nella protezione, miss nella memoria, ecc. ecc.);
- le "**interrupt**", che consistono in eventi asincroni e inizializzati dall'HW (ad esempio il completamento di un'operazione I/O, un timer, ecc. ecc.).

[slide 39 - 43]

### Categorie di system call

In genere, una qualsiasi system call appartiene a una delle seguenti categorie in base alla mansione che svolge o al servizio che richiede:
- **controllo dei processi**;
- **gestione dei file**;
- **gestione dei dispositivi**;
- **"manutenzione" delle informazioni**;
- **comunicazioni**.

##### Controllo dei processi

Nella prima categoria, quella del **controllo dei processi**, rientrano tutte le system call atte a creare, caricare, eseguire o terminare processi, a ottenere o modificare determinati attributi di un processo, ad aspettare per un determinato lasso di tempo o per l'avvenimento di un evento particolare, o anche ad allocare o liberare memoria. [slide 48]
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
### Anatomia di una system call



[slide 73 - 74 - 78 - 80/84 - 86 - 91 - 92 - 94 - 95] 
___
## Scheduling e sincronizzazione

Per facilitare lo **scheduling** e la **sincronizzazione** tra i vari processi eseguiti in un calcolatore, una delle soluzioni più importanti è l'implementazione di un **timer**, concretamente rappresentato da un **clock a livello di HW**; in sistemi che permettono di eseguire più processi "contemporaneamente", il timer viene utilizzato per permettere alla CPU di non essere monopolizzata da un processo unico e di concentrarsi, volta per volta, sull'esecuzione di un programma diverso. Tipicamente, il timer genera un [[SO1_02 - OS e HW#System calls, gestione delle eccezioni e operazioni di I/O|interrupt]] a intervalli di tempo regolari, e in corrispondenza di ciascuno di questi interrupt il "**CPU scheduler**" prende il controllo e decide, volta per volta, su quale processo direzionare la CPU.

Tali interrupt, tuttavia, potrebbero interferire con l'esecuzione di alcuni processi: per evitare questa problematica, l'OS deve essere in grado di sincronizzare le attività dei vari processi, siano essi cooperanti o concorrenti, e perciò l'HW deve essere progettato in maniera tale che assicuri che **piccole sequenze di istruzioni contigue vengano eseguite atomicamente**. Ciò implica che:
- gli interrupt non possano avvenire durante l'esecuzione di queste sequenze;
- alcune istruzioni importanti vengano eseguite sempre.
___
## Memoria virtuale



[slide 109/111 - 114]
___