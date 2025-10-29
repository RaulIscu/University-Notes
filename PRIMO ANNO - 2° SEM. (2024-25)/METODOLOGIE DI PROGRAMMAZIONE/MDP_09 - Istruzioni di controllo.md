Alcune delle componenti fondamentali e più utili di un qualsiasi linguaggio di programmazione sono le "**istruzioni di controllo**", o ***control statements***, delle istruzioni particolari che portano il programma a variare il suo comportamento e le sue azioni in base a particolari condizioni. In Java, i *control statements* possono essere divisi in **tre categorie** in base al loro funzionamento:
- le istruzioni di **selezione**, che scelgono diversi "percorsi" all'interno del programma in base al risultato di un espressione o allo stato di una variabile;
- le istruzioni di **iterazione**, che creano dei *loop* all'interno del programma;
- le istruzioni di **salto**, che permettono al programma di essere eseguito in maniera non-lineare.

Di seguito, verrà analizzata nel dettaglio ciascuna di queste categorie.

## Istruzioni di selezione

Le **istruzioni di selezione**, lavorando in Java, possono presentarsi principalmente in due forme: gli ***if statements*** e gli ***switch statements***. Come anticipato precedentemente, queste due istruzioni permettono di controllare il flusso di esecuzione del programma considerato, in base ad alcune condizioni che verranno controllate proprio al momento dell'esecuzione.

##### L'if statement

L'**if statement** viene usato, a livello basilare, per selezionare uno tra due possibili percorsi di esecuzione in base a una determinata condizione. Generalmente, un if statement si presenta nel modo seguente:

```
if (condizione) {
	// ISTRUZIONI
} else {
	// ISTRUZIONI
}
```

Le **istruzioni** possono essere singole azioni o anche interi blocchi di codice; nel caso in cui si tratti di istruzioni singole, è possibile omettere le parentesi graffe:

```
if (condizione) istruzione1;
else istruzione2;
```

La **condizione**, invece, è sostanzialmente una qualsiasi espressione che restituisce un valore [[MDP_07 - Tipi primitivi|booleano]], e va necessariamente racchiusa all'interno di parentesi tonde.

Un if statement segue questo funzionamento: se la condizione stabilita è `true`, allora viene eseguito il codice contenuto nel corpo dell'`if`; altrimenti, se esiste (l'inserimento di un'istruzione `else` è, infatti, opzionale), viene eseguito il codice contenuto nel corpo dell'`else`. In un if statement del genere, non può mai succedere che vengano eseguiti entrambi i blocchi di istruzioni.

È possibile inserire if statements all'interno di altri if statements: si parla, in questo caso, di **if annidati**. Ad esempio:

```
if (i == 10) {
	if (j < 20) a = b;
	if (k > 100) c = d;
	else a = c;
} else a = d;
```

Inoltre, è anche possibile avere una **sequenza di if ed else if**, chiamata anche "**if-else-if ladder**". Genericamente, essa assume la seguente struttura:

```
if (condizione1) {
	// ISTRUZIONI
} else if (condizione2) {
	// ISTRUZIONI
} else if (condizione3) {
	// ISTRUZIONI
}

...

else {
	// ISTRUZIONI
}
```

In questo contesto, gli if statement sono eseguiti in ordine dal primo all'ultimo: se `condizione1` viene soddisfatta, verrà eseguito il blocco di codice contenuto nell'`if` e tutto il resto della if-else-if ladder viene bypassata; altrimenti, si passa a `condizione2`, e così via. Nel caso in cui nessuna delle condizioni degli `else if` viene soddisfatta, si passa all'`else` finale, che agisce quindi come condizione di default.

Infine, è possibile definire un if statement in maniera compatta utilizzando il cosiddetto **operatore condizionale**, che segue il seguente formato:

```
condizione ? valoreSeVero : valoreSeFalso;
```
___
##### Lo *switch statement*

Lo ***switch** statement*, a grandi linee, funziona in maniera simile a un *if-else-if ladder*, ma è spesso preferibile ad esso, essendo generalmente più efficiente (a livello di compilazione e di costo computazionale) oltre a risultare più organizzato e comprensibile. Inoltre, si tratta sostanzialmente di un meccanismo diverso: mentre un *if* va a controllare espressioni booleane, lo *switch* ricerca **uguaglianze tra espressioni**. La forma generale di uno *switch statement* è la seguente:

```
switch (espressione) {
	case valore1:
		// ISTRUZIONI
		break;
	
	case valore2:
		// ISTRUZIONI
		break;

	...

	case valoreN:
		// ISTRUZIONI
		break;
	
	default:
		// ISTRUZIONI
		break;
}
```

Similmente all'*if-else-if ladder*, lo *switch statement* ha il seguente funzionamento: il valore attuale di `espressione` è confrontato con ognuno dei valori dei vari *case*, andando dall'alto verso il basso; se viene trovata una coincidenza, viene eseguito il blocco di istruzioni relativo al caso in questione; invece, se non vengono trovate coincidenze, viene eseguito il blocco di istruzioni associato a `default`. Tuttavia, essendo tale blocco opzionale, se ciò accade e non è presente alcun blocco `default` non viene eseguito nulla. L'inserimento di `break` al termine del blocco di istruzioni di ogni *case* permette di uscire fuori dallo *switch statement* dopo l'esecuzione di uno dei blocchi; l'istruzione `break`, infatti, porterà all'esecuzione del codice immediatamente seguente allo *switch statement*.

