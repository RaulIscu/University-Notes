La funzione **`print()`**, che a seconda del linguaggio assume vari nomi, è una delle funzioni più basilari e utilizzate nella programmazione in generale. Tale funzione permette semplicemente di mostrare, come output nella console, ciò che prende come argomento, che può essere sostanzialmente qualsiasi cosa. Ad esempio, se si vuole visualizzare il testo "33 trentini entrarono a Trento tutti e 33 trotterellando", si potrà eseguire il seguente codice:

```
print(str(33) + " trentini entrarono a Trento tutti e " + str(33) + " trotterellando")
```

In particolare, per modificare e perfezionare la visualizzazione di un testo, si potranno utilizzare alcuni caratteri speciali detti "**escape characters**", ognuno cominciante con un backslash (**`\`**) e con una funzionalità ben precisa, tra cui:
- **`\n`**, o "**newline**", che permette di inserire un accapo nella stringa;
- **`\t`**, o "**tab**", che permette di inserire una tabulazione nella stringa;
- **`\"`** e **`\'`**, che permette di inserire le virgolette tipicamente utilizzate per definire una stringa all'interno di una stringa di testo;
- **`\\`**, che permette di inserire un backslash all'interno di una stringa di testo.