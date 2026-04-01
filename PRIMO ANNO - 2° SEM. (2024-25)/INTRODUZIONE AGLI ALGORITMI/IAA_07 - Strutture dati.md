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
- un campo **`key`**, contenente l'informazione effettiva associata all'elemento (rappresentato con la notazione `p.key`);
- un campo **`next`**, contenente un puntatore all'elemento successivo della lista (rappresentato con la notazione `p.next`), e nel caso dell'ultimo elemento il puntatore in questione sarà un valore nullo (rappresentato con il simbolo `/`).

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
	
	while p_corr != None and p_corr.key != k:
		p_corr = p_corr.next
	
	return p_corr
```

In parole povere, il funzionamento di tale implementazione di `Search` è il seguente: partendo dalla testa della lista puntata, dunque dal suo primo elemento, si scorre la lista puntata fino al suo termine (`p_corr != null`) o finché non si trova l'elemento `k` (`p_corr . key != k`); se si terminano gli elementi e `k` non è stato ancora trovato, verrà restituito un valore nullo, mentre se `k` viene trovato la funzione restituisce un puntatore ad esso. Ovviamente, tale operazione risulta avere un **costo** pari a $O(n)$.

Vediamo, ora, un'operazione **`Insert_in_testa(S, k)`**, ossia un'operazione di inserimento dell'elemento `k` in testa alla lista puntata:

```
def insert_in_testa(p: puntatore alla testa, k: valore da inserire):
	if (k != None):
		k.next = p
	
	p = k
	return p
```

Semplicemente, l'operazione `Insert_in_testa` rende l'elemento `k` la nuova testa della lista puntata in questione, e lo fa associando il puntatore alla testa precedente `p` al campo `next` di `k`, e ritornando un puntatore a quest'ultimo. Come si può facilmente dedurre studiando lo pseudocodice, l'operazione di inserimento in testa ha **costo** pari a $\Theta(1)$.

Nell'analizzare questa operazione, e in generale qualsiasi operazione di inserimento di elementi nella lista puntata, risulta evidente che **l'elemento `k` da inserire deve essere a tutti gli effetti un nodo valido**, e deve di conseguenza essere effettuata un'**allocazione di memoria** per tale elemento, in modo che esso possa contenere i campi necessari e supportare le varie operazioni. Nell'implementazione che abbiamo visto nel [[IAA_07 - Strutture dati#Liste puntate|paragrafo precedente]], questa allocazione di memoria avviene mediante l'istruzione `q = Nodo(x)`. 

A questo punto, possiamo pensare a un'ipotetica operazione **`Insert_dopo_d(S, k, d)`**, ossia un inserimento che non aggiunge l'elemento `k` in testa, ma piuttosto dopo un determinato elemento `d`:

```
def insert_dopo_d(p: puntatore alla testa, k: valore da inserire, d: valore dopo cui inserire k):
	if d != None:
		k.next = d.next
		d.next = k
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
			p = p.next
			return p
		
		p_corr = p
		
		while p_corr.next != k:
			p_corr = p_corr.next
		
		p_corr.next = k.next
	
	return p
```

Notiamo che l'implementazione dell'operazione **include**, al suo interno, **pseudocodice equivalente all'operazione di `Search`**: questo perché, per poter eliminare l'elemento, sarà necessario trovare quello precedente. In parole povere, la funzione controlla prima di tutto (assumendo che `k` esista effettivamente) se `k` è la testa della lista puntata, e in tal caso basterà "tagliare" la testa della lista e restituire il puntatore alla nuova testa; altrimenti, si andrà a trovare il nodo precedente a `k` (nello pseudocodice, tale nodo verrà memorizzato in `p_corr`) e si sostituirà il suo puntatore `next` (inizialmente associato a `k` stesso) con il puntatore `next` di `k`, scollegando a tutti gli effetti `k` dalla lista puntata. Il **costo** dell'operazione sarà pari a $O(n)$.

**Le liste puntate sono strutture dati inerentemente ricorsive**: perciò, tutti gli algoritmi proposti finora possono essere implementati anche sfruttando la [[IAA_05 - Ricorsione#Cos'è un algoritmo ricorsivo?|ricorsione]]. Ad esempio, di seguito vediamo un esempio di implementazione ricorsiva dell'operazione di `Delete`:

```
def delete_ric(p: puntatore alla testa, k: valore da eliminare):
	if p == k:
		p = p.next
	else:
		p.next = delete_ric(p.next, k)
	
	return p
```
___
##### Array, liste puntate semplici e `list` di Python

L'oggetto **`list`**, nel linguaggio Python, ha **somiglianze sia con gli [[IAA_07 - Strutture dati#Array|array]] che con le [[IAA_07 - Strutture dati#Liste puntate semplici|liste puntate semplici]]**: ad esempio, similmente agli array, è possibile accedere agli elementi memorizzati al suo interno tramite la loro posizione, e la sua lunghezza è sempre nota (e ottenibile tramite il comando `len`); invece, come le liste puntate semplici, permette di memorizzare dati non omogenei, dunque di tipo diverso, e la sua lunghezza non è necessariamente fissa.

Questa natura "ibrida" di `list` è possibile grazie alla sua peculiare **implementazione**: ciò che viene fatto, infatti, è **collegare tramite puntatori, elemento per elemento, una lista puntata semplice a un array**. Seppur ciò consenta di ereditare da entrambe le strutture dati alcune proprietà fondamentali, è necessario tenere conto di questa duplice natura quando si calcola il costo delle operazioni semplici che si compiono su una `list`, ad esempio:
- l'operazione di **`append`**, che consiste in un inserimento in ultima posizione, si esegue in tempo pari a $\Theta(1)$;
- l'operazione di **`insert`**, che consiste in un inserimento all'$i$-esima posizione, si esegue in tempo pari a $O(n)$, dato che bisogna far scorrere in avanti tutti gli elementi in posizione successiva all'$i$-esima;
- l'operazione di **`pop`**, che consiste nella rimozione e restituzione dell'elemento in $i$-esima posizione, si esegue in tempo pari a $O(n)$, dato che bisogna far scorrere all'indietro tutti gli elementi in posizione successiva all'$i$-esima;
- l'operazione di **`concatenate`**, che consiste nell'unire due oggetti `list` in uno solo aggiungendo al termine del primo tutti gli elementi del secondo, si esegue in tempo pari a $\Theta(k)$, dove $k$ è il numero di elementi contenuti nella seconda `list`.
___
##### Liste puntate doppie

Alcune inefficienze della [[IAA_07 - Strutture dati#Liste puntate semplici|liste puntate semplici]], ad esempio il costo lineare dell'eliminazione di un elemento, si può modificare tale struttura dati in modo che **ogni nodo disponga sia di un puntatore all'elemento successivo** (**`next`**) **che di un puntatore all'elemento precedente** (**`prev`**). Una struttura dati del genere prende il nome di **lista puntata doppia**, spesso detta anche "**lista doppia**" per semplicità. Una lista puntata doppia ha le stesse proprietà di una lista semplice, con la differenza che **una lista doppia può essere attraversata in entrambe le direzioni**.

In tale struttura dati, le [[IAA_07 - Strutture dati#Operazioni sulle liste puntate semplici|operazioni]] di inserimento e di ricerca rimangono pressoché invariate, ma l'operazione **`Delete`** assume la seguente forma:

```
def delete_doppia(p: puntatore alla testa, k: valore da eliminare):
	if k.prev != None:
		k.prev.next = k.next
	else:
		p = k.next
		
	if k.next != None:
		k.next.prev = k.prev
	
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

La **pila**, detta più comunemente "**stack**", è una struttura dati che si ispira al concetto di una pila di oggetti: inserendo un oggetto nella pila lo andremo ad aggiungere in cima alla stessa, mentre l'oggetto che andremo ad eventualmente rimuovere sarà sempre quello in cima. Più formalmente, la pila è una struttura dati di tipo **LIFO**, cioè "**Last In First Out**". Dunque, una pila ha sempre la seguente proprietà:
- gli elementi **vengono prelevati** dalla pila **nell'ordine inverso rispetto a quello nel quale vi sono stati inseriti**.

Possiamo trovare, senza neanche pensarci troppo, innumerevoli esempi di utilizzo di strutture del genere: nella nostra quotidianità, una **pila di piatti** o **di sedie** segue la stessa proprietà; nel mondo dell'informatica, la pila viene utilizzata dal sistema operativo per **gestire le chiamate a funzione**, o anche per **memorizzare in ordine le pagine web** che abbiamo visitato, in modo da poterle recuperare "tornando indietro".

Approfondiamo meglio l'utilizzo delle pile negli elaboratori, e in particolare nella catena delle **chiamate a funzione**. Supponiamo che un programma in esecuzione voglia effettuare una chiamata a un'ipotetica funzione `A()`: per fare ciò, deve avvenire il cosiddetto "**context switch**", o **cambio di contesto**, grazie al quale il controllo della CPU passa dal flusso di esecuzione corrente alla funzione `A()`. Questo, ad esempio, significa che la funzione `A()` modificherà, tra le altre cose, il "program counter", ossia l'indirizzo di memoria della prossima istruzione da eseguire, e il contenuto dei registri della CPU: queste informazioni, che fanno parte del cosiddetto "**contesto di esecuzione**", dovranno essere salvate prima di passare il controllo ad `A()`, altrimenti, una volta che l'esecuzione di quest'ultima sarà terminata e il controllo dovrà essere restituito al programma chiamante, esso non potrà riprendere l'esecuzione in modo corretto. Ciò vale anche in caso di catene di chiamate a funzione (potrebbe essere che, durante l'esecuzione di `A()`, venga chiamata un'altra funzione `B()`, e così via). Dato che **i ritorni dalle varie chiamate a funzione si verificano esattamente nell'ordine inverso rispetto a quello in cui sono state chiamate**, la struttura dati più naturale da utilizzare per salvare i vari contesti di esecuzione è proprio la pila.

Di seguito, proviamo a visualizzare meglio quanto detto con delle immagini. Supponiamo che la funzione `A()` contenga una chiamata alla funzione `B()`; immediatamente prima che avvenga tale chiamata, il sistema operativo salva su una pila di sistema il contesto di esecuzione di `A()`:

![[pila_esempio.png]]

E se `B()` fa a sua volta una chiamata a una funzione `C()`? Prima di eseguire tale chiamata, verrà salvato nella pila il contesto di esecuzione di `B()`:

