## Cos'è un "design pattern"?

Nella progettazione di un software, tendenzialmente di un'applicazione, è quasi sicuro che si incapperà in problemi comuni e ricorrenti, riguardanti principalmente:
- la struttura delle classi progettate;
- le relazioni che intercorrono tra di esse;
- le responsabilità che dovrebbero essere assegnate alle varie componenti del programma;
- la scelta di un approccio piuttosto che un altro nel risolvere un problema;
ecc. ecc.

Per cercare di ovviare in maniera sistematica e collaudata a problemi del genere, nel corso del tempo hanno preso piede i cosiddetti "***design pattern***", che possiamo definire come delle soluzioni generali e riutilizzabili per alcuni di questi problemi ricorrenti. Si tratta non tanto di codice prefabbricato, pronto da copiare e incollare, ma piuttosto di modelli architetturali, di schemi teorici da seguire a grandi linee per progettare una determinata componente del software.

Il concetto di *design pattern* nasce negli **anni '70**, ed è stato poi specializzato e formalizzato nell'ambito informatico da un gruppo di quattro autori soprannominato "**Gang of Four**", o **GoF** in breve. Nel **1994**, questi autori pubblicarono il libro "*Design Patterns: Elements of Reusable Object-Oriented Software*", che descriveva nel dettaglio **23 design pattern** divisi in tre categorie principali:
- **creazionali**;
- **strutturali**;
- **comportamentali**.

Sostanzialmente, i *design pattern* servono a **offrire soluzioni collaudate e sicure** a problemi ricorrenti, **favorire il riutilizzo e la manutenzione** del codice (implementare soluzioni conosciute e comuni favorisce la leggibilità e la comprensibilità del proprio programma), **rendere il software più flessibile e modulare**. Non si tratta di strumenti obbligatori in alcun modo, ma molto preziosi in varie evenienze, a patto che non si cerchi di implementarli ovunque andando a sfociare nell'*overengineering*.

Di seguito, si analizzeranno alcuni dei *design pattern* principali e più usati, spiegandone lo scopo, la struttura generale, i vantaggi e degli esempi di applicazione.
___
## Singleton

Il *design pattern* **Singleton** appartiene alla categoria dei **pattern creazionali**, e il suo scopo principale è quello di **garantire che una classe disponga di una singola istanza in tutto il programma**, fornendo e controllando un punto di accesso globale ad essa.

Questo scopo può essere raggiunto in vari modi. Innanzitutto, distinguiamo un'implementazione "eager" da una "lazy":
- un'implementazione di "**eager Singleton**" procede a inizializzare subito l'istanza della classe, a prescindere dalla chiamata o meno di altri metodi (si tratta di un approccio semplice e *thread-safe*, ma inefficiente in alcune situazioni);
- un'implementazione di "**lazy Singleton**", invece, inizializza l'istanza della classe in un secondo momento, e tipicamente fornisce un metodo che ne gestisce la costruzione (si evita la creazione potenzialmente inutile di istanze a priori, ma non rappresenta una soluzione sicura in ambienti *multi-threaded*).

Di seguito, un esempio generico di come si potrebbe definire una classe la cui struttura rispecchia quella dell'eager Singleton:

```
public class EagerSingleton {

	private static final EagerSingleton instance = new Singleton();

	private EagerSingleton() {
		// CORPO DEL COSTRUTTORE
	}

	public static EagerSingleton getInstance() {
		return instance;
	}
}
```

Essendo un esempio di eager Singleton, notiamo come la costruzione dell'istanza, e la sua assegnazione al campo della classe `EagerSingleton`, avvengano istantaneamente, e che di conseguenza il metodo `getInstance()` vada solo a restituire l'istanza che è già stata creata. Ora, analizziamo un esempio generico di come si potrebbe definire una classe la cui struttura rispecchia quella del lazy Singleton:

```
public class LazySingleton {

	private static LazySingleton instance;

	private LazySingleton() {
		// CORPO DEL COSTRUTTORE
	}

	public static LazySingleton getInstance() {
		if (instance == null) instance = new Singleton();
		return instance;
	}
}
```

