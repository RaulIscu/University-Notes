## Cos'è una "logica"?

Per parlare di **logica di primo ordine**, o "**First Order Logic**" (spesso abbreviata in **FOL**), è opportuno chiarire prima di tutto il concetto di "**logica**" più in generale.

Una logica può essere definita come una **famiglia di linguaggi formali utilizzati per rappresentare informazioni e derivare conseguenze**. Ogni logica, come ogni linguaggio formale, è definita da due componenti:
- una **sintassi**, ossia l'insieme delle sequenze finite di simboli ammesse dal linguaggio (tali sequenze vengono anche dette "**formule**"), dove ogni simbolo appartiene a un insieme prefissato (tale insieme viene detto "**alfabeto**");
- una **semantica**, ossia l'assegnamento di un significato a ogni formula della logica considerata.

Dunque, in parole povere, la sintassi definisce **la struttura che le formule devono rispettare**, mentre la semantica definisce **la verità di una formula nei diversi "mondi" possibili**.

Per comprendere meglio di cosa si sta parlando, prendiamo come esempio l'aritmetica: la sintassi dell'aritmetica impone che l'espressione $x+2\ge y$ è effettivamente una formula valida, mentre ad esempio $x2 + y\ge$ non lo è; al tempo stesso, per la semantica dell'aritmetica possiamo affermare che la formula $x+2\ge y$ è vera se e solo se il valore di $x+2$ non è minore del valore di $y$, oppure che $x+2\ge y$ è una formula vera in un "mondo" dove $x=7$ e $y=1$, mentre è falsa laddove $x=0$ e $y=6$.

Nelle logiche classiche, **ogni formula è vera o falsa in ogni mondo**. In generale, dunque, dato un mondo $m$ e una formula $\varphi$, si dice che "**m è modello di $\varphi$**" e si scrive:
$$m\,\vDash\,\varphi$$
se e solo se la formula $\varphi$ è vera nel mondo $m$.

##### Sintassi

Come già anticipato, la **sintassi** di una logica serve a **definire l'insieme delle sequenze finite di simboli ammesse** nella stessa, dove ciascuno di questi simboli deve appartenere a un insieme prefissato; abbiamo anche già detto che tali sequenze vengono dette "**formule**", mentre l'insieme a cui devono appartenere i simboli viene detto "**alfabeto**".

Dunque, per **definire la sintassi di una logica**, occorre stabilire:
- quali simboli appartengono al suo alfabeto;
- quali sequenze finite di elementi dell'alfabeto (dunque, quali formule) compongono la logica.

