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

___