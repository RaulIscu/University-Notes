Per poter progettare basi di dati e, conseguentemente, applicazioni concrete, il linguaggio **UML** (**Unified Modeling Language**) rappresenta uno strumento potente e universalmente riconosciuto.

## Storia dell'UML

Ma cos'è concretamente l'UML? Probabilmente si è già incontrato qualcosa del genere nello studio della programmazione a oggetti, dove uno schema UML può essere utilizzato per formalizzare le caratteristiche di varie classi nonché il collegamento tra di esse. In realtà, **l'UML è uno standard molto più vasto** di quello visto finora: possiamo intenderlo come una sorta di "**dizionario**" per la progettazione di applicazioni e basi di dati.

L'UML come lo intendiamo al giorno d'oggi nasce nel **1994**: fino ad allora, gli ingegneri del software usavano approcci diversi per fare analisi concettuale e per progettare applicazioni: si utilizzavano schemi e regole eterogenee, non uniformi, e dunque la comunicazione e la condivisione era assai difficile. Ciò cominciò a cambiare proprio con il progetto UML, che ambiva a **standardizzare la progettazione**; inizialmente, l'UML nasce come **unificazione di tre metodologie di analisi concettuale**:
- il metodo **Booch**;
- il metodo **Rumbaugh**;
- il metodo **Jacobson**.

A partire dal 1994, passando per il nuovo millennio e **fino** all'incirca **al 2005**, lo standard viene aggiornato a cadenza regolare, man mano ampliato e perfezionato; al tempo stesso, però, l'UML stava diventando relativamente complesso e, per certi versi, sembrava un'astrazione "inutile" di un problema a cui si potevano trovare soluzioni più semplici. Dunque, a partire dalla versione 2.0, rilasciata proprio nel 2005 e che ha portato ingenti cambiamenti allo standard, comincia a scemare l'attenzione verso l'UML, attenzione che risalirà solo dopo anni (l'UML continuerà comunque ad essere aggiornato più o meno regolarmente, anche se andando avanti la frequenza è diminuita, con l'ultimo aggiornamento degno di nota costituito dalla versione 2.5.1 rilasciata nel 2017).

Al giorno d'oggi, l'UML definisce un totale di **14 tipi di diagrammi**, che permettono di modellare l'applicazione sotto prospettive diverse. Questi 14 tipi possono essere divisi innanzitutto in tre macro-categorie:
- **diagrammi strutturali**;
- **diagrammi comportamentali**;
- **diagrammi architetturali**.

