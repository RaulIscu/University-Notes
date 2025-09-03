## Gerarchia delle memorie

Fin dal principio dell'era dell'informatica, i programmatori hanno sempre agognato una memoria illimitata e al tempo stresso velocissima, che possa contenere tutti i dati che si desiderano e che possa permettere l'accesso ad essi in fretta. Naturalmente, una memoria che rispetti concretamente queste esigenze non esiste, ma ci sono varie tecniche che si possono utilizzare per creare una memoria che ci si avvicini il più possibile.

La prima di queste tecniche che analizzeremo è il cosiddetto "**principio di località**". Così come uno studente, interessato a una determinata materia, non ha bisogno di dover consultare con la stessa probabilità tutti i libri di una biblioteca, così **un programma non deve accedere, con la stessa probabilità, a tutta la memoria a sua disposizione**. Di conseguenza, il principio di località afferma, in sostanza, che **un programma, in un certo istante di tempo, accede soltanto a una porzione relativamente piccola della memoria**. Questo principio può essere reinterpretato come l'unione di due sotto-principi, ossia:
- il principio di **località temporale**;
- il principio di **località spaziale**.

In particolare, il primo afferma che, **se si accede a una certa locazione di memoria, è probabile che vi si acceda di nuovo poco tempo dopo**; il secondo, invece, afferma che **se si accede a una certa locazione di memoria, è probabile che in seguito si acceda a locazioni vicine ad essa**. Questi principi emerge in modo spontaneo dalla struttura tipica dei programmi: ad esempio, all'interno di un ciclo, dati e istruzioni vengono ripetutamente letti dalla memoria, dimostrando un elevato livello di località temporale; inoltre, le istruzioni di un programma sono normalmente memorizzate in sequenza, portando in questo caso a una spiccata località spaziale.

La conoscenza di questi principi viene sfruttata per **strutturare la memoria di un [[Il calcolatore#Da cosa è composto un calcolatore?|calcolatore]] in forma gerarchica**, rispettando quella che viene chiamata "**gerarchia delle memorie**".

La **gerarchia delle memorie** consiste in un insieme di **livelli di memoria**, ciascuno caratterizzato da una **diversa velocità di accesso** e una **diversa dimensione**. A parità di capacità, le memorie più veloci hanno tendenzialmente un costo più elevato per singolo bit rispetto a quelle più lente, dunque di solito sono più piccole. **La memoria più veloce è posta più vicino al processore**, mentre quella più lenta è quella più "lontana" dallo stesso.


___

[pag. 341... 18, slide 3]