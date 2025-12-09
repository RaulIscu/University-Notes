Riprendiamo l'esempio di database presentato alla fine del capitolo sul [[BD1_01 - Modello relazionale#Come formulare un "buon" schema di database?|modello relazionale]], e in particolare consideriamo la versione finale, ossia lo schema di database contenente i seguenti 4 schemi di relazione:
$$\begin{align} &\text{Student(Matr, Name, Surname, TC, Birth, City)} \\ &\text{Course(C\#, Title, Prof)} \\ &\text{Exam(Matr, C\#, Date, Grade)} \\ &\text{Municipality(City, Prov)} \end{align}$$
Come è facilmente intuibile, ogni matricola $\text{Matr}$ identifica univocamente un singolo studente: ciò significa che a ciascuna matricola potrà essere associato un solo nome, un solo cognome, un solo tax code, ecc. ecc. Possiamo, così, dedurre che per avere un'istanza legale di $\text{Student}$ essa dovrà rispettare la seguente [[BD1_02 - Dipendenze funzionali#Cos'è una dipendenza funzionale?|dipendenza funzionale]]:
$$\text{Matr}\rightarrow \text{Matr, Name, Surname, TC, Birth, City}$$
Seguendo lo stesso ragionamento, sappiamo che anche l'attributo $\text{TC}$ è unico per ogni studente, e dunque in un'istanza legale deve valere anche la seguente dipendenza funzionale:
$$\text{TC}\rightarrow \text{Matr, Name, Surname, TC, Birth, City}$$
Possiamo affermare di conseguenza che **$\text{Matr}$ e $TC$ sono chiavi dello schema di relazione $\text{Student}$**. Lo stesso non vale per gli altri attributi: possiamo avere due studenti con stesso cognome e diverso nome, due studenti nati nello stesso giorno, provenienti dalla stessa città, e così via. Formalmente, ciò implica che dipendenze funzionali come:
$$\begin{align} &\text{Surname}\rightarrow \text{Name} \\ &\text{Name}\rightarrow \text{Surname} \\ &\text{Surname}\rightarrow \text{Birth} \end{align}$$
non devono essere necessariamente soddisfatte da un'istanza legale di $\text{Student}$. Da queste considerazioni si conclude che **l'unica dipendenza funzionale non [[BD1_02 - Dipendenze funzionali#Dipendenze funzionali triviali|triviale]] che deve essere soddisfatta da un'istanza legale di $\text{Student}$ è una dipendenza funzionale del tipo:**
$$K\rightarrow X$$
dove $K$ contiene una **chiave** della relazione (nel nostro esempio, $\text{Matr}$ o $\text{TC}$). Un discorso simile può essere applicato anche agli altri schemi di relazione del database, ottenendo che $\text{C\#}$ è la chiave di $\text{Course}$, $\text{Matr, C\#}$ è la chiave di $\text{Exam}$ e $\text{City}$ è la chiave di $\text{Municipality}$, e anche per tutti questi schemi vale la stessa regola che abbiamo appena esplicitato. Dunque, generalizzando:

> Le uniche dipendenze funzionali non triviali che devono necessariamente essere soddisfatte da una qualsiasi istanza di relazione legale sono quelle del tipo:
> $$K\rightarrow X$$
> dove $K$ contiene una chiave.



[09 - slide 13]