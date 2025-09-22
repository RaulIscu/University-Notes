Essendo Java un linguaggio basato sulla programmazione a oggetti, l'[[MDP_01 - Java e la OOP#Incapsulamento|incapsulamento]] risulta essere un meccanismo fondamentale nel suo funzionamento. Come spiegato in precedenza, l'incapsulamento permette, in parole povere, di collegare facilmente determinati dati con il codice che può manipolarli, e di prevenire un utilizzo errato o delle modifiche non permesse del codice.

È possibile avere maggiore controllo su questo aspetto mediante quello che viene definito "***access control***": la modalità principale in cui si controlla l'accesso a una parte del proprio programma è mediante l'utilizzo dei **modificatori d'accesso**, parole chiave che vengono inserite all'inizio della dichiarazione di tali parti. Di seguito, si analizzeranno i principali modificatori d'accesso utilizzabili in Java, ossia:
- **`public`**;
- **`private`**;
- **`protected`**;
- **package-private**.

## Public

Definire una [[MDP_02 - Classi|classe]], un [[MDP_02 - Classi#Variabili d'istanza, metodi e costruttori|metodo]] o qualsiasi altro blocco di codice come **`public`**, vuol dire sostanzialmente renderlo **accessibile da parte di chiunque**, ossia dalla stessa classe, da eventuali sottoclassi, da altre classi dello stesso package e anche da classi esterne al package in questione.

Tendenzialmente, il modificatore `public` viene utilizzato per classi e metodi che devono essere universalmente visibili, per "*entry-point*" del programma (ad esempio, il metodo `public static void main` da cui parte l'esecuzione di un programma), o addirittura per la scrittura di API.
___
## Private

Definire qualcosa come **`private`**, vuol dire renderlo **accessibile solo all'interno della stessa classe**. Quindi, qualsiasi tentativo di accederci da parte di altre classi, siano esse nello stesso package o meno, o anche di eventuali sottoclassi che estendono quella considerata, fallisce.

Tendenzialmente, il modificatore `private` viene utilizzato per incapsulare dati e logica interni che vengono usati esclusivamente dalla classe in questione, soprattutto per le [[MDP_02 - Classi#Variabili d'istanza, metodi e costruttori|variabili d'istanza]], che convenzionalmente vengono sempre definite come private e che presentano, invece, eventuali metodi pubblici "get" e "set" che regolano la loro visualizzazione e manipolazione.
___
## Protected

Definire qualcosa come **`protected`**, vuol dire renderlo **accessibile all'interno della stessa classe, di tutte le eventuali sottoclassi, e del package** dove si trova la classe in questione.

Tendenzialmente, il modificatore `protected` viene usato per favorire un corretto incapsulamento proprio in relazione alle sottoclassi, consentendo di controllare l'[[MDP_01 - Java e la OOP#Ereditarietà|ereditarietà]] tra classi.
___
## Package-private

Definire qualcosa come **package-private**, vuol dire renderlo **accessibile solo all'interno dello stesso package**; dunque, qualsiasi classe appartenente ad altri package non potrà accedere a tale membro. A differenza degli altri modificatori d'accesso, per definire un membro come package-private basterà semplicemente **omettere qualsiasi modificatore** nella sua definizione.

Tendenzialmente, questa forma di accesso viene usata per aumentare il grado di incapsulamento all'interno di un certo package, regolando la collaborazione tra classi dello stesso. Può essere utile soprattutto in vista dell'applicazione di [[MDP_16 - Design pattern|design pattern]] come Builder o Factory, per definire dei costruttori visibili solo a una factory situata nello stesso package della classe da istanziare.
___