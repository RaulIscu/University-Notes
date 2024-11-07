In informatica, qualsiasi dato viene rappresentato usando i ***bit***, componenti elementari rappresentati da cifre tra ***0*** e ***1***.

Generalmente, un numero è espresso in “base 10”, o in un sistema decimale. Ad esempio: 
> $$5374₁₀ = (5 × 10^3) + (3 × 10^2) + (7 × 10^1) + (4 × 10^0)$$

Nell’informatica e nell’elettronica, invece, si utilizza il **sistema binario**, dunque in "base 2"; il meccanismo rimane lo stesso, con la differenza dell’utilizzo esclusivo di 1 e 0, ad esempio: 
> $$1101₂ = (1 × 2^3) + (1 × 2^2) + (0 × 2^1) + (1 × 2^0) = 13₁₀$$

Per convertire un numero binario in numero decimale, si moltiplicano le singole cifre per *2ⁱ*, dove i rappresenta l’*i*-esima posizione della cifra considerata all’interno del numero, e si sommano i risultati. Viceversa, per convertire un numero decimale in numero binario, si possono usare due metodi:
- si trova la massima potenza con base 2 che rientra nel numero considerato e la si sottrae al numero iniziale (rappresenterà un 1 nella posizione corrispondente all’apice della potenza), e si ripete il procedimento fino ad arrivare a 0;
- si divide a oltranza il numero considerato per 2, e si segnano via via i resti di queste divisioni (che saranno o 0 o 1) da destra verso sinistra.

Operando in un sistema binario, è utile nonché molto importante avere dimestichezza con le varie potenze di base 2. Tra le più importanti, troviamo **2⁸ = 256**, che rappresenta un valore degno di nota in quanto le sequenze di *bit* vengono spesso spezzate e considerate separatamente per semplificare vari processi, e in genere tali sequenze vengono spezzate in ***byte*** composti da 8 bit ciascuno, che possono quindi rappresentare 256 combinazioni diverse. Un’altra potenza utile è sicuramente  **2¹⁰ = 1024 ≃10³**, da tenere a mente per calcolare più efficientemente potenze di base 2 con apice elevato.

Analogamente ai numeri decimali, anche i numeri binari consentono di operare tra di loro con le operazioni fondamentali. Innanzitutto, affrontiamo l’addizione: è utile, prima di farlo, chiarificare alcune regole fondamentali, che possiamo definire come “tavole di verità”:
$$0 + 0 = 0$$ 
$$0 + 1 = 1$$
$$1 + 1 = 10 $$   

Stabilito ciò, possiamo affrontare le addizioni tra numeri binari, che in genere si svolgono in colonna. Consideriamo un esempio:
![[add_binaria.png]]
Come si nota subito, l’applicazione della terza tavola di verità, a livello base, implica il porre (da destra) la prima cifra del risultato ottenuto come risultato della colonna in questione, e la seconda cifra come riporto della colonna seguente. Ciò vale anche per somme di più 1, come si può riscontrare nella seconda colonna da sinistra dell’operazione: 1 + 1 + 1 = 3, ossia 11₂, dunque si scrive 1 come risultato della colonna in questione e 1 come riporto della colonna seguente. Quando i riporti diventano a più cifre, si scrive una singola cifra del riporto per colonna, andando sempre da destra verso sinistra.

[PASSAGGIO AL COMPLEMENTO]
[SOTTRAZIONE TRA BINARI]