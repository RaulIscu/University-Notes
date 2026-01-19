In questo capitolo, si approfondirà un aspetto trattato in parte nel [[SO1_03 - I processi#Come vengono programmati i processi nella CPU?|capitolo precedente]]: lo **scheduling dei processi all'interno della CPU**. In particolare, partiremo con un'introduzione generale, soffermandoci sulle definizioni e i concetti di base, e passeremo in seguito a vari algoritmi e concetti più avanzati applicabili a tale argomento.

## Introduzione allo scheduling

Sappiamo bene che pressoché qualsiasi programma alterna, in qualche modo, fasi incentrate sulla **computazione nella CPU** a fasi che dipendono dall'**I/O**. Assumendo di avere un sistema in grado di eseguire un solo processo alla volta, il tempo passato ad attendere un dato o un evento di I/O è sostanzialmente sprecato, dato che è un lasso di tempo in cui la CPU non lavora e non contribuisce all'esecuzione del [[SO1_03 - I processi|processo]]. Questa rappresenta una delle problematiche principali a cui deve provvedere lo **scheduling**: l'obiettivo, dunque, è sostanzialmente **ottimizzare l'esecuzione dei processi, massimizzando la produttività della CPU e garantendo un'equità di esecuzione tra i vari processi**.

Come abbiamo già anticipato, tutti i processi gestiti dall'OS risiedono in esattamente una delle varie **process state queues**; inoltre, possiamo affermare che tutti i processi si alternano tra **due stati possibili** in un ciclo continuo:
- uno "**slancio di CPU**";
- uno "**slancio di I/O**".

Il primo dei due corrisponde alla fase dell'esecuzione incentrata sui calcoli e sulle operazioni svolte grazie alla CPU, mentre il secondo corrisponde alla fase dell'esecuzione dedicata all'attesa del trasferimento di dati in invio o in ricezione. Nella maggioranza dei casi, **gli slanci di CPU hanno una durata breve**, mentre **gli slanci di I/O portano ad attese prolungate**.

L'obiettivo di uno **scheduler**, dunque, è quello innanzitutto di **assegnare un nuovo processo da eseguire alla CPU non appena questa diventa inattiva**: quando ciò accade, lo scheduler va a prendere un processo dalla process state queue relativa allo stato `ready`, dunque un processo che è pronto per essere eseguito, e attiva la sua esecuzione all'interno della CPU, rimuovendo quello che la occupava in precedenza. L'algoritmo con cui lo scheduler sceglie il processo da mandare in esecuzione non si basa necessariamente su una coda di tipo FIFO (First In, First Out), ma dipende dall'implementazione specifica e dall'obiettivo con maggiore priorità.

In generale, **lo scheduling della CPU si attiva quando si verifica una delle seguenti 4 condizioni**:
1. quando un processo passa **dallo stato `running` allo stato `waiting`**, ad esempio in attesa di una risposta I/O o dell'esecuzione di una system call;
2. quando un processo passa **dallo stato `running` allo stato `ready`**, ad esempio in risposta a un interrupt;
3. quando un processo passa **dallo stato `waiting` allo stato `ready`**, ad esempio in seguito al completamento di una richiesta di I/O o al termine di una chiamata `wait()`;
4. quando un processo viene **creato** o **terminato**.

In particolare, nel primo e nell'ultimo caso generalmente lo scheduler è **forzato a scambiare il processo attualmente considerato con uno nuovo**, mentre nel secondo e nel terzo caso, in base al contesto, esso può **scegliere di eseguire un nuovo processo o di continuare con quello attuale**. In base a quale dei due approcci viene scelto, si distingue tra due tipi diversi di scheduling:
- il "**non-preemptive scheduling**", ossia lo scheduling che avviene solo quando non si ha altra scelta, come nelle condizioni $1$ e $4$ (in questo tipo di sistema, una volta che un processo inizia la sua esecuzione nella CPU esso non potrà essere sospeso dallo scheduler, a meno che il processo stesso non sospenda da solo la sua esecuzione o la termini);
- il "**preemptive scheduling**", ossia lo scheduling che avviene non solo quando non si ha altra scelta, ma anche in condizioni come la $2$ e la $3$ (in questo tipo di sistema, lo scheduler ha il pieno controllo sui processi che vengono eseguiti nella CPU).

Come si può immaginare, il non-preemptive scheduling è un approccio ormai antiquato e che presenta vari limiti, mentre il preemptive scheduling è diventato lo standard per gli OS moderni. Ciononostante, l'implementazione del preemptive scheduling può presentare delle **problematiche**: ad esempio, potrebbe causare comportamenti imprevisti se avviene durante l'esecuzione di una system call, oppure contestualmente a [[SO1_03 - I processi#Come comunicano i processi tra di loro?|processi cooperanti]]. Per ovviare a questi problemi, possiamo implementare soluzioni come fare in modo che **lo scheduling attenda il completamento o il blocco di una system call** prima di attivarsi (benché funzionante, tale soluzione può interferire con eventuali sistemi real-time, dove naturalmente ritardare lo scheduling porterebbe a un ritardo anche nella reattività del sistema).

Nel momento in cui lo scheduler ha scelto il processo da inviare alla CPU, entra in gioco il "**dispatcher**", ossia il modulo che concretamente si occupa di **dare il controllo della CPU a tale processo**. Tra le sue mansioni, dunque, troviamo quella di eseguire il [[SO1_03 - I processi#Come vengono programmati i processi nella CPU?|context switch]], di effettuare la transizione alla modalità utente, e di saltare alla posizione opportuna del programma da far eseguire alla CPU. Per sua natura, **il dispatcher viene eseguito con ogni context switch**, e avendo già stabilito che quest'ultimo rappresenta un'operazione relativamente costosa a livello di tempo e di trasferimento di dati, è cruciale che il dispatcher sia il più veloce possibile, diminuendo la cosiddetta "**dispatcher latency**".

Parlando di **tempistiche**, prima di continuare soffermiamoci su alcune **definizioni utili** per comprendere i vari intervalli di tempo a cui si deve prestare attenzione quando si tratta lo scheduling:
- l'**arrival time** ($T_{arrival}$) consiste nel momento in cui un processo entra nella coda `ready`;
- il **completion time** ($T_{completion}$) consiste nel momento in cui un processo completa la sua esecuzione;
- il **burst time** ($T_{burst}$) consiste nel tempo richiesto da un processo per l'esecuzione nella CPU;
- il **turnaround time** ($T_{turnaround}=T_{completion}-T_{arrival}$) consiste nel tempo trascorso tra l'arrivo di un processo nella coda `ready` e il completamento della sua esecuzione;
- il **waiting time** ($T_{waiting}=T_{turnaround}-T_{burst}$) consiste nel tempo dell'esecuzione di un processo non dedicato alla computazione nella CPU.



[05, slide 53 - 56 - 59 - 63 - 66 - 67 - 71 - 74 - 75 - 77 - 81]
___