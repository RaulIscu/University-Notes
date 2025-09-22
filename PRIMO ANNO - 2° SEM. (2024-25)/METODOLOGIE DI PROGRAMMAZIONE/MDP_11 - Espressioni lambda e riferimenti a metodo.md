## Espressioni lambda

In parole povere, un'**espressione lambda** è definibile come una "**funzione anonima**", una funzione senza un nome preciso e che può, in certi contesti, essere utilizzata come un oggetto. È stata introdotta in Java a partire da **Java 8**, e torna particolarmente utile soprattutto quando accoppiata con le **[[MDP_12 - Interfacce#Interfacce funzionali|interfacce funzionali]]**.

A livello generico, un'espressione lambda presenta la seguente **struttura**:

```
(tipo1 param1, tipo2 param2, ...) -> { corpo }
```

tuttavia è molto comune che essa venga semplificata, a seconda di dove e come viene utilizzata. In particolare:
- **il tipo dei parametri è opzionale**, poiché, essendo un'espressione lambda il più delle volte associata a un'interfaccia funzionale, esso è facilmente intuibile dal contesto dove viene utilizzata;
- **le parentesi tonde sono opzionali se in input si ha un solo parametro**;
- **le parentesi graffe sono opzionali se il corpo è costituito da una sola riga**;
- **non è necessario**, spesso, **inserire un `return`**.

Per certi versi, le espressioni lambda ricordano le **[[MDP_02 - Classi#Classi anonime|classi anonime]]**, soprattutto per la loro anonimità e per la natura "temporanea" che hanno, tuttavia presentano anche delle sostanziali **differenze**. Oltre, ovviamente, al fatto che un'espressione lambda è una funzione mentre una classe anonima è una classe, vi è anche una differenza a livello di **compilazione**, dato che le classi anonime vengono compilate come classi interne, mentre le espressioni lambda come metodi privati, invocati dinamicamente; un'altra fondamentale differenza sta nell'utilizzo della keyword **`this`**, che in una classe anonima si riferisce proprio a tale oggetto anonimo, mentre in un'espressione lambda si riferisce all'oggetto della classe che la racchiude.

In generale, l'utilizzo di espressioni lambda permette di avere **codice più conciso** e **più leggibile**, un maggiore supporto per la **programmazione funzionale**, in particolare quando si lavora con [[MDP_12 - Interfacce#Stream|stream]] e interfacce funzionali, e anche una maggiore **testabilità**.
___
## Riferimenti a metodo

I **riferimenti a metodo**, o ***method references***, rappresentano sostanzialmente una **forma concisa e leggibile di [[MDP_11 - Espressioni lambda e riferimenti a metodo#Espressioni lambda|espressione lambda]]**, possibile nel momento in cui essa vada a richiamare un metodo esistente sui suoi argomenti. Esistono principalmente **4 tipi** di riferimenti a metodo in Java:
- i riferimenti a un **metodo statico**;
- i riferimenti a un **metodo di istanza su oggetti**;
- i riferimenti a un **metodo di istanza su un tipo**;
- i riferimenti a un **costruttore**.

##### Riferimenti a metodo statico

I **riferimenti a metodo statico** sono della seguente forma:

```
Classe::metodoStatico
```

ed equivalgono alla seguente espressione lambda:

```
(parametri) -> Classe.metodoStatico(parametri)
```
___
##### Riferimenti a metodo d'istanza su oggetti

I **riferimenti a metodo d'istanza su oggetti** sono della seguente forma:

```
istanza::metodo
```

ed equivalgono alla seguente espressione lambda:

```
(parametri) -> istanza.metodo(parametri)
```
___
##### Riferimenti a metodo d'istanza su tipo

I **riferimenti a metodo d'istanza su un tipo** sono della seguente forma:

```
Classe:metodo
```

ed equivalgono alla seguente espressione lambda:

```
(obj) -> obj.metodo()
```
___
##### Riferimenti a costruttore

I **riferimenti a costruttore** sono della seguente forma:

```
Classe::new
```

ed equivalgono alla seguente espressione lambda:

```
() -> new Classe()
```
___