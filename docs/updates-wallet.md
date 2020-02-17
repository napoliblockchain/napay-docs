# Aggiornamenti

#### versione 1.3

    **new features**
    - #74 Logout from create/restore seed
    - #57 Napay: togli copyright nel footer e metti powered by
    - #52 Napay: prorogare scadenza iscrizione al 28 febbraio
    - #48 Napay: gestione/visualizzazione dei log delle applicazioni

    **fix**
    - #62 Napay: Settings, social compare in tutte le maschere
    - #61 Push: i messaggi sono tutti [bolt]
    - #27 Napay: inserire recaptha2 in ripristino pwd, form, bugs e login


------------------------------------------------
#### 15.01.2020 - TEST
------------------------------------------------
**Nuove features**

    - Integrazione completa con le 4 applicazioni NaPay
    - Nuova gestione issue su github (La numerazione riparte da 1)


------------------------------------------------
#### 09.08.2019 - ALLINEAMENTO PRODUZIONE E TEST
------------------------------------------------
**Nuove features**

    - Inserito nuovo controllo Login senza Privilegi di commerciante
    - Preparazione nuova funzione FastScan sulla blockchain


    - fixed bug in multiwallet

------------------------------------------------
#### 12.07.2019 - ALLINEAMENTO PRODUZIONE E TEST
------------------------------------------------

**dalla versione d16b85d (16.06.2019) alla versione 34afab6 (12.07.2019)**


    **New features**    
	- #239 : 2fa opzionale
	- funzione di inserimento, controllo e rimozione del pin per l'accesso al wallet
	- creato Comando `watchtower`  per gestire scansione transazioni su blockchain e inviare messaggi push ai
	  possessori di wallet che abbiano effettuato la sottoscrizione
	- visualizzazione conferme (240: numero di blocchi in 1 ora a 15 secondi)
	- visualizzazione balance del GAS, per evidenziare la possibilità di inviare o meno i TOKEN
	- multiple transactions management
	- new function createAccount offline
	- nuova funzione con libreria ethereum-tx [ERC20]
	- funzione di copia negli appunti indirizzo di Ricezione
	- funzione ajax in caso non funziona sw
	- aggiunto blockexplorer corretto per visualizzazione address e hash
	- block explorer senza sw
	- pulsante settings a scopmarsa
	- Storage wallet priv key
	- invio token con decrypt priv-key da js
	- new logo
	- generazione e ripristino seed

	**fix**
	- Fix Lista wallet
	- Selezionando altro wallet deve cambiare qrcode di ricezione!
	- fix sw
	- fix double ckick on send
	- fix modal dialog
	- fix clipboard copy
	- new function estimategas issue #38, #39
	- solved issue #34
	- solved issue #10

------------------------------------------------
#### 30.05.2019 - ALLINEAMENTO PRODUZIONE E TEST
------------------------------------------------
**Nuove features**        

    - multiple transactions management
    - Gestione new seed
    - Gestione ripristino old seed
    - Storage wallet priv key
    - funzione di copia negli appunti indirizzo di Ricezione
    - Vapid keys for push subscription
    - Pulsante notifica rimanda ad history
    - Completato Blockchain search
    - Nuova gestione delle notifiche WebApp
    - Selezione della camera da utilizzare
    - Predisposizione per Messaggi Push

------------------------------------------------
#### 23.04.2019 - ALLINEAMENTO PRODUZIONE E TEST
------------------------------------------------
**v0.2.2 - 23.04.2019**

    - versione 0.2.2 stable

    - push subscriptions
    - listening push messages
    - send push messages from server

    - Web push notification
        - Requesting permission
        - Showing notification
        - using  VAPID with Web Push


    - Background Sync...
        - Optimizing best caching strategy
        - Syncing Data in the Service Worker


    - IndexedDB and Dynamic Data
        - Firebase
        - Storing Fetched Posts in IndexedDB
        - IndexedDB and Caching Strategies
    - Creating a Responsive User Interface (UI)
    - Background Sync
        - Registering a Synchronization Task
        - Storing our Post in IndexedDB

    - Service worker
    - Promise and Fetch
    - Caching
        - Dynamic caching
        - Static caching
        - Optimize caching management: best practice
    - Advanced Caching
        - Offline Fallback page
        - Cache with network fallback

    - Google 2FA Login
    - Layout solo per mobile
    - Invio Token e Eth
    - Ricezione Token e Eth
    - Lista Transazioni
    - Dettaglio Transazioni
    - Creazione Nuovo Wallet
    - Selezione del wallet in uso
    - Google reCaptcha
    - Real time Balance     


## v0.0.1
**25/03/2019**
    - Initial Release
