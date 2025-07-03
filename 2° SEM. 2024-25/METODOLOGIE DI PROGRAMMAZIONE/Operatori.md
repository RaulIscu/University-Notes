Si possono distinguere principalmente tre tipi di **operatori** presenti in Java:
- operatori **logici**;
- operatori **di confronto**;
- operatori **aritmetici**.
___
### Operatori logici

Gli **operatori logici** sono operatori che svolgono operazioni logiche di algebra booleana, e vengono quindi utilizzati in relazione a metodi e istruzioni che restituiscono in qualche modo dei valori di tipo `boolean`.

In Java, i principali operatori logici sono i seguenti:
- **`&&`** indica un ***AND***;
- **`||`** indica un ***OR***;
- **`!`** indica un ***NOT***.
___
### Operatori di confronto

Gli **operatori di confronto** sono operatori che servono, come suggerisce il nome, a confrontare una coppia di valori, dati o oggetti, e restituiscono un valore di tipo `boolean` che rispecchia la veridicità o meno della relazione espressa dall'operatore.

In Java, i principali operatori di confronto sono i seguenti:
- **`==`**, corrisponde a dire "**è uguale a**";
- **`!=`**, corrisponde a dire "**è diverso da**";
- **`<`**, corrisponde a dire "**è minore di**";
- **`<=`**, corrisponde a dire "**è minore o uguale a**";
- **`>`**, corrisponde a dire "**è maggiore di**";
- **`>=`**, corrisponde a dire "**è maggiore o uguale a**".

È opportuna una precisazione relativamente al funzionamento dell'operatore `==` quando i due termini confrontati sono degli oggetti: in tal caso, l'operatore restituirà `true`, e dunque che i due oggetti sono "uguali", solo ed esclusivamente se essi rappresentano la stessa identica istanza; per confrontare, invece, a livello logico due oggetti (verificare se presentano le stesse caratteristiche, e se, pur essendo istanze diverse, costituiscono sostanzialmente lo stesso oggetto), si dovrà utilizzare il metodo `o1.equals(o2)`.
___
### Operatori aritmetici

Gli **operatori aritmetici** sono operatori che svolgono delle semplici operazioni matematiche, come moltiplicazione, divisione, addizione, ecc., tra due valori numerici.

In Java, i principali operatori aritmetici (in ordine di precedenza) sono i seguenti:
- **`*`**, che indica una moltiplicazione;
- **`/`**, che indica una divisione;
- **`%`**, che indica il resto di una divisione;
- **`+`**, che indica un'addizione;
- **`-`**, che indica una sottrazione.
___
### Ordine di precedenza tra gli operatori


___
