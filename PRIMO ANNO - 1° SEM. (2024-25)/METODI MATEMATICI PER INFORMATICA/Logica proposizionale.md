Nell'ambito della **logica proposizionale**, si studiano e si approfondiscono le proprietà di alcuni costrutti logici utilizzati nel linguaggio naturale e nella pratica scientifica e matematica, quali il "***non***" (negazione), l’"***oppure***" (disgiunzione), l’"***e***" (congiunzione), il "***se... allora***" (implicazione) o il "***se e solo se***" (equivalenza, doppia implicazione).

Per comprendere meglio come la logica proposizionale analizza un determinato argomento logico, vediamo un esempio. Supponiamo di voler analizzare il seguente argomento matematico:
1. se *a* = 0 e *b* = 0, allora *a × b* = 0;
2. *a × b* ≠ 0;
3. *a* ≠ 0 e *b* ≠ 0.

Ci accorgiamo, intuitivamente, che il punto 3 è la conseguenza delle premesse dei punti 1 e 2. Come possiamo **formalizzare** quest'argomento? Innanzitutto, si identificano le "**parti atomiche**" di quest'ultimo, ossia quelle parti logiche che possono essere solo vere o false e che non possono essere ulteriormente analizzate: in questo caso, le parti atomiche sono "*a = 0*", che indicheremo con *A*, "*b = 0*", che indicheremo con *B*, e "*a × b = 0*", che indicheremo con *C*. A questo punto, procediamo a formalizzare il tutto sostituendo ai costrutti del linguaggio naturale dei "**connettivi booleani**", ossia simboli come:
- **¬**, che rappresenta la negazione (*non*);
- **∨**, che rappresenta la disgiunzione (*oppure*);
- **∧**, che rappresenta la congiunzione (*e*);
- **→**, che rappresenta l'implicazione (*se... allora*);
- **↔**, che rappresenta la doppia implicazione (*se e solo se*).

Utilizzando queste componenti per formalizzare l'esempio precedente, si ottiene:
1. *A ∨ B → C*;
2. *¬ C*;
3. *¬ A ∧ ¬ B*.

È importante ricordare che un argomento può essere ritenuto "**valido**" o "**corretto**" ogni qualvolta in cui, se le premesse sono vere, allora è vera la conclusione. Ciò non implica, tuttavia, che le premesse siano concretamente vere e questo fattore non altera la correttezza di un argomento logico.
___
Degli argomenti formalizzati mediante la logica proposizionale sono scritti in un "**linguaggio proposizionale**", ossia un insieme *L* di simboli contenente:
- dei **connettivi logici** (o booleani): ¬, ∨, ∧, →, ↔;
- le **parentesi tonde** chiuse e aperte;
- una quantità finita o infinita numerabile di simboli (distinti dai connettivi e dalle parentesi), detti **variabili proposizionali**, il cui insieme viene indicato con VAR*L*.

Dunque, sia *L* un linguaggio proposizionale. L’insieme delle proposizioni (o formule ben formate) in *L* è il minimo insieme *X* di stringhe finite di simboli in *L* tale per cui:
- tutte le variabili proposizionali di *L* sono in *X*;
- se *A* è in *X* allora anche *¬A* è in *X*;
- se *A* e *B* sono in *X* allora *(A ∧ B)*, *(A ∨ B)*, *(A → B)* e *(A ↔ B)* sono in *X*.

Denotiamo con **PROP*L*** (o **FML*L***) l’insieme delle proposizioni (o formule) nel linguaggio *L*; se *L* è chiaro dal contesto, possiamo scrivere solo PROP (o FML).
___
Un **assegnamento** è una funzione di tipo:
$$v: VAR → {1, 0}$$
I numeri 1 e 0 vengono detti "**valori di verità**", e sono intuitivamente da identificarsi come vero (`True`) e falso (`False`). Supponiamo di voler estendere un qualunque assegnamento *v:* *VAR* → {1, 0} a una funzione *v': PROP* → {1, 0}: si può fare ciò dando delle regole per calcolare ricorsivamente il valore di *v′* su una proposizione *A* come funzione dei valori di *v′* sulle sottoformule immediate di *A*. Si ottiene:

![[assegnamento_estensione.png]]

È possibile presentare i casi della definizione appena vista in maniera molto più chiara e compatta utilizzando delle **tavole di verità**; per esempio, è possibile riscrivere la definizione di *v((A ∨ B))* nel modo seguente:

