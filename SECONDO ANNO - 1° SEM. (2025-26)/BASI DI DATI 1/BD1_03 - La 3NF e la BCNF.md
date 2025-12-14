## La 3NF

Per arrivare alla definizione della **terza forma normale**, o "**3NF**" in breve, riprendiamo l'esempio di database presentato alla fine del capitolo sul [[BD1_01 - Modello relazionale#Come formulare un "buon" schema di database?|modello relazionale]], e in particolare consideriamo la versione finale, ossia lo schema di database contenente i seguenti 4 schemi di relazione:
$$\begin{align} &\text{Student(Matr, Name, Surname, TC, Birth, City)} \\ &\text{Course(C\#, Title, Prof)} \\ &\text{Exam(Matr, C\#, Date, Grade)} \\ &\text{Municipality(City, Prov)} \end{align}$$
Come è facilmente intuibile, ogni matricola $\text{Matr}$ identifica univocamente un singolo studente: ciò significa che a ciascuna matricola potrà essere associato un solo nome, un solo cognome, un solo tax code, ecc. ecc. Possiamo, così, dedurre che per avere un'istanza legale di $\text{Student}$ essa dovrà rispettare la seguente [[BD1_02 - Dipendenze funzionali#Cos'è una dipendenza funzionale?|dipendenza funzionale]]:
$$\text{Matr}\rightarrow \text{Matr, Name, Surname, TC, Birth, City}$$
Seguendo lo stesso ragionamento, sappiamo che anche l'attributo $\text{TC}$ è unico per ogni studente, e dunque in un'istanza legale deve valere anche la seguente dipendenza funzionale:
$$\text{TC}\rightarrow \text{Matr, Name, Surname, TC, Birth, City}$$
Possiamo affermare di conseguenza che **$\text{Matr}$ e $TC$ sono chiavi dello schema di relazione $\text{Student}$**. Lo stesso non vale per gli altri attributi: possiamo avere due studenti con stesso cognome e diverso nome, due studenti nati nello stesso giorno, provenienti dalla stessa città, e così via. Formalmente, ciò implica che dipendenze funzionali come:
$$\begin{align} &\text{Surname}\rightarrow \text{Name} \\ &\text{Name}\rightarrow \text{Surname} \\ &\text{Surname}\rightarrow \text{Birth} \end{align}$$
non devono essere necessariamente soddisfatte da un'istanza legale di $\text{Student}$. Da queste considerazioni si conclude che **l'unica dipendenza funzionale non [[BD1_02 - Dipendenze funzionali#Dipendenze funzionali triviali|triviale]] che deve essere soddisfatta da un'istanza legale di $\text{Student}$ è una dipendenza funzionale del tipo:**
$$K\rightarrow X$$
dove $K$ contiene una **chiave** della relazione (nel nostro esempio, $\text{Matr}$ o $\text{TC}$). Un discorso simile può essere applicato anche agli altri schemi di relazione del database, ottenendo che $\text{C\#}$ è la chiave di $\text{Course}$, $\text{Matr, C\#}$ è la chiave di $\text{Exam}$ e $\text{City}$ è la chiave di $\text{Municipality}$, e anche per tutti questi schemi vale la stessa regola che abbiamo appena esplicitato. Dunque, generalizzando, le uniche dipendenze funzionali non triviali che devono necessariamente essere soddisfatte da una qualsiasi istanza di relazione legale sono quelle del tipo:
$$K\rightarrow X$$
dove $K$ contiene una chiave.

Possiamo partire da questa caratteristica per definire la 3NF. Dunque, una sua definizione non formale potrebbe essere la seguente:

> Uno schema di relazione è in 3NF se **le uniche dipendenze funzionali non triviali che devono necessariamente essere soddisfatte da una qualsiasi istanza di relazione legale sono quelle del tipo:**
> $$K\rightarrow X$$
> dove **$K$ contiene una chiave** o dove **$X$ è contenuto in una chiave**.

Possiamo riformulare questa definizione nel modo seguente:

> Dato uno schema di relazione $R$ e un insieme $F$ di dipendenze funzionali definite su di esso, possiamo affermare che $R$ sia in **3NF** se vale che, per ogni dipendenza funzionale $X\rightarrow A\,\in\,F^{+}$, con $A$ singoletto e tale per cui $A\not\in X$, si ha che $A$ è contenuto in una chiave (in altre parole, $A$ è "**primo**") oppure che $X$ contiene una chiave (in altre parole, $X$ è una "**super-chiave**").

La condizione $A\not\in X$ è molto importante per la definizione, dato che per l'[[BD1_02 - Dipendenze funzionali#Assiomi di Armstrong e regole corollarie|assioma di riflessività]] se valesse che $A\in X$ si avrebbe sempre che $X\rightarrow A\,\in\,F^{A}$, e dunque $X\rightarrow A\,\in\,F^{+}$, anche nei casi in cui $A$ non è primo o in cui $X$ non è una super-chiave: dunque, se non si ponesse quella condizione, realisticamente non sarebbe possibile avere uno schema di relazione in 3NF.

È possibile dimostrare che, per verificare se uno schema di relazione è in 3NF, basterà controllare tutte le dipendenze funzionali non triviali $X\rightarrow A\,\in\,F^{+}$, ottenute scomponendo i dipendenti delle dipendenze definite in $F$. 
___
## Esempi: verificare se una relazione è in 3NF

##### Esempio n°1

Supponiamo di avere il seguente schema $R$ e insieme $F$ di dipendenze funzionali:
$$\begin{align} &R=ABCD \\ &F=\{A\rightarrow B,\,B\rightarrow CD\} \end{align}$$
Nello schema $R$ considerato, la chiave è $A$ (vedremo meglio come trovare le chiavi di uno schema di relazione nei capitoli successivi). A questo punto, andiamo a verificare se $R$ è posto in 3NF: analizziamo le dipendenze funzionali che troviamo in $F$, ossia $A\rightarrow B$ e $B\rightarrow CD$; la prima rispetta la condizione, dato che $A$, essendo una chiave, può essere considerata una super-chiave (contiene una chiave, ossia sé stessa); per quanto riguarda la seconda, per analizzarla la si dovrà scomporre nelle dipendenze funzionali $B\rightarrow C$ e $B\rightarrow D$, che si trovano in $F^{+}$, e per entrambe queste relazioni non si ha né che $B$ è una super-chiave né che $C$ o $D$ sono primi, dunque la condizione non viene rispettata. 

Di conseguenza, si ha che $R$ non è in 3NF.
___
##### Esempio n°2

Supponiamo di avere il seguente schema $R$ e insieme $F$ di dipendenze funzionali:
$$\begin{align} &R=ABCD\\ &F=\{AC\rightarrow B,\,B\rightarrow AD\} \end{align}$$
Nello schema $R$ considerato, le chiavi sono $AC$ e $BC$. A questo punto, andiamo a verificare se $R$ è posto in 3NF: analizziamo le dipendenze funzionali che troviamo in $F$, ossia $AC\rightarrow B$ e $B\rightarrow AD$; la prima rispetta la condizione dato che $AC$, essendo una chiave, può essere considerata una super-chiave; per quanto riguarda la seconda, per analizzarla la si dovrà scomporre nelle dipendenze funzionali $B\rightarrow A$ e $B\rightarrow D$, che si trovano in $F^{+}$, e mentre la prima di queste non crea problemi ($A$ è primo, ossia contenuto in una chiave) lo stesso non si può dire della seconda, dato che non si ha né che $B$ è una super-chiave né che $D$ è primo, dunque la condizione non viene rispettata. 

Di conseguenza, si ha che $R$ non è in 3NF.
___
##### Esempio n°3

Supponiamo di avere il seguente schema $R$ e insieme $F$ di dipendenze funzionali:
$$\begin{align} &R=ABCD\\ &F=\{AB\rightarrow CD,\,BC\rightarrow A,\,D\rightarrow AC\} \end{align}$$
Nello schema $R$ considerato, le chiavi sono $AB$, $BC$ e $DB$. A questo punto, andiamo a verificare se $R$ è posto in 3NF: analizziamo le dipendenze funzionali che troviamo in $F$, ossia $AB\rightarrow CD$, $BC\rightarrow A$ e $D\rightarrow AC$; la prima rispetta la condizione dato che $AB$, essendo una chiave, può essere considerata una super-chiave; anche la seconda rispetta la condizione dato che vale sia che $BC$, essendo una chiave, può essere considerata una super-chiave, sia che $A$ è primo (in quanto contenuto nella chiave $AB$); per analizzare la terza la si dovrà scomporre nelle dipendenze funzionali $D\rightarrow A$ e $D\rightarrow C$, che si trovano in $F^{+}$, e notiamo che entrambe queste dipendenze funzionali rispettano la condizione, in quanto sia $A$ che $C$ sono primi.

Non essendoci dipendenze funzionali che non rispettano la condizione fondamentale della 3NF, si ha che $R$ è in 3NF.
___
## Dipendenze parziali e transitive

È possibile fornire una **definizione alternativa della 3NF**, per certi versi più semplice e diretta:

> Dato uno schema di relazione $R$ e un insieme $F$ di dipendenze funzionali definite su di esso, possiamo affermare che $R$ sia in **3NF** se e solo se non ci sono attributi di $R$ che dipendono parzialmente o transitivamente da una chiave.

In parole povere, tale definizione impone che uno schema $R$ può essere in 3NF se e solo se non esistono dipendenze parziali o transitive definite su tale schema. Ma cosa si intende per "**dipendenze parziali**" e "**dipendenze transitive**"?

Dato uno schema di relazione $R$ e un insieme $F$ di dipendenze funzionali, si dice che "**$A$ dipende parzialmente da una chiave $K$**" se esiste un sottoinsieme $X$ di attributi di $R$ (diverso da $R$ stesso) tale per cui valga che:
- $X\rightarrow A\,\in\,F^{+}$;
- $A\,\not\in\,X$;
- $X\subset K$;
- $A$ non fa parte di una chiave (dunque, A non è primo).

Dato uno schema di relazione $R$ e un insieme $F$ di dipendenze funzionali, si dice che "**$A$ dipende transitivamente da una chiave $K$**" se esiste un sottoinsieme $X$ di attributi di $R$ (diverso da $R$ stesso) tale per cui valga che:
- $K\rightarrow X\,\in\,F^{+}$;
- $X\rightarrow A\,\in\,F^{+}$;
- $A\,\not\in\,X$;
- $X$ non è una chiave;
- $A$ non fa parte di una chiave (dunque, A non è primo).

##### Verificare una 3NF considerando dipendenze parziali e transitive

Avendo fornito una definizione alternativa della 3NF sulla base dei concetti di dipendenze parziali e transitive, vediamo come esse influenzano una **verifica di 3NF su uno schema di relazione**.

Supponiamo di avere il seguente schema $R$ e insieme $F$ di dipendenze funzionali:
$$\begin{align} &R=ABC\\ &F=\{A\rightarrow B,\,B\rightarrow C\} \end{align}$$
Notiamo subito che $C$ dipende transitivamente dalla chiave $A$: infatti, si ha che sia $A\rightarrow B$ che $B\rightarrow C$ appartengono ad $F^{+}$, che $C\not\in B$, che $B$ non è una chiave (l'unica chiave dello schema è $A$) e che $C$ non fa parte di alcuna chiave. La presenza di questa dipendenza transitiva porta lo schema di relazione che stiamo considerando a non essere in 3NF. 

In generale, in una situazione del genere, **per portare lo schema di partenza in 3NF conviene scomporlo in più schemi che siano, a loro volta, in 3NF**; inoltre, è importante anche **preservare tutte le dipendenze originariamente trovate in $F^{+}$**. Nel nostro esempio, una soluzione possibile tenendo a mente queste regole è di scomporre lo schema di partenza nei seguenti due schemi:
$$R_{1}=AB\,\,\,\text{con}\,\,\,F_{1}=\{A\rightarrow B\}\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,R_{2}=BC\,\,\,\text{con}\,\,\,F_{2}=\{B\rightarrow C\}$$
Si ottiene, in questo modo, un insieme di schemi di relazione in 3NF, e dunque perfettamente validi.

Consideriamo un altro esempio. Supponiamo di avere il seguente schema $R$ e insieme $F$ di dipendenze funzionali:
$$\begin{align} &R=ABC\\ &F=\{A\rightarrow B,\,C\rightarrow B\} \end{align}$$
In questo caso, notiamo che $B$ dipende parzialmente dalla chiave $AC$: infatti, si ha che $A\rightarrow B$ e $C\rightarrow B$ appartengono a $F^{+}$, sia che $B\not\in A$ che $B\not\in C$, sia che $A\subset AC$ che $C\subset AC$, e infine che $B$ non fa parte di alcuna chiave. La presenza di questa dipendenza parziale porta lo schema di relazione che stiamo considerando a non essere in [[BD1_03 - La 3NF e la BCNF#La 3NF|3NF]]. Seguendo lo stesso approccio utilizzato nell'esempio del [[BD1_03 - La 3NF e la BCNF#Verificare una 3NF considerando dipendenze parziali e transitive|paragrafo precedente]], possiamo scomporre lo schema di partenza nei seguenti due schemi:
$$R_{1}=AB\,\,\,\text{con}\,\,\,F_{1}=\{A\rightarrow B\}\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,R_{2}=BC\,\,\,\text{con}\,\,\,F_{2}=\{C\rightarrow B\}$$
Notiamo, però, che seppur gli schemi risultanti preservino tutte le dipendenze funzionali originariamente trovate in $F^{+}$, e si trovino in 3NF, questa non è comunque una soluzione soddisfacente: infatti, si è dato per scontato finora che **le istanze di relazione generate dagli schemi scomposti devono essere equivalenti a un'istanza corrispondente dello schema di partenza**, e dunque non si dovrà avere né la creazione di nuovi dati né la perdita degli stessi. Concretamente, ciò vuol dire che se consideriamo un'istanza legale di $R$ e la scomponiamo in una coppia di istanze di $R_{1}$ ed $R_{2}$, un eventuale [[BD1_01 - Modello relazionale#Join naturale|join naturale]] su queste ultime due istanze dovrebbe restituire esattamente l'istanza di partenza. Nel nostro esempio, invece, non abbiamo questa sicurezza: supponiamo, ad esempio, di avere la seguente istanza legale di $R$:

| A   | B   | C   |
| --- | --- | --- |
| a1  | b1  | c1  |
| a2  | b1  | c2  |

È possibile scomporla in una coppia di istanze di $R_{1}$ ed $R_{2}$ nel modo seguente:

| A   | B   |
| --- | --- |
| a1  | b1  |
| a2  | b1  |

| B   | C   |
| --- | --- |
| b1  | c1  |
| b1  | c2  |

A questo punto, però, operando un join naturale su queste ultime due tabelle, otterremmo la seguente tabella risultante:

| A   | B   | C   |
| --- | --- | --- |
| a1  | b1  | c1  |
| a2  | b1  | c2  |
| a1  | b1  | c2  |
| a2  | b1  | c1  |

Notiamo che le ultime due tuple di tale tabella non esistevano nell'istanza di $R$ originale, e sono state create in seguito alla scomposizione in $R_{1}$ ed $R_{2}$. Dunque, la soluzione che avevamo previsto in realtà non è valida.

Quest'ultimo esempio, in particolare, ci mostra che dobbiamo **aggiungere una condizione da rispettare** quando si vuole scomporre uno schema per ottenerne altri in 3NF. In generale, dunque, oltre alla definizione di 3NF stessa si deve fare attenzione a:
- **preservare le dipendenze funzionali** poste per una qualsiasi istanza legale dello schema di partenza;
- fare in modo che **sia possibile ricostruire una qualsiasi istanza legale dello schema di partenza con un join naturale sulle istanze scomposte** (senza perdere o aggiungere informazioni).
___
## La BCNF

La [[BD1_03 - La 3NF e la BCNF#La 3NF|3NF]] non è la forma normale più stringente: vediamo, ad esempio, una nuova forma normale chiamata "**Boyce-Codd Normal Form**", o "**BCNF**".

> Dato uno schema di relazione $R$ e un insieme $F$ di dipendenze funzionali definite su di esso, possiamo affermare che $R$ sia in **BCNF** se **ogni determinante che si ha nello schema è una super-chiave**.

In generale, una relazione che è posta in BCNF è automaticamente posta anche in 3NF, ma non è vero il contrario.

Vediamo un esempio: supponiamo di voler creare uno schema di relazione che rappresenti l'allocazione delle sale operatorie all'interno di un ospedale. Tali sale operatorie sono prenotate giorno per giorno, a orari programmati, per eseguire delle operazioni su determinati pazienti dai chirurghi dell'ospedale; durante una singola giornata, una sala operatoria sarà sempre occupata dallo stesso chirurgo, che eseguirà una o più operazioni a diversi orari; inoltre, vogliamo fare in modo che, conoscendo il paziente e la data, si possa risalire all'orario dell'operazione, al chirurgo e alla sala operatoria.

Seguendo queste indicazioni, possiamo creare il seguente schema di relazione:
$$\text{Interventions}=\text{Patient, Date, Time, Surgeon, Room}$$
e definire anche un insieme $F$ di dipendenze funzionali:
$$\begin{align} F = \{&\text{Patient, Date}\rightarrow \text{Time, Surgeon, Room}\\ &\text{Surgeon, Date, Time}\rightarrow \text{Patient, Room}\\ &\text{Room, Date, Time}\rightarrow \text{Patient, Surgeon}\\ &\text{Surgeon, Date}\rightarrow \text{Room} \} \end{align}$$
In questa situazione, abbiamo tre chiavi:
$$\{\text{Patient, Date}\}\,\,\,\,\,\,\,\,\,\,\{\text{Surgeon, Date, Time}\}\,\,\,\,\,\,\,\,\,\,\{\text{Room, Date, Time}\}$$
Notiamo che le prime 3 dipendenze funzionali dell'insieme $F$ rispettano la condizione della BCNF, dato che i 3 determinanti costituiscono ciascuno una delle chiavi dello schema; lo stesso non si può dire per la quarta dipendenza, dato che $\{\text{Surgeon, Date}\}$ non è una super-chiave, ma piuttosto è contenuto in una chiave. Si ha, dunque, che $\text{Interventions}$ non è in BCNF. 

Ciononostante, si ha che invece $\text{Interventions}$ rispetta tutte le condizioni per essere in 3NF, anche se potrebbe comunque essere ottimizzata per evitare delle ridondanze. Infatti, supponendo che ad esempio un chirurgo si sposti da una sala operatoria a un'altra, con lo schema attuale si dovrebbero modificare tutte le tuple in cui compare quel chirurgo. Per rendere il tutto più efficiente, possiamo scomporre lo schema nei due seguenti:
$$\begin{align} &\text{Interventions}=\text{Patient, Date, Time, Surgeon} \\ &\text{Occupation}=\text{Surgeon, Date, Room} \end{align}$$
Ora, vediamo un altro esempio. Supponiamo di voler tenere traccia dei pazienti che devono sottostare a più operazioni, anche in diversi dipartimenti; creiamo, a questo proposito, lo schema di relazione:
$$\text{MultipleSurgery}=\text{Patient, Department, Surgeon}$$
Ogni tupla di tale relazione rappresenta un'operazione che il paziente ha affrontato, associando tale paziente con il chirurgo che l'ha operato e con il dipartimento dove si è svolta l'operazione. Vale il seguente insieme di dipendenze funzionali:
$$\begin{align} F=\{&\text{Surgeon}\rightarrow \text{Department}  \\ &\text{Patient, Department}\rightarrow \text{Surgeon} \} \end{align}$$
con $\{\text{Patient, Department}\}$ che è l'unica chiave dello schema. In queste condizioni, si ha che la prima dipendenza viola la condizione della BCNF, dato che $\text{Surgeon}$ non è una super-chiave. Dunque, proviamo lo stesso approccio di prima e scomponiamo lo schema di partenza in due schemi $\text{Surgeons}$ e $\text{Patients}$:
$$\begin{align} &\text{Surgeons}=\text{Surgeon, Department}\\ &\text{Patients}=\text{Patient, Surgeon} \end{align}$$
Tuttavia, questa non rappresenta un'opzione valida, dato che non viene conservata la seconda dipendenza funzionale dell'insieme $F$ di partenza.

Dall'esempio appena analizzato, deduciamo che **non è sempre possibile scomporre uno schema di relazione in più schemi in BCNF preservando tutte le dipendenze originali**. Tuttavia, tale operazione è sempre possibile con la 3NF, e dunque in seguito si preferirà quest'ultima alla prima, anche se in certi casi può portare a ridondanze.
___
## Come scomporre correttamente uno schema in più schemi in 3NF

In questo paragrafo, approfondiremo nello specifico il modo corretto di **scomporre uno schema in più schemi posti in [[BD1_03 - La 3NF e la BCNF#La 3NF|3NF]]**. Dato uno schema di relazione $R$ e un insieme $F$ di dipendenze funzionali definite su di esso, se lo si vuole scomporre in più schemi in 3NF si dovrà prestare attenzione a:
- **preservare tutte le dipendenze contenute nella [[BD1_02 - Dipendenze funzionali#Chiusura di $F$|chiusura di F]]**, ossia nell'insieme $F^{+}$;
- mantenere la possibilità di **ricostruire tramite un [[BD1_01 - Modello relazionale#Join naturale|join]] tutte e sole le informazioni originali**.

###### Preservare le dipendenze di $F^{+}$

Focalizziamoci, per ora, sul primo punto. Dovendo preservare tutte le dipendenze contenute in $F^{+}$, siamo naturalmente interessati a calcolare tale insieme, tuttavia come anticipato in precedenza tale operazione risulta molto dispendiosa e inefficiente. 

In alternativa, quello che possiamo fare è **trovare un metodo per capire se una dipendenza funzionale $X\rightarrow Y$ appartiene a $F^{+}$**. Per fare ciò, possiamo usufruire del concetto di [[BD1_02 - Dipendenze funzionali#Chiusura di un insieme di attributi $X$|chiusura di un insieme di attributi]], ossia dell'insieme $X^{+}$. Infatti, in generale vale che:
$$X\rightarrow Y\,\in\,F^{A}\,\,\,\iff\,\,\,Y\subseteq X^{+}$$
e avendo [[BD1_02 - Dipendenze funzionali#Teorema $F {+}=F {A}$|dimostrato]] che $F^{A}=F^{+}$, possiamo utilizzare questo lemma per il nostro scopo.

Ma come facciamo a **calcolare l'insieme $X^{+}$**? Per farlo, possiamo sfruttare un **algoritmo**, che ha i seguenti input e output:
- come **input**, uno schema di relazione $R$, un insieme $F$ di dipendenze funzionali definite su di esso, e un sottoinsieme $X$ di attributi di $R$;
- come **output**, la chiusura di $X$ rispetto a $F$, ossia l'insieme $X^{+}_{F}$, nella variabile $Z$.

Di seguito, lo **pseudocodice dell'algoritmo**:

```
Z = X
S = {A | Y → V ∈ F, A ∈ V ∧ Y ⊆ Z}
	
while S ⊄ Z:
	Z = Z ∪ S
	S = {A | Y → V ∈ F, A ∈ V ∧ Y ⊆ Z}		
```

Analizziamo l'operato dell'algoritmo passo per passo. Come abbiamo detto, la variabile $Z$ sarà quella dove troveremo la chiusura del sottoinsieme $X$; inizialmente, ci andiamo a mettere solo $X$ stesso. 

Di seguito, inseriamo nell'insieme $S$ tutti i singoli attributi $A$ che compongono la parte destra (ossia, il fattore "dipendente") delle dipendenze contenute in $F$ le cui parti sinistre (ossia, i fattori "determinanti") siano contenute in $Z$.

Essendo inizialmente $Z = X$, nel passaggio precedente si inseriscono in $S$ solo attributi determinati funzionalmente da $X$; una volta entrati nel ciclo, invece, si aggiungeranno tali attributi a $Z$ e si procederà a trovare altri attributi sfruttando la transitività. Generalmente, all'iterazione $i$ del ciclo, si aggiungeranno a $S$ i singoli attributi $A$ che comporranno la parte destra delle dipendenze contenute in $F$ le cui parti sinistre siano contenute in $Z^{i-1}$.

L'algoritmo terminerà la sua esecuzione una volta che il nuovo insieme $S^{i}$ ottenuto sarà già contenuto nell'insieme $Z^{i}$, e dunque quando non si potranno più aggiungere nuovi attributi all'insieme $X^{+}$.

Vediamo un esempio. Supponiamo di avere il seguente schema di relazione $R$ e insieme $F$ di dipendenze funzionali definite su di esso:
$$\begin{align} &R=ABCDEHL \\ &F=\{AB\rightarrow C,\,B\rightarrow D,\,AD\rightarrow E,\,CE\rightarrow H\} \end{align}$$
e di voler calcolare la chiusura di $AB$, ossia l'insieme $AB^{+}$, utilizzando l'algoritmo appena presentato. Partiamo con $Z=AB$, e aggiungiamo all'insieme $S$ gli attributi che compongono la parte destra delle dipendenze contenute in $F$ le cui parti sinistre si trovano in $Z$: la prima dipendenza di $F$ è $AB\rightarrow C$, quindi aggiungiamo subito $C$; la seconda dipendenza, invece, è $B\rightarrow D$, ed essendo $B$ contenuto in $Z$ possiamo aggiungere anche $D$. Dunque, 

[11 - slide 7]
___