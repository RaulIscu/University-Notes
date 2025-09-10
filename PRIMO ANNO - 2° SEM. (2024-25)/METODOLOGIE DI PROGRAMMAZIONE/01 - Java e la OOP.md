## Caratteristiche di Java

**Java** è un **linguaggio di programmazione** creato dalla **Sun Microsystems** e pubblicato ufficialmente per la prima volta nel **1995**. Si tratta di un linguaggio completamente basato sulla **[[01 - Java e la OOP#Cos'è la programmazione a oggetti?|programmazione a oggetti]]**, o **OOP**, ampiamente utilizzato anche da applicazioni e aziende famosissime e diffuse (tra le altre, Java viene utilizzato nello sviluppo di Spotify, Airbnb, Google, Instagram, Netflix, e molte altre).

La principale caratteristica che differenzia Java dagli altri linguaggi del genere è la sua possibilità di essere notevolmente ***cross-platform***: un programma Java, infatti, rispetta la politica "**WORA**", ossia "***write once, run anywhere***", ed è sostanzialmente **neutro rispetto all'architettura che lo esegue**. Ciò viene ottenuto soprattutto grazie agli strumenti contenuti nel **Java Development Kit**, o **JDK**, che contiene principalmente questi strumenti:
- la **Java Virtual Machine**, la componente che più di tutte è responsabile dell'abilità di essere *cross-platform* di Java;
- il **Java Runtime Envoirment**;
- il compilatore **Java Compiler**, o **javac**;
- varie **librerie** utili per la scrittura di codice e per la sua compilazione.

Oltre a ciò, Java è un linguaggio **sicuro** e **difficilmente manomissibile**, supporta l'esecuzione di più attività in contemporanea mediante un **ambiente di esecuzione *multithreaded***, è molto **flessibile** e **versatile** (può essere utilizzato per applicazioni desktop, programmi di puro back-end, integrato in ambienti web, ecc. ecc.), e costantemente **aggiornato** con nuove versioni a cadenza pressoché annua.
___
## Cos'è la programmazione a oggetti?

Come detto nel capitolo precedente, Java è un linguaggio basato sulla programmazione a oggetti: ma cos'è la programmazione a oggetti?

La **programmazione a oggetti** è un paradigma di programmazione ben diverso da quello "**procedurale**" che caratterizza maggiormente linguaggi come C o Python. Nella OOP, si potrebbe dire che "**tutto è un oggetto**", un'entità di un certo tipo che può contenere altri dati ed eventualmente altri oggetti, che ha uno stato e che può effettuare determinate operazioni. In questo contesto, il funzionamento di un programma va a coincidere con le diverse interazioni che hanno gli oggetti tra di loro, e con i risultati di tali interazioni.

La corretta applicazione del paradigma della programmazione a oggetti, il più delle volte, si valuta in base all'applicazione dei suoi **principi fondamentali**, che sono:
- **incapsulamento**;
- **ereditarietà**;
- **polimorfismo**;
- **astrazione**.

##### Incapsulamento

L'**incapsulamento** è il principio che professa la **protezione dei dati** da accessi non controllati ed eventualmente inopportuni. Un'applicazione corretta dell'incapsulamento in un programma porta all'**occultamento di informazioni non necessarie all'utente**, rendendo invece pubblica una certa "interfaccia", tendenzialmente corrispondente con un insieme di metodi pubblici.

Protagonisti nell'applicazione concreta dell'incapsulamento sono i **[[03 - Modificatori d'accesso|modificatori d'accesso]]**, e il contesto principale dove viene utilizzato è nella **definizione dei [[02 - Classi#Campi, metodi e costruttori|campi di una classe]]**, che vengono solitamente definiti come  `private` e sono resi visualizzabili e manipolabili tramite dei metodi "getter" e "setter" definiti come `public`.

Un corretto utilizzo dell'incapsulamento offre vari vantaggi, tra cui:
- maggiore **protezione** e un miglior **controllo dei dati**, il cui accesso viene regolato e permesso solo sotto certe condizioni (ad esempio, è possibile progettare metodi getter e setter che prevedano dei controlli o delle operazioni particolari);
- **semplificazione dell'ambiente di lavoro** (nascondere informazioni non necessarie per l'utente rende minore l'ammontare totale di informazioni disponibili);
- spesso, **maggiore manutenibilità del codice**, così come una maggiore **riutilizzabilità**.
___
##### Ereditarietà

L'**ereditarietà** è il principio che viene applicato quando **una classe "eredita" dei membri da un'altra classe**. Un'applicazione corretta dell'ereditarietà porta alla creazione di una **struttura gerarchica** di classi, dove le classi ereditanti vengono dette "**sottoclassi**" e quelle da cui si eredita "**superclassi**" o "**classi base**".

Per creare una relazione di tipo ereditario tra due classi, si sfrutta la keyword **`extends`**, seguita dal nome della superclasse, nella dichiarazione della sottoclasse. Ad esempio, supponiamo di avere una classe `Animale`, e di voler creare una sottoclasse `Cane` che erediti da tale superclasse; si andrebbe a scrivere il seguente codice:

```
public class Animale {
	...
}

public class Cane extends Animale {
	...
}
```

In un esempio del genere, la sottoclasse `Cane` potrà accedere tranquillamente a tutti i membri della superclasse definiti come `public` e `protected`, oltre che a quelli `default` (package-private) se esse si trovano nello stesso package; invece, non avrà modo di accedere ai membri privati della superclasse da cui eredita. In particolare, il **costruttore** della superclasse non viene propriamente ereditato, ma è possibile richiamarlo dal costruttore della sottoclasse utilizzando l'istruzione **`super()`**, che dovrà prendere come parametri un insieme di dati compatibili con il costruttore originario della superclasse.

In Java, si può avere esclusivamente un'**ereditarietà singola**, il che vuol dire che una classe può ereditare solo da una sola superclasse. Per ovviare a questo limite, spesso si utilizzano le **[[12 - Interfacce|interfacce]]**, per cui esso non viene posto.

È importante distinguere in maniera chiara relazioni ereditarie, di tipo "**is-a**" (`Cane` è un `Animale`), da relazioni compositive, di tipo "**has-a**" (`Auto` ha un `Motore`), e dunque più in generale tra **ereditarietà** e **composizione**. Se la prima va a istanziare relazioni puramente gerarchiche, in cui una sottoclasse può essere considerata a tutti gli effetti come la superclasse, la seconda va a creare delle "associazioni" di oggetti, in cui tendenzialmente un oggetto contiene riferimenti ad altri oggetti, e quindi può essere visto come composto da essi.

Un corretto utilizzo dell'ereditarietà offre vari vantaggi, tra cui:
- **riutilizzo** del codice delle superclassi;
- **estendibilità**;
- definizione di **strutture gerarchiche** ben definite, che semplificano la manutenzione e l'utilizzo del codice, e forniscono una buona **base per l'applicazione del [[01 - Java e la OOP#Polimorfismo|polimorfismo]]**.
___
##### Polimorfismo

Il **polimorfismo** è il principio che viene applicato quando **un oggetto può assumere comportamenti diversi** (la parola "polimorfismo", del resto, significa "molte forme") in base al contesto in cui viene utilizzato. Concretamente, il polimorfismo può essere applicato in vari modi, tra cui:
- polimorfismo a ***compile-time***, o **polimorfismo statico**;
- polimorfismo a ***run-time***, o **polimorfismo dinamico**.

Nel **polimorfismo statico**, si parla principalmente di "***overloading***" di determinati metodi, ossia della definizione di più metodi, all'interno di una stessa classe, che hanno **stesso nome ma "firme" diverse** (per "firma", si intende principalmente il **tipo di ritorno** e il **numero e tipo dei parametri** presi in input). Ad esempio, nella seguente classe:

```
public class Calcolatrice {
	public int somma(int a, int b) {
		return a + b;
	}

	public double somma(double a, double b) {
		return a + b;
	}
}
```

viene effettuato un overloading del metodo `somma()`, per cui vengono fornite due implementazioni diverse. In un contesto del genere, chiamando il metodo in questione, Java deciderà quale delle due implementazioni utilizzare a tempo di compilazione, in base ai parametri forniti concretamente nella chiamata e al tipo di ritorno previsto.

Nel **polimorfismo dinamico**, invece, si parla principalmente di "***overriding***" di determinati metodi, ossia della ridefinizione di un determinato metodo, per cui viene fornita una nuova implementazione; ciò avviene strettamente in contesti legati all'**[[01 - Java e la OOP#Ereditarietà|ereditarietà]]**, in cui una sottoclasse va a ridefinire un metodo precedentemente definito nella sua superclasse. Ad esempio, nel seguente sistema di classi:

```
public class Animale {
	public void faiVerso() {
		System.out.println("Verso generico!");
	}
}


public class Cane extends Animale {
	@Override
	public void faiVerso() {
		System.out.println("Bau!");
	}
}

public class Gatto extends Animale {
	@Override
	public void faiVerso() {
		System.out.println("Miao!");
	}
}
```

le sottoclassi `Cane` e `Gatto` vanno a ridefinire il metodo `faiVerso()`, fornendone un'implementazione personalizzata (si noti che, convenzionalmente, un metodo che opera un overriding è preceduto dall'annotazione **`@Override`**). L'applicazione del polimorfismo dinamico permette di trattare un oggetto, a seconda del caso, sia come istanza del suo tipo effettivo sia come istanza della sua superclasse; ad esempio, tornando al sistema di classi precedente, si potrebbe scrivere il seguente codice:

```
Animale a1 = new Cane();
Animale a2 = new Gatto();

a1.faiVerso();
a2.faiVerso();
```

Notiamo che, in questo caso, il polimorfismo si palesa nel fatto che gli oggetti `a1` e `a2` vengono istanziati come essendo di tipo `Animale`, essendo `Cane` e `Gatto` sottoclassi di quest'ultima, e tuttavia l'invocazione di un metodo sugli oggetti (in questo caso, `faiVerso()`) va a chiamare l'implementazione relativa al tipo effettivo dell'oggetto, non della sua superclasse.

Un corretto utilizzo del polimorfismo offre vari vantaggi, tra cui:
- maggiore **flessibilità** del codice (del codice relativamente generico potrà lavorare con oggetti diversi se trattati in modo polimorfico);
- **estendibilità** e **manutenibilità** del codice, principalmente per la gestione efficiente della struttura ereditaria delle classi.
___
##### Astrazione

L'**astrazione** è il principio che professa la **separazione tra generalizzazione e implementazione**, e che consiglia di modellare una certa entità mostrandone solo gli aspetti essenziali e nascondendone i dettagli non rilevanti. Un'applicazione corretta dell'astrazione permette di **definire cosa fa un oggetto, senza specificare come esso lo faccia**.

In Java, ci sono principalmente due strumenti che permettono di applicare l'astrazione:
- le **[[02 - Classi#Classi astratte|classi astratte]]**;
- le **[[12 - Interfacce|interfacce]]**.

Un corretto utilizzo dell'astrazione offre vari vantaggi, tra cui:
- notevole **semplificazione della struttura** del proprio codice, oltre a maggiore **modularità** e **manutenibilità**;
- maggiore **flessibilità** delle classi implementate;
- **riutilizzo** del codice;
- una solida **base per l'applicazione del [[01 - Java e la OOP#Polimorfismo|poliformismo]]**.
___