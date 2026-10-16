Per poter affrontare nel dettaglio la teoria della computazione, partiamo dal modellare ciò su cui tale computazione avviene, ossia un computer. Naturalmente, analizzare teoricamente un computer effettivo risulterebbe fin troppo complesso, dunque in questi contesti si preferisce utilizzare dei cosiddetti "**modelli di computazione**". Un modello di computazione rappresenta, sostanzialmente, un'astrazione di un calcolatore, che può essere accurata in alcuni aspetti e meno in altri; per questo motivo, durante questo corso si vedranno diversi modelli di computazione, a seconda delle caratteristiche su cui ci si vorrà concentrare.

Il primo modello di computazione che andremo ad analizzare, il più semplice, è il cosiddetto "**automa finito**", chiamato anche "**macchina a stati finiti**".

## Cos'è un automa finito?

Un **automa finito** può essere utilizzato per **modellare un semplice computer** con una **quantità estremamente limitata di memoria**. 

Per comprendere al meglio questo concetto, vediamo un **esempio concreto** prima di arrivare alla definizione formale: supponiamo, ad esempio, di avere a che fare con il **sistema di controllo di una porta automatica di sola entrata**. Il suo compito è di aprirsi quando rileva una persona che sta per attraversarne la soglia, e di rimanere aperta abbastanza da permettere a tale persona di arrivare dall'altra parte. Per svolgere queste due mansioni, saranno necessari due sensori, per cui possiamo schematizzare questo esempio nel modo seguente:

![[automa_esempio.png]]

Ora, naturalmente il sistema che stiamo considerando può trovarsi solamente in uno di **due stati**: **`OPEN`** quando la porta è aperta, e **`CLOSED`** quando la porta è chiusa. Invece, per quanto riguarda i possibili **input** del sistema, ossia ciò che viene rilevato dai due sensori, essi sono 4: **`FRONT`** quando è rilevata una persona dal sensore anteriore, **`REAR`** quando è rilevata dal sensore posteriore, **`BOTH`** quando è rilevata da entrambi, e **`NEITHER`** quando nessuno dei due sensori rileva nulla. Il sistema di controllo **passa da uno stato all'altro in base all'input che riceve e allo stato in cui si trova quando lo riceve**: ad esempio, se si trova nello stato `CLOSED` e riceve input `NEITHER` o `REAR` rimane in tale stato; invece, se riceve l'input `FRONT`, la porta si apre e il sistema passa nello stato `OPEN`; se, poi, nello stato `OPEN` si riceve l'input `NEITHER`, la porta si chiuderà e si passerà allo stato `CLOSED`; e così via. Queste transizioni possono essere riassunte in quella che chiamiamo "**tabella delle transizioni di stato**", che riassume e schematizza tutti i possibili comportamenti del sistema in base a stato e input. Ad esempio, per l'esempio appena visto, una possibile tabella delle transizioni di stato è la seguente:

![[automa_esempio1.png]]

Ancora, tale sistema può essere formalizzato in modo più chiaro e immediato con un "**diagramma di stato**", come il seguente:

![[automa_esempio2.png]]

In base alle premesse appena fatte, se ad esempio il sistema ricevesse la sequenza di input `FRONT`-`REAR`-`NEITHER`-`FRONT`-`BOTH`-`NEITHER`-`REAR`-`NEITHER`, esso passerebbe attraverso la sequenza di stati `CLOSED`-`OPEN`-`OPEN`-`CLOSED`-`OPEN`-`OPEN`-`CLOSED`-`CLOSED`-`CLOSED`.

Ora, a partire da questo esempio, vediamo di generalizzare e di arrivare eventualmente a una definizione di automa finito. Prendiamo un altro automa generico, chiamato $M_{1}$ e definito dal seguente diagramma di stato:

![[automa_esempio3.png]]

