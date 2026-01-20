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


___

[09, slide 67 - 69 - 74 - 78 - 81 - 84 - 88 - 93 - 97 - 101 - 107 - 112 - 114 - 119 - 124 - 128 - 131 - 134 - 137 - 142 - 145 - 147/151 - 153 - 155/160 - 163 - 165 - 167 - 170 - 171]