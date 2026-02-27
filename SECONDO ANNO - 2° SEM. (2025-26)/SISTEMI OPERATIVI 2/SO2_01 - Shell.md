All'interno di Linux, uno degli strumenti più importanti (se non il più importante) a disposizione dell'utente è la "**shell**", spesso chiamata anche "**terminal**" o "**terminale**". Si tratta, sostanzialmente, di un **interprete di comandi**, un **programma che esegue altri comandi** chiamati dall'utente. 

## Diversi tipi di shell

Ci sono vari tipi di shell:
- **Thompson-Bourne Shell**, abbreviata in **sh**;
- **Bourne-Again Shell**, abbreviata in **bash**;
- **Korn Shell**, abbreviata in **ksh**;
- **Friendly Interactive Shell**, abbreviata in **fish**;

e così via. 

In questo corso, si approfondirà il funzionamento della shell **bash**. Per **verificare quale tipo di shell si sta utilizzando**, si può avviare un'istanza della shell e impartire ad essa il [[SO2_01 - Shell#Prompt e comandi|comando]]:

```
echo $0
```
___
## Prompt e comandi

Quando non sta eseguendo una qualche mansione, quello che fa la shell è **attendere che l'utente scriva un comando da eseguire**: nel fare ciò, la shell stampa a schermo quello che viene chiamato "**prompt**", che indica visivamente all'utente la disponibilità ad eseguire comandi (infatti, se il sistema sta ancora eseguendo una mansione precedentemente impartita dall'utente il prompt non compare, mentre viene stampato solo nel momento in cui la shell è pronta a ricevere un nuovo comando da eseguire).

Tipicamente, il prompt è strutturato nel modo seguente:

```
nomeutente@nomemacchina:~path$
```

dove **`nomeutente`** è il nome dell'utente attualmente in controllo della macchina, **`nomemacchina`** è il nome con cui viene indicata tale macchina, e **`path`** è il percorso da percorrere per arrivare dalla cartella `home` alla cartella attuale (dunque, se si è semplicemente nella cartella `home`, tale path sarà nullo e non verrà stampato); alternativamente, se la cartella corrente non si trova nel sottoalbero radicato in `home`, allora `path` conterrà il percorso assoluto.

Una volta stampato il prompt, dunque, l'utente potrà eseguire dei **comandi**. Tipicamente, un comando assume la seguente struttura:

```
comando [opzioni] argomenti_obbligatori
```

dove **`comando`** può essere visto come l'identificatore del comando stesso, ossia la componente che indica alla macchina qual è la funzionalità richiesta, **`opzioni`** indica eventuali parametri supplementari che possono essere aggiunti per ottenere una funzionalità più specifica, e **`argomenti_obbligatori`** sono gli argomenti da inserire per il corretto funzionamento del comando (file sorgente, file di destinazione, altri comandi, ecc. ecc.). 

Si noti che `opzioni` è indicato tra parentesi quadre: in generale, **se delle opzioni sono indicate tra parentesi quadre, significa che possono esserci 0, 1 o più opzioni facoltative** per l'esecuzione del comando. Ad esempio, di seguito vediamo il layout generico del comando `cp`:

```
cp [OPTION...] SOURCE... DEST
```

La voce **`[OPTION...]`** indica che si possono aggiungere delle opzioni al comando per ottenere effetti particolari, ma è anche perfettamente possibile omettere qualsiasi opzione supplementare. Certe volte, invece, si richiede l'**inserimento di caratteri separatori tra certi argomenti**; ad esempio, di seguito si vede il layout generico del comando `chmod`:

```
chmod [OPTION...] MODE[, MODE...] FILE...
```

In questo caso, la voce **`MODE[, MODE...]`** indica che almeno un parametro `MODE` va sempre specificato, ma che opzionalmente se ne possono specificare anche altri, a patto che siano separati da virgole (`,`). 

##### Approfondimento sulle opzioni

Tipicamente, le opzioni sono composte o da **un carattere** o da **una parola**, e in base a quale dei due scenari si verifica c'è anche una differenza nel **prefisso dell'opzione**. Infatti, in generale, si ha:
- **`-carattere`** se l'opzione è individuata solo da un carattere;
- **`--parola`** se l'opzione è individuata da una parola.

Ad esempio, tornando al comando `cp`, le opzioni `-i` e `--interactive` sono perfettamente equivalenti, e lo stesso vale per la coppia di opzioni `-r` e `--recursive`.

In certi casi, **le opzioni possono avere degli argomenti**, e in base al contesto tale argomento può essere aggiunto in vari modi:
- adiacente all'identificatore dell'opzione, ad esempio `-k1`;
- separato da uno spazio dall'identificatore dell'opzione, ad esempio `-k 1`;
- indicato tramite un segno dell'uguale (`=`), ad esempio `--key=1`.

Nel caso in cui più opzioni di tipo `-carattere` vengano specificate e siano tutte senza argomento, esse possono essere **raggruppate** in un'unica opzione; ad esempio, le opzioni:

```
-b -r -c
```

possono essere raggruppate in:

```
-brc
```

Infine, in alcuni casi, è possibile inserire anche **opzioni senza trattini di prefisso**, ad esempio:

```
tar xfz nomefile.tgz
```
___
##### Il comando `man`

Esiste un comando particolare, ossia il **comando `man`**, che ha la seguente sinossi:

```
man [sezione] comando
```

il cui scopo è **fornire informazioni sul funzionamento e sulle caratteristiche di altri comandi**. Impartire il comando `man` alla shell, indicando un qualsiasi altro comando (`man` stesso incluso), stamperà a schermo un manuale di utilizzo del comando in questione, che comprende una descrizione sommaria del suo funzionamento, una o più sinossi, una lista delle opzioni possibili e una breve spiegazione per ciascuna di esse.
___
## Gestire gli utenti tramite shell

Durante l'installazione di Linux, così come avviene generalmente anche per gli altri OS, si deve specificare necessariamente almeno un **utente**, ossia una sorta di profilo per utilizzare la macchina. Per creare questo utente, che spesso verrà considerato da allora in poi l'**utente principale**, basterà specificare **username** e **password** (alcune versioni e distribuzioni creano un utente in modo automatico, con dati da personalizzare in seguito).

Oltre ai vari utenti che possono essere creati, vi è anche un "**superutente**", ossia un utente che ha **tutti i privilegi**, ed è concretamente l'amministratore di sistema (viene chiamato **`root`**). `root` non è un utente qualsiasi, e in quanto tale non ci si può loggare come si farebbe con altri utenti; ciononostante, **è possibile per un utente acquisire i diritti di `root` mediante comandi specifici** (generalmente, tali comandi sono **`su`** o **`sudo`**).

Per approfondire il comando `sudo`, introduciamo il concetto di "**gruppo di utenti**": ogni utente appartiene almeno a un gruppo, e un gruppo viene automaticamente creato durante la configurazione della macchina, spesso con lo stesso nome dell'utente principale. Nelle distribuzioni di Linux appartenenti alla famiglia Debian, l'utente principale è un "**sudoer**", ossia un utente appartenente quindi al gruppo **`sudo`**: l'appartenenza a questo gruppo permette di poter eseguire comandi con privilegi da superutente (`root`) utilizzando proprio il comando `sudo`, nel modo seguente:

```
sudo comando
```

dove **`comando`** è proprio il comando che si vuole eseguire con i privilegi di `root`. Dunque, in parole povere, **`sudo` è un comando che prende in input un altro comando, e che permette di eseguire quest'ultimo con tutti i privilegi**.

Di default, **un utente creato non appartiene subito al gruppo `sudo`**; per **aggiungere un utente al gruppo `sudo`** si può però eseguire il seguente comando:

```
adduser nuovoutente
```

Se invece si vuole aggiungere l'utente `nuovoutente` a un gruppo particolare (non necessariamente quello dei sudoer), si potrà eseguire il seguente comando:

```
adduser nuovoutente gruppo
```
___