I 3 nodi del diagramma sono detti "**stati**", e in questo esempio sono etichettati come $q_{1}$, $q_{2}$ e $q_{3}$. Tra questi, possiamo identificare $q_{1}$ come lo "**stato iniziale**" dell'automa, dato che presenta un arco entrante in esso ma non uscente da altri stati; al tempo stesso, possiamo identificare $q_{2}$ come lo "**stato accettante**", o "**stato finale**", dell'automa, dato che presenta un contorno doppio (uno stato accettante può apparire anche come un cerchio con l'interno colorato). Formalmente, infine, gli archi tra i vari stati si dicono "**transizioni**", e i valori annessi a ciascuna transizione sono i **valori di input** che provocano tale transizione.

In generale, **un automa finito prende in input una sequenza di simboli**, simboli che devono far parte di un **alfabeto $\Sigma$** (in questo esempio, l'alfabeto è $\Sigma=\{0,\,1\}$), e tali simboli vengono **letti uno alla volta, da sinistra verso destra**. Sono proprio tali simboli che, come nell'esempio della porta automatica, determinano le transizioni di stato dell'automa considerato. Ad esempio, se l'automa $M_{1}$ riceve in input la sequenza `1101`, avvengono le seguenti transizioni:
1. l'automa parte dallo stato iniziale $q_{1}$;
2. l'automa legge `1`, dunque effettua la transizione allo stato $q_{2}$;
3. l'automa legge `1`, dunque rimane nello stato $q_{2}$;
4. l'automa legge `0`, dunque effettua la transizione allo stato $q_{3}$;
5. l'automa legge `1`, dunque effettua la transizione allo stato $q_{2}$.

Ora, **tipicamente un automa produce un output**; in questo esempio, per semplicità, supponiamo che gli output possibili siano solamente due, `True` e `False`. L'output restituito dall'automa **dipende esclusivamente dall'ultimo simbolo letto in input**: se l'ultimo simbolo di input porta l'automa a trovarsi in uno stato finale, allora l'automa restituirà `True`, altrimenti restituirà `False`. Elaborando, ad esempio, sempre l'input `1101`, l'automa $M_{1}$ restituirà `True`, dato che al termine dell'elaborazione si troverà nello stato $q_{2}$. Un'analisi più approfondita dell'automa $M_{1}$ permette di mostrare che esso accetterà qualsiasi sequenza che termina con $1$, o anche qualsiasi sequenza che termina con un numero pari di $0$ dopo l'ultimo $1$.

Forniamo, a questo punto, una **definizione formale di automa finito**:

> Un **automa finito**, o "**DFA**" (Deterministic Finite-State Automaton), è una tupla $(Q,\,\Sigma,\,\delta,\,q_{0},\,F)$, dove:
> - **$Q$** è un insieme finito chiamato "**insieme degli stati**";
> - **$\Sigma$** è un insieme finito chiamato "**alfabeto**";
> - **$\delta:Q\times\Sigma\to Q$** è una "**funzione di transizione**";
> - **$q_{0}\in Q$** è lo **stato iniziale**;
> - **$F\subseteq Q$** è l'**insieme degli stati accettanti**.

Da questa definizione formale, possiamo anche capire meglio il comportamento di un automa finito in eventuali casi limite: ad esempio, porre $F=\emptyset$ è tranquillamente consentito, il che implica che **un automa finito può non avere stati accettanti**. 

Chiariamo, a questo punto, anche il concetto di "funzione di transizione", non analizzato concretamente finora: la funzione $\delta$ associa a una tupla costituita da uno stato e un simbolo un nuovo stato, dunque in parole povere **definisce le transizioni dell'automa finito considerato**, specificando esattamente uno stato successivo per ogni possibile combinazione di uno stato e un simbolo di input.

##### Linguaggi

Indicando con $\Sigma^{*}$ l'insieme di tutte le possibili sequenze di lunghezza $k\in\mathbb{N}$ di caratteri contenuti nell'alfabeto $\Sigma$, possiamo dire che **a ogni automa finito corrisponde un "linguaggio"**. Ma cos'è un linguaggio? Informalmente, possiamo vedere un linguaggio come un qualsiasi sottoinsieme $L$ dell'insieme $\Sigma^*$ (dunque, $L\subseteq \Sigma^*$); in particolare, indichiamo con $L(M)$ il **linguaggio riconosciuto dall'automa $M$**, che consiste nell'**insieme di tutte le sequenze di simboli accettate dall'automa $M$ considerato**. Indicando con $A$ tale insieme, scriviamo che:
$$L(M)=A$$
In questo contesto, si dice che "**$M$ riconosce $A$**", oppure che "**$M$ accetta $A$**". Se vogliamo fornire una definizione più rigorosa del linguaggio riconosciuto da un automa $M$, si dovrà definire la cosiddetta "**funzione di transizione estesa**", una variante $\delta^*$ della funzione di transizione $\delta$, che non cattura più un singolo "passo di computazione" ma più passi tutti assieme, senza particolare attenzione verso i passi intermedi. La firma della funzione è $\delta^*:Q\times \Sigma^*\to Q$, e può essere definita ricorsivamente nel modo seguente:
$$\begin{cases} \delta^*(q,\,\epsilon)=\delta(q,\,\epsilon)\\ \delta^*(q,\,ax)=\delta^*(\delta(q,\,a),\,x) \end{cases}$$
dove $\epsilon$ rappresenta la stringa vuota, $a\in \Sigma$ un singolo simbolo e $x\in \Sigma^*$ una stringa di simboli. Data tale definizione, il linguaggio riconosciuto da un DFA $M$, ossia $L(M)$, può essere definito come segue:
$$L(M)=\{x\in\Sigma^*\,|\,\delta^*(q_{0},\,x)\in F\}$$
Nel caso in cui un determinato automa non accetti alcuna sequenza in input, esso riconoscerà comunque un linguaggio $L$, semplicemente con $L(M)=\emptyset$.
___
##### Esempi di automi finiti

Riprendiamo l'automa visto in precedenza, $M_{1}$, che ricordiamo essere definito da tale diagramma di stato:

![[automa_esempio5.png]]

Cerchiamo di formalizzare $M_{1}$ sulla base della definizione appena data. Costruiamo dunque la tupla $(Q,\,\Sigma,\,\delta,\,q_{0},\,F)$:
- $Q$ è l'insieme degli stati di $M_{1}$, dunque sarà $\{q_{1},\,q_{2},\,q_{3}\}$;
- $\Sigma$ è l'alfabeto della sequenza presa in input, dunque sarà $\{0,\,1\}$;
- $\delta$ è una funzione definibile, in questo esempio, dalla seguente tabella:

|         | 0       | 1       |
| ------- | ------- | ------- |
| $q_{1}$ | $q_{1}$ | $q_{2}$ |
| $q_{2}$ | $q_{3}$ | $q_{2}$ |
| $q_{3}$ | $q_{2}$ | $q_{2}$ |

- lo stato iniziale di $M_{1}$ è $q_{1}$;
- l'insieme $F$ è costituito da un solo stato, ossia $\{q_{2}\}$.

Per quanto riguarda il linguaggio riconosciuto da $M_{1}$, esso è:
$$L(M_{1})=\{w\,|\,w\text{ contiene almeno un } 1\text{ e un numero pari di } 0\text{ segue l'ultimo }1\}$$

Andiamo avanti, e vediamo un nuovo esempio $M_{2}$ di automa finito, identificato dal seguente diagramma:

![[automa_esempio5.png]]

In questo caso, abbiamo:
- $Q=\{q_{1},\,q_{2}\}$;
- $\Sigma=\{0,\,1\}$;
- $\delta$ è definita dalla seguente tabella:

|         | 0       | 1       |
| ------- | ------- | ------- |
| $q_{1}$ | $q_{1}$ | $q_{2}$ |
| $q_{2}$ | $q_{1}$ | $q_{2}$ |

- lo stato iniziale è $q_{1}$;
- $F=\{q_{2}\}$.

In questo caso, provando vari input, è facile convincersi che $M_{2}$ accetta tutte le sequenze di simboli che terminano con un $1$, il che vuol dire che:
$$L(M_{2})=\{w\,|\,w\text{ termina con un }1\}$$

Passiamo a un altro esempio, con l'automa finito $M_{3}$:

![[automa_esempio6.png]]

Notiamo subito, ad occhio, che $M_{3}$ è quasi identico a $M_{2}$, con la sola eccezione che $F=\{q_{1}\}$, dunque troviamo un caso particolare in cui lo stato iniziale è anche lo stato finale dell'automa. Data questa particolarità, possiamo subito affermare con certezza che $M_{3}$ accetta la stringa vuota $\epsilon$. Oltre a ciò, si può osservare che $M_{3}$ accetta tutte le sequenze che terminano con uno $0$, dunque abbiamo che:
$$L(M_{3})=\{w\,|\,w\text{ è la stringa vuota }\epsilon\text{ oppure termina con uno 0}\}$$

Vediamo un ultimo esempio, con l'automa $M_{4}$:

![[automa_esempio7.png]]

In questo caso, si ha $Q=\{q_{0},\,q_{1},\,q_{2}\}$ e $\Sigma=\{(RESET),\,0,\,1,\,2\}$, con $q_{0}$ come stato iniziale e stato accettante. Seppur possa sembrare particolarmente complessa rispetto agli esempi visti finora, si tratta di un automa che svolge una mansione molto semplice: conserva al suo interno la somma parziale dei simboli che legge in input, modulo $3$ (se $M_{4}$ si trova in $q_{0}$ tale somma vale $0$, se si trova in $q_{1}$ tale somma vale $1$, e così via), e ogni volta che riceve il simbolo $(RESET)$ riporta il conto a $0$. Con questo chiarimento, diventa palese che $M_{4}$ accetta tutte le sequenze che risultano in una somma pari a $0\text{ mod }3$, ossia in una somma che è multipla di $3$.
___
##### Definizione formale di computazione

Finora, ci siamo occupati di definire, informalmente e poi formalmente, gli automi finiti, ma non abbiamo veramente fatto lo stesso per la **computazione**, la mansione effettivamente svolta da un automa. 

Prima di fare ciò, introduciamo un concetto importante: la "**configurazione**". Formalmente, essa è una **coppia in $Q\times \Sigma^*$**, dunque una tupla $(q,\,x)$ contenente uno stato e una stringa di simboli; in parole povere, essa viene utilizzata per fornire una **"fotografia" dell'automa in un determinato momento**, dato che $q$ sarà lo stato corrente dell'automa, mentre $x$ sarà la porzione della sequenza di simboli di input che deve ancora essere letta e processata dall'automa. In particolare, la configurazione $(q_{0},\,w)$, dove $q_{0}$ è lo stato iniziale dell'automa e $w$ è l'intera sequenza di input, viene detta "**configurazione iniziale**". Ora, definire la configurazione ci permette di fare passi avanti verso la formalizzazione della computazione, dato che avere a disposizione le varie fotografie dei passi di computazione, insieme alla funzione di transizione $\delta$, ci permette di **mettere in relazione le varie configurazioni**: se l'automa $M$ si trova nella configurazione $(q,\,ax)$, e $\delta$ impone che leggere $a$ nello stato $q$ porti l'automa nello stato $p$, allora si sa già che la prossima configurazione di $M$ sarà proprio $(p,\,x)$. Formalmente, questo passaggio viene indicato con il simbolo di "**produzione**", ossia:
$$(q,\,ax)\,\vdash_{M}\,(p,\,x)$$
relazione che, per quanto detto finora, vale se e solo se $\delta(q,\,a)=p$. Ora, così come abbiamo esteso la funzione di transizione $\delta$ in $\delta^*$, è ugualmente possibile estendere la relazione $\vdash_{M}$ in $\vdash_{M}^*$. Anche in questo caso, converrà farlo in modo ricorsivo, dunque:
$$\begin{cases} (q,\,x)\,\vdash_{M}^*\,(q,\,x) \\ \text{se }(q,\,aby)\vdash_{M}(p,\,by)\text{ e }(p,\,by)\vdash_{M}(r,\,y),\text{ allora }(q,\,aby)\vdash_{M}^*(r,\,y) \end{cases}$$
Secondo questa definizione formale, **la relazione $\vdash_{M}^*$ è riflessiva e transitiva**.

Di seguito, dunque, forniamo una **definizione formale del concetto di "computazione"**:

> Sia $M=(Q,\,\Sigma,\,\delta,\,q_{0},\,F)$ un automa finito, e sia $w$ una stringa dove ogni elemento è un simbolo dell'alfabeto $\Sigma$. Si dice che "**$M$ accetta $w$**" se e solo se vale la relazione:
> $$(q_{0},\,w)\,\vdash_{M}^*\,(q,\,\epsilon)$$
> con $q\in F$, o alternativamente se $\delta^*(q_{0},\,w)\in F$.

Non volendo utilizzare la relazione $\vdash_{M}^*$, è possibile fornire anche una **definizione alternativa**:

> Sia $M=(Q,\,\Sigma,\,\delta,\,q_{0},\,F)$ un automa finito, e sia $w=w_{1}w_{2}\dots w_{n}$ una stringa dove ogni elemento $w_{i}$ è un simbolo dell'alfabeto $\Sigma$. Si dice che "**$M$ accetta $w$**" se esiste una sequenza di stati $r_{0},\,r_{1},\,\dots,\,r_{n}$ in $Q$ tale per cui:
> 1. $r_{0}=q_{0}$;
> 2. $\delta(r_{i},\,w_{i\,+\,1})=r_{i\,+\,1}$ per $i=0,\,1,\,\dots,\,n-1$;
> 3. $r_{n}\in F$.

In altre parole, la prima condizione impone che l'automa parta dallo stato iniziale $q_{0}$, la seconda che l'automa passi da uno stato all'altro seguendo seguendo la sua funzione di transizione $\delta$, e la terza che lo stato di arrivo definito dalla sequenza presa in input sia uno stato accettante.

Forniamo, a questo punto, anche un'altra definizione, quella di "**linguaggio regolare**".

> Un linguaggio è detto "**linguaggio regolare**" se esiste un automa finito che lo riconosce. Formalmente, indichiamo l'insieme dei linguaggi regolari con $REG$, dove:
> $$REG=\{L\subseteq \Sigma^*\,|\,\exists\,M\text{ tale che }L(M)=L\}$$

In questo contesto, è chiaro che i vari linguaggi visti negli esempi del [[ACC_02 - Automi#Esempi di automi finiti|paragrafo precedente]], ossia:
$$\begin{align} &L(M_{1})=\{w\,|\,w\text{ contiene almeno un } 1\text{ e un numero pari di } 0\text{ segue l'ultimo }1\} \\&L(M_{2})=\{w\,|\,w\text{ termina con un }1\} \\&L(M_{3})=\{w\,|\,w\text{ è la stringa vuota }\epsilon\text{ oppure termina con uno 0}\} \\&L(M_{4})=\{w\,|\,\text{la somma dei simboli in }w\text{ è }0\text{ mod }3,\text{ con }(RESET)\text{ che riporta la somma a }0\} \end{align}$$
sono tutti linguaggi regolari, dato che tutti sono riconosciuti da un automa finito. Vedremo, in seguito, che **non tutti i linguaggi sono regolari**, e ne esistono molti che non possono essere riconosciuti da un automa.
___
##### Progettare un automa finito

Ora che siamo perfettamente coscienti di cosa sia un automa finito, delle componenti che lo caratterizzano, e del concetto di linguaggio, dovremmo avere tutti gli strumenti per essere in grado di **progettare un automa finito che riconosca un determinato linguaggio**. Per fare ciò, nonostante non ci siano formule immediate o metodi infallibili, è comunque possibile seguire alcune linee guida e consigli, che sicuramente facilitano molto la progettazione.

Innanzitutto, può essere utile approcciarsi al problema **immedesimandosi nell'automa da progettare**: in altre parole, conviene immaginare di dover analizzare l'input in prima persona, in modo da capire meglio se la stringa di simboli vista finora appartiene al linguaggio che si vuole riconoscere. Per prendere queste decisioni, occorre capire **cosa è utile ricordare della stringa letta**: sarà, infatti, pressoché impossibile ricordarla tutta (data la finitezza della memoria di un automa finito), e ciononostante risulterebbe in soluzioni incredibilmente complesse, inefficienti e poco eleganti. Le informazioni necessarie da ricordare dipendono dal linguaggio, dunque sarà nostro compito reinterpretare la definizione del linguaggio fornito, in modo da identificarne le caratteristiche fondamentali e osservarle nell'automa.

Vediamo un esempio, in modo da concretizzare quanto detto finora. Supponiamo di avere l'alfabeto $\Sigma=\{0,\,1\}$, e il linguaggio:
$$L=\{w\,|\,w\text{ contiene un numero dispari di 1}\}$$
e di voler costruire un automa finito $E_{1}$ che riconosca il linguaggio $L$. Naturalmente, supponendo di ricevere in input, un simbolo per volta, una qualsiasi sequenza di $0$ e $1$, non sarà necessario (né possibile) ricordare l'intera sequenza per verificarne la validità, ma basterà tenere traccia dell'unica informazione fondamentale: la parità o disparità del numero di $1$. Per memorizzare questa informazione, utilizziamo un meccanismo molto semplice: se viene letto un $1$, la risposta viene cambiata (ovviamente, se finora abbiamo letto un numero pari di $1$ e ne leggiamo un altro, tale numero diventerà dispari, e viceversa); se viene letto uno $0$, la risposta rimane invariata.

Siamo arrivati, dunque, a un ragionamento semplice e diretto che ci permette di memorizzare l'informazione richiesta. Ma come possiamo applicare questa conoscenza per progettare $E_{1}$? Per fare ciò, bisogna **rappresentare le informazioni memorizzate come una lista finita di possibilità**, che diventeranno l'insieme finito degli stati dell'automa. Nel nostro esempio, le possibilità sono due, ossia:
- la stringa letta finora ha un numero pari di $1$;
- la stringa letta finora ha un numero dispari di $1$.

Dunque, assegnando uno stato per ciascuna di queste possibilità (ad esempio, $q_{\text{even}}$ per la prima e $q_{\text{odd}}$ per la seconda), cominciamo ad abbozzare il nostro automa $E_{1}$:

![[automa_esempio8.png]]

A questo punto, definiamo le transizioni che collegano questi stati, e fare ciò sarà facile dato che abbiamo già definito, in precedenza, il ragionamento da seguire per memorizzare l'informazione desiderata: a prescindere dallo stato in cui ci troviamo, ricevere in input un $1$ porterà l'automa a cambiare stato, mentre ricevere uno $0$ lascerà lo stato invariato. Dunque:

![[automa_esempio9.png]]

Ora rimangono da definire solo lo stato iniziale e l'insieme degli stati accettanti. Lo stato iniziale corrisponderà alla possibilità associata all'aver letto la stringa vuota $\epsilon$, dunque nel nostro esempio con l'aver letto $0$ volte un $1$, e dato che consideriamo $0$ come un numero pari lo stato iniziale sarà $q_{\text{even}}$. Per quanto riguarda gli stati accettanti, per la definizione del linguaggio l'unico stato accettante dovrà necessariamente essere $q_{\text{odd}}$, per cui l'automa $E_{1}$ assume la seguente forma:

![[automa_esempio10.png]]

Vediamo un altro esempio, leggermente più complesso. Supponiamo di avere nuovamente lo stesso alfabeto $\Sigma=\{0,\,1\}$, e di voler progettare un automa finito $E_{2}$ che riconosca il linguaggio:
$$L=\{w\,|\,w\text{ contiene al suo interno la sotto-stringa }001\}$$
Il nostro obiettivo, nel leggere la stringa un simbolo alla volta, sarà dunque memorizzare se, finora, abbiamo letto la sotto-stringa di simboli $001$, e per fare ciò sarà utile memorizzare anche le "possibilità intermedie" che devono verificarsi prima del nostro obiettivo, ossia:
- la lettura di uno $0$;
- la lettura di $00$;
- la lettura di $001$.

Il ragionamento, in poche parole, è questo: inizialmente, si ignorano tutti gli $1$ che vengono letti nell'input; non appena si legge uno $0$, memorizziamo tale evento e leggiamo il simbolo successivo; se leggiamo un altro $0$, memorizziamo di aver letto $00$ e leggiamo il simbolo successivo, mentre se leggiamo un $1$ torniamo allo stato iniziale; infine, se leggiamo un $1$ dopo due $0$, sappiamo che la stringa contiene la sotto-stringa $001$, dunque in seguito a ciò qualsiasi input non cambierà questa certezza. La lista delle possibilità può essere tradotta nei seguenti 4 stati:
- non si è ancora visto lo $0$ iniziale della sotto-stringa;
- si è visto il primo $0$ della sotto-stringa;
- si è visto il secondo $0$ della sotto-stringa;
- si è visto l'$1$ finale della sotto-stringa.

Con le considerazioni fatte, possiamo costruire l'automa finito $E_{2}$:

![[automa_esempio11.png]]
___
## Operazioni regolari

Una volta visti nel dettaglio gli [[ACC_02 - Automi#Cos'è un automa finito?|automi finiti]], e approfondito il concetto di broccolo, [[ACC_02 - Automi#Linguaggi|linguaggio]] e di [[ACC_02 - Automi#Definizione formale di computazione|linguaggio regolare]], studiamo le loro **proprietà**. Nella teoria della computazione, i linguaggi sono gli "oggetti di base", e abbiamo a disposizione vari strumenti per gestirli e modificarli. 

##### Esempi di operazioni regolari e dimostrazione della chiusura rispetto all'unione

Definiamo, per prima cosa, tre operazioni chiamate "**operazioni regolari**", e usiamole per studiare le proprietà dei linguaggi regolari.

> Siano $A$ e $B$ due linguaggi, possiamo definire le seguenti **operazioni regolari**:
> - **unione**, indicata dal simbolo $\cup$ e definita formalmente come $A\cup B=\{x\,|\,x\in A\,\lor\,x\in B\}$;
> - **intersezione**, indicata dal simbolo $\cap$ e definita formalmente come $A\cap B=\{x\,|\,x\in A\,\land\,x\in B\}$;
> - **complemento**, indicata dal simbolo $\overline{}$ e definita formalmente come $\overline{A}=\{x\,|\,x\not\in A\}$;
> - **concatenazione**, indicata dal simbolo $\circ$ e definita formalmente come $A\circ B=\{xy\,|\,x\in A\,\land\,x\in B\}$;
> - **potenza**, definita formalmente in modo ricorsivo come
>$$\begin{cases} L^0=\{\epsilon\}\\L^{n+1}=L^n \circ L\,\,\,\,\,\,\,\,\,\,\text{per }n\ge 0 \end{cases}$$
> - **star**, indicata dal simbolo $^*$ e definita formalmente come $A^*=\{x_{1}x_{2}\dots x_{k}\,|\,k\ge 0,\,\text{ogni }x_{i}\in A\}$.

In altre parole, presi due linguaggi $A$ e $B$: l'operazione di unione $A\cup B$ definisce un nuovo linguaggio che include **tutte le stringhe contenute almeno in uno dei due linguaggi operandi**; l'operazione di intersezione definisce un nuovo linguaggio che include **tutte le stringhe contenute in entrambi i linguaggi operandi**; l'operazione di complemento definisce un nuovo linguaggio che include **tutte le stringhe non contenute nel linguaggio operando**; l'operazione di concatenazione definisce un nuovo linguaggio che include **le stringhe generate anteponendo una stringa di $A$ a una stringa di $B$ in tutti i modi possibili**; l'operazione di potenza è un'operazione unaria, dato che opera su un singolo linguaggio, e definisce un nuovo linguaggio che include **le stringhe generate concatenando il linguaggio con sé stesso $n$ volte**; l'operazione star è un'operazione unaria, e definisce un nuovo linguaggio che include **tutte le possibili concatenazioni di stringhe di $A$**. In particolare, l'operazione star può anche essere vista come un'unione di potenze, infatti:
$$L^*\,=\,\bigcup_{n\,\ge\,0}L^n\,=\,\{\epsilon\}\cup L\cup L^2\cup \,\dots$$
Sarà utile, in questo contesto, definire anche il concetto di "**chiusura rispetto a un'operazione**".

> Una classe di oggetti si dice **"chiusa" rispetto a un'operazione** se l'applicazione di tale operazione agli elementi della classe restituisce sempre un oggetto appartenente alla stessa classe.

Data questa definizione, vogliamo dimostrare che **i linguaggi regolari sono chiusi rispetto a tutte e sei le operazioni regolari**.

Iniziamo con l'operazione di **unione**. Vogliamo dimostrare che, **avendo due linguaggi regolari $A_{1}$ e $A_{2}$, anche l'unione $A_{1}\cup A_{2}$ definisce un linguaggio regolare**. L'idea di fondo è questa: poiché $A_{1}$ e $A_{2}$ sono entrambi regolari, sappiamo che esiste un automa finito $M_{1}$ che riconosce $A_{1}$, e un altro automa $M_{2}$ che riconosce $A_{2}$, dunque vogliamo costruire, a partire da $M_{1}$ e $M_{2}$, un terzo automa finito $M$ che riconosca l'unione $A_{1}\cup A_{2}$; in altre parole, l'automa $M$ dovrà accettare qualsiasi input che verrebbe accettato da $M_{1}$ o da $M_{2}$. Un possibile approccio è fare in modo che $M$ simuli sia $M_{1}$ che $M_{2}$ sull'input che riceve, e accettare quest'ultimo se almeno una tra queste due simulazioni lo accettano. Queste simulazioni, però, devono avvenire contemporaneamente, dato che l'input non può essere letto per una di esse, riavvolto e poi riletto per l'altra. Dunque, immedesimandoci in $M$, le informazioni che dovremo memorizzare relativamente alle due simulazioni sono semplicemente lo stato in cui $M_{1}$ e $M_{2}$ si troverebbero se avessero letto l'input fino a quel punto: in altre parole, quella che deve essere memorizzata è sostanzialmente una coppia di stati. Supponendo che $M_{1}$ abbia $k_{1}$ stati, e che $M_{2}$ abbia $k_{2}$ stati, il numero delle possibili coppie di stati, ossia il numero di stati effettivi di $M$, sarà pari a $k_{1}\times k_{2}$. Per quanto riguarda gli stati accettanti di $M$, essi saranno tutti quelli relativi a una coppia di stati tale per cui $M_{1}$ o $M_{2}$ si trova in uno stato accettante. 

Cerchiamo quindi di formalizzare quanto detto finora. Supponiamo, dati i due linguaggi $A_{1}$ e $A_{2}$, che $M_{1}=(Q_{1},\,\Sigma,\,\delta_{1},\,q_{1},\,F_{1})$ riconosca $A_{1}$ e che $M_{2}=(Q_{2},\,\Sigma,\,\delta_{2},\,q_{2},\,F_{2})$ riconosca $A_{2}$, e costruiamo l'automa $M=(Q,\,\Sigma,\,\delta,\,q_{0},\,F)$ che riconosca l'unione $A_{1}\cup A_{2}$. In base a quanto detto:
- $Q=\{(r_{1},\,r_{2})\,|\,r_{1}\in Q_{1}\,\land\,r_{2}\in Q_{2}\}$, che è del resto un altro modo per denotare il prodotto cartesiano degli insiemi $Q_{1}$ e $Q_{2}$ (indicabile anche come $Q_{1}\times Q_{2}$), ossia l'insieme di tutte le coppie possibili di stati, dove il primo appartiene all'automa $M_{1}$ e il secondo a $M_{2}$;
- $\Sigma$ sarà lo stesso alfabeto di $M_{1}$ e $M_{2}$, condizione che assumiamo per semplicità ma non necessaria per la dimostrazione (anche se i due automi operandi hanno due alfabeti $\Sigma_{1}$ e $\Sigma_{2}$ diversi, valgono pressoché le stesse considerazioni, ponendo però $\Sigma=\Sigma_{1}\cup \Sigma_{2}$);
- $\delta$ è definita come una funzione ricevente, in input, uno stato di $M$ (ossia una coppia $(r_{1},\,r_{2})$ di stati di $M_{1}$ e $M_{2}$) e un simbolo, e restituente lo stato successivo di $M$, dunque
$$\delta((r_{1},\,r_{2}),\,a)=(\delta_{1}(r_{1},\,a),\,\delta_{2}(r_{2},\,a))$$
- $q_{0}$ sarà lo stato coincidente con la coppia $(q_{1},\,q_{2})$;
- $F$ consiste nell'insieme delle coppie $(r_{1},\,r_{2})$ in cui o $r_{1}$ o $r_{2}$ è uno stato accettante, dunque
$$F=\{(r_{1},\,r_{2})\,|\,r_{1}\in F_{1}\,\lor\,r_{2}\in F_{2}\}\,\,\,\,\,\,\,\,\,\,\text{oppure}\,\,\,\,\,\,\,\,\,\,F=(F_{1}\times Q_{2})\cup(F_{2}\times Q_{1})$$

Siamo riusciti, così, a costruire un automa $M$ che riconosce l'unione dei due linguaggi regolari generici $A_{1}$ e $A_{2}$ in modo relativamente semplice. La correttezza di questa costruzione risulta evidente dal ragionamento informale esposto in precedenza, ma in situazioni più complesse potrebbero essere necessarie ulteriori discussioni o prove formali (tali prove, tendenzialmente, vengono esposte procedendo per **induzione**).

Altre dimostrazioni, ad esempio quelle relative a concatenazione o a intersezione, purtroppo non sono ugualmente immediate, e per effettuarle sarà necessario introdurre un nuovo concetto fondamentale: il "**[[ACC_02 - Automi#Non-determinismo|non-determinismo]]**".
___
## Non-determinismo

Il **non-determinismo** è un concetto che ha avuto un forte impatto sulla teoria della computazione, e che per certi versi la rivoluziona. Finora, nel parlare di [[ACC_02 - Automi#Cos'è un automa finito?|DFA]], ossia di automi a stati finiti deterministici, ogni passo della computazione seguiva in modo univoco dal passo precedente, dunque quando l'automa si trovava in un determinato stato e leggeva un simbolo in input, lo stato successivo era determinato in modo certo e univoco. È proprio qui che sta il "**determinismo**", dei DFA. La differenza nel non-determinismo sta proprio in come l'automa passa da uno stato all'altro: in un **NFA**, o **Non-Deterministic Finite-State Automaton**, a partire da un determinato stato e ricevendo un determinato input **si può transitare "non-deterministicamente" in un insieme di stati**.

In generale, **il non-determinismo rappresenta una generalizzazione del determinismo**, il che implica che **ogni DFA è anche un NFA**. Ciò detto, tipicamente un NFA presenta alcune caratteristiche peculiari, che non troviamo nei DFA. 

##### Definizione di NFA e differenze con i DFA

Per capire meglio di cosa si sta parlando, vediamo un esempio di NFA:

![[nfa_esempio.png]]

La prima differenza evidente sta nelle transizioni: in particolare, mentre in un DFA c'è sempre esattamente un arco di transizione uscente da ogni stato per ogni simbolo nell'alfabeto, **in un NFA uno stato può avere $0$, $1$ o più archi uscenti per ogni simbolo dell'alfabeto** (nel nostro caso, ciò avviene ad esempio in $q_{1}$, che presenta 2 archi uscenti per il simbolo $1$). Un'altra peculiarità sta proprio nei simboli associati a tali archi di transizione: mentre in un DFA non è prevista una transizione in corrispondenza della stringa vuota $\epsilon$ (se un DFA non riceve input, rimane nello stato corrente), **un NFA può avere archi di transizione relativi sia a simboli dell'alfabeto che a $\epsilon$** (d'ora in poi, chiameremo tali archi "**$\epsilon$-archi**"). Fatte queste considerazioni, possiamo in realtà già fornire una **definizione formale di NFA**:

>  Un **automa finito non-deterministico**, o "**NFA**" (Non-Deterministic Finite-State Automaton), è una tupla $(Q,\,\Sigma,\,\delta,\,q_{0},\,F)$, dove:
> - **$Q$** è un insieme finito chiamato "**insieme degli stati**";
> - **$\Sigma$** è un insieme finito chiamato "**alfabeto**";
> - **$\delta:Q\times(\Sigma\cup\epsilon)\to \mathcal{P}(Q)$** è una "**funzione di transizione**";
> - **$q_{0}\in Q$** è lo **stato iniziale**;
> - **$F\subseteq Q$** è l'**insieme degli stati accettanti**.

Si noti, dunque, che quasi tutte le componenti di un NFA sono definite identicamente a un [[ACC_02 - Automi#Cos'è un automa finito?|DFA]], tranne per la funzione di transizione $\delta$: in questo caso, $\delta$ include nei possibili simboli in input la stringa vuota $\epsilon$, e non restituisce un singolo stato in modo deterministico ma piuttosto un insieme di stati in modo non-deterministico. 

A livello strutturale, le differenze principali sono queste. Ma **come avviene la computazione in un NFA?** Può sembrare, infatti, un controsenso affermare che l'automa può transitare in un insieme di stati: come si decide in quale di questi stati si transita? La risposta è, in realtà, che si transita in tutti questi stati! Avendo a che fare con NFA, infatti, si parla di più "**rami di computazione**", o anche "**cammini di computazione**", in cui quest'ultima si dirama in corrispondenza di transizioni di stato non-deterministiche. Per capire meglio di cosa stiamo parlando, vediamo uno schema generalizzato che pone a confronto le computazioni di un DFA e di un NFA:

![[confronto_dfa_nfa.png]]

Come si può vedere chiaramente dall'immagine, mentre **un DFA segue un unico flusso di computazione sequenziale**, e deciderà solo al termine dello stesso se accettare o rifiutare l'input ricevuto; **un NFA**, invece, **esegue tutti i suoi cammini di computazione in parallelo**, e ciascuno di questi cammini può terminare con un'accettazione o un rifiuto dell'input ricevuto. In questo contesto, l'accettazione di una sequenza di simboli assume un significato leggermente diverso: infatti, **un NFA accetta "overall" una sequenza se esiste almeno un cammino di computazione accettante**, dunque se almeno uno dei rami generati dalla computazione dell'NFA termina in uno stato accettante.

Come abbiamo detto, un NFA include nel suo alfabeto anche la stringa vuota $\epsilon$; ma cosa vuol dire concretamente ciò nel contesto della computazione? In parole povere, **in corrispondenza di un $\epsilon$-arco, l'NFA si dirama automaticamente nello stato di arrivo di tale arco**, senza bisogno dunque di un ulteriore input. E invece cosa succede se, una volta letto un determinato simbolo, non c'è nessun arco di transizione uscente dallo stato corrente associato a tale simbolo? Semplicemente, **il cammino di computazione considerato "muore"**, viene terminato, e si continuano a considerare gli eventuali altri.  

Ora, abbiamo tutta la conoscenza necessaria per comprendere un **esempio concreto di computazione di un NFA**. Considerando lo stesso automa fornito come esempio all'inizio di questo paragrafo, vediamo cosa succede se gli forniamo la sequenza di input $010110$:

![[computazione_nfa_esempio.png]]

Iniziamo, naturalmente, partendo dallo stato iniziale $q_{1}$, e leggiamo il primo simbolo $0$, che ci porta a rimanere su $q_{1}$; leggiamo poi il secondo simbolo $1$, e troviamo due archi di transizione, dunque la computazione si dirama in due cammini diversi, uno che rimane in $q_{1}$ e un altro che passa a $q_{2}$; al tempo stesso, però, appena arrivati in $q_{2}$ troviamo un arco di transizione con $\epsilon$, dunque viene generato subito anche un terzo cammino, che ci porta nello stato $q_{3}$; ora, leggiamo il terzo simbolo $0$, e notiamo subito che il cammino che si trova in $q_{3}$ muore, dato che $q_{3}$ non presenta nessun arco uscente associato a $0$; e così via. Dallo schema, notiamo che l'NFA finisce per accettare l'input $010110$, dato che almeno uno dei suoi cammini di computazione termina in uno stato accettante (in questo esempio, $q_{4}$). Più in generale, l'automa proposto accetta qualsiasi sequenza di simboli che contiene al suo interno la sotto-sequenza $101$ o $11$.

Come fatto per i DFA, anche per gli NFA possiamo introdurre il concetto di **configurazione**. In questo caso, si tratterà di una tupla $(q,\,x)\in Q\times \Sigma_{\epsilon}^*$, dato che l'alfabeto degli NFA include anche la stringa vuota $\epsilon$. Anche in questo caso, definire la configurazione ci permette di fare passi avanti verso la formalizzazione della computazione: se l'automa $M$ si trova nella configurazione $(q,\,ax)$, e $\delta$ impone che leggere $a$ nello stato $q$ porti l'automa nello stato $p$, allora si sa già che la prossima configurazione di $M$ sarà proprio $(p,\,x)$. Si tratta del medesimo passaggio di **produzione**, ossia:
$$(q,\,ax)\,\vdash_{M}\,(p,\,x)$$
In questo caso, però, la relazione vale se e solo se $p \in \delta(q,\,a)$, e non se i due membri coincidono (questo perché, tecnicamente, negli NFA $\delta(q,\,a)$ è un insieme di stati, non uno stato unico). Come abbiamo fatto in precedenza, anche stavolta è possibile estendere la relazione $\vdash_{M}$ in $\vdash_{M}^*$, e si ha che **la relazione $\vdash_{M}^*$ è riflessiva e transitiva**. Dunque, **la definizione formale di computazione rimane pressoché invariata**.

In generale, **[[ACC_02 - Automi#Trasformare un NFA in un DFA|ogni NFA può essere trasformato in un DFA equivalente]]**, ma costruire un NFA è spesso più facile, o perlomeno più semplice.
___
##### Linguaggi regolari tra NFA e DFA

Definiamo i **[[ACC_02 - Automi#Linguaggi|linguaggi regolari]] per gli NFA** nel modo seguente:

> Un linguaggio è detto "**linguaggio regolare per gli NFA**" se esiste un NFA che lo riconosce. Formalmente, indichiamo l'insieme di tali linguaggi con $\mathcal{L}(NFA)$, dove:
> $$\mathcal{L}(NFA)=\{L\subseteq \Sigma^*_{\epsilon}\,|\,\exists\text{ un NFA }N\text{ tale che }L(N)=L\}$$

È possibile dimostrare che l'insieme dei linguaggi regolari per gli NFA coincide con quello dei linguaggi regolari per i DFA, e che tali insiemi coincidano con l'insieme $REG$ definito in precedenza. Vogliamo dimostrare, dunque, che:
$$\mathcal{L}(NFA)=\mathcal{L}(DFA)=REG$$
Per dimostrare tale equivalenza, conviene dividere il procedimento in due parti ben distinte, ossia:
$$\mathcal{L}(NFA)\supseteq\mathcal{L}(DFA)\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\mathcal{L}(NFA)\subseteq\mathcal{L}(DFA)$$
Il primo verso, ossia che **$\mathcal{L}(DFA)$ sia un sottoinsieme di $\mathcal{L}(DFA)$**, è in realtà di banale dimostrazione: sappiamo che, per definizione, gli NFA rappresentano una generalizzazione dei DFA, o meglio che quest'ultimi consistono in un caso particolare di NFA, il che implica che lo stesso vale per i linguaggi riconosciuti da queste due categorie di automi.

Il secondo verso andrà, invece, formalmente dimostrato. L'idea alla base della nostra dimostrazione sarà la seguente: considerando un generico NFA $N=(Q_{N},\,\Sigma,\,\delta_{N},\,q_{0}^N,\,F_{N})$ che riconosca un determinato linguaggio $L$, vogliamo costruire un generico DFA $D=(Q_{D},\,\Sigma,\,\delta_{D},\,q_{0}^D,\,F_{D})$ che riconosca il medesimo linguaggio. Per fare ciò, il DFA $D$ dovrà essere in grado di tenere traccia di tutti i possibili [[ACC_02 - Automi#Definizione di NFA e differenze con i DFA|cammini di computazione]] esplorati dall'NFA $N$. Per semplicità, iniziamo questa costruzione supponendo che non ci siano $\epsilon$-archi (la dimostrazione verrà completata in seguito, aggiungendoli alle supposizioni che stiamo per fare):
- **l'insieme $Q_{D}$ degli stati di $D$**, dato che quest'ultimo dovrà tenere traccia di tutti i possibili cammini di computazione di $N$, **coinciderà con l'insieme $\mathcal{P}(Q_{N})$** (in altre parole, **ogni stato di $D$ corrisponde a un insieme di stati di $N$**);
- l'alfabeto $\Sigma$ rimane identico;
- **la funzione di transizione $\delta_{D}$** è definita come segue: 
$$\delta_{D}:Q_{D}\times \Sigma\to F_{D}\,\,\,\,\,\,\,\,\,\,\delta_{D}(R,\,a)=\bigcup_{r\,\in\,R}\delta_{N}(r,\,a)$$
     Informalmente, la funzione $\delta_{D}$ fa in modo che $D$ passi da uno stato $R$, che in realtà sappiamo rappresentare un insieme di stati $r$ di $N$, a un nuovo stato che rappresenta l'unione degli output dati da $\delta_{N}$ per quello stesso input;
- banalmente, **lo stato iniziale $q_{0}^D$ sarà lo stato corrispondente all'insieme $\{q_{0}^N\}$**;
- **l'insieme $F_{D}$** viene definito come $\{R\in Q_{D}\,|\,R\cap F_{N}\neq \emptyset\}$ (in altre parole, **è l'insieme degli stati $R$ di $D$ tali per cui $R$ contiene almeno uno stato accettante di $N$**).

La correttezza dell'automa $D$ appena creato non verrà dimostrata rigorosamente. A questo punto, per aggiungere la possibilità di $\epsilon$-archi e completare la dimostrazione, andiamo a definire, per ogni stato $R$ di $D$, l'insieme $E(R)$, ossia:
$$E(R)=\{q\in Q_{N}\,|\,q\text{ può essere raggiunto da stati in }R\text{ attraverso 0 o più }\epsilon\text{-archi}\}$$
A questo punto, possiamo utilizzare $E(R)$ per modificare alcune delle caratteristiche del DFA $D$: innanzitutto, visto che è possibile che $N$ abbia degli $\epsilon$-archi uscenti dal suo stato iniziale $q_{0}^N$, definiamo il nuovo stato iniziale $q_{0}^D$ come:
$$q_{0}^D=E(\{q_{0}^N\})$$
Modifichiamo anche la funzione di transizione $\delta_{D}$:
$$\delta_{D}(R,\,a)=\bigcup_{r\,\in\,R}E(\delta_{N}(r,\,a))$$
Abbiamo completato, a questo punto, la costruzione dell'automa $D$, dimostrando il teorema iniziale.
___
##### Trasformare un NFA in un DFA

Nella [[ACC_02 - Automi#Linguaggi regolari tra NFA e DFA|dimostrazione]] che abbiamo visto nel paragrafo precedente, abbiamo visto come creare, generalmente, un DFA equivalente a un NFA. Vediamo come farlo in modo concreto, partendo da un NFA $N$ e trasformandolo in un DFA $D$.

Consideriamo, ad esempio, il seguente NFA $N$:

![[nfa_to_dfa_esempio.png]]

L'**insieme degli stati** di $N$ è $Q_{N}=\{1,\,2,\,3\}$, dunque sappiamo subito che il DFA $D$ avrà un insieme di stati:$$Q_{D}=\mathcal{P}(Q_{N})=\{\emptyset,\,\{1\},\,\{2\},\,\{3\},\,\{1,\,2\},\,\{2,\,3\},\,\{1,\,3\},\,\{1,\,2,\,3\}\}$$Gli **stati iniziali** di $D$ saranno dati dall'insieme $E(\{1\})$, ossia dall'insieme degli stati raggiungibili da $1$ passando attraverso $\epsilon$-archi (più $1$ stesso); abbiamo un solo $\epsilon$-arco uscente da $1$, che porta a $3$, quindi otteniamo:$$q_{0}^D=E(\{1\})=\{1,\,3\}$$Per quanto riguarda gli **stati accettanti** di $D$, ossia l'insieme $F_{D}$, esso conterrà tutti gli stati che, al loro interno, contengono lo stato accettante di $N$. Dunque:
$$F_{D}=\{\{1\},\,\{1,\,2\},\,\{1,\,3\},\,\{1,\,2,\,3\}\}$$
Infine, determiniamo la **funzione di transizione** $\delta_{D}$, analizzando il comportamento dell'automa $D$ in base ai possibili input ricevuti e allo stato in cui esso viene ricevuto. Analizziamo, per primo, lo stato $\{2\}$:
- se viene letto $a$, $D$ va nello stato $\{2,\,3\}$ (in $N$, lo stato $2$ va sia in sé stesso che in $3$ con tale input, e non si va più lontano tramite $\epsilon$-archi); 
- se viene letto $b$, $D$ va nello stato $\{3\}$ (in $N$, lo stato $2$ va solo nello stato $3$ con tale input, e non si va più lontano tramite $\epsilon$-archi). 

Vediamo, poi, come ci si comporta nello stato $\{1\}$:
- se viene letto $a$, $D$ va nello stato $\emptyset$ (in $N$, non c'è un arco di transizione associato ad $a$ uscente dallo stato $1$);
- se viene letto $b$, $D$ va nello stato $\{2\}$ (in $N$, lo stato $1$ va solo nello stato $2$ con tale input, e non si va più lontano tramite $\epsilon$-archi).

Passiamo allo stato $\{3\}$:
- se viene letto $a$, $D$ va nello stato $\{1,\,3\}$ (in $N$, lo stato $3$ va solo nello stato $1$ con tale input, ma torna anche in $3$ tramite un $\epsilon$-arco);
- se viene letto $b$, $D$ va nello stato $\emptyset$ (in $N$, non c'è un arco di transizione associato a $b$ uscente dallo stato $3$).

Ora vediamo come ci si comporta con stati un po' più particolari, come ad esempio $\{1,\,2\}$:
- se viene letto $a$, $D$ va nello stato $\{2,\,3\}$ (in $N$, non c'è un arco di transizione associato ad $a$ uscente dallo stato $1$; al tempo stesso, però, lo stato $2$ va sia in sé stesso che in $3$ con tale input);
- se viene letto $b$, $D$ va nello stato $\{2,\,3\}$ (in $N$, lo stato $1$ va solo nello stato $2$ con tale input; al tempo stesso, lo stato $2$ va solo nello stato $3$ con tale input).

Procedendo in modo analogo per gli stati rimanenti, abbiamo a questo punto tutte le caratteristiche necessarie per disegnare il diagramma dell'automa $D$:

![[nfa_to_dfa_esempio1.png]]

L'automa ottenuto può essere semplificato osservando che nessun arco di transizione entra negli stati $\{1\}$ e $\{1,\,2\}$, per cui essi potranno essere rimossi senza ripercussioni. Facendo ciò, l'automa $D$ diventa:

![[nfa_to_dfa_esempio2.png]]
___
## Chiusura rispetto alle operazioni regolari (continua)

[[ACC_02 - Automi#Esempi di operazioni regolari e dimostrazione della chiusura rispetto all'unione|In precedenza]], ci eravamo fermati nel dimostrare la chiusura dei linguaggi regolari rispetto alle operazioni considerate per l'eccessiva complessità delle prove utilizzando automi deterministici. Tuttavia, ora che è stato introdotto il [[ACC_02 - Automi#Non-determinismo|non-determinismo]] e l'NFA, tali dimostrazioni potranno essere esposte molto più semplicemente.

##### Chiusura rispetto all'unione tramite NFA

Come prima cosa, torniamo a dimostrare la **chiusura rispetto all'operazione di unione**, ma stavolta facciamolo **tramite NFA** piuttosto che tramite DFA.



[TODO: Dimostrazione della chiusura rispetto all'unione con NFA (Lezione 4, pag. 5)]
[Libro: pag. 44]
___