![[pila_esempio1.png]]

Supponiamo, ora, che la funzione `C()` termini la propria esecuzione. Prima di restituire il controllo a `B()`, il sistema operativo dovrà recuperare dalla pila di sistema il contesto di esecuzione di `B()` e ricaricarlo nella CPU, nel modo seguente:

![[pila_esempio2.png]]

e lo stesso avverrà al termine dell'esecuzione di `B()`:

![[pila_esempio3.png]]
___
##### Operazioni sulle pile

Tipicamente, una [[IAA_07 - Strutture dati#Pile|pila]] supporta solo **due operazioni**:
- **`Push`**, ossia l'**aggiunta di un elemento** in cima alla pila;
- **`Pop`**, ossia l'**estrazione di un elemento** dalla cima della pila.

**Non è prevista**, invece, **la possibilità di scandire gli elementi** della pila (fare ciò implicherebbe il rimuoverli dalla pila stessa), così come quella di **eliminare elementi con mezzi diversi dalla `Pop`**. 

Naturalmente, **le operazioni di `Pop` e `Push`**, per la natura LIFO della pila, **operano sulla stessa estremità della stessa** attraverso un puntatore o un indice **`top`**, a seconda che la pila sia implementata rispettivamente come una sorta di [[IAA_07 - Strutture dati#Liste puntate|lista puntata]] o come un [[IAA_07 - Strutture dati#Array|array]]. Seppur perfettamente valido e facilissimo da implementare, quest'ultimo approccio si rivela spesso poco conveniente, soprattutto per la dimensione fissa che hanno di norma gli array; invece, il primo approccio è molto più versatile e flessibile, ma implica ovviamente una maggiore difficoltà implementativa, dato che ogni elemento memorizzato dovrà disporre di un puntatore **`next`**, che punterà al prossimo elemento della pila (quello subito più "in basso", per intenderci). In questo contesto, si chiarisce subito che **se il puntatore `top` è pari a `None`, vuol dire che la pila considerata è vuota**.

Di seguito, forniamo dunque un'**implementazione delle operazioni effettuabili su una pila** vedendola implementata mediante liste puntate (si presuppone che l'elemento da inserire sia già creato e con valore `None` nel suo campo `next`):

```
def push_lista(top: puntatore alla cima, e: puntatore all'elemento da inserire):
	e.next = top
	top = e
	return top
	

def pop_lista(top: puntatore alla cima):
	if top == None:
		return None
	
	e = top
	top = e.next
	e.next = None
	return e, top
```

Analizziamo più nel dettaglio cosa fanno queste due operazioni:
- l'operazione **`push_lista`** va ad associare al campo `next` dell'elemento da inserire `e` il puntatore alla cima originaria della pila, e in seguito sovrascrive il puntatore `top` sostituendolo con un puntatore a `e`, rendendo quest'ultimo a tutti gli effetti la nuova cima della pila (tale operazione ha **costo** pari a $\Theta(1)$);
- l'operazione **`pop_lista`** controlla innanzitutto che la pila contenga effettivamente un qualche valore da rimuovere, e in seguito salva nella variabile `e` il puntatore alla cima della pila (ossia all'elemento che stiamo rimuovendo), associa a `top` l'elemento successivo a quello da rimuovere, rendendo tale elemento la nuova cima della pila, "scollega" `e` da quest'ultima (`e . next = None`) e infine restituisce un puntatore all'elemento rimosso e alla nuova cima della pila (tale operazione ha **costo** pari a $\Theta(1)$). 

Come detto a inizio paragrafo, le pile potrebbero essere anche realizzate mediante array, se il numero massimo di elementi da memorizzare è noto a priori. Incappiamo, però, in un problema di efficienza: se implementassimo `top` come l'indice del primo elemento dell'array, le operazioni di `Pop` e `Push` non avrebbero più costo costante, dato che si dovrebbe considerare anche lo spostamento (rispettivamente, verso sinistra e verso destra) di tutti gli altri elementi contenuti nell'array. Per questo motivo, conviene **considerare  `top` come l'indice dell'ultimo elemento conservato nell'array**, cioè quello più a destra, in modo che inserimenti e rimozioni non alterino la posizione degli altri elementi.
___
##### Code

La **coda**, detta anche "**queue**", è una struttura dati che si ispira al concetto di una coda di persone in attesa: inserendo una persona nella coda la andremo ad aggiungere in fondo alla stessa, e al tempo stesso le persone usciranno dalla coda nell'ordine in cui sono entrate. Più formalmente, la coda è una struttura dati di tipo **FIFO**, cioè "**First In First Out**". In altre parole, una coda ha sempre la seguente proprietà:
- gli elementi **vengono prelevati** dalla coda **nello stesso ordine nel quale vi sono stati inseriti**.
___
##### Operazioni sulle code

Tipicamente, come per una [[IAA_07 - Strutture dati#Pile|pila]], una [[IAA_07 - Strutture dati#Code|coda]] supporta solo **due operazioni**:
- **`Enqueue`**, ossia l'**aggiunta di un elemento** in fondo alla coda;
- **`Dequeue`**, ossia l'**estrazione di un elemento** dalla testa della coda.

**Non è prevista**, invece, **la possibilità di scandire gli elementi** della coda, così come quella di **eliminare elementi con mezzi diversi dalla `Dequeue`**.

Per la natura FIFO della coda, a differenza della pila, **le operazioni di `Enqueue` e `Dequeue` non operano sulla stessa estremità della coda**: infatti, l'operazione di `Enqueue` opera sul fondo (**`tail`**) della coda, mentre l'operazione di `Dequeue` opera sulla testa (**`head`**) della coda. Anche nel caso della coda, essa può essere implementata utilizzando una [[IAA_07 - Strutture dati#Liste puntate|lista puntata]] o un [[IAA_07 - Strutture dati#Array|array]]: anche in questo caso, gli array non sono molto convenienti rispetto alle liste puntate, principalmente per la loro dimensione fissa. Nell'implementazione mediante liste puntate, `tail` e `head` sono due puntatori rispettivamente al fondo e alla testa della coda.

Di seguito, forniamo dunque un'**implementazione delle operazioni effettuabili su una coda** vedendola implementata mediante liste puntate (si presuppone che l'elemento da inserire sia già creato e con valore `None` nel suo campo `next`):

```
def enqueue_lista(head: puntatore alla testa, tail: puntatore al fondo, e: puntatore all'elemento da inserire):
	if tail == None:
		tail = e
		head = e
	else:
		tail.next = e
		tail = e
	
	return head, e
	
	
def dequeue_lista(head: puntatore alla testa, tail: puntatore al fondo):
	if head == None:
		return None, None, None
	
	e = head
	head = e.next
	
	if head == None:
		tail = None
	
	return head, tail, e
```

Analizziamo più nel dettaglio cosa fanno queste due operazioni:
- l'operazione di **`Enqueue`** controlla innanzitutto se la coda è vuota (se `tail == None`, vuol dire che non ci sono elementi all'interno della coda), e in tal caso l'elemento `e` da inserire diventerebbe l'unico elemento della coda, motivo per cui è ad esso che punteranno sia `head` che `tail`; invece, se la coda contiene già almeno un elemento, si associa `e` al puntatore `next` dell'elemento originariamente in fondo alla coda, e si aggiorna il puntatore `tail`, rendendo a tutti gli effetti `e` il nuovo fondo della coda; in seguito, si restituiscono `head` e il puntatore a `e` (non viene restituito anche `tail` perché, in seguito a un inserimento, l'elemento inserito è l'ultimo della coda, dunque il puntatore `tail` coincide con il puntatore a tale elemento), terminando l'esecuzione dell'operazione con un **costo** di $\Theta(1)$;
- l'operazione di **`Dequeue`** controlla innanzitutto se la coda è vuota, e in tal caso non essendoci elementi da rimuovere terminerà subito l'esecuzione; in alternativa, andiamo a memorizzare in una variabile `e` il puntatore all'elemento in testa alla coda (sarà l'elemento che vorremo rimuovere e restituire), e rendiamo invece la nuova `head` l'elemento successivo; a questo punto, viene semplicemente effettuato un ultimo controllo per verificare che la nuova testa della coda esista effettivamente (se la coda conteneva un solo elemento, dopo la `Dequeue` essa risulterà vuota, e dunque il puntatore `head` diventerà un valore nullo), e in caso contrario si aggiorna anche il puntatore `tail` in modo appropriato; l'esecuzione viene terminata dopo aver restituito tre puntatori, ossia `head`, `tail` ed `e`, con **costo** complessivo pari a $\Theta(1)$.

Anche le code, come le pile, possono essere implementate anche con gli **array**, se il numero massimo di elementi da memorizzare è noto a priori. Tuttavia, si incappa in un problema: a seguito di ripetute operazioni di `Enqueue` e `Dequeue`, gli elementi della coda si spostano progressivamente verso una delle due estremità dell’array e, quando la raggiungono, non vi è più apparentemente spazio per i successivi inserimenti. La ragione è che, al fine di garantire costo computazionale costante, i dati da estrarre vengono cancellati solo logicamente e non fisicamente: gli elementi estratti tramite `Dequeue` infatti rimangono nell’array ma sono considerati come eliminati grazie all’opportuna posizione degli indici `head` e `tail`. La soluzione a questo problema è gestire l’array in modo circolare, considerando cioè il primo elemento come successore dell’ultimo. Implementando una coda utilizzando un array, è possibile anche contemplare una funzione **`CodaPiena`**, che restituisca `True` se la coda considerata è piena e `False` altrimenti (si può fare lo stesso con una pila implementata mediante array); si tenga a mente, però, che una funzione del genere può esistere solo con questa implementazione specifica, dato che una lista puntata non ha realmente fine, dunque non potrà mai essere "piena".
___
##### Code con priorità

La **coda con priorità** è una variante della [[IAA_07 - Strutture dati#Code|coda]], che si differenzia da quest'ultima per l'**ordine di inserimento degli elementi** al suo interno: la posizione dell'elemento all'interno della coda non dipende dal momento in cui l'elemento è stato inserito al suo interno, ma piuttosto dal valore di una determinata grandezza detta "**priorità**", la quale generalmente è associata a **uno dei campi dell'elemento stesso**. Di conseguenza, **gli elementi di una coda con priorità sono collocati in ordine crescente o decrescente rispetto alla priorità**.

Ad esempio, supponendo di avere una coda con priorità crescente dove la priorità viene associata al valore del campo `key`, quando un nuovo elemento avente `key = x` viene inserito nella coda esso viene collocato come predecessore del primo elemento che abbia il valore `key` maggiore o uguale a `x`. Se, invece, la coda contiene solo elementi con priorità minore a quella dell'elemento che viene inserito, esso diverrà l'elemento in testa alla coda, dunque il primo che verrà eventualmente estratto (essendo quello con priorità maggiore). In questo senso, **un [[IAA_07 - Strutture dati#Array|array]] ordinato può essere visto come una coda con priorità**, in cui la priorità coincide con la chiave dell'elemento. 

Un altro esempio di coda con priorità è la struttura dati **heap**, che abbiamo già incontrato studiando gli [[IAA_06 - Algoritmi di ordinamento#Heap Sort|algoritmi di ordinamento]]. Anche una **coda** può essere intesa come una coda con priorità, in cui il parametro di priorità è il maggior tempo di permanenza nella struttura dati. Viceversa, la **pila** è una coda con priorità dettata dal minor tempo di permanenza nella struttura. Si noti che la coda con priorità presenta un potenziale pericolo di "**starvation**" (detta anche "**attesa illimitata**"): un elemento potrebbe non venire mai estratto, se viene continuamente scavalcato da altri elementi di priorità maggiore che vengono via via immessi nella struttura dati.
___
##### Pile, code e `list` di Python

Volendo implementare la funzionalità della **[[IAA_07 - Strutture dati#Pile|pila]]**, possiamo sfruttare i metodi della **classe `list` di Python** così come sono, infatti:
- `append()` corrisponde all’operazione di `push()`;
- `pop()` esiste sia per le liste di Python che per le pile.

Inoltre, entrambi questi metodi possono essere eseguiti in **tempo costante**. Non altrettanto si può dire per la **coda**: i metodi `append()` e `pop()`, alla fine di una struttura `list` sono veloci, ma gli `insert()` e i `pop()` all’inizio della stessa hanno **costo lineare**, dato che tutti gli elementi che seguono dovranno slittare di una posizione; se vogliamo implementare la coda con un oggetto `list`, e garantire al tempo stesso che le operazioni abbiano costo costante, dobbiamo scrivere la funzione
`Dequeue` in modo che gli elementi rimasti in coda non slittino, ma rimangano dove sono.
___
## Alberi

L'**albero** è una struttura dati estremamente versatile, utilizzabile per modellare una grande quantità di problemi e per progettare le relative soluzioni algoritmiche. 

Per poter fornire una definizione formale dell'albero, è necessario introdurre un'altra struttura dati: il **grafo**. Un grafo $G$ è una tupla $(V, E)$ costituita da **due insiemi**:
- un insieme finito **$V$** di **nodi**, detti anche **vertici**;
- un insieme finito $E\subseteq\, V\,\times V$ di **coppie non ordinate di nodi**, detti **archi** o **spigoli**.

All'interno di un grafo, possiamo trovare vari "**cammini**", ossia sequenze $(v_{1},\,v_{2},\,\dots,\,v_{k})$ di nodi distinti appartenenti a $V$ tali che $(v_{i},\,v_{i\,+\,1})$ sia un arco appartenente a $E$ per ogni $i$ compreso tra $1$ e $k-1$. Se, poi, a un cammino generico $(v_{1},\,v_{2},\,\dots,\,v_{k})$ si aggiunge anche l'arco $(v_{k},\,v_{1})$, allora il cammino diventa un "**ciclo**". Un grafo $G$ si dice "**connesso**" se, **per ogni coppia di nodi $(u,\,v)$ appartenente a $V$ esiste un cammino tra $u$ e $v$**. Inoltre, un grafo si dice "**aciclico**" se **non contiene cicli**.

Sulla base delle proprietà dei grafi appena spiegate, possiamo fornire la seguente **definizione di albero**: un albero è un **grafo connesso e aciclico**. Ad esempio, il seguente grafo:

![[albero_esempio.png]]

è a tutti gli effetti un albero.

Sugli alberi è definito il seguente **lemma**:

> Sia $G=(V,E)$ un grafo connesso e aciclico. Eliminando da $G$ un arco qualsiasi, $G$ diventa disconnesso, cioè suddiviso in due grafi $G_{1}=(V_{1},\,E_{1})$ e $G_{2}=(V_{2},\,E_{2})$, che risultano però entrambi connessi e aciclici.

Possiamo dimostrare il lemma **per assurdo**. Supponiamo che, dopo l'eliminazione di un arco $e=(u,\,v)$ il grafo $G$ rimanga connesso: questo significherebbe che, nel nuovo grafo privato dell'arco $e$, esiste ancora un cammino tra i due nodi $u$ e $v$. Ciò, però, vorrebbe dire che nel grafo $G$ originario esisteva un ciclo che includeva i nodi $u$ e $v$ (se, eliminando un arco tra questi due nodi, c'è comunque un cammino tra di loro, ciò implica che esiste comunque una sequenza $(u,\,v_{1},\,v_{2},\,\dots,\,v)$ di nodi distinti tutti legati da archi, e l'iniziale presenza anche dell'arco $e=(u,\,v)$ rende tale cammino un ciclo), risultato che andrebbe contro l'ipotesi iniziale, che stabiliva come $G$ fosse un grafo aciclico. Siamo dunque arrivati a una contraddizione, e abbiamo così dimostrato il lemma.

Inoltre, vale il seguente **teorema**:

> Sia $G=(V,E)$ un grafo. Le seguenti due affermazioni sono equivalenti:
> 1. $G$ è connesso e aciclico (in altre parole, $G$ è un albero);
> 2. $G$ è connesso, e $|E|=|V|-1$.

Dimostrare che le due proposizioni sono equivalenti vuol dire **dimostrare la seguente doppia implicazione**:
$$1.\iff 2.$$
scomponibile in due implicazioni:
$$1. \Rightarrow 2.\,\,\,\,\,\,\,\,\,\,2.\Rightarrow 1.$$

Partiamo dimostrando la prima, ossia che se $G$ è un grafo connesso e aciclico, allora si ha che $|E|=|V|-1$. Per dimostrare questa affermazione, procediamo per **induzione** sul valore $|V|$, ossia sulla cardinalità dell'insieme $V$ dei nodi del grafo. Partendo con il **caso base**, ossia che $|V|=1$ o che $|V|=2$, l'affermazione è banalmente vera (se il grafo contiene un solo nodo, allora non ci saranno archi dato che l'esistenza di un arco implica l'esistenza di almeno due nodi, mentre se il grafo contiene due nodi allora basterà che ci sia un solo arco che li colleghi, e il grafo risultante sarà connesso e aciclico); a questo punto, procediamo con il **passo induttivo**

[DISPENSE: pag. 26 - 27]
[SLIDES: pag. 5]

Pur avendo stabilito la definizione e le principali caratteristiche di un albero, si potrebbe pensare che gli esempi forniti si discostano comunque dalla tipica struttura ad albero che si è sicuramente vista in altri contesti: con tutta probabilità, l'albero che si ha in mente è il cosiddetto "**albero radicato**", ossia un albero in cui, tra i vari nodi che lo compongono, se ne distingue uno che assume il ruolo di **radice**. Ad esempio, quello della seguente immagine:

![[albero_esempio1.png]]

è un albero radicato, con radice nel nodo $V_{3}$. Come si può notare dall'immagine di esempio appena fornita, tipicamente un albero radicato viene rappresentato come **"crescente" dall'alto verso il basso**, nel senso che la radice si trova in cima all'albero e non alla base. Inoltre, è importante ricordare le seguenti **caratteristiche degli alberi radicati**:
- **i nodi sono organizzati in livelli**, numerati in ordine crescente man mano che ci si allontana dalla radice, e con il livello della radice che di norma è il livello 0;
- dato un qualunque nodo $v$ diverso dalla radice, il primo nodo che si incontra sul cammino da $v$ alla radice è detto "**padre di $v$**";
- due o più **nodi che hanno lo stesso padre** sono detti "**fratelli**", e **la radice è l'unico nodo dell'albero a non avere padre**;
- ogni nodo sul cammino da $v$ alla radice viene detto "**antenato di $v$**";
- tutti i nodi che hanno il nodo $v$ come padre sono detti "**figli di $v$**", mentre i **nodi che non hanno figli** vengono detti "**foglie**";
- tutti i nodi che hanno il nodo $v$ come antenato sono detti "**discendenti di $v$**";
- l'**altezza** dell'albero radicato è la **lunghezza del più lungo cammino dalla radice a una foglia** (un albero di altezza $h$ contiene $h+1$ livelli, di norma numerati da $0$ a $h$).

Possiamo visualizzare più chiaramente le caratteristiche appena elencate nell'immagine seguente, rappresentante un albero radicato di altezza $h=3$:

![[albero_esempio2.png]]

Inoltre, un albero radicato viene detto "**ordinato**" se viene attribuito un qualche ordine ai figli di ciascun nodo (se un nodo ha $k$ figli, c'è una qualche distinzione tra primo figlio, secondo figlio, e così via).

##### Alberi binari

Una particolare sottoclasse degli alberi radicati è quella dei cosiddetti "**alberi binari**". Si tratta di **alberi radicati e ordinati**, con la particolarità che **ogni nodo ha al più due figli**: in questo contesto, possiamo definire ordinato un albero binario dato che i due figli di ciascun nodo vengono distinti in "**figlio sinistro**" e "**figlio destro**". Un albero binario nel quale **tutti i livelli contengono il massimo numero possibile di nodi** è detto "**albero binario completo**"; invece, se tutti i livelli tranne l'ultimo contengono il numero massimo possibile di nodi, mentre l'ultimo livello è riempito completamente da sinistra verso destra solo fino a un certo punto, allora l'albero viene chiamato "**albero binario quasi completo**". Nell'immagine seguente, si mostra un esempio di albero binario completo di altezza 2, costituito cioè da 3 livelli:

![[albero_esempio3.png]]

Si ricordi che abbiamo già incontrato un esempio di albero binario in questo corso, parlando di "[[IAA_06 - Algoritmi di ordinamento#Complessità minima di un ordinamento|alberi di decisione]]" nel contesto degli algoritmi di ordinamento. In tale circostanza, abbiamo accennato ad alcune importanti **caratteristiche degli alberi binari completi**, che elencheremo nuovamente per chiarezza:
- un albero binario completo ha **$2^{h}$ foglie**;
- il numero dei **nodi interni** di un albero binario completo è pari a $\sum_{i\,=\,0}^{h\,-\,1}\,2^{i}=\frac{2^{h}-1}{2-1}=2^{h}-1$;
- il **numero totale di nodi** di un albero binario completo è pari a $2^{h}+2^{h}-1=2^{h\,+\,1}-1$.

A questo punto, possiamo **stimare l'altezza di un albero binario completo contenente $n$ nodi**. Infatti, essendo l'albero considerato un albero completo, potremo affermare che:
$$n=2^{h\,+\,1}-1$$
e dunque, sfruttando i logaritmi, abbiamo che:
$$\log_{2}(n+1)=h+1\,\,\,\,\,\Rightarrow\,\,\,\,\,h=\log(n+1)-1=\log\left( \frac{n+1}{2} \right)$$
Possiamo, dunque, affermare che **l'altezza di un albero binario completo sia in $\Theta(\log n)$**. Invece, nel caso in cui l'albero non sia completo, l'altezza sarà in $O(n)$ (si pensi, ad esempio, a un **albero pienamente sbilanciato**, in cui tutti i nodi sono agglomerati su uno dei due lati dell'albero).

Ma **come vengono rappresentati in memoria gli alberi binari?** Tendenzialmente, un albero binario può essere rappresentato in tre modi:
- **record e puntatori**;
- **rappresentazione posizionale**;
- **vettore dei padri**.

Il primo, quello dei **record** e dei **puntatori**, è forse il più naturale e comune. In questa implementazione, **ogni nodo è costituito da un record contenente tre campi**:
- **`key`**, contenente le informazioni pertinenti al nodo stesso;
- **`left`**, contenente il puntatore al figlio sinistro (o un valore nullo se il nodo in questione non ha un figlio sinistro);
- **`right`**, contenente il puntatore al figlio destro (o un valore nullo se il nodo in questione non ha un figlio destro).

**L'accesso iniziale all'albero avviene per mezzo di un puntatore alla sua radice**, e a partire da quest'ultimo sarà possibile accedere a qualsiasi nodo dell'albero (ciò è possibile perché un albero è, in generale, un grafo connesso). Un'implementazione tramite record e puntatori ha tutti i vantaggi e la versatilità delle strutture dati dinamiche implementate mediante puntatori, come le [[IAA_07 - Strutture dati#Liste puntate|liste puntate]] ad esempio, ma presenta al contempo alcuni svantaggi: primo su tutti, il fatto che l'unico modo per accedere a un nodo sia scendere verso di esso a partire dalla sua radice, ma che a ogni "bivio" non sia chiaro quale strada prendere (vedremo in seguito come risolvere questo tipo di problemi).

Il secondo tipo di implementazione, quello che abbiamo definito "**rappresentazione posizionale**", consiste nel **memorizzare i nodi in un [[IAA_07 - Strutture dati#Array|array]]**, nel quale **la radice occupa la posizione `0`**, ossia la prima posizione dell'array, e i figli sinistro e destro del generico nodo in posizione $i$ occupano rispettivamente le posizioni $2i+1$ e $2i+2$. Ad esempio, il seguente albero binario:

![[albero_rappresentazioneposizionale_esempio.png]]

può essere rappresentato con il seguente array:

![[albero_rappresentazioneposizionale_esempio1.png]]

Rispetto alla rappresentazione mediante record e puntatori, questa implementazione presenta alcuni svantaggi:
- richiede di **conoscere a priori l'altezza massima $h$ dell'albero** e, una volta noto tale valore, di **allocare a priori memoria per un array** in grado di contenere un albero binario completo di altezza $h$ (dunque, un array di dimensione $2^{h\,+\,1}-1$);
- a meno che l'albero non sia abbastanza "denso" di nodi, si avrà quasi sicuramente uno **spreco di memoria**.

L'ultima implementazione che andremo ad analizzare è quella del "**vettore dei padri**". In questo caso, l'albero è rappresentato utilizzando **due array**:
- un array $A$ contenente i **nodi dell'albero**;
- un array $P$ contenente **il padre di ciascun nodo**.

Si tratta, sostanzialmente, di due "**array paralleli**", ossia di array in cui uno stesso indice può essere utilizzato per accedere simultaneamente a dati contenuti in tutti questi array. In questo caso, ad esempio, si avrà che **l'elemento `A[i]` conterrà un nodo dell'albero, mentre l'elemento `P[i]` conterrà l'indice del padre di `A[i]` all'interno dell'array $A$**. Si osservi che questo metodo di memorizzazione funziona
senza alcuna modifica anche per alberi non necessariamente binari, in cui cioè ogni nodo può avere un numero qualunque di figli.

Confrontiamo le diverse implementazioni mostrate finora su alcune **operazioni tipiche** che vengono fatte sugli alberi. In particolare, dato un albero $T$ e un suo nodo $v$, le operazioni su cui faremo tale confronto sono:
- **trovare il padre di $v$**;
- sapere **quanti figli ha $v$**;
- qual è la **distanza dalla radice di $v$**.

**Trovare il padre di un nodo $v$**, nodo di cui abbiamo il puntatore o l'indice (a seconda dell'implementazione), è un'operazione impossibile, per quello che sappiamo ora, nell'implementazione tramite record e puntatori, dato che come detto in precedenza non abbiamo i mezzi per capire quale strada scegliere davanti a un "bivio" tra due nodi; nella rappresentazione posizionale, sappiamo a priori che il padre del nodo si troverà nella posizione $\left[ \frac{i-1}{2} \right]$ (per assicurarsi di trovare il nodo giusto, eventualmente arrotondare per difetto); nel vettore dei padri, invece, basterà accedere all'elemento $P[i]$. Sia per la rappresentazione posizionale che per il vettore dei padri, dunque, trovare il padre di un nodo è un'operazione che ha **costo** pari a $\Theta(1)$.

Per **determinare il numero di figli di un nodo $v$**, nella struttura a record e puntatori basterà controllare se i campi `left` e `right` contengono o meno dei valori nulli; nella rappresentazione posizionale, bisognerà verificare se le posizioni $2i+1$ e $2i+2$ contengono o meno dei nodi; avendo un vettore dei padri, infine, dovremo scorrere l'intero array $P$ e contare il numero di occorrenze del nodo $v$. Dunque, per l'implementazione mediante record e puntatori e per la rappresentazione posizionale determinare il numero di figli di un nodo è un'operazione che ha **costo** pari a $\Theta(1)$, mentre per un albero implementato tramite vettore dei padri tale operazione assume costo pari a **$\Theta(n)$**.

Per **calcolare la distanza di un nodo $v$ dalla radice**, come per la ricerca del padre di un nodo, non abbiamo i mezzi nella struttura a record e puntatori; nel caso della rappresentazione posizionale, sappiamo che il livello su cui si trova il nodo $v$, indicando con $i$ il suo indice, è pari a $\log (i+1)$, e ciò ci permette di calcolare la distanza in modo immediato; nel vettore dei padri, a partire da $P[i]$ si dovrà risalire di padre in padre fino a giungere alla radice. Dunque, nella rappresentazione posizionale calcolare la distanza di un nodo dalla radice è un'operazione di **costo** pari a $\Theta(1)$, mentre nell'implementazione tramite vettore dei padri l'operazione assume costo pari a $\Theta(h)$.
___
##### Visite di alberi

Un'operazione basilare, ma molto utile, da effettuare sugli alberi, che rappresenta il presupposto per poter risolvere molti problemi su di essi, è la **"visita" di un albero**, ossia l'**accesso a tutti i suoi nodi, uno dopo l'altro**, in modo da poter effettuare una specifica operazione (che dipende dal problema posto) su ciascun nodo.

Nel caso specifico degli [[IAA_07 - Strutture dati#Alberi binari|alberi binari]], nei quali i figli di ogni nodo (e quindi i rispettivi sotto-alberi) sono al massimo due, e volendo comportarsi nello stesso modo su tutti i nodi, la visita può essere effettuata in **tre modi diversi**:
- una **visita in pre-ordine** (o "**pre-order**"), nella quale un nodo è visitato prima di proseguire con la visita dei suoi sotto-alberi;
- una **visita in ordine** (o "**in order**"), nella quale il nodo è visitato dopo la visita del suo sotto-albero sinistro e prima della visita del suo sotto-albero destro;
- una **visita in post-ordine** (o "**post-order**"), nella quale il nodo è visitato dopo aver già visitato entrambi i suoi sotto-alberi.

Per comprendere meglio come funziona ciascun tipo di visita, consideriamo il seguente albero binario:

![[visita_albero_esempio.png]]

Supponiamo, prima di tutto, di effettuare una **visita in pre-ordine** di questo albero. Così facendo, l'ordine di visita dei nodi sarebbe il seguente:
$$a,\,f,\,z,\,g,\,b,\,k$$
Ora, immaginiamo di effettuare una **visita in ordine** dello stesso albero, ottenendo così il seguente ordine di visita:
$$z,\,f,\,g,\,a,\,b,\,k$$
Infine, effettuando una **visita in post-ordine**, l'ordine di visita diventerebbe il seguente:
$$z,\,g,\,f,\,k,\,b,\,a$$

La visita di un albero binario ha un'**implementazione molto semplice**, che varia minimamente in base al tipo di visita considerato. Si tratta di un **algoritmo [[IAA_05 - Ricorsione|ricorsivo]]**, e l'unica differenza tra l'implementazione specifica di ciascuno dei tre tipi di visita è la posizione delle istruzioni relative all'accesso al nodo rispetto alle chiamate ricorsive. In particolare, supponendo che l'albero binario venga implementato tramite [[IAA_07 - Strutture dati#Alberi binari|record e puntatori]], indicando con `p` il puntatore alla radice, e supponendo che l'albero sia effettivamente esistente e accessibile, possiamo considerare le seguenti implementazioni:

```
def visita_preordine(p):
	if p != None:
		# istruzioni di accesso al nodo e operazioni conseguenti
		visita_preordine(p.left)
		visita_preordine(p.right)
	return
	
	
def visita_inordine(p):
	if p != None:
		visita_inordine(p.left)
		# istruzioni di accesso al nodo e operazioni conseguenti
		visita_inordine(p.right)
	return
	
	
def visita_postordine(p):
	if p != None:
		visita_postordine(p.left)
		visita_postordine(p.right)
		# istruzioni di accesso al nodo e operazioni conseguenti
	return
```

Il **[[IAA_03 - Costo computazionale|costo computazionale]]** dei tre tipi di visita è identico a prescindere da quale si sceglie di implementare; la differenza viene in base all'implementazione scelta per rappresentare l'albero in memoria. Nel caso della struttura a record e puntatori, indicando con $n$ il numero totale di nodi dell'albero, e con $k$ il numero di nodi del sotto-albero sinistro dalla radice, il costo computazionale è definito dalla seguente [[IAA_05 - Ricorsione#Equazioni di ricorrenza|equazione di ricorrenza]]:
$$\begin{cases} T(0)=T(1)=\Theta(1)\\ T(n)=T(k)+T(n-k-1)+\Theta(1) \end{cases}$$
L'unico metodo viabile per risolvere tale equazione di ricorrenza è il **[[IAA_05 - Ricorsione#Metodo di sostituzione|metodo di sostituzione]]**: dunque, per poter procedere, occorre farsi un idea di quale potrebbe essere la soluzione. Per fare ciò nel modo più accurato possibile, pensiamo al **caso peggiore** e al **caso migliore** di esecuzione dell'algoritmo: in particolare, il caso peggiore avviene quando si ha un **albero estremamente sbilanciato**, cioè in cui tutti i nodi discendenti dalla radice sono agglomerati in uno dei due sotto-alberi, mentre il caso migliore avviene quando si ha un **albero completo**, cioè in cui ogni nodo (tranne le foglie) possiede esattamente due figli.

Nel caso migliore, entrambi i sotto-alberi radicati nella radice avranno $\frac{n-1}{2}$ nodi, il che porta l'equazione di ricorrenza nella seguente forma:
$$T(n)=2T\left( \frac{n-1}{2} \right)+\Theta(1)$$
Notiamo subito che l'equazione ottenuta ricade nel **1° caso del [[IAA_05 - Ricorsione#Metodo principale|metodo principale]]**, dunque **il costo nel caso migliore è pari a $\Theta(n^{\log_{2}2})=\Theta(n)$**.

Nel caso peggiore, se tutti i nodi discendenti della radice sono agglomerati nel sotto-albero sinistro, si ha che $n-k-1=0$, mentre se i nodi sono agglomerati nel sotto-albero destro si ha che $k=0$. In entrambi i casi, si ottiene:
$$T(n)=T(n-1)+\Theta(1)$$
Questa nuova equazione diventa facilmente risolvibile, ad esempio, con il **[[IAA_05 - Ricorsione#Metodo iterativo|metodo iterativo]]**, portandoci ad affermare che **il costo nel caso peggiore è pari a $n\cdot\Theta(1)=\Theta(n)$**.

Banalmente, essendo arrivati a dire che **il costo è $\Theta(n)$ nel caso peggiore** (o, generalmente, che il costo è in $O(n)$) **e anche nel caso migliore** (o, generalmente, che il costo è in $\Omega(n)$), potremmo già arrivare alla conclusione che il **costo di una visita è pari a $\Theta(n)$**. Difatti, poiché una visita consiste nell’analizzare tutti i nodi di un albero, e
poiché $n$ corrisponde al numero di nodi totali, è facilmente intuibile che il costo di una
visita sia sempre $\Theta(n)$. Ciononostante, per completezza, verifichiamo che ciò sia vero anche applicando effettivamente il **metodo di sostituzione**. Eliminando le notazioni asintotiche dall'equazione di ricorrenza originale, otteniamo:
$$\begin{cases} T(0)=T(1)=d\\T(n) =T(k)+T(n-k-1)+c \end{cases}$$
dove $c$ e $d$ sono due costanti note.

[DISPENSE: pag. 39]
[SLIDES: pag. 6 - 7]

Le visite di un albero sono estremamente utili per **ispezionare l'albero** e **dedurne alcune proprietà**. A seconda dello scopo della visita, torneranno utili vari tipi di visita, come possiamo vedere nei seguenti esempi, in cui andremo a vedere come sfruttare le visite per:
- calcolare il **numero di nodi** contenuti nell'albero;
- **cercare un valore `k` nell'albero**;
- calcolare l'**altezza** dell'albero;
- calcolare il **numero di nodi presenti nel livello `k`** dell'albero.

Partiamo col calcolo del numero di nodi di un albero. Poiché il numero di nodi di un albero, in generale, coincide col numero di nodi dei due sotto-alberi destro e sinistro, sommati alla radice stessa dell'albero, possiamo ottenere il numero di nodi totale di un albero, alla cui radice punta il puntatore `p`, nel modo seguente:

```
def calcola_n(p):
	if p != None:
		num_l = calcola_n(p.left)
		num_r = calcola_n(p.right)
		num = num_l + num_r + 1
		return num
	return 0
```

La funzione `calcola_n`, come si può facilmente notare dallo pseudocodice, è una funzione [[IAA_05 - Ricorsione|ricorsiva]], che richiama sé stessa sui due sotto-alberi radicati in `p`, in modo da ottenere passo dopo passo il numero di nodi di tali sotto-alberi, ed effettuare in seguito la somma per trovare il numero di nodi totale dell'albero. Si noti che la funzione appena vista sfrutta la **visita in post-ordine**. Possiamo anche comprimere lo pseudocodice precedente in questo modo:

```
def calcola_n(p):
	if p != None:
		return calcola_n(p.left) + calcola_n(p.right) + 1
	return 0
```

Pensiamo, ora, alla **ricerca di un valore `k`** all'interno dell'albero. È logico pensare che, nel cercare un nodo specifico all'interno dell'albero, prima di controllare nodi successivi dovremmo controllare che `k` non si trovi nel nodo attuale: dunque, è naturale configurare il problema come una **visita in pre-ordine**:

```
def cerca(p, k):
	if p != None:
		if p.info == k:
			return true
		else:
			if cerca(p.left, k) == true:
				return true
			else:
				return cerca(p.right, k)
	
	return false
```

Anche in questo caso abbiamo davanti una funzione ricorsiva. Vediamo, più in particolare, il funzionamento dell'operazione `cerca`: prima di tutto, si effettua l'accesso e si controlla se il nodo attualmente considerato (quello a cui punta il puntatore `p`) contiene effettivamente l'informazione ricercata `k`, e se ciò si verifica si restituisce subito `true`; altrimenti, si ricerca il valore `k` nei due sotto-alberi che hanno radice nel nodo attuale, andando prima nel sotto-albero sinistro e poi in quello destro. Se non si trova `k` in nessuna delle chiamate ricorsive, viene restituito `false`.

Poi, vediamo un modo per **calcolare l'altezza di un albero binario**: l'altezza di un albero corrisponde all'altezza dei suoi sotto-alberi incrementata di 1, quindi per ottenere tale grandezza potremo utilizzare nuovamente un'operazione ricorsiva, che prenderà la forma di una **visita in post-ordine**:

```
def calcola_h(p):
	if p == None:
		return -1
	
	if p.left == None and p.right == None:
		return 0
	
	h = max(calcola_h(p.left), calcola_h(p.right))
	return h + 1
```

La prima cosa che fa la funzione `calcola_h` è controllare che `p` punti effettivamente a un nodo, e nel caso contrario restituisce $-1$ per simboleggiare che l'albero considerato è in realtà vuoto; se, invece, l'albero contiene effettivamente dei nodi, il passaggio seguente è controllare se esistono i sotto-alberi radicati nel nodo attuale, e in caso contrario si ritorna $0$ (si ricorda che abbiamo definito l'altezza di un albero come il più lungo cammino dalla radice a una foglia, dunque se l'albero è composto solo dalla sua radice l'albero ha altezza $0$); se, infine, esistono i sotto-alberi, si va a calcolare ricorsivamente la loro altezza, e viene restituito il massimo di queste due altezze incrementato di 1.

Infine, vediamo come **calcolare il numero di nodi presenti nel livello `k`** di un albero. Possiamo utilizzare la seguente funzione:

```
def conta_k(p, k: livello da controllare, i: livello attuale):
	if p == None:
		return 0
	
	if k == i:
		return 1
		
	k_left = conta_k(p.left, k, i + 1)
	k_right = conta_k(p.right, k, i + 1)
	
	return k_left + k_right
```

Prima di tutto, si verifica se l'albero a cui punta `p` contiene effettivamente dei nodi, e in caso contrario si restituisce subito 0 (banalmente, se l'albero non contiene nodi, ci saranno 0 nodi qualsiasi sia il livello `k`). Si arriva, in seguito, al caso base della ricorsione effettuata dalla funzione: se il livello in cui ci si trova corrisponde al livello `k`, usciamo dalla chiamata in questione restituendo 1. A questo punto, avvengono le due chiamate ricorsive sui due sotto-alberi radicati nel nodo attualmente considerato, e infine si restituisce la somma tra `k_left` e `k_right`, che al termine della catena di chiamate corrisponderà alla somma delle varie unità trovate visitando i nodi del livello `k`. Il costo computazionale di tale operazione dipenderà strettamente dal numero di nodi che si trovano nei livelli precedenti a `k`.

Oltre alle visite in pre-ordine, in ordine e in post-ordine viste finora, è possibile effettuare anche una "**visita per livelli**", cioè una visita che scandisca l'albero livello per livello, visitando tutti i nodi di un livello prima di passare al prossimo. Per implementare questa forma di visita, però, sarà necessaria una **[[IAA_07 - Strutture dati#Code|coda]] d'appoggio** nella quale inserire opportunamente i nodi, per poi estrarli al momento della loro visita. Per semplicità, possiamo supporre che **l'implementazione della coda sia fatta in modo tale da poter inserire ed estrarre direttamente puntatori a nodi dell'albero**. Lo pseudocodice di una possibile implementazione della visita per livelli potrebbe essere il seguente:

```
def visita_per_livelli(r):
	if r == None:
		return
		
	Enqueue(head, tail, r)
	
	while !CodaVuota(head):
		p = Dequeue(head, tail)
		
		# accesso al nodo e operazioni conseguenti
		
		if p.left != None:
			Enqueue(head, tail, p.left)
		if p.right != None:
			Enqueue(head, tail, p.right)
	
	return
```

La caratteristica fondamentale di questa implementazione è che vengono inseriti nella coda tutti i nodi del livello $i$ prima che ne venga inserito anche solo uno del livello $i+1$. Inoltre, essendo la coda una struttura di tipo FIFO, ed essendo l'accesso al nodo immediatamente seguente alla sua estrazione, si scandirà con successo l'albero livello per livello. Il **costo computazionale della visita per livelli**, implementata in questo modo, è pari a $\Theta(n)$, dato che, per ognuno degli $n$ nodi dell'albero, si effettua:
- un'operazione di `Enqueue`, con costo pari a $\Theta(1)$;
- un'operazione di `Dequeue`, con costo pari a $\Theta(1)$;
- un numero costante di operazioni elementari, tutte con costo pari a $\Theta(1)$.
___
##### Alberi binari di ricerca

Gli **alberi binari di ricerca**, comunemente detti in breve **ABR**, sono un particolare tipo di [[IAA_07 - Strutture dati#Alberi binari|albero binario]], nel quale vengono mantenute le seguenti proprietà:
- **ogni nodo** dell'albero **contiene una chiave**;
- il valore della chiave contenuta in ciascun nodo è **maggiore del valore della chiave contenuta in ciascun nodo del suo sotto-albero sinistro** (se esiste);
- il valore della chiave contenuta in ciascun nodo è **minore del valore della chiave contenuta in ciascun nodo del suo sotto-albero destro** (se esiste).

Visivamente, possiamo schematizzare un ABR generico nel modo seguente:

![[abr.png]]

Un esempio più concreto di ABR potrebbe invece essere il seguente:

![[abr_esempio.png]]

Gli ABR supportano tutte le operazioni tipicamente definite su insiemi dinamici, tra cui:
- **`Search(T, k)`**, che restituisce un puntatore all'elemento con chiave di valore `k` all'interno dell'albero `T` se questo è presente, e un valore nullo altrimenti;
- **`Minimum(T)`**, che restituisce un puntatore all'elemento con chiave minore all'interno dell'albero `T`;
- **`Maximum(T)`**, che restituisce un puntatore all'elemento con chiave maggiore all'interno dell'albero `T`;
- **`Predecessor(T, p)`**, che restituisce un puntatore all'elemento in `T` con la chiave che precederebbe, in una sequenza ordinata, quella contenuta nel nodo puntato da `p`;
- **`Successor(T, p)`**, che restituisce un puntatore all'elemento in `T` con la chiave che seguirebbe, in una sequenza ordinata, quella contenuta nel nodo puntato da `p`;
- **`Insert(T, k)`**, che inserisce un elemento con chiave `k` all'interno di `T`;
- **`Delete(T, p)`**, che elimina da `T` l'elemento a cui punta `p`.

Per natura dell'ABR, al suo interno **il nodo con chiave minima è sempre il nodo più "a sinistra"** dell'albero, e viceversa **il nodo con chiave massima è sempre il nodo più "a destra"**; ciononostante, i nodi più a sinistra e più a destra **non sono necessariamente foglie**, ma possono tranquillamente avere rispettivamente un figlio destro o un figlio sinistro, pur mantenendo le loro proprietà.

In questo contesto, notiamo che se volessimo **elencare in ordine crescente tutte le chiavi** contenute in un ABR basterebbe applicare in modo abbastanza banale una **[[IAA_07 - Strutture dati#Visite di alberi|visita in ordine]]** dell'albero, nel modo seguente:

```
def stampa_crescente(p):
	if p != None:
		stampa_crescente(p.left)
		print(p.key)
		stampa_crescente(p.right)
```

Per certi versi, dunque, **un ABR può essere visto come un'applicazione di un [[IAA_06 - Algoritmi di ordinamento#Cos'è un algoritmo di ordinamento?|algoritmo di ordinamento]]**, costituito da due fasi:
- l'inserimento di tutte le $n$ chiavi da ordinare in un ABR, inizialmente vuoto;
- la visita in ordine dell'ABR appena costruito.

Se il costo della visita sappiamo essere pari a $\Theta(n)$, lo stesso non si può dire del costo della costruzione dell'ABR; approfondiremo questo aspetto in seguito.

Approfondiamo come effettuare una **ricerca in un ABR**. Concettualmente, essendo l'ABR una struttura dati "ordinata", la ricerca al suo interno è molto simile alla **[[IAA_04 - Ricerca#Ricerca binaria|ricerca binaria]]**: a partire dalla radice, si scende ad ogni livello in uno o l'altro sotto-albero in base alla chiave contenuta nel nodo considerato (se la chiave del nodo è maggiore di quella cercata, si prosegue nel sotto-albero sinistro, altrimenti in quello destro); quando il nodo con la chiave cercata viene trovato, si restituisce un puntatore a tale nodo; alternativamente, se si arriva a una foglia senza aver trovato tale nodo, si restituirà un valore nullo. La similitudine con la ricerca binaria sta proprio nell'esclusione, ogni volta che si prosegue in un sotto-albero, dell'altro sotto-albero radicato nel nodo di partenza, esclusione che porta **lo spazio di ricerca a restringersi ad ogni iterazione**. 

La ricerca può essere implementata sia con un [[IAA_05 - Ricorsione#Cos'è un algoritmo ricorsivo?|algoritmo ricorsivo]] che con uno iterativo. Vediamo prima l'**implementazione ricorsiva**:

```
def abr_search_ric(p, k):
	if p == None or p.key == k:
		return p
	
	if k < p.key:
		return abr_search_ric(p.left)
	else:
		return abr_search_ric(p.right)
```

Prima di mostrare anche la versione iterativa, chiariamo un punto: nonostante la grande somiglianza con la ricerca binaria, **la ricerca in un ABR non garantisce un costo in $O(\log n)$**. Ciò è dovuto al fatto che **l'algoritmo esegue una iterazione per ogni livello, tuttavia l'ABR non include fra le sue proprietà alcuna limitazione sulla propria altezza**: per intenderci, è tranquillamente possibile ad esempio che l'ABR su cui si sta effettuando la ricerca sia estremamente sbilanciato, situazione in cui la ricerca avrebbe un costo pari a $O(n)$. In particolare, possiamo distinguere un caso migliore e un caso peggiore:
- nel **caso migliore**, che coincide con l'avere un ABR completo, l'altezza dell'albero è $\log(n+1)-1$ (dove $n$ è il numero totale di nodi dell'albero), per cui il costo della ricerca sarebbe pari a $O(\log n)$;
- nel **caso peggiore**, che coincide con l'avere un ABR estremamente sbilanciato, l'altezza dell'albero è $n-1$, per cui il costo della ricerca sarebbe pari a $O(n)$.

Dunque, in generale sarebbe più corretto affermare che **la ricerca in un ABR ha costo in $O(h)$**, dove $h$ è l'altezza dell'ABR stesso, e per garantire che tale valore si avvicini il più possibile a $\log n$ è opportuno implementare qualche tecnica di **bilanciamento in altezza**, che ci permetta tenere sotto controllo quest'ultima. Ciononostante, analogamente a quanto visto parlando dell'algoritmo [[IAA_06 - Algoritmi di ordinamento#Quick Sort|Quick Sort]], è dimostrabile che **il caso medio, nella ricerca negli ABR, si avvicina più al caso migliore che al caso peggiore**. Vale, infatti, il seguente teorema:

> L'altezza attesa di un ABR costruito in modo casuale con $n$ chiavi tutte distinte è tipicamente in $O(\log n)$.

Di conseguenza, una strategia che (in media) costruisce un albero bilanciato per un insieme fisso di elementi consiste nel **permutare in modo casuale gli elementi e, in seguito, nell'inserire gli elementi in quell'ordine** all'interno dell'ABR. Questa tecnica, però, non può essere usata se non abbiamo tutti gli elementi contemporaneamente, ad esempio in casi in cui gli elementi vengono ricevuti in input uno alla volta. È proprio in questo contesto che ci preoccupa utilizzare qualche tecnica di bilanciamento in altezza, argomento che verrà approfondito [[IAA_07 - Strutture dati#Alberi rosso-neri|in seguito]].

A questo punto, prima di procedere, forniamo anche la **versione iterativa dell'algoritmo di ricerca in un ABR**:

```
def abr_search_iter(p, k):
	while p != None and p.key != k:
		if k < p.key:
			p = p.left
		else:
			p = p.right
		
	return p
```

Un'altra operazione molto comune è l'**inserimento di un nodo nell'ABR**. Anche in questo caso, si tratta di un algoritmo abbastanza semplice: come nel caso della ricerca, vogliamo discendere lungo l'albero a partire dalla radice, facendoci guidare dai valori `key` memorizzati nei nodi che incontriamo lungo la strada, e nel momento in cui si vorrebbe proseguire la discesa verso un puntatore vuoto, in quella posizione si va a inserire un nuovo nodo contenente il valore da inserire. Possiamo vedere un esempio concreto di questo procedimento nella seguente immagine, che illustra come verrebbe inserito in un ABR il valore $11$:

![[abr_inserimento_esempio.png]]

Per convenienza, da ora in poi introdurremo una piccola modifica alla struttura dati dell'ABR: all'interno di un nodo, oltre ai campi `key`, `left` e `right`, introduciamo anche un campo **`parent`**, destinato a contenere un **puntatore al padre del nodo** (naturalmente, in tale campo sarà memorizzato un valore nullo nella radice). L'aggiunta di questo campo torna utile proprio nel contesto dell'inserimento e, soprattutto, dell'eliminazione di nodi da un ABR. Lo **pseudocodice** dell'algoritmo di inserimento, di cui vedremo solo la **versione iterativa**, include anche l'**allocazione di memoria** necessaria per la creazione del nodo da inserire, che verrà fatta grazie al comando `NodoABR(k)`, dove `k` è il valore da inserire nel campo `key` del nuovo nodo (gli altri campi, invece, verranno inizializzati con un valore nullo). Di seguito tale pseudocodice:

```
def abr_insert(p, k):
	x, y = p, None
	z = NodoABR(k)
	
	while x != None:
		y = x
		
		if z.key < x.key:
			x = x.left
		else:
			x = x.right
	
	if y == None:
		p = z
	else:
		if z.key < y.key:
			y.left = z
		else:
			y.right = z
			
	z.parent = y
	return p
```

Vediamo, più nel dettaglio, i passaggi che svolge l'algoritmo: prima di tutto, creiamo le variabili `x` e `y` per memorizzare, rispettivamente, il puntatore `p` alla radice dell'ABR e un valore nullo (in seguito, `y` diventerà un puntatore al padre di `x`); nella variabile `z`, invece, effettuiamo l'allocazione di memoria per creare il nodo con chiave `k`. A questo punto, entriamo nel ciclo `while`, il cui scopo è scendere lungo l'ABR fino alla prima posizione disponibile, che sarà proprio quella in cui verrà inserito il nodo `z`. Usciti dal ciclo, si controlla se `y == None`, condizione che si verifica solamente se l'albero considerato era vuoto sin dal principio: in tal caso, il nodo `z` diventa la radice dell'ABR; altrimenti, si va ad inserire il nodo `z` come figlio (sinistro o destro in base al valore della sua chiave) del nodo puntato da `y`, e infine si associa al campo `z.parent` un puntatore al nodo padre di `z`, ossia `y`.

Il costo computazionale dell'operazione appena vista dipende sostanzialmente dal numero di iterazioni eseguite dal ciclo `while`: esso viene eseguito al massimo un numero di volte pari all'altezza dell'ABR, dunque il **costo** è pari a $O(h)$.

Consideriamo, a questo punto, la **ricerca del minimo e del massimo di un ABR**. La soluzione, anche in questo caso, è molto semplice: come già detto, il minimo di un ABR è contenuto nel suo nodo più "a sinistra", e viceversa il massimo è contenuto nel suo nodo più "a destra"; perciò, per arrivare al minimo o al massimo, basterà **scendere sempre a sinistra**, oppure **sempre a destra**, a partire dalla radice dell'albero. Un possibile **pseudocodice** che implementi la ricerca di un minimo, prima iterativamente e poi ricorsivamente, può essere il seguente:

```
def abr_minimo_ric(p):
	if p == None:
		return None
		
	if p.left != None:
		return abr_minimo_ric(p.left)
	
	return p
		
		
def abr_minimo_iter(p):
	if p == None:
		return None
	
	min = p
	
	while min.left != None:
		min = min.left
	
	return min
```

Nel contesto della ricerca del massimo, gli algoritmi sarebbero perfettamente analoghi, con l'unica differenza che starebbe nella sostituzione del campo `left` con il campo `right`. Entrambe queste operazioni, come si può facilmente notare a logica o analizzando l'implementazione, hanno **costo computazionale** limitato superiormente dall'altezza dell'albero, dunque pari a $O(h)$.

Pensiamo, ora, a come **trovare il predecessore o il successore di una chiave `k` contenuta nell'ABR** (ricordiamo che per "predecessore di `k`" si intende il nodo dell'albero contenente la chiave che precederebbe `k` in una sequenza ordinata, e viceversa per "successore di `k`" si intende il nodo dell'albero contenente la chiave che seguirebbe `k` in una sequenza ordinata). 

Per comprendere meglio questo problema, analizziamo più nel dettaglio la ricerca del predecessore. Possiamo distinguere due scenari:
1. il nodo **ha il sotto-albero sinistro**;
2. il nodo **non ha il sotto-albero sinistro**.

Nel primo caso, il predecessore del nodo considerato sarà **il massimo del sotto-albero sinistro radicato in tale nodo**, ossia il nodo contenente la chiave maggiore tra quelle minori. Nel secondo caso, l'assenza di un sotto-albero sinistro radicato nel nodo considerato implica che quest'ultimo è il nodo più a sinistra del sotto-albero a cui appartiene, e perciò il minimo di tale sotto-albero: in questo caso, per trovare il predecessore, si dovrà:
- **risalire alla radice del sotto-albero**, il che significa salire "a destra" finché possibile;
- una volta giunti alla radice del sotto-albero, **risalire, con un singolo passo "a sinistra", al padre di tale nodo**, e sarà proprio quest'ultimo a essere il predecessore del nodo considerato.

Una situazione perfettamente simmetrica vale per il problema della ricerca del successore di `k`; in entrambi i casi, dunque, si richiede o una discesa lungo un singolo cammino a partire dalla radice, oppure una singola risalita verso la radice. Entrambe queste operazioni, banalmente, avranno **costo** pari a $O(h)$. Indicando con `x` il nodo contenente la chiave `k`, lo **pseudocodice per la ricerca del predecessore di `k` in un ABR** può essere il seguente:

```
def abr_predecessore(x):
	if x.left != None:
		return abr_massimo(x.left)
		
	padre = x.parent
	
	while padre != None and x == padre.left:
		x = padre
		padre = padre.parent
		
	return padre
```

Vediamo più nel dettaglio il funzionamento di questo algoritmo. La prima cosa che viene fatta è controllare se esiste o meno un sotto-albero sinistro: se esiste, ci troviamo nel caso 1 e basterà restituire il massimo di tale sotto-albero. Alternativamente, se non esiste un sotto-albero sinistro, ci troveremo nel caso 2 e dovremo risalire alla radice del sotto-albero in cui ci troviamo, risalita che si ferma o se arriviamo alla radice dell'albero (`padre == None`) o se `x` non è più il figlio sinistro di suo padre (`x != padre.left`): una volta terminato questo ciclo, nella variabile `padre` avremo il predecessore di `x`, che potremo dunque restituire.

Un ragionamento perfettamente analogo può essere fatto per lo **pseudocodice della ricerca del successore di `k`**:

```
def abr_successore(x):
	if x.right != None:
		return abr_minimo(x.right) 
		
	padre = x.parent 
	
	while padre != None and x == padre.right: 
		x = padre
		padre = padre.parent
		
	return padre
```

Arriviamo, infine, a trattare il problema dell'**eliminazione di un nodo da un ABR**. Si tratta forse del problema più complicato tra quelli visti finora, principalmente per la necessità di riaggiustare l'ABR nel caso in cui il nodo da eliminare abbia entrambi i figli. Per "riaggiustare l'ABR" si intende trovare un nodo da collocare al posto di quello che va eliminato, in modo da mantenere connesso l'albero: per fare ciò garantendo il mantenimento delle proprietà fondamentali degli ABR, il nodo che rimpiazzerà quello eliminato sarà necessariamente o il suo predecessore o il suo successore. Dunque, nell'eliminazione di un nodo da un ABR possono verificarsi **tre scenari**:
1. se **il nodo da eliminare è una foglia**, lo si elimina molto semplicemente, inserendo un valore nullo nell'opportuno campo del nodo padre;
2. se **il nodo da eliminare ha un solo figlio**, si vanno a collegare direttamente tra loro il padre del nodo eliminato e il figlio dello stesso;
3. se **il nodo da eliminare ha entrambi i figli**, lo si dovrà sostituire col predecessore o col successore, che a sua volta dovrà essere "eliminato" dalla sua posizione originale.

[DISPENSE: pag. 27/30]
[SLIDES: pag. 16/20]
[EXYSS: pag. 112]
___
##### Alberi rosso-neri

Come abbiamo visto parlando di [[IAA_07 - Strutture dati#Alberi binari di ricerca|alberi binari di ricerca]], quasi tutte le operazioni svolgibili su di essi hanno un **costo limitato superiormente dalla loro altezza**, il che vuol dire che, per avere la maggior efficienza possibile, è necessario che **l'ABR sia il più bilanciato possibile**, in modo che la sua altezza $h$ diventi un valore in $O(\log n)$.

Le tecniche di bilanciamento, tipicamente, sono tutte basate sull'idea di **riorganizzare la struttura dell'albero** se essa, a seguito di operazioni di inserimento o di eliminazione di nodi, viola determinati requisiti. In particolare, ciò che ci interessa maggiormente è che **l'altezza dei due sotto-alberi principali non sia "troppo diversa"**. Inoltre, ciò che rende non banali queste tecniche di bilanciamento è che naturalmente si vuole implementarle **senza peggiorare il costo computazionale delle operazioni**, dato che a quel punto perderebbero di significato.

Una variazione dell'ABR che implementa una di queste tecniche è il cosiddetto "**albero rosso-nero**", in breve indicato come **A-RB**. La caratteristica peculiare di un A-RB è che **ogni nodo o è rosso o è nero** (tale informazione verrebbe memorizzata in un campo aggiuntivo). Inoltre, all'albero vengono aggiunte **foglie fittizie**, che non contengono chiavi, in modo che **tutti i nodi "veri" dell'albero abbiano esattamente due figli**. Di conseguenza, possiamo definire un A-RB come un ABR che soddisfa anche le seguenti proprietà:
1. **ciascun nodo è rosso o nero**;
2. **ciascuna foglia fittizia è nera**;
3. **se un nodo è rosso, entrambi i suoi figli sono neri**;
4. **ogni cammino da un nodo a ciascuna delle foglie del suo sottoalbero contiene lo stesso numero di nodi neri**;
5. **la radice è sempre nera**;
6. **nessun cammino dalla radice ad una foglia può essere lungo più del doppio di un cammino dalla radice ad una qualunque altra foglia**.

Di seguito, un esempio di A-RB:

![[a-rb_esempio.png]]

Indichiamo con il termine "**black height**" di `x`, o "**b-altezza**" di `x`, o ancora **`bh(x)`**, il **numero di nodi neri sui cammini dal nodo `x`** (non incluso) **alle foglie sue discendenti**. La b-altezza di un A-RB, di conseguenza, è la **b-altezza della sua radice**.

Dalla combinazione della proprietà n°3 (se un nodo è rosso, entrambi i suoi figli sono neri) e della proprietà n°4 (ogni cammino da un nodo a ciascuna delle foglie del suo sottoalbero contiene lo stesso numero di nodi neri) discende un fatto interessante: **nessun cammino dalla radice ad una foglia può essere più lungo del doppio di un cammino dalla radice ad una qualunque altra**. Possiamo dire ciò perché:
- per la proprietà n°4, il numero di nodi neri è lo stesso lungo tutti i cammini dalla radice a una qualsiasi foglia (chiamiamo questo numero fisso di nodi $B$), e dunque **il cammino più corto possibile tra una radice e una foglia è quello che non contiene alcun nodo rosso**, ma solo nodi neri (dunque, un cammino lungo $B$);
- per la proprietà n°3, il numero di nodi rossi lungo un cammino non può essere maggiore del numero di nodi neri lungo lo stesso cammino (se compare un nodo rosso, esso avrà per definizione entrambi i figli neri), dunque per massimizzare la lunghezza di un cammino si dovrebbero alternare perfettamente nodi rossi e neri, e ciò vuol dire che **il cammino più lungo possibile tra una radice e una foglia è quello che contiene lo stesso numero di nodi rossi e nodi neri**;
- se il cammino più corto possibile è quello formato solamente da $B$ nodi, mentre il cammino più lungo possibile è quello formato da $B$ nodi neri e $B$ nodi rossi, si ottiene che nessun cammino può essere più lungo del doppio di un altro cammino.

Questa proprietà è sufficiente a dimostrare che **l'altezza di un A-RB formato da $n$ nodi è in $O(\log n)$**, come mostra il seguente teorema:

> Un A-RB con $n$ nodi interni ha un'altezza $h$ tale per cui:
> $$h\le 2\log(n+1)$$

Per poter dimostrare questo teorema, è importante sapere che **il sotto-albero radicato in un qualsiasi nodo `x` contiene almeno $2^{bh(x)}-1$ nodi interni**. Vediamo la dimostrazione. Indicando con $h$ l'altezza dell'A-RB e con $r$ la sua radice, sappiamo già che $h\le 2bh(r)$, ossia che l'altezza dell'A-RB è sempre minore o uguale del doppio della b-altezza dell'A-RB, dunque che:
$$bh(r)\ge \frac{h}{2}$$
Inoltre, sappiamo che il numero $n$ di nodi interni dell'A-RB, pari al numero di nodi interni del sotto-albero radicato in $r$, è:
$$n\,\,\ge\,\, 2^{bh(r)}-1\,\,\ge\,\, 2^{\frac{h}{2}}-1$$
da cui otteniamo che:
$$n+1\,\,\ge\,\, 2^{\frac{h}{2}}\,\,\,\Rightarrow\,\,\,2\log(n+1)\ge h$$
come volevasi dimostrare. Dunque, tale teorema garantisce che le operazioni di **ricerca** di una chiave `k`, del **massimo**, del **minimo**, del **predecessore** e del **successore** siano tutte eseguite con un **costo computazionale pari a $O(\log n)$**. Un discorso a parte, invece, va fatto per gli inserimenti e per le cancellazioni.

L'esigenza di mantenere le proprietà di un A-RB implica che, dopo un inserimento o un'eliminazione, la struttura dell'albero deve essere **riaggiustata**, in termini di:
- **colori** assegnati ai nodi;
- **collocazione** dei nodi.

A tal fine, sono definite operazioni dette "**rotazioni di un A-RB**", che permettono di **ripristinare le proprietà di un A-RB dopo un inserimento o un'eliminazione**. Le rotazioni possono essere **destre** o **sinistre**, in base al loro "verso", e sono operazioni di **costo pari a $\Theta(1)$**, che **non modificano l'ordinamento delle chiavi secondo la visita in-ordine**. Ogni rotazione viene effettuata su un nodo `x`, che possiamo vedere come **"perno" della rotazione**: 
- in una **rotazione a sinistra**, il sotto-albero sinistro $\beta$ del figlio destro del nodo `x` (che chiameremo `y` per comodità) diventa il nuovo sotto-albero destro del nodo `x`, mentre quest'ultimo diventa il figlio sinistro del nodo `y`;
- in una **rotazione a destra**, il sotto-albero destro $\beta$ del figlio sinistro del nodo `x` (che chiameremo `y` per comodità) diventa il nuovo sotto-albero sinistro del nodo `x`, mentre quest'ultimo diventa il figlio destro del nodo `y`.

Per capire meglio, vediamo un esempio di rotazione a sinistra:

![[a-rb_rotazionesinistra_esempio.png]]

Per effettuare una rotazione a sinistra, si può implementare una funzione con il seguente **pseudocodice**:

```
def arb_rotazione_sinistra(p: puntatore alla radice, x: nodo perno):
	y = x.right
	x.right = y.left
	
	if x.right != None:
		x.right.parent = x
	
	y.left = x
	y.parent = x.parent
	
	if x.parent == None:
		p = y
	else:
		if x == x.parent.left:
			x.parent.left = y
		else:
			x.parent.right = y
	
	x.parent = y
	
	return p
```

Come si può confermare avendo, ora, a disposizione lo pseudocodice, il costo della rotazione è effettivamente $\Theta(1)$.

[DISPENSE: pag. 55/58]
[EXYSS: pag. 115/117]
___
##### Alberi AVL

[DISPENSE: pag. 30/51]
[SLIDES: pag. 1/14]
___
## Dizionari

Un **dizionario** è una struttura dati che permette di gestire un **insieme dinamico di dati totalmente ordinato** tramite **tre sole operazioni**:
- **`Insert`**, ossia l'**inserimento** di un elemento;
- **`Search`**, ossia la **ricerca** di un elemento;
- **`Delete`**, ossia l'**eliminazione** di un elemento.

Quando l'esigenza si ferma a queste proprietà, tipicamente si sceglie di implementare un dizionario tramite soluzioni specifiche. In questo capitolo ne approfondiremo due:
- **tabelle ad indirizzamento diretto**;
- **tabelle hash**.

Nel trattare queste implementazioni, indicheremo con $U$ l'**insieme delle chiavi**, con $m$ il **numero delle posizioni** a disposizione nella struttura dati, e con $n$ il **numero degli elementi da memorizzare** nel dizionario. Inoltre, si specifica che **i valori delle chiavi sono tutti diversi tra loro**.

##### Tabelle ad indirizzamento diretto

Una **tabella a indirizzamento diretto**, molto semplicemente, consiste in un **[[IAA_07 - Strutture dati#Array|array]] in cui ogni indice corrisponde alla chiave dell'elemento da memorizzare in tale posizione**. Ad esempio, l'elemento avente $25$ come chiave verrà memorizzata nella posizione dell'array avente $25$ come indice:

![[diz_tabellainddir_esempio.png]]

Naturalmente, affinché tale tipologia di dizionario possa funzionare correttamente, è necessario che:
$$n\,\le\, m\,=\,|U|$$
ossia che **il numero degli elementi da memorizzare sia minore o uguale del numero di posizioni a disposizione**, e che quest'ultima coincida con il numero di possibili chiavi associabili agli elementi. Si tratta di una struttura che, seppur molto semplice, è **particolarmente efficiente**; infatti, tutte e tre le operazioni che devono essere supportate da un qualsiasi dizionario hanno **costo pari a $\Theta(1)$**. Di seguito, troviamo lo **pseudocodice** di tali operazioni:

```
def insert_indirizz_diretto(A: array, e: elemento da inserire):
	A[e.key] = e
	return
	
	
def search_indirizz_diretto(A, k: chiave da cercare):
	return A[k]
	
	
def delete_indirizz_diretto(A, k: chiave da cancellare):
	A[k] = None
	return
```

Purtroppo, però, lavorando con problemi reali le tabelle a indirizzamento diretto non sono utili come sembrano, dato che:
- **l'insieme $U$ potrebbe assumere dimensioni spropositate**, al punto da rendere impraticabile l'allocazione in memoria di un array $A$ di capienza sufficiente;
- **il numero di chiavi effettivamente utilizzate è spesso molto più piccolo di $|U|$**,il che porta a un grande spreco di memoria dato che in tal caso la maggioranza delle posizioni dell'array $A$ rimarrebbero inutilizzate.

Per questi motivi, spesso si ricorre a implementazioni differenti, a meno che non ci siano delle condizioni ottimali per l'utilizzo dell'indirizzamento diretto (ad esempio il mantenimento di un insieme $U$ relativamente ridotto).
___
##### Tabelle hash

Quando l'insieme $U$ dei valori possibili delle chiavi è molto grande, e l'insieme $K$ delle chiavi da memorizzare effettivamente è invece molto più piccolo di $U$, la soluzione migliore è la cosiddetta "**tabella hash**", prima di tutto perché **richiede molta meno memoria rispetto alle [[IAA_07 - Strutture dati#Tabelle ad indirizzamento diretto|tabelle ad indirizzamento diretto]]**.

L'idea, in questo caso, è quella di utilizzare sempre un **[[IAA_07 - Strutture dati#Array|array]] di dimensione $m$**, ma stavolta non metteremo in relazione direttamente le chiavi con l'indice corrispondente (le possibili chiavi sono molte di più rispetto agli indici disponibili, dunque fare ciò sarebbe impossibile), ma piuttosto andremo a definire una "**funzione hash**", ossia una **funzione che permette di calcolare la posizione in cui va inserito un elemento sulla base del valore della sua chiave**. Dunque, supponendo che la tabella hash $T$ contenga $m$ posizioni, i cui indici vanno da $0$ a $m-1$, la funzione hash $h$ potrà essere definita nel modo seguente:
$$h:U\rightarrow\{0,\,1,\,2,\,\dots,\,m-1\}$$
In questo contesto, indichiamo con **$h(k)$** il "**valore hash**" della chiave $k$.

Questo meccanismo presenta, però, un problema di fondo: anche nel caso in cui le chiavi da memorizzare sono meno di $m$, **non si può escludere che due chiavi $k_{1}$ e $k_{2}$, diverse tra loro, siano tali per cui $h(k_{1})=h(k_{2})$**, situazione in cui entrambe le chiavi risulterebbero da memorizzare nella stessa posizione nella tabella. Tale situazione viene chiamata "**collisione**", ed è naturalmente un fenomeno da prevenire il più possibile o, altrimenti, da risolvere in qualche modo. A tal fine, una **buona funzione hash** deve essere tale da **rendere il più possibile equiprobabile il valore risultante dall'applicazione della funzione**, ossia tutti i valori dell'insieme $\{0,\,1,\,2,\,\dots,\,m-1\}$; in altre parole, la funzione dovrebbe far apparire quasi "casuale" il valore risultante, disgregando qualunque regolarità della chiave. Al tempo stesso, la funzione deve essere "**deterministica**", il che vuol dire che, **se applicata più volte alla stessa chiave, dovrà sempre restituire lo stesso risultato**.



[DISPENSE: pag. 5/7]
[SLIDES: pag. 8 - 9]
[EXYSS: pag. 120]
___
##### Tabelle a liste di trabocco

[DISPENSE: pag. 7/9]
[SLIDES: pag. 9/11]
[EXYSS: pag. 120 - 121]
___
##### Tabelle ad indirizzamento aperto

[DISPENSE: pag. 9/16]
[SLIDES: pag. 11/16]
[EXYSS: pag. 122 - 123]
___