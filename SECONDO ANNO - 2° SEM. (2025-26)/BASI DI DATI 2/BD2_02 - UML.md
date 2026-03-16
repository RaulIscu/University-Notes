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
- l'inserimento di **`1..1`** indica che ogni istanza di `Impiegato` deve essere legata a una e una sola istanza di `Città` tramite un link dell'associazione `nascita`.

In questo modo, abbiamo ottenuto un sistema che rispecchia la realtà, dato che un impiegato può nascere in una sola città, ma una città può essere luogo di nascita di un numero indeterminato di impiegati.

Allo stesso modo, riprendendo l'esempio visto in precedenza del sistema progettato per gestire le prenotazioni degli hotel, si potrebbero inserire i seguenti vincoli di molteplicità:

![[dia_classioggetti_esempio6.png]]

Vediamo nel dettaglio cosa implicano tali vincoli: nell'associazione `hotel_prenotato`, si specifica come una prenotazione specifica debba essere legata a uno e un solo hotel, mentre un hotel possa avere un numero qualsiasi di prenotazioni; allo stesso modo, nell'associazione `cliente_prenotazione`, si ha che una specifica prenotazione può essere fatta da una e una sola persona, mentre una persona può effettuare un numero qualsiasi di prenotazioni.

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
##### Vincoli di identificazione di classe

