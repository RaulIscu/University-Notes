Definire una **variabile** vuol dire definire una parola che nel programma indica uno spazio di memoria ben preciso, un "contenitore", a cui viene associato un dato variabile. Esse sono dunque fondamentali per nominare, richiamare, e manipolare qualsiasi dato all'interno di un programma. La creazione di una variabile viene detta "**assegnazione**" di un dato a tale variabile, e si esegue nel modo seguente:
```
nomeVariabile = dato
```
L'assegnazione di una variabile è un processo, seppur semplice, da attuare con attenzione. Conviene, infatti, ricordarsi di assegnare a una variabile un nome chiaro e specifico, in modo da capire in maniera immediata a quale dato o tipo di dato si riferisce.

A differenza di altri linguaggi di programmazione, in Python una variabile non è necessariamente di un tipo specifico, e si può assegnare ad essa sostanzialmente qualsiasi classe di dato si voglia.
___
Nello stabilire delle variabili, è possibile fare più assegnamenti contemporaneamente per più variabili, ovvero un **assegnamento multiplo**:
```
A, B, C = 1, 2, 3 ===> A = 1, B = 2, C = 3
```
L’assegnamento multiplo è uno strumento molto utile ed efficiente, in quanto:
- permette di estrarre dati da strutture complesse senza dover ricordarne le posizioni;
- consente di scandire una lista di coppie prodotte da ```enumerate()``` o ```dizionario.items()```.
___
I nomi ammessi come identificatori di variabili su Python devono rispettare tre precise condizioni per essere validi:
- possono contenere solo caratteri alfanumerici o *underscore* (```_```);
- non possono iniziare con un numero;
- non possono contenere spazi.

Tutti i nomi che rispettano queste condizioni, e possono essere utilizzati all’interno di Python, vengono immagazzinati in un ***namespace***, o “tabella dei nomi”. Ci sono vari *namespace* all’interno di Python, uno dentro l’altro; in ordine di grandezza decrescente, troviamo:
- ***namespace built-in***, il più comprensivo, che contiene tutte le funzioni e le variabili presenti nell’interprete Python;
- ***namespace* globale**, appartenente al programma principale, che contiene le variabili globali accessibili a tutte le funzioni che le seguono nel file, le funzioni e le classi definite all’interno di quest’ultimo, e i moduli e le librerie importati nel file;
- ***namespace* di modulo**, o di libreria, che contiene tutte le variabili, funzioni e classi definite nel modulo considerato, nonché eventuali ulteriori moduli importati da quest’ultimo;
- ***namespace* locale** a una determinata funzione in esecuzione, che contiene i nomi degli argomenti formali della funzione e le variabili locali definite all’interno della stessa.
  
Ogni volta che, all’interno di un programma, si vorrà utilizzare un nome, esso verrà cercato seguendo l’ordine di precedenza “LEGB”, ossia “**L**ocal **E**nclosing **G**lobal **B**uilt-in”; ciò implica che, ad esempio, una variabile locale possa “nascondere” una variabile globale con lo stesso nome.