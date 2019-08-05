#### 05.08.2019
    - fixed bug in multiwallet

#### 01.08.2019
    - #270 : Aperto nuovo branch no-associazione

    - eliminato campo da np_merchants (id_association) [ALTER TABLE np_merchants DROP id_association;]
    - eliminati Controller Association, Merchants, Users, Userstytpe
    - eliminati Model Associations, DockerWallets
    - ripulite tutte le views e i controllers dove compariva Associations
    - Inserito nuovo controllo Login senza Privilegi di commerciante

    - Preparazione nuova funzione FastScan sulla blockchain

#### 12.07.2019
    - #239 : 2fa opzionale
    - adeguamento subscriptions

#### 01.07.2019
    [pinpad]
        - modificato css

#### 27.06.2019
    [issue]
        - #58

#### 25.06.2019 Nuova versione 0.4
    [pin]
        - funzione di inserimento, controllo e rimozione del pin per l'accesso al wallet

#### 20.06.2019
    [swiper]
        - rimosso perchÃ¨ rallenta troppo il sistema
    [push]
        - creato Comando `watchtower`  per gestire scansione transazioni su blockchain e inviare messaggi push ai
        possessori di wallet che abbiano effettuato la sottoscrizione
    [conferme]
        - visualizzazione conferme (240: numero di blocchi in 1 ora a 15 secondi)
    [balance]
        - visualizzazione balance del GAS, per evidenziare la possibilitÃ  di inviare o meno i TOKEN

#### 10.06.2019
    [swiper]
        - swipe pages like mobile phone

#### 31.05.2019
    [blockchain]
        - multiple transactions management

#### 30.05.2019
    [gas station]
        - lavorato su estimateGas

#### 29.05.2019
    [ERC20]
        - invio token con decrypt priv-key da js
        - storage priv-key
        - new logo
        - generazione e ripristino seed
        - fix sw
        - fix double ckick on send
        - fix modal dialog
        - fix clipboard copy
        - new function estimategas issue #38, #39
        - solved issue #34
        - solved issue #10


#### 28.05.2019
    - Gestione new seed
    - Gestione ripristino old seed
    - Storage wallet priv key

#### 27.05.2019 - new branch seed-js (with more js than php)
    [settings]
        - caricato lightwallet.min.js
        - caricato aes.js

#### 27.05.2019
    [Details]
        - aggiunto blockexplorer corretto per visualizzazione address e hash

    [Blockchain]    
        - ricerca su tutti gli indirizzi del wallet
        - block explorer senza sw

    [Settings]    
        - pulsante a scopmarsa

#### 26.05.2019
  [Ricevi token]
      - funzione di copia negli appunti indirizzo di Ricezione

  [ERC20 Send]
      - wip nonce ed altro

  [Check blockchain]
      - funzione ajax in caso non funziona sw

  [Commands]
      - Modificati in base a nuova funzionalitÃ  settings->poa_url

  [issues]
      - #22 Selezionando altro wallet deve cambiare qrcode di ricezione!

#### 23.05.2019
    [ERC20 Send]
        - nuova funzione con libreria ethereum-tx

    [Settings]
      - Fix Lista wallet: nel Model Wallet, wallet_address (unique). Da esportare
      in NaPay

#### 22.05.2019
    [createAccount]
        - new function createAccount offline

#### 20.05.2019
    [Vapid keys for push subscription]
        - vapid key website: https://web-push-codelab.glitch.me/
        - created Model for PushSubscription
        - put subscription just after user login
        - save user subscription on server

#### 15.05.2019
    [icone]
        - nuove icone - nuovo logo
    [Invio]
        - controllo invio decimali
        - salvataggio numero blocco al posto di balance
        - pulsante cliccabile (in corso/inviato)
    [Android APK]
        - creato apk android


#### 14.05.2019
    [issue]
        #19 : new row 'in corso' non Ã¨ cliccabile
        #23 : Invio -> Invio token
        #28 : disable camera on annulla click
        #24 : Nuovo Balance non funziona sottrazione
        #20 : camera principale
        #3  : impostazioni:messaggio di conferma cambio Wallet predefinito
        #21 : Error 404 Il sistema non ha potuto trovare l'azione "about" richiesta.

    [sw]    
        Pulsante push rimanda ad history

