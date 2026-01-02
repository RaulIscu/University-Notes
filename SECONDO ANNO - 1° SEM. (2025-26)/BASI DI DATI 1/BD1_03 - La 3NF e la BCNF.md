## La 3NF

Per arrivare alla definizione della **terza forma normale**, o "**3NF**" in breve, riprendiamo l'esempio di database presentato alla fine del capitolo sul [[BD1_01 - Modello relazionale#Come formulare un "buon" schema di database?|modello relazionale]], e in particolare consideriamo la versione finale, ossia lo schema di database contenente i seguenti 4 schemi di relazione:
$$\begin{align} &\text{Student(Matr, Name, Surname, TC, Birth, City)} \\ &\text{Course(C\#, Title, Prof)} \\ &\text{Exam(Matr, C\#, Date, Grade)} \\ &\text{Municipality(City, Prov)} \end{align}$$
Come è facilmente intuibile, ogni matricola $\text{Matr}$ identifica univocamente un singolo studente: ciò significa che a ciascuna matricola potrà essere associato un solo nome, un solo cognome, un solo tax code, ecc. ecc. Possiamo, così, dedurre che per avere un'istanza legale di $\text{Student}$ essa dovrà rispettare la seguente [[BD1_02 - Dipendenze funzionali#Cos'è una dipendenza funzionale?|dipendenza funzionale]]:
$$\text{Matr}\rightarrow \text{Matr, Name, Surname, TC, Birth, City}$$
Seguendo lo stesso ragionamento, sappiamo che anche l'attributo $\text{TC}$ è unico per ogni studente, e dunque in un'istanza legale deve valere anche la seguente dipendenza funzionale:
$$\text{TC}\rightarrow \text{Matr, Name, Surname, TC, Birth, City}$$
Possiamo affermare di conseguenza che **$\text{Matr}$ e $\text{TC}$ sono chiavi dello schema di relazione $\text{Student}$**. Lo stesso non vale per gli altri attributi: possiamo avere due studenti con stesso cognome e diverso nome, due studenti nati nello stesso giorno, provenienti dalla stessa città, e così via. Formalmente, ciò implica che dipendenze funzionali come:
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

##### Trovare la chiusura di un sottoinsieme $X$ di attributi di $R$

Focalizziamoci, per ora, sul primo punto. Dovendo preservare tutte le dipendenze contenute in $F^{+}$, siamo naturalmente interessati a calcolare tale insieme, tuttavia come anticipato in precedenza tale operazione risulta molto dispendiosa e inefficiente. 