Un altro tipo di vincolo di integrità che possiamo introdurre nella base di dati che stiamo progettando, oltre a quelli di [[BD2_02 - UML#Associazioni e link|molteplicità]] visti in precedenza, sono i cosiddetti "**vincoli di identificazione di classe**". Tali vincoli impongono che **non possano coesistere due [[BD2_02 - UML#Classi e oggetti|oggetti]] di una classe che coincidono nel valore di uno o più attributi**. Ad esempio, è possibile definire la seguente [[BD2_02 - UML#Classi e oggetti|classe]] `Persona`:

![[dia_classioggetti_esempio12.png]]

I due simboli `{id1}` e `{id2}` rappresentano due vincoli di identificazione di classe posti su `Persona`: in questo esempio, si impone che non possano esistere due persone con lo stesso codice fiscale, così come non possano esistere due persone che abbiano contemporaneamente lo stesso nome, cognome e data di nascita. Dunque, in generale possiamo dire che, **abbinando a un insieme di attributi il medesimo "indicatore", si impone che gli oggetti non possano essere uguali contemporaneamente su tutti gli attributi di quell'insieme**.

I vincoli di identificazione di classe possono essere applicati anche sui **ruoli che svolge la classe** considerata. Supponiamo, ad esempio, di star costruendo una base di dati per delle università, e si vuole implementare il fatto che non possono esistere due studenti con la stessa matricola nella stessa università; tale vincolo può essere formalizzato in un UML nel modo seguente:

![[dia_classioggetti_esempio13.png]]

Spieghiamo nel dettaglio cosa si intende con questa notazione: innanzitutto, tra `Studente` e `Università` sussiste un vincolo di molteplicità che impone che a ogni studente possa essere iscritto a una e una sola università, ma che un'università possa ospitare un numero qualsiasi di studenti; più nel dettaglio, il vincolo di identificazione di classe è attinente all'associazione tra uno studente e un'università, e dunque impone che non possano esistere due studenti con la stessa matricola se essi sono iscritti alla stessa università (dunque, se si trovano in università diverse, ciò è perfettamente possibile).
___
##### Ereditarietà e generalizzazioni

Finora, abbiamo implicitamente assunto che le classi fossero tutte entità indipendenti (anche se sussistono [[BD2_02 - UML#Associazioni e link|associazioni]] tra di loro, non sono mai associazioni di tipo "ontologico", non riguardano l'essenza vera e propria delle classi coinvolte) e che due classi diverse non avessero mai oggetti in comune. In molte situazioni, però, potrebbe fare comodo rappresentare il fatto che **una classe sia sottoinsieme di un'altra**: ciò è in realtà possibile nell'UML, implementando una relazione di "**ereditarietà**". La relazione di ereditarietà tra due classi assegna il ruolo di "**superclasse**" a una e di "**sottoclasse**" all'altra, implicando che la sottoclasse derivi in qualche modo dalla superclasse, che sia una sorta di specializzazione di quest'ultima. Nell'UML, la relazione di ereditarietà assume la seguente forma:

![[dia_classioggetti_esempio14.png]]

La relazione di ereditarietà viene anche chiamata **relazione "is-a"** (letteralmente "è un"), nel senso che **ogni istanza della sottoclasse è anche istanza della superclasse**: ad esempio, ogni studente è ovviamente anche una persona. Non vale, però, il contrario, e dunque non ogni persona è uno studente (per evitare confusioni, leggere la relazione is-a seguendo il verso della freccia nel diagramma, dato che la sottoclasse punta sempre alla superclasse).

Nel contesto di relazioni is-a, vige il **meccanismo dell'ereditarietà**, secondo il quale **la sottoclasse "conserva" e amplia le caratteristiche della superclasse**. Si guardi, ad esempio, il seguente diagramma:

![[dia_classioggetti_esempio15.png]]

Si noti che la classe `Persona` (per adesso, ignoriamo `Studente` e l'associazione tra le due classi) presenta due attributi `nome` e `genere`, così come un'associazione `nascita` con la classe `Città`, e dunque informalmente che nella base di dati considerata una persona dispone di un nome, di un genere e di una e una sola città di nascita. A questo punto, notiamo che `Studente` è una sottoclasse di `Persona`: per il meccanismo dell'ereditarietà, ciò vuol dire che ogni studente disporrà di un nome, di un genere e di una città di nascita, e oltre a ciò di una `matricola` ed eventualmente di un `Tutor`. Insomma, la classe `Studente` eredita le caratteristiche di `Persona` (attributi e associazioni) e le amplia aggiungendo le proprie.

L'ereditarietà funziona anche su più livelli, ed è infatti una **relazione transitiva**: ad esempio, potremmo ampliare il diagramma appena visto aggiungendo una classe `StudenteStraniero` come sottoclasse di `Studente`, e tale classe sarebbe sottoclasse sia di `Studente` che, per transitività, di `Persona`. 

**Un oggetto può essere istanza di più di una classe**, e non ci sono vincoli sulle relazioni di ereditarietà che sussistono tra tali classi: dunque, in un contesto del genere, definiamo "**classi più specifiche**" dell'oggetto le **classi di cui esso è istanza che non sono a loro volta superclassi**. Ad esempio, nel seguente diagramma:

![[dia_classioggetti_esempio16.png]]

l'oggetto `anna` è istanza di `Persona`, di `Studente` e di `Lavoratore`, ma solo le ultime due rappresentano le classi più specifiche di `anna`.

Specifichiamo, infine, che nell'UML vale l'**ereditarietà multipla**: dunque, **una classe può essere sottoclasse di più classi**, anche se quest'ultime non sono a loro volta legate da relazioni is-a.

Oltre all'ereditarietà tipica che abbiamo visto finora, l'UML fornisce anche un tipo di relazione is-a più complesso: la **generalizzazione**. Sostanzialmente, la generalizzazione permette di **definire che le istanze di una classe possano essere istanze di più sottoclassi secondo uno stesso criterio concettuale**; in parole povere, le generalizzazioni permettono di definire gruppi di sottoclassi che "specializzano" la superclasse in base a uno stesso criterio. Ad esempio, si potrebbe costruire il seguente diagramma:

![[dia_classioggetti_esempio17.png]]

dove `Studente` e `Lavoratore` sono entrambe sottoclassi di `Persona`, e in cui il criterio secondo il quale le persone sono studenti o lavoratori è quello dell'`occupazione`, come specificato nel diagramma stesso. Chiariamo che, con una generalizzazione del genere, è perfettamente possibile che un oggetto sia istanza di `Studente` e di `Lavoratore` contemporaneamente. Non c'è un vincolo a quante generalizzazioni si possono implementare, dunque **una stessa classe può essere superclasse di generalizzazioni distinte e indipendenti**, cioè basate su criteri diversi, come nel seguente esempio:

![[dia_classioggetti_esempio18.png]]

In alcuni casi, vorremmo applicare delle condizioni più stringenti alle generalizzazioni: ad esempio, si potrebbe voler **evitare che un oggetto sia istanza di più di una sottoclasse della generalizzazione**; oppure, in altri casi potremmo voler fare in modo che **ogni oggetto della superclasse debba necessariamente essere istanza di almeno una delle sottoclassi della generalizzazione**. Queste due esigenze vengono rispettivamente soddisfatte da due vincoli che possiamo imporre alle generalizzazioni:
- **`disjoint`**;
- **`complete`**.

Dunque, una generalizzazione `disjoint` fa in modo che ogni istanza di una delle sottoclassi della stessa non possa essere anche istanza di una qualche altra sottoclasse. Ad esempio, definendo come `disjoint` la generalizzazione di genere fatta nell'esempio precedente, evitiamo che un oggetto della classe `Uomo` possa essere anche istanza della classe `Donna`, e viceversa. Al tempo stesso, una generalizzazione `complete` fa in modo che ogni istanza della superclasse debba necessariamente essere anche istanza di almeno una delle sottoclassi della generalizzazione. Ad esempio, definendo come `complete` la generalizzazione di genere fatta nell'esempio precedente, facciamo in modo che un oggetto della classe `Persona` debba necessariamente essere anche istanza o di `Uomo` o di `Donna`.

Questi due vincoli possono anche verificarsi contemporaneamente: **è possibile**, dunque, **che una generalizzazione sia disgiunta e completa contemporaneamente**, implicando che **ogni istanza della superclasse sia anche istanza di esattamente una sottoclasse della generalizzazione**. Ad esempio, trasformando nel modo seguente le generalizzazioni dell'esempio precedente:

![[dia_classioggetti_esempio19.png]]

ogni istanza di `Persona` deve essere anche istanza di esattamente una sottoclasse tra `Uomo` e `Donna`, così come deve essere anche istanza di esattamente una sottoclasse tra `Studente` e `Lavoratore`. Possiamo schematizzare le varie possibili combinazioni di vincoli sulle generalizzazioni nella seguente immagine:

![[dia_classioggetti_esempio20.png]]
___
##### Operazioni di classe

Finora, parlando di [[BD2_02 - UML#Classi e oggetti|classi]], abbiamo parlato solo di **proprietà statiche** come attributi e [[BD2_02 - UML#Associazioni e link|associazioni]], ossia di proprietà i cui valori cambiano solo in seguito a un esplicita modifica da parte degli utenti o del sistema. Una classe UML, però, può definire anche delle **proprietà dinamiche**, che si presentano sottoforma di "**operazioni**". 

Sostanzialmente, un'operazione è un modo per **calcolare dei valori ogni volta che servono, a partire dai valori di altre proprietà**. Dunque, un'operazione di una determinata classe indica che su ogni oggetto di tale classe si può eseguire un determinato calcolo, che può:
- restituire un valore a partire da altri dati o operazioni;
- modificare le proprietà dell'oggetto considerato, dei link in cui è coinvolto o eventualmente anche degli oggetti collegati ad essi.

Va chiarito che le operazioni, così come definite nel contesto delle UML, sono diverse dai metodi visti nella programmazione a oggetti, anche se si tratta di due concetti collegati: si possono vedere i **metodi come implementazioni concrete delle operazioni**.

Per segnare un'operazione all'interno di una classe UML, si segue una **sintassi** ben precisa:

```
nome_operazione(argomenti): tipo_ritorno
```

dove **`nome_operazione`** è, banalmente, il nome dell'operazione, che dovrà dunque essere utilizzato per riferirsi ad essa, **`argomenti`** è una lista di elementi nella forma `nome_argomento : tipo_argomento`, e **`tipo_ritorno`** è il tipo del valore restituito dall'esecuzione dell'operazione. Gli argomenti, in particolare, sono proprio i dati che l'operazione riceverà in input per restituire l'output. I tipi degli argomenti e del valore di ritorno possono essere tipi di dato concettuali oppure classi del diagramma. Nel diagramma seguente, si vede un esempio di classi al cui interno sono definite anche delle operazioni:

![[dia_classioggetti_esempio21.png]]

Per **invocare un'operazione**, sarà necessario un oggetto della classe (tecnicamente, quest'ultimo è un ulteriore argomento); una tipica invocazione di operazione assumerà infatti la seguente forma:

```
oggetto.nome_operazione(argomenti) --> valore_restituito
```

**Il meccanismo dell'[[BD2_02 - UML#Ereditarietà e generalizzazioni|ereditarietà]] si applica anche alle operazioni**: dunque, se un'operazione è definita in una classe, sarà accessibile anche da qualunque oggetto che sia istanza di una sua sottoclasse.
___
##### Specializzazioni di attributi, associazioni ed operazioni

In generale, quando si lavora con [[BD2_02 - UML#Ereditarietà e generalizzazioni|generalizzazioni]], vale la seguente proprietà: **in una generalizzazione, una sottoclasse può "[[BD2_02 - UML#Tipi di dato concettuali|specializzare]]" le proprietà ereditate dalla superclasse**, restringendone il tipo. 

Vediamo un esempio di questo tipo di specializzazione di attributi. Supponiamo di voler modellare un sistema per la gestione di articoli in vendita, di cui alcuni sono nuovi e alcuni no, e si vuole specificare in particolare che gli articoli nuovi hanno una garanzia di almeno due anni, mentre ciò non è garantito per gli altri articoli (possono comunque avere una garanzia). In questo contesto, si potrebbe creare un diagramma che implementa proprio il meccanismo di cui abbiamo appena parlato: si può creare una classe `ArticoloInVendita` che faccia da superclasse a una generalizzazione che include la sottoclasse `ArticoloNuovo`, e fare in modo che quest'ultima specializzi un attributo `anni_garanzia`, come si può vedere nella seguente immagine:

![[dia_classioggetti_esempio22.png]]

Si deve, però, tenere a mente una cosa: **il tipo dell'attributo specializzato deve essere sempre più ristretto del tipo di attributo iniziale**; ad esempio, se l'attributo `anni_garanzia` nella sottoclasse fosse stato di tipo Reale, si avrebbe avuto un diagramma UML non ammesso.

È possibile anche **specializzare delle associazioni con attributi**: infatti, l'associazione con attributi viene detta anche "classe dell'associazione" (o "association class"), e in quanto classe essa può essere terminale di [[BD2_02 - UML#Associazioni e link|associazioni]] così come radice di [[BD2_02 - UML#Ereditarietà e generalizzazioni|relazioni is-a]] e generalizzazioni. Ad esempio, ampliando l'esempio precedente, supponiamo di voler aggiungere al modello il fatto che ogni articolo debba essere venduto da esattamente un utente, e che gli articoli nuovi possano essere venduti solo da venditori professionali: per affrontare il primo punto, potremmo semplicemente aggiungere una classe `Utente` e associarla alla classe `ArticoloInVendita`, magari tramite un'associazione con attributi per specificare anche quando è avvenuta la transazione; per affrontare il secondo punto, invece, si possono creare delle sottoclassi nel modo seguente:

![[dia_classioggetti_esempio23.png]]

Bisogna fare particolare attenzione, in questi contesti, ai **vincoli di molteplicità associati alle specializzazioni di associazioni**. Supponiamo, ad esempio, che nell'esempio appena visto si modifichino i vincoli di molteplicità nel modo seguente:

![[dia_classioggetti_esempio24.png]]

Tecnicamente, il diagramma in questa forma impone a ogni articolo in vendita di essere venduto da esattamente un utente, ma al tempo stesso permette agli articoli nuovi di essere venduti da "almeno" un venditore professionale: quest'ultimo vincolo risulta però fuorviante, dato che, essendo `ArticoloNuovo` una sottoclasse di `ArticoloInVendita`, e `VenditoreProfessionale` una sottoclasse di `Utente`, ogni articolo nuovo potrà in realtà essere venduto da solo venditore professionale. Allo stesso modo, il seguente diagramma:

![[dia_classioggetti_esempio25.png]]

presenta un'incongruenza: seppur il vincolo sull'associazione tra `ArticoloInVendita` e `Utente` imponga che ogni articolo venga venduto da esattamente un utente, il vincolo sull'associazione tra `ArticoloNuovo` e `VenditoreProfessionale` impone che un articolo nuovo debba essere venduto da almeno 2 venditori professionali; ciò vuol dire che, concretamente, non potranno esistere articoli nuovi nella base di dati.

**Anche le operazioni di classe possono essere oggetto di specializzazione nelle sottoclassi**. In questo caso, per capire al meglio il concetto, si può pensare alla specializzazione delle operazioni come al meccanismo di "**overriding**": nella sottoclasse, ci sarà un metodo con la stessa firma del metodo nella superclasse, ma con un funzionamento più o meno diverso che permetta di sfruttare le informazioni in più date nella sottoclasse. Ad esempio, nel seguente diagramma:

![[dia_classioggetti_esempio26.png]]

vogliamo che l'operazione `prezzo` nella classe `Articolo` calcoli il prezzo dell'articolo in questione, inteso come il prezzo unitario moltiplicato per il numero di pezzi richiesto e incrementato in base alle spese di spedizione relative alla nazione considerata; invece, l'operazione `prezzo` nella classe `ArticoloInOfferta` dovrà restituire il prezzo come calcolato nell'operazione equivalente nella superclasse ma scontato di un certo fattore.

Come per la specializzazione degli attributi, anche la firma dell'operazione specializzata dovrà essere compatibile con quella dell'operazione equivalente nella superclasse: ciò vuol dire che ci dovrà essere lo **stesso numero e tipo di argomenti**, nonché **stesso tipo o sotto-tipo del valore restituito**.
___
## Diagrammi degli use-case

I **diagrammi degli use-case**, a differenza di quelli visti nei [[BD2_02 - UML#Diagrammi delle classi e degli oggetti|paragrafi precedenti]]

include è come una funzione che ne chiama un altra

[SLIDES: A.1, slide 75/83]
___
## Documenti di specifica

I diagrammi UML, seppur uno strumento utile per delineare le caratteristiche principali del sistema che si sta modellando, non permette da solo di avere tutte le informazioni necessarie: ad esempio, un [[BD2_02 - UML#Diagrammi delle classi e degli oggetti|diagramma delle classi]] non definisce nel dettaglio cosa calcolano le operazioni di classe, né come lo fanno, né se e come modificano gli oggetti considerati; allo stesso modo, un [[BD2_02 - UML#Diagrammi degli use-case|diagramma degli use-case]] non definisce quali sono le operazioni effettivamente svolte in corrispondenza di ciascun use-case, né analogamente cosa calcolano o se modificano gli oggetti considerati. Dunque, per precisare al meglio tali caratteristiche, lo standard UML adotta anche i cosiddetti "**documenti di specifica**".

Si tratta, sostanzialmente, di **documenti separati, da abbinare allo schema concettuale, che spiegano meglio dei dettagli specifici**. Possono essere utilizzati in vari contesti, tra cui:
- documenti di **specifica dei tipi di dato**, che definiscono i [[BD2_02 - UML#Tipi di dato concettuali|tipi di dato]] non standard eventualmente utilizzati nello schema concettuale;
- documenti di **specifica di una classe**, che definiscono cosa calcola ogni [[BD2_02 - UML#Operazioni di classe|operazione di classe]], oltre che se e come modifica gli [[BD2_02 - UML#Classi e oggetti|oggetti]] e i [[BD2_02 - UML#Associazioni e link|link]] esistenti;
- documenti di **specifica di uno use-case**, che definiscono l'insieme delle operazioni svolte in corrispondenza di uno use-case, e che per ogni operazione definisce cosa calcola e se e come modifica gli oggetti e link esistenti;
- documenti di **specifica dei vincoli esterni**, che definiscono ulteriori vincoli non esprimibili nel diagramma delle classi che i vari oggetti e link dovranno rispettare.

##### Documenti di specifica dei tipi di dato

I **documenti di specifica dei tipi di dato** sono documenti in cui si forniscono maggiori informazioni sulle caratteristiche di [[BD2_02 - UML#Tipi di dato concettuali|tipi di dato]] non standard, che per un motivo o per un altro si può scegliere di adottare all'interno del sistema che si sta modellando. Ricordiamo, per chiarezza, che questa categoria di tipi comprende:
- tipi di dato **specializzati**;
- tipi di dato **enumerativi**;
- tipi di dato **composti**;
- tipi di dato rappresentati da **espressioni regolari**.

Un esempio di documento di specifica dei tipi di dato potrebbe essere il seguente:

![[specifica_tipidato_esempio.png]]
___
##### Documenti di specifica di una classe

[SLIDES: A.2, slide 4/7]
___
##### Documenti di specifica di uno use-case

[SLIDES: A.2, slide 8 - 9]
___
##### Documenti di specifica di vincoli esterni

[SLIDES: A.2, slide 10/12]
___