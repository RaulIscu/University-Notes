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



[SLIDES: A.3... pag. 10...]
___