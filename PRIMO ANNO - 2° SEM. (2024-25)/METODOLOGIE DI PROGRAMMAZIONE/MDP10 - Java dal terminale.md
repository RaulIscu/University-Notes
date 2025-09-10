Java è un **linguaggio compilato**, dunque per poter essere eseguito deve prima passare per un **compilatore**, che legge il codice del file e, sfruttando vari strumenti, genera un eseguibile. È quest'ultimo ad essere, appunto, eseguito per ottenere il funzionamento del programma scritto.

Java dispone di un proprio compilatore, chiamato "**Java Compiler**", o **`javac`**.

## Come compilare ed eseguire un file .java da terminale

Per eseguire opportunamente un file `.java` dal **terminale**, ad esempio da Windows Powershell, dovremo innanzitutto **assicurarci di trovarci nella** cartella, o "**directory**", **apposita**, ossia quella contenente il file che ci interessa: per spostarci nella directory desiderata, su Windows, è possibile sfruttare il comando **`cd`** ("*current directory*") seguito dal nome della directory in cui si vuole entrare, ricordando che quest'ultima deve trovarsi nella directory in cui siamo situati attualmente. Per tornare, invece, in una directory precedente, basterà utilizzare il comando **`cd ..`**; se invece si vuole avere un elenco dei contenuti della directory attuale, si può utilizzare il comando **`dir`**.

Una volta all'interno della giusta directory, si potrà procedere a **compilare il programma** desiderato. Per fare ciò, occorrerà chiamare il compilatore di Java e indicargli il file che ci interessa, mediante il comando **`javac nomeDelFile.java`**.

Ora, se il passaggio precedente è stato completato senza intoppi, sarà possibile eseguire il programma. Per fare ciò, il comando che si dovrà eseguire è **`java nomeDelFile`**: inviando questo comando, si avrà eseguito con successo il programma precedentemente compilato.
___
## Passare degli argomenti da terminale

A volte, si vorranno dare delle informazioni o dei dati aggiuntivi a un programma nel momento in cui lo si eseguirà. Per fare ciò, è possibile passare dei "***command-line arguments***" al metodo **`main()`** del programma in questione.

I *command-line arguments* vengono passati al metodo `main()` al momento dell'esecuzione del programma. Per passarli a quest'ultimo, sarà sufficiente inserirli subito dopo il nome del programma che si vuole eseguire, come nel seguente esempio generico:

```
java nomeDelFile argomento0 argomento1 argomento2 ...
```

Accedere a questi argomenti dal codice è molto facile: infatti, i *command-line arguments*, una volta forniti, vengono conservati in un [[MDP14 - Strutture dati#Array|array]] di [[MDP08 - Stringhe|stringhe]] (**`String args[]`**), facilmente accessibili mediante l'indicizzazione di tale array (ad esempio, il primo dei *command-line arguments* si otterrà come `args[0]`, il secondo come `args[1]`, e così via).
___

