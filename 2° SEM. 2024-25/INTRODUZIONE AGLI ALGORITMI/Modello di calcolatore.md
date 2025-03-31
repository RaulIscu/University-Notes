Per poter approfondire al meglio il problema del costo computazionale degli algoritmi, è necessario definire un modello astratto di **calcolatore**. È possibile immaginare tale strumento come costituito da **4 tipi di unità funzionali**:
- un **processore**, o ***CPU*** (*Central Processing Unit*);
- una **memoria centrale**, o ***RAM*** (*Random Access Memory*);
- una **memoria secondaria**, detta anche memoria di massa;
- dei **dispositivi di *input* e di *output*** (come tastiere, schermi, stampanti, ecc. ecc.).
___
### La RAM

Concentriamoci, in particolare, sulla ***RAM***. Essa può essere vista come una lunga sequenza di componenti elementari, ognuna delle quali contenente un'unità di informazione, il ***bit*** (o *binary digit*); ciascuna di queste componenti viene detta "**cella di memoria**".

Un gruppo di 8 bit viene anche detto "***byte***"; questi sono, a loro volta, raggruppati in strutture dette "**registri di memoria**" o "**parole di memoria**", caratterizzate dal fatto che su di esse la *CPU* è in grado di operare con un'unica operazione. Nei calcolatori moderni, una parola di memoria può essere costituita da 4 *bytes* (in un calcolatore a 32 *bit*) o 8 *bytes* (in un calcolatore a 64 *bit*).

Una *RAM* presenta anche i seguenti aspetti importanti:
- ciascuna parola di memoria ha un indirizzo;
- gli indirizzi corrispondono alla posizione dei *bytes* nella sequenza;
- gli indirizzi sono numeri interi e non sono memorizzati da nessuna parte, ma sono determinati dall’ordinamento consecutivo delle celle stesse;
- solo i *bytes* e non i singoli *bit* sono indirizzabili (cioè accessibili da parte della *CPU*).

Nella *RAM*, **il tempo di accesso ad una qualunque parola di memoria è sempre lo stesso**, indipendentemente dalla posizione (e quindi dall’indirizzo) della parola. Le operazioni che il processore può effettuare su una parola di memoria sono la **lettura**, che preleva il contenuto corrente della parola, e la **scrittura**, che memorizza un contenuto nella parola sovrascrivendo quello precedente. Il tempo di accesso, molto ridotto, oggi è dell’ordine dei nanosecondi (10⁻⁹ secondi).

Gli indirizzi dei *bytes* sono numeri interi, quindi possono essere codificati in binario. Il numero di *bytes* esistenti (e quindi le dimensioni della RAM) determina il numero minimo di *bit* necessari a rappresentare gli indirizzi per poter accedere alle celle stesse; viceversa, il numero di *bits* utilizzati per rappresentare gli indirizzi di memoria determina il numero massimo di *bytes* indirizzabili. Questo numero viene chiamato "**spazio di indirizzamento**". Ad esempio, con indirizzi a 32 *bit*, non si possono indirizzare più di 2³² (circa quattro miliardi) celle di memoria, nemmeno se il calcolatore ne contenesse molte di più.

La parola di memoria è l’unità massima sulla quale è possibile operare mediante un’unica operazione (o "**istruzione**"). Per eseguire un’operazione si deve specificare l’indirizzo della parola di memoria su cui si vuole operare, che coincide con l’indirizzo del primo *byte* facente parte della parola stessa. Di conseguenza gli indirizzi delle parole di memoria sono numeri interi multipli di 4 o di 8, a seconda dei casi; in genere, gli indirizzi dei *bytes* intermedi non si possono usare. Perciò, in queste situazioni, di norma il tentativo di accedere a una cella di memoria il cui indirizzo non è un multiplo di 4 o di 8 produce un errore (ad esempio, “*illegal memory access*”), che causa l’immediata terminazione del programma in esecuzione. 

La *RAM* è piuttosto costosa, e perde il suo contenuto quando viene a mancare l’alimentazione elettrica: questa caratteristica si indica col termine "**volatilità**".
___
### La memoria di massa

Per superare il problema della volatilità, si deve fare ricorso anche a un tipo diverso di memoria. È qui che entra in gioco la **memoria secondaria**. Essa ha le seguenti caratteristiche:
- conserva il suo contenuto anche in assenza di alimentazione elettrica;
- è molto più lenta della memoria centrale;
- è molto più abbondante della memoria centrale (arriva anche ai *terabyte*, composti da 10¹² *bytes*);
- è meno costosa della memoria centrale.

