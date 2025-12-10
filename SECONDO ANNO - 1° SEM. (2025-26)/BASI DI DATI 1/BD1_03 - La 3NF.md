## Definizione di 3NF

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



[10 - slide 4]
___