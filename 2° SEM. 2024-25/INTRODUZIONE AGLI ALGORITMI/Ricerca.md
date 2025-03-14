Uno dei problemi più ricorrenti e importanti in ambito informatico è quello della **ricerca** di un dato specifico in un insieme di altri dati (numeri, stringhe, o qualsiasi altro elemento).

Possiamo formalizzare questo problema descrivendo gli *input* e gli *output* di una possibile soluzione:
1. come ***input*** si riceverà un *array* A di *n* elementi, e un valore v;
2. come ***output***, invece, si otterrà un indice *i* tale che A[i] = v, oppure un determinato valore `None` se il valore v non è presente nell'*array*.
___
Analizziamo delle possibili implementazioni di algoritmi che risolvono questo problema.

Un primo approccio consiste nella cosiddetta **ricerca sequenziale**. Si tratta dell'algoritmo più semplice utilizzabile, e consiste nei seguenti passaggi:
- ispezionare gli elementi dell'*array* uno alla volta;
- confrontare ciascun elemento con v;
- restituire il risultato, interrompendo il procedimento nell'eventualità in cui si trova v.

[PSEUDOCODICE e COSTO COMPUTAZIONALE: 04_Ricerca2025]

Si può, alternativamente, applicare una **ricerca binaria** (o **ricerca dicotomica**). Questo algoritmo necessita, come premessa per poter funzionare in maniera affidabile, che l'*array* su cui si sta lavorando sia ordinato; si può riassumere nei seguenti passaggi:
- ispezionare l'elemento centrale della sequenza, e se esso corrisponde a v si può terminare qui;
- se l'elemento non corrisponde a v, nel caso in cui v sia più piccolo dell'elemento trovato si ripete il primo passaggio lavorando solo sulla metà inferiore dell'*array*, altrimenti si lavora nella metà superiore.

[PSEUDOCODICE e COSTO COMPUTAZIONALE]

[RICERCA COSTANTE]