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
- $\text{succ/1}$ è un simbolo di funzione di arità $1$, che può essere utilizzato per indicare il numero naturale successivo a un numero $x$ dato, in modo che $\text{succ}(x)=x+1$;
- $\text{socrate/0}$ è un simbolo di funzione di arità $0$, che può essere utilizzato per indicare l'individuo Socrate (si tratta di un simbolo di costante);
- $\text{padre/1}$ è un simbolo di funzione di arità $1$, che può essere utilizzato per indicare il padre di un certo individuo $x$ in modo che $\text{padre}(x)$ sia il padre di $x$.

Ora, vediamo alcuni **esempi di possibili simboli di predicato**:
- $\text{doppio/2}$ è un simbolo di predicato di arità $2$, che può essere utilizzato per decretare se un numero naturale $y$ è il doppio di un altro numero naturale $x$, in modo che $\text{doppio}(x,\,y)$ sia vero solo se $y=2x$; 
- $\text{somma/3}$ è un simbolo di predicato di arità $3$, che può essere utilizzato per decretare se un numero naturale $z$ è dato dalla somma di altri due numeri naturali $x$ e $y$, in modo che $\text{somma}(x,\,y,\,z)$ sia vero solo se $x+y=z$; 
- $\text{uomo/1}$ è un simbolo di predicato di arità $1$, che può essere utilizzato per decretare se un certo individuo $x$ è un uomo, in modo che $\text{uomo}(x)$ sia vero solo se $x$ è un uomo;
- $\text{mortale/1}$ è un simbolo di predicato di arità $1$, che può essere utilizzato per decretare se un certo individuo $x$ è mortale, in modo che $\text{mortale}(x)$ sia vero solo se $x$ è mortale.

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
Dato questo insieme, possiamo affermare che le seguenti sequenze di simboli sono a tutti gli effetti dei termini (si specifica che $\text{MiaVariabile}$ e $x$ sono variabili): 
- $\text{zero}$;
- $\text{MiaVariabile}$;
- $\text{succ(zero)}$;
- $\text{padre(padre(socrate))}$;
- $\text{padre(succ(x))}$;
- $\text{succ(succ(zero))}$. 

A questo punto, avendo chiarito cosa si intende con "termini", possiamo arrivare alle **formule**. In particolare, l'insieme delle formule è definito induttivamente come segue:
- se $p$ è un simbolo di predicato di arità $n$ e $t_{1},\,t_{2},\,\dots,\,t_{n}$ sono termini, allora $p(t_{1},\,t_{2},\,\dots,\,t_{n})$ è una **formula** (una formula di questo tipo viene detta "**formula atomica**");
- se $\phi$ e $\psi$ sono formule, allora lo sono anche $(\phi)$, $\lnot\phi$, $\phi \lor\psi$, $\phi \land \psi$, $\phi\rightarrow \psi$ e $\phi\leftrightarrow \psi$;
- se $\phi$ è una formula e $x$ è una variabile, allora $\forall x\,\,\phi$ e $\exists x\,\,\phi$ sono formule.



[SLIDES: A.3... pag. 18/20]
___
##### Semantica della FOL

[SLIDES: A.3... pag. 23/35]
___
##### Valutazione dei termini

[SLIDES: A.3... pag. 37/47]
___
##### Valutazione delle formule

[SLIDES: A.3... pag. 49/67]
___