L'espressione analizzata dallo *switch* può essere di tipo `byte`, `short`, `int`, `char` o anche `String`. Ognuno dei valori specificati nei vari casi deve essere costante e unico, e non è possibile avere più casi uguali; è possibile, tuttavia, avere **un *case* che racchiuda più valori** possibili per `espressione`. Ad esempio, nel seguente codice:

```
switch (espressione) {
	case valore1, valore2:
		// ISTRUZIONI
		break;

	case valore3:
		// ISTRUZIONI
		break;

	...	
}
```

lo *switch statement* entrerà nel primo *case* nel caso in cui l'espressione assuma il valore `valore1` oppure `valore2`.

Come con gli *if statements*, è possibile avere anche degli ***switch* annidati**. Inoltre, a partire da Java 13, è possibile costruire degli ***switch* compatti**, che non solo richiedono meno righe ma non necessitano neanche dell'inserimento dell'istruzione `break` all'interno di ogni *case*:

```
switch (espressione) {
	case valore1 -> istruzione1;
	case valore2 -> istruzione2;
	
	...
	
	case valoreN -> istruzioneN;
	default -> istruzioneDefault;
}
```

Com'è evidente, tuttavia, ciò è possibile solo nel momento in cui il blocco di istruzioni da eseguire per ciascun *case*, esclusa l'istruzione `break`, corrisponde a una singola istruzione.
___
## Istruzioni di iterazione

Le **istruzioni di iterazione**, lavorando in Java, possono presentarsi in tre forme: i ***while loops***, i ***do-while loops*** e i ***for loops***. Queste istruzioni, ovviamente, permettono di creare dei *loop*, che eseguiranno ripetutamente uno stesso blocco di istruzioni finché non si raggiungerà una condizione di termine.

##### Il *while loop*

Il ***while loop*** è probabilmente l'istruzione iterativa più importante e basilare utilizzata all'interno di Java. Come suggerisce il nome, permette di ripetere un blocco di codice **finché** la condizione che viene controllata è `true`. Genericamente, assume la seguente forma:

```
while (condizione) {
	// ISTRUZIONI
}
```

dove `condizione` può essere una qualsiasi espressione che restituisce un valore di tipo `boolean`; nel momento in cui la condizione in questione diventa `false`, si esce dal *loop* e vengono eseguite le istruzioni immediatamente successive ad esso. Come per gli `if`, se il blocco di istruzioni è costituito da una sola azione, è possibile omettere le parentesi graffe.

Per via del funzionamento del *while loop*, se la condizione che controlla è inizialmente `false`, il blocco di istruzioni relativo ad esso non verrà mai eseguito, neanche se in seguito la condizione diventerà `true`.
___
##### Il *do-while loop*

Il ***do-while loop*** elude, parzialmente, questa caratteristica. Si tratta, infatti, di un *while* il cui corpo di codice viene sempre eseguito almeno una volta, anche se la sua condizione è inizialmente falsa: ciò avviene, banalmente, perché il corpo di codice viene posto prima della condizione legata ad esso. Genericamente, il *do-while loop* assume la seguente forma:

```
do {
	// ISTRUZIONI
} while (condizione);
```

Ogni iterazione di un *do-while loop* eseguirà prima il suo corpo di codice, e solo dopo valuterà la sua condizione: a quel punto, se la condizione risulterà essere `true`, tutto il procedimento verrà ripetuto; altrimenti, il ciclo viene terminato.
___
##### Il *for loop*

Il ***for loop***, in Java, si presenta principalmente in due forme: una è quella più "tradizionale", mentre la seconda è il cosiddetto "***for-each loop***". La **forma tradizionale** del *for loop* assume, genericamente, la seguente forma:

```
for (inizializzazione; condizione; iterazione) {
	// ISTRUZIONI
}
```

Come per le altre istruzioni di controllo precedentemente analizzate, se il blocco di codice all'interno delle parentesi graffe è composto da una sola azione, tali parentesi possono essere omesse. Il suo funzionamento è il seguente: 
- all'inizio del *loop*, viene eseguita l'**`inizializzazione`**, che consiste in un'espressione in cui viene dichiarata una cosiddetta "**variabile di controllo**" a cui viene assegnato un valore di partenza (la variabile di controllo svolgerà, sostanzialmente, il ruolo di contatore); 
- in seguito a ciò, viene valutata la **`condizione`**, che solitamente consiste in un confronto tra la variabile di controllo e un determinato valore;
- se tale confronto è `true`, viene eseguito il blocco di codice del *for loop*, e in seguito viene eseguita l'**`iterazione`**, che solitamente va a incrementare il valore della variabile di controllo, e si va a ripetere l'intero procedimento; se, invece, il confronto è `false`, il *loop* viene terminato.

