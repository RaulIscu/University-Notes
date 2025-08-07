## Da decimale a binario

Per convertire un **decimale in binario**, si possono usare due metodi alternativi, a seconda se si vuole operare da destra verso sinistra o viceversa.

Il primo metodo, che opera **da destra verso sinistra**, consiste nel:
- dividere il numero decimale per $2$;
- segnare il resto della divisione (che sarà o $0$ o $1$) a sinistra di un eventuale cifra già presente;
- ripetere i primi due passaggi fino ad aver esaurito il dividendo.

Ad esempio, per convertire il decimale $84_{10}$ in binario, si fa la divisione $84 \div 2 = 42$ con resto $0$, e quindi si segna $0$; poi, la divisione $42 \div 2 = 21$ con resto $0$, e quindi si segna $0$; poi, la divisione $21 \div 2 = 10$ con resto $1$, e quindi si segna $1$; poi, la divisione $10 \div 2 = 5$ con resto $0$, e quindi si segna $0$; poi, la divisione $5 \div 2 = 2$ con resto $1$, e quindi si segna $1$; poi, la divisione $2 \div 2 = 1$ con resto $0$, e quindi si segna $0$; infine, la divisione $1 \div 2 = 0$ con resto $1$, e quindi si segna $1$. Si ottiene così:
$$84_{10} = 1010100_{2}$$
Il secondo metodo, che opera da sinistra verso destra, consiste nel:
- trovare la più grande potenza di $2$ che sia minore o uguale al numero decimale da convertire;
- sottrarla al numero decimale e segnare un $1$;
- per ogni potenza di $2$ minore di quella iniziale, controllare se essa sia minore o uguale al nuovo numero, e ripetere il secondo passaggio segnando $1$ a destra delle cifre già presenti se ciò si verifica, altrimenti segnare uno $0$ e passare alla prossima.

Ad esempio, per convertire il decimale $84_{10}$ in binario, si trova la più grande potenza di $2$ che sia minore o uguale a $84$, ossia $2^6 = 64$, la si sottrae ($84 - 64 = 20$) e si segna $1$; poi, $2^5 = 32 > 20$, quindi si segna $0$; poi, $2^4 = 16 \le 20$, quindi si sottrae ($20 - 16 = 4$) e si segna $1$; poi, $2^3 = 8 > 4$, quindi si segna $0$; poi, $2^2 = 4 \le 4$, quindi si sottrae ($4 - 4 = 0$) e si segna $1$; essendo rimasto $0$, le cifre rimanenti saranno tutte $0$. Si ottiene così:
$$84_{10} = 1010100_{2}$$
___
## Da binario a decimale

Per convertire un **binario in decimale**, si moltiplica ogni cifra del numero binario, da destra verso sinistra, per $2^n$ (dove $n$ è un numero che va da $0$ a $N - 1$, con $N$ pari al numero delle cifre del numero binario), e si sommano i risultati.

Ad esempio, per convertire il binario $10110_{2}$ in decimale, si fa:
$$10110_{2} = (0 \cdot 2^0) + (1 \cdot 2^1) + (1 \cdot 2^2) + (0 \cdot 2^3) + (1 \cdot 2^4) = 22_{10}$$
___
## Da decimale a esadecimale

Per convertire un **decimale in esadecimale**, si possono usare due metodi alternativi, a seconda se si vuole operare da destra verso sinistra o viceversa, in maniera analoga alla conversione di decimali in binari.

Il primo metodo, che opera da destra verso sinistra, consiste nel:
- dividere il numero decimale per $16$;
- segnare il resto della divisione (che sarà incluso tra $0$ e $15$) a sinistra di un eventuale cifra già presente;
- ripetere i primi due passaggi fino ad aver esaurito il dividendo.

Ad esempio, per convertire il decimale $333_{10}$ in esadecimale, si fa la divisione $333 \div 16 = 20$ con resto $13_{10} = 0xD$, e quindi si segna $D$; poi, la divisione $20 \div 16 = 1$ con resto $4$, e quindi si segna $4$; infine, la divisione $1 \div 16 = 1$ con resto $1$, e quindi si segna $1$. Si ottiene così:
$$333_{10} = 0x14D$$
Il secondo metodo, che opera da sinistra verso destra, consiste nel:
- trovare la più grande potenza di $16$ che sia minore o uguale al numero decimale da convertire;
- segnare il numero di volte che tale potenza è contenuta nel numero decimale (da $0$ a $15$) e sottrarre ad esso la potenza moltiplicata per tale numero;
- per ogni potenza di $16$ minore di quella iniziale, controllare se essa sia minore o uguale al nuovo numero, e ripetere il secondo passaggio segnando a destra delle cifre già presenti se ciò si verifica.

Ad esempio, per convertire il decimale $333_{10}$ in esadecimale, si trova la più grande potenza di $16$ che sia minore o uguale a $333$, ossia $16^2 = 256$, la si sottrae ($333 - (256 \cdot 1) = 77$) e si segna $1$; poi, $16^1 = 16$ è contenuta $4$ volte in $77$, quindi si sottrae ($77 - (16 \cdot 4) = 13$) e si segna $4$; infine, $16^0 = 1$ è contenuta $13$ volte in $13$, quindi si sottrae ($13 - (1 \cdot 13) = 0$) e si segna $D$. Si ottiene così:
$$333_{10} = 0x14D$$
___
## Da esadecimale a decimale

Per convertire un **esadecimale in decimale**, si moltiplica ogni cifra del numero esadecimale, da destra verso sinistra, per $16^n$ (dove $n$ è un numero che va da $0$ a $N - 1$, con $N$ pari al numero delle cifre del numero esadecimale), e si sommano i risultati.

Ad esempio, per convertire l'esadecimale $0x2ED$ in decimale, si fa:
$$0x2ED = (13 \cdot 16^0) + (14 \cdot 16^1) + (2 \cdot 16^2) = 749_{10}$$
___
## Da binario a esadecimale

Per convertire un **binario in esadecimale**, si suddivide il numero in nibble da 4 bit andando da destra verso sinistra (completando, eventualmente, l'ultimo nibble con degli zeri a sinistra dell'ultimo bit), e a ogni nibble si associa la cifra esadecimale corrispondente.

Ad esempio, per convertire il binario $1111010_{2}$ in esadecimale, lo si suddivide nei nibble $1010$ e $(0)111$, che corrispondono rispettivamente alle cifre esadecimali $A$ e $7$. Si ottiene così:
$$1111010_{2} = 0x7A$$
___
## Da esadecimale a binario

Per convertire un **esadecimale in binario**, basterà operare in maniera inversa alla conversione [[Conversioni tra decimali, binari ed esadecimali#Da binario a esadecimale|da binario a esadecimale]], associando a ogni cifra esadecimale il nibble di bit corrispondente.

Ad esempio, per convertire $0x2ED$ in binario, si considera che $0x2 = 0010_{2}$, che $0xE = 1110_{2}$ e che $0xD = 1101_{2}$. Si ottiene così:
$$0x2ED = 001011101101_{2}$$
___