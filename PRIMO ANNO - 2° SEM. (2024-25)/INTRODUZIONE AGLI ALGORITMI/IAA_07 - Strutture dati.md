Una "**struttura dati**" può essere definita come un **tipo particolare di dato che ne ospita altri**, caratterizzato più dal modo in cui i dati interni essi sono organizzati piuttosto che dal loro tipo. Dunque, **una struttura dati specifica presenterà un modo sistematico di organizzare i dati** al suo interno, e metterà di conseguenza a disposizione determinati **operatori** che permetteranno di accedere e di manipolare la struttura.

In generale, una struttura dati può essere "**lineare**" o "**non lineare**", a seconda se esista una forma di sequenzialità al suo interno e se, informalmente, possa essere pensata con un inizio e una fine; al tempo stesso, può essere "**statica**" o "**dinamica**", a seconda se la sua dimensione possa variare nel tempo; infine, può essere anche "**omogenea**" o "**disomogenea**", a seconda se ospiti tutti dati dello stesso tipo o meno. 

Comunque sia, **una struttura dati serve a memorizzare e manipolare insiemi dinamici**, ossia insiemi i cui elementi possono variare nel tempo, in base alle operazioni compiute dagli algoritmi che li utilizzano. A loro volta, gli elementi contenuti all'interno dell'insieme dinamico (spesso chiamati **nodi**, **record** o **oggetti**) possono anche essere piuttosto complessi, e contenere ciascuno più di un dato "elementare". In tal caso, è comune che questi elementi contengano:
- una **chiave**, utilizzata per distinguere un elemento da un altro (normalmente, le chiavi vengono scelte da un insieme totalmente ordinato);
- altri "**dati satellite**", associati all'elemento ma spesso non direttamente utilizzati nelle operazioni di manipolazione dell'insieme dinamico.

Nel continuo della nostra trattazione, per semplicità, assumeremo che **ogni elemento coincida con la propria chiave** (a meno che non venga specificato il contrario), e dunque i termini "chiave" e "valore" diventeranno pressoché interscambiabili.

Tipicamente, le **operazioni** che si compiono su un insieme dinamico $S$, e dunque sulla struttura dati che ne permette la gestione, si dividono nelle due categorie di operazioni di interrogazione e operazioni di modifica. Tra le **operazioni di interrogazione**, ossia operazioni che ottengono informazioni sull'insieme ma non ne modificano la forma, alcuni esempi comuni sono:
- **`Search(S, k)`**, che permette di recuperare l'elemento con chiave `k`, se è presente all'interno di `S`, e di restituire un valore speciale nullo in caso contrario;
- **`Min(S)`**, che permette di recuperare l'elemento di valore minimo presente in `S`;
- **`Max(S)`**, che permette di recuperare l'elemento di valore massimo presente in `S`;
- **`Pred(S, k)`**, che permette di recuperare l'elemento presente in `S` che precederebbe quello con chiave `k` se `S` fosse ordinato;
- **`Succ(S, k)`**, che permette di recuperare l'elemento presente in `S` che seguirebbe quello con chiave `k` se `S` fosse ordinato.

Invece, tra le **operazioni di modifica**, ossia operazioni modificano nel concreto la forma dell'insieme, alcuni esempi comuni sono:
- **`Insert(S, k)`**, che permette di inserire l'elemento con chiave `k` in `S` (supponendo di conoscerne, se necessario, la locazione di destinazione);
- **`Delete(S, k)`**, che permette di eliminare l'elemento con chiave `k` da `S` (supponendo di conoscerne la locazione).

Le diverse strutture dati che vedremo in questo capitolo, se da un lato hanno in comune la capacità di memorizzare insiemi dinamici, dall'altro **differiscono profondamente tra loro per le proprietà che le caratterizzano**, e sono proprio queste proprietà a determinare la scelta di struttura dati da effettuare quando si progetta un algoritmo per risolvere un determinato problema.

## Array

Prima di approfondire strutture dati più complesse, dedichiamoci a un'analisi più dettagliata di una struttura già incontrata in precedenza: l'**array**. Possiamo vedere un array semplicemente come una **lista di elementi, ordinati o meno**; a prescindere dall'ordinamento o meno dell'array, si possono attribuire a quest'ultimo alcune caratteristiche:
- un array **memorizza elementi omogenei**, cioè dello stesso tipo;
- è una struttura dati **statica**, dunque la sua dimensione deve essere definita a priori e rimane invariata;
- è una struttura dati **ad accesso casuale**, cioè che permette di accedere ad ogni suo elemento in un tempo costante ($\Theta(1)$), indipendentemente dalla sua locazione.

Avendo chiarito le caratteristiche principali di cui è dotato un array, è opportuno fare un chiarimento: seppur in precedenza si sia assimilata questa struttura dati al tipo `list` di Python, quest'ultimo è in realtà molto più potente e versatile, infatti una `list` non solo non ha una lunghezza statica, ma non deve necessariamente memorizzare elementi omogenei.

##### Operazioni sugli array ordinati e non

