Alcune delle componenti fondamentali e più utili di un qualsiasi linguaggio di programmazione sono le "**istruzioni di controllo**", o **control statements**, delle istruzioni particolari che portano il programma a variare il suo comportamento e le sue azioni in base a particolari condizioni. In Python, i control statements possono essere divisi in **tre categorie** in base al loro funzionamento:
- le istruzioni di **selezione**, che scelgono diversi "percorsi" all'interno del programma in base al risultato di un espressione o allo stato di una variabile;
- le istruzioni di **iterazione**, che creano dei loop all'interno del programma;
- le istruzioni di **salto**, che permettono al programma di essere eseguito in maniera non-lineare.

Di seguito, verrà analizzata nel dettaglio ciascuna di queste categorie.

## Istruzioni di selezione

Le **istruzioni di selezione**, lavorando in Python, possono presentarsi principalmente in due forme: gli **if statements** e i **match statements**. Come anticipato precedentemente, queste due istruzioni permettono di controllare il flusso di esecuzione del programma considerato, in base ad alcune condizioni che verranno controllate proprio al momento dell'esecuzione.

##### L'if statement

L'**if statement** viene usato, a livello basilare, per selezionare uno tra due possibili percorsi di esecuzione in base a una determinata condizione. Generalmente, un if statement si presenta nel modo seguente:

```
if condizione:
	# ISTRUZIONI
else:
	# ISTRUZIONI
```

