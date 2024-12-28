Le **mappe di Karnaugh**, ideate nel 1953 dall'ingegnere Maurice Karnaugh, rappresentano un metodo per semplificare un'equazione booleana (con al più 4 variabili, superata questa soglia le cose si complicano) di un circuito digitale in maniera grafica.

Analizziamo subito un esempio concreto, per comprendere al meglio il funzionamento di una mappa di Karnaugh (o ***K-map***). Supponiamo di avere la tavola di verità di un circuito a 3 *input*:

![[kmap_example_truth.png]]

Ora, per impostare la mappa di Karnaugh relativa a tale tavola di verità, si crea una tabella che presenterà sulla riga superiore i possibili valori degli *input* A e B (essendo gli *input* considerati 2, i possibili valori saranno 4), e sulla colonna di sinistra i possibili valori dell'*input* C (essendo l'*input* considerato 1, i possibili valori saranno 2). A questo punto, nella tabella risultante, si inserirà in ogni casella il valore di *output* corrispondente agli *input* relativi a tale casella; facendo ciò, si avrà che ogni casella della *K-map* corrisponderà a una riga della tavola di verità, e dunque a un mintermine del circuito considerato. Di seguito, la *K-map* relativa alla tavola di verità dell'esempio, prima scritta in forma classica, poi evidenziando i mintermini corrispondenti:

![[kmap_example.png]]

Nella costruzione di una *K-map*, è importante ricordare di inserire i valori di *input* in un ordine particolare, definito ***gray code***, secondo cui essi vanno inseriti in modo che tra valori adiacenti cambi una sola cifra; ciò porta a variazioni rispetto al classico ordine binario, ma risulterà utile in seguito. Facendo ciò, infatti, ogni casella, o mintermine, presente nella *K-map* differisce da una casella adiacente ad essa di una sola variabile: dunque, caselle adiacenti condividono tutti i loro *literals* tranne uno, che appare nella sua *true form* in una casella e con il suo complemento nell'altra.

Un'altra proprietà interessante delle *K-map* è che sono "**circolari**", nel senso che, ad esempio, le ultime caselle a destra sono considerate adiacenti alle ultime a sinistra (infatti, anch'esse variano di un solo *literal*).

A questo punto, si può notare immediatamente che solo due dei mintermini saranno presenti nell'equazione booleana del circuito, ossia quelli indicati da un 1 nella *K-map*. Si potrebbe, dunque, semplificare l'equazione algebricamente, oppure graficamente lavorando proprio sulla *K-map*. Per fare ciò, basterà:
- raggruppare gli 1 in caselle adiacenti;
- per ogni raggruppamento, segnare l'implicante corrispondente ad esso;
- se all'interno di un raggruppamento è presente una variabile insieme al suo complemento, escludere tale variabile dall'implicante.

Nell'esempio, si cerchieranno gli 1 nelle caselle a sinistra, ottenendo:

![[kmap_example_1.png]]

Essendo inclusi nel raggruppamento sia C che il suo complemento, la variabile C verrà esclusa dall'implicante risultante, che sarà dato dunque solo dai complementi delle variabili A e B. Si è ottenuta, così, l'equazione booleana semplificata che si sarebbe ottenuta lavorando algebricamente sulla tavola di verità.

In generale, per lavorare al meglio anche su mappe e circuiti più complessi, è utile stabilire alcune linee guida, tra cui:
- usare il minor numero di raggruppamenti possibile, e fare in modo che ogni raggruppamento sia il più grande possibile;
- tutte le caselle di un raggruppamento possono contenere solo 1;
- ogni raggruppamento deve contenere 2*ⁱ* caselle (1, 2, 4, 8, ecc. ecc.);
- una casella può essere compresa in più raggruppamenti se fare ciò consente di avere meno raggruppamenti totali.

All'interno di una mappa di Karnaugh, e dunque anche all'interno di una tavola di verità, si possono trovare anche dei *[[Circuiti combinatori|don't care]]* tra gli *output*, nei casi in cui tale *output* è irrilevante per qualche motivo o quando la combinazione di *input* che porterebbe a tale *output* non può verificarsi. Trovare dei *don't care* in una *K-map*, in realtà, può risultare notevolmente comodo, in quanto, all'occorrenza, essi possono essere considerati sia come 0 che come 1, consentendo una maggiore semplificazione logica.