https://github.com/gtolomei/operating-systems/blob/master/lectures/slides/Introduction.pdf

## Cos'è un sistema operativo?

In questo corso, come suggerisce il nome dello stesso, verrà approfondito il concetto, la struttura e l'implementazione di un "sistema operativo". Ma di cosa si tratta veramente? Nel concreto, un **sistema operativo**, spesso abbreviato in "**OS**" (Operating System), non ha una definizione univoca e ben precisa, ma in generale può essere visto come una **forma di Virtual Machine**, o "**VM**", che si inserisce come **intermediario tra software**, o **SW**, **e hardware**, o **HW**, e di conseguenza anche tra l'utilizzatore del calcolatore e l'hardware dello stesso. La presenza del sistema operativo facilita notevolmente l'interazione con la macchina su cui risiede, così come la sua programmazione, molto più approcciabile rispetto all'interfaccia diretta con l'hardware. Per visualizzare chiaramente il ruolo dell'OS, possiamo schematizzare a grandi linee l'architettura di un calcolatore generico nel modo seguente:

![[os_calcolatore.png]]

Oppure, supponendo di avere un calcolatore che permette più utenti:

![[os_calcolatore1.png]]

L'OS, all'interno di un calcolatore, svolge vari ruoli, tra cui:
- "**resource manager**", cioè si occupa della gestione delle varie risorse fisiche condivise nel calcolatore, come CPU, memoria, dispositivi di I/O, ecc. ecc., in modo da massimizzare l'efficienza;
- "**virtual machine**", in modo da virtualizzare queste risorse fisiche e fornire ad applicazioni e utenti l'illusione di disporre di infinite risorse;
- **interfaccia tra HW e SW**, fornendo una serie di servizi condivisi, e consentendo alle applicazioni e agli utenti di interagire con il sistema senza che comunichino direttamente con il HW.

Ma **da cos'è composto** effettivamente un OS? Anche qui, non c'è una risposta univoca, ma dipende dalle scelte progettuali e architetturali (le cosiddette scelte di "system design") che si prendono, e quindi dallo scopo per cui viene progettato tale OS. In questo corso, si affronteranno principalmente **sistemi "general-purpose"**, più simili a quelli che utilizziamo quotidianamente lavorando con PC o altri dispositivi del genere, ma esistono anche altri tipi di sistemi più specializzati. Ciononostante, a grandi linee è possibile riconoscere nella struttura di un OS qualsiasi **due parti principali**:
- il **kernel**, ossia il "nucleo" dell'OS, la sua unità centrale, che è sempre attivo e funzionante mentre il calcolatore è acceso;
- vari **programmi di sistema**, ossia programmi, strumenti e altre componenti che fanno parte dell'OS ma, rispetto al kernel, sono più "accessori".
___
## Struttura di un calcolatore

Per comprendere meglio il ruolo di un OS all'interno di un calcolatore, rivediamo sommariamente la **struttura interna di un calcolatore**, con una panoramica sulle sue principali componenti. Facciamo riferimento al seguente schema:

![[struttura_calcolatore.png]]

Elenchiamo le caratteristiche principali di ciascuna delle componenti principali che vediamo nello schema:
- la **CPU**, l'unità centrale del calcolatore, che esegue concretamente le operazioni computazionali (al giorno d'oggi, la gran parte delle CPU è divisa in più "core" per permettere di eseguire più processi in parallelo);
- la **memoria**, che si occupa di conservare dati e istruzioni necessari per qualsiasi operazione svolta dalla CPU;
- i **dispositivi di I/O** (mouse, tastiera, stampante, monitor, ecc. ecc.), ognuno associato a uno specifico "**device controller**", che si occupano di gestire l'input e l'output del calcolatore;
- un **system bus**, che in poche parole si occupa della comunicazione tra CPU, memoria e i vari dispositivi.

A livello di base, il modello architetturale di un calcolatore rimane sempre lo stesso, indipendentemente dallo scopo finale o dall'implementazione specifica dello stesso. Questo modello generale è stato ideato da **John von Neumann**, e può essere riassunto nel seguente schema:

![[struttura_calcolatore1.png]]

[Introduction.pdf, slide 44/68: ciclo di istruzione, pipeline, linguaggio macchina]

All'interno di una CPU, i dati su cui opera sono conservati in "**registri**", delle piccole unità di memoria interne alla stessa, la cui grandezza tipicamente coincide con la grandezza di una word. In un'architettura come **`x86`**, ci sono vari **registri "general-purpose"**, come `eax`, `ebx` e `ecx`, e altri con uno **scopo specifico**, come:
- `esp`, che contiene lo "stack pointer", ossia l'indirizzo corrispondente alla cima dello stack;
- `ebp`, che contiene lo "stack base pointer";
- `eip`, che contiene lo "instruction pointer", ossia il Program Counter, o PC.

In base al numero di CPU incluse in un calcolatore, questi ultimi possono essere divisi in due categorie:
- sistemi **a singolo processore**, che contengono una sola CPU principale che si occupa dell'esecuzione dei programmi e altri processori secondari con compiti più specifici (controller del disco, GPU, ecc. ecc.);
- sistemi **multi-processore**, che contengono più CPU per aumentare il throughput del calcolatore e consentono una maggiore resilienza di fronte a errori o malfunzionamenti.

Per quanto riguarda la **memoria**, nei calcolatori moderni si implementa la cosiddetta "**[[AE_06 - La memoria#Gerarchia delle memorie|gerarchia delle memorie]]**": in un calcolatore, non è presente una sola memoria, ma piuttosto vari **livelli di memoria**, che concettualmente possono essere raccolti 



![[Pasted image 20250923143140.png]]

A livello astratto, la memoria principale può essere rappresentata come una sequenza di celle (blocchi), ciascuna organizzata. Ogni cella è organizzata in byte, ossia gruppi da 8 bit, o in multipli di questi gruppi (ad esempio, 4 byte o 32 bit). Ogni cella ha un proprio indirizzo, e la unità di memoria più piccola indirizzabile è un byte.

[slide 91]

![[Pasted image 20250923143848.png]]

Ogni dispositivo di I/O è principalmente composto da due parti:
- il dispositivo fisico;
- il controller, ossia un chip o un insieme di chip che controlla il funzionamento del dispositivo.

I dispositivi di I/O possono essere categorizzati in base alla loro funzione: ce ne sono relativi alla memoria, alla comunicazione, all'interfaccia utente, ecc. ecc. L'OS comunica con il controller di uno di questi dispositivi, e dunque con il dispositivo stesso, tramite un cosiddetto "device driver".

![[Pasted image 20250923144110.png]]

Ogni controller ha un numero di registri dedicati che permettono di comunicare con il dispositivo, tra cui:
- registri di stato, che forniscono informazioni sullo stato attuale del dispositivo di I/O alla CPU;
- registri di configurazione e di controllo, utilizzati dalla CPU per configurare e controllare il dispositivo;
- registri di dati, utilizzati per leggere o inviare dati.

[slide 105/111]
[slide 112/117]
[slide 118/134]