Si possono distinguere principalmente tre tipi di **operatori** presenti in Java:
- operatori **logici**;
- operatori **di confronto**;
- operatori **aritmetici**;
- operatori **di assegnamento**.

Le operazioni prescritte da questi operatori vengono eseguite secondo un **ordine di precedenza** ben preciso, ossia:
1. le operazioni racchiuse tra parentesi tonde (`()`);
2. le operazioni aritmetiche, secondo l'ordine di precedenza interno ad esse;
3. le operazioni logiche bit a bit;
4. le operazioni di confronto;
5. le operazioni logiche.

## Operatori logici

Gli **operatori logici** sono operatori che svolgono operazioni logiche di algebra booleana, e vengono quindi utilizzati in relazione a valori booleani.

In Python, i principali operatori logici sono i seguenti:
- **`and`**, che indica un **AND**;
- **`or`**, che indica un **OR**;
- **`not`**, che indica un **NOT**.

Oltre a questi, che sono gli operatori logici più utilizzati e comuni, ci sono anche le loro varianti "**bit a bit**", che vengono utilizzate per operare su numeri binari. In Python, i principali operatori logici bit a bit sono i seguenti:
- **`&`**, che indica un **AND bit a bit**;
- **`|`**, che indica un **OR bit a bit**;
- **`~`**, che indica un **NOT bit a bit**.
___
## Operatori di confronto

Gli **operatori di confronto** sono operatori che servono, come suggerisce il nome, a confrontare una coppia di valori, dati o oggetti, e restituiscono un valore booleano che rispecchia la veridicità o meno della relazione espressa dall'operatore.

In Python, i principali operatori di confronto sono i seguenti:
- **`==`**, corrisponde a dire "**è uguale a**";
- **`!=`**, corrisponde a dire "**è diverso da**";
- **`<`**, corrisponde a dire "**è minore di**";
- **`<=`**, corrisponde a dire "**è minore o uguale a**";
- **`>`**, corrisponde a dire "**è maggiore di**";
- **`>=`**, corrisponde a dire "**è maggiore o uguale a**".

Oltre agli operatori di confronto propriamente detti, Python prevede anche degli **operatori di identità**, il cui scopo non è confrontare il contenuto di due variabili, ma valutare se le due variabili confrontate sono concretamente la stessa, e occupano dunque la stessa zona di memoria. Gli operatori di identità principali sono:
- **`is`**, che restituisce `True` se le due variabili confrontate coincidono;
- **`is not`**, che restituisce `True` se le due variabili confrontate non coincidono.
___
## Operatori aritmetici

Gli **operatori aritmetici** sono operatori che svolgono delle semplici operazioni matematiche, come moltiplicazione, divisione, addizione, ecc., tra due valori numerici.

In Python, i principali operatori aritmetici (in ordine di precedenza) sono i seguenti:
- **`**`**, che indica una potenza (il valore a sinistra è la base, il valore a destra è l'esponente);
- **`*`**, che indica una moltiplicazione;
- **`/`**, che indica una divisione;
- **`//`**, che indica la parte intera di una divisione;
- **`%`**, che indica il resto di una divisione;
- **`+`**, che indica un'addizione;
- **`-`**, che indica una sottrazione.
___
## Operatori di assegnamento

Gli **operatori di assegnamento** sono operatori utilizzati, come suggerisce il nome, per assegnare valori alle variabili.

In Python, i principali operatori di assegnamento sono i seguenti:
- **`=`**, che rappresenta un regolare assegnamento;
- **`+=`**, che rappresenta l'assegnamento del valore della variabile sommato a un determinato valore (ad esempio, `x += 5` equivale a scrivere `x = x + 5`);
- **`-=`**, che rappresenta l'assegnamento del valore della variabile a cui viene sottratto un determinato valore (ad esempio, `x -= 5` equivale a scrivere `x = x - 5`);
- **`*=`**, che rappresenta l'assegnamento del valore della variabile che viene moltiplicato per un determinato valore (ad esempio, `x *= 5` equivale a scrivere `x = x * 5`);
- **`/=`**, che rappresenta l'assegnamento del valore della variabile diviso per un determinato valore (ad esempio, `x /= 5` equivale a scrivere `x = x / 5`);
- **`//=`**, che rappresenta l'assegnamento alla variabile della parte intera della divisione tra il valore della variabile e un determinato valore (ad esempio, `x //= 5` equivale a scrivere `x = x // 5`);
- **`%=`**, che rappresenta l'assegnamento alla variabile del resto della divisione tra il valore della variabile e un determinato valore (ad esempio, `x %= 5` equivale a scrivere `x = x % 5`);
- **`&=`**, che rappresenta l'assegnamento alla variabile dell'AND bit a bit tra il valore della variabile e un determinato valore (ad esempio, `x &= 5` equivale a scrivere `x = x & 5`);
- **`|=`**, che rappresenta l'assegnamento alla variabile dell'OR bit a bit tra il valore della variabile e un determinato valore (ad esempio, `x |= 5` equivale a scrivere `x = x | 5`);
- **`:=`**, che consente di assegnare un valore alla variabile e, contemporaneamente, di stamparlo (ad esempio, `x := 5` equivale a scrivere prima `x = 5` e poi `print(x)`).
___