#### 13.05.2019
    [Ricevi]
        issue #30 : disabilitare pulsante ricevi
        issue #29 : richiesta notifiche push all'vvio
        issue #25 : wallet predefinito tasto conferma a dx
        issue #17 : logout blocca app


#### 10.05.2019
    [SW]
        - Completato Blockchain search

#### 09.05.2019 New branch blockchain-search
    [SW]
        - cerca dall'ultimo blocco salvato in db le transazioni relative
            al wallet dell'utente
            ALTER TABLE `np_wallets` ADD `blocknumber` VARCHAR(50) NOT NULL DEFAULT '0x0' AFTER `poa_port`;

#### 09.05.2019
    [webcam]
        - Selezionando altra camera cambia visualizzazione front/rear
    [sw]            
        - no cache su history

#### 08.05.2019
    [Notifications]
        - Nuova gestione delle notifiche WebApp
    [WebCam]
        - Selezione della camera da utilizzare

#### 07.05.2019
    [ERC20]
        - Visualizzazione esclusiva dell'erc20 e non dell'ether


#### 07.05.2019
    [ERC20 Transactions]
        - Risolto problema di salvataggio importo in ricezione ERC20
        - issue #16 : transazioni cliccabili sui pulsanti
        - cambio colori 'invio' 'ricezione' ecc.
        - Riaggiustato command send & receive per eth e erc20
        - Issue #6 : RICEVI: se si riceve piÃ¹ volte senza fare il refresh della pagina l'ultimo prezzo sovrascrive anche i precedenti


#### 06.05.2019
    [Wallet history]
        - issue #14 : dataProvider criteria must show all transactions
        - issue #12 : menu history al 100%
        - fixing camera qrcode for android
        - issue #8 : id wallet criptato

#### 03.05.2019
    - Nuovo Pulsante 'Abilitazione Messaggi Push' in Settings.
    - Predisposizione per libreria Messaggi Push da Server
    - web-push-php libreria installata

#### 30.04.2019
    - Login: number field to google 2fa
    - syncing check txpool
    - error messages on send
    - issue #9 : cambiare chiavi private cryptoURL

#### 29.04.2019
    - issue #7 : notifications view- il link riporta alla cartella wallet-tts.

### V 0.2.0 - 23.04.2019
    - versione 0.2.2 stable

#### 17.04.2019
    - push subscriptions
    - listening push messages
    - send push messages from server

#### 16.04.2019
    #151 Storing Subscription
     setup npm firebase-tools firebase-admin web-push
     firebase deploy  

#### 15.04.2019
    - issue #4 : solved: impostazioni: nuovo Wallet generato deve essere wrapped se lenght ã€‹200px
    - Web push notification
        - Requesting permission
        - Showing notification
        - using  VAPID with Web Push

#### 12.04.2019
    - Background Sync...
        - Optimizing best caching strategy
        - Syncing Data in the Service Worker

#### 11.04.2019
    - IndexedDB and Dynamic Data
        - Firebase
        - Storing Fetched Posts in IndexedDB
        - IndexedDB and Caching Strategies
    - Creating a Responsive User Interface (UI)
    - Background Sync
        - Registering a Synchronization Task
        - Storing our Post in IndexedDB

#### 10.04.2019
    - Service worker
    - Promise and Fetch
    - Caching
        - Dynamic caching
        - Static caching
        - Optimize caching management: best practice
    - Advanced Caching
        - Offline Fallback page
        - Cache with network fallback

#### 09.04.2019
    - issue #1 : rimuovere footer
    - issue #2 : transazioni non ha css card

#### 08.04.2019
    - node module installed
    - manifest.json
    - pwa Service Worker
    - App Install Banner

#### 26.03.2019
    - Google 2FA Login
    - Layout solo per mobile
    - Invio Token e Eth
    - Ricezione Token e Eth
    - Lista Transazioni
    - Dettaglio Transazioni
    - Creazione Nuovo Wallet
    - Selezione del wallet in uso

    - PWA Progressive Web App
        https://medium.com/dev-channel/learn-how-to-build-a-pwa-in-under-5-minutes-c860ad406ed

    - Google reCaptcha
    - Real time Balance     


### V 0.0.1 - 25.03.2019
    Initial Release
