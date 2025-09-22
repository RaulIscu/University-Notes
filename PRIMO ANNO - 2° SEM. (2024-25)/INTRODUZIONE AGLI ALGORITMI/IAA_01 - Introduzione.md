## Cos'è un algoritmo?

Il concetto di "algoritmo" è fondamentale per l'informatica, e ne costituisce per certi versi la base. Infatti, l'**informatica** può essere definita come la **scienza degli algoritmi** che descrivono e trasformano l'informazione. È dunque fondamentale chiarire cosa sia, concretamente, un algoritmo.

Un **algoritmo** è definito come una **sequenza di comandi elementari ed univoci**, che **terminano in un tempo finito** e **operano su strutture dati**.

In particolare, un **comando** è considerabile "**elementare**" quando non può essere scomposto in comandi più semplici, mentre è considerabile "**univoco**" quando può essere interpretato in un unico modo. Queste due caratteristiche risultano molto importanti nella progettazione di un algoritmo, dato che **un algoritmo ben specificato permette a chi lo esegue di "non pensare"**, ma di eseguire una serie di passaggi ben precisi in sequenza. Del resto, un calcolatore non pensa, si limita ad eseguire algoritmi progettati da esseri umani.

Come abbiamo detto, un algoritmo opera su **strutture dati**: esse possono essere definite come **strumenti utilizzati per organizzare e memorizzare dei dati**, consentendone l'accesso e la modifica. In generale, **non esiste una struttura dati adeguata per ogni problema**; bisogna, invece, conoscere le proprietà, i vantaggi e gli svantaggi di tutte le principali strutture dati, in modo da saper scegliere la più adatta in base al contesto e al problema da risolvere.

Infine, si è stabilito che l'esecuzione di un algoritmo deve **terminare in un tempo finito**. Con questa espressione, naturalmente, non si intende evidenziare soltanto la finitezza, ma anche la velocità e l'**efficienza** di un algoritmo, ossia la **quantificazione delle sue esigenze in termini di tempo** (tempo di esecuzione) **e spazio** (quantità di memoria richiesta). L'efficienza di un algoritmo viene spesso misurata mediante il suo **[[IAA_03 - Costo computazionale|costo computazionale]]**, argomento che verrà approfondito in seguito.
___
## Algoritmi e problem-solving

Gli algoritmi sono a tutti gli effetti una forma di **problem-solving**, uno strumento ideato per raggiungere una soluzione a partire da un problema iniziale. 

Generalmente, per risolvere un problema tramite un algoritmo si seguono questi passaggi:
- **analisi del problema**, che consiste in una lettura approfondita della situazione iniziale e in una comprensione e identificazione chiara del problema da risolvere;
- **esplorazione degli approcci possibili**, che consiste nella ricerca di una possibile metodologia per risolvere il problema;
- **selezione di un approccio** tra quelli possibili;
- **definizione dell'algoritmo risolutivo**, che richiede l'identificazione dei dati e la progettazione di una sequenza di comandi da eseguire su di essi;
- **riflessione critica**, da operare in seguito alla risoluzione per migliorare la soluzione trovata, identificando eventuali criticità o aumentando l'efficienza dell'algoritmo.

Nel nostro contesto, ci focalizzeremo su **problemi computazionali**, ossia problemi che richiedono di descrivere in maniera automatica una specifica relazione tra un insieme di valori presi in **input** e un altro insieme di valori presi in **output**. Pertanto, un algoritmo è definibile "corretto" se, per ogni istanza del problema, vengono generati i corretti valori in output.

Tra i vari problemi computazionali, possiamo evidenziare alcune **macro-categorie** ricorrenti, tra cui:
- problemi di **decisione**, ossia quei problemi per cui la risposta può essere o `True` o `False`;
- problemi di **ricerca**, ossia quei problemi per cui la risposta è un determinato valore o dato richiesto, magari a partire da un insieme di dati;
- problemi di **enumerazione**, ossia quei problemi per cui la risposta è un elenco di tutte le soluzioni ammissibili;
- problemi di **verifica**, ossia quei problemi in cui si deve andare a verificare se una risposta fornita risulta effettivamente valida per il problema che si sta cercando di risolvere;
- problemi di **ottimizzazione**, ossia quei problemi in cui, ad esempio, è definita una certa "funzione" e si chiede di selezionare la soluzione "massima" o "minima" in relazione a tale funzione.
___
## La Random Access Machine

Per valutare l'efficienza di un algoritmo, è necessario quantificare le risorse (in termini di tempo e di spazio) che richiede; per fare ciò in maniera accurata, tale analisi **non deve essere influenzata dalle capacità di una tecnologia specifica**. Per questo motivo, spesso, nell'analisi di un algoritmo viene utilizzata una "macchina astratta", un modello teorico indipendente dalle caratteristiche tecniche di un calcolatore reale: tale modello viene definito "**Random Access Machine**", o **modello RAM**.

Il modello RAM presenta alcune caratteristiche fondamentali e costanti, tra cui:
- l'esistenza di un **singolo processore**, che esegue le operazioni sequenzialmente;
- la capacità di eseguire **operazioni elementari**, ciascuna delle quali richiede un **tempo costante per l'esecuzione**;
- la presenza di un **limite per la dimensione dei valori memorizzati e per il numero di valori utilizzati**.
___
## Pseudocodice

Concretamente, un algoritmo viene implementato tramite la scrittura di codice. Prima della sua reale implementazione, però, può essere comodo avere un modo di **illustrare il funzionamento di un algoritmo formalmente**, in maniera indipendente dallo specifico linguaggio di programmazione scelto per implementarlo, in modo che sia immediatamente comprensibile il suo scopo e i mezzi che utilizza per arrivarci.

La soluzione usata per rispondere a questa esigenza è il cosiddetto "**pseudocodice**", ossia una scrittura dei passaggi che ricorda, per forma e sequenzialità, del codice effettivo, ma che è dotata di una sintassi molto più "rilassata" e permissiva: infatti, lo scopo principale dello pseudocodice è di illustrare il funzionamento di un algoritmo, non di rispettare i canoni di un linguaggio di programmazione effettivo.

Per la sua natura e sintassi, spesso lo pseudocodice utilizzato in questo corso ricorderà del codice scritto in **Python**.
___