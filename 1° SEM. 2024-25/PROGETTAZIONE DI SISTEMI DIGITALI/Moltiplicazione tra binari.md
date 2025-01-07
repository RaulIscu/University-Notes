Le **moltiplicazioni tra binari** funzionano in maniera analoga, in realtà, alle moltiplicazioni tra numeri decimali. Dopo aver appropriamente incolonnato i numeri da moltiplicare, si procede al calcolo dei vari "prodotti parziali", ottenuti moltiplicando il moltiplicando per ogni singola cifra del moltiplicatore; come per i numeri decimali, ognuno di questi prodotti parziali andrà poi appuntato spostato a sinistra di una cifra (in questo caso, di un bit) rispetto a quello precedente. Una volta trovati tutti i prodotti parziali ed essersi assicurati di averli incolonnati accuratamente, si può procedere alla loro somma. 

Di seguito, per esempio, la moltiplicazione tra i numeri 5 (0101₂) e 7 (0111₂):

![[binarymult.png]]

___
Un tipo particolare di moltiplicazione, nonché di divisione, è l'utilizzo di "***shifters***", che consentono di moltiplicare o dividere un numero binario per una determinata potenza di 2. Infatti:
- shiftare un numero binario verso sinistra di *N* bit vuol dire moltiplicarlo per la potenza di 2 con esponente *N*;
- shiftare un numero binario verso destra di *N* bit vuol dire dividerlo per la potenza di 2 con esponente *N*.

Gli *shifters* sono "**>>**" per le divisioni e "**<<**" per le moltiplicazioni. Vediamo degli esempi che coinvolgono numeri binari rappresentati in [[Sistema binario|complemento a due]]:
$$11101 << 2 = 10100$$
$$10000 >> 2 = 11100$$
___
La moltiplicazione tra numeri binari in *[[Sistema binario|floating point]]* risulta meno immediata. Si dovranno seguire, infatti, una serie di passaggi:
1. estrarre gli esponenti dei due numeri e sommarli;
2. moltiplicare le mantisse tra di loro;
3. se necessario, normalizzare il risultato;
4. riassemblare il numero binario risultante.

