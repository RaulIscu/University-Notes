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

Per poter parlare di "**liste puntate**", è opportuno introdurre il concetto di "**puntatore**". In parole povere, un puntatore è una **variabile che contiene l'indirizzo in memoria di un'altra variabile**; si tratta di uno strumento pressoché necessario per costruire **strutture dati dinamiche** e per **passare parametri per riferimento**.

##### Liste puntate semplici

Una **lista puntata semplice**, spesso detta "**lista semplice**" per comodità, è una struttura dati nella quale **gli elementi sono organizzati in successione**. Si possono attribuire, in generale, a una lista puntata semplice le seguenti caratteristiche:
- l'accesso avviene sempre ad una **estremità della lista**, per mezzo di un puntatore alla testa della stessa;
- è permesso solo un **accesso sequenziale agli elementi** (a differenza degli [[IAA_07 - Strutture dati#Array|array]], le liste puntate non permettono un accesso casuale a uno qualsiasi dei loro elementi);
- è una struttura dati **dinamica**, dunque le sue dimensioni possono variare;
- la successione degli elementi è implementata mediante un **collegamento esplicito di ogni elemento a un altro mediante un puntatore**.

Ogni elemento `p` di una lista puntata, detto anche "**nodo**", è un **[[IAA_07 - Strutture dati|record]] a due campi**:
- un campo **`key`**, contenente l'informazione effettiva associata all'elemento (rappresentato con la notazione `p → key`);
- un campo **`next`**, contenente un puntatore all'elemento successivo della lista (rappresentato con la notazione `p → next`), e nel caso dell'ultimo elemento il puntatore in questione sarà un valore nullo (rappresentato con il simbolo `/`).

Per avere le idee più chiare, possiamo fornire un'implementazione basilare (anche se non perfettamente corretta) di una classe `Nodo`, che rappresenti un elemento della lista puntata semplice, così come dei metodi che permettano di creare una lista puntata semplice a partire da una lista normale e di stampare una lista puntata semplice:

```
class Nodo:
	def __init__(self, key=None, next=None):
		self.key = key
		self.next = next
	
	
def crea(lista):                                # crea lista puntata e restituisce puntatore alla testa
	p = None
	
	for x in lista:
		q = Nodo(x)
		q.next = p
		p = q
	
	return p
	

def stampa(p):                                  # stampa lista puntata da p
	while p:
		print(p.key)
		p = p.next
```
___
##### Operazioni sulle liste puntate semplici

Come abbiamo detto [[IAA_07 - Strutture dati#Liste puntate|in precedenza]], una lista puntata permette esclusivamente un accesso sequenziale ai suoi elementi: questo implica che, in generale, l'**accesso a un qualsiasi dato** di una lista puntata semplice avrà **costo** pari a $O(n)$.

Avendo stabilito ciò, possiamo procedere ad analizzare l'**implementazione di alcune delle operazioni principali** che si possono svolgere su una lista puntata semplice. Ad esempio, un'operazione **`Search(S, k)`** assume la seguente forma:

```
def search(p: puntatore alla testa, k: valore da cercare):
	p_corr = p
	
	while p_corr != None and p_corr → key != k:
		p_corr = p_corr → next
	
	return p_corr
```

In parole povere, il funzionamento di tale implementazione di `Search` è il seguente: partendo dalla testa della lista puntata, dunque dal suo primo elemento, si scorre la lista puntata fino al suo termine (`p_corr != null`) o finché non si trova l'elemento `k` (`p_corr → key != k`); se si terminano gli elementi e `k` non è stato ancora trovato, verrà restituito un valore nullo, mentre se `k` viene trovato la funzione restituisce un puntatore ad esso. Ovviamente, tale operazione risulta avere un **costo** pari a $O(n)$.

Vediamo, ora, un'operazione **`Insert_in_testa(S, k)`**, ossia un'operazione di inserimento dell'elemento `k` in testa alla lista puntata:

```
def insert_in_testa(p: puntatore alla testa, k: valore da inserire):
	if (k != None):
		k → next = p
	
	p = k
	return p
```

Semplicemente, l'operazione `Insert_in_testa` rende l'elemento `k` la nuova testa della lista puntata in questione, e lo fa associando il puntatore alla testa precedente `p` al campo `next` di `k`, e ritornando un puntatore a quest'ultimo. Come si può facilmente dedurre studiando lo pseudocodice, l'operazione di inserimento in testa ha **costo** pari a $\Theta(1)$.

Nell'analizzare questa operazione, e in generale qualsiasi operazione di inserimento di elementi nella lista puntata, risulta evidente che **l'elemento `k` da inserire deve essere a tutti gli effetti un nodo valido**, e deve di conseguenza essere effettuata un'**allocazione di memoria** per tale elemento, in modo che esso possa contenere i campi necessari e supportare le varie operazioni. Nell'implementazione che abbiamo visto nel [[IAA_07 - Strutture dati#Liste puntate|paragrafo precedente]], questa allocazione di memoria avviene mediante l'istruzione `q = Nodo(x)`. 

A questo punto, possiamo pensare a un'ipotetica operazione **`Insert_dopo_d(S, k, d)`**, ossia un inserimento che non aggiunge l'elemento `k` in testa, ma piuttosto dopo un determinato elemento `d`:

```
def insert_dopo_d(p: puntatore alla testa, k: valore da inserire, d: valore dopo cui inserire k):
	if d != None:
		k → next = d → next
		d → next = k
		return p
	else:
		return None
```

In parole povere, la prima cosa che fa la funzione è verificare che il nodo `d` esista veramente, e in caso contrario fermare subito l'operazione. Se invece `d` esiste, procede a inserire `k` dopo di esso in due passaggi: prima rende l'elemento inizialmente successivo a `d` successivo a `k`; poi, rende `k` stesso l'elemento successivo a `d`. Così facendo, si inserirà con successo `k` tra `d` e l'elemento inizialmente successivo a `d`. Essendo la lista puntata semplice una struttura dati non inerentemente ordinata, per trovare al suo interno il nodo `d` dopo cui inserire `k` richiede la sua ricerca, mediante l'operazione **`Search`** vista poco fa: avendo tale operazione un costo di $O(n)$, anche il costo avrà in realtà un **costo** pari a $O(n)$ (se, invece, si suppone di avere già il nodo `d`, il costo stretto dell'operazione `insert_dopo_d` diventa $\Theta(1)$).

Vediamo, infine, l'operazione **`Delete(S, k)`**, che potrà essere utilizzata per eliminare l'elemento `k` dalla lista puntata:

```
def delete(p: puntatore alla testa, k: valore da eliminare):
	if k != None:
		if k == p:
			p = p → next
			return p
		
		p_corr = p
		
		while p_corr → next != k:
			p_corr = p_corr → next
		
		p_corr → next = k → next
	
	return p
```

Notiamo che l'implementazione dell'operazione **include**, al suo interno, **pseudocodice equivalente all'operazione di `Search`**: questo perché, per poter eliminare l'elemento, sarà necessario trovare quello precedente. In parole povere, la funzione controlla prima di tutto (assumendo che `k` esista effettivamente) se `k` è la testa della lista puntata, e in tal caso basterà "tagliare" la testa della lista e restituire il puntatore alla nuova testa; altrimenti, si andrà a trovare il nodo precedente a `k` (nello pseudocodice, tale nodo verrà memorizzato in `p_corr`) e si sostituirà il suo puntatore `next` (inizialmente associato a `k` stesso) con il puntatore `next` di `k`, scollegando a tutti gli effetti `k` dalla lista puntata. Il **costo** dell'operazione sarà pari a $O(n)$.

**Le liste puntate sono strutture dati inerentemente ricorsive**: perciò, tutti gli algoritmi proposti finora possono essere implementati anche sfruttando la [[IAA_05 - Ricorsione#Cos'è un algoritmo ricorsivo?|ricorsione]]. Ad esempio, di seguito vediamo un esempio di implementazione ricorsiva dell'operazione di `Delete`:

```
def delete_ric(p: puntatore alla testa, k: valore da eliminare):
	if p == k:
		p = p → next
	else:
		p → next = delete_ric(p → next, k)
	
	return p
```

[DISPENSE: pag. 12]
___
##### Liste puntate doppie

Alcune inefficienze della [[IAA_07 - Strutture dati#Liste puntate semplici|liste puntate semplici]], ad esempio il costo lineare dell'eliminazione di un elemento, si può modificare tale struttura dati in modo che **ogni nodo disponga sia di un puntatore all'elemento successivo** (**`next`**) **che di un puntatore all'elemento precedente** (**`prev`**). Una struttura dati del genere prende il nome di **lista puntata doppia**, spesso detta anche "**lista doppia**" per semplicità. Una lista puntata doppia ha le stesse proprietà di una lista semplice, con la differenza che **una lista doppia può essere attraversata in entrambe le direzioni**.

In tale struttura dati, le [[IAA_07 - Strutture dati#Operazioni sulle liste puntate semplici|operazioni]] di inserimento e di ricerca rimangono pressoché invariate, ma l'operazione **`Delete`** assume la seguente forma:

```
def delete_doppia(p: puntatore alla testa, k: valore da eliminare):
	if k → prev != None:
		k → prev → next = k → next
	else:
		p = k → next
		
	if k → next != None:
		k → next → prev = k → prev
	
	return p
```

e il **costo** dell'operazione diventa $\Theta(1)$.

Possiamo riassumere i costi delle varie operazioni nelle liste puntate (semplici e doppie) nella seguente tabella:

| Struttura dati         | Search(S, k) | Min(S) | Max(S) | Pred(S, k) | Succ(S, k) | Insert(S, k) | Delete(S, k) |
| ---------------------- | ------------ | ------ | ------ | ---------- | ---------- | ------------ | ------------ |
| Lista puntata semplice | $O(n)$       | $O(n)$ | $O(n)$ | $O(n)$     | $O(n)$     | $\Theta(1)$  | $O(n)$       |
| Lista puntata doppia   | $O(n)$       | $O(n)$ | $O(n)$ | $O(n)$     | $O(n)$     | $\Theta(1)$  | $\Theta(1)$  |

Eventualmente, si può operare un’ulteriore evoluzione della lista doppia: **la lista circolare**, nella quale **il primo e l’ultimo elemento sono collegati fra loro**. Essa può essere utile nelle situazioni in cui si voglia, ad esempio, effettuare una computazione organizzata per fasi, nella quale ciascuna fase richiede la scansione dell’intera struttura dati; inoltre, semplifica l’implementazione delle operazioni standard poiché in esse non è necessario tenere conto dei casi speciali relativi al primo e all’ultimo elemento della lista.
___
## Pile e code

##### Pile

[DISPENSE: pag. 19/24]
[SLIDES: pag. 4/7]
[EXYSS: pag. 98]
___

[DISPENSE: pag. 15/24]
[SLIDES: pag. 4/13]
[EXYSS: pag. 98 - 99]
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