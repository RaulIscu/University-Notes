### Istruzioni aritmetiche

Le principali **istruzioni aritmetiche** previste dall'[[L'architettura RISC-V#L'architettura RISC-V|architettura RISC-V]] sono le seguenti:
- **`add rd, rs1, rs2`**;
- **`addi rd, rs1, 10`**;
- **`sub rd, rs1, rs2`**.

L'istruzione **`add`** corrisponde alla **somma** tra i valori nei registri `rs1` e `rs2`, andando poi a memorizzare il risultato nel registro `rd`.

L'istruzione **`addi`** corrisponde sempre a una somma, ma più in particolare a una **somma in cui è coinvolta una costante** (nell'esempio, vengono sommati il valore memorizzato in `rs1` e la costante $10$); anche in questo caso, il risultato viene memorizzato nel registro `rd`.

L'istruzione **`sub`** corrisponde, infine, alla **sottrazione** tra i valori nei registri `rs1` e `rs2`, andando poi a memorizzare il risultato nel registro `rd`.
___
### Istruzioni di trasferimento dati

Le principali **istruzioni di trasferimento dati** previste dall'architettura RISC-V sono le seguenti:
- **`lw rd, 40(rs3)`**;
- **`lwu rd, 40(rs3)`**;
- **`sw rs1, 40(rs3)`**;
- **`lh rd, 40(rs3)`**;
- **`lhu rd, 40(rs3)`**;
- **`sh rs1, 40(rs3)`**;
- **`lb rd, 40(rs3)`**;
- **`lbu rd, 40(rs3)`**;
- **`sb rs1, 40(rs3)`**;
- **`lr.d rd, (rs3)`**;
- **`sc.d rs1, rs2, (rs3)`**;
- **`lui rd, 0x12345`**.

