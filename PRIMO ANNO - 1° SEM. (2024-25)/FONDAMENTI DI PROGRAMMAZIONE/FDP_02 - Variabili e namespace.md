In Python, a un livello di base, le **variabili** funzionano allo stesso modo di altri linguaggi. Definire una variabile vuol dire **creare un "contenitore"** per un determinato dato, e definire una parola che nel programma indica proprio questo contenitore, e di conseguenza uno spazio di memoria ben preciso, destinato a contenere tale dato. Esse sono dunque fondamentali per nominare, richiamare, e manipolare qualsiasi dato all'interno di un programma. Creare una variabile, e soprattutto associare un dato a tale variabile, avviene con un procedimento definito "**assegnazione**", e a livello di codice si esegue nel modo seguente:

```
nome_variabile = dato
```

A differenza di altri linguaggi, in Python **non c'è un modo per dichiarare una variabile** senza assegnare un dato ad essa: una variabile è creata esclusivamente nel momento in cui avviene un'assegnazione. 

L'assegnazione di una variabile, seppur semplice e immediata, va comunque attuata con attenzione, soprattutto dal punto di vista della chiarezza: è importante, infatti, **definire una variabile con un nome chiaro ed esplicativo**, che permetta di capire immediatamente quale sia lo scopo della variabile considerata, o cosa ci si può aspettare che essa contenga (del resto, questo consiglio è utile in qualsiasi linguaggio di programmazione, non solo in Python). 

Per quanto riguarda la **tipizzazione di una variabile**, l'intenzione di rendere Python un linguaggio accessibile e immediato da utilizzare si manifesta anche nella scelta di utilizzare la cosiddetta "**tipizzazione dinamica**", oltre al meccanismo della "**type inference**": la prima consiste in un meccanismo per cui una variabile generica può assumere diversi tipi a seconda del dato che le viene via via assegnato; la seconda, invece, è ciò che permette di non specificare necessariamente il tipo di una variabile quando la si definisce, lasciando invece all'interprete il compito di "prevedere" il tipo della variabile in base all'utilizzo e all'assegnazione.

In ogni caso, è possibile **"forzare" il tipo di una variabile**, o specificando il tipo previsto con una sintassi del genere:

```
x: int = 5
```

oppure tramite un meccanismo chiamato "**casting**" [APPROFONDIMENTO SUL CASTING]. In generale, è possibile **ottenere il tipo attuale di una variabile** tramite la funzione **`type()`**, che prenderà come argomento il nome della variabile di cui si vuole sapere il tipo.

## Assegnamenti multipli

Nella creazione delle variabili, per comodità, è possibile fare anche **più assegnamenti contemporaneamente** per più variabili, tramite quello che viene definito un "**assegnamento multiplo**". Per eseguire un assegnamento multiplo, si dovrà scrivere del codice del genere:

```
A, B, C = 1, 2, 3
```

che equivale alle istruzioni:

```
A = 1
B = 2
C = 3
```

Alternativamente, è possibile applicare una forma di assegnamento multiplo anche per **assegnare lo stesso dato a più variabili contemporaneamente**, come nel seguente esempio:

```
A = B = C = 1
```

L’assegnamento multiplo è uno strumento molto utile ed efficiente, non solo data la sua compattezza e rapidità di scrittura, ma anche in vista di contesti più specifici. Uno di questi è il cosiddetto "**unpacking**", che permette di assegnare comodamente a più variabili i dati contenuti all'interno di una lista o di una tupla:

```
l_num = [1, 2, 3]
A, B, C = l_num
```

L'esecuzione, ad esempio, del codice appena mostrato porta alla seguente assegnazione:

```
A = 1
B = 2
C = 3
```

È importante ricordare, nel contesto di un unpacking ma anche in generale nell'utilizzo dell'assegnamento multiplo, di prevedere un numero di variabili esattamente uguale al numero di dati che si stanno considerando, per evitare di incappare in errori.
___
## Convenzioni per nominare le variabili e namespace

I nomi ammessi come identificatori di variabili su Python devono rispettare **quattro precise condizioni** per essere validi:
- possono contenere **solo caratteri alfanumerici** o **trattini bassi** (```_```);
- **non possono iniziare con un numero**;
- **non possono contenere spazi**;
- **non possono corrispondere a keyword** di Python.

Per nomi di variabili composti da **più parole**, ci sono varie convenzioni utilizzabili tra cui:
- il "**camel case**", dove la prima parola si scrive con l'iniziale minuscola e tutte le parole successive con l'iniziale maiuscola (ad esempio, `myVariableName`);
- lo "**snake case**", dove tutte le parole sono scritte con l'iniziale minuscola e sono intervallate da trattini bassi (ad esempio, `my_variable_name`).

Tutti i nomi che rispettano queste condizioni, e quindi che vengono effettivamente utilizzati all’interno di Python, vengono immagazzinati in un cosiddetto "**namespace**", detto anche “tabella dei nomi”. Ci possono essere vari namespace all’interno di un programma Python, secondo una struttura "gerarchica" in cui uno contiene l'altro; in ordine di grandezza decrescente, troviamo:
- **namespace built-in**, il più comprensivo, che contiene tutte le funzioni e le variabili contemplate nell’interprete di Python;
- **namespace globale**, appartenente al programma principale, che contiene le variabili globali accessibili a tutte le funzioni del file, le funzioni e le classi definite all’interno di quest’ultimo, e i moduli e le librerie importati nel file;
- **namespace di modulo**, o **di libreria**, che contiene tutte le variabili, funzioni e classi definite nel modulo considerato, nonché eventuali ulteriori moduli importati da quest’ultimo;
- **namespace locale** a una determinata funzione in esecuzione, che contiene i nomi degli argomenti formali della funzione e le variabili locali definite all’interno della stessa.
  
Ogni volta che, all’interno di un programma, si vorrà utilizzare un nome, esso verrà cercato seguendo l’ordine di precedenza “LEGB”, ossia “**L**ocal **E**nclosing **G**lobal **B**uilt-in”; ciò implica che, ad esempio, **una variabile locale può “nascondere” una variabile globale con lo stesso nome**, dato che seguendo l'ordine di precedenza appena fornito essa verrà trovata per prima.
___