I ***file*** sono formati da blocchi di *bytes* consecutivi; possono essere di testo (.txt, .py) o binari (.png, .mp4, .mp3, .jpeg, ecc.), memorizzati nella memoria di massa (HD, SSD, DVD) o in rete, e sono organizzati in una struttura di "*directory* ad albero".

Per leggere e scrivere i *file* bisogna aprirli, ovvero chiedere al sistema operativo di preparare le strutture dati necessarie ad interagire con la
memoria di massa. Per interagire con il cosiddetto *file-system*, su Python si utilizza la libreria ```os``` e la funzione ```open```. Genericamente, dunque, un'interazione con un *file* in un codice Python è del tipo:

```
open(filename: str,
	 mode: str = 'rt',
	 encoding: str = <encoding>)
```

Analizziamo i diversi parametri inseriti nella funzione precedente:
- **```filename```** è una stringa che indica il percorso del *file* da aprire, che di default viene letto dalla *directory* corrente, oppure da un altro punto del *filesystem* se si indica il percorso che ne individua la posizione (ad esempio: ```"paperino.txt"``` viene cercato nella *directory* corrente, mentre ```"/usr/bin/python"``` viene cercato nella *directory* /usr/bin all'interno della *directory* corrente); [PATH]
- **```mode```** è una stringa che indica in che modo il *file* viene aperto; inizia con un carattere che indica la "intenzione" con cui si apre il *file* (```r``` (*read*) solo per leggerne il contenuto (viene utilizzato questo carattere di default), ```w``` (*write*) per scriverci dentro, ```a``` (*append*) per aggiungere nuovo contenuto alla fine del *file*, ```x``` (*exclusive*) crea un nuovo *file* e da errore se esiste già), che è seguito da un altro carattere che indica in che modo viene aperto il *file* considerato (con ```t``` il *file* viene aperto in modo testo, e il contenuto viene interpretato come caratteri (viene utilizzato questo carattere di default), mentre con ```b``` il *file* viene aperto in modo binario (il contenuto non viene interpretato automaticamente);
- **```encoding```** è una stringa che indica come viene codificato o decodificato un *file* di testo (alcuni esempi sono ```utf-8``` per la codifica Unicode, ```latin``` per la codifica Latin, ```ascii``` per la codifica Ascii, ```cp1252``` per la codifica usata di default da Windows).

In generale, lavorando con dei *file*, per semplicità conviene assegnare la funzione ```open()``` (e quindi, indirettamente, il *file* stesso) a una variabile (ad esempio: ```A = open(filename, mode, encoding)```) Una volta aperto e manipolato un *file*, esso dovrà essere chiuso: in questo modo potranno essere rilasciate le strutture dati del sistema operativo, liberando memoria, e verranno completate le scritture dei *file*. La chiusura di un *file* può essere effettuata mediante la funzione ```variabileOpen.close()```; alternativamente, si potrà utilizzare ```with```, che chiuderà automaticamente il *file* dopo che sarà finito il codice riguardante quest'ultimo. Genericamente, ```with``` viene utilizzato nel seguente modo:

```
with open(filename, mode, encoding) as variabile:
	blocco di codice
```
[SEEK]

Per leggere il contenuto di un *file* ci servono le funzioni:
• **```file.read()```**, che permette di leggerne tutto il contenuto (o una parte);
• **```file.readline()```**, che permette di leggere una riga da un *file* di testo;
• **```file.readlines()```**, che permette di leggere tutte le righe da un *file* di testo;
• **```file.close()```**, per chiudere il *file*, finire di scriverlo su disco e rilasciare la memoria usata.

Un *file* di testo può essere visto anche come un "generatore di righe"; ad esempio, il codice:
```
with open('topolino.txt', encoding='utf8') as F:
	for riga in F:
		print(riga)
```
darà come risultato le righe del *file* di testo considerato una ad una.

In un *file* di testo, i caratteri sono codificati come numeri, e il parametro ```encoding``` risulta quindi fondamentale nel riconoscere in quale delle diverse codifiche esistenti lavora il *file* considerato. In particolare, Python usa ```utf-8```, ma i file possono provenire da sistemi operativi diversi (Windows, Unix, MacOS, ecc.).


