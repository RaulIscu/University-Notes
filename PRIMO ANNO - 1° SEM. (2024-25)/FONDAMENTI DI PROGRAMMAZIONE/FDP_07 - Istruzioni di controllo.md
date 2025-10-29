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
	// ISTRUZIONI
else:
	// ISTRUZIONI
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
	// ISTRUZIONI
elif condizione2:
	// ISTRUZIONI
elif condizione3:
	// ISTRUZIONI

...

else:
	// ISTRUZIONI
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
		// ISTRUZIONI
	case valore2:
		// ISTRUZIONI

	...

	case valoreN:
		// ISTRUZIONI
	case _:
		// ISTRUZIONI
}
```

Similmente all'if-elif ladder, il match statement ha il seguente funzionamento: il valore attuale di `espressione` è confrontato con ognuno dei valori dei vari `case`, andando dall'alto verso il basso; se viene trovata una coincidenza, viene eseguito il blocco di istruzioni relativo al caso in questione; invece, se non vengono trovate coincidenze, viene eseguito il blocco di istruzioni del caso di default, ossia `case _`. Tuttavia, essendo tale blocco opzionale, se ciò accade e non è presente alcun caso `_` non viene eseguito nulla. Una volta eseguito un blocco appartenente a uno qualsiasi dei casi previsti, l'esecuzione del programma esce dal match e prosegue con l'istruzione immediatamente successiva ad esso.

Ognuno dei valori specificati nei vari casi deve essere costante e unico, e non è possibile avere più casi uguali; è possibile, tuttavia, avere **un caso che racchiuda più valori** possibili per `espressione`. Ad esempio, nel seguente codice:

```
match espressione:
	case valore1 | valore2:
		// ISTRUZIONI
	case valore3:
		// ISTRUZIONI

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


___
##### Il for loop


___
## Istruzioni di salto

Infine, le **istruzioni di salto**, in Python, possono anch'esse presentarsi in tre forme: il **break**, il **continue** e il **return**. Queste istruzioni vengono utilizzate per "saltare" ad altre parti del codice.

##### L'istruzione break


___
##### L'istruzione continue


___
##### L'istruzione return


___