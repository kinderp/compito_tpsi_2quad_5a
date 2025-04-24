<div align="justify">
Per un'azienda sanitaria è necessario progettare ed implementare un sistema per la gestione dei biglietti di entrata ed uscita dell'ospedale.

I pazienti, all'ingresso, richiederanno l'apertura della sbarra premendo un bottone sulle apposite colonnine.
Alla pressione del bottone, il sistema deve creare un nuovo biglietto sul database e segnare la data di entrata (in millisecondi, timestamp). 
Una volta creato il nuovo record sul db, il biglietto verrà stampato e fornito in output al paziente attraverso la colonnina stessa. 
Il ritiro del biglietto dalla colonnina farà alzare la sbarra d'ingresso.

All'uscita, il paziente inserirà il biglietto prelevato in entrata dalla colonnina nelle casse automatiche. Il sistema segnerà la data di uscita sul corrispondente record nel db e calcolerà il costo della sosta (uscita - entrata)*0.01.
Effettuato il pagamento, la cassa restituirà il biglietto precedentemente inserito che servirà per far alzare la sbarra nelle colonnine d'uscita.
La sbarra d'uscita non si alzerà se la data di uscita (aggiornata in fase di pagamento) non è valorizzata.

Dopo una settimana i record dei biglietti verranno eliminati automaticamente dal sistema 

</div>

Creare il file `create_db.js` che crea il database `compito.db` e la tabella `biglietto` con i seguenti campi:
* id (`TEXT PRIMARY KEY`)
* entrata (`INTEGER NOT NULL`)
* uscita (`INTEGER DEFAULT 0`)

Realizzare un'interfaccia rest in node.js (express.js) con tutte le rotte elencate di segiuto.
Le rotte devono restiture un json fatto in questo modo:

```json
{
  "code": 1,
  "data": []
}
```

`code` è un codice di ritorno (-1 in caso di errore) e `data` è un vettore contenente i dati da tornare al client


* **/biglietti** (`GET`)
Deve restituire tutti biglietti con tutti i campi della tabella corrispondente

* **/biglietto** (`POST`)
Deve creare un nuovo biglietto con la data di entrata nel parcheggio

* **/biglietto/:id** (`GET`)
Ritorna tutte le informazioni di uno specifico biglietto

* **/biglietto/:id** (`PUT`)
Deve impostare la data di uscita per il biglietto corrispondente

* **/pagamento/:id** (`GET`)
Deve calcolare la differenza tra uscita ed entrata e ritornare il costo della sosta (tariffa di un centesimo al minuto)

* **/biglietto/:id** (`DELETE`)
Deve eliminare il biglietto con il corrispondente id
  
