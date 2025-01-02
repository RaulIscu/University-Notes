Un **circuito sequenziale** è un circuito in cui gli *output* dipendono sia dagli *input* attuali che da quelli precedenti (esso, dunque, "ricorda" gli *input* precedenti a quelli attuali, infatti un circuito sequenziale è dotato di memoria).

In un circuito sequenziale potrebbero essere ricordati degli *input* precisi, oppure essi potrebbero essere condensati in un'informazione riassuntiva chiamata lo "**stato**" del sistema. Lo stato di un circuito è, solitamente, rappresentato da una determinata quantità di bit chiamati "**variabili di stato**", che contengono le informazioni relative al funzionamento passato del circuito necessarie per definire il funzionamento futuro dello stesso.
___
Il componente fondamentale di un circuito dotato di memoria, e dunque anche di un circuito sequenziale, è un "**elemento bistabile**", ossia un elemento che presenta due stati stabili e distinti. Un esempio basilare di un elemento del genere è il seguente:

![[bistable_example.png]]

Come si può notare immediatamente, questo piccolo circuito è costituito da due porte *NOT*, collegate in un *loop*; possiamo affermare che le due porte in questione sono "***cross-coupled***", in quanto l'*output* di una è l'*input* dell'altra e viceversa. Il circuito non presenta *input*, tuttavia tecnicamente presenta due *output*, ossia Q e il suo complemento. Possiamo visualizzare meglio questa proprietà in un'implementazione equivalente:

![[bistable_example1.png]]

Essendo un circuito ciclico, Q dipenderà dal suo complemento e viceversa. Cerchiamo, dunque, di analizzare il circuito in base a due casistiche, Q = 0 e Q = 1:
- se Q = 0, la porta I2 riceverà in *input* Q e ritornerà il suo complemento, ossia 1, che verrà ricevuto a sua volta come *input* da I1, che ritornerà Q, ossia 0;
- se Q = 1, la porta I2 riceverà in *input* Q e ritornerà il suo complemento, ossia 0, che verrà ricevuto a sua volta come *input* da I1, che ritornerà Q, ossia 1.

Si noti che entrambe le casistiche hanno un risultato finale che coincide con le condizioni stabilite inizialmente: ciò vuol dire che entrambi i casi sono "**stabili**"; inoltre, essendoci due stati stabili per il circuito, si può affermare che esso sia effettivamente bistabile.

In generale, un elemento con *N* stati stabili può "trasportare" un numero di bit di informazione pari a log₂*N*. Dunque, un elemento bistabile come quello appena analizzato trasporta un bit di informazione, che in questo caso corrisponde all'*output* Q: infatti, conoscere il valore della variabile Q ci consente di sapere tutto il necessario sul passato funzionamento del circuito per predire e conoscere accuratamente il suo funzionamento futuro. Questo perché, se sappiamo che Q = 0, vorrà dire che anche in futuro Q rimarrà sempre 0, e lo stesso vale se Q = 1. Anche il complemento di Q è una variabile di stato accettabile, ma la sua considerazione insieme a Q non aggiungerà informazioni ulteriori, dunque sceglierne una rende l'altra trascurabile.
___
Circuiti sequenziali come quello appena analizzato, seppur utili per conservare un bit di informazione, non sono molto pratici, in quanto non presentano *input*, e dunque non possono essere effettivamente controllati. Altri componenti, invece, consentono questo controllo proprio disponendo di *input* manipolabili: i più comuni e diffusi sono i *[[Latch|latch]]* e i *[[Flip-flop|flip-flop]]*.