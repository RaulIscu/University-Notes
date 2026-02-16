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



[SLIDES: pag. 8/11]
[DISPENSE: pag. 6 - 7]
[EXYSS: pag. 70 - 71]
___
##### Bubble Sort

[SLIDES: pag. 11/13]
[DISPENSE: pag. 8]
[EXYSS: pag. 71 - 72]
___
## Merge Sort


___
## Quick Sort


___
## Heap Sort


___
## Algoritmi di ordinamento lineari



##### Counting Sort


___
##### Bucket Sort


___