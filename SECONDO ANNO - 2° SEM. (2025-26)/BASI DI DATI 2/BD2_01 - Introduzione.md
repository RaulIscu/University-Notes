Nel corso di Basi di Dati 2, l'obiettivo principale sarà imparare a **progettare applicazioni reali di basi di dati**, in contesti concreti e tendenzialmente di dimensioni più o meno grandi. Si tratta di un obiettivo complesso, dove **gran parte del tempo viene speso nella comprensione profonda dei dati** di nostro interesse e **delle relazioni** che intercorrono tra di essi. 

Data la complessità dell'obiettivo, spesso non esiste una soluzione unica, né una sorta di "ricetta" da applicare che possa soddisfare tutta una branca di casi: perciò, è fondamentale imparare a **ragionare logicamente**, a **considerare eventuali conseguenze di ogni scelta** che viene fatta, a **valutare più alternative** e soprattutto a **scomporre i problemi complessi in sottoproblemi**.

## Ciclo di vita di un software

Trovandoci a lavorare anche con esempi concreti di sviluppo di applicazioni e di basi di dati, è opportuno aprire una parentesi sul tipico **ciclo di vita di un software**, ossia dei vari passaggi che intercorrono tra la richiesta dello stesso da parte di un committente e il rilascio della sua versione definitiva. Sommariamente, si possono riassumere le **fasi principali** del ciclo di vita di un software nei seguenti punti:
1. studio di fattibilità;
2. raccolta dei requisiti;
3. analisi concettuale dei requisiti;
4. progetto dell'applicazione;
5. implementazione dell'applicazione;
6. integrazione dei componenti e verifica dell'applicazione;
7. messa in esercizio dell'applicazione;
8. manutenzione dell'applicazione.

Analizziamo ciascuna di queste tappe più nel dettaglio. Durante lo **studio della fattibilità**, che rappresenta l'inizio dell'iter, la priorità è quella di comprendere effettivamente quali sono i requisiti richiesti dal committente per l'applicazione considerata, valutare costi e benefici della stessa, e cominciare a pianificare le attività e le risorse del progetto, così come il suo ambiente di programmazione, sia a livello di hardware che di software (ciò risulta essere cruciale soprattutto se si pensa all'applicazione in larga scala, sia per un discorso di compatibilità tra dispositivi sia per eventuali interazioni che l'applicazione deve prevedere con altre applicazioni).

Il secondo passaggio è la **raccolta dei requisiti** presso i vari "attori" che contribuiranno allo sviluppo dell'applicazione (analisti, progettisti, programmatori, ecc. ecc.), che prevede anche una sintesi e un raffinamento dei requisiti raccolti, in modo da renderli il più semplici e compatibili l'uno con l'altro possibili.

A questo punto, passiamo all'**analisi concettuale dei requisiti**, il cui obiettivo è produrre uno "**schema concettuale**" dell'applicazione, che definisca in dettaglio cosa l'applicazione dovrà realizzare (per adesso, non si considera il "come"). All'interno di questo schema concettuale, si dovranno:
- modellare i dati di interesse, le loro articolazioni, interrelazioni e possibili evoluzioni;
- specificare i servizi computazionali che l'applicazione dovrà fornire all'utente.

Nel quarto passaggio, quello del **progetto dell'applicazione**, si specificherà il "come" dell'applicazione, dunque come compiere effettivamente le mansioni specificate in modo dettagliato e non ambiguo nel passo precedente. Nel fare ciò, si dovrà prendere una decisione definitiva sul "mix tecnologico" ottimale per l'applicazione, definirne l'architettura e le strutture di rappresentazione dei dati.

In seguito, si può passare all'**implementazione dell'applicazione**, ossia alla scrittura effettiva del codice e della documentazione dello stesso. Va specificato che, tendenzialmente, la realizzazione dell'applicazione non avviene tutta in blocco, ma piuttosto vengono sviluppati singoli sistemi o singole parti dell'applicazione indipendentemente, fino a coprire l'interezza della funzionalità della stessa. 

Passiamo al sesto passaggio, che consiste nell'**integrazione dei componenti** precedentemente implementati, e nella **verifica del corretto funzionamento dell'applicazione**, che dovrà svolgere la sua mansione in modo corretto, completo ed efficiente.

Infine, si può **mettere in esercizio l'applicazione**, rendendola disponibile al committente e a un eventuale pubblico. In seguito, l'ultima parte rimasta del ciclo di vita di tale applicazione è la sua **manutenzione**, dunque il monitoraggio del comportamento della stessa durante l'esercizio, così come eventuali correzioni ed aggiornamenti ove necessario.

Si precisa che, al termine di ognuna delle fasi appena analizzate, si può tranquillamente tornare indietro a una fase precedente nel momento in cui si notano problematiche o difficoltà di vario tipo.

##### Modelli di ciclo di vita del software

Va chiarita una cosa, riguardo quanto detto finora: **una sequenza di questo tipo**, dove le fasi si susseguono sequenzialmente e dove la successiva viene avviata solo in seguito al completamento della precedente (modello che prende il nome di **modello "a cascata"**) in realtà **è abbastanza inefficiente** nel concreto, e va presa piuttosto da un punto di vista puramente didattico.

Spesso, in contesti concreti, si preferisce un **modello "a spirale"**, detto anche **modello iterativo**: invece di completare al 100% una fase prima di passare alla prossima, si suddividono i requisiti totali dell'applicazione in più parti, e ci si focalizza in ogni passaggio su una di queste parti (partendo, naturalmente, da quelle più importanti per il funzionamento dell'applicazione). Si può formalizzare questo modello con il seguente grafico a torta:

![[sw_modelloiterativo_esempio.png]]

Come specificato nell'immagine, ciò porta alla **messa in esercizio di versioni sempre più complete**, che vengono rilasciate quando una più avanzata sta già venendo implementata e/o verificata. Idealmente, **più fasi della sequenza dovrebbero essere attive contemporaneamente**: ad esempio, mentre sta venendo effettuata l'analisi della prima versione dell'applicazione, sarebbe ottimale effettuare già la raccolta dei requisiti della seconda versione. In questo modo si ottiene un'**ingente ottimizzazione dei tempi**. 
___