A loro volta, ciascuna di queste categorie include più tipi di diagramma: i diagrammi strutturali sono principalmente costituiti da diagrammi delle classi e degli oggetti; i diagrammi comportamentali possono presentarsi come diagrammi degli use-case, diagrammi degli stati e delle transizioni, diagrammi di sequenza e collaborazione, o "activity diagrams"; infine, tra i diagrammi architetturali troviamo i "component diagrams" e i "deployment diagrams". In questo corso, ci concentreremo soprattutto su **diagrammi delle classi** (si chiarisce fin da subito che, parlando di "classi", non intenderemo le classi tipicamente viste nella programmazione, ma piuttosto le articolazioni dei dati di interesse), su **diagrammi degli use-case** (tendenzialmente, servono a spiegare come sono strutturate varie funzionalità dell'applicazione), su **diagrammi degli stati e delle transizioni** ed eventualmente su **documenti esterni** che specifichino meglio il funzionamento di certe parti dell'applicazione (tali documenti non sono, necessariamente, dei diagrammi).
___
## Diagrammi delle classi e degli oggetti

Come abbiamo anticipato nel [[BD2_02 - UML#Storia dell'UML|paragrafo precedente]], uno dei diagrammi più importanti su cui ci concentreremo in questo corso è il **diagramma delle classi e degli oggetti**; in particolare, nella fase di analisi ci si concentra più sulle prime che sui secondi, mentre questi ultimi servono essenzialmente per descrivere singoli elementi particolarmente significativi o per fornire esempi del funzionamento del sistema.

##### Classi e oggetti

Chiariamo meglio cosa si intende con "**classe**" e con "**oggetto**" nel contesto in cui ci troviamo. 

Possiamo vedere una classe come un **tipo di dato ben specifico**, come la **generalizzazione di una determinata entità**: dunque nel definire una classe, definiamo in realtà una sorta di "famiglia" di oggetti omogenei, che se appartengono a tale classe devono necessariamente disporre di determinate caratteristiche (i cosiddetti "**attributi**").

Invece, un'oggetto è un **elemento concreto del dominio di analisi**, una qualche **entità identificabile nel mondo reale**. In generale, un oggetto dovrebbe avere le seguenti caratteristiche:
- ha "**vita propria**", nel senso che ha una sua individualità e una propria "essenza", non rappresentando semplicemente un aggregato di dati e non confondendosi con altro;
- è **identificato univocamente dal suo "identificatore di oggetto"**, che consiste sostanzialmente in una qualsiasi stringa di testo che non ha, in realtà, un significato concreto ed è arbitraria, ma che prende significato proprio come indicatore di un oggetto in particolare;
- è **"istanza" di una classe** (in alcune circostanze, che vedremo in seguito, un oggetto può essere istanza anche di più classi, ma in quei casi si individua comunque una "classe più specifica" che rappresenta meglio l'oggetto considerato).

In un diagramma, sia le classi che gli oggetti si rappresentano con delle "**scatole**", divise orizzontalmente in più parti dove la prima va a contenere l'**identificatore** della classe o dell'oggetto, mentre la seguente contiene, nel caso della classe, un **elenco degli attributi generici** che un oggetto di tale classe deve possedere (con annessi i relativi tipi di dato) e, nel caso dell'oggetto, un **elenco degli attributi specifici** che l'oggetto in questione presenta. Inoltre, per distinguere al meglio tra classi e oggetti, generalmente nei diagrammi UML **gli oggetti hanno l'identificatore sottolineato, mentre le classi no**. Per comprendere meglio come si presenta un tipico diagramma delle classi e degli oggetti, ecco un esempio molto semplice:

![[dia_classioggetti_esempio.png]]

Come abbiamo detto poco fa, ogni oggetto è individuato in maniera univoca dal suo identificatore: ciò permette l'esistenza di **oggetti "identici" ma diversi**, ossia di due o più oggetti che dispongono delle stesse identiche caratteristiche interne ma che, concretamente, sono due oggetti diversi ed entrambi con una propria individualità. Ad esempio, il seguente diagramma:

![[dia_classioggetti_esempio1.png]]

è perfettamente valido, perché anche se i due oggetti `div_comm` e `div_comm_2` sono internamente, in base ai loro attributi, identici, sono a tutti gli effetti due oggetti ben distinti.
___
##### Associazioni e link

Naturalmente, un sistema complesso non può essere modellato in maniera accurata esclusivamente tramite un elenco di classi: va contemplato, infatti, anche **come interagiscono tra loro le varie classi e i rispettivi oggetti**. Questo aspetto viene modellato dalle cosiddette "**associazioni**", che in parole povere rappresentano eventuali **legami tra due o più classi**.

Inoltre, se le associazioni rappresentano i legami tra classi, i "**link**" sono le **istanze delle associazioni**, e dunque rappresentano **legami tra due o più oggetti**. Più formalmente, se $A$ è un'associazione tra le classi $C1$ e $C2$, allora un link che è istanza di $A$ sarà un link tra due oggetti di cui uno è istanza della classe $C1$ mentre l'altro è istanza della classe $C2$. Di seguito, un esempio basilare di applicazione di associazioni e link:

![[dia_classioggetti_esempio2.png]]

A questo punto, specifichiamo per chiarezza che, nel contesto dei diagrammi delle classi e degli oggetti, il livello delle classi e delle associazioni viene anche detto "**livello intensionale**", mentre il livello degli oggetti e dei link viene anche detto "**livello estensionale**".

Come abbiamo detto, i link sono a tutti gli effetti delle istanze delle associazioni; tuttavia, a differenza degli oggetti, **i link non hanno identificatori espliciti**, ma sono **implicitamente identificati dalla coppia di oggetti** che va a collegare. Ciò implica che **non possa sussistere più di un link dello stesso tipo tra una coppia di oggetti**.

Vediamo, ora, un esempio. Supponiamo di voler progettare un'applicazione che permetta ai clienti di prenotare hotel. A livello basilare, avremo bisogno almeno di una classe `Hotel` e di una classe `Persona`, con un'associazione `prenota` che sussista tra persone e hotel (una persona va a prenotare un hotel). Dunque, un possibile diagramma delle classi e degli oggetti per risolvere questo problema potrebbe essere il seguente:

![[dia_classioggetti_esempio3.png]]

Notiamo, tuttavia, un limite di questa implementazione: se, ad esempio, `alice` volesse effettuare una seconda prenotazione presso lo stesso hotel, l'unico modo possibile per fare ciò nel sistema creato sarebbe istanziando un ulteriore link tra `h1` e `alice`, operazione che però abbiamo appena stabilito essere non ammessa, dato che verrebbero istanziati due link identici tra una stessa coppia di oggetti. Per risolvere questo problema, e permettere dunque a una persona specifica di effettuare più di una prenotazione, converrà aggiungere una classe intermedia `Prenotazione`, e piuttosto che prevedere un'associazione diretta tra `Persona` e `Hotel` converrà creare due associazioni, una tra hotel e prenotazioni (possiamo chiamarla `hotel_prenotato`) e una tra persone e prenotazioni (possiamo chiamarla `cliente_prenotazione`). Questa versione migliorata del diagramma precedente assume la seguente forma:

![[dia_classioggetti_esempio4.png]]

Chiariamo, inoltre, che ovviamente **tra le stesse classi possono essere definite più associazioni**. Ad esempio, riprendendo l'esempio delle classi `Libro` e `Persona`, è possibile definire sia un'associazione `autore` che un'eventuale associazione `editore` tra questa stessa coppia di classi.

Ora, un aspetto fondamentale delle associazioni che non abbiamo ancora toccato sono i cosiddetti "**vincoli di molteplicità**". Effettivamente, i sistemi visti finora sono formalmente giusti ma non sempre rispettano la realtà dei fatti: supponiamo, ad esempio, di avere due classi `Impiegato` e `Città`, e di definire un'associazione `nascita` tra di esse per esprimere il fatto che un impiegato è nato in una determinata città; per come l'abbiamo descritto finora, sarebbe perfettamente ammesso un diagramma in cui risulta che un certo impiegato è nato in due città, cosa che però nel concreto è ovviamente impossibile. È proprio per ovviare a questo problema che l'UML prevede la presenza dei vincoli di molteplicità, uno dei tanti tipi di **vincoli di integrità** inseribili in un diagramma delle classi, che **impone delle restrizioni sulla quantità di oggetti coinvolti nell'associazione**. Ad esempio, per "riparare" l'esempio appena visto, si potrebbero inserire dei vincoli di molteplicità del genere:

![[dia_classioggetti_esempio5.png]]

Letteralmente, i numeri inseriti implicano che **ogni istanza di una determinata classe deve essere coinvolta in un numero di link dell'associazione considerata che rientra nell'intervallo specificato**. Nel nostro caso, i vincoli di molteplicità sono interpretabili nel modo seguente:
- l'inserimento di **`0..*`** indica che ogni istanza di `Città` può essere legata a un numero qualsiasi (da 0 a infinito) di istanze di `Impiegato` tramite dei link dell'associazione `nascita`;
- l'inserimento di **`1..1`** indica che ogni istanza di `Impiegato` può essere legata a una e una sola istanza di `Città` tramite un link dell'associazione `nascita`.

In questo modo, abbiamo ottenuto un sistema che rispecchia la realtà, dato che un impiegato può nascere in una sola città, ma una città può essere luogo di nascita di un numero indeterminato di impiegati.

Allo stesso modo, riprendendo l'esempio visto in precedenza del sistema progettato per gestire le prenotazioni degli hotel, si potrebbero inserire i seguenti vincoli di molteplicità:

![[dia_classioggetti_esempio6.png]]

Vediamo nel dettaglio cosa implicano tali vincoli: nell'associazione `hotel_prenotato`, si specifica come una prenotazione specifica possa essere legata a uno e un solo hotel, mentre un hotel possa avere un numero qualsiasi di prenotazioni; allo stesso modo, nell'associazione `cliente_prenotazione`, si ha che una specifica prenotazione può essere fatta da una e una sola persona, mentre una persona può effettuare un numero qualsiasi di prenotazioni.

Introduciamo ora il concetto di **associazione che insiste più volte sulla stessa classe**. Per capire quando questo meccanismo possa essere utile, vediamo un esempio: supponiamo di voler modellare i sovrani di un regno, dove di ogni sovrano ci interessa il nome da regnante, il periodo in cui ha regnato e il predecessore. Sappiamo, banalmente, che avremo bisogno di una classe `Sovrano`, che presenterà come attributi `nome` (il nome da regnante), `inizio` (la data d'inizio del suo regno) e `fine` (la data di fine del suo regno). Ci manca da definire il concetto di "predecessore": per fare ciò, ragioniamo sul fatto che l'eventuale predecessore di un sovrano sarà sempre un sovrano, dunque apparterrà sempre alla classe `Sovrano`, e perciò possiamo definire un'associazione `successione` che insiste sulla stessa classe due volte, nel modo seguente:

![[dia_classioggetti_esempio7.png]]

In questo caso, dato che la classe `Sovrano` gioca due ruoli ben distinti nell'associazione, l'UML ci obbliga a dare dei nomi espliciti ai due ruoli, e dunque ogni link dell'associazione deve diventare una cosiddetta "**coppia etichettata**" (nell'esempio, le due etichette sono `predecessore` e `successore`).

Un'associazione non deve necessariamente essere un semplice legame tra due o più classi: si può, infatti, avere anche un'**associazione con attributi**. Anche stavolta, per capire meglio cosa si intende, partiamo da un esempio concreto: supponiamo di star progettando un sistema che gestisca gli esiti (voti in trentesimi) dei test superati dagli studenti di un corso; il corso, in particolare, è diviso in moduli, e uno studente può superare il test di ogni modulo al più una volta. Si potrebbe pensare a un'implementazione del genere:

![[dia_classioggetti_esempio8.png]]

A questo punto, come si può vedere dall'immagine, rimane il dubbio su dove "memorizzare" il voto con cui si è superato il test. In realtà, nessuna delle due alternative esplicitate ha molto senso, dato che un voto non è né una proprietà locale di uno studente, né di un modulo: in realtà, il voto è una **proprietà specifica dell'associazione tra le due classi**, che ha senso di esistere solo contestualmente all'associazione `test_superato` (il test viene superato con un determinato voto), dunque conviene convertire tale associazione in un'associazione con attributi, nel modo seguente:

![[dia_classioggetti_esempio9.png]]

Si presti, però, attenzione a una cosa: **anche in presenza di attributi, una stessa coppia di oggetti può comunque formare al più un link di una stessa associazione**. Nel nostro caso, ciò previene ad esempio che uno stesso studente superi due volte lo stesso modulo, scenario che banalmente non ha senso.
___
##### Tipi di dato concettuali

Durante l'analisi concettuale, è fondamentale definire il **tipo di ogni attributo**, sia esso di [[BD2_02 - UML#Classi e oggetti|classe]] o di [[BD2_02 - UML#Associazioni e link|associazione]]. Trattandosi di analisi concettuale, si vogliono utilizzare **tipi di dato concettuali**, cioè slegati da eventuali linguaggi di programmazione specifici, e che siano facilmente realizzabili da una qualsiasi tecnologia informatica. In generale, i **tipi base di dato** contemplati sono:
- **Intero**;
- **Reale**;
- **Booleano**;
- **Data**;
- **Ora**;
- **DataOra**.

Spesso, però, questi tipi base non bastano per modellare la realtà in modo accurato. 

Ad esempio, ripescando il sistema progettato alla fine del [[BD2_02 - UML#Associazioni e link|paragrafo precedente]], ossia quello contenente le classi `Studente` e `Modulo` e l'associazione con attributi `test_superato`, possiamo assumere che l'attributo `voto` di `test_superato` sia di tipo Intero, tuttavia ciò permetterebbe ad esempio l'esistenza di voti negativi, che non hanno senso di esistere: per evitare ciò, spesso si fa utilizzo dei cosiddetti "**tipi specializzati**", ossia di **tipi di base su cui sono definiti determinati vincoli**. Ad esempio, per migliorare tale esempio, si può rendere il tipo di `voto` un tipo specializzato tale per cui `voto` possa essere solamente un Intero incluso nell'intervallo $[18,\,30]$, o `18..30`:

![[dia_classioggetti_esempio10.png]]

Utilizzando questo tipo specializzato, il link dell'associazione `test_superato` che possiamo vedere nel [[BD2_02 - UML#Associazioni e link|livello estensionale]] del diagramma diventa non ammesso, proprio perché il valore di `voto` non è incluso nell'intervallo specificato, pur essendo un Intero.

In altri casi, **l'insieme dei possibili valori** di un attributo può essere **molto piccolo**: in tal caso, si può utilizzare un "**tipo di dato enumerativo**", che definisce esplicitamente e completamente l'insieme dei valori possibili per l'attributo in questione. Ad esempio, se dovessimo specificare il genere di una persona, potremmo assegnare alla classe `Persona` un attributo `genere: {maschio, femmina}`, specificando dunque che il genere di una persona possa essere solo maschile o femminile; ancora, se dovessimo per qualche motivo inserire un attributo `continente` in una classe, è opportuno utilizzare un tipo di dato enumerativo come `{Africa, America, Antartide, Asia, Europa, Oceania}`. Si specifica, poi, che i possibili valori di un tipo di dato enumerativo non sono individualmente di un certo tipo base, ma sono piuttosto dei "**simboli**", dunque non andrà specificato un tipo base anche per tali valori. L'UML, formalmente, consente all'analista di **definire nuovi tipi di dato**, che potranno poi essere usati liberamente nello schema concettuale. Perciò, ad esempio, il tipo di dato enumerativo visto poco fa per il genere può essere formalizzato da un nuovo tipo `Genere`, e quindi un attributo di quel tipo può essere direttamente indicato come `genere: Genere`.

È possibile anche definire **tipi di dato composti da più campi**, che possiamo chiamare "**tipi di dato composti**" o più in breve "**tipi record**". Ad esempio, si potrebbe definire un tipo `Indirizzo` definito dall'unione tra i seguenti campi:
- `via: Stringa`;
- `civico: Intero > 0`;
- `cap: Intero > 0`.

Infine, **anche gli attributi di classe e di associazione possono presentare vincoli di molteplicità**: di default, a meno che non venga specificato altro, si assume che tale vincolo sia settato a `1..1`, dunque che un oggetto di tale classe debba avere uno e un solo dato specifico per ogni attributo definito dalla classe; in alternativa, però, si può definire qualsiasi altro vincolo di molteplicità si desideri. Ad esempio, nella seguente classe:

![[dia_classioggetti_esempio11.png]]

si specifica che ogni studente può avere un solo nome e un solo genere, ma una o più email e al massimo un indirizzo.
___