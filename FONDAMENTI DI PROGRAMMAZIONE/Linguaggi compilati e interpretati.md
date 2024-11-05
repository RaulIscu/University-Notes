Nei **linguaggi compilati** (come C, C++, Objective C, Swift, Pascal, Delphi, Rust e “Java”), la programmazione avviene in 3 fasi:
- **compilazione**, in cui il programma analizza un file di testo che contiene tutte le istruzioni, e avviene automaticamente la “generazione assembly” (o “formato intermedio"), creando istruzioni che hanno un diretto collegamento con il processore, che procede a generare del “codice oggetto”;
- ***linking***, in cui si ottiene il programma eseguibile (.exe) sommando il codice oggetto alle librerie necessarie;
- **esecuzione**, in cui si carica il file eseguibile nella memoria e si esegue partendo da un indirizzo fissato in memoria.

Le fasi di compilazione e *linking* vanno a formare il cosiddetto ***compile time***, mentre l’esecuzione viene anche detta ***run time***.

Tra gli aspetti positivi, i linguaggi compilati sono capaci di un’esecuzione estremamente veloce, e permettono di proteggere il codice iniziale da modifiche o accessi indesiderati; tuttavia, ogni modifica, benché minima, del programma richiede la ricompilazione dello stesso, e quindi anche l’eventuale ridistribuzione.

Nei **linguaggi interpretati** (come Basic, JavaScript, Python, Perl e PHP), il programma analizza le istruzioni riga per riga, eseguendo e richiamando gradualmente ogni pezzo di codice, semplificando così il lavoro del sistema operativo.

Tra gli aspetti positivi, i linguaggi interpretati sono facili da modificare e da imparare, ottimizzati, leggibili; tuttavia, gli eseguibili che ne risultano sono in genere facilmente modificabili, e tali linguaggi sono in media 5-10 volte più lenti del corrispondente linguaggio compilato.