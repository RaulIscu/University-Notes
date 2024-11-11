Analizzando alcuni problemi di conteggio particolari, si potrà notare la comparsa di alcuni tipi particolari di funzioni.

Ad esempio, supponiamo di voler distribuire 8 giochi tra 5 bambini, e di voler sapere in quanti modi possibili si può fare questa operazione. Applicando il [[Principio moltiplicativo|principio moltiplicativo]], avrò 5 possibilità per il primo gioco, 5 per il secondo, e così via, ottenendo 5⁸ possibili assegnazioni. Posso, però, rappresentare il problema anche come l’associazione di un gioco a un bambino, ossia come una funzione dal dominio {1, 2, 3, 4, 5, 6, 7, 8} al codominio {1, 2, 3, 4, 5}. Questo semplice problema di conteggio corrisponde dunque al concetto generico di [[METODI MATEMATICI PER INFORMATICA/Funzioni|funzione]]: sto contando le funzioni dal dominio {1, 2, 3, 4, 5, 6, 7, 8} al codominio {1, 2, 3, 4, 5}. **Il concetto generale di funzione** (su dominio finito) **corrisponde quindi esattamente a quello di [[Disposizioni e permutazioni|disposizione con ripetizione]]**, e dunque, in generale, il numero di funzioni con dominio di cardinalità *k* e codominio di cardinalità *n* sono:
$$num(f: n → k) = n^k$$
Consideriamo un altro esempio, supponendo di voler distribuire 3 giochi tra 5 bambini, in modo che nessuno riceva più di un gioco, e di voler sapere in quanti modi possibili si può fare questa operazione. Avrò 5 scelte per il primo gioco, 4 scelte per il secondo, e 3 per il terzo, ossia 5×4×3 modi di distribuire i giochi rispettando il vincolo. Considerando la soluzione come un'associazione di un gioco a un bambino, mi interessano le funzioni dal dominio {1, 2, 3} al codominio {1, 2, 3, 4, 5}, escludendo quelle in cui due elementi distinti del dominio hanno la stessa immagine. Una funzione di questo tipo si dice "**iniettiva**". In generale, dunque, il numero di funzioni iniettive da un dominio di cardinalità *k* a un codominio di
cardinalità *n* corrisponde al numero di **[[Disposizioni e permutazioni|disposizioni semplici]]**:
$$num(f_i : n → k) = n!/(n-k)!$$
Infine, analizziamo un esempio in cui si vogliono distribuire 8 giochi tra 5 bambini, in modo che ciascuno abbia almeno un gioco, e di voler sapere in quanti modi possibili si può fare questa operazione. Il problema è risolvibile mediante il [[Principio di inclusione-esclusione|principio di inclusione-esclusione]]; alternativamente, in termini di funzioni, sto considerando le funzioni con dominio {1, 2, 3, 4, 5, 6, 7, 8} e codominio {1, 2, 3, 4, 5} tali che ogni elemento del codominio sia immagine di almeno un elemento del dominio. Questo tipo di funzione si definisce come funzione "**suriettiva**".

Mediante i precedenti esempi, capiamo quanto i concetti di "funzione iniettiva" e "funzione suriettiva" siano, in realtà, abbastanza naturali e immediati. Approfondiamo le definizioni di questi due concetti da un punto di vista più classico e propriamente matematico.

>Una funzione *f: X → Y* è detta **iniettiva** se ogni elemento del codominio *Y* è immagine di al più un elemento del dominio *X*. Tale definizione può essere riformulata nel modo seguente: 
$$f_i: X → Y ⇔ ∀i, i' ∈ X, i ≠ i' → f(i) ≠ f(i')$$

In termini di diagrammi, una funzione è iniettiva se e solo se ogni punto del codominio ha al massimo una freccia entrante; in termini grafici, invece, una funzione è iniettiva se e solo se ogni asse orizzontale contiene al più un punto del grafico della funzione. Una funzione *f: X → Y* non è iniettiva se e solo se esistono *i* e *i'* tali per cui:
$$i ≠ i' → f(i) = f(i')$$
>Una funzione *f: X → Y* è detta **suriettiva** se ogni elemento del codominio *Y* è immagine di almeno un elemento del dominio *X*. Tale definizione può essere riformulata nel modo seguente: una funzione f : I → O è suriettiva se e solo se per ogni o ∈ O esiste i ∈ I tale che f(i) = o.
>$$f_s: X → Y ⇔ ∀y ∈ Y, ∃x ∈ X t.c. f(x) = y$$

In termini di diagrammi, una funzione è suriettiva se e solo se ogni punto del codominio ha almeno una freccia entrante. In termini grafici, invece, una funzione è suriettiva se e solo se ogni asse verticale contiene almeno un punto del grafico della funzione. Una funzione *f: X → Y* non è suriettiva se e solo se esiste *y ∈ Y* tale che:
$$∀x ∈ X → f(x) ≠ y$$
Una funzione *f: X → Y* è detta **biettiva** se è sia suriettiva che iniettiva, dunque se ogni elemento del codominio *Y* è immagine di esattamente un elemento del dominio *X*. In termini di diagrammi, una funzione è biettiva se e solo se ogni punto del codominio ha esattamente una freccia entrante.

[DISPENSA 8]