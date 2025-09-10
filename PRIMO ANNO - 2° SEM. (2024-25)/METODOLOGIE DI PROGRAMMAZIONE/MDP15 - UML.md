## Cos'è l'UML?

Quando si lavora a un progetto ampio e complesso, che comprende un grande numero di classi collegate in modo intricato tra di loro, diventa molto utile se non fondamentale avere uno **schema comprensivo e chiaro** di tali classi e dei modi in cui interagiscono tra di loro. È a questo scopo che si utilizza l'UML.

**UML**, o ***Unified Modeling Language***, è un "**linguaggio di modellazione**" standardizzato, che in programmazione viene tendenzialmente utilizzato per **progettare** e **visualizzare il design** di un determinato software (viene utilizzato anche in altri ambiti, come l'ingegneria o l'economia, per altri scopi). In particolare, nella [[MDP01 - Java e la OOP#Cos'è la programmazione a oggetti?|OOP]], si utilizza un certo tipo di diagramma UML, il cosiddetto "**diagramma delle classi**", o ***class diagram***, che mostra, in maniera più o meno compatta:
- le **classi** che compongono un programma;
- i **membri** di tali classi;
- i **collegamenti tra le classi**, siano essi di tipo [[MDP01 - Java e la OOP#Ereditarietà|ereditario]], compositivo, associativo, ecc. ecc.
___
## Come costruire una classe in UML

Ma come possiamo rappresentare, concretamente, una **classe** in un diagramma UML? Per convenzione, **ogni classe viene rappresentata con un rettangolo** diviso in **tre sezioni**:
- il **nome della classe**;
- i **campi**;
- i **metodi** (incluso il [[MDP02 - Classi#Campi, metodi e costruttori|costruttore]]).

La sezione relativa al nome della classe sarà sempre la prima, ed è esclusivamente destinata a ciò; la sezione seguente sarà quella dei campi, che verranno elencati in ordine arbitrario, e la stessa cosa vale per la sezione dei metodi (preferibilmente, però, si inserisce il costruttore come il primo dei metodi).

Analizziamo più nel dettaglio le due sezioni principali, ossia quella dei **campi** e quella dei **metodi**. Partendo dai **campi della classe**, generalmente dichiarare un campo in linguaggio UML porta alla seguente scrittura:

```
visibilità identificatore: Tipo
```

Quindi, la prima cosa che si inserisce è la **visibilità** del campo, ossia sostanzialmente il suo **[[MDP03 - Modificatori d'accesso|modificatore d'accesso]]**, che per semplicità non viene inserito così com'è, ma **"codificato" da un singolo segno** secondo le convenzioni UML, che sono le seguenti:
- il simbolo **`+`** indica un campo definito come **`public`**;
- il simbolo **`-`** indica un campo definito come **`private`**;
- il simbolo **`#`** indica un campo definito come **`protected`**;
- il simbolo **`~`** indica un campo definito come default, o package-private.

In seguito, si inserisce normalmente l'**identificatore** del campo, seguito dai due punti (`:`) e dal **tipo** a cui appartiene.

Vediamo ora i **metodi della classe**. Generalmente, dichiarare un metodo in linguaggio UML porta alla seguente scrittura:

```
visibilità identificatore(param1: Tipo, param2: Tipo...): TipoDiRitorno
```

Anche in questo caso, la prima cosa che si inserisce è la **visibilità** del campo, codificata in modo analogo ai campi; in seguito, si inserisce l'**identificatore** del metodo, seguito dalle parentesi tonde che racchiudono i vari **parametri** del metodo, inseriti in sequenza e intervallati da virgole (`,`), con ognuno di essi che presenta prima il suo identificatore (`param1`, `param2`, ecc. ecc.) e poi il tipo a cui appartiene; infine, finiti i parametri e chiuse le parentesi tonde, si inserisce il **tipo di ritorno** del metodo in questione.

Queste sono tutte le indicazioni principali per disegnare una classe in UML; proviamo ad applicarle in un esempio. Supponiamo di voler disegnare l'UML che rappresenti visivamente la seguente classe `Contatore`:

```
public class Contatore {
	private int count;

	public Contatore() {
		this.count = 0;
	}

	public void conta(int num) {
		count += num;
	}
}
```

Il corrispondente schema UML sarebbe il seguente:

```
+---------------------------+
|         Contatore         |
+---------------------------+
| - count: int              |
+---------------------------+
| + Contatore(): Contatore  |
| + conta(num: int): void   |
+---------------------------+
```

Oltre alle regole spiegate prima, ci sono altre **convenzioni aggiuntive** per raggiungere una precisione ancora maggiore nella rappresentazione di una classe, che riguardano in particolare classi e membri definiti come **`static`**, **`final`** o **`abstract`**:
- una classe annidata o un membro di una classe definiti come `static` presentano il proprio identificatore (se si parla di una classe annidata) o l'intera riga che li definisce (se si parla di un membro) **sottolineati**;
- un membro di una classe definito come `final` presenta il proprio identificatore scritto in **maiuscolo**;
- una classe o un membro di una classe definiti come `abstract` presentano il proprio identificatore scritto in **corsivo**.

Infine, è possibile anche inserire dei cosiddetti "**stereotipi UML**" in certi contesti, principalmente per indicare il ruolo o la particolare natura di una classe. Si tratta di **etichette opzionali** racchiuse tra parentesi del tipo **`<< >>`** e inserite nella sezione relativa al nome di una classe, come:
- **`<<interface>>`**, che indica che la classe in questione è un'[[MDP12 - Interfacce|interfaccia]];
- **`<<abstract>>`**, che indica che la classe in questione è una [[MDP02 - Classi#Classi astratte|classe astratta]];
- **`<<enumeration>>`**, che indica che la classe in questione è un'[[MDP02 - Classi#Enumerazioni|enumerazione]].
___
## I collegamenti tra classi in UML

Ora, avendo chiarito come rappresentare una determinata classe in UML, vediamo come rappresentare i **collegamenti tra classi**.

Nel linguaggio UML, sono definiti principalmente **5 tipi di collegamenti** tra classi:
- la relazione di **associazione**;
- la relazione di **aggregazione**;
- la relazione di **composizione**;
- la relazione di **ereditarietà**;
- la relazione di **implementazione**.

##### Associazione

La relazione di **associazione** rappresenta una relazione molto generale tra due classi, e definisce sostanzialmente il fatto che **un'istanza di una classe "conosce" o "usa" un'istanza di un'altra**; in poche parole, potremmo dire che se tra due classi sussiste una relazione di associazione, allora una classe ha un riferimento all'altra.

Generalmente, la relazione di associazione si traduce, nel codice, come **un campo di una classe che ha come tipo un'altra classe**, e viene rappresentata con una **linea continua** che collega le due classi, che a seconda del caso può possedere anche alcune caratteristiche peculiari e opzionali.

Ad esempio, si può denotare la **cardinalità** della relazione, ossia quante istanze di una classe sono legate a quante istanze di un'altra; ad esempio, se affermiamo che "una persona ha un solo indirizzo", insieme alla freccia di associazione inseriremo la dicitura `1` sia all'apice collegato a `Persona` sia a quello collegato a `Indirizzo`; invece, se affermiamo che "un'università ha molti studenti", inseriremo `1` all'apice collegato a `Università`, e `0..*` all'apice collegato a `Studente`, per indicare che ogni studente è iscritto a una sola università ma un'università può avere molti studenti.

Oltre alla cardinalità, è possibile anche specificare la **direzione** della relazione, ossia in che verso sussiste la "conoscenza" o l'"utilizzo" tra le classi. Di norma, se si mantiene una **linea continua semplice**, ciò vorrebbe dire che **entrambe le classi conoscono l'altra**, tuttavia nel concreto questa situazione è abbastanza rara. Più spesso, invece, si troverà una relazione di associazione **unidirezionale**, ossia in cui solo una delle classi conosce l'altra, ma quest'ultima non ha alcun riferimento alla prima: in tal caso, si utilizza una **linea continua terminata da una freccia triangolare piena**, rivolta verso la classe conosciuta ma non conoscente. Ad esempio, se una classe `Cliente` contiene un riferimento alla classe `Fattura`, ma quest'ultima non conosce la classe `Cliente`, la freccia unidirezionale partirà da `Cliente` e finirà in `Fattura`.

Infine, è possibile anche specificare il "**ruolo**" della relazione, ossia il nome concreto assunto dal membro che stabilisce la relazione. Ad esempio, se una classe `Persona` possiede un campo di tipo `Indirizzo` denominato come `residenza`, sarà possibile inserire la dicitura `residenza` in corrispondenza dell'apice collegato alla classe a cui appartiene tale campo (in questo caso, `Indirizzo`).
___
##### Aggregazione

La relazione di **aggregazione** rappresenta, per certi versi, una forma specializzata di associazione, e definisce sostanzialmente **una relazione di tipo "has-a" debole**, in cui la parte può esistere indipendentemente dal tutto. 

Generalmente, la relazione di aggregazione si traduce, nel codice, in casi simili a quelli dell'[[MDP15 - UML#Associazione|associazione]], ma in cui risulta un po' più evidente che una classe "possiede" o "è composta" da altre classi, che a loro volta possono però esistere in maniera indipendente. Viene rappresentata con una **linea continua terminata da un rombo vuoto**, rivolto verso la classe "contenente".

Trattandosi di una forma più specifica di associazione, anche per l'aggregazione si applicano gli stessi concetti di **cardinalità**, **direzione** e **ruolo**, rispecchiando sostanzialmente le stesse modalità e casi di utilizzo.
___
##### Composizione

La relazione di **composizione** rappresenta una forma di aggregazione più dura, e definisce sostanzialmente **una relazione di tipo "has-a" forte**, in cui la parte non può esistere indipendentemente dal tutto. In questo contesto, il "tutto" possiede e gestisce completamente il ciclo di vita della "parte", e se il "tutto" viene distrutto in qualche modo la stessa cosa avviene per le "parti".

Generalmente, la relazione di composizione si traduce, nel codice, come **una classe che istanzia, al suo interno, altre classi** e le conserva come propri attributi, e viene rappresentata con una **linea continua terminata da un rombo pieno**, rivolto verso la classe "contenente" in maniera analoga alla relazione di [[MDP15 - UML#Aggregazione|aggregazione]].

Anche in questo caso, si applicano gli stessi concetti di **cardinalità** e **ruolo**, rispecchiando sostanzialmente le stesse modalità e casi di utilizzo; invece, per quanto riguarda la **direzione**, tendenzialmente in una relazione di composizione la parte non conosce il tutto, e quindi solitamente si ha una **composizione unidirezionale**, ma non è detto che debba sempre essere così.
___
##### Ereditarietà

La relazione di **[[MDP01 - Java e la OOP#Ereditarietà|ereditarietà]]**, come suggerisce il nome, rappresenta una **relazione gerarchica** tra due classi, una **relazione di tipo "is-a"** tra una superclasse e una sottoclasse, dove la sottoclasse estende la superclasse, ne eredita i campi, e può essere considerata a tutti gli effetti come la sua superclasse.

Generalmente, la relazione di ereditarietà si traduce, nel codice, come **una classe che ne estende un'altra**, e viene rappresentata con una **linea continua terminata da un triangolo vuoto**, rivolto verso la superclasse.

Per natura dell'ereditarietà in Java, la relazione di ereditarietà presenta dei limiti dal punto di vista della **direzione** (non può esistere un'ereditarietà bidirezionale, ci sarà sempre una superclasse e una sottoclasse), del **ruolo** (si tratta di una relazione puramente a livello di classi e non di campi, quindi non si può associare un eventuale identificatore a nessuno dei due apici del collegamento) e della **cardinalità** (sempre essendo una relazione puramente a livello di classe, non ha senso parlare di quante istanze di una sono collegate a quante istanze dell'altra).
___
##### Implementazione

La relazione di **implementazione**, come suggerisce il nome, rappresenta una **relazione gerarchica** tra due classi, una **relazione di tipo "is-a"** tra un'**[[MDP12 - Interfacce|interfaccia]]** e una classe, dove quest'ultima **implementa** l'interfaccia, e ne fornisce quindi una realizzazione concreta.

Generalmente, la relazione di implementazione si traduce, nel codice, come **una classe che implementa un'interfaccia**, e viene rappresentata con una **linea tratteggiata terminata da un triangolo vuoto**, rivolto verso tale interfaccia.

Per pressoché gli stessi motivi precisati nella spiegazione della relazione di ereditarietà, valgono gli stessi limiti per quanto riguarda la **direzione**, il **ruolo** e la **cardinalità**.
___