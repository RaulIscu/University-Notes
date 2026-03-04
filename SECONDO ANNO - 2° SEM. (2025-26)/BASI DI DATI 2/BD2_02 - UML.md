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

LE CLASSI DI PROGRAMMAZIONE NON SONO LE CLASSI DEGLI UML. [A.1: slide 4 - 5] Un oggetto UML rappresenta un qualche elemento che, nel mondo reale, è identificabile; si rappresenta in un diagramma come una "scatola" divisa in 3 fette:
1. identificatore di oggetto (una qualsiasi stringa di testo, non ha un significato concreto serve solo per indicare quell'oggetto in particolare) 

ha vita propria = ha una sua individualità, non si confonde con altro

[fino a A.1: slide 42]
___