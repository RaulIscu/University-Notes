L'**addizione tra binari** funziona in modo sostanzialmente analogo all'addizione tra decimali. I numeri vengono sempre messi in colonna, con le singole cifre nelle colonne corrispondenti, e, nell'addizione di ogni singola colonna, se si ottiene un numero che supera il massimo numero contenibile in una singola cifra, si riporta nella colonna successiva.

La differenza più sostanziale sta proprio nell'ultimo punto: mentre nell'addizione tra decimali una singola cifra può rappresentare al massimo 9, e quindi qualsiasi numero superiore a 9 presenterà una cifra nella colonna delle decine e, dunque, un riporto, nell'addizione tra binari una singola cifra può rappresentare al massimo 1, e quindi qualsiasi numero superiore a 1 presenterà un riporto.

Vediamo un esempio, sommando i binari 1011 e 0011:

![[binaryaddition.png]]

In questo caso, la somma che avviene nella prima colonna avrà come risultato 10₂, ossia 2, dunque si segna 0 e si riporta 1; nella seconda colonna, la somma avrà come risultato 11₂, ossia 3, dunque si segna 1 e si riporta 1; e così via.

In un'addizione tra binari arbitraria, compiuta manualmente, si può tranquillamente sforare il numero di bit dei binari iniziali senza conseguenze; in un sistema digitale, tuttavia, ciò può creare problemi, in quanto il sistema opererà su un numero fisso di bit (pari a quello dei binari iniziali), e ignorerà qualsiasi bit in posizioni superiori a quelle considerate. Quando ciò avviene, si verifica un cosiddetto "***overflow***"; l'avvenire di un *overflow* può essere accertato controllando se vi è un riporto a partire dal *msb* (*most significant bit*).