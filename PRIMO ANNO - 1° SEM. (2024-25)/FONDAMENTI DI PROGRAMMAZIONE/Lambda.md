In Python, una funzione **`lambda`** è una funzione "anonima" e generalmente abbastanza piccola. Vediamo subito un esempio di applicazione:

```
x = lambda a: a + 10
print(x(5))
```

In questo esempio, alla variabile `x` viene associata una funzione `lambda` che, preso come argomento un valore `a`, gli aggiunge 10 e restituisce il risultato di tale somma. In generale, una funzione `lambda` può avere un numero qualsiasi di argomenti, che possono però essere manipolati solo in una singola espressione.

Utilizzare una funzione `lambda` può essere vantaggioso in vari contesti: è conveniente, infatti, utilizzarla all'interno di altre funzioni, oppure, analizzando un esempio più specifico, per applicare più criteri di ordinamento a una successione di elementi.