Si ricorda, tuttavia, che **la sintassi non dice nulla sul significato delle formule**: tale compito, infatti, è riservato strettamente alla [[BD2_03 - FOL#Semantica|semantica]].
___
##### Semantica

Come già anticipato, la **semantica** di una logica serve a **definire il significato di ogni formula della logica**, così come **la loro verità nei diversi mondi possibili**. L'idea alla base del **definire la semantica di una logica**:
1. dare un significato (in altre parole, un'interpretazione) alle formule più semplici, dette anche "formule atomiche";
2. usare le regole del sistema logico per stabilire il significato di formule arbitrarie.

Per capire meglio come funziona la semantica, si guardi di nuovo alle espressioni aritmetiche: per valutare, ad esempio, l'espressione $x+y\le 20$, si valutano prima le formule atomiche $x$ e $y$, e poi si sfruttano le regole dell'aritmetica per valutare l'espressione completa.
___
## Logica di primo ordine (FOL)

La **logica di primo ordine**, che verrà chiamata **FOL** per semplicità, è naturalmente un esempio di [[BD2_03 - FOL#Cos'è una "logica"?|logica]]. In quanto tale, in questo paragrafo andremo ad approfondire aspetti della FOL come:
- l'**[[BD2_03 - FOL#Alfabeto della FOL|alfabeto]]**, e di conseguenza le varie **[[BD2_03 - FOL#Formule nella FOL|formule]]** che si possono comporre;
- la **[[BD2_03 - FOL#Semantica della FOL|semantica]]**;
- i modi per **valutare [[BD2_03 - FOL#Valutazione dei termini|termini]] e [[BD2_03 - FOL#Valutazione delle formule|formule]]**.

##### Alfabeto della FOL

L'**alfabeto** della FOL è composto da:
- un insieme **$\mathcal{V}$** di **variabili**;
- un insieme **$\mathcal{F}$** di **simboli di funzione**, ognuno dei quali associato a un proprio numero di argomenti, detto "**arità**";
- un insieme **$\mathcal{P}$** di **simboli di predicato**, ognuno dei quali associato a una propria **arità** (si assume che $\mathcal{P}$ contenga sempre il predicato di arità pari a 2 chiamato "**uguaglianza**" e denotato dal simbolo **$=$**);
- i **connettivi logici** $\lnot$, $\lor$, $\land$, $\rightarrow$ e $\leftrightarrow$;
- i **quantificatori** $\forall$ e $\exists$, denominati rispettivamente "**quantificatore universale**" e "**quantificatore esistenziale**";
- i **simboli speciali** "$($", "$)$" e "$,$".

Dato che il simbolo di predicato $=$, ossia quello dell'uguaglianza, è obbligatorio e presente pressoché in qualsiasi logica, spesso verrà omesso per semplicità quando si elencheranno i simboli di interesse.

Per riferirci a un **simbolo di funzione $f$ di arità $k$**, o anche a un **simbolo di predicato $p$ di arità $k$**, si utilizzeranno rispettivamente le notazioni $f/k$ e $p/k$. In questo contesto, i simboli di funzione di arità $0$ vengono anche detti "**simboli di costante**"; invece, i simboli di predicato di arità $0$ vengono anche detti "**lettere proposizionali**". Vediamo, di seguito, alcuni **esempi di possibili simboli di funzione**, per farci un'idea di come funzionano:
- **$\text{zero/0}$** è un simbolo di funzione di arità $0$, che può essere utilizzato per indicare il numero naturale $0$ (avendo arità pari a $0$, si tratta di un simbolo di costante);
- $\text{succ/1}$ è un simbolo di funzione di arità $1$, che può essere utilizzato per indicare il numero naturale successivo a un numero $X$ dato, in modo che $\text{succ}(X)=X+1$;
- $\text{socrate/0}$ è un simbolo di funzione di arità $0$, che può essere utilizzato per indicare l'individuo Socrate (si tratta di un simbolo di costante);
- $\text{padre/1}$ è un simbolo di funzione di arità $1$, che può essere utilizzato per indicare il padre di un certo individuo $X$ in modo che $\text{padre}(X)$ sia il padre di $X$.

Ora, vediamo alcuni **esempi di possibili simboli di predicato**:
- $\text{doppio/2}$ è un simbolo di predicato di arità $2$, che può essere utilizzato per decretare se un numero naturale $Y$ è il doppio di un altro numero naturale $X$, in modo che $\text{doppio}(X,\,Y)$ sia vero solo se $Y=2X$; 
- $\text{somma/3}$ è un simbolo di predicato di arità $3$, che può essere utilizzato per decretare se un numero naturale $z$ è dato dalla somma di altri due numeri naturali $X$ e $Y$, in modo che $\text{somma}(X,\,Y,\,Z)$ sia vero solo se $X+Y=Z$; 
- $\text{uomo/1}$ è un simbolo di predicato di arità $1$, che può essere utilizzato per decretare se un certo individuo $X$ è un uomo, in modo che $\text{uomo}(X)$ sia vero solo se $X$ è un uomo;
- $\text{mortale/1}$ è un simbolo di predicato di arità $1$, che può essere utilizzato per decretare se un certo individuo $X$ è mortale, in modo che $\text{mortale}(X)$ sia vero solo se $X$ è mortale.

In caso non si sia capito finora, si chiarisce la **differenza principale tra funzioni e predicati**, e di conseguenza tra simboli degli uni e degli altri: in parole povere, **le funzioni individuano degli oggetti specifici nel "dominio" in cui si sta lavorando, mentre i predicati verificano delle verità riguardanti tali oggetti**. Insomma, i simboli di funzione vengono utilizzati per ottenere dei valori, mentre i simboli di predicato servono per affermare dei fatti riguardo tali valori, o per verificare che dei fatti siano veri.
___
##### Formule nella FOL

A partire dall'[[BD2_03 - FOL#Alfabeto della FOL|alfabeto della FOL]], si può definire il **linguaggio** della stessa. Si tratta di un linguaggio con una struttura sintattica, per certi versi, più complessa di quella della logica proposizionale classica: la sua definizione induttiva, infatti, viene effettuata in **due passaggi**:
1. viene definito un linguaggio intermedio, chiamato "**linguaggio dei termini**";
2. viene definito l'effettivo "**linguaggio delle formule**", utilizzando al suo interno le regole base stabilite nel linguaggio dei termini.

Partiamo dal primo passaggio, ossia la **definizione del linguaggio dei termini**. Per poter approfondire ciò, dovremo innanzitutto chiarire cosa si intende con "**termini**". L'insieme dei termini è definito induttivamente come segue:
- **ogni variabile in $\mathcal{V}$ è un termine**;
- **ogni [[BD2_03 - FOL#Alfabeto della FOL|simbolo di costante]] in $\mathcal{F}$ è un termine**;
- se $f$ è un simbolo di funzione di arità $n>0$ e $t_{1},\,t_{2},\,\dots,\,t_{n}$ sono tutti termini, allora anche **$f(t_{1},\,t_{2},\,\dots,\,t_{n})$ è un termine**.

Ad esempio, supponiamo di avere il seguente insieme $\mathcal{F}$ di simboli di funzione:
$$\mathcal{F}=\{\text{zero/0},\,\text{succ/1},\,\text{socrate/0},\,\text{padre/1}\}$$
Dato questo insieme, possiamo affermare che le seguenti sequenze di simboli sono a tutti gli effetti dei termini (si specifica che $\text{MiaVariabile}$ e $X$ sono variabili): 
- $\text{zero}$;
- $\text{MiaVariabile}$;
- $\text{succ(zero)}$;
- $\text{padre(padre(socrate))}$;
- $\text{padre(succ(X))}$;
- $\text{succ(succ(zero))}$. 

A questo punto, avendo chiarito cosa si intende con "termini", possiamo arrivare alle **formule**. In particolare, l'insieme delle formule è definito induttivamente come segue:
- se $p$ è un simbolo di predicato di arità $n$ e $t_{1},\,t_{2},\,\dots,\,t_{n}$ sono termini, allora $p(t_{1},\,t_{2},\,\dots,\,t_{n})$ è una **formula** (una formula di questo tipo viene detta "**formula atomica**");
- se $\phi$ e $\psi$ sono formule, allora lo sono anche $(\phi)$, $\lnot\phi$, $\phi \lor\psi$, $\phi \land \psi$, $\phi\rightarrow \psi$ e $\phi\leftrightarrow \psi$;
- se $\phi$ è una formula e $x$ è una variabile, allora $\forall x\,\,\phi$ e $\exists x\,\,\phi$ sono formule.

Per quello che abbiamo detto finora, il simbolo di predicato dell'uguaglianza potrebbe essere utilizzato solo nei modi seguenti in formule valide: $=(X,\,Y)$ per indicare che $x$ e $y$ sono uguali; $\lnot=(X,\,Y)$ per indicare che $X$ e $Y$ non sono uguali. Tuttavia, per semplicità e leggibilità, si preferirà utilizzare le forme $X=Y$ e $X\neq Y$.

Vediamo, a questo punto, alcuni **esempi di formule valide**:
- $\text{doppio}(\text{succ}(\text{succ}(\text{zero})),\,X)$;
- $\exists X\,\,\text{doppio}(\text{succ}(\text{succ}(\text{zero})),\,X)$;
- $\forall X\,\,\text{doppio}(\text{succ}(\text{succ}(\text{zero})),\,X)$;
- $\text{somma}(\text{succ}(\text{zero}),\,\text{zero},\,\text{succ}(zero))$;
- $\forall X\,\forall Y\,\,\text{somma}(X,\,X,\,Y)\rightarrow \text{doppio}(X,\,Y)$;
- $(\forall X\,\exists Y\,\,\text{doppio(X,\,Y)})\,\land\,(\forall I\,\forall J\,\exists K\,\,\text{somma}(I,\,J,\,K))$;
- $\text{mortale}(\text{socrate})\,\land\,\text{mortale}(\text{padre}(\text{socrate}))$;
- $\forall X\,\,\text{mortale}(X)$;
- $\forall X\,\forall Y\,\,\text{uomo}(X)$;
- $X=\text{socrate}$;
- $\forall X\,\,\text{uomo}(X)\rightarrow \text{uomo}(\text{socrate})$.

Di seguito, invece, si presentano alcune notazioni che non sono formule, con annesse le motivazioni:
- $\text{succ}(\text{zero})$, dato che si tratta semplicemente di un termine;
- $\text{mortale}(\text{mortale}(\text{socrate}))$, dato che **il simbolo di predicato** $\text{mortale}$ **può ricevere come "input" solo un termine**, e $\text{mortale}(\text{socrate})$ non lo è;
- $\exists\text{socrate}\,\,\text{mortale}(\text{socrate})$, dato che **i quantificatori possono essere applicati solo a variabili**, mentre $\text{socrate}$ è in realtà un [[BD2_03 - FOL#Alfabeto della FOL|simbolo di costante]];
- $\exists X\,\,\text{padre}(X)$, dato che $\text{padre}(X)$ è un termine, e **i quantificatori formano formule solo se abbinati ad altre formule**;
- $X\lor Y$, dato che **i connettivi logici servono a collegare due formule**, non due variabili come $X$ e $Y$;
- $X\land\text{zero}=$, sia per il motivo appena visto sia perché **l'uguaglianza è un predicato binario**, dunque che chiede di avere un termine da un lato e uno dall'altro per formare una formula, mentre in questo esempio non c'è alcun termine nel lato destro.
___
##### Semantica della FOL

Per poter proseguire nel trattare la **semantica della FOL**, soffermiamoci su un tipo di formule che rappresenteranno il nostro punto di partenza: le "**formule atomiche**". Una formula atomica è una **[[BD2_03 - FOL#Formule nella FOL|formula]] priva di connettivi e di quantificatori, che non può essere divisa in formule più semplici**. Rappresenta la base della semantica proprio perché consiste nel "mattoncino" logico più semplice possibile, e per verificare la sua realtà non serve fare calcoli logici o semplificazioni di qualche tipo, ma basta **osservare il "mondo" in cui si sta lavorando**. Tipicamente, le formule atomiche nella FOL possono presentarsi solo in tre modi diversi:
- un **predicato** di arità $n$ **applicato a $n$ termini**;
- un'**uguaglianza**;
- un **predicato con arità $0$**, ossia una **lettera proposizionale**.

Ricordiamo brevemente, a questo punto, come funziona la **semantica nella logica proposizionale**, in modo da avere delle basi per la trattazione di quella nella FOL. Nella logica proposizionale, le formule atomiche sono proprio le lettere proposizionali, e la semantica parte da una funzione speciale detta "**interpretazione**" e indicata con la lettera **$I$**: in parole povere, la funzione $I$ serve per **assegnare un valore di verità ad ogni lettera proposizionale** nel mondo in cui si sta lavorando. Data un'interpretazione per le varie lettere proposizionali, entra in gioco una "**funzione di valutazione**" che, data una formula più o meno complessa e un'interpretazione delle sue sotto-formule atomiche, **calcola il valore di verità della formula rispetto all'interpretazione data**. Per comprendere meglio, vediamo un esempio. Supponiamo di avere la formula:
$$\varphi:\,a\land(b\lor c)$$
All'interno della formula $\varphi$, le lettere proposizionali sono $a$, $b$ e $c$, dunque per procedere si dovrà fornire un'interpretazione di tali lettere; supponiamo, dunque, che l'interpretazione sia $I(a)=true$, $I(b)=true$ e $I(c)=false$. A questo punto, grazie alla funzione di valutazione, la formula viene valutata induttivamente proprio a partire dei valori dati alle sotto-formule atomiche (ossia, alle lettere proposizionali) dall'interpretazione $I$. Avremo, infatti, che:
- se $I(b)=true$ e $I(c)=false$, allora per la semantica del connettivo $\lor$ la formula $(b\lor c)$ viene valutata come $true$;
- se $I(a)=true$ e, come abbiamo appena dimostrato, $(b\lor c)$ vale $true$, allora per la semantica del connettivo $\land$ la formula $a\land (b\lor c)$ vale $true$.

Dunque, nell'interpretazione $I$ data, la formula proposizionale $\varphi$ è vera, e possiamo quindi dire che l'interpretazione $I$ è [[BD2_03 - FOL#Cos'è una "logica"?|modello]] di $\varphi$, o simbolicamente che:
$$I\,\vDash\,\varphi$$
In generale, i significati delle formule proposizionali possono essere estesi senza necessariamente fare riferimento a particolari interpretazioni. Infatti, tra le varie formule possibili, possiamo trovare:
- formule **soddisfacibili**, tali per cui **esiste un'interpretazione che è loro modello**;
- formule **valide**, tali per cui **ogni interpretazione è loro modello**;
- formule **insoddisfacibili**, tali per cui **nessuna interpretazione è loro modello**.

La **semantica della FOL**, per certi versi, segue lo stesso itinerario che vale per la logica proposizionale: 
1. si definisce la nozione di **interpretazione**, e dunque di **valutazione delle formule atomiche**;
2. si definisce **come viene valutata una formula data una particolare interpretazione**;
3. si stabilisce il **significato di ogni formula senza necessariamente fare riferimento a particolari interpretazioni**.



[SLIDES: A.3... pag. 28/35]
___
##### Valutazione dei termini

[SLIDES: A.3... pag. 37/47]
___
##### Valutazione delle formule

[SLIDES: A.3... pag. 49/67]
___