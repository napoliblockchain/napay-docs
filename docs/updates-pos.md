## POS

#### versione 1.3.1

    - Il tasto segnala bug non ha tutti i campi #64



#### versione 1.3

	**new features**
	- #57 Napay: togli copyright nel footer e metti powered by
	- #52 Napay: prorogare scadenza iscrizione al 28 febbraio
	- #48 Napay: gestione/visualizzazione dei log delle applicazioni
    - #27 Bolt: inserire recaptha2 in ripristino pwd, form, bugs e login

	**fix**
	- #61 Push: i messaggi sono tutti [bolt]
    - #58 pos: check sw static cache
    - #54 Napay: transaction details error
    - #51 Pos: invoice TTS deve mostrare logo personalizzato caricato nello store di Napay
    - #46 Pos: errore in lista token se non si ha un wallet
    - #44 POS: id_pos
    - #34 Pos/Bolt: non si aggiorna messaggio memo dalla transazione ipn
    - #24 Napay: col nuovo sistema di notifiche mancano le notifiche agli admin
    - #20 POs Desktop : select "undeleted"


------------------------------------------------
#### 15.01.2020 - TEST
------------------------------------------------
**Nuove features**

    - Integrazione completa con le 4 applicazioni NaPay


#### 01.08.2019
    - #270 : Aperto nuovo branch no-associazione
    - eliminato campo da np_merchants (id_association) [ALTER TABLE np_merchants DROP id_association;]
    - eliminato Associations da MerchantsController
    - eliminato UsersController
    - ripulite tutte le views e i controllers dove compariva Associations
    - aggiunta funzione get_domain in classe Utility

#### 22.07.2019
- #271 : menu: icona $ diventa btc

#### 11.07.2019
- #251 : dopo creazione pos automatico non funziona pos invoice

#### 02.07.2019
**sin**
- get del sin da parte della app principale Napay

#### 12.06.2019
**Service Worker**
- new sw. Logout funzionante

**menu**  
- Visualizzazione lista transazioni e dettaglio
- visualizzazione lista transazioni token e dettaglio
- Logout funzionante

**sin**
- funzionalità di salvataggio del SIN dopo il primo ingresso in modo tale da non doverlo ripetere in caso di logout

#### 26.05.2019
    - adeguamento utilizzo nuovo url settings->poa_url

#### 22.05.2019
    - new icons

#### 17.05.2019
**Notifiche**
- Notifiche x N-Pay

**PWA**
- Adeguamento index con manifest.json


#### 15.05.2019
- Pulizia software

#### 08.05.2019
- First commit

**Notifications**
- Nuova gestione delle notifiche WebApp


### v0.0.1 - 08.05.2019
    Initial release