![[truth_example.png]]

Con la definizione data sopra di *v: PROP* → {1, 0} abbiamo identificato una proposizione con una funzione booleana. Generalizzando, Una proposizione *A* contenente *n* variabili proposizionali si può identificare con una funzione booleana di *n* argomenti; le funzioni di questo tipo vengono definite "**funzioni di verità**".
___
La possibilità di organizzare in una **tavola di verità** i valori di verità di una proposizione composta come funzione dei valori di verità delle sue componenti può essere applicata a qualunque proposizione. Data una proposizione *A* che contiene le variabili proposizionali *p₁*, *p₂*, ..., *pn* distinte e le sottoformule *B₁*, *B₂*, ..., *Bk*, possiamo organizzare la tavola di verità di *A* come segue: 
- nelle prime *n* colonne si scrivono tutti i possibili valori assunti dalle variabili proposizionali;
- nelle restanti colonne si scrivono i valori assunti dalle sottoformule di *A* in ordine crescente di complessità (misurata in termini di rango).

Ad esempio, sia *A* = *(P ∨ Q) → (R ∨ (R → Q))*, il valore di *A* sarà dato dalla seguente tavola di verità:

![[truth_example1.png]]

In generale, è possibile costruire meccanicamente la tavola di verità di una qualunque proposizione *A*. Se la proposizione contiene *i* variabili proposizionali, la sua tavola di verità avrà *2ⁱ* righe, e ogni assegnamento di valori di verità alle variabili proposizionali di *A* corrisponde ad una riga della tavola di verità, e viceversa.
___
Un assegnamento *v* "**soddisfa**" una proposizione *A* se *v(A) = 1*; si dice anche che *v* è un "**modello**" di *A*. A sua volta, *A* si dice "**soddisfacibile**" se esiste almeno un assegnamento che la soddisfa; altrimenti, *A* si dice "**insoddisfacibile**". Indichiamo con *SAT* l’insieme delle proposizioni soddisfacibili e con *UNSAT* l’insieme delle proposizioni insoddisfacibili.

Sia *F* = {*A₁*, *A₂*, ..., *An*} un insieme di proposizioni, e sia *A* una proposizione: si può affermare che *A* è "**conseguenza logica**" di *F* se ogni assegnamento che soddisfa tutti gli elementi di *F* soddisfa anche *A*. In tal caso, scriviamo che "*A₁*, *A₂*, ..., *An* ⊨ *A*" e diciamo che le premesse *A₁*, *A₂*, ..., *An* implicano logicamente la conclusione *A*.

Se *F* è l’insieme vuoto, scriviamo semplicemente "⊨ *A*" per ∅ ⊨ *A*: in questo caso, la definizione afferma che *A* è soddisfatta da tutti gli assegnamenti possibili (e dunque che, per ogni assegnamento *v*, *v(A) = 1*). Infatti, per qualunque *v*, è vero a vuoto che *v* soddisfa tutti gli elementi dell’insieme ∅. Una proposizione *A* per cui avviene ciò, dunque che è soddisfatta da qualsiasi assegnamento, è "**valida**", e viene detta "**verità logica**" o "**tautologia**". Indichiamo con *TAUT* l'insieme delle tautologie.

Si osserva che l'appartenenza di *A* all'insieme delle proposizioni soddisfacibili è un concetto "esistenziale", visto che è verificata se e solo se *esiste* almeno un assegnamento che la soddisfa, e quindi:
$$A ∈ SAT ↔ ∃v(v(A) = 1)$$
Invece, l'appartenenza di *A* all'insieme delle tautologie è un concetto "universale", visto che è verificata se e solo se è soddisfatta da *tutti* i possibili assegnamenti, e quindi:
$$A ∈ TAUT ↔ ∀v(v(A) = 1)$$
Esiste, dunque, la seguente dualità tra *TAUT* e *UNSAT*:
$$A ∈ TAUT ⇔ ¬A ∈ UNSAT$$
D’altra parte, è ovvio che esistono proposizioni tali che sia *A* che *¬A* appartengano a *SAT*.

