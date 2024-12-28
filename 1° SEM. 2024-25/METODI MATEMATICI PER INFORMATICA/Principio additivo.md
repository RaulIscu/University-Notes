Supponiamo, ad esempio, di voler comporre dei panini, formati da pane, una proteina e una salsa, e di poter scegliere tra 3 tipi di pane, 3 proteine e 4 salse; è possibile suddividere i risultati in categorie, o tipi, in modo che tutti i panini possibili rientrino in una delle categorie. Ad esempio:
- Categoria n°1, o *A*, formata da panini con pane bianco;
- Categoria n°2, o *B*, formata da panini con pane ai semi di sesamo;
- Categoria n°3, o *C*, formata da panini con pane integrale.

Con le condizioni poste in precedenza, ciascuna delle 3 categorie conterrà al suo interno 12 panini possibili. A questo punto, per ottenere il numero di panini possibili totali, basterà sommare il numero di possibilità delle tre categorie; il risultato ottenuto sarà lo stesso dato dallo svolgimento del problema mediante il principio moltiplicativo.

Agendo mediante l’uso di categorie, è importante ricordare che quest’ultime dovranno essere **esaustive** (la somma dei sottoinsiemi-categoria dovrà dare l’insieme totale) ed **esclusive** (ognuna delle possibilità potrà trovarsi in una e una sola categoria).

> Esempio:
  Quante possibili targhe automobilistiche contengono un’unica P in qualsiasi posizione?
  SOLUZIONE: $$(1 * 25 * 10 * 10 * 10 * 25 * 25) * 4 = (10^3 * 25^3) * 4$$
  
Cerchiamo di analizzare il ragionamento fatto sopra. La richiesta iniziale è quella di contare gli oggetti, scelti in un insieme ambiente (nel nostro caso l’insieme di tutte le targhe) che hanno una certa proprietà o soddisfano un certo vincolo (nel nostro caso quello di contenere una unica P). Abbiamo ragionato distinguendo in 4 tipi gli oggetti che soddisfano il vincolo: un oggetto che soddisfa il vincolo ricade in uno dei tipi specificati e un oggetto di uno solo dei tipi specificati sicuramente soddisfa il vincolo.

Generalizzando, in questi casi vale il **principio additivo**, o **principio di partizione**: per contare gli oggetti che soddisfano una certa proprietà, li si può suddividere in categorie, o tipi, mutualmente esclusive ed esaustive, contare la numerosità di ciascun tipo e sommare i numeri trovati.

Per poter formalizzare al meglio tale principio, ricordiamo alcune nozioni insiemistiche fondamentali:
- un **insieme** è una collezione di oggetti non ripetuti e privo di ordine, tipicamente indicato, in matematica, come un gruppo di elementi racchiuso tra parentesi graffe; può essere finito, infinito, o vuoto, e può essere indicato come la totalità degli elementi che rispettano una particolare proprietà;
- un **sottoinsieme** X di un insieme Y (per cui XY) è tale se e solo se tutti gli elementi di X sono anche elementi di Y.

Arriviamo dunque, all’espressione formale del principio additivo: considerando un insieme finito *A* e siano *T1*, *T2*, …, *Tn* sottoinsiemi di *A*, se *T1* ⋃ *T2* ⋃ … ⋃ *Tn* = *A* e suddetti sottoinsiemi sono **mutualmente esclusivi** (l’intersezione tra qualsiasi coppia di sottoinsiemi è l’insieme vuoto), allora il numero di elementi di *A* corrisponde alla somma del numero di elementi dei vari sottoinsiemi di *A*. Una qualsiasi suddivisione dell’insieme di partenza A che rispetta le due condizioni di esclusività ed esaustività è detta **partizione**. In altre parole una partizione di un insieme *A* è una famiglia di sottoinsiemi di *A* tale che l’unione di questi sottoinsiemi coincide con *A* (esaustività) e questi sottoinsiemi sono due a due disgiunti (esclusività).

Ci sono due **casi limite** (o casi banali) del concetto di partizione: 
- se *A* è un insieme allora *A* è una partizione di *A* (in una unica parte, A stesso).
- se *A* = {*a1*, . . . , *an*} è un insieme di *n* elementi, allora {*a1*}, {*a2*}, . . . , {*an*} è una partizione di A (in *n* parti). 
Un insieme contenente un singolo elemento è detto **singoletto**.