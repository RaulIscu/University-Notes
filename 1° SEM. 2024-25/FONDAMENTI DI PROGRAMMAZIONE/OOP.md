Nella programmazione comune, applicata in contesti concreti, si utilizza spesso un metodo di programmazione "**a oggetti**", o ***OOP*** (*Object Oriented Programming*). In realtà, gli oggetti sono ricorrenti anche nella programmazione che sfrutta le varie strutture dati, in quanto proprio le strutture dati stesse (`str`, `int`, `dict`, ecc. ecc.) sono degli oggetti, con i propri attributi e i propri metodi.

Un oggetto, dunque, può essere definito genericamente come l'unione di informazioni particolari, ossia:
- **attributi**, cioè i dati che caratterizzano una particolare entità;
- **metodi**, cioè le funzionalità caratteristiche dell'entità considerata.

Ad esempio, una [[Stringhe|stringa]] avrà come attributi i caratteri che la compongono, la sua lunghezza, ecc. ecc.; i suoi metodi, invece, saranno funzioni come `str.find()`, `str.lower()`, ecc. ecc.

Una tipologia generica di oggetto viene detta "**classe**", mentre un individuo appartenente a una certa tipologia di oggetto viene detto "**istanza della classe**".
___
Oltre ad essere utilizzate, le classi possono, ovviamente, essere anche create. Vediamo, dunque, come **creare una nuova classe**.

Per fare ciò, si dovrà utilizzare la parola chiave **`class`** (similmente a come è necessaria la parola chiave `def` per definire una funzione) seguita dal nome della classe da creare e da un *colon* (`:`); per consuetudine, tale nome presenta l'iniziale maiuscola per ognuna delle parole che lo compongono. Tale passaggio coincide con il seguente codice:
```
class NomeDellaClasse:
```
A questo punto, il blocco di codice riferito a tale classe dovrà essere indentato. Possiamo assegnare degli attributi alla classe appena definita in due modi diversi:
- se si vogliono definire degli attributi condivisi da tutte le istanze della classe, si definiscono subito dei cosiddetti "attributi di classe";
- se si vogliono definire degli attributi per delle singole istanze, si definiscono degli attributi individuali.

Per il primo approccio, sarà sufficiente assegnare a una variabile `attributo_di_classe` un determinato valore, e ciò varrà per tutte le istanze della classe. Per il secondo approccio, più complesso, si definisce un metodo speciale chiamato **inizializzatore** (`__init__()`), che come argomenti prende prima di tutto l'oggetto da costruire (`self`), e poi un gruppo variabile di argomenti; a questo punto, per assegnare a `self` degli attributi, si indenterà un ulteriore blocco di codice, in cui ogni riga rappresenta un attributo individuale assegnato a `self` (generalmente, questo attributo viene fornito proprio dal gruppo di argomenti). In codice, possiamo rappresentare entrambi gli approcci nel modo seguente:
```
class NomeDellaClasse:
	attributo_di_classe = valore1
	
	def __init__(self, <argomenti>):
		self.attributo_individuale = valore2
```
___
Per creare un'istanza di una determinata classe, ossia per inizializzarla, si opera un assegnamento molto semplice, del tipo:
```
A = NomeDellaClasse(argomenti_del_metodo_init)
```
>**NB:** gli argomenti che vengono passati non corrispondono all'argomento `self`, ma alla lista di argomenti `<argomenti>`

Ad esempio, se volessimo creare un'istanza di insieme (`set`) a partire da una lista, si scriverà il codice seguente:
```
L = set([1, 2, 3, 4, 5, 1, 4, 2, 5])
```
___
Invece, per eseguire un metodo di un determinato oggetto, si scrive:
```
risultato = oggetto.metodo1(argomenti_del_metodo)
```
Ad esempio, se volessimo cercare una particolare stringa all'interno di una stringa di partenza, si scriverà il codice seguente:
```
posizione = testo.find("Paperino")
```
___
