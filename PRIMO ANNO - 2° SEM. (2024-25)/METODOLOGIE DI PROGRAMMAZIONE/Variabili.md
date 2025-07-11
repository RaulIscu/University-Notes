Una **variabile**, in Java, rappresenta il **contenitore** per qualsiasi dato o oggetto che si voglia conservare o manipolare in un programma. In maniera astratta, potremmo vedere una variabile come composta da tre parti:
- il **tipo** della variabile, che il più delle volte corrisponderà a quello di ciò che viene conservato al suo interno;
- l'**identificatore** della variabile, ossia il nome con cui riferirsi e accedere ad essa;
- il **contenuto**, che può essere pressoché qualsiasi cosa (un [[Classi#Classi e oggetti|oggetto]], un dato di [[Tipi primitivi|tipo primitivo]], una [[Stringhe|stringa]], ecc. ecc.).
___
## Le "fasi" di una variabile

Per **creare una variabile** e poterla utilizzare in seguito, si dovranno effettuare dei passaggi ben precisi riassumibili nei due seguenti:
- la **dichiarazione**;
- l'**inizializzazione**.

Nella prima fase, ossia quella della **dichiarazione** di una variabile, si va a specificare il tipo e l'identificatore associati a tale variabile. Ad esempio, se volessimo avere una variabile denominata `x` di tipo `int`, dovremmo effettuare la seguente dichiarazione:

```
int x;
```

In seguito alla dichiarazione di una variabile, Java andrà automaticamente ad allocare una quantità di memoria adeguata per quest'ultima in base al suo tipo. Ora, però, dobbiamo stabilire il contenuto effettivo della variabile: per fare ciò, effettuiamo un'**inizializzazione**. Se volessimo, quindi, assegnare il valore `5` alla variabile `x` dell'esempio precedente, andremmo a scrivere:

```
x = 5;
```

Si noti come, avendo già dichiarato il tipo della variabile, non sarà più necessario specificarlo in utilizzi futuri della stessa.

Per comodità, è possibile **effettuare la dichiarazione e l'inizializzazione di una variabile nella stessa istruzione**, ad esempio:

```
int x = 5;
```
___
## La visibilità delle variabili

In base a dove e come vengono create le variabili, esse presentano diversi gradi di **visibilità**. In particolare, possiamo classificare le variabili sotto questo aspetto in 3 categorie:
- variabili **locali**, dove rientrano variabili dichiarate nel **corpo di un metodo** o di un **costruttore**, e che sono effettivamente visibili solo all'interno di tale blocco di codice;
- variabili **d'istanza**, dove tendenzialmente rientrano le variabili dichiarate come **[[Classi#Campi, metodi e costruttori|campi]] non statici di una classe**, e di cui ogni oggetto di tale classe possiede una copia;
- campi **statici** di classe, che sono comuni per tutti gli oggetti che istanziano tale classe.

Una particolarità che differenzia in particolare le variabili locali dalle variabili d'istanza: **le variabili locali non hanno un valore di default**, e quindi, in caso si dichiari una variabile locale ma non la si inizializzi, un tentativo di utilizzo della stessa porterebbe a un errore di compilazione; invece, **le variabili d'istanza hanno dei valori di default** a seconda del loro tipo, in particolare:
- $0$ per quelle di tipo **`int`**;
- $0.0$ per quelle di tipo **`double`**;
- **`false`** per quelle di tipo **`boolean`**;
- **`null`** per quelle che contengono un qualsiasi **oggetto**;

e così via.

La differenza di visibilità, in particolare tra variabili d'istanza e variabili locali, può dar vita a un fenomeno detto "**shadowing**", che avviene quando **una variabile locale va a "nascondere" una variabile d'istanza con lo stesso nome**. Ad esempio, nella seguente [[Classi#Cos'è una classe?|classe]]:

```
public class ShadowingDemo {
	int num = 5;

	public void stampa() {
		int num = 10;
		
		System.out.println(num);
		System.out.println(this.num);
	}
}
```

la variabile `num` definita nel metodo `stampa()` va a "nascondere" la variabile d'istanza omonima, e così l'istruzione `System.out.println(num)` andrà a stampare `10` e non `5`. Per accedere effettivamente alla variabile d'istanza dal corpo del metodo, si dovrà utilizzare la keyword **`this`**, in modo da specificare che si sta cercando di accedere alla variabile d'istanza associata all'oggetto e non a quella locale definita nel metodo in questione.