In questo caso, notiamo che l'istanza viene costruita solo quando viene chiamato per la prima volta il metodo `getInstance()`, che quindi controlla attivamente lo stato del campo `instance` prima di restituirlo.

In alternativa, è anche possibile rispettare il pattern Singleton sfruttando una classe interna statica, seguendo una struttura del genere:

```
public class InnerStaticSingleton {

	private InnerStaticSingleton() {
		// CORPO DEL COSTRUTTORE
	}

	private static class Holder {
		private static final InnerStaticSingleton INSTANCE = new InnerStaticSingleton();
	}

	public static InnerStaticSingleton getInstance() {
		return Holder.INSTANCE;
	}
}
```

Un'implementazione di Singleton permette un **controllo centralizzato dell'accesso** a una risorsa condivisa, **riduce** notevolmente il rischio di **creazione di oggetti inutili**, e fornisce un **punto di accesso globale** all'istanza in questione da parte di tutte le classi, senza bisogno di doverla passare come parametro. Tuttavia, si va a ridurre anche la flessibilità del codice, diventa più difficile testarlo, e potrebbero verificarsi casi di concorrenze e dipendenze problematiche.

Essendo un pattern potente ma anche rischioso da usare, si preferisce sfruttare il Singleton solo quando è veramente necessario, e quando si è sicuri che servirà sempre e solo una singola istanza di una determinata classe per il proprio programma.
___
## Simple Factory