Vale, inoltre, un teorema che riduce il problema della conseguenza logica (validità di un argomento) a quello della verità logica e della soddisfacibilità. Esso, infatti, afferma che, siano *A₁*, *A₂*, ..., *An*, *A* varie proposizioni, i seguenti 3 punti sono equivalenti:
1. *A₁*, *A₂*, ..., *An* ⊨ *A*;
2. ((*A₁* ∧ *A₂* ∧ ... ∧ *An*) → *A*) ∈ *TAUT*;
3. (*A₁* ∧ *A₂* ∧ ... ∧ *An* ∧ *¬A*) ∈ *UNSAT*.

Data una proposizione *A* qualunque, possiamo verificare algoritmicamente l'appartenenza o meno di *A* a *TAUT*: basterà, infatti, costruire la tavola di verità di *A* e controllare se l’ultima colonna contiene solo il valore 1.
___
Vediamo alcuni esempi di formalizzazione e verifica della validità di un argomento logico.

Analizziamo, innanzitutto, un argomento verbale come il seguente:
1. Se studi e sei intelligente, allora superi l’esame;
2. Se sei intelligente, allora studi;
3. Non superi l’esame;
4. Sei scemo.

Per formalizzarlo, individuiamo le parti atomiche, che in questo caso sono "studi", "sei intelligente" e "superi l’esame", assumendo che "sei scemo" equivalga a "non sei intelligente"; associamo quindi *p₁* a "studi", *p₂* a "sei intelligente" e *p₃* a "superi l’esame". L’argomento viene formalizzato nel modo seguente:
1. (*p₁* ∧ *p₂*) → *p₃*;
2. *p₂* → *p₁*;
3. ¬*p₃*;
4. ¬*p₂*.

Ora, seguendo i 3 punti che definiscono la soddisfacibilità di un argomento logico, possiamo valutarne la validità in tre modi:
1. verificando che ogni assegnamento che soddisfa (*p₁* ∧ *p₂*) → *p₃*, (*p₂* → *p₁*) e ¬*p₃* soddisfi anche ¬*p₂*;
2. verificando che la singola proposizione ((*p₁* ∧ *p₂*) → *p₃* ∧ (*p₂* → *p₁*) ∧ ¬*p₃* → ¬*p₂*) sia una tautologia;
3. verificando che la singola proposizione ((*p₁* ∧ *p₂*) → *p₃* ∧ (*p₂* → *p₁*) ∧ ¬*p₃* → ¬¬*p₂*) sia una formula insoddisfacibile.

In tutti e tre i casi è possibile rispondere usando delle tavole di verità. In alternativa, possiamo ragionare sulla definizione di conseguenza logica: supponiamo per assurdo che esista un assegnamento *α* che soddisfa le premesse (*p₁* ∧ *p₂*) → *p₃*, (*p₂* → *p₁*) e ¬*p₃* e non soddisfa la conseguenza, ossia *α(¬p₂) = 0*. Dato che *α(¬p₃) = 1*, abbiamo *α(p₃) = 0*; inoltre, dato che *α((p₁ ∧ p₂) → p₃) = 1* e *α(p₃) = 0*, deve necessariamente valere *α(p₁ ∧ p₂) = 0* (altrimenti l’implicazione sarebbe di tipo 1 → 0, che vale 0). D’altro canto abbiamo *α(¬p₂) = 0* e dunque *α(p₂) = 1*; deve valere, quindi, *α(p₁) = 0* (altrimenti la congiunzione *p₁ ∧ p₂* sarebbe vera). Ma il fatto che *α(p₁) = 0* e *α(p₂) = 1* contraddice l’ipotesi che *α(p₂ → p₁) = 1*: per questo, non può esistere un *α* come ipotizzato, e quindi l’argomento è valido.

Il concetto di soddisfacibilità permette anche di usare insiemi di formule proposizionali per catturare determinate strutture matematiche. Ad esempio, sia *X* un insieme, e consideriamo il linguaggio proposizionale composto dalle variabili p*x,y* per ogni *(x, y)* ∈ *X* × *X*. Consideriamo, ora, il seguente insieme *T* di proposizioni in questo linguaggio:
1. per ogni *x* ∈ *X*, ¬p*x,x*;
2. per ogni *x, y* ∈ *X*, p*x,y* → ¬p*y,x*;
3. per ogni *x, y, z* ∈ *X*, (p*x,y* ∧ p*y,z*) → p*x,z*;
4. per ogni *x, y* ∈ *X* con *x* ≠ *y*, p*x,y* ∨ p*y,x*.

Si nota che l'insieme *T* cattura il concetto di [[Relazioni d'ordine|ordine totale]] stretto su *X* nel senso seguente.


___