L'istruzione **`lw`** consiste nella **lettura di una parola** di memoria, e al suo spostamento in un registro. Invece, l'istruzione **`lwu`** consiste nella **lettura di una parola senza segno** della memoria, e al suo spostamento in un registro. L'istruzione **`sw`**, poi, consiste nella **memorizzazione di una parola**, ossia nello spostamento di essa da un registro (nell'esempio, `rs1`) a un indirizzo in memoria (nell'esempio, `rs3 + 40`).

L'istruzione **`lh`** consiste nella **lettura di una mezza parola** di memoria, e al suo spostamento in un registro. Invece, l'istruzione **`lhu`** consiste nella **lettura di una mezza parola senza segno** della memoria, e al suo spostamento in un registro. L'istruzione **`sh`**, poi, consiste nella **memorizzazione di una mezza parola**, ossia nello spostamento di essa da un registro (nell'esempio, `rs1`) a un indirizzo in memoria (nell'esempio, `rs3 + 40`).

L'istruzione **`lb`** consiste nella **lettura di un byte** di memoria, e al suo spostamento in un registro. Invece, l'istruzione **`lbu`** consiste nella **lettura di un byte senza segno** della memoria, e al suo spostamento in un registro. L'istruzione **`sb`**, poi, consiste nella **memorizzazione di un byte**, ossia nello spostamento di esso da un registro (nell'esempio, `rs1`) a un indirizzo in memoria (nell'esempio, `rs3 + 40`).

[ISTRUZIONI LR.D E SC.D]

[ISTRUZIONE LUI]

Nell'utilizzo di molte delle istruzioni di trasferimento dati, si utilizza il valore contenuto in un determinato registro come "**indirizzo di base**", e gli viene sommata una costante di "**offset**": la somma tra questi due valori consisterà tendenzialmente nell'indirizzo di memoria a cui accedere per eseguire l'istruzione in questione. Ad esempio, nell'esempio di `lw`, si legge la parola contenuta in memoria all'indirizzo `rs3 + 40`, e la si sposta nel registro `rd`.
___
### Istruzioni logiche

Le principali **istruzioni logiche** previste dall'architettura RISC-V sono le seguenti:
- **`and rd, rs1, rs2`**;
- **`andi rd, rs1, 0b10101010`**;
- **`or rd, rs1, rs2`**;
- **`ori rd, rs1, 0b10101010`**;
- **`xor rd, rs1, rs2`**;
- **`xori rd, rs1, ob10101010`**.

È importante ricordare che, nel linguaggio assembly dell'architettura RISC-V, le istruzioni logiche eseguono le loro rispettive operazioni **bit a bit**: ad esempio, dato `rs1 = 0b11001100` e `rs2 = 0b10101010`, si avrà che `and rd, rs1, rs2` porterà a memorizzare in `rd` il valore `0b10001000`.

L'istruzione **`and`** restituisce l'AND bit a bit tra i due registri `rs1` e `rs2`, e ne memorizza il risultato in `rd`. L'istruzione **`andi`**, invece, restituisce l'AND bit a bit tra il registro `rs1` e una costante (nell'esempio, `0b10101010`).

L'istruzione **`or`** restituisce l'OR bit a bit tra i due registri `rs1` e `rs2`, e ne memorizza il risultato in `rd`. L'istruzione **`ori`**, invece, restituisce l'OR bit a bit tra il registro `rs1` e una costante (nell'esempio, `0b10101010`).

L'istruzione **`xor`** restituisce lo XOR bit a bit tra i due registri `rs1` e `rs2`, e ne memorizza il risultato in `rd`. L'istruzione **`xori`**, invece, restituisce lo XOR bit a bit tra il registro `rs1` e una costante (nell'esempio, `0b10101010`).
___
### Istruzioni di scorrimento

Le principali **istruzioni di scorrimento** previste dall'architettura RISC-V sono le seguenti:
- **`sll rd, rs1, rs2`**;
- **`slli rd, rs1, 2`**;
- **`srl rd, rs1, rs2`**;
- **`srli rd, rs1, 2`**;
- **`sra rd, rs1, rs2`**;
- **`srai rd, rs1, 2`**.

L'istruzione **`sll`** consiste nello **scorrimento** (o **shift**) **a sinistra** del valore nel registro `rs1` di un numero di posizioni specificato nei 5 bit meno significativi di `rs2`, e memorizza il risultato in `rd` (riempiendo con zeri a destra). Invece, l'istruzione **`slli`** funziona allo stesso modo ma con il numero di posizioni specificato da una **costante** (nell'esempio, $2$ posizioni).

L'istruzione **`srl`** consiste nello **scorrimento** (o **shift**) **a destra** del valore nel registro `rs1` di un numero di posizioni specificato nei 5 bit meno significativi di `rs2`, e memorizza il risultato in `rd` (riempiendo con zeri a sinistra). Invece, l'istruzione **`slli`** funziona allo stesso modo ma con il numero di posizioni specificato da una **costante** (nell'esempio, $2$ posizioni).

L'istruzione **`sra`** consiste nello **scorrimento** (o **shift**) **aritmetico a destra** del valore nel registro `rs1` di un numero di posizioni specificato nei 5 bit meno significativi di `rs2`, e memorizza il risultato in `rd` (riempiendo con bit di segno a sinistra). Invece, l'istruzione **`srai`** funziona allo stesso modo ma con il numero di posizioni specificato da una **costante** (nell'esempio, $2$ posizioni). Questa coppia di istruzioni viene tendenzialmente utilizzata quando si lavora con **valori negativi**.
___
### Istruzioni di salto condizionato

Le principali **istruzioni di salto condizionato** previste dall'architettura RISC-V sono le seguenti:
- **`beq rs1, rs2, 100`**;
- **`bne rs1, rs2, 100`**;
- **`blt rs1, rs2, 100`**;
- **`bltu rs1, rs2, 100`**;
- **`bge rs1, rs2, 100`**;
- **`bgeu rs1, rs2, 100`**.

Possiamo generalizzare queste 6 istruzioni nella formula **`inst rs1, rs2, offset`**, dove `inst` rappresenta la particolare condizione che deve venire valutata, `rs1` e `rs2` rappresentano i due registri da confrontare, e `offset` rappresenta lo **spostamento** (in byte) **relativo al PC** (Program Counter), per calcolare così l'indirizzo a cui saltare.

Analizziamo meglio questa caratteristica. Il PC, o Program Counter, è un registro speciale del processore, che contiene dinamicamente l'indirizzo della prossima istruzione da eseguire; nell'architettura RISC-V, ogni istruzione è lunga 4 byte, quindi di default il PC viene aumentato sempre di 4. Nel caso delle istruzioni di salto condizionato, quindi, aggiungere l'`offset` al PC porta a cambiare il flusso di esecuzione, e a saltare ad altre istruzioni.

Vediamo ora, che condizione vanno a valutare le varie singole istruzioni:
- **`beq`** controlla se `rs1` e `rs2` sono uguali, e in tal caso salta all'indirizzo desiderato;
- **`bne`** controlla se `rs1` e `rs2` sono diversi, e in tal caso salta all'indirizzo desiderato;
- **`blt`** controlla se `rs1` è minore di `rs2` (tenendo conto del segno), e in tal caso salta all'indirizzo desiderato;
- **`bltu`** controlla se `rs1` è minore di `rs2` (senza considerare il segno), e in tal caso salta all'indirizzo desiderato;
- **`bge`** controlla se `rs1` è maggiore o uguale di `rs2` (tenendo conto del segno), e in tal caso salta all'indirizzo desiderato;
- **`bgeu`** controlla se `rs1` è maggiore o uguale di `rs2` (senza considerare il segno), e in tal caso salta all'indirizzo desiderato;
___
### Istruzioni di salto incondizionato

Le principali **istruzioni di salto incondizionato** previste dall'architettura RISC-V sono le seguenti:
- **`jal rd, 100`**;
- **`jalr rd 100(rs1)`**.

L'istruzione **`jal`** ("jump and link") va a salvare nel registro `rd` l'indirizzo dell'istruzione successiva ad essa, dunque `PC + 4`, e in seguito salta all'istruzione che si trova all'indirizzo `PC + offset`, dove `offset` è la costante inserita espressa in byte (nell'esempio, $100$).

L'istruzione **`jalr`** ("jump and link register") funziona sostanzialmente allo stesso modo dell'istruzione appena spiegata, con la differenza che, invece di saltare a `PC + offset`, si salta all'indirizzo dato da `rs1 + offset`.
___