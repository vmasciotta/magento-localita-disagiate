# magento-localita-disagiate

##Configurazione tablerates Magento per le località disagiate italiane
File CSV per le spese di spedizione, tablerates, delle località disagiate italiane, basato sulla lista fornita da [SDA](http://www.sda.it/SITO_SDA-INSIDEX-WEB/pages/CAP_Localita_disagiate_it/200). 

Il file, così come servito, è neutro. Questo significa che vanno aggiunti i prezzi delle spedizioni ai relativi CAP.

La riga #2 del file csv definisce un prezzo forfettario, anche questo da definire, così che tutti i CAP della nazione ITALIA (*) hanno prezzo X. 

Cancellare questa riga se non necessaria.

*Questo repository ha un branch per ogni versione (data di inizio validità della lista) del file messo a disposizione da SDA. Il branch master punta sempre all'ultima versione disponibile.*

###Configurazione regola spedizone gratuita

Nel caso in cui si voglia ad esempio impostare la spedizione gratuita per un ordine superiore a X per tutta Italia, fatta eccezione per le località disagiate,  e non si vuole usare qualche tool di configurazione avanzata come MatrixRate, si può impostare una regola prezzo carrello in cui viene definito che:

####Condizioni
Se tutte queste condizioni sono vere:

* Subtotale è uguale o maggiore a X
* Paese di spedizione è Italia
* cap di spedizione non è uno di 51021,67020 ...(fare copia/incolla dei valori presenti nel file regola-prezzo-carrello.txt)

####Azioni
...

**Applica all'importo di spedizione:** si

**Spedizione gratuita:** scegliere un valore diverso da no a seconda delle esigenze

...

**Bug conosciuti:**

Con questa procedura in fase di checkout, se si raggiunge l'importo per la spedizione gratuita e il cap non è tra quelli delle località disagiate, apparirà nello step delle *Informazioni di pagamento* l'etichetta *Nome metodo* inserita in: 

Admin->System->Vendite->Metodi di spedizione->Nome metodo e non ipoteticamente un "Spedizione gratuita"

Senza effettuare modifiche al codice, non c'è modo di cambiare da amministrazione questa etichetta per questa particolare condizione.