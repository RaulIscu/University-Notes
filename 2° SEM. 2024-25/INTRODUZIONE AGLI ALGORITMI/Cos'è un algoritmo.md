Un **algoritmo** può essere visto, in via generale, come una sequenza di comandi "**elementari ed univoci**", che deve terminare in un **tempo finito**, e opera su delle "**strutture dati**".
___
Un comando "**elementare**" è un comando che non può essere scomposto in comandi più semplici; inoltre, un comando "**univoco**" è un comando non ambiguo, che può essere interpretato in un solo modo.

Se un algoritmo è ben specificato, e dunque composto da comandi elementari e univoci, chi lo esegue non ha necessità di interpretare o riflettere sulle istruzioni, ma può eseguirle con precisione e in sequenza senza problemi. Generalmente, dunque, se si verifica un errore nell'esecuzione di un algoritmo, esso sarà generalmente ascrivibile a un errore nella progettazione dell'algoritmo stesso.
___
Per poter risolvere un problema mediante un algoritmo, è ovviamente necessario gestire, organizzare e manipolare dei dati. A tal fine, bisogna definire delle opportune "**strutture dati**", che si occupano proprio di queste mansioni, in modo da semplificare il tutto.

In genere, non esiste una struttura dati universalmente migliore di un'altra, o una struttura dati imprescindibile per un problema più che per un altro; è importante, invece, conoscere al meglio tutte le strutture dati fondamentali, e saper decidere sul momento quale convenga utilizzare. Progettare un buon algoritmo implica sempre anche una scelta efficace della struttura dati.
___
Un algoritmo deve produrre un *output* in un **tempo finito e ragionevole**, preferibilmente il più corto possibile.

Nello studio e progettazione di un algoritmo, dunque, un aspetto fondamentale è la sua **efficienza**, ossia la quantificazione delle sue esigenze in termini di **tempi di esecuzione** e di **memoria richiesta**. Per confrontare due algoritmi che risolvono uno stesso problema, è fondamentale conoscerne questi due parametri, e saper così discernere quale dei due sia il più efficiente nella risoluzione di tale problema. 

Per indicare al meglio i parametri che indicano l'efficienza di un algoritmo, si definisce il concetto di "**costo computazionale**", che dipende dunque principalmente dal numero di operazioni elementari eseguite, dal tempo necessario per eseguirle, e dalla quantità di memoria necessaria (in funzione della dimensione dell'*input*).
___
Un algoritmo è uno dei metodi più comuni e basilari di applicazione di "***problem-solving***", ossia dell'attività consistente nel raggiungere una soluzione a partire da una situazione problematica iniziale.

Un buon approccio al *problem-solving* segue, in genere, i seguenti passaggi:
- **analizzare il problema** al meglio, studiando la situazione iniziale e identificando con precisione il problema stesso;
- **esplorare tutti gli approcci possibili**, teorizzando possibili metodi di risoluzione tra quelli conosciuti;
- **selezionare un approccio**, tra quelli trovati, che si ritiene più efficiente o adatto al problema considerato;
- **definire un algoritmo risolutivo**, identificando i dati a disposizione e progettando la sequenza dei vari passi elementari di cui esso è composto;
- **riflettere criticamente** e **testare l'algoritmo creato**, sia a livello di funzionalità che di efficienza.

In questo corso, si affronteranno principalmente "**problemi computazionali**", ossia problemi che richiedono di descrivere in modo automatico una specifica relazione tra un insieme di *input* e il corrispondente insieme di *output*. In questo contesto, un algoritmo è **corretto** se per ogni *input* (o per ogni "**istanza**" del problema) viene prodotto l'*output* corretto.

È possibile individuare delle macro-categorie di problemi computazionali, le più comuni delle quali sono:
- **problemi di decisione**, cioè problemi per cui la soluzione, ad ogni istanza, può essere "vero" o "falso";
- **problemi di ricerca**, cioè problemi per cui la soluzione consiste nell'individuamento di un elemento che soddisfi le richieste del problema;
- **problemi di enumerazione**, cioè problemi che richiedono di elencare tutte le soluzioni ammissibili;
- **problemi di verifica**, cioè problemi in cui l'*input* consiste non solo da un'istanza del problema ma anche da una possibile soluzione (detta "**certificato**), e in cui si chiede di verificare che il certificato sia effettivamente una soluzione ammissibile;
- **problemi di ottimizzazione**, cioè problemi per cui è definita anche una funzione costo/vantaggio, e in cui è necessario scegliere, tra tutte le soluzioni ammissibili, quella con il rateo costo/vantaggio più basso o più alto.
___
Per rendere un algoritmo facilmente comprensibile per tutti, è necessario utilizzare una descrizione che possiamo chiamare "**pseudocodice**". Si tratta di una descrizione il più formale possibile, e generalmente indipendente dal linguaggio che si intende usare concretamente per implementare l'algoritmo.