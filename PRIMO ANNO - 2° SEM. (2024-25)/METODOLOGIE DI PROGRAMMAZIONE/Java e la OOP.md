## Caratteristiche di Java

**Java** è un **linguaggio di programmazione** creato dalla **Sun Microsystems** e pubblicato ufficialmente per la prima volta nel **1995**. Si tratta di un linguaggio completamente basato sulla **[[Java e la OOP#Cos'è la programmazione a oggetti?|programmazione a oggetti]]**, o **OOP**, ampiamente utilizzato anche da applicazioni e aziende famosissime e diffuse (tra le altre, Java viene utilizzato nello sviluppo di Spotify, Airbnb, Google, Instagram, Netflix, e molte altre).

La principale caratteristica che differenzia Java dagli altri linguaggi del genere è la sua possibilità di essere notevolmente ***cross-platform***: un programma Java, infatti, rispetta la politica "**WORA**", ossia "***write once, run anywhere***", ed è sostanzialmente **neutro rispetto all'architettura che lo esegue**. Ciò viene ottenuto soprattutto grazie agli strumenti contenuti nel **Java Development Kit**, o **JDK**, che contiene principalmente questi strumenti:
- la **Java Virtual Machine**, la componente che più di tutte è responsabile dell'abilità di essere *cross-platform* di Java;
- il **Java Runtime Envoirment**;
- il compilatore **Java Compiler**, o **javac**;
- varie **librerie** utili per la scrittura di codice e per la sua compilazione.

Oltre a ciò, Java è un linguaggio **sicuro** e **difficilmente manomissibile**, supporta l'esecuzione di più attività in contemporanea mediante un **ambiente di esecuzione *multithreaded***, è molto **flessibile** e **versatile** (può essere utilizzato per applicazioni desktop, programmi di puro back-end, integrato in ambienti web, ecc. ecc.), e costantemente **aggiornato** con nuove versioni a cadenza pressoché annua.
___
## Cos'è la programmazione a oggetti?

Come detto nel capitolo precedente, Java è un linguaggio basato sulla programmazione a oggetti: ma cos'è la programmazione a oggetti?

La **programmazione a oggetti** è un paradigma di programmazione ben diverso da quello "**procedurale**" che caratterizza maggiormente linguaggi come C o Python. Nella OOP, si potrebbe dire che "**tutto è un oggetto**", un'entità di un certo tipo che può contenere altri dati ed eventualmente altri oggetti, che ha uno stato e che può effettuare determinate operazioni. In questo contesto, il funzionamento di un programma va a coincidere con le diverse interazioni che hanno gli oggetti tra di loro, e con i risultati di tali interazioni.

La corretta applicazione del paradigma della programmazione a oggetti, il più delle volte, si valuta in base all'applicazione dei suoi **principi fondamentali**, che sono:
- **incapsulamento**;
- **ereditarietà**;
- **polimorfismo**;
- **astrazione**.
___
## Incapsulamento

L'**incapsulamento** è il principio che professa la **protezione dei dati** da accessi non controllati ed eventualmente inopportuni. Un'applicazione corretta dell'incapsulamento in un programma porta all'**occultamento di informazioni non necessarie all'utente**, rendendo invece pubblica una certa "interfaccia", tendenzialmente corrispondente con un insieme di metodi pubblici.

Protagonisti nell'applicazione concreta dell'incapsulamento sono i **[[Modificatori d'accesso|modificatori d'accesso]]**, e il contesto principale dove viene utilizzato è nella **definizione dei [[Classi#Campi, metodi e costruttori|campi di una classe]]**, che vengono solitamente definiti come  `private` e sono resi visualizzabili e manipolabili tramite dei metodi "getter" e "setter" definiti come `public`.

Un corretto utilizzo dell'incapsulamento offre vari vantaggi, tra cui:
- una maggiore **protezione** e un miglior **controllo dei dati**, il cui accesso viene regolato e permesso solo sotto certe condizioni (ad esempio, è possibile progettare metodi getter e setter che prevedano dei controlli o delle operazioni particolari);
- una **semplificazione dell'ambiente di lavoro** (nascondere informazioni non necessarie per l'utente rende minore l'ammontare totale di informazioni disponibili);
- spesso, una **maggiore manutenibilità del codice**, così come una maggiore **riutilizzabilità**.
___
## Ereditarietà

[tra le altre cose, EREDITARIETA' vs. COMPOSIZIONE]
___
## Polimorfismo

Il **polimorfismo** è il principio che viene applicato quando 
___
## Astrazione


___




Un elemento essenziale della programmazione a oggetti è l'**astrazione**, ossia la capacità di vedere un insieme di parti individuali collegate come un unico oggetto con le sue proprietà e i suoi comportamenti. Applichiamo, ad esempio, una forma d'astrazione quando pensiamo al complesso di sistemi di accelerazione, freno, sterzo, e così via come a una "macchina".

Utilizzare l'astrazione implica l'utilizzo di **classificazioni gerarchiche**, che permettono di stratificare un sistema o un oggetto complesso, suddividendolo gradualmente in componenti più semplici e più specializzate. Ad esempio, una macchina può essere suddivisa nel motore, nello sterzo, nei freni, e nei suoi vari altri sotto-sistemi, e ognuno di questi può essere suddiviso a sua volta. Lo stesso principio vale per un programma informatico: dei dati possono essere organizzati in vari **oggetti**, e si potranno definire con chiarezza dei **metodi** che si potranno usare per comunicare con ognuno di essi; in questo modo, si potranno trattare gli oggetti come entità uniche, a cui si potranno impartire determinati comandi.
___
Alla base della programmazione a oggetti troviamo tre meccanismi fondamentali:
- l'**incapsulamento**;
- l'**ereditarietà**;
- il **polimorfismo**.

L'**ereditarietà** è il meccanismo che consente a un oggetto di acquisire le proprietà di un altro oggetto, supportando il concetto di "classificazione gerarchica" esposto in precedenza. Senza l'utilizzo di gerarchie, ogni singolo oggetto dovrebbe definire da zero tutte le sue caratteristiche; le gerarchie, e dunque l'ereditarietà, consentono invece a un oggetto di definire all'interno di sé stesso solo quelle caratteristiche che lo rendono unico rispetto al resto della sua classe.

L'ereditarietà si può applicare anche tra classi: è possibile, infatti, avere una **sotto-classe** all'interno di una classe più grande. Gli oggetti della sotto-classe prenderanno, quindi, tutte le caratteristiche della classe iniziale (o **super-classe**), ma anche quelle più specifiche che definiscono la sotto-classe, oltre ovviamente a quelle relative ai singoli oggetti.

Il **polimorfismo**, sostanzialmente, è il meccanismo per il quale una stessa "interfaccia" può indicare più metodi. Per capire meglio cosa si intende per "polimorfismo", immaginiamo di istanziare dei metodi per la somma di due numeri all'interno di una classe: volendo separare la somma tra interi e quella tra reali, si potrebbero definire due metodi distinti e separati; in alternativa, per semplificare il tutto, si può invece sfruttare il concetto di polimorfismo e definire entrambi i metodi con la stessa denominazione, modificandone piuttosto il tipo previsto di *input*. Così facendo, si potrà semplicemente chiamare il metodo generale, e spetterà al compilatore il compito di capire, in base agli *input* forniti, quale delle due variazioni del metodo utilizzare.

Dunque, in parole povere, il polimorfismo permette di ridurre la complessità di un programma, sfruttando la stessa interfaccia per svolgere più azioni.

