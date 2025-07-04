La funzione **`input()`** permette all'utente di inserire manualmente dei dati in fase di esecuzione del programma. Ciò che si inserisce mediante tale funzione viene letto come stringa (`str`). Ad esempio, nel codice:
```
x = input()
print(x)
```
ci verrà chiesto di inserire un valore per la variabile `x`, e verrà in seguito visualizzata una stringa contenente ciò che abbiamo scritto.

La funzione `input()` accetta un argomento opzionale, in particolare una stringa, che rappresenterà un messaggio che verrà visualizzato quando verrà data all'utente la possibilità di inserire il dato. Ad esempio, se si esegue il seguente codice:
```
x = input("Enter your name: ")
print("Hello, " + x)
```
ci verrà chiesto di inserire un valore per la variabile `x` con annesso il messaggio `Enter your name:`.