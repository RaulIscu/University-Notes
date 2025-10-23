I **file** sono costituiti, a livello basilare, da blocchi di bit consecutivi da leggere insieme; possono essere di testo o binari, memorizzati nella memoria di massa o in rete, e sono organizzati tendenzialmente in una struttura di file e cartelle chiamata anche "**directory ad albero**": una cartella può contenere file oppure altre cartelle, che a loro volta possono contenere file e altre cartelle, e così via.

## Aprire e chiudere un file in Python

In Python, per leggere e scrivere un file bisogna prima di tutto **aprirlo**, ovvero chiedere al sistema operativo di interagire con la memoria di massa per rendere disponibili i dati contenuti all'interno del file desiderato. Per interagire con il cosiddetto "file-system", su Python si utilizza la funzione **`open(filename, mode, encoding)`**.

Analizziamo i diversi parametri inseriti nella funzione considerata. Partendo dal primo, **`filename: str`** rappresenta il **percorso del file da aprire**, che viene letto dalla directory corrente (ad esempio, `"file.txt"` viene cercato nella directory corrente) o da un altro punto del file system se si indica il percorso che ne individua la posizione (ad esempio, `"/usr/bin/python"` viene cercato nella directory `usr/bin` all'interno della directory corrente).

Abbiamo poi **`mode: str`**, che rappresenta la **modalità di apertura del file**; è composta da due caratteri, di cui il primo indica lo scopo dell'apertura e il secondo indica "come interpretare" il file in questione. In particolare, il primo carattere può essere scelto tra i seguenti:
- **`r`**, ossia "**read**", che indica che il file dovrà essere aperto per la **sola lettura del suo contenuto** (viene utilizzato questo carattere di default);
- **`w`**, ossia "**write**", che indica che si vuole **sovrascrivere il contenuto del file**, e che porterà alla creazione del file indicato nel `filename` in caso esso non esista;
- **`a`**, ossia "**append**", che indica che si vuole **aggiungere qualcosa alla fine del file**, e che porterà alla creazione del file indicato nel `filename` in caso esso non esista;
- **`x`**, ossia "**exclusive**", che indica che si vuole **creare un nuovo file** con il nome specificato nel `filename` (in caso il file esista già, verrà sollevato un errore).

Per quanto riguarda il secondo carattere, si hanno due possibili alternative:
- **`t`**, che porta all'interpretazione del file specificato come **file di testo** (viene utilizzato questo carattere come default);
- **`b`**, che porta all'interpretazione del file specificato come **file binario**.

 Infine, abbiamo il parametro opzionale **`encoding: str`**, che indica la **codifica dell'eventuale file di testo considerato**. Alcuni esempi sono **`utf-8`** per l'Unicode, **`latin`** per la Latin, **`ascii`** per l'ASCII, **`cp1252`** per quella utilizzata di default da Windows, e così via.

Per comprendere meglio, analizziamo i seguenti due esempi:

```
open("file.txt", "w")

open("/dir/photo.png", "rb")
```

Nella prima chiamata alla funzione `open`, verrà aperto il file `file.txt` presente nella directory corrente, interpretandolo come file di testo e con l'intento di scriverci qualcosa; invece, nella seconda chiamata, verrà aperto il file `photo.png` nella directory `dir` all'interno di quella corrente, interpretandolo come file binario e con l'intento di sola lettura.

Una volta aperto e manipolato un file, esso dovrà essere chiuso: in questo modo potranno essere rilasciate le strutture dati del sistema operativo, liberando memoria, e verranno completate le eventuali scritture del file. La **chiusura di un file** può essere effettuata mediante la funzione **`var_file.close()`**; alternativamente, si potrà utilizzare la keyword **`with`**, che chiuderà automaticamente il file dopo che sarà finita l'esecuzione del blocco di codice riguardante quest'ultimo. Generalmente, `with` viene utilizzato nel seguente modo:

```
with open(filename, mode, encoding) as var:
	...
```
___
## Leggere un file in Python

Per **leggere il contenuto di un file**, potranno essere utili le seguenti funzioni:
• **`file.read()`**, che permette di leggerne tutto il contenuto (non inserendo alcun argomento) o una parte (ad esempio, lavorando con file di testo, si può specificare il numero di caratteri da leggere come argomento);
• **`file.readline()`**, che permette di leggere una riga da un file di testo;
• **`file.readlines()`**, che permette di leggere tutte le righe da un file di testo;
• **`file.close()`**, per chiudere il file, finire di scriverlo su disco e rilasciare la memoria usata.

Nella lettura di un file, può capitare di arrivarne alla fine e di voler tornare al suo inizio, o a un qualsiasi punto generico del file stesso. Per fare ciò, si utilizza la funzione **`file.seek()`**: se come argomento di questa funzione si utilizza `0`, la lettura del file ripartirà dall'inizio dello stesso. Inoltre, un file di testo può essere visto anche come un "generatore di righe"; ad esempio, il codice:

```
with open("file.txt") as f:
	for riga in f:
		print(riga)
```

darà come risultato le righe del file di testo considerato una ad una.
___
## Scrivere un file in Python

Per scrivere in un file, si utilizza la funzione **`file.write()`**, o in alternativa la funzione **`print()` con l'aggiunta del parametro `file`**:

```
with open(filename, mode = 'w') as f:
	f.write(stringa_o_sequenza_di_byte)

with open(filename, mode = 'w') as f:
	print(cose_da_stampare, file = f)
```
___
## Alcuni file particolari: JSON, YAML

Ci sono alcuni tipi di file particolari, utilizzati principalmente su Internet e per codificare strutture dati: infatti, per l'interazione tra, ad esempio, pagine web e server, è utile avere dei file che rendano semplificata e più immediata tale interazione. Ci sono vari formati importanti e ampiamente utilizzati; in questo capitolo, approfondiremo due di questi, ossia **JSON** e **YAML**.

##### JSON

Un file **`.json`** ("**JavaScript Object Notation**") può essere definito come un file di testo con sintassi semplificata, utilizzato per rappresentare elementi semplici come dizionari, liste, interi, numeri a virgola mobile, stringhe o booleani (sono assenti strutture più "complesse", come le tuple). Questo tipo di file viene usato frequentemente nello scambio dati con un server.

Nel lavorare con un file `.json`, è importante tenere a mente una serie di regole:
- non si possono inserire commenti;
- non si può aggiungere una virgola in fondo a una lista o a un dizionario;
- non si possono utilizzare tuple in maniera diretta;
- nei dizionari, si possono usare solo chiavi "semplici" (`int`, `float`, `str`, `bool`, `None`);
- nel definire una stringa, si possono usare solo i doppi apici (`""`) e non i singoli apici (`''`)
- il valore `None` diventa **`null`**, mentre i booleani `True` e `False` vengono scritti con lettere minuscole.

Per utilizzare un file `.json`, lo si apre come un file di testo e se ne decodifica il contenuto, rendendolo nelle strutture dati tipiche di Python. Per lavorare con un file `.json` in Python, è opportuno importare la libreria **`json`**. Vediamo un esempio:

```
import json

with open("api.github.com.json") as f:
	api = json.load(f)
```

Con la funzione **`json.load()`**, è possibile leggere il contenuto del file e decodificarlo nelle strutture dati di Python corrispondenti. In alternativa, se si vuole scrivere nel file, si può implementare la funzione **`json.dump(oggetto, file)`**, che come primo argomento prende l'`oggetto` da salvare nel file, e come secondo argomento il `file` in cui si vuole scrivere, che deve quindi essere aperto in modalità scrittura.
___
#### YAML

Un altro file importante per rappresentare dati nidificati in maniera semplice e leggibile è il file **`.yaml`** ("**Yet Another Markup Language**"), in cui si possono inserire dizionari (inserendo una coppia `chiave : valore` per riga), liste (inserendo i valori su righe diverse, e ciascuno preceduto da `-`), dati semplici (`bool`, `int`, `float`, `None` e stringhe) e documenti multipli.

Per lavorare con i file `.yaml`, conviene sempre importare la libreria **`yaml`**, che include funzioni come:
- **`yaml.dump(oggetto, file)`**, che funziona in modo analogo a `json.dump()`;
- **`yaml.safe_load(file)`**, che permette non solo di leggere un *file* ma anche di codificare una stringa in formato `.yaml`.

Un esempio di utilizzo della funzione `yaml.safe_load()` può essere il seguente:

```
testo = """
	none: [~, null]
	bool: [true, false, on, off]
	int: 42
	float: 3.14159
	list:
		- LITE
		- RES_ACID
		- SUS_DEXT
	dict:
		hp: 13
		sp: 5
"""
yaml.safe_load(testo)
```

che restituirà:

```
{'none': [None, None],
 'bool': [True, False, True, False],
 'int': 42,
 'float': 3.14159,
 'list': ['LITE', 'RES_ACID', 'SUS_DEXT'],
 'dict': {'hp': 13, 'sp': 5}}
```
___
