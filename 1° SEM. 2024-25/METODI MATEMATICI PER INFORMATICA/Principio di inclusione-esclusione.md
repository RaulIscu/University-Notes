É possibile un altro modo di trovare le combinazioni semplici: supponiamo, ad esempio, di avere un insieme di *n* pecore, tra cui una nera che possiamo denotare con *p*. Per contare tutti i sottoinsiemi possibili di *k* pecore del gregge di *n* pecore totali, si può applicare il [[Principio additivo |principio additivo]] e dividere tali sottoinsiemi in due categorie:
1. categoria n°1, o "gruppi tolleranti", che contengono la pecora nera;
2. categoria n°2, o "gruppi intolleranti", che non contengono la pecora nera.

I gruppi della prima categoria contengono la pecora nera *p* e altre *k − 1* pecore scelte tra le restanti *n − 1*. Il loro numero è dunque dato da:
$$C(n−1, k−1)$$
I gruppi della seconda categoria contengono *k* pecore scelte tra le *n − 1* pecore (tutte le pecore tranne quella nera). Il loro numero è dunque dato da:
$$C(n-1, k)$$
I due casi sopra considerati sono una partizione in due parti dell’insieme dei sottoinsiemi di *k* elementi in A in due parti. Posso dunque concludere che:
![[comb_pecoranera.png]]

Dunque, in via generale, il **principio di inclusione-esclusione** si basa sulla considerazione di un “elemento pecora nera”, e su una partizione tra i sottoinsiemi dell’insieme A, in cui nella prima categoria rientrano i raggruppamenti che contengono l’elemento pecora nera, mentre nella seconda rientrano i raggruppamenti che la escludono.

Il principio di inclusione-esclusione ci permette di contare collezioni definite da proprietà disgiuntive (A o B) anche nel caso in cui queste proprietà non sono mutualmente esclusive.

Consideriamo un esempio: vogliamo sapere quante targhe automobilistiche contengono una P in prima posizione o una R in ultima. Possiamo risolvere il quesito per partizione o mediante passaggio al complemento, ma proviamo un altro approccio. Consideriamo i seguenti insiemi:
- *A* = insieme delle targhe che contengono una P in prima posizione;
- *B* = insieme delle targhe che contengono una R in ultima posizione.

Se stimiamo che la risposta al  problema sia la somma *A + B*, ci accorgiamo che stiamo sovra-contando la quantità desiderata. Infatti, alcuni elementi tra quelli che vogliamo contare sono considerati più di una volta. Per ottenere la quantità corretta dobbiamo dunque sottrarre il numero di elementi in *Y*, con *Y = A ∩ B*. L’insieme delle targhe con P in prima o R in ultima è dunque:
$$A + B − (A ∩ B)$$
In termini astratti, il numero di oggetti di tipo A oppure B è dato dalla somma del numero di oggetti di tipo A più il numero di oggetti di tipo B meno il numero di oggetti di tipo A e B. In termini insiemistici, possiamo scrivere il seguente principio come:
$$(A ∪ B) = A + B - (A ∩ B)$$
Si dimostra che, nel caso in cui abbiamo tre termini invece di due, tale formula diventa:
$$(A ∪ B ∪ C) = A + B + C - (A ∩ B) - (A ∩ C) - (B ∩ C) + (A ∩ B ∩ C)$$
Si arriva quindi alla **forma generale** del principio di inclusione-esclusione, che si ottiene seguendo i seguenti passaggi:
1. includo (sommo) le cardinalità dei singoli;
2. escludo (sottraggo) le cardinalità delle intersezioni a due termini;
3. includo (sommo) le cardinalità delle intersezioni a tre termini;
4. escludo (sottraggo) le cardinalità delle intersezioni a quattro termini;

e così via.

[TEOREMA CON SOMMATORIE: DISPENSA 5]

