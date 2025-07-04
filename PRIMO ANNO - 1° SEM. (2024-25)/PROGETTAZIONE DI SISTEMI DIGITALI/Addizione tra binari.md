L'**addizione tra binari** funziona in modo sostanzialmente analogo all'addizione tra decimali. I numeri vengono sempre messi in colonna, con le singole cifre nelle colonne corrispondenti, e, nell'addizione di ogni singola colonna, se si ottiene un numero che supera il massimo numero contenibile in una singola cifra, si riporta nella colonna successiva.

La differenza più sostanziale sta proprio nell'ultimo punto: mentre nell'addizione tra decimali una singola cifra può rappresentare al massimo 9, e quindi qualsiasi numero superiore a 9 presenterà una cifra nella colonna delle decine e, dunque, un riporto, nell'addizione tra binari una singola cifra può rappresentare al massimo 1, e quindi qualsiasi numero superiore a 1 presenterà un riporto.

Vediamo un esempio, sommando i binari 1011 e 0011:

![[binaryaddition.png]]

In questo caso, la somma che avviene nella prima colonna avrà come risultato 10₂, ossia 2, dunque si segna 0 e si riporta 1; nella seconda colonna, la somma avrà come risultato 11₂, ossia 3, dunque si segna 1 e si riporta 1; e così via.

In un'addizione tra binari arbitraria, compiuta manualmente, si può tranquillamente sforare il numero di bit dei binari iniziali senza conseguenze; in un sistema digitale, tuttavia, ciò può creare problemi, in quanto il sistema opererà su un numero fisso di bit (pari a quello dei binari iniziali), e ignorerà qualsiasi bit in posizioni superiori a quelle considerate. Quando ciò avviene, si verifica un cosiddetto "***overflow***"; l'avvenire di un *overflow* può essere accertato controllando se vi è un riporto a partire dal *msb* (*most significant bit*).
___
L'addizione tra numeri binari in *[[Sistema binario|floating point]]* risulta meno immediata. Si dovranno seguire, infatti, una serie di passaggi:
1. estrarre i bit relativi al segno e all'esponente dal numero, e preporre un 1 alla mantissa (l'*implicit leading 1*);
2. comparare gli esponenti dei due numeri;
3. se necessario, "[[Moltiplicazione tra binari|shiftare]]" la mantissa del numero con esponente minore verso destra di un numero di bit pari alla differenza tra i due esponenti;
4. sommare le due mantisse;
5. se necessario, normalizzare la mantissa risultante (portare il *floating point* alla sua posizione canonica e modificare di seguito l'esponente);
6. se la parte frazionaria eccede i bit massimi della precisione che si sta utilizzando, arrotondarla;
7. riassemblare il tutto in un numero binario rappresentato in *floating point*.

Per comprendere meglio i vari passaggi, analizziamo un esempio. Sommiamo i numeri 1.5 e 3.25; innanzitutto, convertiamoli in binario rappresentandoli in *floating point*:
$$1.5₁₀ = 0|01111111|10000000000000000000000$$
$$3.25₁₀ = 0|10000000|10100000000000000000000$$
Si tratta di numeri entrambi positivi, con esponenti rispettivamente 127 e 128, e le cui mantisse complete risultano essere 1.1 e 1.101. L'esponente del primo numero risulta essere di un'unità più piccolo rispetto a quello del secondo, quindi la mantissa del primo numero va shiftata verso destra di un bit (1.1 >> 1 = 0.11).

A questo punto, si può procedere alla somma delle due mantisse 0.11 e 1.101, incolonnandole in maniera tale da far coincidere i punti binari di entrambi i numeri; il risultato sarà 10.011 × 2¹, che dovrà essere normalizzato:
$$10.011 × 2^1 = 1.0011 × 2^2$$
Non sarà necessario arrotondare la parte frazionaria, in quanto il suo numero di bit è abbondantemente inferiore a 23. A questo punto possiamo procedere a riassemblare il numero binario risultante:
$$0|10000001|00110000000000000000000$$