Le **funzioni** sono definibili come **parti di programma riutilizzabili** all’occorrenza, chiamando la funzione con il nome che le è stato assegnato ed, eventualmente, con annessi degli **argomenti** su cui la funzione lavorerà. Per definire una funzione, si usa la seguente sintassi:

```
def nome_della_funzione(argomenti):
	# ISTRUZIONI
```

Il corpo di codice che rappresenta le istruzioni interne alla funzione vanno indentate a destra rispetto alla riga di definizione, costituendo un blocco unico; questo codice viene eseguito sequenzialmente, riga per riga.

La dicitura **`argomento`** prende il posto degli eventuali dati che vanno dati in input alla funzione (è possibile avere una funzione che accetti uno, più o nessun argomento) in modo da ottenere un risultato, ossia ciò che la funzione restituisce dopo aver eseguito il suo blocco di codice sull’argomento considerato. Un dettaglio importante da ricordare, nella definizione di una funzione, è che eventuali variabili definite all’interno del corpo di una funzione saranno disponibili esclusivamente all’interno della stessa.

L’istruzione **`return`** viene utilizzata, una volta terminate le operazioni svolte dalla funzione, per restituire il risultato di tali operazioni. Inoltre, similmente a **`break`**, permette di uscire da un ciclo, o dall'esecuzione di una funzione, prima che esso sia effettivamente terminato. Le variabili locali create all’interno di una funzione, dunque, vengono eliminate non solo al completamento della funzione stessa, ma anche in caso di `return`. Se nella definizione di una funzione non viene inserita alcuna istruzione `return`, essa risulterà in un valore **`None`**: dunque, se in fase di debug il programma riscontra un errore `NoneType`, sarà opportuno controllare le varie funzioni definite per aggiungere eventuali `return` dimenticati.

## Funzioni ricorsive


___
## Espressioni lambda


___