Le **istruzioni** possono essere singole azioni o anche interi blocchi di codice. La **condizione**, invece, è sostanzialmente una qualsiasi espressione che restituisce un valore [[FDP_05 - Tipi#I booleani `bool`|booleano]].

Un if statement segue questo funzionamento: se la condizione stabilita è `True`, allora viene eseguito il codice contenuto nel corpo dell'`if`: altrimenti, se esiste (l'inserimento di un'istruzione `else` è, infatti, opzionale), viene eseguito il codice contenuto nel corpo dell'`else`. In un if statement del genere, non può mai succedere che vengano eseguiti entrambi i blocchi di istruzioni.

È possibile inserire if statements all'interno di altri if statements: si parla, in questo caso, di **if annidati**. Ad esempio:

```
if i == 10:
	if j < 20:
		a = b
	if k > 100:
		c = d;
	else:
		a = c
else:
	a = d
```

Inoltre, è anche possibile avere una **sequenza di if ed elif**, chiamata anche "**if-elif ladder**". Genericamente, essa assume la seguente struttura:

```
if condizione1:
	# ISTRUZIONI
elif condizione2:
	# ISTRUZIONI
elif condizione3:
	# ISTRUZIONI

...

else:
	# ISTRUZIONI
```

In questo contesto, gli if statement sono eseguiti in ordine dal primo all'ultimo: se `condizione1` viene soddisfatta, verrà eseguito il blocco di codice contenuto nell'`if` e tutto il resto della if-elif ladder viene bypassata; altrimenti, si passa a `condizione2`, e così via. Nel caso in cui nessuna delle condizioni degli `elif` viene soddisfatta, si passa all'`else` finale, che agisce quindi come condizione di default.

Infine, è possibile definire un if statement in maniera compatta utilizzando il cosiddetto **operatore ternario**, che segue il seguente formato:

```
valore_se_vero if condizione else valoreSeFalso;
```
___
##### Il match statement

Il **match statement**, a grandi linee, funziona in maniera simile a un if-elif ladder, ma è spesso preferibile ad esso, essendo generalmente più efficiente oltre a risultare più organizzato e comprensibile. Inoltre, si tratta sostanzialmente di un meccanismo diverso: mentre un if va a controllare espressioni booleane, il match ricerca **uguaglianze tra espressioni**. La forma generale di un match statement è la seguente:

```
match espressione:
	case valore1:
		# ISTRUZIONI
	case valore2:
		# ISTRUZIONI

	...

	case valoreN:
		# ISTRUZIONI
	case _:
		# ISTRUZIONI
```

Similmente all'if-elif ladder, il match statement ha il seguente funzionamento: il valore attuale di `espressione` è confrontato con ognuno dei valori dei vari `case`, andando dall'alto verso il basso; se viene trovata una coincidenza, viene eseguito il blocco di istruzioni relativo al caso in questione; invece, se non vengono trovate coincidenze, viene eseguito il blocco di istruzioni del caso di default, ossia `case _`. Tuttavia, essendo tale blocco opzionale, se ciò accade e non è presente alcun caso `_` non viene eseguito nulla. Una volta eseguito un blocco appartenente a uno qualsiasi dei casi previsti, l'esecuzione del programma esce dal match e prosegue con l'istruzione immediatamente successiva ad esso.

Ognuno dei valori specificati nei vari casi deve essere costante e unico, e non è possibile avere più casi uguali; è possibile, tuttavia, avere **un caso che racchiuda più valori** possibili per `espressione`. Ad esempio, nel seguente codice:

```
match espressione:
	case valore1 | valore2:
		# ISTRUZIONI
	case valore3:
		# ISTRUZIONI

	...	
```

il match statement entrerà nel primo caso nel caso in cui l'espressione assuma il valore `valore1` oppure `valore2`.

Infine, è possibile **aggiungere degli [[FDP_07 - Istruzioni di controllo#L'if statement|if statement]] in determinati casi**, nell'eventualità in cui si voglia effettuare un controllo in più prima di eseguire il blocco di istruzioni relativo ad essi. Ad esempio:

```
month = 5
day = 4

match day:
	case 1 | 2 | 3 | 4 | 5 if month == 4:
		print("A weekday in April")
	case 1 | 2 | 3 | 4 | 5 if month == 5:
		print("A weekday in May")
```
___
## Istruzioni di iterazione

Le **istruzioni di iterazione**, lavorando in Python, possono presentarsi in due forme: i **while loops** e i **for loops**. Queste istruzioni, ovviamente, permettono di creare dei loop, che eseguiranno ripetutamente uno stesso blocco di istruzioni finché non si raggiungerà una condizione di termine.

##### Il while loop

Il **while loop** è probabilmente l'istruzione iterativa più importante e basilare utilizzata all'interno di Python. Come suggerisce il nome, permette di ripetere un blocco di codice **finché** la condizione che viene controllata è `True`. Genericamente, assume la seguente forma:

```
while condizione:
	# ISTRUZIONI
```

dove `condizione` può essere una qualsiasi espressione che restituisce un valore di tipo `bool`; nel momento in cui la condizione in questione diventa `False`, si esce dal loop e vengono eseguite le istruzioni immediatamente successive ad esso. In alternativa, se prima di passare a istruzioni successive si vuole eseguire un blocco di codice, lo si può inserire in un **`else`**. Possiamo vedere un ciclo del genere nel seguente esempio:

```
i = 1  

while i < 6:  
  print(i)  
  i += 1  
else:  
  print("i non è più minore di 6")
```

Per via del funzionamento del while loop, se la condizione che controlla è inizialmente `False`, il blocco di istruzioni relativo ad esso non verrà mai eseguito, neanche se in seguito la condizione diventerà `True`.
___
##### Il for loop

Il **for loop**, in Python, ha una struttura nettamente diversa e molto più semplice rispetto ad altri linguaggi di programmazione. Il for loop di Python ricorda particolarmente il funzionamento di un "for-each loop" di linguaggi come Java o C++, e viene infatti utilizzato principalmente per **iterare sugli elementi di una sequenza**. A livello generale, esso assume la seguente struttura:

```
for elemento in sequenza:
	# ISTRUZIONI
```

e permette di eseguire le istruzioni contenute nel suo corpo per ogni `elemento` contenuto in `sequenza`. Ciononostante, è anche possibile implementare un for loop che, per certi versi, ricorda il funzionamento di un for loop in altri linguaggi, in particolare in relazione alla presenza di un valore che funge da **contatore**: infatti, come abbiamo detto, in Python il for loop viene utilizzato per iterare sugli elementi di una sequenza, ma quest'ultima può anche essere ad esempio una **sequenza di interi fornita da un [[FDP_06 - Generatori e strutture dati#Generatori|generatore]]** come `range()`. Ad esempio, il seguente loop:

```
for x in range(6):
	# ISTRUZIONI
```

eseguirà il proprio corpo di istruzioni per ogni numero intero `x` compreso nell'intervallo $[0,6)$.

Analogamente al [[FDP_07 - Istruzioni di controllo#Il while loop|while loop]], se terminata l'iterazione si vuole eseguire un blocco di codice prima di passare alle istruzioni successive, lo si può inserire in un **`else`**. Possiamo vedere un ciclo del genere nel seguente esempio:

```
for x in range(6):  
  print(x)  
else:  
  print("Finito!")
```

Una funzione particolarmente utile nel contesto dei for loop, che si può utilizzare con le **[[FDP_06 - Generatori e strutture dati|strutture dati]] indicizzabili**, è **`enumerate(seq)`** che riceve in input una sequenza `seq` di elementi e restituisce, sostanzialmente, una lista ordinata di coppie `indice : elemento`, dove `indice` è l'indice dell'elemento considerato all'interno di `seq`, mentre `elemento` è proprio tale elemento. Questa funzione ci permette facilmente di iterare su una sequenza considerando, ad ogni iterazione, sia un elemento che il suo indice. Per utilizzarla all'interno di un for loop, si può scrivere:

```
for i, el in enumerate(seq):
	# ISTRUZIONI
```
___
## Istruzioni di salto

Infine, le **istruzioni di salto**, in Python, possono anch'esse presentarsi in tre forme: il **break**, il **continue** e il **return**. Queste istruzioni vengono utilizzate per "saltare" ad altre parti del codice.

##### L'istruzione break

L'istruzione **`break`** viene spesso utilizzata per forzare il termine di un qualsiasi ciclo, saltando al codice immediatamente successivo al blocco in questione (quando viene utilizzato in loop annidati, il `break` ha effetto solo sul suo livello).
___
##### L'istruzione continue

L'istruzione **`continue`**, invece, consente di forzare una nuova iterazione del loop, andando a ignorare determinate istruzioni nell'iterazione in cui viene eseguito. Ad esempio, nel seguente [[FDP_07 - Istruzioni di controllo#Il while loop|while loop]]:

```
i = 0 
 
while i < 6:  
  i += 1  
  if i == 3:  
    continue  
  print(i)
```

se il numero `i` considerato nell'iterazione corrente è diverso da $3$, viene stampato; se, invece, il numero è pari a $3$, e dunque viene rispettata la condizione valutata dall'`if`, viene eseguita l'istruzione `continue`, che forza la prossima iterazione del ciclo ignorando qualsiasi altra istruzione presente nel suo corpo.

Analogamente a `break`, anche `continue` consente l'utilizzo di etichette, precisamente alla stessa maniera e con le stesse restrizioni.
___
##### L'istruzione return

L'istruzione **`return`** viene usata, appunto, per fare in modo che un metodo "restituisca" qualcosa. Oltre a questa sua caratteristica principale, esso può essere effettivamente considerato un'istruzione di salto in quanto, alla sua esecuzione, viene immediatamente terminata l'esecuzione del metodo in cui è presente.
___