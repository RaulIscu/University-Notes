**Python** viene creato da **Guido van Rossum**, e nasce come linguaggio di *scripting* del sistema operativo Amoeba. É progettato in primis per essere leggibile e facile da imparare, e a tal proposito vengono presi vari provvedimenti e decisioni, tra cui:
- vengono sostanzialmente rimosse le *{ }* e i *;* di C, C++ e Java, con le parentesi che vengono invece usate per delimitare blocchi di istruzioni da leggere contemporaneamente;
- l'indentazione viene a far parte della sintassi di scrittura; 
- vengono inseriti molti costrutti facili da leggere.

All’interno della programmazione su Python, alcuni dei mezzi fondamentali sono:
- **variabili**, cioè nomi che corrispondono a posizioni in memoria ben precise, che contengono dei dati;
- **funzioni**, verbi riutilizzabili all’interno del codice che restituiscono un risultato svolgendo una determinata azione;
- **procedure**, simili alle funzioni ma che si limitano a svolgere un compito ben preciso.

I mezzi appena esposti agiscono su determinati dati, che possono essere di vari tipi, tra cui:
- **numeri interi** (**`int`**), codificati come sequenza di cifre binarie, che in Python presentano una precisione “infinita”;
- **numeri con la virgola** (**```float```**), codificati con un numero di bit fisso, che in Python presentano una precisione limitata;
- **valori booleani** (**```bool```**), che indicano se un confronto è vero (**```True```**) o falso (**```False```**), e servono ad indicare al programma l’esecuzione di azioni diverse a seconda di tale condizione;
- **testo**, o **stringhe** (**```str```**), sequenze di caratteri immutabili (se ne possono solo creare di nuove in memoria); ciascun carattere è codificato in Unicode, linguaggio che contiene tutti i caratteri possibili; su Python, una stringa deve essere racchiusa tra *‘ ‘* o *“ “*.

Per conoscere a che tipo appartiene un determinato dato, si può usare il comando ```type(dato)```.