Il *design pattern* **Simple Factory** appartiene alla categoria dei **pattern creazionali** (non fa ufficialmente parte dei 23 pattern definiti dal GoF, ma è ampiamente diffuso soprattutto come variante semplificata del pattern [[Design pattern#Factory Method|Factory Method]]), e il suo scopo principale è quello di **centralizzare la costruzione di oggetti di varie classi**, separando la logica di costruzione dalle classi da istanziare e fornendo un metodo statico per gestirla.

Per comprendere meglio la struttura generale di questo pattern, analizziamo un esempio: supponiamo di avere una classe `Forma`, e varie sottoclassi `Quadrato`, `Cerchio`, `Triangolo`, ecc. che ereditano da `Forma`. Piuttosto che andare a costruire singolarmente ciascuna di queste forme, è possibile centralizzarne la costruzione in una classe `FormaFactory`, definita ad esempio nel modo seguente:

```
public class FormaFactory {

	public static Forma creaForma(String tipo) {
	
		return switch (tipo.toLowerCase()) {
			case "quadrato" -> new Quadrato();
			case "cerchio" -> new Cerchio();
			case "triangolo" -> new Triangolo();
			default -> throw new IllegalArgumentException("Non supportato: " + tipo);
		}
	}
}
```

Come anticipato, uno dei principali vantaggi è la centralizzazione della logica di costruzione di più classi, e la maggiore astrazione che ne consegue. Oltre a ciò, un approccio del genere aumenta la manutenibilità del codice, e lo rende in ogni caso facilmente estensibile (in caso si vogliano aggiungere altri tipi istanziabili, basterà aggiungere le righe di codice corrispondenti nel metodo `creaX()`).

Allo stesso tempo, gestire un pattern Simple Factory diventa problematico quando si cerca di gestire un numero eccessivo di tipi, o quando quest'ultimi presentano dipendenze più o meno complesse. Si tratta, insomma, di una **variazione potente ma meno flessibile del pattern Factory Method**.

È consigliato utilizzare questo *design pattern* quando si ha un numero sostanzioso ma non eccessivo di sottotipi di un'interfaccia o di una superclasse, e in particolare quando questi sottotipi non presentano un'ereditarietà complessa e non necessitano di molti parametri per essere costruiti. Se si ha bisogno di una soluzione più flessibile ed eventualmente più complessa, si consiglia l'utilizzo di Factory Method.
___
## Factory Method

Il *design pattern* **Factory Method** appartiene alla categoria dei **pattern creazionali**, e il suo scopo principale è simile a quello del pattern [[Design pattern#Simple Factory|Simple Factory]] nel voler **centralizzare la costruzione di oggetti**, con la differenza che in questo caso la responsabilità della scelta della classe concreta da istanziare viene delegata a delle sottoclassi, e non a un metodo statico unico e polimorfico.

Tendenzialmente, un'implementazione del pattern Factory Method rispetta una struttura generale che include le seguenti classi:
- una [[Classi#Classi astratte|classe astratta]] o un'[[Interfacce|interfaccia]] **`Product`**, che definisce il contratto da rispettare per le classi da istanziare;
- una serie di classi concrete **`ConcreteProduct`**, che implementano `Product` e che rappresentano le classi da istanziare;
- una classe astratta **`Creator`**, che definisce il metodo astratto `factoryMethod()`, il cui compito è gestire la costruzione dei `Product`, e che contiene eventualmente una logica per l'utilizzo del prodotto;
- delle sottoclassi **`ConcreteCreator`**, che estendono `Creator` andando a definire concretamente il metodo `factoryMethod()` per creare istanze specifiche di una classe `Product`.

Per comprendere meglio l'utilizzo di questo pattern, analizziamo un esempio concreto. Supponiamo di voler creare un sistema per gestire comodamente la costruzione e manipolazione di documenti di vario tipo; per fare ciò, definiamo le seguenti componenti:
- un'interfaccia `Documento`, che rappresenterà la nostra `Product`;
- delle classi concrete come `DocumentoPDF`, `DocumentoWord` ecc. ecc., che rappresenteranno le nostre classi `ConcreteProduct`;
- una classe astratta `DocumentoCreator`, che rappresenterà la nostra `Creator`;
- delle sottoclassi `PDFCreator`, `WordCreator` ecc. ecc., che rappresenteranno le nostre `ConcreteCreator`.

A livello di codice, si andranno a definire i seguenti blocchi:

```
public interface Documento {
	void apri();
}



public class DocumentoPDF implements Documento {
	public void apri() {
		// ISTRUZIONI SPECIFICHE
	}
}

public class DocumentoWord implements Documento {
	public void apri() {
		// ISTRUZIONI SPECIFICHE
	}
}



public abstract class DocumentoCreator {
	public abstract Documento creaDocumento();

	public void gestisciDocumento() {
		Documento doc = creaDocumento();
		doc.apri();
	}
}



public class PDFCreator extends DocumentoCreator {
	public Documento creaDocumento() {
		return new DocumentoPDF();
	}
}

public class WordCreator extends DocumentoCreator {
	public Documento creaDocumento() {
		return new DocumentoWord();
	}
}
```

Quello che avviene in questo esempio è che viene creata un'interfaccia `Documento` che definisce i metodi che devono necessariamente avere le sottoclassi che la implementano (in questo caso, una logica di apertura); in seguito, si definiscono due sottoclassi `DocumentoPDF` e `DocumentoWord` che implementano tale interfaccia e definiscono una variazione specifica del metodo `apri()`; a questo punto, si va a creare anche una classe astratta `DocumentoCreator`, che impone a sue eventuali sottoclassi di implementare un metodo `creaDocumento()`, e che fornisce anche un metodo `gestisciDocumento()` per incapsulare comodamente la creazione e l'apertura dello stesso; infine, si creano le sottoclassi `PDFCreator` e `WordCreator`, che definiscono l'implementazione specifica del metodo `creaDocumento()`, in modo che ognuna di esse istanzi il documento del tipo corrispondente.

Confrontandolo con il pattern Simple Factory, il Factory Method risulta essere **più estendibile** e **più flessibile** della sua controparte semplificata, oltre a sfruttare in maggior misura il principio dell'**[[Java e la OOP#Ereditarietà|ereditarietà]]**; allo stesso tempo, tuttavia, risulta essere per natura **molto più complesso**, sia a livello di implementazione che di manutenzione.

Per questi motivi, è consigliabile utilizzare il pattern Factory Method in casi specifici dove si presenta necessariamente una **gerarchia complessa di prodotti**, o quando si vuole creare una base più facilmente estendibile in caso di aggiunta di numerose nuove tipologie di prodotti.
___
## Builder

Il *design pattern* **Builder** appartiene alla categoria dei **pattern creazionali**, e il suo scopo principale è quello di **rendere più leggibile e semplificata la creazione di oggetti complessi**, evitando l'utilizzo di costruttori con troppi parametri e separando la configurazione di quest'ultimi.

Generalmente, un'implementazione del pattern Builder rispetta una struttura che comprende le seguenti componenti:
- una classe **`Product`**, che consiste nella classe dell'oggetto che si vuole costruire (tipicamente, il costruttore viene definito come [[Modificatori d'accesso#Private|privato]]);
- una classe **`Builder`**, spesso definita come [[Classi#Classi annidate|classe statica interna]] a `Product`, che gestisce la costruzione di un oggetto di quest'ultima classe.

Vediamo un esempio di applicazione di tale pattern. Supponiamo di avere una classe `Computer`, che presenta vari campi come `CPU`, `GPU`, `RAM`, `SSD` e `hasWifi`; piuttosto che gestire la costruzione di una sua istanza tramite un costruttore pubblico, è possibile definire una classe statica interna, ottenendo il seguente codice:

```
public class Computer {

	private final String CPU, GPU;
	private final int RAM, SSD;
	private final boolean hasWifi;

	private Computer(Builder builder) {
		this.CPU = builder.CPU;
		this.GPU = builder.GPU;
		this.RAM = builder.RAM;
		this.SSD = builder.SSD;
		this.hasWifi = builder.hasWifi;
	}

	public static class Builder {
		private final String CPU, GPU;
		private final int RAM, SSD;
		private final boolean hasWifi;

		public Builder CPU(String cpu) {
			this.CPU = cpu;
			return this;
		}

		public Builder GPU(String gpu) {
			this.GPU = gpu;
			return this;
		}

		public Builder RAM(int ram) {
            this.RAM = ram;
            return this;
        }

        public Builder SSD(int ssd) {
            this.SSD = ssd;
            return this;
        }

        public Builder hasWifi(boolean wifi) {
            this.hasWiFi = wifi;
            return this;
        }

        public Computer build() {
            return new Computer(this);
        }
	}
}
```

In questo modo, invece di istanziare un `Computer` mediante un costruttore molto lungo e contenente un alto numero di parametri obbligatori, si può sfruttare l'oggetto `Builder` per andare a costruire pezzo per pezzo l'istanza in questione. Ad esempio, con questo approccio, la costruzione di un `Computer` assume le seguenti sembianze:

```
Computer pc = new Computer.Builder()
		.CPU("Intel i9");
		.GPU("NVIDIA RTX 4090");
		.RAM(32);
		.SSD(1000);
		.hasWifi(true);
		.build();
```

Così facendo, non solo il codice risulta molto più leggibile ma anche più flessibile, dato che si può tranquillamente scegliere di omettere alcuni di questi metodi "setter" intermedi e quindi alcuni attributi dell'istanza. Inoltre, la presenza di un metodo `build()` che gestisce la costruzione finale permette di effettuare eventuali controlli e validazioni dei dati assegnati al `Builder` prima di istanziare effettivamente l'oggetto.

Si noti che, sotto un certo punto di vista, la pipeline di costruzione di un oggetto nel pattern Builder sembra ricalcare quella della manipolazione di uno [[Stream|stream]] di dati, in quanto entrambi presentano delle **operazioni intermedie** (nel caso del Builder, i vari metodi destinati all'assegnazione di valori alle variabili d'istanza) e un'**operazione terminale** (nel caso del Builder, il metodo `build()`).

Va comunque detto che un'implementazione del pattern Builder non è sempre consigliata, soprattutto se ad essere istanziati sono oggetti semplici che presentano pochi campi, oppure nel caso in cui ci siano molte classi da costruire (in entrambi questi casi, aggiungere per ogni classe un proprio Builder diventerebbe dispendioso e, per certi versi, anche inutile).
___
## Decorator


___
## Observer

Il *design pattern* **Observer** appartiene alla categoria dei **pattern comportamentali**, e il suo scopo principale è quello di **facilitare l'aggiornamento di certi oggetti in base a cambiamenti che avvengono in un altro oggetto**; concretamente, un'applicazione corretta di questo pattern va a definire una **relazione uno-a-molti**, in modo che quando un certo oggetto (il "**Subject**") cambia stato, esso notifichi automaticamente tutti gli oggetti che lo stanno "osservando" (gli "**Observer**").

Generalmente, un'implementazione del pattern Observer rispetta una struttura che comprende le seguenti componenti:
- una classe **`Observer`**, che consiste nella classe dell'oggetto "osservante", che tendenzialmente presenta un metodo che verrà chiamato quando viene notificato dall'oggetto "osservato", oppure un qualche altro modo di aggiornare il loro comportamento o i loro dati in base ad esso;
- una classe **`Subject`**, che consiste nella classe dell'oggetto "osservato", che tendenzialmente presenta dei metodi per aggiungere e rimuovere degli `Observer` ad esso, e quindi anche un campo costituito dalla lista di tali `Observer`, così come un metodo per notificare comodamente tutti gli `Observer` legati ad esso.

In alternativa, per un maggior **disaccoppiamento** e una maggiore **modularità**, è possibile anche definire **`Observer` e `Subject` come [[Interfacce|interfacce]]**, e creare delle classi `ConcreteObserver` e `ConcreteSubject` che vanno a implementare quest'ultime.

Vediamo un esempio di applicazione di tale pattern. Supponiamo di voler definire una classe `NewsReader`, che sarà il nostro `Observer`:

```
public class NewsReader {
	private String name;

	public NewsReader(String name) {
		this.name = name;
	}

	public void update(String message) {
		System.out.println(name + " ha ricevuto notizia: " + message);
	}
}
```

Ora, definiamo la classe "osservata", ossia il nostro `Subject`, che chiameremo `NewsAgency`:

```
public class NewsAgency {
	private List<NewsReader> readers = new ArrayList<>();
	private String news;

	public void attach(NewsReader nr) {
		readers.add(nr);
	}

	public void detach(NewsReader nr) {
		readers.add(nr);
	}

	public void notifyReaders() {
		for (NewsReader nr : readers) {
			nr.update(news);
		}
	}

	public void setNews(String news) {
		this.news = news;
		notifyReaders();
	} 
}
```

Grazie a questa implementazione, è possibile aggiungere o rimuovere facilmente degli `Observer` con i metodi `attach()` e `detach()`, e notificare comodamente tutti gli `Observer` legati al `Subject` tramite il metodo `notifyReaders()`, che richiama il metodo `update()` su ognuno degli osservatori e che viene chiamato ogni volta che vengono aggiornate le notizie tramite il metodo `setNews()`.

Come si può facilmente intuire, il *design pattern* Observer risulta particolarmente utile quando **un cambiamento di un oggetto deve influenzare automaticamente altri oggetti**, quando si vogliono **disaccoppiare varie componente** per rendere la struttura del programma più modulare e flessibile, e soprattutto quando si lavora con **GUI reattive e mutevoli**.
___
## Strategy


___
## MVC

Il *design pattern* **MVC**, acronimo che sta per **Model-View-Controller**, può essere definito come un **pattern "architetturale"**. Pur non rientrando tra i 23 pattern ufficiali definiti dal GoF, è molto utilizzato e comune. Il suo scopo principale, come suggerisce il nome, è quello di **suddividere un'applicazione in tre macro-componenti principali**, ossia:
- **Model**, ossia la parte che gestisce la logica dei dati e dello stato del software;
- **View**, ossia la parte responsabile della presentazione di tali dati nonché della GUI;
- **Controller**, ossia la parte destinata alla ricezione di input dall'utente e, di conseguenza, alla modifica e all'aggiornamento di Model e di View.

Più nel dettaglio, le interazioni tra queste tre parti seguono le seguenti strade:
- l'utente interagisce con la View;
- la View, avendo ricevuto input dall'utente, notifica il Controller;
- il Controller elabora l'input ricevuto e aggiorna di conseguenza il Model;
- il Model notifica la View dei cambiamenti imposti dal Controller (o direttamente o attraverso l'implementazione di [[Design pattern#Observer|Observer]]);
- la View aggiorna la GUI in base allo stato aggiornato del Model.

Si tratta, come si evince subito, di un *design pattern* molto più **generale e comprensivo** di altri, che non va tanto a migliorare la progettazione di una particolare componente del proprio codice, ma piuttosto quella dell'intero programma che si sta creando. Un'applicazione strutturata rispettando il pattern MVC è, tendenzialmente, più **modulare**, **mantenibile** e **testabile**.
___