Oltre ad assicurarsi che un circuito digitale compia effettivamente la funzione desiderata, nonché minimizzare il più possibile il numero di componenti impiegate per fare ciò, un altro aspetto fondamentale della progettazione di un circuito è l'attenzione ai **tempi**, e come rendere il più veloce possibile un circuito.
___
Un *output* richiede tempo per essere emesso in seguito all'aggiornamento degli *input*. Il ritardo con cui l'*output* viene emesso rispetto all'*input* viene detto "***delay***", ed esso può essere rappresentato in maniera grafica ed esplicita mediante un "**diagramma di tempo**"; ad esempio, di seguito il diagramma di tempo di un *BUFFER*:

![[delay_buffer.png]]

Generalmente, la transizione tra un segnale *LOW* (0) e un segnale *HIGH* (1) viene detta "***rising edge***", e viceversa la transizione tra un segnale *HIGH* e un segnale *LOW* viene detta "***falling edge***". In questo caso, notiamo come la freccia rossa indichi che la *rising edge* dell'*output* Y è causata dalla *rising edge* dell'*input* A. È importante notare, inoltre, che il *delay* di un segnale di *output* viene misurato dal "punto di mezzo" (o ***50% point***) dell'*input* al punto di mezzo dell'*output*, dove per "punto di mezzo" intendiamo il punto, nel tempo, in cui un segnale si trova a metà strada tra un valore *LOW* e un valore *HIGH*.

In particolare nella logica combinatoria, si incontrano dei tipi particolari di *delay*, ossia:
- il ***propagation delay***;
- il ***contamination delay***.

Il *propagation delay*, indicato anche come ***t`pd`***, è definito come il tempo massimo che intercorre tra l'aggiornamento di un *input* e il raggiungimento da parte dell'*output* del suo valore finale; il *contamination delay*, indicato anche come ***t`cd`***, è definito come il tempo minimo che intercorre tra l'aggiornamento di un *input* e l'inizio dell'aggiornamento dell'*output*. Volendo visualizzare graficamente questi due valori nello stesso caso analizzato prima, otterremmo il seguente grafico:

![[delay_buffer_pdcd.png]]

Ci sono diverse cause che possono portare a variazioni del *propagation delay* e del *contamination delay*, tra cui:
- i diversi *delay* della *rising edge* e della *falling edge* di un segnale;
- la presenza di molteplici *input* e *output*, alcuni più veloci di altri;
- il rallentamento o la velocizzazione di un circuito in base alla temperatura.

Oltre a ciò, un fattore determinante risulta essere spesso il **percorso** di un segnale da *input* ad *output*. All'interno di un circuito, si definisce "percorso critico" (o ***critical path***) il percorso più lungo, e dunque più lento, preso da un segnale del circuito; al contrario, si definisce "percorso corto" (o ***short path***) il percorso più corto, e dunque più veloce. La velocità di un percorso è influenzata principalmente dal numero di porte che attraversa. Stabilito ciò, arriviamo a definire più precisamente i valori dei due tipi di *delay* per un circuito combinatorio:
- il *propagation delay* di un circuito combinatorio è dato dalla somma dei vari *propagation delay* degli elementi presenti nel percorso critico;
- il *contamination delay* di un circuito combinatorio è dato dalla somma dei vari *contamination delay* degli elementi presenti nel percorso corto.
___
Essere ben coscienti dei tempi di un circuito risulta importantissimo quando si considerano i possibili "***glitch***", o "***hazard***", dello stesso. Un *glitch* può essere definito, in parole povere, come l'occorrenza di più cambiamenti di *output* a partire da un solo cambiamento di *input*.

Per comprendere meglio il concetto, analizziamo un circuito di esempio:

![[glitch_example1.png]]

Prendiamo in considerazione, quindi, il caso in cui A = 0, C = 1 e B cambia da 1 a 0, operazione che secondo la *[[Mappe di Karnaugh|K-map]]* non dovrebbe produrre cambiamenti nell'*output* del circuito. Per comodità, rappresentiamo il circuito evidenziando lo *short path* e il *critical path*:

![[glitch_example2.png]]

Nella transizione di B da 1 a 0, il segnale sul nodo n2 (che si trova sullo *short path*) va a 0 prima che il segnale sul nodo n1 (che si trova sul *critical path*) possa arrivare a 1; in questa situazione, l'*output* del circuito diventa 0 finché il segnale su n1 non arriverà a 1, portando così a un *glitch*, non previsto dalla *K-map*.

Seppur imprevisto, un *glitch* in un circuito non risulta sempre in un problema vero e proprio: per evitare risultati imprevisti, sarà sufficiente attendere un tempo pari al *propagation delay* del circuito prima di elaborare in qualche modo l'*output* dello stesso. 

Altrimenti, si può evitare a priori il *glitch* aggiungendo delle [[Porte logiche|porte]] al circuito. Analizzando la *K-map* del circuito di esempio, infatti, si nota che il passaggio di B da 1 a 0 solca i perimetri di due raggruppamenti distinti all'interno della mappa: ogni qualvolta che avviene ciò in un circuito, è possibile che avvenga un *glitch*. In particolare, quest'ultimo è sostanzialmente garantito se, nel concreto, le componenti coinvolte in uno degli implicanti primi si spengono prima che quelle coinvolte nell'altro si possano accendere. Per evitare questo problema, dunque, possiamo aggiungere un implicante al circuito, in modo che esso, seppur ridondante, vanifichi la possibilità di *glitch*. La nuova *K-map* una volta completata questa operazione sarà:

![[glitch_fix.png]]