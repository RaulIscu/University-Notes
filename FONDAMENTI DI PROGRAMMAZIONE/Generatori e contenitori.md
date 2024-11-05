Per scrivere lunghe liste di valori, si può usare un **generatore**, un oggetto che fornisce un numero per volta da un intervallo determinato (ad esempio: ```range(start, end, inc)```). Di seguito alcuni esempi di applicazione: 
- ```range(101)``` = 0, 1, 2, …, 100; 
- ```range(3, 101)``` = 3, 4, 5, …, 100; 
- ```range(3, 101, 2)``` = 3, 5, 7, ..., 99.

Avendo introdotto i generatori, diventa importante ora parlare anche dei **contenitori**, definibili in generale come insiemi di elementi aventi varie caratteristiche. In particolare, vediamo:
- la **lista** (```list```), un insieme indicizzato e mutabile di elementi eterogenei;
- la **tupla** (```tuple```), un insieme indicizzato e immutabile di elementi eterogenei;
- l’**insieme** (```set```), un insieme non indicizzato, mutabile e senza ripetizioni di elementi eterogenei immutabili;
- il **dizionario** (```dict```), un insieme mutabile di coppie “chiave : valore” indicizzato sulle chiavi.

A seconda del tipo di contenitore, si utilizzano caratteri diversi per indicarne uno: la lista si delimita con delle parentesi quadre (```[ ]```), la tupla si delimita con delle parentesi tonde (```( )```), e l’insieme si delimita con delle parentesi graffe (```{ }```), così come il dizionario.

[REGISTRAZIONI DEL PROF]

Approfondiamo le varie operazioni fattibili sui diversi contenitori visti finora. Innanzitutto, vediamo come si può agire su una **lista**:
- **```elemento in L```**, istruzione che restituirà ```True``` nel caso in cui l’elemento considerato è effettivamente presente nella lista L, e ```False``` se non è presente;
- **```L[i]```**, restituirà l’elemento presente all’indice *i* della lista L;
- **```L1 + L2```**, che crea una nuova lista rappresentata dalla concatenazione di L1 e L2;
- **```L1 * n```**, comando che replica n volte la lista L1 e compie una concatenazione tra le varie repliche;
- **```L.append(elemento)```**, che aggiunge un elemento alla fine della lista L;
- **```L.clear()```**, che elimina tutti gli elementi della lista L;
- **```L.count(elemento)```**, che conta il numero di volte in cui compare l’elemento considerato nella lista L;
- **```L.index(elemento)```**, che trova il primo indice di una lista L in cui è presente un determinato elemento (nel caso in cui tale elemento non sia presente, si avrà un errore);
- **```L.insert(i, elemento)```**, che inserisce, all’indice *i* della lista L, un determinato elemento (non elimina l’elemento che si trovava precedentemente all’indice *i*);
- **```L.pop(i)```**, che porta all’estrazione distruttiva dell’elemento all’indice *i* della lista L (se non si specifica un indice, verrà eliminato l’ultimo elemento della lista; si avrà un errore in caso di lista vuota o di non esistenza di *i*);
- **```L.remove(elemento)```**, che permette di eliminare la prima occorrenza di un elemento da una lista L (nel caso in cui tale elemento non sia presente, si avrà un errore);
- **```L.reverse()```**, che inverte l’ordine degli elementi di una lista L;
- **```L.sort()```**, che riordina gli elementi di una lista L.

Inoltre, utilizzando la tecnica dell’**assegnamento a slice**, è possibile sostituire non solo singoli elementi, ma anche gruppi di elementi di una lista con un diverso gruppo (o contenitore):

	L[inizio: fine] = contenitore

