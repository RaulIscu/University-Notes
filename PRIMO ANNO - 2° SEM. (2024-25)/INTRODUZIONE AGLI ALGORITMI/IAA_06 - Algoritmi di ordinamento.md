## Cos'è un algoritmo di ordinamento?

Uno dei problemi più ricorrenti nell'ambito dell'informatica, e dunque da risolvere mediante [[IAA_01 - Introduzione#Algoritmi e problem-solving|algoritmi]], è quello dell'**ordinamento** di un insieme di elementi.

Gli algoritmi che affrontano il problema dell'ordinamento vengono detti, banalmente, "**algoritmi di ordinamento**", e sono definiti come **algoritmi capaci di ordinare gli elementi di un insieme in base a una certa relazione d'ordine**, relazione definita sull'insieme stesso. Per semplicità di trattazione, nell'affrontare questa categoria di algoritmi supporremo di avere **$n$ numeri interi** da ordinare, tutti contenuti in un **array** i cui indici vanno da $0$ a $n-1$; ciononostante, in problemi reali i dati da ordinare possono essere molto più complessi.
___
## Algoritmi di ordinamento naif

In questo paragrafo, andremo a trattare di tre algoritmi che potremmo inserire nella categoria degli "**algoritmi di ordinamento naif**": si tratta, sostanzialmente, di algoritmi di ordinamento molto semplici a livello di funzionamento, che riescono nel loro intento ma che non lo fanno in modo particolarmente efficiente. In particolare, i tre algoritmi che andremo ad analizzare sono:
- l'**[[IAA_06 - Algoritmi di ordinamento#Insertion Sort|Insertion Sort]]**;
- il **[[IAA_06 - Algoritmi di ordinamento#Selection Sort|Selection Sort]]**;
- il **[[IAA_06 - Algoritmi di ordinamento#Bubble Sort|Bubble Sort]]**.

##### Insertion Sort

L'algoritmo "**Insertion Sort**", o di "**ordinamento per inserzione**", può essere intuitivamente paragonato al modo in cui si tende a ordinare un mazzo di carte: partendo da un mazzo disordinato e da un "mazzo vuoto", inseriamo una carta alla volta dal primo nel secondo cercando di volta in volta il punto giusto dove inserirla; seguendo questo procedimento a ogni passaggio, avremo assicurato che le carte si troveranno in ordine, e lo stesso principio viene applicato per l'Insertion Sort.

Nel caso di tale algoritmo, però, gli $n$ elementi da ordinare sono inizialmente contenuti in un array e l'ordinamento avviene al suo interno (per continuare con il paragone, si può pensare all'ordinamento di un mazzo di carte tenendo il mazzo in mano): il problema diventa, dunque, **trovare la posizione giusta in cui "inserire" ciascun elemento**, e ciò viene fatto **estraendo l'elemento da reinserire e spostando verso destra tutti gli elementi maggiori di esso**, finché non si raggiungerà un elemento minore di quello considerato e che, dunque, dovrà restare alla sua sinistra, indicando così la sua posizione finale.

Per natura dell'algoritmo, **gli elementi che si trovano alla sinistra di quello considerato saranno sempre già ordinati tra loro**. Dunque, si può affermare il seguente "**invariante**", ossia una proposizione che è sempre vera indipendentemente dalle manipolazioni effettuate dall'algoritmo a ogni iterazione:

> Ad ogni iterazione $i$, gli elementi con indice minore di $i$ (ossia a sinistra dell'elemento considerato) sono già ordinati, mentre gli elementi con indice maggiore di $i$ (ossia a destra dell'elemento considerato) sono ancora da ordinare.

Dunque, ad ogni iterazione, aumenta di $1$ la dimensione della porzione ordinata dell'array, finché l'intero array non sarà ordinato.

Per comprendere meglio il funzionamento di questo algoritmo, vediamo un **esempio**. Supponiamo di avere l'array $[5,\,2,\,1,\,4,\,3]$, e di volerlo ordinare seguendo i ragionamenti appena spiegati. Innanzitutto, notiamo che un array di un solo elemento è sempre già ordinato, dunque possiamo partire dal secondo elemento (indice $j=1$): si "estrae" tale elemento, ossia $2$, e si spostano a destra tutti gli elementi maggiori di lui, ossia $5$; fatto ciò, possiamo reinserire il $2$ nell'array. Dopo la prima iterazione dell'algoritmo, l'array assume ora la seguente forma:
$$[2,\,5,\,1,\,4,\,3]$$
Rifacciamo lo stesso procedimento con $j=2$, ossia prendendo l'elemento $1$: in questo caso, vengono spostati a destra sia $2$ che $5$, portando $1$ a diventare il nuovo primo elemento dell'array, che dopo la seconda iterazione assume la seguente forma:
$$[1,\,2,\,5,\,4,\,3]$$
Ora, con $j=3$, si considera l'elemento $4$: l'unico elemento minore di $4$, all'interno della porzione ordinata dell'array, è $5$, dunque verrà spostato a destra solo lui, mentre $4$ assumerà la sua posizione precedente. A questo punto, dopo la terza iterazione, si ha il seguente array:
$$[1,\,2,\,4,\,5,\,3]$$
Infine, passiamo a considerare l'indice $j=4$, e dunque l'elemento $3$: vengono spostati a destra $4$ e $5$, inserendo $3$ all'indice $2$ e rendendo finalmente l'array completamente ordinato:
$$[1,\,2,\,3,\,4,\,5]$$

Di seguito, lo **pseudocodice** dell'algoritmo di Insertion Sort:

```
def Insertion_Sort(A):
	for j in range(1, len(A)):
		x = A[j]
		i = j - 1
		
		while (i >= 0 and A[i] > x):
			A[i + 1] = A[i]
			i = i - 1
		
		A[i + 1] = x
```

Ora, cerchiamo di trovare il **[[IAA_03 - Costo computazionale#Come calcolare il costo computazionale di un algoritmo?|costo computazionale]]** dell'algoritmo di Insertion Sort. Innanzitutto, la totalità del codice dell'algoritmo si trova all'interno di un ciclo `for`, che eseguirà $n-1$ iterazioni (ricordiamo che $n$ è il numero di elementi contenuti nell'array $A$); ogni iterazione $j$ di questo ciclo `for` esterno prevederà l'esecuzione di alcune [[IAA_03 - Costo computazionale#Come calcolare il costo computazionale di un algoritmo?|istruzioni elementari]], dunque di costo $\Theta(1)$, e di un certo numero di iterazioni del ciclo `while` interno, che può essere diverso in base ai valori contenuti nell'array $A$. In particolare, identificando con $t_{j}$ il numero di volte che viene verificata la condizione iniziale del `while`, possiamo identificare un caso peggiore e un caso migliore:
- il **caso migliore** si verifica quando **l'array è già ordinato**, dunque quando non devono essere effettuati spostamenti e perciò la condizione iniziale del `while` non è mai verificata, caso in cui si ha $t_{j}=1$ per ogni $j$;
- il **caso peggiore** si verifica quando **l'array è ordinato al contrario**, dunque quando si deve effettuare il numero massimo di spostamenti e perciò si ha $t_{j}=j$ per ogni $j$.

Dato il costo complessivo $T(n)$ dell'algoritmo, che risulta essere:
$$T(n)=\sum_{j\,=\,1}^{n\,-\,1}(\Theta(1)+t_{j}\,\Theta(1)+\Theta(1))+\Theta(1)$$
possiamo dunque **quantificare il costo computazionale dell'Insertion Sort nel caso migliore e nel caso peggiore**. Nel **caso migliore**, dunque avendo $t_{j}=1$ per ogni $j$, il costo computazionale risulta essere:
$$T(n)\,=\,\sum_{j\,=\,1}^{n\,-\,1}\Theta(1)+\Theta(1)\,=\,\Theta(n)+\Theta(1)\,=\,\Theta(n)$$
Invece, nel **caso peggiore**, dunque avendo $t_{j}=j$ per ogni $j$, il costo computazionale risulta essere:
$$T(n)\,=\,\sum_{j\,=\,1}^{n\,-\,1}(\Theta(1)+\Theta(j))\,=\,\Theta(n)+\Theta(n^{2})\,=\,\Theta(n^{2})$$
Chiariamo un punto: dato che i costi asintotici dell'algoritmo nel caso migliore e nel caso peggiore sono diversi, si può affermare che l'Insertion Sort è un esempio di **algoritmo "input-sensitive"**. In contesti del genere, si tende a dare più importanza al costo previsto nel caso peggiore, dato che rappresenta appunto un costo "limite" per l'algoritmo, mentre prendere per buono il costo del caso migliore rappresenterebbe una previsione fin troppo ottimista e irrealistica.
___
##### Selection Sort

L'algoritmo "**Selection Sort**", o di "**ordinamento per selezione**", funziona nel modo seguente: alla prima iterazione, si cerca l'elemento minimo dell'intero array e lo si scambia con quello che si trova alla prima posizione dell'array; alla seconda iterazione, si cerca il minimo nelle posizioni dalla seconda all'ultima (incluse), e lo si scambia con l'elemento che si trovava nella seconda posizione; e così via. Dunque, possiamo formulare il medesimo invariante individuato per l'[[IAA_06 - Algoritmi di ordinamento#Insertion Sort|Insertion Sort]]:

> Ad ogni iterazione $i$, gli elementi con indice minore di $i$ (ossia a sinistra dell'elemento considerato) sono già ordinati, mentre gli elementi con indice maggiore di $i$ (ossia a destra dell'elemento considerato) sono ancora da ordinare.

Le differenze principali tra Selection Sort e Insertion Sort sono due:
- nell'Insertion Sort, si prendono gli elementi dell'array nell'ordine in cui si trovano inizialmente, e si sposta ciascuno di essi nella posizione corretta, mentre nel Selection Sort **ad essere spostato è sempre il minimo del sotto-array non ancora ordinato**, che verrà scambiato con la posizione $i$ corrispondente all'iterazione in cui ci si trova;
- nell'Insertion Sort avviene un numero relativamente elevato di scambi, mentre nel Selection Sort si esegue **un unico scambio per elemento**, anche se ciò prevede che venga sempre "scansionato" tutto il sotto-array non ancora ordinato per ogni elemento da scambiare (dunque, il Selection Sort risulta essere più conveniente dell'Insertion Sort principalmente quando l'operazione di scambio risulta molto costosa).

Per comprendere meglio il funzionamento di questo algoritmo, vediamo un **esempio**. Supponiamo di avere l'array $[5,\,2,\,1,\,4,\,3]$, e di volerlo ordinare seguendo i ragionamenti appena spiegati. Nella prima iterazione (si considera $i=0$), si considera l'intero array e dunque si cerca l'elemento più piccolo tra tutti quelli contenuti nello stesso: nel nostro esempio, tale elemento è $1$, che viene dunque scambiato con l'elemento nella posizione $i=0$, ossia $5$, portando l'array ad assumere la seguente forma:
$$[1,\,2,\,5,\,4,\,3]$$
Ora, per la seconda iterazione, consideriamo $i=1$, e cerchiamo dunque il minimo del sotto-array che va dalla seconda all'ultima posizione: in questo caso, il minimo è $2$, che si trova già nella posizione desiderata, quindi non saranno necessari altri scambi. Passiamo così alla terza iterazione, in cui consideriamo $i=2$: il minimo del sotto-array che va dalla terza all'ultima posizione è $3$, dunque si scambia tale numero con quello presente nella posizione $i=2$, ossia $5$, portando l'array nella forma:
$$[1,\,2,\,3,\,4,\,5]$$
Notiamo che, a questo punto, l'array risulta già essere completamente ordinato, dunque le ultime due iterazioni non porteranno ad alcun risultato visibile (pur venendo comunque eseguite).

Di seguito, lo **pseudocodice** dell'algoritmo di Selection Sort:

```
def Selection_Sort(A):
	n = len(A)
	
	for i in range(n - 1):
		m = i
		
		for j in range(i + 1, n):
			if (A[j] < A[m]):
				m = j
			
		A[i], A[m] = A[m], A[i]
```

Notiamo, analizzando lo pseudocodice di questo algoritmo, che a differenza dell'Insertion Sort **il [[IAA_03 - Costo computazionale#Come calcolare il costo computazionale di un algoritmo?|costo computazionale]] non dipende in alcun modo dalla distribuzione iniziale degli elementi nell'array**, dato che comunque si dovrà scansionare a ogni iterazione tutto il sotto-array non ancora ordinato, anche se l'array $A$ risulta ordinato in partenza e dunque il minimo si troverà sempre già nella posizione corretta. Possiamo, di conseguenza, trovare un costo computazionale generale e complessivo per l'algoritmo:
$$\begin{align} T(n)\,&=\,\Theta(1)+\sum_{i\,=\,0}^{n\,-\,2}(\Theta(1)+(n-i)\Theta(1)+\Theta(1))\\&=\,\Theta(1)+\sum_{i\,=\,0}^{n\,-\,2}(\Theta(1)+(n-i)\Theta(1))\\&=\,\Theta(1)+\Theta(n)+\Theta(n^{2})\\&=\,\Theta(n^{2}) \end{align}$$
Si deduce che **il Selection Sort non è un algoritmo input-sensitive**.
___
##### Bubble Sort

L'algoritmo "**Bubble Sort**", o di "**ordinamento a bolle**", ha un funzionamento molto semplice, ma sostanzialmente diverso da [[IAA_06 - Algoritmi di ordinamento#Insertion Sort|Insertion Sort]] e [[IAA_06 - Algoritmi di ordinamento#Selection Sort|Selection Sort]]: in parole povere, l'algoritmo **ispeziona, una dopo l'altra, ogni coppia di elementi adiacenti dell'array $A$, e se l'ordine interno alla coppia è sbagliato scambia i due elementi considerati**; tale procedimento viene, sostanzialmente, ripetuto finché non si garantisce che non ci sono più coppie di elementi adiacenti nell'ordine sbagliato. Si precisa che tale procedimento **scorre l'array da destra verso sinistra**, e dunque possiamo dedurre, logicamente, che anche per il Bubble Sort vale lo stesso invariante visto in precedenza:

> Ad ogni iterazione $i$, gli elementi con indice minore di $i$ (ossia a sinistra dell'elemento considerato) sono già ordinati, mentre gli elementi con indice maggiore di $i$ (ossia a destra dell'elemento considerato) sono ancora da ordinare.

Per comprendere meglio il funzionamento di questo algoritmo, vediamo un **esempio**. Supponiamo di avere l'array $[5,\,2,\,1,\,4,\,3]$, e di volerlo ordinare seguendo i ragionamenti appena spiegati. Si parte considerando l'ultima coppia di elementi, dunque $(4,\,3)$: si trovano nell'ordine sbagliato, dunque procediamo a scambiarli, portando l'array nella seguente forma:
$$[5,\,2,\,1,\,3,\,4]$$
Ora, si considera la penultima coppia, ossia $(1,\,3)$, e notiamo che questa coppia rispetta, invece, l'ordine crescente, dunque rimarrà invariata. Lo stesso non si può dire della coppia $(2,\,1)$, che dovrà essere "ribaltata" portando l'array ad assumere la seguente forma:
$$[5,\,1,\,2,\,3,\,4]$$
Possiamo a questo punto terminare il primo "giro" dell'array analizzando la coppia $(5,\,1)$, che naturalmente si trova in ordine sbagliato e che perciò dovrà essere scambiata, risultando nella seguente situazione:
$$[1,\,5,\,2,\,3,\,4]$$
A questo punto, notiamo che è finita la prima iterazione ($i=1$) dell'algoritmo e che, come previsto dall'invariante, si ha che il sotto-array di lunghezza $i$ nella parte sinistra dell'array $A$, ossia $[1]$, è ordinato; procediamo dunque alla seconda iterazione ($i=2$), in seguito alla quale l'array si presenterà così:
$$[1,\,2,\,5,\,3,\,4]$$
Ora la parte ordinata ha lunghezza $i=2$, e corrisponde al sotto-array $[1,\,2]$. Procedendo in modo analogo, si ha che dopo la terza iterazione l'array diventa:
$$[1,\,2,\,3,\,5,\,4]$$
mentre dopo la quarta iterazione arriviamo finalmente all'array ordinato:
$$[1,\,2,\,3,\,4,\,5]$$
Di seguito, lo **pseudocodice** dell'algoritmo di Bubble Sort:

```
def Bubble_Sort(A):
	n = len(A)

	for i in range(n):
		for j in range(n - 1, i, -1):     # scorre gli indici dall'ultimo al primo
			if (A[j] < A[j - 1]):
				A[j], A[j - 1] = A[j - 1], A[j]			
```

Anche in questo caso, notiamo subito che si tratta di un **algoritmo non input-sensitive**, dunque potremo stimare un [[IAA_03 - Costo computazionale#Come calcolare il costo computazionale di un algoritmo?|costo computazionale]] che non dipenda da un caso migliore e un caso peggiore. In particolare, il costo $T(n)$ dell'algoritmo di Bubble Sort risulta essere il seguente:
$$\begin{align} T(n)\,&=\,\Theta(1)+\sum_{i\,=\,0}^{n\,-\,1}(n-1-i)\,\Theta(1)\\&=\,\Theta(1)+\Theta(n^{2})\\&=\,\Theta(n^{2}) \end{align}$$
___
## Complessità minima di un ordinamento

Dopo aver analizzato i tre [[IAA_06 - Algoritmi di ordinamento#Algoritmi di ordinamento naif|algoritmi di ordinamento naif]] più comuni, si può notare che **tutti hanno un [[IAA_03 - Costo computazionale|costo computazionale]] che tende a crescere come il quadrato del numero di elementi da ordinare**, e dunque che hanno un costo in $\Theta(n^{2})$ (in realtà, sarebbe più preciso dire che per l'algoritmo di [[IAA_06 - Algoritmi di ordinamento#Insertion Sort|Insertion Sort]] ciò vale solo nel caso peggiore, ma come già anticipato nel calcolo del costo di un algoritmo si dà sempre priorità ad esso, dunque la proposizione precedente rimane valida). Sorge spontanea una domanda: **è possibile ordinare in modo più efficiente?** E se sì, **c'è un limite all'efficienza di un algoritmo di ordinamento?** La seconda domanda, più complessa e interessante della prima, chiede sostanzialmente di **stabilire un limite di costo computazionale al di sotto del quale nessun algoritmo di ordinamento possa scendere**.

Prima di continuare, chiariamo un aspetto che può sembrare banale ma risulta in realtà fondamentale nella nostra trattazione: gli algoritmi di ordinamento che abbiamo considerato finora, così come quelli a cui rivolgiamo la nostra curiosità nel rispondere al quesito, sono **algoritmi di ordinamento basati su confronti tra coppie di elementi**.

Per poter rispondere alla domanda che ci siamo posti, possiamo utilizzare il cosiddetto "**albero di decisione**". Si tratta di un modo per **rappresentare tutte le "strade" che la computazione di un algoritmo può intraprendere**, sulla base dei possibili esiti dei confronti previsti dall'algoritmo stesso. Ora, ricordandoci che si stanno trattando algoritmi di ordinamento basati su confronti tra coppie di elementi, sappiamo che **ogni confronto ha due esiti possibili**: o il confronto è verificato, o il confronto non è verificato. Da questa osservazione, possiamo identificare l'albero di decisione come un **[[IAA_05 - Ricorsione#Metodo dell'albero|albero binario]]**, che ha le seguenti proprietà:
- l'albero rappresenta tutti i possibili confronti che vengono effettuati dall'algoritmo, ed essendo un albero binario **ogni nodo interno ha esattamente due figli**;
- **ogni nodo interno rappresenta un singolo confronto**, e di conseguenza **i due figli di ogni nodo interno rappresentano i due possibili esiti del confronto** ad esso associato;
- **ogni foglia rappresenta una possibile soluzione del problema**, ossia nel nostro contesto una specifica permutazione della sequenza di elementi ricevuta in input inizialmente.

Supponiamo, ad esempio, di avere un array $A$ di $3$ elementi $a$, $b$ e $c$, e di voler rappresentare l'albero di decisione relativo all'applicazione dell'algoritmo di [[IAA_06 - Algoritmi di ordinamento#Insertion Sort|Insertion Sort]] su un array del genere. Si potrebbe costruire il seguente albero:

![[alberodidecisione_esempio.png]]

Naturalmente, indifferentemente dall'ordine in cui si presentano i tre elementi, l'applicazione di un algoritmo di ordinamento ben progettato porterà sempre alla soluzione corretta (in questo esempio, $abc$); infatti, si precisa che l'albero di decisione non rappresenta interamente un "diagramma di flusso" dell'algoritmo, ma piuttosto una rappresentazione grafica di tutti gli scenari possibili in base ai confronti previsti dall'algoritmo.

**Eseguire l'algoritmo di ordinamento corrisponde a scendere lungo l'albero di decisione andando dalla radice alla foglia che contiene la permutazione corretta**, ossia quella in cui gli elementi considerati sono correttamente ordinati: per la natura dell'albero di decisione, **la lunghezza di tale cammino rappresenta il numero di confronti necessari per trovare la soluzione**. Va da sé, dunque, che la lunghezza del percorso più lungo dalla radice ad una foglia (ossia l'**altezza** dell'albero binario) rappresenta il numero di confronti che l'algoritmo deve effettuare nel caso peggiore. Da tutta questa catena di ragionamenti, si deduce infine che **trovare una limitazione al costo computazionale** (nel caso peggiore) **di un qualsiasi algoritmo di ordinamento basato su confronti equivale a determinare una limitazione inferiore all'altezza dell'albero di decisione**.

Ora, dato che la soluzione del problema potrebbe corrispondere a una qualsiasi delle permutazioni degli $n$ elementi presi in input dall'algoritmo, sappiamo che ci sono $n!$ "soluzioni" possibili al problema. D'altra parte, un albero binario di altezza $h$ non può contenere più di $2^{h}$ foglie: dato che sono proprio le foglie dell'albero di decisione a corrispondere alle soluzioni possibili, deve necessariamente valere che:
$$2^{h}\ge n!\,\,\,\Rightarrow\,\,\,h\ge \log n!$$
Sfruttando una delle [[IAA_02 - Notazione asintotica#Sommatorie notevoli|sommatorie notevoli]] viste qualche capitolo fa, sappiamo che:
$$\log n! = \sum_{i\,=\,1}^{n}\log i=\Theta(n\,\log n)$$
Dunque, avendo che $h\ge \Theta(n\,\log n)$, si deduce che:

> Il costo computazionale di qualunque algoritmo di ordinamento basato su confronti è in $\Omega(n\,\log n)$.

Possiamo dimostrare quanto appena detto ragionando sul significato di $\log n!$:
$$\log n!\,=\,\sum_{i\,=\,1}^{n}\log i\,=\,\sum_{i\,=\,1}^{\frac{n}{2}}\log i+\sum_{i\,=\,\frac{n}{2}\,+\,1}^{n}\log i$$
e affermiamo che vale sicuramente la seguente disuguaglianza:
$$\sum_{i\,=\,1}^{\frac{n}{2}}\log i+\sum_{i\,=\,\frac{n}{2}\,+\,1}^{n}\log i\,\ge\,\sum_{i\,=\,1}^{\frac{n}{2}}\log i+\sum_{i\,=\,\frac{n}{2}\,+\,1}^{n}\log \frac{n}{2}$$
Concentrandoci sulle seconde sommatorie di entrambi i membri della disuguaglianza (le prime sono identiche), vale che:
$$\sum_{i\,=\,\frac{n}{2}\,+\,1}^{n}\log i\,\ge\,\sum_{i\,=\,\frac{n}{2}\,+\,1}^{n}\log \frac{n}{2}$$
disuguaglianza che è sicuramente vera dato che la sommatoria presente al secondo membro somma logaritmi il cui argomento non dipende da $i$, e coincide sempre con $\frac{n}{2}$, tuttavia notiamo che nella sommatoria al primo membro, che somma invece logaritmi dipendenti dal valore di $i$, quest'ultima parte da $\frac{n}{2}+1$, e dunque ogni valore di $\log i$ sarà sicuramente maggiore di $\log \frac{n}{2}$. Ora, la sommatoria al secondo membro può essere sviluppata come segue:
$$\sum_{i\,=\,\frac{n}{2}\,+\,1}^{n}\log \frac{n}{2}\,=\,\left( n-\left( \frac{n}{2}+1 \right) +1\right)\cdot \log \frac{n}{2}\,=\, \frac{n}{2}\,\log \frac{n}{2}\,=\,\frac{n}{2}(\log n-\log 2)\,=\,\frac{n}{2}\,\log n-\frac{n}{2}$$
A livello di notazione asintotica, si può trovare che $\frac{n}{2}\log n-\frac{n}{2}$ è in $\Theta(n\,\log n)$, ed essendo $\log n!\ge\Theta(n\,\log n)$ e $h\ge \log n!$, abbiamo dimostrato che $h=\Omega(n\,\log n)$.
___
## Algoritmi di ordinamento avanzati

In questo paragrafo, studieremo tre algoritmi di ordinamento più avanzati di quelli visti [[IAA_06 - Algoritmi di ordinamento#Algoritmi di ordinamento naif|un paio di paragrafi fa]], e al tempo stesso anche più efficienti: essi, infatti, **raggiungono il costo computazionale [[IAA_06 - Algoritmi di ordinamento#Complessità minima di un ordinamento|minore possibile]] per un algoritmo di ordinamento basato su confronti** (in particolare, il Merge Sort e l'Heap Sort presentano questa proprietà anche nel loro caso peggiore, mentre il Quick Sort solo nel caso "medio"). I tre algoritmi che tratteremo in questo paragrafo sono:
- il **[[IAA_06 - Algoritmi di ordinamento#Merge Sort|Merge Sort]]**;
- il **[[IAA_06 - Algoritmi di ordinamento#Quick Sort|Quick Sort]]**;
- l'**[[IAA_06 - Algoritmi di ordinamento#Heap Sort|Heap Sort]]**.

##### Merge Sort

L'algoritmo "**Merge Sort**", o di "**ordinamento per fusione**", è un **[[IAA_05 - Ricorsione#Cos'è un algoritmo ricorsivo?|algoritmo ricorsivo]]** che adotta una strategia detta "**divide et impera**", che può essere descritta nei seguenti passaggi:
- il problema complessivo viene suddiviso in sotto-problemi di dimensione inferiore;
- i vari sotto-problemi vengono risolti individualmente;
- le soluzioni dei sotto-problemi vengono ricomposte per ottenere la soluzione del problema complessivo.

Nel contesto del nostro algoritmo, questa strategia si traduce nei seguenti passaggi principali:
1. l'array $A$ di $n$ elementi viene diviso in due sotto-sequenze di $\frac{n}{2}$ elementi ciascuna;
2. le due sotto-sequenze vengono, a loro volta, ordinate ricorsivamente richiamando l'algoritmo stesso su di esse;
3. la ricorsione termina quando la sotto-sequenza risultante dalla chiamata ricorsiva è costituita da un unico elemento, per cui tale sequenza è naturalmente già ordinata;
4. man mano, le varie sotto-sequenze vengono "fuse" in modo ordinato, tornando a formare una sequenza di $n$ elementi ordinata.

Di seguito, lo **pseudocodice** dell'algoritmo di Bubble Sort:

```
def Merge_Sort(A, indice_primo, indice_ultimo):
	if (indice_primo < indice_ultimo):
		indice_medio = (indice_primo + indice_ultimo) // 2
		Merge_Sort(A, indice_primo, indice_medio)
		Merge_Sort(A, indice_medio + 1, indice_ultimo)
		Fondi(A, indice_primo, indice_medio, indice_ultimo)
```

Per adesso, si ignori il funzionamento effettivo del sotto-algoritmo `Fondi`, che vedremo tra poco; si tenga presente solo che è il responsabile del passaggio $4$, ossia della "fusione" delle varie sotto-sequenze, e di conseguenza dell'ordinamento delle stesse. Vediamo una schematizzazione di un esempio di applicazione dell'algoritmo di Merge Sort:

![[mergesort_esempio.png]]

In questo schema, le caselle blu corrispondono alle **operazioni di suddivisione dell'array $A$** in più sotto-array, operazioni che avvengono grazie alle chiamate ricorsive dell'algoritmo; le caselle arancioni, invece, corrispondono ai **casi base**, ossia i sotto-array contenenti un unico elemento; infine, le caselle viola corrispondono alle **chiamate al sotto-algoritmo `Fondi`**, che restituiscono sotto-array ordinati sempre più grandi, fino ad arrivare a un array di dimensione $n$.

Dall'analisi dello [[IAA_01 - Introduzione#Pseudocodice|pseudocodice]] visto poco fa, possiamo ottenere un'[[IAA_05 - Ricorsione#Equazioni di ricorrenza|equazione di ricorrenza]] che esprima il [[IAA_03 - Costo computazionale#Come calcolare il costo computazionale di un algoritmo?|costo computazionale]] complessivo $T(n)$ dell'algoritmo di Merge Sort (per adesso, non avendolo approfondito, indichiamo semplicemente con $S(n)$ il costo del sotto-algoritmo `Fondi`):
$$\begin{cases} T(1)=\Theta(1) \\T(n)=\Theta(1)+2T\left( \frac{n}{2} \right) +S(n) \end{cases}$$

Prima di approfondire il funzionamento dell'algoritmo `Fondi`, e di conseguenza il suo costo computazionale $S(n)$, è giusto fare un'osservazione: per come è progettato l'algoritmo di Merge Sort, risulta evidente che sarebbe possibile utilizzare un qualunque altro algoritmo, al posto di `Fondi`, purché sia in grado di restituire una sequenza ordinata partendo da due sotto-sequenze; l'utilizzo dell'algoritmo `Fondi` è tuttavia indicato per la natura estremamente ottimizzata dello stesso, che risulta in un costo computazionale minimo per lo scopo per cui viene utilizzato.

Ora, illustriamo il **funzionamento di `Fondi`**. Esso si basa sul fatto che **le due sotto-sequenze che prende in input sono individualmente ordinate**, proprietà che è sempre rispettata per natura dell'algoritmo di Merge Sort e che permette di arrivare a un meccanismo semplice ma efficace: **il minimo della sequenza complessiva sarà necessariamente il minimo tra il primo elemento della prima sotto-sequenza e il primo elemento della seconda**; una volta trovato il minimo tra questi due elementi, **esso viene inserito nella sequenza complessiva**, rimosso dalla rispettiva sotto-sequenza, e **la stessa operazione viene ripetuta sulle due sotto-sequenze risultanti**; non appena una delle due sotto-sequenze termina i suoi elementi, tutti gli elementi rimasti nell'altra (che sono necessariamente, oltre che già ordinati, tutti maggiori o uguali degli elementi inseriti finora nella sequenza complessiva) vengono aggiunti uno ad uno in coda alla sequenza complessiva. Vediamo, ora, lo pseudocodice di una possibile implementazione di `Fondi`:

```
def Fondi(A, indice_primo, indice_medio, indice_ultimo):
	i, j = indice_primo, indice_medio + 1
	B = []
	
	while (i <= indice_medio and j <= indice_ultimo):
		if (A[i] <= A[j]):
			B.append(A[i])
			i += 1
		else:
			B.append(A[j])
			j += 1
	
	while (i <= indice_medio):
		B.append(A[i])
		i += 1
	
	while (j <= indice_ultimo):
		B.append(A[j])
		j += 1
		
	for i in range(len(B)):
		A[indice_primo + i] = B[i]
```

L'algoritmo `Fondi`, dunque, prende in input l'array iniziale $A$, l'indice di inizio `indice_primo` della sotto-sequenza complessiva da considerare, l'indice medio `indice_medio` che divide quest'ultima nelle due sotto-sequenze ordinate da fondere in modo ordinato, e l'indice di fine `indice_ultimo` della sotto-sequenza complessiva. L'array `B`, inizializzato all'inizio dell'esecuzione di `Fondi`, andrà ad ospitare temporaneamente gli elementi ordinati, prima che essi vengano reinseriti nelle apposite posizioni dell'array $A$ su cui si sta lavorando.

Il primo ciclo `while` controlla, nella sua condizione, che le due sotto-sequenze da fondere abbiano entrambe almeno un elemento rimasto al loro interno, ed esegue concretamente il confronto tra i primi elementi di ciascuna, trovando il minimo tra di essi e aggiungendolo in coda a `B` tramite l'istruzione `B.append`. Non appena una delle due sotto-sequenze esaurisce i propri elementi, l'esecuzione esce dal ciclo appena visto, e incontra i due cicli `while` successivi, andando ad eseguire solamente quello relativo alla sotto-sequenza non ancora esaurita, e aggiungendo in coda a `B`, uno alla volta e in ordine, tutti gli elementi rimasti in tale sotto-sequenza. Infine, viene eseguito l'ultimo ciclo `for`, che non fa altro che inserire gli elementi ordinati (ora contenuti tutti in `B`) nelle posizioni giuste all'interno dell'array $A$.

Avendo ben chiaro il funzionamento di `Fondi`, parliamo ora del suo **costo computazionale $S(n)$**. Andando istruzione per istruzione, troviamo innanzitutto delle istruzioni elementari di costo $\Theta(1)$. Arriviamo così al primo ciclo `while`, che esegue un numero costante di istruzioni elementari per ogni iterazione, e che esegue un numero di iterazioni compreso tra $\frac{n}{2}$ e $n$, dato che scorre almeno una sotto-sequenza di dimensione $\frac{n}{2}$ (nel caso in cui una delle due sotto-sequenze contenga tutti elementi minori del primo elemento dell'altra) e al più due sotto-sequenze di dimensione $\frac{n}{2}$ (nel caso in cui gli elementi della prima e della seconda sotto-sequenza "si alternano" nell'ordinamento); da ciò, deduciamo che il costo computazionale di questo ciclo è in $\Theta(n)$. Passiamo ora ai due cicli `while` successivi, o più precisamente a uno dei due (si ricorda che verrà sempre eseguito al più uno di essi): anch'essi eseguono un numero costante di istruzioni elementari per ogni iterazione, e un numero di iterazioni compreso tra $1$ (se è rimasto un solo elemento nella sotto-sequenza) e $\frac{n}{2}$ (se tutti gli elementi della sotto-sequenza sono ancora presenti): possiamo, quindi, affermare che il suo costo sarà in $O(n)$. Infine, l'ultimo ciclo `for` ha un costo facilmente individuabile di $\Theta(n)$, dato che esegue una singola istruzione elementare per $n$ volte. Da tutte queste considerazioni, possiamo ottenere una formula per il costo complessivo $S(n)$:
$$S(n)=\Theta(1)+\Theta(n)+O(n)+\Theta(n)=\Theta(n)$$
il che porta il costo computazionale $T(n)$ dell'algoritmo di Merge Sort a corrispondere alla seguente equazione di ricorrenza:
$$\begin{cases} T(1)=\Theta(1)\\T(n)=2T\left( \frac{n}{2} \right)+\Theta(n) \end{cases}$$
Per ottenere il costo concreto, possiamo risolvere tale equazione di ricorrenza ad esempio utilizzando il [[IAA_05 - Ricorsione#Metodo principale|metodo principale]]: individuando $a=2$ e $b=2$, e di conseguenza $n^{\log_{b}a}=n^{\log_{2}2}=n$, si trova subito che $f(n)=\Theta(n)$ è in $\Theta(n^{\log_{b}a})=\Theta(n)$, e dunque troviamo che il costo computazionale dell'algoritmo di Merge Sort è:
$$T(n)=\Theta(n\,\log n)$$

Incontrando per la prima volta l'algoritmo di Merge Sort e la sua implementazione, ci si potrebbe fare una domanda: **non è possibile effettuare le operazioni di ordinamento e "fusione" eseguite da `Fondi` in loco**, ossia senza creare ogni volta dei nuovi array dove ospitare temporaneamente gli elementi ordinati? La risposta è **no, a meno che non si voglia aumentare il costo dell'algoritmo**: infatti, eseguire tali operazioni in loco, o "in-place", implicherebbe il dover spostare ogni volta parte della sotto-sequenza considerata per fare spazio al valore minimo (un funzionamento simile a quello dell'[[IAA_06 - Algoritmi di ordinamento#Insertion Sort|Insertion Sort]]), e ciò vorrebbe dire eseguire un'operazione di costo $\Theta(n)$ per ognuno degli $n$ elementi da riordinare, portando il costo della fusione ad aumentare da $\Theta(n)$ a $\Theta(n^{2})$. Dunque, al costo di mantenere contenuto il costo computazionale dell'algoritmo di Merge Sort, si preferisce utilizzare quantità relativamente elevate di memoria per ospitare i nuovi array che vengono creati ad ogni chiamata di `Fondi`.

Notiamo un'altra particolarità del Merge Sort, che riguarda proprio l'algoritmo di Insertion Sort a cui abbiamo rimandato poco fa: complice, per certi versi, la somiglianza tra i funzionamenti di `Fondi` e dell'Insertion Sort, e nonostante l'Insertion Sort abbia un costo computazionale maggiore ($O(n^{2})$) del Merge Sort, si può affermare che **per valori $n$ sufficientemente piccoli, è più conveniente utilizzare l'Insertion Sort all'interno del Merge Sort**. Ipotizziamo, dunque, di avere il seguente algoritmo chiamato **`Merge_Insertion`**, un ibrido tra i due algoritmi che stiamo considerando, e chiamiamo $k$ il limite superato il quale torna a convenire il Merge Sort, dunque il limite che stabilisce se continuare con la solita catena di ricorsione prevista dall'algoritmo originale o se passare all'utilizzo dell'Insertion Sort:

```
def Merge_Insertion(A, k, primo, ultimo, dim):
	if (dim > k):
		medio = (primo + ultimo) // 2
		Merge_Insertion(A, k, primo, medio, medio - primo + 1)
		Merge_Insertion(A, k, medio + 1, ultimo, ultimo - primo)
		Fondi(primo, medio, ultimo)
	else:
		Insertion_Sort(primo, ultimo)
```

L'equazione di ricorrenza di questa nuova variante dell'algoritmo è la seguente:
$$\begin{cases} T(k)=\Theta(k^{2})\\T(n)=2T\left( \frac{n}{2} \right)+\Theta(n) \end{cases}$$
dove il caso base coincide con la chiamata all'algoritmo di Insertion Sort, che avviene quando $n\le k$. Ma quali valori può assumere $k$ affinché l'algoritmo `Merge_Insertion` mantenga lo stesso tempo di esecuzione del Merge Sort, e sia dunque potenzialmente preferibile ad esso? Per rispondere a questa domanda, risolviamo l'equazione di ricorrenza attraverso il [[IAA_05 - Ricorsione#Metodo iterativo|metodo iterativo]], ottenendo:
$$\begin{align}T(n)\,&=\,2T\left( \frac{n}{2} \right)+\Theta(n)\\&=\,2\left[ 2T\left( \frac{n}{4} \right)+\Theta\left( \frac{n}{2} \right) \right]+\Theta(n)\\&\dots\\&=\,2^{h}\, T\left( \frac{n}{2^{h}} \right)+\sum_{i\,=\,0}^{h\,-\,1}2^{i}\cdot \Theta\left( \frac{n}{2^{i}} \right)\\&=\,2^{h}\,T\left( \frac{n}{2^{h}} \right)+\sum_{i\,=\,0}^{h\,-\,1}\Theta(n)\end{align}$$
Ora, sappiamo che la catena di chiamate ricorsive procede finché $\frac{n}{2^{h}}=k$, da cui possiamo ottenere:
$$\frac{n}{2^{h}}=k\,\,\,\Rightarrow\,\,\,2^{h}=\frac{n}{k}\,\,\,\Rightarrow\,\,\,h=\log\left( \frac{n}{k} \right)$$
Sostituendo $h$ all'interno dell'equazione ottenuta, abbiamo:
$$\begin{align} T(n)\,&=\,2^{h}\,T\left( \frac{n}{2^{h}} \right)+\sum_{i\,=\,0}^{h\,-\,1}\Theta(n)\\&=\,2^{\log\left( \frac{n}{k} \right)}\cdot \Theta(k^{2})+\sum_{i\,=\,0}^{\log\left( \frac{n}{k} \right)\,-\,1}\Theta(n)\\&=\,\frac{n}{k}\,\Theta(k^{2})+\Theta\left( n\log\left( \frac{n}{k} \right) \right)\\&=\,\Theta(nk)+\Theta(n\,\log n)-\Theta(n\,\log k) \end{align}$$
Ponendo $k=O(\log n)$, il che vuol dire che deve valere la disuguaglianza $k\le c\cdot \log n$, otteniamo che:
$$T(n)=\Theta(n\,\log n)+\Theta(n\,\log n)-\Theta(n\,\log(\log n))=\Theta(n\,\log n)$$
Concludiamo, così, che se per valori $n\le c\cdot \log n$ viene utilizzato l'Insertion Sort internamente al Merge Sort, si ottiene **un costo computazionale invariato ma una riduzione notevole di costo in termini di memoria**, dato che l'Insertion Sort è un algoritmo che lavora in-place.

Una piccola curiosità: in Python, il comando `sort`, che può essere utilizzato per ordinare un oggetto di tipo `list`, viene implementato utilizzando la variante del Merge Sort integrata con l'Insertion Sort (variante che viene anche detta "**Timsort**"), e pertanto ha costo computazionale pari a $\Theta(n\,\log n)$.
___
##### Quick Sort

[SLIDES: pag. 3/14]
[DISPENSE: pag. 20/27]
[EXYSS: pag. 80/83]
___
##### Heap Sort


___
## Algoritmi di ordinamento lineari



##### Counting Sort


___
##### Bucket Sort


___