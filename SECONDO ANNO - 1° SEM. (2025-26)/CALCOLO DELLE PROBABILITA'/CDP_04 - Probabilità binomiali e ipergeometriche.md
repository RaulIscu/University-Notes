In questo capitolo, andremo ad approfondire due particolari modelli probabilistici, che porteranno alla definizione di due tipi di probabilità particolari:
- le "**probabilità binomiali**";
- le "**probabilità ipergeometriche**".

## Probabilità binomiali

Consideriamo, su uno [[CDP_02 - Probabilità#Misure di probabilità|spazio finito di probabilità]], $n$ **[[CDP_03 - Correlazione e indipendenza tra eventi#Prove bernoulliane|prove bernoulliane]]** $E_{1},\,E_{2},\,\dots,\,E_{n}$, ossia un'insieme di eventi [[CDP_03 - Correlazione e indipendenza tra eventi#Indipendenza completa e prove bernoulliane|completamente indipendenti]] ed equiprobabili: ponendo dunque $\mathbb{P}(E_{i})=\theta$ per $i=1,\,2,\,\dots,\,n$, e considerando:
$$X_{i}=\begin{cases} 1 & \text{se si verifica }E_{i}\\0&\text{se si verifica }\overline{E_{i}}\end{cases}$$
si ha, per ogni $n$-upla $x=(x_{1},\,x_{2},\,\dots,\,x_{n})\in\{0,\,1\}^{n}$:
$$\mathbb{P}(\{X_{1}=x_{1},\,X_{2}=x_{2},\,\dots,\,X_{n}=x_{n}\})\,=\,\theta^{\sum_{i\,=\,1}^{n}x_{i}}(1-\theta)^{n-\sum_{i\,=\,1}^{n}x_{i}}$$
Seppur sembri un'equivalenza abbastanza complessa, è in realtà più semplice del previsto: ricordando che, lavorando con prove bernoulliane, si ha che $\mathbb{P}(E_{i})=\theta$, e avendo stabilito il significato di $X_{i}$, la $n$-upla $x$ rappresenta semplicemente una tupla di $0$ e $1$, dove la presenza dell'uno o dell'altro valore nell'$i$-esima posizione dipende dall'avvenimento o meno dell'evento $E_{i}$; dunque, la probabilità risultante è data dal prodotto tra $\theta^{r}$, dove $r$ è il numero di $1$ che compaiono all'interno di $x$ (ossia $\sum_{i\,=\,1}^{n}x_{i}$), e $(1-\theta)^{s}$, dove $s$ è il numero di $0$ che compaiono all'interno di $x$ (ossia $n-\sum_{i\,=\,1}^{n}x_{i}$).

Poniamo, a questo punto, $S_{n}=\sum_{i\,=\,1}^{n}X_{i}$, e consideriamo, per $k=0,\,1,\,\dots,\,n$ la probabilità dell'evento composto $\{S_{n}=k\}$. Possiamo scrivere:
$$\{S_{n}=k\}=\left\{ \sum_{i\,=\,1}^{n}X_{i}=k\right\}=\bigcup_{x\,\in\,\{0,\,1\}^{n}\,:\,\sum_{i\,=\,1}^{n}x_{i}\,=\,k}\{X_{i}=x_{1},\,X_{2}=x_{2},\,\dots,\,X_{n}=x_{n}\}$$
È chiaro che due eventi del tipo:
$$\{X_{1}=x'_{1},\,X_{2}=x'_{2},\,\dots,\,X_{n}=x'_{n}\}\,\,\,\,\,\,\,\,\,\,\{X_{1}=x''_{1},\,X_{2}=x''_{2},\,\dots,\,X_{n}=x''_{n}\}$$
sono incompatibili nel caso in cui $x'=(x'_{1},\,x'_{2},\,\dots,\,x'_{n})\neq x''=(x''_{1},\,x''_{2},\,\dots,\,x''_{n})$; inoltre, nel caso in cui
$$\sum_{i\,=\,1}^{n}x'_{i}=\sum_{i\,=\,1}^{n}x''_{i}=k$$
sappiamo che quegli stessi eventi risultano anche equiprobabili, ed entrambi di probabilità $\theta^{k}(1-\theta)^{n-k}$. Perciò, dal momento che la cardinalità dell'insieme $\left\{ x\in\{0,\,1\}^{n}:\sum_{i\,=\,1}^{n}x_{i}=k \right\}$ è uguale a $\binom{n}{k}$, potremmo scrivere per $k=0,\,1,\,\dots,\,n$:
$$\mathbb{P}(\{S_{n}=k\})\,=\,\sum_{x\,\in\,\{0,\,1\}^{n}\,:\,\sum_{i\,=\,1}^{n}x_{i}\,=\,k}\mathbb{P}(\{X_{1}=x_{1},\,X_{2}=x_{2},\,\dots,\,X_{n}=x_{n}\})\,=\,\binom{n}{k}\,\theta^{k}(1-\theta)^{n-k}$$
Una probabilità del genere definita sull'insieme $\{0,\,1,\,\dots,\,n\}$ prende il nome di "**probabilità binomiale** di parametri $n$ e $\theta$", e rappresenta una **[[CDP_02 - Probabilità#Misure di probabilità|misura di probabilità]] $\mathbf{P}$ definita sull'insieme delle parti di $\{0,\,1,\,\dots,\,n\}$** come segue:
$$\mathbf{P}:\mathcal{P}(\{0,\,1,\,\dots,\,n\})\rightarrow[0,\,1],\,\,\,I \mapsto \mathbf{P}(I):=\sum_{k\,\in\,I}p(k)$$
dove $p(k)=\binom{n}{k}\theta^{k}(1-\theta)^{n-k}$ e $k\,\in\,\{0,\,1,\,\dots,\,n\}$.

##### Esempi di probabilità binomiali

Per comprendere al meglio il concetto di probabilità binomiali, vediamo degli esempi concreti. Partiamo osservando un dado che viene lanciato $10$ volte: indicando con $S$ il numero di volte che si ottiene il valore $1$ dal lancio del dado, si vuole sapere la probabilità $\mathbb{P}(\{S=5\})$. Notiamo subito che l'insieme degli eventi formato dall'ottenimento di $1$ in ciascuno dei $10$ lanci del dado costituisce a tutti gli effetti $10$ prove bernoulliane, ossia $10$ eventi indipendenti tra loro di eguale probabilità, e sappiamo banalmente che tale probabilità è uguale a $\theta=\frac{1}{6}$. Dunque, sappiamo di trovarci in un modello di probabilità binomiale, e di conseguenza potremo applicare quanto detto per ottenere:
$$\mathbb{P}(\{S = 5\})\,=\,\binom{10}{5}\cdot\left( \frac{1}{6} \right)^{5}\cdot\left( \frac{5}{6} \right)^{5}\,=\,\binom{10}{5}\cdot \frac{5^{5}}{6^{10}}$$

Vediamo un altro esempio. In un treno, ciascun viaggiatore che occupa un posto in uno scompartimento "per fumatori" ha una probabilità del $70\%$ di essere effettivamente un fumatore; se lo scompartimento contiene $5$ posti prenotati, oltre a quello prenotato da me stesso, qual è la probabilità che io vi incontri meno di $3$ fumatori? Indicando con $S$ il numero di fumatori nei $5$ posti rimasti nello scompartimento, si sta insomma chiedendo la probabilità $\mathbb{P}(\{S<3\})$, che può intuitivamente essere scomposta nel modo seguente:
$$\mathbb{P}(\{S<3\})\,=\,\mathbb{P}(\{S=0\})+\mathbb{P}(\{S=1\})+\mathbb{P}(\{S=2\})$$
Notiamo, anche in questo caso, che l'insieme degli eventi formato dalla presenza di un fumatore in ciascuno dei $5$ posti dello scompartimento costituisce a un'insieme di $5$ prove bernoulliane, ossia di $5$ eventi indipendenti ed equiprobabili, con tale probabilità pari a $\theta=\frac{7}{10}$. Possiamo, dunque, applicare la formula delle probabilità binomiali per calcolare ciascuna delle tre probabilità necessarie per trovare quella richiesta:
$$\begin{align}\mathbb{P}(\{S<3\})\,&=\,\mathbb{P}(\{S=0\})+\mathbb{P}(\{S=1\})+\mathbb{P}(\{S=2\})\\&=\binom{5}{0}\left( \frac{7}{10} \right)^{0}\left( \frac{3}{10} \right)^{5}\,+\,\binom{5}{1}\left( \frac{7}{10} \right)^{1}\left( \frac{3}{10} \right)^{4}\,+\,\binom{5}{2}\left( \frac{7}{10} \right)^{2}\left( \frac{3}{10} \right)^{3}\end{align}$$

Passiamo, ora, a un ultimo esempio. Un testo, contenente precisamente $20$ errori di stampa, viene sottoposto a due diversi correttori: ciascun errore contenuto nel testo viene individuato da ciascun correttore con una probabilità $p=0.6$, e indipendentemente da quello che accade per gli altri errori; al tempo stesso, i due correttori lavorano indipendentemente uno dall'altro. Si vuole sapere la probabilità che il numero degli errori individuati da almeno uno dei correttori sia superiore a $15$ (si precisa, dunque, che non ci interessa se un errore viene individuato da uno dei due correttori, dall'altro, o da entrambi, ma solo che almeno uno dei due lo individui). Sfruttando l'indipendenza tra i due correttori, e ponendo $A=\{\text{l'errore viene individuato dal 1° correttore}\}$ e $B=\{\text{l'errore viene individuato dal 2° correttore}\}$, possiamo affermare che ciascun errore viene individuato da almeno uno dei due correttori con una probabilità $\theta$ pari a:
$$\begin{align} \theta\,&=\,\mathbb{P}(A\cup B)\\&=\,\mathbb{P}(A)+\mathbb{P}(B) -\mathbb{P}(A\cap B)\\&=\,\mathbb{P}(A)+\mathbb{P}(B)-\mathbb{P}(A)\mathbb{P}(B)\\&=\,2\,\mathbb{P}(A)-[\mathbb{P}(A)]^{2}\\&=\,2p-p^{2}\\&=\,1.2-0.36=0.84\end{align}$$
Dunque, avendo trovato la probabilità $\theta=0.84=\frac{21}{25}$ di una singola delle $20$ prove bernoulliane che stiamo considerando, possiamo procedere ad applicare la solita formula:
$$\mathbb{P}(\{S>15\})=\sum_{k\,=\,16}^{20}\binom{20}{k}\left( \frac{21}{25} \right)^{k}\left( \frac{4}{25} \right)^{20-k}$$
___
##### Estrazioni casuali da un'urna con reinserimento

Illustriamo, in questo paragrafo, un altro esempio tipico di situazione in cui si incontra uno schema di [[CDP_03 - Correlazione e indipendenza tra eventi#Prove bernoulliane|prove bernoulliane]]. Pensiamo ad una popolazione composta da $M$ oggetti, indicati come $c_{1},\,c_{2},\,\dots,\,c_{M}$, di cui $m_{1}$ oggetti sono di tipo $A$ e $m_{2}=M-m_{1}$ di tipo $B$; supponiamo, ad esempio, di numerare i vari oggetti in modo che $c_{1},\,c_{2},\,\dots,\,c_{m_{1}}$ siano di tipo $A$, e che $c_{m_{1}+1},\,c_{m_{1}+2},\,\dots,\,c_{M}$ siano di tipo $B$ (per semplicità, possiamo pensare a un'urna contenente $M$ palline, dove $m_{1}$ palline sono rosse e numerate $1,\,2,\,\dots,\,m_{1}$, e $m_{2}=M-m_{1}$ palline sono blu e numerate $m_{1}+1,\,m_{1}+2,\,\dots,\,M$).

Ora, stabilito il contesto in cui ci troviamo, supponiamo di eseguire **$n$ estrazioni casuali con reinserimento** da tale popolazione di oggetti, ossia $n$ estrazioni successive dove, dopo ogni estrazione, l'oggetto estratto viene reinserito nella popolazione, e banalmente dove ciascun oggetto ha ogni volta la stessa probabilità (pari a $\frac{1}{M}$) di essere estratto, sia esso di tipo $A$ o di tipo $B$. Lo spazio campione $\Omega$, in tale esperimento, può essere identificato come l'insieme:
$$\Omega=\{1,\,2,\,\dots,\,M\}^{n}=\{(j_{1},\,j_{2},\,\dots,\,j_{n}):j_{k}\in\{1,\,2,\,\dots,\,M\}\text{ per ogni }k=1,\,2,\,\dots,\,n\}$$
ossia l'insieme costituito dalle $n$-uple ordinate di elementi in $\{1,\,2,\,\dots,\,M\}$. L'insieme $\Omega$ ha dunque cardinalità $M^{n}$. In tale spazio campione, consideriamo per $i=1,\,2,\,\dots,\,n$ gli eventi del tipo:
$$A_{i}=\{\text{l'oggetto estratto nell'}i\text{-esima estrazione è di tipo A}\}$$
Possiamo dimostrare che **gli eventi $A_{i}$ costituiscono delle prove bernoulliane con $\mathbb{P}(A_{i})=\frac{m_{1}}{M}$**. Per dimostrare ciò, dobbiamo dimostrare che i vari eventi $A_{i}$ sono completamente indipendenti ed equiprobabili. Partiamo deducendo, dalla condizione che le estrazioni siano casuali e con reinserimento, che ciascuno degli eventi elementari $(j_{1},\,j_{2},\,\dots,\,j_{n})\in\Omega$ ha la stessa probabilità $\frac{1}{M^{n}}$; inoltre, in virtù della numerazione effettuata a inizio esempio, possiamo affermare che:
$$\begin{align} A_{i}&=\{(j_{1},\,j_{2},\,\dots,\,j_{n})\in \Omega\,:\,1\le j_{i}\le m_{1}\}\\&=\overbrace{\{1,\,2,\,\dots,\,M\}\times\,\dots\,\times\{1,\,2,\,\dots,\,M\}}^{i\,-\,1\,\text{volte}}\times\{1,\,2,\,\dots,\,m_{1}\}\times\overbrace{\{1,\,2,\,\dots,\,M\}\times \,\dots\,\times\{1,\,2,\,\dots,\,M\}}^{n\,-\,i\,\text{volte}} \end{align}$$
E, in modo analogo, possiamo esprimere il generico evento complementare $\overline{A_{i}}$ come:
$$\begin{align} \overline{A_{i}}&=\{(j_{1},\,j_{2},\,\dots,\,j_{n})\in \Omega\,:\,m_{1}+1\le j_{i}\le M\}\\&=\overbrace{\{1,\,2,\,\dots,\,M\}\times\,\dots\,\times\{1,\,2,\,\dots,\,M\}}^{i\,-\,1\,\text{volte}}\times\{m_{1}+1,\,m_{1}+2,\,\dots,\,M\}\times\overbrace{\{1,\,2,\,\dots,\,M\}\times \,\dots\,\times\{1,\,2,\,\dots,\,M\}}^{n\,-\,i\,\text{volte}} \end{align}$$
Dunque, considerando per $1\le i\le n$ la quantità $X_{i}$ definita come nella [[CDP_04 - Probabilità binomiali e ipergeometriche#Probabilità binomiali|definizione iniziale di probabilità binomiali]], ossia:
$$X_{i}=\begin{cases}1&\text{se si verifica }A_{i}\\0&\text{se si verifica }\overline{A_{i}}\end{cases}$$
si ha che:
$$\begin{align}\mathbb{P}(X_{i}=1)=\mathbb{P}(A_{i})&=\frac{|\{(j_{1},\,j_{2},\,\dots,\,j_{n})\in \Omega\,:\,1\le j_{i}\le m_{1}\}|}{M^{n}}\\&=\frac{m_{1}\cdot M^{n-1}}{M^{n}}\end{align}$$
e analogamente che:
$$\mathbb{P}(\{X_{1}=x_{1},\,X_{2}=x_{2},\,\dots,\,X_{n}=x_{n}\})=\frac{m_{1}^{\sum_{i\,=\,1}^{n}x_{i}}m_{2}^{n-\sum_{i\,=\,1}^{n}x_{i}}}{M^{n}}=\left( \frac{m_{1}}{M} \right)^{\sum_{i\,=\,1}^{n}x_{i}}\left( \frac{m_{2}}{M} \right)^{n-\sum_{i\,=\,1}^{n}s_{i}}$$
Mettendo insieme le due relazioni, si ottiene che per tutti gli eventi $\tilde{A_{i}}\in\mathcal{P}_{i}=\{A_{i},\,\overline{A_{i}}\}=\{\{X_{i}=1\},\,\{X_{i}=0\}\}$ si ha:
$$\mathbb{P}(\tilde{A_{1}}\cap \tilde{A_{2}}\cap\,\dots\,\cap \tilde{A_{n}})\,=\,\mathbb{P}(\tilde{A_{1}})\cdot\mathbb{P}(\tilde{A_{2}})\cdot\,\dots\,\cdot\mathbb{P}(\tilde{A_{n}})$$
Tale equivalenza corrisponde alla condizione che definisce l'[[CDP_03 - Correlazione e indipendenza tra eventi#Indipendenza completa e prove bernoulliane|indipendenza completa]], e avendo dimostrato che i vari eventi $A_{i}$ sono completamente indipendenti e anche equiprobabili, si è dimostrato che costituiscono delle prove bernoulliane.

Consideriamo, ora:
$$S_{n}=\sum_{i\,=\,1}^{n}X_{i}$$
dove $S_{n}$ rappresenta il numero di elementi di tipo $A$ estratti nell'estrazione casuale con reinserimento di $n$ elementi considerata. Possiamo concludere affermando che:
$$\mathbb{P}(\{S_{n}=k\})=\binom{n}{k}\left( \frac{m_{1}}{M} \right)^{k}\left( \frac{m_{2}}{M} \right)^{n-k}$$
___
## Probabilità ipergeometriche



[pag. 74/78]
___