In alternativa, quello che possiamo fare è **trovare un metodo per capire se una dipendenza funzionale $X\rightarrow Y$ appartiene a $F^{+}$**. Per fare ciò, possiamo usufruire del concetto di [[BD1_02 - Dipendenze funzionali#Chiusura di un insieme di attributi $X$|chiusura di un insieme di attributi]], ossia dell'insieme $X^{+}$. Infatti, per il lemma della chiusura vale che:
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

Analizziamo l'operato dell'algoritmo passo per passo. Come abbiamo detto, **la variabile $Z$ sarà quella dove troveremo la chiusura del sottoinsieme $X$**; inizialmente, ci andiamo a mettere **solo $X$ stesso**. 

Di seguito, **inseriamo nell'insieme $S$ tutti i singoli attributi $A$ che compongono la parte destra** (ossia, il fattore "dipendente") **delle dipendenze contenute in $F$ le cui parti sinistre** (ossia, i fattori "determinanti") **siano contenute in $Z$**.

Essendo inizialmente $Z = X$, nel passaggio precedente si inseriscono in $S$ solo attributi determinati funzionalmente da $X$; una volta entrati nel ciclo, invece, si aggiungeranno tali attributi a $Z$ e si procederà a **trovare altri attributi sfruttando la transitività**. Generalmente, all'iterazione $i$ del ciclo, si aggiungeranno a $S$ i singoli attributi $A$ che comporranno la parte destra delle dipendenze contenute in $F$ le cui parti sinistre siano contenute in $Z^{i-1}$.

**L'algoritmo terminerà la sua esecuzione** una volta che il nuovo insieme $S^{i}$ ottenuto sarà già contenuto nell'insieme $Z^{i}$, e dunque **quando non si potranno più aggiungere nuovi attributi all'insieme $X^{+}$**.

Vediamo un esempio. Supponiamo di avere il seguente schema di relazione $R$ e insieme $F$ di dipendenze funzionali definite su di esso:
$$\begin{align} &R=ABCDEHL \\ &F=\{AB\rightarrow C,\,B\rightarrow D,\,AD\rightarrow E,\,CE\rightarrow H\} \end{align}$$
e di voler calcolare la chiusura di $AB$, ossia l'insieme $AB^{+}$, utilizzando l'algoritmo appena presentato. Partiamo con $Z=AB$, e aggiungiamo all'insieme $S$ gli attributi che compongono la parte destra delle dipendenze contenute in $F$ le cui parti sinistre si trovano in $Z$: la prima dipendenza di $F$ è $AB\rightarrow C$, quindi aggiungiamo subito $C$; la seconda dipendenza, invece, è $B\rightarrow D$, ed essendo $B$ contenuto in $Z$ possiamo aggiungere anche $D$. Dunque, all'entrata del ciclo, si ha la seguente situazione:
$$\begin{align} &Z=AB\\ &S=CD \end{align}$$
A questo punto, si valuta la condizione del ciclo, ossia se $S$ non è un sottoinsieme di $Z$ (in altre parole, la condizione è rispettata se l'insieme $S$ ha elementi che non sono contenuti in $Z$): la condizione è vera, quindi si entra nel ciclo. Procediamo a fare l'unione tra $Z$ e $S$ e memorizzarla in $Z$, e a questo punto ricontrolliamo se possiamo aggiungere altri attributi in $S$: notiamo la terza dipendenza funzionale di $F$, ossia $AD\rightarrow E$, e aggiungiamo $E$ ad $S$ avendo sia $A$ che $D$ all'interno di $Z$. Dunque, al termine della prima iterazione del ciclo, si ha la seguente situazione:
$$\begin{align} &Z=ABCD\\ &S=CDE \end{align}$$
Rivalutiamo la condizione del ciclo: anche in questo caso, la condizione viene rispettata (l'attributo $E$ non è contenuto in $Z$), dunque procediamo con la seconda iterazione del ciclo. Facciamo l'unione tra $Z$ e $S$ e memorizziamola in $Z$, e ricontrolliamo se possiamo aggiungere altro a $S$: in questo caso, utilizziamo l'ultima dipendenza contenuta in $F$, ossia $CE\rightarrow H$, e aggiungiamo $H$ ad $S$ avendo sia $C$ che $E$ all'interno di $Z$. Dunque al termine della seconda iterazione del ciclo, si ha la seguente situazione:
$$\begin{align} &Z=ABCDE\\ &S=CDEH \end{align}$$
Valutiamo ancora una volta la condizione del ciclo: di nuovo, la condizione viene rispettata (l'attributo $H$ non è contenuto in $Z$), dunque procediamo con la terza iterazione del ciclo. Facciamo l'unione tra $Z$ e $S$ e vediamo se è possibile aggiungere altro a $S$: stavolta, non troviamo dipendenze di $F$ che fanno al nostro caso, dunque $S$ rimarrà così com'è. Non avendo aggiunto altri attributi a $S$, quando andremo a rivalutare nuovamente la condizione del ciclo, essa non verrà rispettata, dato che tutti gli elementi di $S$ saranno contenuti anche in $Z$: a questo punto, l'algoritmo termina la sua esecuzione. Rimaniamo con i seguenti insiemi di attributi:
$$\begin{align} &Z=ABCDEH\\ &S=CDEH \end{align}$$
e, dunque, si ha che la chiusura di $AB$ corrisponde all'insieme $AB^{+}=ABCDEH$.

Notiamo una particolarità: anche se non è ciò che viene concretamente fatto dall'algoritmo, **estendere la variabile $S$ implica l'applicazione degli [[BD1_02 - Dipendenze funzionali#Assiomi di Armstrong e regole corollarie|assiomi di Armstrong]] sulle dipendenze di $F$**. Ad esempio, per aggiungere l'attributo $D$, e quindi per dimostrare che $D$ è determinato funzionalmente da $AB$, avremmo potuto lavorare nel modo seguente:
1. per l'assioma della riflessività, si ha che $AB\rightarrow B$;
2. all'interno di $F$ troviamo la dipendenza $B\rightarrow D$;
3. di conseguenza, per l'assioma della transitività, possiamo affermare che $AB\rightarrow D$.

Ragionamenti analoghi possono essere fatti per tutti gli altri attributi inseriti man mano in $Z$.
___
##### Dimostrazione dell'algoritmo di calcolo di $X^{+}$

È possibile **dimostrare che l'algoritmo** presentato nel [[BD1_03 - La 3NF e la BCNF#Trovare la chiusura di un sottoinsieme $X$ di attributi di $R$|paragrafo precedente]] **computa correttamente l'insieme $X^{+}$**, ossia la chiusura di un sottoinsieme $X$ di attributi di $R$ rispetto a un insieme $F$ di dipendenze funzionali definite su quest'ultimo.

Indichiamo con $Z^{(0)}$ il valore iniziale di $Z$ (ossia $X$) e con $Z^{(i)}$ e $S^{(i)}$ i valori di $Z$ e di $S$ dopo la $i$-esima iterazione del ciclo presente all'interno dell'algoritmo; è banale notare che vale che $Z^{(i)}\subseteq Z^{(i+1)}$ per ogni $i$, dunque possiamo affermare che $Z^{(i)}$ è una successione monotona crescente limitata da $R$. A questo punto, consideriamo un'iterazione $j$ tale per cui si ha che $S^{(j)}\subseteq Z^{(j)}$ (dunque, l'iterazione $j$ dopo la quale l'algoritmo termina la sua esecuzione); si vuole dimostrare che:
$$A\,\in\,Z^{(j)}\,\,\,\iff\,\,\,A\,\in\,X^{+}$$
Dividiamo questa dimostrazione in **due parti**: innanzitutto, dimostriamo per **induzione** su $i$ che, per ogni $i$, vale che $Z^{(i)}\subseteq X^{+}$, e dunque in particolare che $Z^{(j)}\subseteq X^{+}$. Partiamo con la **base dell'induzione**, ossia con $i=0$: come abbiamo anticipato, $Z^{(0)}=X$, e valendo banalmente che $X\subseteq X^{+}$ abbiamo anche che $Z^{(0)}\subseteq X^{+}$. Arriviamo dunque al **passo dell'induzione**, ossia a considerare valori $i>0$: come ipotesi induttiva, si pone che $Z^{(i-1)}\subseteq X^{+}$, e dunque si vuole dimostrare che lo stesso valga per un qualsiasi $i$. Indichiamo con $A$ un attributo contenuto nell'insieme $Z^{(i)}-Z^{(i-1)}$, e sappiamo che deve necessariamente esistere una dipendenza $Y\rightarrow V\,\in\,F$ tale che $Y\subseteq Z^{(i-1)}$ e che $A\,\in\,V$ (sono i requisiti per l'inserimento di un attributo in $S$): avendo che $Y\subseteq Z^{(i-1)}$, per ipotesi induttiva deduciamo che $Y\subseteq X^{+}$, e per il [[BD1_02 - Dipendenze funzionali#Chiusura di un insieme di attributi $X$|lemma della chiusura]] ciò significa che $X\rightarrow Y\,\in\,F^{A}$. Avendo stabilito ciò, e sapendo che $Y\rightarrow V\,\in\,F$, per transitività si può concludere che $X\rightarrow V\,\in\,F^{A}$, e sempre per il lemma della chiusura ciò comporta che $V\subseteq X^{+}$. Essendo $A$ un qualsiasi attributo contenuto in $V$, si deduce che per ogni $A$ si ha che $A\,\in\,X^{+}$, ed essendo $A$ anche un attributo generico dell'insieme $Z^{(i)}-Z^{(i-1)}$, ciò dimostra che tale insieme appartiene a $X^{+}$. Dato che sia $Z^{(i-1)}$ che $Z^{(i)}-Z^{(i-1)}$ appartengono a $Z^{+}$, in generale si è dimostrato che $Z^{i}\subseteq X^{+}$.

Passiamo, ora, alla seconda parte della dimostrazione, ossia la dimostrazione che $X^{+}\subseteq Z^{(i)}$. Consideriamo un attributo $A$ contenuto in $X^{+}$, e consideriamo nuovamente l'iterazione $j$ tale per cui $S^{(j)}\subseteq Z^{(j)}$: andremo a dimostrare che $A\,\in\,Z^{(j)}$. Dato che $A\,\in\,X^{+}$, sappiamo per certo che $X\rightarrow A\,\in\,F^{A}$, e per il [[BD1_02 - Dipendenze funzionali#Teorema $F {+}=F {A}$|teorema]] del capitolo precedente ciò vuol dire che $X\rightarrow A\,\in\,F^{+}$: ciò vuol dire che la dipendenza $X\rightarrow A$ deve essere soddisfatta da qualsiasi istanza legale di $R$. Consideriamo, a questo punto, una specifica istanza $r$ di $R$:

|     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1   | 1   | ... | 1   | 1   | 1   | ... | 1   |
| 1   | 1   | ... | 1   | 0   | 0   | ... | 0   |

dove la prima metà della relazione (ossia le prime quattro colonne) rappresentano $Z^{(j)}$, mentre la seconda metà della relazione (ossia le ultime quattro colonne) rappresentano di conseguenza $R-Z^{(j)}$. Dimostriamo, innanzitutto, che tale istanza $r$ è legale. Assumiamo, per assurdo, che $r$ non sia legale, e dunque che esista almeno una dipendenza $V\rightarrow W\,\in\,F$ che non viene soddisfatta da essa: nel nostro caso specifico, per poter dire ciò è necessario che $V\subseteq Z^{(j)}$ (i valori delle due tuple di $r$ sono uguali solo in quel sottoinsieme di $R$, e per poter dire che una dipendenza non è soddisfatta è necessario che i determinanti di due tuple siano effettivamente uguali) e che $W\cap(R-Z^{(j)})\neq\emptyset$. Ora, abbiamo già specificato che l'iterazione $j$ è quella in cui si ha che $S^{(j)}\subseteq Z^{(j)}$, e dunque in cui non si aggiunge più niente all'insieme $Z$. Se abbiamo che $V\subseteq Z^{(j)}$ e che $W\cap(R-Z^{(j)})\neq\emptyset$, ciò vuol dire che ci sono degli elementi di $W$ che non si trovano ancora in $Z^{(j)}$, e dunque che a un'ipotetica iterazione $j+1$ questi elementi verrebbero aggiunti a $Z^{(j+1)}$ proprio attraverso la dipendenza $V\rightarrow W$. Tuttavia, abbiamo detto che $j$ è l'iterazione in cui l'algoritmo termina, dunque siamo arrivati a una contraddizione, dimostrando così che $r$ è un'istanza legale di $R$.

Avendo dimostrato ciò, possiamo tornare al punto principale della dimostrazione. Supponiamo, per assurdo, che esista un attributo $A$ che appartiene a $X^{+}$ ma non a $Z^{(j)}$: essendo $r$ un'istanza legale di $R$, essa deve necessariamente soddisfare la dipendenza $X\rightarrow A\,\in\,F^{+}$; dunque, se ci sono due tuple in $r$ con gli stessi valori su $X$, esse devono avere gli stessi valori anche su $A$. Guardando la tabella $r$, possiamo affermare tranquillamente che ci sono effettivamente due tuple identiche su $X$ (l'insieme $Z^{(0)}$ è inizializzato a $X$, e banalmente si ha che $Z^{(0)}\subseteq Z^{(j)}$, dunque anche $X\subseteq Z^{(j)}$); ciò vuol dire che le due tuple devono essere identiche anche su $A$, ma dato che $A$ non appartiene a $Z^{(j)}$ ciò non può verificarsi. Siamo arrivati a una contraddizione, dunque abbiamo dimostrato che se un attributo $A$ appartiene a $X^{+}$ allora appartiene anche a $Z^{(j)}$, o formalmente che $X^{+}\subseteq Z^{(j)}$.
___
##### Trovare le chiavi di uno schema di relazione $R$

Possiamo sfruttare l'insieme $X^{+}$ anche per trovare le **chiavi di uno schema $R$**. Ricordiamo la definizione di [[BD1_02 - Dipendenze funzionali#Una nuova definizione di chiave|chiave]]:

> Un sottoinsieme $K$ di attributi di $R$ è una chiave di $R$ se sono rispettate due condizioni:
> - $K\rightarrow R\,\in\,F^{+}$;
> - non esiste un sottoinsieme $K^{'}\subseteq K$ tale per cui valga la condizione precedente.

La prima delle due condizioni, ossia che $K\rightarrow R\,\in\,F^{+}$, equivale a dire che **la chiusura di $K$ comprenda tutti gli attributi di $R$**: dunque, per decretare che un sottoinsieme di attributi $K$ sia effettivamente una chiave, si potrà calcolare la sua chiusura, verificare che essa comprenda tutto $R$, e assicurarsi che non esiste un sottoinsieme di $K$ per cui valga la stessa condizione.

Vediamo un esempio. Supponiamo di avere il seguente schema $R$ e insieme $F$ di dipendenze funzionali definite su di esso:
$$\begin{align} &R=ABCDEH\\ &F=\{AB\rightarrow CD,\,C\rightarrow E,\,AB\rightarrow E,\,ABC\rightarrow D\} \end{align}$$
Supponiamo, come prima ipotesi, che $ABH$ sia una chiave (definiamo i sottoinsiemi di attributi che potrebbero essere chiavi "**chiavi candidate**"). Il primo passaggio per verificare questa ipotesi è calcolare l'insieme $ABH^{+}$, per verificare che contenga tutto $R$. Applichiamo quindi l'[[BD1_03 - La 3NF e la BCNF#Trovare la chiusura di un sottoinsieme $X$ di attributi di $R$|algoritmo per il calcolo della chiusura di un insieme di attributi]]: inizializziamo $Z=ABH$, e aggiungiamo $C$, $D$ ed $E$ alla prima iterazione del ciclo ($C$ e $D$ per la dipendenza $AB\rightarrow CD$, $E$ per la dipendenza $AB\rightarrow E$), e notiamo che in realtà abbiamo già incluso nella chiusura di $ABH$ tutti gli attributi di $R$. Si ha, dunque, che:
$$ABH^{+}=ABCDEH$$
A questo punto, per assicurarci che si tratti di una chiave, dovremo assicurarci che non ci sia un sottoinsieme di $ABH$ che determina funzionalmente tutto $R$, dunque si dovrà riapplicare l'algoritmo appena utilizzato sui vari sottoinsiemi di $ABH$. Per eseguire questa operazione, è importante tenere a mente alcune **regole e consigli utili**:
- conviene sempre **cominciare con i sottoinsiemi di cardinalità maggiore**, dato che se la loro chiusura non include tutti gli attributi di $R$ allora lo stesso varrà anche per i loro sottoinsiemi;
- **gli attributi che non compaiono mai nella parte destra delle dipendenze in $F$**, cioè gli attributi che non sono determinati funzionalmente da nessun altro attributo, **devono necessariamente essere inclusi in tutte le chiavi dello schema**.

Tenendo a mente questi due precetti, notiamo che $H$ non è funzionalmente determinato da nessun altro attributo, dunque $H$ dovrà far parte di tutte le chiavi di $R$: ciò ci indica che gli unici sottoinsiemi di $ABH$ che ci conviene considerare sono $AH$ e $BH$. Applicando l'algoritmo su $AH$, si ottiene che la sua chiusura corrisponde sempre a $AH$; lo stesso vale per $BH$, la cui chiusura è proprio $BH$: dunque, abbiamo verificato che non esistono sottoinsiemi di $ABH$ che determinano tutti gli attributi di $R$, e perciò possiamo affermare che **$ABH$ è una delle chiavi di $R$**.

Naturalmente, però, possono esserci **più chiavi in uno schema $R$**, dunque proseguiamo la nostra ricerca. Abbiamo stabilito che $H$ è un attributo che deve necessariamente fare parte di tutte le chiavi di $R$: dunque, vediamo se i sottoinsiemi $CH$, $DH$ ed $EH$ sono anch'essi chiavi di $R$. Applicando l'algoritmo per il calcolo della chiusura, otteniamo i seguenti risultati:
- $CH^{+}=CEH$;
- $DH^{+}=DH$;
- $EH^{+}=EH$.

Dunque, nessuno di questi sottoinsiemi può essere una chiave di $R$. A questo punto, dovremmo procedere ad analizzare sottoinsiemi di $R$ di cardinalità $3$ che contengono $H$. Notiamo, tuttavia, alcune particolarità dello schema che ci permetteranno di arrivare subito a una conclusione: aggiungere l'attributo $A$ a una chiave candidata senza l'attributo $B$ (o viceversa) non può portare a un insieme di attributi con una chiusura soddisfacente, dato che l'attributo $D$ dipende da sottoinsiemi di $R$ dove appaiono entrambi questi attributi; al tempo stesso, né $A$ né $B$ dipendono da altri attributi di $R$, dunque devono necessariamente essere contenuti in ogni chiave di $R$. Queste considerazioni ci fanno capire che, in realtà, $ABH$ è l'unica chiave di $R$.

Vediamo un altro esempio. Supponiamo di avere il seguente schema $R$ e insieme $F$ di dipendenze funzionali determinate su di esso:
$$\begin{align} &R=ABCDEGH\\ &F=\{AB\rightarrow D,\,G\rightarrow A,\,G\rightarrow B,\,H\rightarrow E,\,H\rightarrow E,\,D\rightarrow H\} \end{align}$$
Vogliamo determinare le **4 chiavi** di $R$. Innanzitutto, individuiamo gli **attributi che ne  determinano funzionalmente altri**, così come quelli che **non sono determinati da altri attributi**. Abbiamo che **$AB$, $G$, $D$ e $H$ sono gli attributi che ne determinano altri**, mentre $C$ è l'unico attributo che non viene determinato da nessun'altro, dunque **$C$ dovrà essere contenuto in tutte le chiavi di $R$**.

Procediamo, dunque, a **verificare se le chiavi candidate $ABC$, $GC$, $DC$ e $HC$ sono effettivamente chiavi di $R$**:
- la chiusura di $ABC$, ossia $ABC^{+}$, risulta comprendere tutti gli attributi di $R$, dunque se lo stesso non vale per i suoi sottoinsiemi (dovendo $C$ essere contenuto in tutte le chiavi di $R$, basterà controllare solo $AC$ e $BC$) allora $ABC$ è una chiave di $R$; le chiusure di $AC$ e di $BC$ sono rispettivamente $AC$ e $BC$, dunque la condizione è rispettata e **$ABC$ è una chiave di $R$**;
- la chiusura di $GC$, ossia $GC^{+}$, risulta comprendere tutti gli attributi di $R$, e dato che né $G$ (non include $C$) né $C$ (da solo non determina altri attributi oltre a sé stesso) possono essere chiavi, abbiamo che **$GC$ è una chiave di $R$**;
- la chiusura di $DC$, ossia $DC^{+}$, risulta comprendere tutti gli attributi di $R$, e dato che né $D$ né $C$ possono essere chiavi, abbiamo che **$DC$ è una chiave di $R$**;
- la chiusura di $HC$, ossia $HC^{+}$, risulta comprendere tutti gli attributi di $R$, e dato che né $H$ né $C$ possono essere chiavi, abbiamo che **$HC$ è una chiave di $R$**.

Dunque, si ottiene che **le 4 chiavi di $R$ sono $ABC$, $GC$, $DC$ e $HC$**.

In generale, per decidere da dove iniziare a cercare le chiavi di uno schema, possiamo cominciare considerando certi insiemi di attributi identificati sfruttando le dipendenze funzionali dell'insieme $F$. Data una dipendenza $V\rightarrow W\,\in\,F$, possiamo partire calcolando la chiusura degli insiemi di attributi $X=R-(W-V)$: se la chiusura di $X$ contiene $R$, allora abbiamo identificato una super-chiave di $R$ (si dovranno comunque controllare i suoi sottoinsiemi per trovare le chiavi effettive).

Vediamo un esempio di applicazione di questo metodo: supponiamo di avere il seguente schema $R$ e insieme $F$ di dipendenze funzionali definite su di esso:
$$\begin{align} &R=ABCDE\\ &F=\{AB\rightarrow C,\,AC\rightarrow B,\,D\rightarrow E\} \end{align}$$
Basandoci sulle dipendenze contenute in $F$, andremo ad analizzare i sottoinsiemi $ABDE$ ($R - C$), $ACDE$ ($R-B$) e $ABCD$ ($R-E$). Le chiusure di tutti questi sottoinsiemi comprendono tutti gli attributi di $R$, dunque tutti e 3 sono super-chiavi di $R$. A questo punto, andiamo ad analizzare i loro sottoinsiemi: partiamo analizzando $AB$, e notiamo che $AB^{+}=ABC\neq R$, tuttavia aggiungendo $D$ andremo a determinare anche $E$, trovando dunque che $ABD^{+}=R$; ciò ci indica non solo che **$ABD$ è una chiave di $R$**, ma anche che $ABDE$ e $ABCD$ sicuramente non lo sono. Analizziamo, ora, $AC$, e notiamo che $AC^{+}=ABC\neq R$, tuttavia anche in questo caso aggiungendo $D$ andremo a determinare anche $E$, trovando dunque che $ACD^{+}=R$; ciò ci indica che $ACDE$ sicuramente non è una chiave, e verificando che non lo siano neanche $D$ ($D^{+}=DE$) o $E$ ($E^{+}=E$) possiamo affermare che **$ACD$ è una chiave di $R$**. Dunque, le due chiavi di $R$ sono $ABD$ e $ACD$.

In alcuni casi, può essere utile applicare la seguente regola, chiamata "**test dell'unicità**":

> Dato uno schema di relazione $R$ e un insieme $F$ di dipendenze funzionali definite su di esso, se per ogni dipendenza $V\rightarrow W\,\in\,F$ si trovano i vari sottoinsiemi di attributi $X=R-(W-V)$, e l'intersezione dei vari insiemi $X$ trovati determina tutto $R$, allora tale intersezione sarà l'unica chiave di $R$.

Invece, se l'intersezione dei sottoinsiemi $X$ trovati non determina tutto $R$, vorrà dire che ci sono più chiavi per tale schema.
___
##### Preservare le dipendenze contenute in $F^{+}$

Ora che abbiamo capito come sfruttare la [[BD1_03 - La 3NF e la BCNF#Trovare la chiusura di un sottoinsieme $X$ di attributi di $R$|chiusura di un sottoinsieme di attributi]] per trovare le [[BD1_03 - La 3NF e la BCNF#Trovare le chiavi di uno schema di relazione $R$|chiavi]] di uno schema $R$, possiamo pensare concretamente a come **scomporre uno schema $R$ in più schemi in 3NF**.

Innanzitutto, definiamo formalmente la scomposizione di $R$:

> Dato uno schema di relazione $R$, definiamo una **"scomposizione" di $R$** una famiglia $R_{1},\,R_{2},\,\dots,\,R_{k}$ di sottoinsiemi di $R$ tali per cui:
> $$R=\bigcup_{i\,=\,1}^{k}R_{i}$$
> In altre parole, scomporre uno schema $R$ significa definire vari "sotto-schemi", ognuno dei quali contenente una parte degli attributi di $R$ e la cui unione dovrà restituire proprio $R$.

Come abbiamo già detto varie volte, però, per scomporre correttamente uno schema $R$ si dovrà fare attenzione a diversi fattori, tra cui **preservare le dipendenze funzionali contenute in $F^{+}$**, ossia nella chiusura dell'insieme $F$ di dipendenze definite inizialmente su $R$. Vogliamo, dunque, accertarci che l'insieme di dipendenze iniziale sia "**equivalente**" a quello che otterremo dopo la scomposizione: ma cosa vuol dire concretamente che due insiemi di dipendenze funzionali sono equivalenti?

> Dati due insiemi $F$ e $G$ di dipendenze funzionali, si dice che "**$F$ e $G$ sono equivalenti**", simbolicamente scritto come $F\equiv G$, se vale che:
> $$F^{+}=G^{+}$$

Dunque, non è necessario che $F$ e $G$ contengano le stesse dipendenze, ma piuttosto che ciò valga per le loro chiusure. In altre parole, per fare in modo che $F$ e $G$ siano equivalenti devono valere le seguenti due condizioni:
$$F^{+}\subseteq\, G^{+}\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,G^{+}\subseteq\, F^{+}$$
Come già visto in precedenza, calcolare la chiusura di un insieme di dipendenze funzionali è un'operazione molto inefficiente, che preferiremmo evitare. In alternativa, possiamo basarci su un **lemma** e su un nuovo **algoritmo per verificare l'equivalenza tra due insiemi di dipendenze funzionali** in **tempo polinomiale**. 

Il lemma è il seguente:

> Siano $F$ e $G$ due insiemi di dipendenze funzionali. Si ha che:
> $$\text{se }F\subseteq G^{+},\,\text{allora }F^{+}\subseteq\,G^{+}$$

Dimostriamo questo lemma: consideriamo una generica dipendenza $f\,\in\,F^{+}-F$, dunque una dipendenza contenuta in $F^{+}$ ma non in $F$. Essendo $F$ un sottoinsieme di $G^{+}$ per ipotesi, possiamo affermare che qualsiasi dipendenza funzionale trovata in $F$ può essere derivata da $G$ applicando ricorsivamente gli [[BD1_02 - Dipendenze funzionali#Assiomi di Armstrong e regole corollarie|assiomi di Armstrong]], e naturalmente sapendo che $F^{+}=F^{A}$, la dipendenza $f\,\in\,F^{+}$ può essere derivata da $F$ con le stesse modalità. Ciò, dunque, implica che qualsiasi dipendenza $f\,\in\,F^{+}$ può essere derivata da $G$ applicando gli assiomi di Armstrong, e dunque che l'insieme di dipendenze $F^{+}$ è un sottoinsieme di $G^{+}$, come volevasi dimostrare.

A questo punto, torniamo al problema principale, ossia il verificare che una scomposizione preservi tutte le dipendenze di $F$. Concretamente, vale la seguente definizione:

> Dato uno schema di relazione $R$, un insieme $F$ di dipendenze funzionali definite su di esso, e una scomposizione $\rho=R_{1},\,R_{2},\,\dots,\,R_{k}$ di $R$, si può affermare che "**$\rho$ preserva $F$**" se vale che:
> $$F\equiv G=\bigcup_{i\,=\,1}^{k}\pi_{R_{i}}(F)$$
> dove $\pi_{R_{i}}(F)=\{X\rightarrow Y\,\in\,F^{+}\,\,|\,\,XY\subseteq R_{i}\}$.

Per chiarezza, $G$ naturalmente è un insieme di dipendenze funzionali, e ciascun insieme $\pi_{R_{i}}(F)$ è un insieme di dipendenze ottenuto proiettando $F$ sul sottoschema $R_{i}$, ossia considerando tutte le dipendenze derivabili da $F$ applicando gli assiomi di Armstrong (dunque, le dipendenze di $F^{+}$) che contengono solo attributi di $R_{i}$.

Supponiamo di avere già una scomposizione, e di voler **verificare che preservi tutte le dipendenze dell'insieme $F$ di partenza**. Verificare che una scomposizione rispetti questa condizione richiede di verificare l'equivalenza tra i due insiemi di dipendenze funzionali $F$ e $G=\bigcup_{i\,=\,1}^{k}\pi_{R_{i}}(F)$: notiamo che, per la definizione di $G$, è garantito che $G\subseteq F^{+}$, e si ha che ogni proiezione di $F$ che è inclusa in $G$ è inclusa anche in $F^{+}$, dunque deduciamo che $G^{+}\subseteq\,F^{+}$; dunque, l'unica condizione che si dovrà verificare è che **$F\subseteq G^{+}$**. 

È qui che entra in gioco un nuovo **algoritmo**, utilizzato per **verificare che $F$ sia contenuto in $G^{+}$**. L'algoritmo in questione ha i seguenti input e output:
- come **input**, abbiamo due insiemi $F$ e $G$ di dipendenze funzionali definite su $R$;
- come **output**, una variabile booleana che è `true` se $F\subseteq G^{+}$, e `false` altrimenti.

Di seguito, lo **pseudocodice** dell'algoritmo:

```
success = true

for each X → Y ∈ F:
	compute Z = closure of X with respect to G
	if (Y ⊄ Z) then success = false
```

Infatti, se vale che $Y\subseteq X^{+}_{G}$, allora si ha che $X\rightarrow Y\,\in\,G^{A}$ e di conseguenza che $X\rightarrow Y\,\in\,G^{+}$. Sarà sufficiente trovare anche una singola dipendenza per cui non vale questa condizione per dimostrare che l'equivalenza tra $F$ e $G$ non sussista.

Ma come facciamo a **calcolare $X^{+}_{G}$**? Per usare l'[[BD1_03 - La 3NF e la BCNF#Trovare la chiusura di un sottoinsieme $X$ di attributi di $R$|algoritmo per il calcolo della chiusura di un insieme di attributi]] dovremmo calcolare prima $G$; al tempo stesso, per definizione di $G$, esso dipende da $F^{+}$, e calcolare tale insieme sappiamo essere un'operazione tediosa e inefficiente. Per fortuna, possiamo sfruttare un **algoritmo per calcolare $X^{+}_{G}$ a partire da $F$**. Tale algoritmo ha i seguenti input e output:
- come **input**, abbiamo uno schema di relazione $R$, un insieme $F$ di dipendenze funzionali definite su $R$, una scomposizione $\rho=R_{1},\,R_{2},\,\dots,\,R_{k}$ e un sottoinsieme $X$ di attributi di $R$;
- come **output**, una variabile $Z$ contenente la chiusura $X^{+}_{G}$.

Di seguito, lo **pseudocodice** dell'algoritmo:

```
Z = X
S = ∅

for i = 1 to k:
	S = S ∪ (closure of (Z ∩ Ri) w.r.t. F) ∩ Ri

while S ⊄ Z:
	Z = Z ∪ S
	for i = 1 to k:
		S = S ∪ (closure of (Z ∩ Ri) w.r.t. F) ∩ Ri
```

Più nel dettaglio, quello che andiamo a fare nel primo ciclo è raccogliere in $S$ gli attributi determinati funzionalmente dall'intersezione tra $Z$ e $R_{i}$ secondo le dipendenze contenute in $F^{+}$, e tra questi selezioniamo solo quelli contenuti nel rispettivo sottoschema $R_{i}$. Dunque, partendo da un insieme di attributi $X$, stiamo costruendo la sua chiusura a partire dalle proiezioni di $F$ che andranno a comporre $G$, e poi da lì a partire da $G^{+}$ per transitività. L'intersezione con $R_{i}$, del resto, è molto importante perché ci assicura che la dipendenza che stiamo considerando è valida nel sottoschema corrente.

Dimostriamo che l'algoritmo appena presentato computa correttamente la chiusura $X^{+}_{G}$. Indichiamo con $Z^{(0)},\,Z^{(1)},\,\dots,\,Z^{(j)}$ la sequenza di valori assunti dalla variabile $Z$ a ogni iterazione del ciclo `while` dell'algoritmo, con $Z^{(j)}$ che rappresenta il valore ritornato (dunque, $j$ è l'iterazione con cui termina l'algoritmo). Vogliamo dimostrare che:
$$Z^{(j)}=X^{+}_{G}$$
Scomponiamo tale dimostrazione in due parti, andando invece a dimostrare le due seguenti inclusioni:
$$Z^{(j)}\subseteq Z^{+}_{G}\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,X^{+}_{G}\subseteq Z^{(j)}$$
Partiamo dalla prima, ossia che $Z^{(j)}\subseteq X^{+}_{G}$, che andremo a dimostrare per induzione proprio sul numero $i$ di iterazioni dell'algoritmo. Il caso base è $i=0$: in questo caso, abbiamo che $Z^{(0)}=X$, e per definizione $X\subseteq X^{+}_{G}$, dunque il caso base è verificato. Passiamo dunque all'ipotesi induttiva: 

[dim 05 - pag. 4]

Si noti che l'algoritmo termina sempre la sua esecuzione, ma che ciò non indica necessariamente che una determinata dipendenza $X\rightarrow Y$ è preservata: infatti, questo algoritmo computa solo ed esclusivamente le chiusure $X^{+}_{G}$, e si dovrà poi fare nuovamente riferimento all'algoritmo precedente per verificare ciò.
___
##### Ricostruire le informazioni originali con un join

La seconda condizione principale che si vuole rispettare per effettuare una "buona" scomposizione di uno schema in più schemi posti in 3NF è quella di poter **ricostruire tutte e sole le informazioni originali con un join** sui sotto-schemi creati. 

In altre parole, se scomponiamo uno schema di relazione $R$ in una scomposizione $\rho=R_{1},\,R_{2},\,\dots,\,R_{k}$, si vuole che essa sia tale per cui **qualsiasi istanza legale $r$ di $R$ può essere ricostruita tramite [[BD1_01 - Modello relazionale#Join naturale|join naturale]] sulle corrispondenti istanze legali $r_{1},\,r_{2},\,\dots,\,r_{k}$ dei sotto-schemi $R_{1},\,R_{2},\,\dots,\,R_{k}$**. Una scomposizione che rispetta questa proprietà si dice dotata di un "lossless join".

> Dato uno schema di relazione $R$, una scomposizione $\rho=R_{1},\,R_{2},\,\dots,\,R_{k}$ di tale schema si dice dotata di "**lossless join**" se, per ogni istanza legale $r$ di $R$, vale che:
> $$r\,=\,\pi_{R_{1}}(r)\,\Join\,\pi_{R_{2}}(r)\,\Join\,\dots\,\Join\pi_{R_{k}}(r)$$

A questo punto, con un approccio analogo ad altri visti finora, il nostro obiettivo diventa trovare un modo di **verificare che una scomposizione rispetti la definizione appena fornita**. Per fare ciò, possiamo utilizzare un **algoritmo**, che presenta i seguenti input e output:
- come **input**, abbiamo uno schema di relazione $R$, un insieme $F$ di dipendenze funzionali definite su $R$ e una scomposizione $\rho=R_{1},\,R_{2},\,\dots,\,R_{k}$;
- come **output**, una variabile booleana che è `true` se $\rho$ ha un lossless join, e `false` altrimenti.

Di seguito, lo **pseudocodice** (molto verboso e approssimativo) dell'algoritmo:

```
construct a table r as follows:
	r has R columns and k rows
	at the intersection of the i-th row and the j-th column put:
		the symbol aj if the attribute A ∈ Rij
		the symbol bij otherwise
		
for each X → Y ∈ F:
	if there are two tuples t1 and t2 in r such that t1[X] = t2[X] and t1[Y] ≠ t2[Y]:
		for each attribute Aj in Y:
			if t1[Aj] = aj:
				t2[Aj] = t1[Aj]
			else:
				t1[Aj] = t2[Aj]

repeat until r has a line with all "a" or r has not changed

if r has a row with all "a":
	it has a lossless join
else:
	it doesn't have a lossless join
```

Cerchiamo di analizzare questo algoritmo più nel dettaglio, in modo da chiarire meglio il suo funzionamento. La prima cosa che ci chiede di fare l'algoritmo è di **costruire una tabella $r$** che rispetti i seguenti requisiti:
- abbia **$R$ colonne**, dunque una colonna per ogni attributo di $R$;
- abbia **$k$ righe**, dunque una riga per ogni sottoschema della scomposizione $\rho$.

Ora, si chiede di **riempire la tabella** $r$ in modo tale che, nella cella rappresentante l'intersezione tra la $i$-esima riga e la $j$-esima colonna, sia presente un valore $a_{j}$ se vale che $A\in R_{i,\,j}$, ossia in altre parole se l'attributo $A_{j}$ è contenuto nel sottoschema $R_{i}$, e un valore $b_{i,\,j}$ altrimenti. Per chiarezza, specifichiamo che $a_{j}$ e $b_{i,\,j}$ rappresentano valori particolari appartenenti al dominio di $A_{j}$, e consideriamo tutti i valori $a_{j}$ uguali tra loro, mentre un particolare valore $b_{i,\,j}$ diverso da $a_{j}$ e da un altro valore $b_{k,\,j}$. Come conseguenza di queste condizioni, **la tabella $r$ iniziale corrisponde a una generica istanza dello schema $R$**.

A questo punto, l'algoritmo intima di ripetere un'operazione **per ogni dipendenza funzionale $X\rightarrow Y$ contenuta in $F$**: l'operazione in questione consiste nel verificare se esistono in $r$ due tuple $t_{1}$ e $t_{2}$ tali per cui si ha che $t_{1}[X]=t_{2}[X]$ e che $t_{1}[Y]\neq t_{2}[Y]$, e se tale condizione è vera allora si controllerà un'ulteriore condizione per ogni attributo $A_{j}$ contenuto in $Y$. Stavolta, si controlla che $t_{1}[A_{j}]=a_{j}$: se ciò è vero, allora si assegna a $t_{2}[A_{j}]$ il valore di $t_{1}[A_{j}]$, altrimenti viceversa, dunque si assegna a $t_{1}[A_{j}]$ il valore di $t_{2}[A_{j}]$. In altre parole, questa parte dell'algoritmo va a **modificare $r$ portandola a soddisfare tutte le dipendenze contenute in $F$**; infatti, se trova due tuple che non rispettano una determinata dipendenza $X\rightarrow Y$, va ad effettuare una modifica per "legalizzare" le tuple, e nel fare ciò l'algoritmo dà priorità a $a_{j}$ piuttosto che a $b_{i,\,j}$ (infatti, notiamo che $a_{j}$ non verrà mai trasformato in $b_{i,\,j}$, ma quest'ultimo può tranquillamente essere sostituito col primo). Più nel dettaglio, se si trovano due tuple che hanno gli stessi valori come [[BD1_02 - Dipendenze funzionali#Cos'è una dipendenza funzionale?|determinanti]] e valori diversi come [[BD1_02 - Dipendenze funzionali#Cos'è una dipendenza funzionale?|dipendenti]], e solo una delle due tuple presenta un valore $a_{j}$ in quest'ultimo, allora il valore dipendente dell'altra diventerà anch'esso $a_{j}$. Invece, se si trovano due tuple che hanno gli stessi valori come determinanti e valori diversi come dipendenti, e nessuna delle due presenta un valore $a_{j}$ in questi ultimi, allora faremo in modo che entrambe le tuple presentino lo stesso valore $b_{i,\,j}$ (come abbiamo detto in precedenza, abbiamo posto che i valori $b_{i,\,j}$ sono diversi sia da $a_{j}$ che da altri valori $b_{k,\,j}$). 

L'operazione svolta nel ciclo che abbiamo appena analizzato **si ripete finché non viene rispettata una delle due seguenti condizioni**:
- $r$ presenta una riga con solo valori $a$;
- $r$ non cambia più.

In particolare, l'algoritmo termina quando **tutte le tuple di $r$ soddisfano le dipendenze contenute in $F$**, dunque quando **$r$ diventa un'istanza legale di $R$**. A questo punto, l'ultimissimo passaggio è quello di determinare se $\rho$ ha un lossless join o meno, e per farlo si verifica se **$r$ presenta una riga con solo valori $a$**.

Ma perché è sufficiente tale condizione per determinare che $\rho$ ha un lossless join? Vediamo una **dimostrazione** di tale regola, e dunque formalmente del seguente teorema:

> Dato uno schema di relazione $R$, un insieme $F$ di dipendenze funzionali definite su di esso, e una scomposizione $\rho=R_{1},\,R_{2},\,\dots,\,R_{k}$ di $R$, si può verificare che $\rho$ ha un lossless join applicando l'algoritmo; in particolare, **$\rho$ ha un lossless join se e solo se, quando termina l'esecuzione dell'algoritmo, $r$ presenta una tupla con solo valori $a$**.

Supponiamo, **per assurdo**, che $\rho$ abbia un lossless join ma che, quando termina l'esecuzione dell'algoritmo, $r$ non presenti una tupla con solo valori $a$. Poco fa abbiamo specificato che, al termine dell'algoritmo, $r$ è a tutti gli effetti un'istanza legale di $R$, dato che a quel punto non ci sono più violazioni delle dipendenze contenute in $F$. 

[15 - slide 20]
___
##### Trovare la copertura minimale di un insieme di dipendenze funzionali

Finora, abbiamo stabilito quali fossero i requisiti per una corretta scomposizione di uno schema di relazione $R$ in più sottoschemi, abbiamo approfondito vari passaggi importanti come [[BD1_03 - La 3NF e la BCNF#Trovare le chiavi di uno schema di relazione $R$|trovare le chiavi di uno schema]], [[BD1_03 - La 3NF e la BCNF#Preservare le dipendenze contenute in $F {+}$|preservare le dipendenze]] dello stesso e come verificare che una scomposizione disponga di un [[BD1_03 - La 3NF e la BCNF#Ricostruire le informazioni originali con un join|lossless join]]. Soffermandoci su quest'ultimo aspetto, seppur sappiamo ora verificare ciò, dobbiamo ancora capire **come ottenere una "buona" scomposizione di uno schema $R$**.

Chiariamo subito che **è sempre possibile ottenere una "buona" scomposizione di uno schema**, ossia una scomposizione tale per cui:
- ogni sottoschema ottenuto si trova in [[BD1_03 - La 3NF e la BCNF#La 3NF|3NF]];
- la scomposizione preserva le dipendenze contenute in $F$;
- è possibile ricostruire qualsiasi istanza legale dello schema originale tramite un join naturale delle istanze della scomposizione.

Anche in questo caso, per ottenere tale scomposizione si può utilizzare un **algoritmo**, che vedremo tra poco. È importante ricordare che **la scomposizione che si ottiene applicando l'algoritmo non è necessariamente l'unica buona scomposizione possibile** per quello schema, dato che possono esistere più scomposizioni di uno stesso schema. Dunque, è da escludere la possibilità di controllare se una scomposizione già data è buona applicando l'algoritmo e confrontando la scomposizione risultante con la prima, dato che potrebbero essere due scomposizioni diverse ma entrambe valide.

Prima di continuare, sarà necessario introdurre un concetto fondamentale, ossia quello della "copertura minimale", dato che costituirà l'input dell'algoritmo di calcolo della scomposizione di uno schema $R$.

> Dato un insieme $F$ di dipendenze funzionali, definiamo "**copertura minimale**" di $F$ un insieme $G$, equivalente a $F$, di dipendenze funzionali, tale per cui:
> - per ogni dipendenza in $G$, il dipendente è un singoletto (in altre parole, **ogni dipendente è "non-ridondante"**);
> - per ogni dipendenza $X\rightarrow A\,\in\,G$, non esiste un sottoinsieme $X'\subset X$ tale per cui vale che $G\equiv G-\{X\rightarrow A\}\cup\{X'\rightarrow A\}$ (in altre parole, **ogni determinante è non-ridondante**);
> - non esiste alcuna dipendenza $X\rightarrow A\,\in\,G$ tale per cui vale che $G\equiv G-\{X\rightarrow A\}$ (in altre parole, **ogni dipendenza è non-ridondante**).

Ricordiamo che due insiemi di dipendenze funzionali si dicono "equivalenti" se dispongono della **stessa chiusura**. Chiariamo cosa implica ciascuno dei tre punti visti nella definizione:
- la prima condizione è che ogni dipendente sia non-ridondante, e per fare ciò richiede che ciascun dipendente sia un singoletto (ciò è sempre possibile sfruttando la [[BD1_02 - Dipendenze funzionali#Assiomi di Armstrong e regole corollarie|regola della decomposizione]]);
- la seconda condizione è che ogni determinante sia non ridondante, e in parole povere ciò implica che per ogni dipendenza $X\rightarrow A$ non sia possibile determinare $A$ con un sottoinsieme di $X$;
- la terza e ultima condizione è che ogni dipendenza sia non ridondante, e dunque che per ogni dipendenza $X\rightarrow A$ non sia possibile determinare $A$ attraverso altre dipendenze.

Dato un insieme $F$ di dipendenze funzionali, possono esistere **diverse coperture minimali dello stesso insieme $F$**: è proprio questo il motivo per cui l'algoritmo di calcolo della scomposizione di uno schema $R$ può produrre diversi risultati plausibili.

Per **ottenere una copertura minimale di $F$**, si segue una serie di passaggi che permette di trovare un risultato in **tempo polinomiale**, ossia:
1. utilizzando la regola di decomposizione, **ridurre i dipendenti in singoletti**;
2. **ogni dipendenza funzionale $A_{1}A_{2}\dots A_{i-1}A_{i}A_{i+1}\dots A_{n}\rightarrow A$ di $F$ tale per cui $F\equiv F-\{A_{1}A_{2}\dots A_{i-1}A_{i}A_{i+1}\dots A_{n}\rightarrow A\}\cup\{A_{1}A_{2}\dots A_{i-1}A_{i+1}\dots A_{n}\rightarrow A\}$ va rimpiazzata dalla dipendenza $A_{1}A_{2}\dots A_{i-1}A_{i+1}\dots A_{n}\rightarrow A$**, e se quest'ultima appartiene già a $F$ allora la prima viene semplicemente eliminata; questo procedimento dovrà essere ripetuto ricorsivamente sulla dipendenza ottenuta, e **terminerà quando non ci saranno più dipendenze riducibili**;
3. **rimuovere ogni dipendenza funzionale ridondante**, dunque ogni dipendenza $X\rightarrow A\,\in\,F$ tale per cui $F\equiv F-\{X\rightarrow A\}$.

Notiamo che gli ultimi due passaggi richiedono di verificare l'equivalenza tra due insiemi di dipendenze funzionali: per poter fare ciò, ricordiamo alcune definizioni e conclusioni rilevanti:
- due insiemi $F$ e $G$ di dipendenze funzionali si dicono equivalenti se le loro chiusure coincidono, dunque $F\equiv G\iff F^{+}=G^{+}$, dunque se e solo se vale sia che $F^{+}\subseteq G^{+}$ sia che $G^{+}\subseteq F^{+}$;
- se si ha che $F\subseteq G$, allora banalmente vale anche che $F\subseteq G^{+}$;
- se si ha che $F\subseteq G^{+}$, allora vale anche che $F^{+}\subseteq G^{+}$.

Per verificare che $F\subseteq G^{+}$ basterà verificare che per ogni $X\rightarrow Y\,\in\,F$ si ha anche $X\rightarrow Y\,\in\,G^{+}$, o in altre parole che $Y\subseteq X^{+}_{G}$. 

Analizziamo più da vicino il **secondo passaggio dell'algoritmo**: ogni volta che vogliamo verificare la ridondanza di un attributo nel determinante di una dipendenza, considereremo come $F$ l'insieme di dipendenze che contiene la dipendenza originale $A_{1}A_{2}\dots A_{i-1}A_{i}A_{i+1}\dots A_{n}\rightarrow A$, e come $G$ l'insieme che contiene la dipendenza $A_{1}A_{2}\dots A_{i-1}A_{i+1}\dots A_{n}\rightarrow A$. I due insiemi $F$ e $G$, dunque, sono diverse per un'unica dipendenza, mentre tutte le altre rimangono invariate: ciò ci dice, naturalmente, che quest'ultime appartengono sicuramente alle chiusure dei loro rispettivi insiemi. Dunque, per verificare che $F$ e $G$ siano equivalenti, dovremo verificare solo queste due appartenenze:
$$A_{1}A_{2}\dots A_{i-1}A_{i}A_{i+1}\dots A_{n}\rightarrow A\,\in\,G^{+}\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,A_{1}A_{2}\dots A_{i-1}A_{i+1}\dots A_{n}\rightarrow A\,\in\,F^{+}$$

Per verificare che $A_{1}A_{2}\dots A_{i-1}A_{i}A_{i+1}\dots A_{n}\rightarrow A\,\in\,G^{+}$, sarà sufficiente verificare che $A\,\in\,(A_{1}A_{2}\dots A_{i-1}A_{i}A_{i+1}\dots A_{n})^{+}_{G}$, dunque andiamo a ripescare l'[[BD1_03 - La 3NF e la BCNF#Trovare la chiusura di un sottoinsieme $X$ di attributi di $R$|algoritmo di calcolo della chiusura di un sottoinsieme di attributi]]. Notiamo che l'algoritmo in questione inizializza $Z$ come un insieme che è concretamente più grande rispetto a quello corrispondente presente nell'insieme $G$: infatti, per definizione in $G$ è presente la dipendenza $A_{1}A_{2}\dots A_{i-1}A_{i+1}\dots A_{n}\rightarrow A$, mentre noi stiamo verificando la chiusura dell'insieme di attributi $A_{1}A_{2}\dots A_{i-1}A_{i}A_{i+1}\dots A_{n}$. Di conseguenza, all'interno dell'insieme $S$ verrà automaticamente inserito $A$, data la presenza in $G$ della dipendenza appena vista.

Rimane, ora, il problema di verificare che $A_{1}A_{2}\dots A_{i-1}A_{i+1}\dots A_{n}\rightarrow A\,\in\,F^{+}$; seguendo lo stesso approccio appena visto, vogliamo di conseguenza dimostrare che $A\,\in\,(A_{1}A_{2}\dots A_{i-1}A_{i+1}\dots A_{n})^{+}_{F}$. Stavolta non ci sono scappatoie, e si dovrà eseguire l'algoritmo per verificare la verità di questa proposizione. Potrebbe esserci, ciononostante, il caso particolare in cui la dipendenza $A_{1}A_{2}\dots A_{i-1}A_{i+1}\dots A_{n}\rightarrow A$ appartiene già a $F$, e dunque anche a $F^{+}$: in tal caso, basterà eliminare la dipendenza originale (ad esempio, se $F$ contiene sia $AB\rightarrow C$ che $A\rightarrow C$, allora $AB\rightarrow C$ potrà essere eliminata). In qualsiasi altro caso, si esegue l'algoritmo e, se si verifica l'equivalenza dei due insiemi $F$ e $G$, allora si procede considerando l'insieme $G$ ottenuto come il nuovo insieme $F$.

Un consiglio da tenere a mente per svolgere questo passaggio dell'algoritmo più efficientemente è il seguente: se abbiamo una dipendenza $A_{1}A_{2}\dots A_{n}\rightarrow A\,\in\,F$ e anche una dipendenza di tipo $Y\rightarrow A\,\in\,F$ con $Y\subset A_{1}A_{2}\dots A_{n}$, allora andremo subito ad eliminare la prima senza bisogno di ulteriori controlli.

Passiamo ora al **terzo passaggio dell'algoritmo**. Denotiamo con $F$ l'insieme di dipendenze contenente la dipendenza $X\rightarrow A$, e $G$ l'insieme dove quest'ultima è stata eliminata. Anche in questo caso, i due insiemi $F$ e $G$ sono diversi per un'unica dipendenza, e naturalmente si ha che $G\subseteq F$, dunque possiamo affermare senza problemi che $G^{+}\subseteq F^{+}$. Per verificare l'altro verso dell'equivalenza, dunque che $F^{+}\subseteq G^{+}$, basterà verificare che la dipendenza da eliminare $X\rightarrow A$ appartenga a $G^{+}$, ossia che $A\,\in\,X^{+}_{G}$. 

Un consiglio da tenere a mente per svolgere questo passaggio dell'algoritmo più efficientemente è il seguente: se abbiamo una dipendenza $X\rightarrow A\,\in\,F$, ma non esiste alcuna dipendenza $Y\rightarrow A\,\in\,F$ con $Y\neq X$, allora non avrà senso cercare di eliminare la dipendenza $X\rightarrow A$, dato che in sua assenza non saremmo più in grado di determinare funzionalmente $A$.

Dunque, ricapitolando:
- per eseguire il primo passaggio, basterà applicare ricorsivamente la regola della decomposizione;
- per eseguire il secondo passaggio, ossia per eliminare attributi ridondanti da dipendenze di tipo $A_{1}A_{2}\dots A_{i-1}A_{i}A_{i+1}\dots A_{n}\rightarrow A\,\in\,F$, si dovrà verificare l'equivalenza tra $F$ e $G$, dove $G$ è l'insieme di dipendenze uguale a $F$ ma con la dipendenza considerata sostituita da $A_{1}A_{2}\dots A_{i-1}A_{i+1}\dots A_{n}\rightarrow A$, e per fare ciò basterà verificare che $A\,\in\,(A_{1}A_{2}\dots A_{i-1}A_{i+1}\dots A_{n})^{+}_{F}$; se ciò è vero, allora possiamo eliminare la dipendenza originale e sostituirla con quella trovata;
- per eseguire il terzo passaggio, ossia per eliminare dipendenze ridondanti, si dovrà verificare l'equivalenza tra $F$ e $G$, dove $G$ è l'insieme di dipendenze uguale a $F$ ma con la dipendenza considerata eliminata, e per fare ciò basterà verificare che $A\,\in\,X^{+}_{G}$; se ciò è vero, allora possiamo eliminare la dipendenza originale.

Applicando questo algoritmo, sarà possibile trovare almeno una copertura minimale per qualsiasi insieme $F$ di dipendenze funzionali, e dunque sarà possibile applicare l'[[BD1_03 - La 3NF e la BCNF#Scomporre correttamente uno schema $R$ in più sottoschemi|algoritmo di scomposizione]] che vedremo nel prossimo paragrafo.
___
##### Scomporre correttamente uno schema $R$ in più sottoschemi

Arriviamo, a questo punto, a capire **come scomporre uno schema di relazione $R$ e un insieme $F$ di dipendenze definite su di esso in più sottoschemi**. Tale operazione non solo è sempre possibile, ma è sempre possibile risultare in una **"buona" scomposizione**, ossia una scomposizione $\rho=R_{1},\,R_{2},\,\dots,\,R_{k}$ che presenta le seguenti caratteristiche:
- **tutti i sottoschemi sono in [[BD1_03 - La 3NF e la BCNF#La 3NF|3NF]]**;
- **$\rho$ [[BD1_03 - La 3NF e la BCNF#Preservare le dipendenze contenute in $F {+}$|preserva le dipendenze]] di $F$**;
- **$\rho$ ha un [[BD1_03 - La 3NF e la BCNF#Ricostruire le informazioni originali con un join|lossless join]]**.

Tale scomposizione può essere ottenuta in **tempo polinomiale** attraverso un **algoritmo**, che presenta i seguenti input e output:
- come **input**, uno schema di relazione $R$ e una [[BD1_03 - La 3NF e la BCNF#Trovare la copertura minimale di un insieme di dipendenze funzionali|copertura minimale]] dell'insieme $F$ di dipendenze funzionali definite su di esso;
- come **output**, una scomposizione $\rho$ di $R$.

Di seguito, lo **pseudocodice** dell'algoritmo:

```
S = ∅
ρ = ∅

for each A ∈ R, such that A is not involved in any dependency in F:
	S = S U A

if S ≠ ∅:
	R = R - S
	ρ = ρ U {S}

if there is a dependency in F that involves all the attributes in R:
	ρ = ρ ∪ {R}
else:
	for each X → A ∈ F:
		ρ = ρ U {XA}
```

È possibile, a questo punto, **dimostrare che l'algoritmo restituisce una scomposizione che rispetta tutte le tre condizioni** stabilite poco fa.

Partiamo dimostrando che **$\rho$ preserva le dipendenze contenute in $F$**. Consideriamo l'insieme $G=\bigcup_{i\,=\,1}^{k}\pi_{R_{i}}(F)$: dato che per ogni dipendenza funzionale $X\rightarrow A\,\in\,F$ si ha che $XA\,\in\,\rho$ (nel senso che $XA$ è uno dei sottoschemi di $\rho$), allora abbiamo che tale dipendenza di $F$ sarà contenuta anche in $G$, dunque possiamo dedurre che $F\subseteq G$ e che $F^{+}\subseteq G^{+}$. Invece, l'inclusione $G^{+}\subseteq F^{+}$ è vera a prescindere dato che, per definizione, $G\subseteq F^{+}$. Avendo dimostrato questa doppia inclusione, abbiamo dimostrato che $F\equiv G$, e dunque che $\rho$ preserva le dipendenze di $F$.

Passiamo, ora, al dimostrare che **tutti i sottoschemi di $\rho$ sono in 3NF**. [19 - slide 6]

Infine, per quanto riguarda la dimostrazione che **$\rho$ ha un lossless join**, si può dimostrare che, per avere questa caratteristica, è sufficiente aggiungere a $\rho$ un sottoschema contenente una delle chiavi di $R$.
___