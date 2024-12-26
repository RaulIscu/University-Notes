In generale, un diagramma che rappresenta graficamente la funzionalità di un circuito digitale, mostrandone i vari elementi e i collegamenti che sussistono tra di essi, viene definito "**diagramma schematico**".
___
Potenzialmente, un diagramma schematico può essere disegnato come si desidera, ma per comodità si sono stabilite convenzionalmente delle regole di base che ogni diagramma schematico dovrebbe seguire. Le principali sono:
- i segnali di *input* si trovano nella parte sinistra (o superiore) del diagramma;
- i segnali di *output* si trovano nella parte destra (o inferiore) del diagramma;
- se possibile, le porte logiche dovrebbero confluire una nell'altra da sinistra verso destra;
- è preferibile rappresentare cavi "dritti" rispetto a cavi che presentano vari angoli e spigoli;
- i cavi si collegano sempre tra di loro in un incrocio a T;
- se due cavi si incrociano formando una croce, essi saranno collegati solo se vi sarà un punto al centro di quest'ultima, altrimenti non vi sarà collegamento.

Una qualsiasi equazione booleana, se posta in forma [[Circuiti combinatori|SOP]], può essere disegnata sistematicamente senza problemi con un diagramma schematico che segue le regole appena stabilite. Per farlo, converrà prima di tutto rappresentare varie colonne per gli *input* (con annesse le relative porte *NOT*, in modo da avere anche i complementi degli *input* se necessari); poi, si avranno varie righe di porte *AND*, una per ognuno dei mintermini; infine, per l'*output*, si dovrà inserire una porta *OR* in cui confluiranno i mintermini relativi a tale *output*. Un esempio di diagramma disegnato così è il seguente:

![[pla_example.png]]
Un diagramma disegnato in questo stile, seguendo queste convenzioni, viene chiamato ***PLA*** (***programmable logic array***).