Testing = automatizzare la verifica della correttezza del codice, aumenta la probabilità di correttezza del codice e permette il rilevamento di errori senza necessariamente "prevederli" in modo concreto.

Caratteristiche di un'unità di testing:
- ripetibile (permettere automatizzazione);
- semplice (analizzare un comportamento specifico);
- espressivo (palesare chiaramente l'eventuale errore o il comportamento previsto);
- robusto.

Tipologie di testing:
- customer testing;
- unit testing;
- integration/interaction testing;
- altro.

UNIT TESTING
È una procedura usata per controllare che ogni singola unità del codice sorgente si comporti correttamente. Un'unità è la più piccola paerte collaudabile di un'applicazione (solitamente un singolo metdoo di una classe). I test devono essere indipendenti tra loro, in quanto ogni unità va testata in isolamento.

Per fare il testing di un metodo, sfruttare gli input più importanti non tutti.

JUNIT
L'obiettivo della libreria JUnit è quello di fornire al programmatore un ambiente che permette di sapere in ogni momento e con poco sforzo se il proprio programma ha sueprato i test. È utile per testare singole parti del software come metodi o classi, è integrato in Eclipse. Utilizza le seguenti annotazioni:
- @Test, per i metodi che definiscono i test;
- @Before, per i metodi che debono essere eseguiti prima di ogni unit test (utile per l'inizializzazione delle variabili);
- @After, per i metodi che devono essere eseguiti dopo ogni unit test (utile per eliminare file creati durante il test);
- @

[VEDERE SLIDE TESTING UNITARIO SAMORY]
[VEDERE TUTORIAL JUNIT]

