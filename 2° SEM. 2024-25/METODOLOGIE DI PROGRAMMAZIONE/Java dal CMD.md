Java è un [[Linguaggi compilati e interpretati|linguaggio compilato]], dunque per poter essere eseguito deve prima passare in un **compilatore**, che legge il codice del *file* e, sfruttando anche delle librerie, genera un eseguibile (`.exe`). È questo *file* eseguibile ad essere, appunto, eseguito per ottenere il funzionamento del programma scritto.

Java dispone di un proprio compilatore, chiamato "**Java Compiler**", o `javac`.
___
Vediamo, a questo punto, come eseguire opportunamente un file `.java` a un livello di base, sfruttando un *command prompt* come Windows Powershell. Innanzitutto, dovremo **assicurarci di trovarci nella** cartella, o ***directory***, **apposita**, ossia quella contenente il *file* che ci interessa: per spostarci nella *directory* desiderata, su Windows, è possibile sfruttare il comando `cd` (*current directory*) seguito dal nome della *directory* in cui si vuole entrare, ricordando che quest'ultima deve trovarsi nella *directory* in cui siamo situati nel presente. Per tornare in una *directory* precedente, inserire come "nome" della *directory* `..`; se invece si vuole avere un elenco dei contenuti della *directory* attuale, conviene utilizzare il comando `dir`.

Una volta all'interno della giusta *directory*, si potrà procedere a **compilare il programma** desiderato. Per fare ciò, occorrerà chiamare il compilatore di Java e indicargli il *file* che ci interessa, mediante il comando `javac nomeDelFile.java`.

Ora, se il passaggio precedente è stato completato senza intoppi, sarà possibile eseguire il programma. A questo scopo, il comando che si vorrà scrivere è `java nomeDelFile`: inviando questo comando, si avrà eseguito con successo il programma precedentemente compilato.


