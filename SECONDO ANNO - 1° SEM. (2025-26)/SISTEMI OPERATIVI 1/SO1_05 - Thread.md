Finora, parlando di [[SO1_03 - Processi|processi]], abbiamo sempre dato per scontato che un singolo processo esegue un programma seguendo un unico "filo", in maniera lineare e statica. Tuttavia, **tutti gli OS moderni ormai consentono a un singolo processo di seguire più strade contemporaneamente nella loro esecuzione**. Ciò di cui si sta parlando diventerà più chiaro introducendo l'argomento centrale di questo capitolo, ossia i "**thread**".

## Cos'è un thread?

Ciò che viene chiamato "**thread**" può essere definito come un'**unità dell'utilizzo della CPU**, composta da componenti come:
- un **program counter** (o **PC**);
- uno **[[SO1_03 - Processi#Un approfondimento sullo Stack|stack]]**;
- un **insieme di registri**;
- un **ID**.

Ora, un processo "tradizionale", tipico di sistemi ormai obsoleti, dispongono di **un unico thread**, dunque di un solo PC, e un'unica sequenza di istruzioni che può essere eseguita. Tuttavia, la maggior parte delle applicazioni moderne sono "**multi-threaded**", e permettono a **singoli processi** di avere **più thread**, che condividono però lo stesso codice, gli stessi dati, ed eventualmente le stesse risorse (ad esempio eventuali file aperti).

##### Differenze tra un thread e un processo

Può confondere il dover **distinguere tra thread e processo**: a primo impatto, infatti, potrebbe sembrare che un thread non è altro che un'altra forma di processo, un modo diverso per definire sostanzialmente la stessa cosa. In realtà non è così, e la differenza si trova sia nella **composizione concreta** delle due entità, sia nella "**gerarchia**" in cui si trovano.

Mentre un processo è definito da uno spazio di indirizzamento, un programma da eseguire (e, dunque, del codice), dei dati e delle risorse da utilizzare, e così via, **un thread è definito da un singolo flusso sequenziale di esecuzione all'interno di uno stesso processo**, dunque puramente da componenti come un PC, uno stack o un insieme di registri. Il processo è **colui che definisce il lavoro da svolgere e i mezzi per farlo** (possiamo vederlo come il coordinatore di un gruppo di lavoratori), mentre i thread sono **le varie strade attraverso cui il lavoro viene effettivamente svolto** (possiamo vederli come il gruppo di lavoratori).

Ogni processo, dunque, potrà avere uno o più thread, e **tutti i thread di un processo condivideranno il suo spazio di indirizzamento**. Si tratta di una soluzione molto comoda e intuitiva anche rispetto ai [[SO1_03 - Processi#Come comunicano i processi tra di loro?|processi cooperanti]] visti un paio di capitoli fa, dato che in questo caso non sono necessarie system call o implementazioni particolari per far cooperare i vari thread.
___
##### Perché fa comodo utilizzare più thread?

Suddividere il lavoro svolto da un processo in più thread può essere notevolmente utile, soprattutto in contesti in cui **un processo dispone di più mansioni indipendenti una dall'altra da svolgere**; banalmente, avere più thread consente ad esempio di continuare a lavorare su altre mansioni nel momento in cui una di queste viene sospesa per una richiesta di I/O. 

Un esempio concreto potrebbe essere un comune text editor: se il processo relativo ad esso dispone di più thread, si possono fornire parallelamente le seguenti funzionalità (ciascuna assegnata a un singolo thread):
- controllo della grammatica;
- gestione dell'input dell'utente;
- backup periodici del file di testo.

Ancora, avere più thread può essere utile anche nel contesto di un web server: disporre di più thread permette di poter rispondere a più richieste simultaneamente, evitando invece di considerare una richiesta alla volta in modo sequenziale.

Può sorgere, ciononostante, un dubbio: **creare un processo multi-threaded non equivale a creare più "sotto-processi" single-threaded?** Per rispondere a questa domanda, identifichiamo principalmente due motivi per cui si preferisce la prima alternativa alla seconda:
- **la comunicazione tra thread di uno stesso processo è molto più veloce della comunicazione tra processi**;
- **i context switch tra due thread sono più veloci dei context switch tra processi**.

Andando a generalizzare, possiamo trovare **4 pregi principali** dell'utilizzo di thread:
- **maggiore reattività**, ad esempio nel contesto in cui, mentre dei thread sono bloccati o rallentati da determinate attività, altri potranno comunque fornire risposte rapide;
- **maggiore condivisione di risorse**, dato che i thread condividono lo stesso programma da eseguire, gli stessi dati e lo stesso spazio di indirizzamento;
- **maggiore efficienza e minor lavoro da svolgere**, dato che creare e gestire thread è molto più veloce e facile per l'OS rispetto al fare le stesse operazioni per dei processi;
- **maggiore scalabilità**, data dal fatto che mentre un processo single-threaded può essere eseguito solo su un'unica CPU, un processo multi-threaded può eventualmente essere eseguito su più processori o core, se il calcolatore ne dispone.

La tendenza moderna a creare CPU multi-core va a giovare particolarmente all'ultimo punto, facilitando notevolmente la diffusione delle applicazioni multi-threaded.
___
## Parallelismo

La presenza di **più [[SO1_05 - Thread#Cos'è un thread?|thread]] in un processo** e, allo stesso tempo, di **più core in un unico sistema**, permette a tutti gli effetti di implementare del "**parallelismo**" nella programmazione e nell'esecuzione di programmi. In particolare, distinguiamo tra **due tipi** principali di parallelismo:
- il "**parallelismo sui dati**", che consiste nel dividere i dati su cui lavorare tra i vari thread, e di far eseguire a ogni thread la stessa mansione sul rispettivo sottoinsieme di dati;
- il "**parallelismo sulle mansioni**", che consiste nel dividere le varie mansioni da svolgere tra i vari thread, in modo che ogni thread ne esegua una parallelamente agli altri.

Per capire **come implementare il parallelismo** concretamente, vediamo un esempio. Supponiamo ci venga chiesto di scrivere un programma molto semplice, che prenda come input un intero positivo $N$ e restituisca come output la somma degli interi compresi tra $1$ e $N$. Una soluzione immediata potrebbe essere la seguente:

```
int sum = 0;

for (int i = 0; i <= N; ++i) {
	sum += i;
}

return sum;
```

Si tratta di una soluzione giustissima, che restituirà il risultato desiderato, ma che al crescere di $N$ può diventare lenta e inefficiente; d'altro canto, è una soluzione single-threaded per natura. Ma possiamo trovare soluzioni più efficienti.

Consideriamo varie combinazioni di:
- numero di core;
- numero di processi;
- numero di thread;

e vediamo in ogni caso quello che succede. Partiamo dal caso base, e supponiamo di disporre di **$1$ core e di $1$ processo single-threaded**: questo caso rispecchia perfettamente l'esempio di soluzione fornito poco fa, e rappresenta una soluzione che **non implementa né il parallelismo, né la concorrenza** (ossia sostanzialmente lo pseudo-parallelismo, l'illusione che la CPU esegua più mansioni quando in realtà esegue una mansione per volta ma cambiando molto spesso mansione). 

Facciamo, ora, un passo avanti, e consideriamo un assetto con **$1$ core e $M$ processi single-threaded**: in questo caso, si potrebbe dividere l'intervallo di interi $[1,\,N]$ in $M$ sotto-intervalli, e assegnare a ognuno degli $M$ processi il compito di calcolare la somma dei numeri contenuti in uno di questi sotto-intervalli; questa soluzione **non implementa il parallelismo, ma sfrutta la concorrenza** tra più processi, eppure non velocizza in alcun modo il calcolo desiderato, dato che il processore potrà comunque eseguire un solo processo alla volta e si dovrà attendere il termine di tutte le esecuzioni per ottenere il risultato finale. 

A questo punto, vediamo se un approccio con **$1$ core e $1$ processo con $M$ thread** aiuta: anche in questo caso, in realtà, non si velocizza il calcolo desiderato, e ci si trova in una situazione pressoché analoga a quella precedente (il processore può eseguire un singolo thread alla volta, dunque la soluzione **implementa la concorrenza ma non il parallelismo**), con l'unico vantaggio che è l'assenza di [[SO1_03 - Processi#Come comunicano i processi tra di loro?|processi cooperanti]] in favore della comunicazione tra thread. 

E se considerassimo un sistema con **$M$ core e un numero di $M$ processi single-threaded**? In questo caso, per la prima volta finora, si avrebbe una **vera implementazione di parallelismo**, e conseguentemente una velocizzazione del calcolo desiderato. Tuttavia, nonostante ciò, ciascun processo dovrà comunque comunicare con gli altri per combinare le varie somme parziali, operazione che può diminuire l'efficienza del tutto.

Arriviamo così alla **soluzione ottimale**, ossia utilizzare **$M$ core e $1$ processo dotato di $M$ thread**: in questo modo, si implementerà ugualmente il parallelismo e, allo stesso tempo, si eviterà la presenza di processi comunicanti, velocizzando ulteriormente il tutto.

[09, slide 74 - 78 - 81]
___
## Come si implementa un processo multi-threaded?

Per poter avere un processo multi-threaded, **il sistema deve fornire supporto per la possibilità di più thread in un singolo processo**. Questo supporto può essere fornito principalmente in due modi:
- con i "**kernel threads**";
- con gli "**user threads**".

Vediamo più nel dettaglio cosa implica ciascuna di queste soluzioni.

##### Kernel threads

I **kernel threads** sono **gestiti direttamente**, come suggerisce il nome, **dal [[SO1_01 - Introduzione#Cos'è un sistema operativo?|kernel]] stesso dell'OS**, e rappresentano sostanzialmente la più piccola unità di esecuzione che può essere gestita dall'OS.

L'OS è interamente responsabile della gestione e del supporto di tutti i kernel threads, e predispone **un [[SO1_03 - Processi#Il PCB|PCB]] per ogni processo** e **un TCB** (**Thread Control Block**) **per ogni thread del processo**. Al tempo stesso, solitamente l'OS dispone anche di [[SO1_02 - OS e HW#System calls, gestione delle eccezioni e operazioni di I/O|system call]] apposite per la creazione e la gestione dei kernel threads "da parte dell'utente".

Questo tipo di thread presenta vari **pregi**, tra cui:
- il **pieno controllo da parte del kernel**, che ha conoscenza completa di tutti i thread in esecuzione;
- la **facilità di comunicazione tra thread di uno stesso processo** piuttosto che tra più processi;
- la **libertà di azione dello scheduler**, che può gestire i processi e i thread per in modo ottimale (ad esempio, mandando in esecuzione nella CPU per più tempo un processo con un gran numero di thread).

Può presentare, però, anche dei **difetti**, tra cui:
- una **maggiore complessità del kernel**, oltre che un **carico maggiore di lavoro** dovuto proprio al dover gestire i vari thread del processo;
- un **rallentamento** e una certa **inefficienza**, dovuta al continuo bisogno di system calls e di context switch che, seppur relativamente leggeri, avvengono molto spesso e implicano ogni volta una transizione tra modalità utente e modalità kernel, o viceversa.

Sostanzialmente, i kernel threads sono quelli che abbiamo visto finora, dunque quelli gestiti dall'OS e di cui quest'ultimo ha piena conoscenza. Possiamo visualizzare la gestione dei kernel threads con il seguente schema:

![[kernel_threads.png]]

dove **process table** e **thread table** sono due strutture fondamentali, la prima per la gestione dei processi e la seconda per i thread relativi ai vari processi. Una delle maggiori inefficienze sta proprio nel bisogno di **conservare e aggiornare costantemente i TCB di tutti i thread nella thread table**, che all'aumentare del carico di lavoro può diventare un'operazione molto dispendiosa per l'OS.
___
##### User threads

Se i [[SO1_05 - Thread#Kernel threads|kernel threads]] erano gestiti in tutto e per tutto dall'OS, gli **user threads** si distinguono per essere **gestiti direttamente nello spazio utente, solitamente da una libreria per thread**, senza alcun intervento da parte dell'OS. In questo caso, **l'OS conosce solo il processo che contiene gli user threads**, senza avere alcuna conoscenza dei threads effettivi, e tratterà tale processo come se si trattasse di un normale processo single-threaded; la libreria per thread, invece, si occuperà della gestione dei thread del processo senza bisogno di scheduler o di transizioni tra modalità utente e modalità kernel.

Vediamo i principali **pregi** degli user threads:
- generalmente, sono più **veloci e leggeri** rispetto ai kernel threads;
- consentono uno **scheduling più flessibile** dei loro processi;
- **possono essere implementati anche in OS che**, di norma, **non supportano il multi-threading**;
- **non sono necessarie system call bloccanti**, e la cosa più vicina a una system call bloccante che viene utilizzata in questo contesto è la chiamata a funzione, che naturalmente risulta essere molto più veloce;
- dato che l'OS vede un processo multi-threaded con user threads come un processo single-threaded, **non ci sarà bisogno di effettuare context switch** per passare da uno user thread all'altro.

Ci sono, tuttavia, anche dei **difetti**:
- in questo contesto, **non potrà mai verificarsi una concorrenza tra più processi multi-threaded**;
- spesso i sistemi a runtime forniti dalle librerie per thread effettuano delle **decisioni di scheduling non ottimali**;
- **è assente una coordinazione tra kernel e thread**, e ciò diventa un problema ad esempio nel caso in cui un processo che dispone di $100$ user threads compete, per essere eseguito nella CPU, con un processo che dispone di un solo kernel thread;
- anche se non sono necessarie system call bloccanti, **servono comunque delle system call non bloccanti**.

Possiamo visualizzare la gestione degli user threads con il seguente schema:

![[user_threads.png]]
___
##### Librerie per thread

Nel [[SO1_05 - Thread#User threads|paragrafo precedente]] si sono fatte varie menzioni delle cosiddette "librerie per thread". Ma **cosa sono**, effettivamente, **le librerie per thread?** Si tratta, come suggerisce il nome, di **librerie**, o per certi versi di **API**, **che forniscono ai programmatori vari strumenti per creare e gestire thread**, siano essi [[SO1_05 - Thread#Kernel threads|kernel thread]] o user thread.

Essendoci due tipi principali di thread, ci sono anche **due metodi principali di implementazione di una libreria per thread**:
- nello **spazio utente**, tramite funzioni di una API che funzionano interamente in modalità utente;
- nello **spazio kernel**, tramite system call che delegano al kernel la responsabilità di supportare e gestire i thread.

Volendo fare degli esempi concreti, al giorno d'oggi possiamo individuare **3 librerie per thread ampiamente utilizzate**:
- i "**POSIX Pthreads**", che rappresentano un'estensione dello standard POSIX e possono presentarsi sia come kernel threads che come user threads;
- i "**Win32 threads**", che sono generalmente implementati come kernel threads su sistemi Windows;
- i "**Java threads**", la cui implementazione dipende fortemente dall'OS e dall'HW del calcolatore in questione.
___
##### Comunicazione tra kernel threads e user threads

Nel concreto, deve esistere necessariamente una qualche forma di **comunicazione tra [[SO1_05 - Thread#Kernel threads|kernel threads]] e [[SO1_05 - Thread#User threads|user threads]]**. Questa comunicazione può essere visualizzata sottoforma di una **mappatura** tra questi due tipi di thread, mappatura che può avvenire nei seguenti modi:
- **molti-a-uno** (**N:1**);
- **uno-a-uno** (**1:1**);
- **molti-a-molti** (**N:M**);
- **two-level**.

Il modello **molti-a-uno**, o in breve **N:1**, va a **mappare più user threads a un singolo kernel thread**. In questo contesto, naturalmente, il processo potrà eseguire un solo user thread alla volta dato che è associato a un unico kernel thread; inoltre, dato che un singolo kernel thread può operare su un'unica CPU, dei processi multi-threaded con più user threads non potranno essere divisi tra più CPU seguendo questo modello. Di conseguenza, se ad esempio viene fatta una system call bloccante, l'esecuzione dell'intero processo viene bloccata, anche se altri user thread avrebbero potuto continuare ad essere eseguiti.

Il modello **uno-a-uno**, o in breve **1:1**, va a **mappare ogni user thread a un singolo kernel thread**. In questo contesto, le limitazioni relative alle system call bloccanti e all'esecuzione di più thread in una singola CPU vengono meno, ma si aggiunge un rallentamento dovuto alla gestione di più kernel thread. La maggior parte delle implementazioni di questo modello, poi, pongono un limite al numero di thread che possono essere creati, e ciò può essere un problema all'aumentare del carico di lavoro che si desidera eseguire.

Il modello **molti-a-molti**, o in breve **N:M**, va a **mappare un certo numero di user thread a un numero minore o uguale di kernel thread**. Si ottiene, in questo modo, il meglio dei due approcci precedenti: dal modello N:1 l'assenza di limiti su quanti user threads possono essere creati, dal modello 1:1 la possibilità di dividere un singolo processo multi-threaded tra più CPU e il non dover bloccare l'intero processo in occasione di una system call.

Il modello **two-level** rappresenta, in realtà, semplicemente un'**unione tra i modelli N:M e 1:1**, dunque in cui può avvenire sia uno che l'altro tipo di mappatura tra kernel thread e user thread. Ciò fornisce una maggiore flessibilità, soprattutto in termini di [[SO1_04 - Scheduling della CPU|scheduling]].

Possiamo riassumere le caratteristiche principali dei modelli visti nella seguente tabella:

![[modelli_thread_tabella.png]]
___
##### Thread pool

Supponendo di avere un processo multi-threaded, quando il processo viene avviato vengono creati un certo numero di thread; tuttavia, questi thread non iniziano subito ad eseguire una qualche mansione. 

Prima che i thread svolgano effettivamente del lavoro, essi risiedono in una cosiddetta "**thread pool**": ogni qualvolta che il processo ha bisogno di svolgere una mansione, "sveglia" un thread da questa thread pool, e quando tale thread ha finito la sua esecuzione esso ritorna nella thread pool in attesa di ulteriori direttive. Nell'eventualità in cui non ci siano thread nella thread pool (e, dunque, stiano tutti svolgendo una qualche mansione), il processo dovrà attendere che se ne liberi uno per poter procedere.
___
##### Scheduling dei thread

Partendo dal **[[SO1_05 - Thread#Comunicazione tra kernel threads e user threads|modello N:M]]** di comunicazione tra kernel threads e user threads, che abbiamo visto essere uno dei più efficienti e versatili, vediamo più nel dettaglio come avviene lo **scheduling dei threads ai processori del calcolatore**, e in particolare come viene gestita l'**interfaccia tra user thread e HW**.

Le implementazioni del modello N:M forniscono innanzitutto delle "interfacce" tra user threads e kernel threads, che possiamo chiamare "**lightweight process**", o **LWP**: ciascun LWP è mappato a un unico kernel thread da un lato, e può essere mappato a più user threads dall'altro, con la mappatura degli user threads a eventuali LWP disponibili che viene gestita dal livello utente della [[SO1_05 - Thread#Librerie per thread|libreria per thread]] utilizzata. Dunque, grazie ai LWP, gli user threads potranno essere mappati a un numero minore o uguale di kernel threads, e in seguito questi ultimi potranno essere gestiti dall'OS e messi in esecuzione nei vari processori del calcolatore. Possiamo riassumere quanto appena detto nel seguente schema, dotato anche di legenda:

![[lwp_schema.png]]

Si tratta di un sistema dinamico, in cui **il numero di kernel thread disponibili può variare in base alle esigenze di esecuzione**. Per capire meglio cosa si intende, vediamo un esempio concreto. Supponiamo di avere un processo con $3$ user threads in esecuzione su un singolo kernel thread, in una struttura del genere: 

![[user_thread_scheduling_esempio.png]]

A questo punto, mettiamo caso che lo user thread in esecuzione effettui una system call bloccante: ciò porterebbe il kernel a bloccare il kernel thread da cui è arrivata la system call, e di conseguenza l'LWP ad esso associato e, perciò, tutti gli user thread associati a quest'ultimo. Per evitare che l'intero processo rimanga bloccato a causa della system call effettuata da un unico user thread, il kernel decide di allocare un nuovo kernel thread al processo, e notifica la libreria per thread nello spazio utente di ciò (tale operazione è detta "**upcall**"); in questo modo, tramite il cosiddetto "**upcall handler**", la libreria per thread nello spazio utente andrà a ri-suddividere gli user thread del processo considerato, lasciando il thread bloccato mappato al kernel thread originario, e associando gli altri $2$ thread al kernel thread appena fornito dal kernel. In questo modo, si passa da questa situazione:

![[user_thread_scheduling_esempio1.png]]

a questa situazione:

![[user_thread_scheduling_esempio2.png]]

Ma come avviene, invece, lo **scheduling dei singoli user threads sul kernel thread** ad essi associato? In questo caso lo scheduling avviene **interamente nello spazio utente** ed è gestito dalla libreria per thread. Ci sono principalmente tre approcci a questa forma di scheduling:
- **scheduling cooperativo**;
- **preemptive scheduling**;
- **scheduling ibrido**.

Lo **scheduling cooperativo** funziona in modo molto simile al [[SO1_04 - Scheduling della CPU#Introduzione allo scheduling|non-preemptive scheduling]] che avviene in relazione alla CPU; uno user thread rimane in esecuzione finché non rilascia volontariamente il kernel thread, e solo a quel punto la libreria manda in esecuzione un altro user thread. In particolare, i thread sospendono la loro esecuzione in favore di altri o **esplicitamente**, chiamando una funzione di tipo `yield()` fornita dalla libreria per thread, o **implicitamente**, richiedendo un dato o un evento che dipende da un altro thread.

Il **preemptive scheduling**, invece, funziona in modo analogo al preemptive scheduling che avviene in relazione alla CPU; sfruttando un timer, i thread vengono periodicamente sostituiti a quanti di tempo regolari, e dunque un thread in esecuzione viene rimpiazzato non solo quando rilascia volontariamente il kernel thread, ma anche al termine di un quanto di tempo.

Lo **scheduling ibrido**, molto semplicemente, consiste in un'unione tra scheduling cooperativo e preemptive scheduling.
___