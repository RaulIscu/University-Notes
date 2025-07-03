**`JColorChooser`** è una classe di Swing che estende `JComponent`. Si tratta di una classe che fornisce un pannello di controllo progettato per permettere all'utente di selezionare e manipolare dei colori.

### Costruttori

La classe `JColorChooser` presenta tre possibili **costruttori** per un proprio oggetto:
- **`JColorChooser()`**, che costruisce un oggetto di tipo `JColorChooser` con il bianco come colore iniziale predefinito;
- **`JColorChooser(Color initialColor)`**, che costruisce un oggetto di tipo `JColorChooser` con il colore `initialColor` come colore iniziale predefinito;
- **`JColorChooser(ColorSelectionModel model)`**, che costruisce un oggetto di tipo `JColorChooser` con associato lo specifico modello si selezione `model`.
___
### Metodi

Di seguito, la lista dei **metodi** compatibili con la classe `JColorChooser`:
- `void addChooserPanel(AbstractColorChooserPanel panel)`, che permette di aggiungere un pannello di selezione colore `panel` all'oggetto considerato;
- **`static JDialog(Component c, String title, boolean modal, JColorChooser chooserPane, ActionListener okListener, ActionListener cancelListener)`**, 