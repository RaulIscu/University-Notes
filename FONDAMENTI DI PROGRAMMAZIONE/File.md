I ***file*** sono formati da blocchi di *bytes* consecutivi; possono essere di testo (.txt, .py) o binari (.png, .mp4, .mp3, .jpeg, ecc.), memorizzati nella memoria di massa (HD, SSD, DVD) o in rete, e sono organizzati in una struttura di "*directory* ad albero".
___
Per leggere e scrivere i *file* bisogna aprirli, ovvero chiedere al sistema operativo di preparare le strutture dati necessarie ad interagire con la
memoria di massa. Per interagire con il cosiddetto *file-system*, su Python si utilizza la libreria ```os``` e la funzione ```open```. Genericamente, dunque, un'interazione con un *file* in un codice Python è del tipo:

```
open(filename: str,
	 mode: str = 'rt',
	 encoding: str = <encoding>)
```

Analizziamo i diversi parametri inseriti nella funzione precedente:
- **```filename```** è una stringa che indica il percorso del *file* da aprire, che di default viene letto dalla *directory* corrente, oppure da un altro punto del *filesystem* se si indica il percorso che ne individua la posizione (ad esempio: ```"paperino.txt"``` viene cercato nella *directory* corrente, mentre ```"/usr/bin/python"``` viene cercato nella *directory* `usr/bin` all'interno della *directory* corrente); [PATH]
- **```mode```** è una stringa che indica in che modo il *file* viene aperto; inizia con un carattere che indica la "intenzione" con cui si apre il *file* (```r``` (*read*) solo per leggerne il contenuto (viene utilizzato questo carattere di default), ```w``` (*write*) per scriverci dentro, ```a``` (*append*) per aggiungere nuovo contenuto alla fine del *file*, ```x``` (*exclusive*) crea un nuovo *file* e da errore se esiste già), che è seguito da un altro carattere che indica in che modo viene aperto il *file* considerato (con ```t``` il *file* viene aperto in modo testo, e il contenuto viene interpretato come caratteri (viene utilizzato questo carattere di default), mentre con ```b``` il *file* viene aperto in modo binario (il contenuto non viene interpretato automaticamente);
- **```encoding```** è una stringa che indica come viene codificato o decodificato un *file* di testo (alcuni esempi sono ```utf-8``` per la codifica Unicode, ```latin``` per la codifica Latin, ```ascii``` per la codifica Ascii, ```cp1252``` per la codifica usata di default da Windows); in un *file* di testo, i caratteri sono codificati come numeri, e il parametro ```encoding``` risulta quindi fondamentale nel riconoscere in quale delle diverse codifiche esistenti lavora il *file* considerato; in particolare, Python usa ```utf-8```, ma i file possono provenire da sistemi operativi diversi (Windows, Unix, MacOS, ecc.).

In generale, lavorando con dei *file*, per semplicità conviene assegnare la funzione ```open()``` (e quindi, indirettamente, il *file* stesso) a una variabile (ad esempio: ```A = open(filename, mode, encoding)```) Una volta aperto e manipolato un *file*, esso dovrà essere chiuso: in questo modo potranno essere rilasciate le strutture dati del sistema operativo, liberando memoria, e verranno completate le scritture dei *file*. La chiusura di un *file* può essere effettuata mediante la funzione ```variabileOpen.close()```; alternativamente, si potrà utilizzare ```with```, che chiuderà automaticamente il *file* dopo che sarà finito il codice riguardante quest'ultimo. Genericamente, ```with``` viene utilizzato nel seguente modo:

```
with open(filename, mode, encoding) as variabile:
	blocco di codice
```
___
Per leggere il contenuto di un *file* ci servono le funzioni:
• **```file.read()```**, che permette di leggerne tutto il contenuto (o una parte);
• **```file.readline()```**, che permette di leggere una riga da un *file* di testo;
• **```file.readlines()```**, che permette di leggere tutte le righe da un *file* di testo;
• **```file.close()```**, per chiudere il *file*, finire di scriverlo su disco e rilasciare la memoria usata.

Nella lettura di un *file*, può capitare di arrivarne alla fine e di voler tornare al suo inizio, o a un qualsiasi punto generico del *file* stesso. Per fare ciò, si utilizza la funzione **`file.seek()`**: se come argomento di questa funzione si utilizza 0, la lettura del *file* ripartirà dall'inizio dello stesso.

Un *file* di testo può essere visto anche come un "generatore di righe"; ad esempio, il codice:
```
with open('topolino.txt', encoding='utf8') as F:
	for riga in F:
		print(riga)
```
darà come risultato le righe del *file* di testo considerato una ad una.
___
Per scrivere in un *file*, si utilizza la funzione **`file.write()`**, o in alternativa la funzione `print()` con l'aggiunta del parametro `file`:
```
with open(filename, mode = 'w', encoding = 'utf8') as F:
	F.write(stringa_o_sequenza_di_byte)

with open(filename, mode = 'w', encoding = 'utf8') as F:
	print(cose_da_stampare, file = F)
```
___
Supponiamo di voler esaminare dei *file* di testo all'interno di una *directory*, e di voler sapere in quale dei *file* presenti si parla maggiormente di un certo argomento, o compare maggiormente una certa parola: innanzitutto, per semplificare l'operazione, risulterà molto utile distinguere le parole, quindi sequenze di lettere, da altri caratteri non alfabetici, tra cui segni di interpunzione, che potrebbero invece risultare utili come separatori delle parole stesse; in più, per uniformare il tutto, potremmo rendere tutti i caratteri alfabetici minuscoli.

Per separare le parole ed eliminare i caratteri non alfabetici in una singola operazione, è possibile implementare un ciclo `for` come il seguente:
```
for carattere in testo:
	if not carattere.isalpha():
		testo = testo.replace(carattere, "")
return testo
```
Seppur porti a termine il suo compito, si nota facilmente che non è un metodo particolarmente rapido o efficiente. In alternativa, invece, si può utilizzare la funzione **`str.translate()`**, che permette di rimpiazzare immediatamente tutti i caratteri indicati con una qualsiasi stringa. Tale funzione, per fare ciò, richiede in ingresso un dizionario formato da coppie "codice del carattere da rimpiazzare : stringa con cui rimpiazzarlo", che possono essere composte manualmente (mediante la funzione `ord()`) o con la funzione `str.maketrans()`, a cui va dato in input un dizionario formato da coppie "carattere : stringa". Un esempio di utilizzo di queste due funzioni può essere:
```
nonalfa = "!\"£$%&/()"
D = str.maketrans(dict.fromkeys(nonalfa, ""))
T = testo.translate(D)
```
A questo punto, per trovare parole o argomenti specifici, dobbiamo tenere a mente un "problema": cercare semplicemente le parole più frequenti di un *file* probabilmente non restituirà il risultato sperato, in quanto nella quasi totalità dei casi queste saranno parole comuni, verbi ausiliari, preposizioni e altri costrutti di base del linguaggio, molto frequenti ma non significative. Se si vogliono cercare parole "interessanti", dunque, occorrerà cercare parole frequenti in un determinato *file* (o gruppo di *file*), ma presenti in relativamente pochi *file*; si tratta quindi di calcolare due parametri:
- ***Term Frequency*** (**TF**), ossia la frequenza percentuale della parola in un *file*;
- ***Inverse Document Frequency*** (**IDF**), ossia la percentuale di *file* che la contiene.

Per ottenere la TF, bisognerà, per ciascun *file*, contare le parole che ci interessano e dividere il risultato per il numero totale di parole. Per ottenere la IDF, invece, si parte dalla ***Document Frequency*** (DF), che andrà ottenuta contando il numero di *file* in cui è presente la parola e dividerlo per il numero totale di *file*; a questo punto, la IDF si ottiene con il logaritmo dell'inverso della DF. Infatti, meno *file* contengono la parola cercata, più è grande l'inverso della DF, e quindi il logaritmo e la IDF stessa, e viceversa.

Ora, si è in possesso di tutti i dati necessari per stabilire con certezza quale dei *file* considerati è più importante rispetto a una determinata *query*: per ciascun *file*, e per ciascuna parola della *query*, misuro la TF e la moltiplico per la IDF della parola; sommando i valori ottenuti per ogni parola della *query*, si ottiene quanto il *file* considerato è "utile" in relazione alla *query*.
___
Ci sono alcuni tipi di *file* particolari, utilizzati principalmente su Internet e per codificare strutture dati: infatti, per l'interazione tra, ad esempio, pagine *web* e *server*, è utile avere dei *file* che rendano semplificata e più immediata tale interazione.

Uno di questi è il *file* **`.json`** ("*JavaScript Object Notation*"), che si può definire come un *file* di testo con sintassi semplificata, utilizzato per rappresentare elementi semplici come dizionari, liste, interi, *float*, stringhe o booleani (sono assenti strutture più "complesse", come le tuple). Questo tipo di *file* viene usato frequentemente nello scambio dati con un *server*.

Nel lavorare con un *file* `.json`, è importante tenere a mente una serie di regole:
- non si possono inserire commenti;
- non si può aggiungere una virgola in fondo a una lista o a un dizionario;
- non si possono utilizzare tuple in maniera diretta;
- nei dizionari, si possono usare solo chiavi "semplici" (`int`, `float`, `str`, `bool`, `None`);
- nel definire una stringa, si possono usare solo i doppi apici (`""`) e non i singoli apici (`''`)
- il valore `None` diventa **`null`**, mentre i booleani `True` e `False` vengono scritti completamente con lettere minuscole.

Per utilizzare un *file* `.json`, lo si apre come un *file* di testo e se ne decodifica il contenuto, rendendolo nelle strutture dati tipiche di Python. Per lavorare con un *file* `.json` in Python, è opportuno importare la libreria **`json`**. Vediamo un esempio:
```
import json
with open('api.github.com.json') as F:
	api = json.load(F)
```
Con la funzione **`json.load()`**, è possibile leggere il contenuto del *file* e decodificarlo nelle strutture dati di Python corrispondenti. In alternativa, se si vuole scrivere nel *file*, si può implementare la funzione **`json.dump(oggetto, file)`**, che come primo argomento prende la struttura da salvare nel *file*, e come secondo argomento il *file* in cui si vuole scrivere, che deve quindi essere aperto in modalità scrittura.

Ci sono altre due funzioni abbastanza utili ma più specifiche:
- **`json.loads()`**, che converte una stringa qualsiasi, presa in argomento, nella struttura dati corrispondente in formato `.json`;
- **`json.dumps()`**, che converte una struttura dati qualsiasi, presa in argomento, nella stringa corrispondente in formato `.json` (è possibile inserire un secondo argomento, `indent = int`, che produce un'indentazione di `int` spazi).
___
Un altro *file* importante per rappresentare dati nidificati in maniera semplice e leggibile è il *file* **`.yaml`** ("*Yet Another Markup Language*"), in cui si possono inserire dizionari (inserendo una coppia "chiave : valore" per riga), liste (inserendo i valori su righe diverse, e ciascuno preceduto da `-`), dati semplici (booleani, `int`, `float`, `None` e stringhe) e documenti multipli.

Anche per i *file* `.yaml` conviene sempre importare la libreria **`yaml`**, che include funzioni come:
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
[LEGGERE PAGINE O FILE DA INTERNET: FINE LEZIONE 10]