Le **stringhe** (**```str```**) sono dati più complessi di ```int``` o ```float```; è possibile pensare una stringa codificata in memoria come *array*, ossia come una sequenza di elementi uguali. Nel linguaggio Python, la stringa è una struttura dati di tipo **immutabile**: una volta creata una specifica stringa, essa non potrà essere “modificata” in sé.

Una qualsiasi stringa, per essere tale, deve essere delimitata da **apici** (*‘ ‘*) o **doppi apici** (*“ “*). Se si vuole scrivere una stringa di testo che contiene accapi, esse vanno delimitate da **tripli apici** (*''' '''* o *“”” “””*).

Ci sono varie azioni possibili che riguardano le stringhe, tra cui **```len(stringa)```**, che permette di ottenere la lunghezza (o il numero di caratteri) di una determinata stringa, e **```stringa[i]```**, che restituisce il carattere all’indice *i* di una determinata stringa.
> É infatti possibile “**indicizzare**” la stringa, e accedere in maniera secca a ciascun carattere (azione che viene definita *random access*; nel fare ciò, è importante ricordare che il primo carattere avrà indice *0*, il secondo *1* e così via. Inoltre, per individuare singoli caratteri si possono utilizzare anche numeri negativi: *-1* indica l’ultimo carattere della stringa, *-2* il penultimo e così via.

Da una stringa di partenza, inoltre, si può effettuare un’operazione di ***slicing***, usando la funzione **```stringa[i1:i2:inc]```** ed estraendo un sottoinsieme di caratteri che va dall’indice *i1* all’indice *i2* di una stringa. 
> **NB: quando viene indicato un intervallo di caratteri, l’estremo destro dell’intervallo non viene incluso nella selezione**

È possibile omettere il valore di *start* o di *end*: fare ciò restituirà, omettendo il valore di *end*, tutti i caratteri dall’indice indicato alla fine della stringa; omettendo il valore di *start*, tutti i caratteri dall’inizio della stringa all’indice indicato.

La sezione estratta non deve necessariamente essere formata da caratteri consecutivi: aggiungendo il parametro *inc* nella funzione, è possibile estrarre caratteri, all’interno dell’intervallo considerato, ogni gruppo di caratteri formato da un numero *inc* di caratteri. Si può anche “rovesciare” una stringa inserendo un incremento negativo (ad esempio, ```stringa[::-1]``` restituisce la stessa stringa ma letta al contrario).

Ci sono molte altre funzioni che possono essere utili nel lavorare con stringhe, tra cui:
- **```stringa.capitalize()```**, che “capitalizza” la stringa rendendone maiuscolo il primo carattere;
- **```stringa.count(elemento)```**, che conta quante volte un determinato elemento è presente nella stringa considerata;
- **```stringa.index(elemento)```**, che restituisce l’indice di inizio della prima occorrenza dell’elemento nella stringa considerata;
- **```stringa.isalnum()```**, che ritorna un valore ```True``` se tutti i caratteri della stringa sono alfanumerici;
- **```stringa.isalpha()```**, che ritorna un valore ```True``` se tutti i caratteri della stringa sono alfabetici;
- **```stringa.isspace()```**, che ritorna un valore ```True``` se tutti i caratteri della stringa sono spazi vuoti;
- **```stringa.join(elementi)```**, che crea una nuova stringa unendo all’interno di essa gli elementi iterabili, con *stringa* che rappresenta il separatore che verrà inserito all’interno della stringa tra i vari elementi;
- **```stringa.lower()```**, che converte la stringa considerata in una stringa equivalente ma composta esclusivamente da caratteri minuscoli;
- **```stringa.replace(old, new, count)```**, che sostituisce gli elementi *old* di una stringa con elementi *new*; il parametro *count*, opzionale, serve a specificare, quando presente, un numero preciso di occorrenze dell’elemento old da sostituire, mentre la sua assenza porterà alla sostituzione di tutte le occorrenze;
- **```stringa.split(sep, maxsplit)```**, che divide la stringa considerata in corrispondenza del separatore *sep* (in caso esso non sia inserito, verrà considerato come separatore lo spazio vuoto) e inserisce i vari frammenti in una lista; inserire il parametro *maxsplit* specificherà il numero di divisioni da fare;
- **```stringa.upper()```**, che converte la stringa considerata in una stringa equivalente ma composta esclusivamente da caratteri maiuscoli.

Inoltre, mediante la cosiddetta ***string interpolation***, è possibile costruire facilmente dei testi che contengono valori presi da variabili o calcolati con espressioni. Per fare ciò, basterà precedere la stringa con ```f``` (che sta per ```formatted```) e inserire i valori da interpolare tra parentesi graffe.

Qualsiasi testo scritto in un programma Python che viene preceduto da un cancelletto (```#```) viene considerato come commento, non come istruzione, e non verrà quindi interpretato da Python.