Ora, un array ordinato e uno non ordinato supportano generalmente le medesime **operazioni**, tuttavia il discorso cambia per il loro [[IAA_03 - Costo computazionale|costo computazionale]]. Nel seguente elenco, vediamo un quadro generale dell'**implementazione di alcune operazioni di interrogazione sugli array**:
- l'operazione **`Search(S, k)`**, nel caso in cui `S` sia un array non ordinato di dimensione $n$, può essere eseguita solo scorrendo l'array elemento per elemento, dunque il **costo** è pari a **$O(n)$**; se, invece, `S` è un array ordinato, ciò permette l'utilizzo dell'algoritmo di [[IAA_04 - Ricerca#Ricerca binaria|ricerca binaria]], il che porta il **costo** a scendere fino a $O(\log n)$;
- l'operazione **`Min(S)`**, nel caso in cui `S` sia un array non ordinato di dimensione $n$, richiede necessariamente di scorrere l'intero array, dunque avrà un **costo** pari a $\Theta(n)$; se, invece, `S` è un array ordinato, basterà recuperare l'elemento memorizzato nella prima posizione dell'array, il che porta il **costo** ad essere $\Theta(1)$;
- l'operazione **`Max(S)`**, analogamente a `Min(S)`, nel caso in cui `S` sia un array non ordinato di dimensione $n$ richiede necessariamente di scorrere l'intero array, dunque avrà un **costo** pari a $\Theta(n)$; se, invece, `S` è un array ordinato, basterà recuperare l'elemento memorizzato nell'ultima posizione dell'array, il che porta il **costo** ad essere $\Theta(1)$;
- l'operazione **`Pred(S, k)`**, nel caso in cui `S` sia un array non ordinato di dimensione $n$, richiede anche stavolta di scorrere l'intero array, dunque avrà un **costo** pari a $\Theta(n)$; se, invece, `S` è un array ordinato, basterà accedere alla posizione precedente a quella in cui è memorizzato l'elemento `k`, il che porta il **costo** ad essere $\Theta(1)$;
- l'operazione **`Succ(S, k)`**, analogamente a `Pred(S, k)`, nel caso in cui `S` sia un array non ordinato di dimensione $n$ richiede di scorrere l'intero array, dunque avrà un **costo** pari a $\Theta(n)$; se, invece, `S` è un array ordinato, basterà accedere alla posizione successiva a quella in cui è memorizzato l'elemento `k`, il che porta il **costo** ad essere $\Theta(1)$.

Per quanto riguarda **l'implementazione delle principali operazioni di modifica**:
- l'operazione **`Insert(S, k)`**, nel caso in cui `S` sia un array non ordinato, non richiede particolari requisiti per la posizione che assumerà `k` nell'array, dunque basterà posizionare tale elemento nella prima posizione libera trovata, operazione il cui **costo** sarà pari a $\Theta(1)$; se, invece, `S` è un array ordinato di dimensione $n$, l'inserimento di `k` dovrà avvenire mantenendo l'ordinamento degli elementi, pertanto supponendo di aver già individuato la posizione in cui dovrebbe essere inserito `k` bisognerà "fare posto" a tale elemento, spostando tutti gli elementi successivi di una posizione verso destra, il che porta il **costo** dell'operazione a essere $O(n)$;
- l'operazione **`Delete(S, k)`**, nel caso in cui `S` sia un array non ordinato, basterà scambiare l'elemento `k` da cancellare con l'ultimo elemento dell'array (in modo da mantenere l'array privo di "buchi") ed eliminarlo, operazione che avrà **costo** pari a $\Theta(1)$; se, invece, `S` è un array ordinato di dimensione $n$, l'eliminazione di `k` implica anche il dover spostare di una posizione verso sinistra tutti gli elementi successivi, sempre per evitare spazi vuoti all'interno dell'array, e perciò il **costo** diventa $O(n)$.

Possiamo riassumere quanto appena detto nella seguente tabella:

| Struttura dati     | Search(S, k) | Min(S)      | Max(S)      | Pred(S, k)  | Succ(S, k)  | Insert(S, k) | Delete(S, k) |
| ------------------ | ------------ | ----------- | ----------- | ----------- | ----------- | ------------ | ------------ |
| Array non ordinato | $O(n)$       | $\Theta(n)$ | $\Theta(n)$ | $\Theta(n)$ | $\Theta(n)$ | $\Theta(1)$  | $\Theta(1)$  |
| Array ordinato     | $O(\log n)$  | $\Theta(1)$ | $\Theta(1)$ | $\Theta(1)$ | $\Theta(1)$ | $O(n)$       | $O(n)$       |

Da questo semplice confronto, si evidenzia già un concetto che vale per le strutture dati in generale: **una struttura dati non sarà mai "migliore" di un'altra**, e ogni struttura dati può essere più o meno adatta a un certo tipo di algoritmo piuttosto che un altro.
___
## Liste puntate


___
## Pile


___
## Code


___
## Alberi



##### Alberi binari


___
##### Visite di alberi


___
##### Alberi binari di ricerca


___
##### Alberi AVL


___
## Dizionari


___