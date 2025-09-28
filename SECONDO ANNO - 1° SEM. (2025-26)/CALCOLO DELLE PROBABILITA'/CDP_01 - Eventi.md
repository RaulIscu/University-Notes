https://elearning.uniroma1.it/pluginfile.php/1536989/mod_folder/content/0/APPUNTI-SN-settembre-2024.pdf?forcedownload=1
## Cos'è un evento?

In questo corso, si approfondirà il **calcolo delle probabilità**, una branca della matematica che, come suggerisce il nome, studia la probabilità che avvenga un determinato "**evento**". La definizione di "evento" è particolarmente generica e permissiva: sostanzialmente, possiamo considerare come tale un qualcosa che ha una certa probabilità di avvenire, un possibile risultato di un'azione.

Pensiamo, ad esempio, di osservare il lancio di due dadi, e di indicare con $X_{1}$ il punteggio ottenuto dal primo dado e con $X_{2}$ quello ottenuto dal secondo. Eseguendo questo "esperimento", si potranno ottenere diversi risultati, come:
- $A$, in cui il punteggio del primo dado è minore o uguale al punteggio del secondo ($X_{1} \le X_{2}$);
- $B$, in cui la somma dei punteggi ottenuti è pari ($X_{1} + X_{2} \text{\, è pari}$);
- $C$, in cui il punteggio ottenuto dal primo dado è strettamente maggiore di 3 ($X_{1} > 3$);
- $D$, in cui il punteggio ottenuto dal primo dado è 2 e il punteggio ottenuto dal secondo è 5 ($X_{1} = 2,\, X_{2} = 5$).

Ciascuna di questa situazione è un singolo **evento**: dunque, possiamo vedere un evento anche come una **proposizione logica**, che risulta essere vera se l'evento si verifica e falsa se l'evento non si verifica.

Per il momento, possiamo indicare con il simbolo $\mathcal{E}$ la "**famiglia**" dei possibili eventi distinti in un esperimento del genere. Come è facile notare, la famiglia costituita dagli eventi elencati poco fa è una **famiglia finita**; analogamente, per ora ci si limiterà a trattare esempi con famiglie di eventi finite, ma è possibile anche avere un esperimento che generi una famiglia non finita.
___
## Operazioni logiche sugli eventi

Avendo definito un evento anche come proposizione logica, risulta naturale introdurre all'interno di una famiglia di eventi anche le **operazioni logiche**, in particolare:
- la **somma logica**, detta anche **OR** e indicata con il simbolo $\lor$;
- il **prodotto logico**, detto anche **AND** e indicato con il simbolo $\land$;
- la **negazione**, detta anche **NOT** e indicata con il simbolo $\lnot$.

Dunque, siano $E_{1}$ ed $E_{2}$ due eventi della famiglia di eventi $\mathcal{E}$, si ha che la somma logica $E_{1} \lor E_{2}$ corrisponde all'evento:
$$\{\text{si è verificato almeno uno dei due eventi }E_{1}\text{ ed }E_{2}\}$$
Invece, il prodotto logico $E_{1}\land E_{2}$ corrisponde all'evento:
$$\{\text{si sono verificati entrambi gli eventi }E_{1}\text{ ed }E_{2}\}$$
Infine, la negazione $\lnot E_{1}$ corrisponde all'evento:
$$\{\text{non si è verificato l'evento }E_{1}\}$$
##### Eventi elementari e composti

> Un evento $E\in\mathcal{E}$ si dice "**composto**" se esistono almeno due eventi $E_{1},\,E_{2}\in\mathcal{E}$ tali per cui:
> $$E = E_{1}\lor E_{2}\,\,\,\,\,\,\,\,\,\,\text{con }E\neq E_{1},\,E\neq E_{2}$$
> Qualsiasi evento non sia composto viene detto "**semplice**", o "**elementare**".

Ad esempio, supponendo di lanciare un dado a sei facce, l'evento $E=\{X_{1}>3\}$ è un evento composto, dato che in tale esperimento gli eventi elementari sono:
$$\{X_{1}=1\}, \{X_{1}=2\},\,\dots,\,\{X_{1}=6\}$$
e l'evento $E$ può essere riscritto come:
$$E=\{X_{1}>3\}=\{X_{1}=4\}\lor\{X_{1}=5\}\lor\{X_{1}=6\}$$
Supponendo, in un altro esempio, di lanciare due dadi a sei facce, si ottiene stavolta che gli eventi elementari sono tutti gli eventi del tipo:
$$\{X_{1}=n,\,X_{2}=m\}\,\,\,\,\,\,\,\,\,\,\text{con n} = 1,\,2,\,\dots,\,6\text{ \,e\, m}=1,\,2,\,\dots,\,6$$
ossia eventi in cui entrambi i dadi assumono un valore ben preciso; in questo contesto, invece, un evento $E$ del tipo $\{X_{1}=n\}$ risulta essere un evento composto, dato che può essere riscritto come:
$$E=\{X_{1}=n\}=\bigvee_{k\,=\,1}^{6}\,\{X_{1}=n,\,X_{2}=k\}$$
> L'insieme $\Omega = \{\omega_{1},\,\omega_{2},\,\dots,\,\omega_{k}\}$, che contiene tutti gli eventi elementari di un esperimento, viene detto "**spazio campione**" per tale esperimento.
___
##### Famiglia delle parti

Avendo uno spazio campione $\Omega$, indichiamo con il simbolo $\mathcal{P}(\Omega)$ la "**famiglia delle parti**" di $\Omega$, ossia la famiglia di **tutti i possibili sottoinsiemi** di $\Omega$, e per ogni $E\in \mathcal{P}(\Omega)$ si indica con il simbolo $|\,E\,|$ la "**cardinalità**" di $E$, ossia il numero di elementi contenuti al suo interno. 
___