Finora, la trattazione si è concentrata su [[CDP_02 - Probabilità#Misure di probabilità|spazi di probabilità]] con un numero finito di eventi elementari, o su [[CDP_05 - Variabili aleatorie#Cos'è una variabile aleatoria?|variabili aleatorie]] che possono assumere soltanto un numero finito di valori possibili. Tali limitazioni, però, ci impediscono di analizzare correttamente tutti i casi di possibile interesse, perciò risulta utile, a questo punto, fornire delle **definizioni definitive e generali di "spazio di probabilità" e di "variabile aleatoria"**.

## Spazi di probabilità generali

Fino a questo punto, abbiamo assunto che a ogni elemento della famiglia delle parti dello spazio campione $\Omega$, ossia $\mathcal{P}(\Omega)$, venisse assegnata una qualche probabilità; in altre parole, indicando con $\mathcal{F}$ la **famiglia dei sottoinsiemi di $\Omega$ ai quali viene attribuita una probabilità**, abbiamo assunto che $\mathcal{F}=\mathcal{P}(\Omega)$. In casi più generici, però, sarebbe più corretto riferirsi alla relazione $\mathcal{F}\subseteq\mathcal{P}(\Omega)$, ossia affermare che **la famiglia $\mathcal{F}$ può anche essere strettamente contenuta in $\mathcal{P}(\Omega)$**; ciò vuol dire che, all'interno di $\mathcal{F}$, troveremo solamente i veri e propri "eventi" dell'esperimento, ossia solamente i sottoinsiemi di $\Omega$ a cui è assegnata una qualche probabilità di accadere.

Al tempo stesso, è ragionevole richiedere che, dati due arbitrari eventi $A$ e $B$ (cioè due sottoinsiemi di $\Omega$, entrambi appartenenti a $\mathcal{F}$), anche $A\cup B$, $A\cap B$, $\overline{A}$ e $\overline{B}$ siano degli eventi. A questo proposito, sappiamo per certo che anche $\Omega$ (ossia l'evento certo) e $\emptyset$ (ossia l'evento impossibile) apparterranno a $\mathcal{F}$. Le proprietà appena elencate, in particolare, ci fanno intendere che **la famiglia $\mathcal{F}$ costituisce un'[[CDP_03 - Correlazione e indipendenza tra eventi#Algebre generate da famiglie di eventi|algebra]]**.

Ora, cerchiamo di estendere le considerazioni fatte finora a casi in cui **lo spazio campione $\Omega$ è un insieme infinito**, situazione che si presenta necessariamente quando si devono considerare infiniti eventi diversi, o in cui l'insieme dei valori assumibili da determinate variabili aleatorie è infinito. Innanzitutto, possiamo affermare che anche nel caso generale **uno spazio di probabilità è definito come una terna $(\Omega,\,\mathcal{F},\,\mathbb{P})$**, dove:
- $\Omega$ è un arbitrario spazio di punti;
- $\mathcal{F}$ è un'algebra di sottoinsiemi di $\Omega$;
- $\mathbb{P}$ è una funzione di tipo $\mathcal{F}:[0,\,1]$, per cui vale la [[CDP_02 - Probabilità#Proprietà delle probabilità|proprietà di additività]] e tale per cui $\mathbb{P}(\Omega)=1$.

Supponendo, però, che $\Omega$ sia un insieme infinito, ci sono delle precisazioni ulteriori da fare. Consideriamo una successione di eventi $E_{1},\,E_{2},\,\dots$, cioè di elementi di $\mathcal{F}$: sappiamo che, **per un numero arbitrario finito di eventi, vale che la loro unione è ancora un evento, ma ciò non è garantito per un numero infinito di eventi**; in altri termini, non è detto che l'unione $\bigcup_{j\,=\,1}^{\infty}E_{j}$ sia anch'essa un elemento di $\mathcal{F}$. Dunque, se $\mathcal{F}$, oltre a essere un'algebra, soddisfa anche tale condizione, allora chiameremo $\mathcal{F}$ una "$\sigma$-algebra".

> Una famiglia $\mathcal{F}$ di sottoinsiemi di $\Omega$ è detta "**$\sigma$-algebra**" se sono verificate le seguenti condizioni:
> 1. $\Omega\in\mathcal{F}$;
> 2. $E\in\mathcal{F}\,\Rightarrow\,\overline{E}\in\mathcal{F}$;
> 3. $E_{1},\,E_{2},\,\dots\,\in\mathcal{F}\,\Rightarrow\,\bigcup_{j\,=\,1}^{\infty}E_{j}\in\mathcal{F}$.

In modo analogo a come avremmo fatto per un'algebra "normale", possiamo dimostrare anche che, applicando le proprietà $2$ e $3$, insieme alla [[CDP_01 - Eventi#Proprietà relative alle operazioni insiemistiche|legge di De Morgan]], vale:
$$E_{1},\,E_{2},\,\dots\,\in\mathcal{F}\,\Rightarrow\,\bigcap_{j\,=\,1}^{\infty}E_{j}\in\mathcal{F}$$

A questo punto, considerando una successione di eventi $E_{1},\,E_{2},\,\dots$ all'interno di una $\sigma$-algebra $\mathcal{F}$, supponendo che tali eventi siano disgiunti a due a due, ci chiediamo se valga anche la seguente generalizzazione della proprietà di additività:
$$\mathbb{P}\left( \bigcup_{j\,=\,1}^{\infty}E_{j} \right)=\sum_{j\,=\,1}^{\infty}\mathbb{P}(E_{j})$$
dato che essa non è automaticamente implicata dalla proprietà di additività finita. Possiamo, a questo proposito, definire una nuova proprietà per la funzione $\mathbb{P}$, ossia la "$\sigma$-additività".

>Sia $\mathbb{P}:\mathcal{F}\to[0,\,1]$ una funzione di insieme; tale funzione viene detta "**$\sigma$-additiva**", o "**numerabilmente additiva**", se per qualunque successione $E_{1},\,E_{2},\,\dots$ di eventi incompatibili a due a due risulta che:
>$$\mathbb{P}\left( \bigcup_{j\,=\,1}^{\infty}E_{j} \right)=\sum_{j\,=\,1}^{\infty}\mathbb{P}(E_{j})$$

D'ora in poi, a meno di altre indicazioni, quando si parlerà di misure di probabilità le si considererà sempre come $\sigma$-additive. A questo punto, siamo pronti per fornire una **definizione generale e definitiva di "spazio di probabilità"**.

> Uno **spazio di probabilità** è una terna $(\Omega,\,\mathcal{F},\,\mathbb{P})$ dove:
> 1. $\Omega$ è un arbitrario spazio di punti;
> 2. $\mathcal{F}\subseteq\mathcal{P}(\Omega)$ è una $\sigma$-algebra di sottoinsiemi di $\Omega$;
> 3. $\mathbb{P}:\mathcal{F}\to[0,\,1]$ è una misura di probabilità, cioè una funzione di insieme $\sigma$-additiva tale per cui $\mathbb{P}(\Omega)=1$.

##### Spazi di probabilità numerabili

Considerando uno spazio di probabilità $(\Omega,\,\mathcal{F},\,\mathbb{P})$, dove $\Omega$ è un **insieme infinito numerabile** $\{\omega_{i};\,i=1,\,2,\,\dots\}$ e dove $\mathcal{F}=\mathcal{P}(\Omega)$, notiamo che, in maniera perfettamente analoga a come succede per gli spazi di probabilità finiti, **la probabilità $\mathbb{P}(E)$ di un qualsiasi evento è univocamente determinata una volta fissate le probabilità $\mathbb{P}(\{\omega_{i}\})$**. Infatti, anche in questo caso, vale che:
$$\mathbb{P}(E)=\sum_{i:\,\omega_{i}\,\in\,E}\mathbb{P}(\{\omega_{i}\})$$
Ovviamente, perché ciò sia valido, è necessario anche che $\mathbb{P}(\{\omega_{i}\})\ge 0$ per ogni $i$, e anche che $\sum_{i\,=\,1}^{\infty}\mathbb{P}(\{\omega_{i}\})=1$.

A tal proposito, è interessante fare la seguente osservazione:

> Supponendo di avere $\Omega:=\{1,\,2,\,\dots\}$, ossia coincidente con l'insieme dei numeri naturali, non è possibile definire alcuna misura di probabilità $\mathbb{P}$ $\sigma$-additiva e uniforme su $(\Omega,\,\mathcal{P}(\Omega))$, ossia in modo che risulti:
> $$\mathbb{P}(\{i\})=c\,\,\,\,\,\,\,\,\,\,i=1,\,2,\,\dots$$
> essendo $c$ una costante indipendente da $i$.

Tale osservazione è facilmente dimostrabile: procedendo per assurdo, se invece fosse possibile definire una funzione $\mathbb{P}$ del genere, allora dovrebbe necessariamente valere che:
$$\mathbb{P}(\Omega)=\sum_{i\,=\,1}^{\infty}c=1$$
Tuttavia, una serie a termini costanti $\sum_{i\,=\,1}^{\infty}c$ può convergere solamente se si pone $c=0$, e in tal caso si otterrebbe che $\mathbb{P}(\Omega)=0$; avendo trovato una contraddizione, la nostra osservazione iniziale è dimostrata.

Proseguendo la nostra trattazione degli spazi di probabilità numerabili, passiamo al considerare le varie [[CDP_02 - Probabilità#Proprietà delle probabilità|proprietà della probabilità]] che abbiamo verificato in precedenza come conseguenze immediate degli assiomi: nel caso di spazi di probabilità infiniti, **l'aggiunta dell'assioma della $\sigma$-additività garantisce che continuino a valere tutte le proprietà dimostrate in precedenza**. Anzi, in verità non è neanche necessario "aggiungere" l'assioma della $\sigma$-additività a quello dell'additività finita, ma basterà sostituire la seconda con la prima, dato che la $\sigma$-additività rende automaticamente verificata anche l'additività finita.
___
##### Proprietà di continuità delle probabilità

L'assioma della $\sigma$-additività dà luogo a un'importante conseguenza, ossia la "**proprietà di continuità delle probabilità**", che presenta il seguente enunciato:

> In uno spazio di probabilità $(\Omega,\,\mathcal{F},\,\mathbb{P})$, considerati per $n=1,\,2,\,\dots$ due eventi $A_{n}$ e $B_{n}$, tali che:
> $$A_{n}\subseteq A_{n\,+\,1}\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,B_{n}\supseteq B_{n\,+\,1}$$
> e ponendo:
>$$A:=\bigcup_{n\,=\,1}^{\infty}A_{n}\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,B:=\bigcap_{n\,=\,1}^{\infty}B_{n}$$
> se la probabilità $\mathbb{P}$ è $\sigma$-additiva allora risulta che:
> $$\mathbb{P}(A)=\lim_{n\,\to\,\infty}\mathbb{P}(A_{n})\,\,\,\,\,\,\,\,\,\,\,\,\,\,\,\mathbb{P}(B)=\lim_{n\,\to\,\infty}\mathbb{P}(B_{n})$$
> 

[DIMOSTRAZIONE: pag. 194]

[pag. 195 - 196]
___
## Variabili aleatorie generali

[pag. 196/218 - 222/229 - 232]
___