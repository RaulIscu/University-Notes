## Cos'è il sistema esadecimale?

Spesso, lavorando con dei [[Sistema binario#Cos'è il sistema binario?|numeri binari]], risulta facile incappare in errori o semplicemente faticare a svolgere tali operazioni: quando si cominciano a utilizzare numeri abbastanza grandi, operare correttamente su delle lunghe stringhe di bit non è un lavoro facile. Per ovviare a questo problema, si è creato un nuovo sistema numerico, il **sistema esadecimale**. Come suggerisce il nome, si tratta di un sistema **in base 16**, in cui ogni cifra rappresenta una stringa di **4 bit** (detta "**nibble**") che può quindi assumere un valore compreso tra $0$ e $15$. Le cifre del sistema esadecimale sono i classici numeri da $0$ a $9$, ma anche le lettere alfabetiche da $A$ a $F$. Si può facilmente visualizzare questa lista di caratteri e i loro rispettivi valori nella seguente tabella:

![[hex_table.png]]

Per esempio, il numero $749_{10}$ può essere rappresentato nei seguenti modi:
$$749_{10} = 1011101101_{2} = 2ED_{16}$$
Si nota, quindi, immediatamente quanto sia molto più conveniente utilizzare un sistema esadecimale per rappresentare numeri molto grandi. È utile, a questo punto, ricordare che l'appartenenza di una rappresentazione numerica al sistema esadecimale è stata finora indicata banalmente con il pedice "$_{16}$", ma che in realtà essa venga più spesso indicata preponendo all'esadecimale considerato il prefisso "**$0x$**": ad esempio, il risultato della conversione appena svolta viene convenzionalmente scritto come "$0x2ED$".
___
## Addizioni tra esadecimali

Per effettuare un'**addizione tra esadecimali**, si opererà in maniera analoga all'[[Sistema binario#Addizioni tra binari|addizione tra binari]], ovviamente fatta eccezione per alcune particolarità. Supponiamo, ad esempio, di voler sommare i due numeri esadecimali $0x3A09$ e $0x1B17$. L'operazione svolta avrà il seguente aspetto:

![[hex_addition.png]]

Per comprendere come avvenga l'addizione, analizziamola passo per passo. Come per qualsiasi addizione in colonna, si parte dalle cifre che si trovano più a destra nei numeri considerati: in questo caso, $9 + 7 = 16_{10} = 0x10$, quindi si appunta lo $0$ nella colonna corrispondente e si porta $1$ come riporto alla colonna successiva; nella seconda colonna, si ha $1 + 1 = 2$, quindi si appunta $2$ nella colonna corrispondente e si va alla successiva senza alcun riporto; nella terza colonna, si ha $A + B = 21_{10} = 0x15$, quindi si appunta $5$ nella colonna corrispondente e si porta $1$ come riporto alla colonna successiva; infine, nella quarta colonna, si ha $1 + 3 + 1 = 5$, quindi si appunta $5$ nella colonna corrispondente. Si ottiene, così, che $0x3A09 + 0x1B17 = 0x5520$.
___