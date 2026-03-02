Il **file system** è una delle componenti più importanti, se non la più importante, di un calcolatore e del suo funzionamento. Concretamente, un file system è un'**organizzazione di un'area di memoria di massa**, generalmente basata su due concetti fondamentali:
- il "**file**";
- la "**directory**".

Mentre il primo rappresenta un **insieme effettivo di dati**, il secondo è più che altro un **contenitore**, che può contenere sia file che altre directory. Un file system di questo tipo può essere formalizzato secondo una **struttura gerarchica ad albero**, in cui **solo le directory possono avere figli**, e dunque in cui **i file sono sempre foglie**. In particolare, si può effettuare una distinzione tra "**file regolari**" e "**file non regolari**": mentre i primi sono quelli a cui siamo abituati, ossia sequenze di bit conservate nell'area di memoria di competenza del file system considerato, i secondi hanno forme diverse e vengono utilizzati per scopi particolari, ad esempio per l'accesso di basso livello a periferiche o dispositivi vari.

Un singolo calcolatore, a seconda del caso e delle scelte architetturali, può supportare **uno o più file system**. Ad esempio, di default, **i sistemi Linux e Unix hanno un solo file system principale**, che ha come "directory radice" la directory **`/`**, spesso chiamata anche **`root`**: di conseguenza, tutti i file e le directory del file system saranno contenute nella cartella `/`.

Ricordiamo alcune **regole per la nomina di file e directory**. Infatti, all'interno di una stessa directory, è impossibile creare:
- due file con lo stesso nome;
- due directory con lo stesso nome;
- un file e una directory con lo stesso nome.

Inoltre, i nomi di file e directory sono **case-sensitive**, dunque due nomi che presentano gli stessi caratteri ma che variano in termini di lettere maiuscole o minuscole verranno considerati diversi.
## Il path

Ogni file e directory all'interno di un file system è raggiungibile seguendo un "**path**", ossia letteralmente un percorso, un cammino verso tale entità. Dato che tutto ciò che è contenuto in un file system è contenuto nella sua directory radice (nel nostro caso, `/`), di conseguenza **qualsiasi file o directory è raggiungibile seguendo un "path assoluto" che parte dalla cartella radice**. Ad esempio, il path:

```
/home/utente1/dir1/dir11/dir112/file.pdf
```

punta al file `file.pdf`, che è contenuto nella directory `dir112/`, che è contenuta a sua volta nella directory `dir11/`, e così via fino ad arrivare proprio alla directory radice `/`. Dato che capita spesso che i file e directory di interesse si trovino all'interno della cartella relativa all'utente loggato in quel momento, in molti casi si può **abbreviare la parte `/home/user` del path in `~`**, ad esempio:

```
~/dir1/dir11/dir112/file.pdf
```



[SLIDES: 02 - slide 7/10]
___
## Contenuto di una directory

[SLIDES: 02 - slide 11/16]
___
## Creazione di directory e file

[SLIDES: 02 - slide 17 - 18]
___



[recuperare la lezione di venerdì 27 febbraio]