In seguito, trattiamo delle **tuple**, un contenitore simile alle liste, con la differenza dell’immutabilità. Per questo, valgono buona parte delle stesse operazioni, ad eccezione di quelle che modificano suddetto contenitore:
- **```elemento in T```**, che restituirà ```True``` nel caso in cui l’elemento considerato è effettivamente presente nella tupla T, e ```False``` se non è presente;
- **```T[i]```**, che restituirà l’elemento presente all’indice *i* della tupla T;
- **```T1 + T2```**, che crea una nuova tupla rappresentata dalla concatenazione di T1 e T2;
- **```T1 * n```**, che replica *n* volte la tupla T1 e compie una concatenazione tra le varie repliche;
- **```T.count(elemento)```**, che conta il numero di volte in cui compare l’elemento considerato nella tupla T;
- **```T.index(elemento)```**, che trova il primo indice di una tupla T in cui è presente un determinato elemento (nel caso in cui tale elemento non sia presente, si avrà un errore).

Passiamo ora agli **insiemi**, o **set**:
- **```elemento in S```**, che restituirà ```True``` nel caso in cui l’elemento considerato è effettivamente presente nell’insieme S, e ```False``` se non è presente;
- **```S1 | S2```**, oppure **```S1.union(S2)```**, che restituirà un unione tra i due insiemi S1 ed S2;
- **```S1 & S2```**, oppure **```S1.intersection(S2)```**, che restituirà un’intersezione tra i due insiemi S1 ed S2;
- **```S1 - S2```**, oppure **```S1.difference(S2)```**, che risulterà nell’insieme di elementi di S1 che non sono presenti in S2, o in altre parole la differenza tra S1 ed S2;
- **```S1 ^ S2```**, oppure **```S1.symmetric_difference(S2)```**, che darà l’insieme di elementi che non sono in comune tra S1 ed S2;
- **```S.add(elemento)```**, che permette di aggiungere un elemento all’insieme S;
- **```S.clear()```**, che elimina tutti gli elementi dell’insieme S;
- **```S.pop()```**, che risulterà in un’estrazione distruttiva di un elemento a caso dell’insieme S (si avrà un errore in caso di insieme vuoto);
- **```S.remove(elemento)```**, che rimuove un elemento dall’insieme S (se l’elemento considerato non è presente nell’insieme, si avrà un errore).

Infine, analizziamo le operazioni fattibili nell’ambito dei **dizionari**:
- **```key in D```**, che restituirà ```True``` nel caso in cui l’elemento considerato è effettivamente presente nel dizionario D, e ```False``` se non è presente;
- **```D[key]```**, che restituirà il valore con chiave *key* all’interno del dizionario D;
- **```D1 | D2```**, che fornisce un nuovo dizionario concatenando tutte le coppie di D1 e D2;
- **```D.clear()```**, che elimina tutti gli elementi del dizionario D;
- **```D.fromkeys(keys, value)```**, che costruisce un nuovo dizionario D, associando alle chiavi *keys* fornite lo stesso valore *value*;
- **```D.get(key, default)```**, che restituisce il valore associate alla chiave *key*, nel caso in cui essa sia presente (altrimenti, fornirà il valore di default);
- **```D.items()```**, che risulta in un elenco delle coppie “chiave : valore” appartenenti al dizionario D;
- **```D.keys()```**, che fornisce un elenco delle chiavi uniche del dizionario D;
- **```D.pop(key, default)```**, che rimuove l’elemento associato alla chiave *key* dal dizionario D, nel caso in cui esso sia presente (altrimenti, fornirà il valore di default);
- **```D.popitem()```**, che individua l’ultima coppia “chiave : valore” inserita nel dizionario D e la elimina;
- **```D.setdefault(key, default)```**, che risulta nel valore associato alla chiave *key*, nel caso in cui essa sia presente (altrimenti la inserisce con accoppiato il valore *default*);
- **```D1.update(D2)```**, che modifica il dizionario D1 aggiungendo, in ordine, le coppie “chiave : valore” di D2;
- **```D.values()```**, che restituisce un elenco dei valori del dizionario D (compresi eventuali duplicati).

	adtasfdasjdgasgdkgakgadvjasbgkhdagskud