Di seguito, un esempio di *for loop* che inizializza come variabile di controllo `n = 10`, che valuta come condizione se tale variabile di controllo è positiva, e che a ogni iterazione va a diminuire di 1 il valore della variabile di controllo:

```
for (int n = 10; n > 0; n--;) {
	// ISTRUZIONI
}
```

È possibile, poi, **includere più di un'espressione nella sezione di inizializzazione o in quella di iterazione**. Per fare ciò, bisogna inserire una virgola (`,`) tra le varie espressioni, nel modo seguente:

```
for (int a = 1, int b = 4; a < b; a++, b--;) {
	// ISTRUZIONI
}
```

La struttura delle espressioni su cui si basa un *for loop* è relativamente flessibile: è possibile, ad esempio, avere come condizione una qualsiasi espressione booleana, anche non relativa alla variabile di controllo; è possibile, inoltre, creare un *loop* infinito implementando un *for loop* privo delle sue tre espressioni, nel modo seguente:

```
for ( ; ; ) {
	// ISTRUZIONI
}
```

Il ***for-each loop***, invece, viene utilizzato specificatamente per operare un ciclo su una collezione di oggetti (come un *array*) in maniera sequenziale, ossia dall'inizio alla fine di essa. Genericamente, esso assume la seguente forma:

```
for (tipo variabileIterata : collezione) {
	// ISTRUZIONI
}
```

dove `tipo` specifica il tipo delle variabili che verranno utilizzate dal ciclo, `variabileIterata` è il nome della variabile che conterrà mano a mano gli elementi della collezione considerata, e quest'ultima è indicata da `collezione`. Ad ogni iterazione del *loop*, nella variabile iterata viene conservato l'elemento successivo della collezione; ciò avviene finché non vengono esauriti tutti gli elementi della collezione. Nonostante il *for-each loop* termini automaticamente una volta esauriti gli elementi dell'*array*, è possibile terminare il ciclo prima utilizzando l'istruzione `break`.

È importante ricordare che, iterando su una [[MDP_14 - Strutture dati|struttura dati]] con un *for-each loop*, le variabili iterate sono utilizzate esclusivamente per essere lette, e non potranno essere modificate dal blocco di istruzioni incluso nel corpo del ciclo. Ad esempio, nel seguente codice:

```
int nums[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

for (int x : nums) x = x * 10;
```

il blocco di istruzioni contenuto nel *for-each loop* non farà effettivamente nulla, in quanto sta cercando di modificare un elemento che viene solamente letto.

Anche i *for loops*, così come i *for-each loops*, possono essere **annidati**.
___
## Istruzioni di salto

Infine, le **istruzioni di salto**, in Java, possono anch'esse presentarsi in tre forme: il ***break***, il ***continue*** e il ***return***. Queste istruzioni vengono utilizzate per "saltare" ad altre parti del codice.

##### L'istruzione *break*

L'istruzione **`break`** viene spesso utilizzata per forzare il termine di un qualsiasi ciclo, saltando al codice immediatamente successivo al blocco in questione (quando viene utilizzato in *loop* annidati, il `break` ha effetto solo sul suo livello). Alternativamente, è possibile espandere l'istruzione `break` con un'**etichetta**, che permette di saltare a blocchi di codice ben precisi. Infatti, si può assegnare un'etichetta a un blocco di codice impostandolo nel seguente modo:

```
etichetta: {
	bloccoDiCodice;
}
```

A questo punto, per indirizzare a un blocco etichettato utilizzando l'istruzione `break`, basterà scrivere:

```
break etichetta;
```

Ciò, tuttavia, è possibile solo con blocchi di codice che racchiudono il blocco dove è presente l'istruzione `break` in questione.
___
##### L'istruzione *continue*

L'istruzione **`continue`**, invece, consente di forzare una nuova iterazione del *loop*, andando a ignorare determinate istruzioni nell'iterazione in cui viene eseguito. Ad esempio, nel seguente *for loop*:

```
for (int i = 0; i < 10; i++;) {
	if (i % 2 == 0) continue;
	System.out.println(i + " is an odd number.")
}
```

se il numero considerato nell'iterazione corrente è dispari, e dunque il resto della sua divisione con 2 è diverso da 0, viene stampata la stringa; se, invece, il numero è pari, e dunque viene rispettata la condizione valutata dall'`if`, viene eseguita l'istruzione `continue`, che forza la prossima iterazione del ciclo ignorando qualsiasi altra istruzione presente nel suo corpo.

Analogamente a `break`, anche `continue` consente l'utilizzo di etichette, precisamente alla stessa maniera e con le stesse restrizioni.
___
##### L'istruzione *return*

L'istruzione **`return`** viene usata, appunto, per fare in modo che un metodo "restituisca" qualcosa. Oltre a questa sua caratteristica principale, esso può essere effettivamente considerato un'istruzione di salto in quanto, alla sua esecuzione, viene immediatamente terminata l'esecuzione del metodo in cui è presente.
___