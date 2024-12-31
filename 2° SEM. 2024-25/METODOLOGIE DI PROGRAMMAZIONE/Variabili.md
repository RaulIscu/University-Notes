In Java, possiamo considerare una **variabile** come un contenitore per un determinato elemento modificabile, che si comporta come quest'ultimo. Una variabile può essere di vari "**tipi**", tra cui:
- `int`, ossia un numero intero;
- `double`, ossia un numero con la virgola;
- `boolean`, ossia un valore booleano (`true` o `false`);
- `char`, ossia un singolo carattere di testo (un elemento di tipo `char` va dichiarato tra singoli apici);
- `string`, ossia un gruppo di caratteri di testo (un elemento di tipo `string` va dichiarato tra doppi apici).

Tra i vari tipi di variabili, distinguiamo le variabili **primitive** (`int`, `double`, `char`, `boolean`), costituite da valori semplici che vengono memorizzati direttamente in memoria in una posizione definita "*stack*", e le variabili **non primitive** (`string`, `array`, `object`), che contengono in realtà un indirizzo di memoria nello *stack* che indica a sua volta una posizione definita "*heap*".
___
Per creare una variabile, si seguono principalmente due passaggi:
1. **dichiarazione**;
2. **assegnazione**.

Per dichiarare una variabile, si dovrà prima dichiarare il tipo a cui appartiene tale variabile (ad esempio, `int`), seguito dal nome che si vuole dare alla variabile che si sta dichiarando. Finita la dichiarazione, si dovrà chiudere la riga di codice con un *semicolon* (`;`). Limitarsi a ciò, tuttavia, porterà a creare in sostanza una variabile vuota; bisognerà, dunque, assegnarle un valore, semplicemente con un `=` seguito dal valore da assegnare alla variabile che si sta considerando. Nel complesso, inizializzare una variabile richiede un procedimento del genere:
```
int x = 21;
```
Naturalmente, bisogna fare attenzione nell'assegnare valori a una variabile dichiarata, in quanto si avranno errori nel caso in cui il valore assegnato non rispecchia il tipo che si è dichiarato per tale variabile.

In particolare in Java, nel dichiarare il nome di una variabile si tende a rispettare una convenzione chiamata "***camel case***", secondo la quale se il nome di una variabile è costituito da due o più parole, la prima va scritta completamente in minuscolo, mentre le seguenti vanno scritte tutte con l'iniziale maiuscola.