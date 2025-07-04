### Caratteristiche di Java


___
### Cos'è la programmazione a oggetti?


___
### Incapsulamento


___
### Ereditarietà

[tra le altre cose, EREDITARIETA' vs. COMPOSIZIONE]
___
### Polimorfismo


___
### Astrazione


___



Java è un linguaggio che si basa sulla **programmazione a oggetti**, o ***OOP*** (*Object Oriented Programming*). Qualsiasi programma scritto in Java utilizzerà, in qualche modo, una forma di programmazione a oggetti, e risulta quindi fondamentale comprendere al meglio questo concetto.

In generale, un programma consiste sostanzialmente di due elementi: **codice** e **dati**. Un programma qualsiasi, dunque, può essere organizzato in maniera più incentrata su una o l'altra componente: nel primo caso, si avrà un programma scritto attorno a "cosa sta succedendo", mentre nel secondo un programma basato su "chi viene affetto" da ogni azione. Il primo metodo dà vita alla "**programmazione procedurale**", mentre il secondo, concepito in parte per gestire complessità che il primo fatica a contenere, dà vita proprio alla "**programmazione a oggetti**". Nella programmazione a oggetti, dunque, un programma è organizzato attorno ai dati su cui lavora (chiamati, appunto, "oggetti").
___
Un elemento essenziale della programmazione a oggetti è l'**astrazione**, ossia la capacità di vedere un insieme di parti individuali collegate come un unico oggetto con le sue proprietà e i suoi comportamenti. Applichiamo, ad esempio, una forma d'astrazione quando pensiamo al complesso di sistemi di accelerazione, freno, sterzo, e così via come a una "macchina".

Utilizzare l'astrazione implica l'utilizzo di **classificazioni gerarchiche**, che permettono di stratificare un sistema o un oggetto complesso, suddividendolo gradualmente in componenti più semplici e più specializzate. Ad esempio, una macchina può essere suddivisa nel motore, nello sterzo, nei freni, e nei suoi vari altri sotto-sistemi, e ognuno di questi può essere suddiviso a sua volta. Lo stesso principio vale per un programma informatico: dei dati possono essere organizzati in vari **oggetti**, e si potranno definire con chiarezza dei **metodi** che si potranno usare per comunicare con ognuno di essi; in questo modo, si potranno trattare gli oggetti come entità uniche, a cui si potranno impartire determinati comandi.
___
Alla base della programmazione a oggetti troviamo tre meccanismi fondamentali:
- l'**incapsulamento**;
- l'**ereditarietà**;
- il **polimorfismo**.

L'**incapsulamento** è il meccanismo che organizza e unisce del codice e dei dati, e allo stesso tempo protegge quest'ultimi da interferenze esterne o da usi inadatti. Si può pensare a tale meccanismo come a uno strato protettivo, che impedisce l'accesso arbitrario da parte di altro codice definito fuori da esso; l'accesso a ciò che è contenuto in questo strato protettivo viene invece controllato tramite un'interfaccia ben definita. 

In Java, la base dell'incapsulamento è la "**classe**", che definisce la struttura e il comportamento di un determinato gruppo di oggetti. Dunque, un oggetto di una determinata classe seguirà strettamente il modello astratto imposto da quest'ultima: perciò, un oggetto viene anche definito come una "**istanza**" della sua classe. Nella definizione di una classe, i dati relativi ad essa prendono il nome di "**variabili di istanza**", mentre le varie istruzioni che possono lavorare su quei dati sono i "**metodi**". Sostanzialmente, dunque, i metodi di una classe definiscono i modi in cui le variabili di istanza possono essere utilizzate e manipolate in un programma.

Ogni metodo e variabile di una classe può essere definito come "**privato**" (`private`) o "**pubblico**" (`public`): metodi e variabili privati consentono l'accesso solo ad altri metodi della stessa classe; metodi e variabili pubblici, invece, possono essere visti da qualsiasi utente esterno.

L'**ereditarietà** è il meccanismo che consente a un oggetto di acquisire le proprietà di un altro oggetto, supportando il concetto di "classificazione gerarchica" esposto in precedenza. Senza l'utilizzo di gerarchie, ogni singolo oggetto dovrebbe definire da zero tutte le sue caratteristiche; le gerarchie, e dunque l'ereditarietà, consentono invece a un oggetto di definire all'interno di sé stesso solo quelle caratteristiche che lo rendono unico rispetto al resto della sua classe.

L'ereditarietà si può applicare anche tra classi: è possibile, infatti, avere una **sotto-classe** all'interno di una classe più grande. Gli oggetti della sotto-classe prenderanno, quindi, tutte le caratteristiche della classe iniziale (o **super-classe**), ma anche quelle più specifiche che definiscono la sotto-classe, oltre ovviamente a quelle relative ai singoli oggetti.

Il **polimorfismo**, sostanzialmente, è il meccanismo per il quale una stessa "interfaccia" può indicare più metodi. Per capire meglio cosa si intende per "polimorfismo", immaginiamo di istanziare dei metodi per la somma di due numeri all'interno di una classe: volendo separare la somma tra interi e quella tra reali, si potrebbero definire due metodi distinti e separati; in alternativa, per semplificare il tutto, si può invece sfruttare il concetto di polimorfismo e definire entrambi i metodi con la stessa denominazione, modificandone piuttosto il tipo previsto di *input*. Così facendo, si potrà semplicemente chiamare il metodo generale, e spetterà al compilatore il compito di capire, in base agli *input* forniti, quale delle due variazioni del metodo utilizzare.

Dunque, in parole povere, il polimorfismo permette di ridurre la complessità di un programma, sfruttando la stessa interfaccia per svolgere più azioni.

