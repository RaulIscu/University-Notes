Per convertire un **decimale in binario**, si possono usare due metodi alternativi, a seconda se si vuole operare da destra verso sinistra o viceversa.

Il primo metodo, che opera da destra verso sinistra, consiste nel:
- dividere il numero per 2;
- segnare il resto della divisione (che sarà o 1 o 0) a sinistra di un eventuale cifra già presente;
- ripetere i primi due passaggi fino ad aver esaurito il dividendo.

Ad esempio, per convertire il decimale 84₁₀ in binario, si fa la divisione 84/2 = 42 con resto 0, e quindi si segna 0; poi, la divisione 42/2 = 21 con resto 0, e quindi si segna 0; poi, la divisione 21/2 = 10 con resto 1, e quindi si segna 1; poi, la divisione 10/2 = 5 con resto 0, e quindi si segna 0; poi, la divisione 5/2 = 2 con resto 1, e quindi si segna 1; poi, la divisione 2/2 = 1 con resto 0, e quindi si segna 0; infine, la divisione 1/2 = 0 con resto 1, e quindi si segna 1. Si ottiene così:
$$84₁₀ = 1010100₂$$
Il secondo metodo, che opera da sinistra verso destra, consiste nel:
- trovare la più grande potenza di 2 che sia minore o uguale al numero da convertire;
- sottrarla al numero e segnare un 1;
- per ogni potenza di 2 minore di quella iniziale, controllare se essa sia minore o uguale al nuovo numero, e ripetere il secondo passaggio a destra delle cifre già presenti se ciò si verifica, altrimenti segnare uno 0 e passare alla prossima.

Ad esempio, per convertire il decimale 84₁₀ in binario, si trova la più grande potenza di 2 che sia minore o uguale a 84, ossia 2⁶ = 64, la si sottrae (84 - 64 = 20) e si segna 1; poi, 2⁵ = 32 > 20, quindi si segna 0; poi, 2⁴ = 16 ≤ 20, quindi si sottrae (20 - 16 = 4) e si segna 1; poi, 2³ = 8 > 4, quindi si segna 0; poi, 2² = 4 ≤ 4, quindi si sottrae (4 - 4 = 0) e si segna 1; essendo rimasto 0, le cifre rimanenti saranno tutte 0. Si ottiene così:
$$84₁₀ = 1010100₂$$
___
Per convertire un **binario in decimale**, si moltiplica ogni cifra del numero binario, da destra verso sinistra, per 2*ⁱ* (dove *i* è un numero che va da 0 a N - 1, con N pari al numero delle cifre del numero binario), e si sommano i risultati.

Ad esempio, per convertire il binario 10110₂ in decimale, si fa:
$$10110₂ = (0 * 2^0) + (1 * 2^1) + (1 * 2^2) + (0 * 2^3) + (1 * 2^4) = 22₁₀$$
___
Per convertire un **decimale in esadecimale**, si possono usare due metodi alternativi, a seconda se si vuole operare da destra verso sinistra, in maniera analoga alla conversione di decimali in binari.

Il primo metodo, che opera da destra verso sinistra, consiste nel:
- dividere il numero per 16;
- segnare il resto della divisione (che sarà incluso tra 0 e 15) a sinistra di un eventuale cifra già presente;
- ripetere i primi due passaggi fino ad aver esaurito il dividendo.

Ad esempio, per convertire il decimale 333₁₀ in esadecimale, si fa la divisione 333/16 = 20 con resto 13, e quindi si segna D; poi, la divisione 20/16 = 1 con resto 4, e quindi si segna 4; infine, la divisione 1/16 = 0 con resto 1, e quindi si segna 1. Si ottiene così:
$$333₁₀ = 14D₁₆$$
Il secondo metodo, che opera da sinistra verso destra, consiste nel:
- trovare la più grande potenza di 16 che sia minore o uguale al numero da convertire;
- segnare il numero di volte che tale potenza è contenuta nel numero (da 0 a 15) e sottrarre ad esso la potenza moltiplicata per tale numero;
- per ogni potenza di 16 minore di quella iniziale, controllare se essa sia minore o uguale al nuovo numero, e ripetere il secondo passaggio a destra delle cifre già presenti se ciò si verifica.

Ad esempio, per convertire il decimale 333₁₀ in esadecimale, si trova la più grande potenza di 16 che sia minore o uguale a 333, ossia 16² = 256, la si sottrae (333 - (256 * 1) = 77) e si segna 1; poi, 16¹ = 16 è contenuta 4 volte in 77, quindi si sottrae (77 - (16 * 4) = 13) e si segna 4; infine, 16⁰ = 1 è contenuta 13 volte in 13, quindi si sottrae (13 - (1 * 13) = 0) e si segna D. Si ottiene così:
$$333₁₀ = 14D₁₆$$
___
Per convertire un **esadecimale in decimale**, si moltiplica ogni cifra del numero esadecimale, da destra verso sinistra, per 16*ⁱ* (dove *i* è un numero che va da 0 a N - 1, con N pari al numero delle cifre del numero esadecimale), e si sommano i risultati.

Ad esempio, per convertire l'esadecimale 2ED₁₆ in decimale, si fa:
$$2ED₁₆ = (13 * 16^0) + (14 * 16^1) + (2 * 16^2) = 749₁₀$$
___
Per convertire un **binario in esadecimale**, si suddivide il numero in *nibble* da 4 bit andando da destra verso sinistra (completando, eventualmente, l'ultimo *nibble* con degli zeri a sinistra dell'ultimo bit), e a ogni *nibble* si associa la cifra esadecimale corrispondente.

Ad esempio, per convertire il binario 1111010₂ in esadecimale, lo si suddivide nei *nibble* 1010 e (0)111, che corrispondono rispettivamente alle cifre esadecimali A e 7. Si ottiene così:
$$1111010₂ = 7A₁₆$$
___
Per convertire un **esadecimale in binario**, basterà operare in maniera inversa alla conversione da binario a esadecimale, associando a ogni cifra esadecimale il *nibble* di bit binari corrispondente.

Ad esempio, per convertire 2ED₁₆ in binario, si considera che 2₁₆ = 0010₂, che E₁₆ = 1110₂ e che D₁₆ = 1101₂. Si ottiene così:
$$2ED₁₆ = 001011101101₂$$
