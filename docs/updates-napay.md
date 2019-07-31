# Aggiornamenti

#### 31.07.2019

    - #270 : Aperto nuovo branch no-associazione

    - eliminato campo da np_merchants (id_association) [ALTER TABLE np_merchants DROP id_association;]
    - eliminati AssociationController, Association model, association views
    - eliminato Associations da MerchantsController
    - modificata _form_ in merchants
    - eliminato $merchants->id_association da UsersController
    - fix bug in New Store che caricava i merchants eliminati
    - fix merchant e store creati da admin
    - ripulite tutte le views e i controllers dove compariva Associations
    - spostata funzione CreateBPSUser in classe Napay


------------------------------------
- ALLINEAMENTO TEST


#### 30.07.2017
    - #282 : lista pagamenti per singolo socio non filtra!
    - Creata nuova tabella st_verbali
    - Generata Gestione Verbali

#### 24.07.2019
    - #279 : versioning da file di testo
    - #234 : Aggiunto alert scadenza napay.
    - In caso di rinnovo del pagamento, si aggiunge la differenza dei giorni di scadenza alla data
    di scadenza effettiva
    - Ricerca Provincia da CAP, anche in new Merchant e new Store

#### 23.07.2019
    - #269 : filtro su transazioni, token e pagamenti
    - #278 : widget link wallet nn funziona
    - #280 : storno ricevute non ha senso: eliminare
    - #273 : paga quota: pulsante paga quota, quando si Ã© loggati si deve poter effettuare un nuovo pagamento
    - #153 : quote: invio via mail della ricevuta (NON NECESSARIO)
    - #155 : stampa lista transazioni token ed altri elenchi

#### 22.07.2019
    - #277 : Pagamento quota, verificare salvataggio n. invoice. DEVE essere salvato solo dopo la verifica del pagamento!!!
            e SOLO se lo stato della notifica Ã¨ diverso dallo stato precedente, altrimenti salta numeri!!!
    - #272 : paga quota: sostituire cgridview con clistview per mostra solo ultimo pagamento valido + pulsante download ricevuta
    - #272 : fix aggiornamento con F5 della pagina, aumentava il numero della ricevuta +1 !!!
    - #260 : Pagamento quota, tasto logout
    - #232 : Ricerca Provincia da CAP
    - #263 : idstore e sin creano confusione
    - #264 : notifiche: icona $ diventa btc
    - #267 : notify scaduto check esclamation mark
    - #268 : pulsante apri pos rimanda a .it su tk
    - #265 : notify help crea pos -ã€‹ Attiva pos
    - #266 : notify help wallet 2fa -ã€‹maggiore sicurezza
    - #275 : Lista negozi da ADMIN non mostra i commercianti
    - #274 : Dettaglio utente da ADMIN non deve mostrare 2fa e notifiche push
    - #271 : menu: icona $ diventa btc (anche su POS)
    - #269 : filtro su transazioni: in corso da non mostrare


------------------------------------
- ALLINEAMENTO PRODUZIONE E TEST
------------------------------------


#### 17.07.2019
    - #255 : nuova richiesta di pagamento btc ha icona sbagliata (modificato set icone)
    - icone Widget puntano all'indirizzo sul dominio in uso (it su it, tk su tk, ecc.)
    - #258 : pulsante su transazione si deve attivare sempre escluso su completato
    - #256 : nuovi grafici dashboard
    - icone su lista notifiche

#### 15.07.2019
    - #253 : dashboard vendite totali funziona solo su paid e non confirmed
    - #252 : aggiornamento visualizzazione status della transazione in automatico
    - #254 : Settings USER: Abilitazione Push subscriptions (con cambio della tabella np_vapid_subscription)
             INVIO messaggi push tramite IPN


#### 11.07.2019
    - #245 : concluso
    - #251 : dopo creazione pos automatico non funziona pos invoice
    - #250 : file:///css/images/napay-yellow.png
    - #249 : guida wallet alert in alto su dashboard
    - #248 : notifiche: dopo aver creato il pos...
    - #246 : ipn bitcoin iscrizione invia sempre email

#### 10.07.2019
    - inserito ID Negozio in visualizzazione store
    - Il Nome del POS Ã¨ univoco per singolo Store
    - fix BTCPay class
    - inserito link alla GUIDA di estrazione MPK dal wallet
    - #245 :visualizzare pulsante per mostrare in chiaro la pwd di accesso a BPS


#### 09.07.2019
    [issues]
    - #244 :promemoria non invio indirizzo email
    - #243 :lista soci filtri
    - #242 :lista soci errore scadenza se presenti piÃ¹ pagamenti
    - #214 :scadenze e sollecito pagamento
    - #241 :togliete nome da lista pagamenti in caso di pagamenti filtrati x utente
    - #240 : classe gestione remota BTCPay server FUNZIONANTE!

#### 08.07.2019
**CREAZIONE AUTOMATICA USER SU BTCPAY SERVER**
- CREAZIONE USER, STORE, PAIRING
    - issue #240 : nuova classe per accesso a BTCPay Server da remoto (da continuare...)
        1. Admin Conferma USER  
            a. crea merchant
            b. crea user btcpay server (da ora in poi BPS)
        2. Admin o user CREA Store
            a. crea store
            b. crea store su BPS
        3. admin o user crea POS
            a. crea pos
            b. crea pairings su BPS

        1. Nuovi parametri di configurazione webapp x BPS (servono per creare i nuovi user su BPS)
            a. admin email => bps_admin_email
            b. admin password => bps_admin_password

            Creazione nuova tabella `np_bps_users`
            -   id_bps_user
            -   id_merchant (unique)
            -   bps_auth crypted (32) chars
        2. Modifica tabella `np_stores`
            -   aggiunta campo bps_storeid (char 50)
            a. creo in np_stores il Negozio
            b. creo lo store su BPS
            c. salvo il bps_storeid in np_stores
        3. creo pos inserendo MPK. Invece del messaggio di attesa del SIN, mostrare pulsante "CONVALIDA"
            che effettua il pairing .

    - lista merchants
        solo admins tranne segretario, possono visualizzare pulsante per mostrare in chiaro la pwd di accesso a BPS
        sulla lista mostrare un icona (Â°-Â°)

#### 05.07.2019
    [bugfix]
    - #237 :rinominato sitebehind in payfee per risolvere problema di maiuscole e minuscola windows Linux
    - FIX COINGATE VERSION ERROR
    - #235 :in register in caso di errore deve salvare i campi. soprattutto corporate e denominazione
    - #231 :STORNO Fatture: dEVE ESSERE emessa una nuova fattura con importo NEGATIVO, pari all'importo da restituire!
    - #230 :nn esce pulsante cancella user dopo aver cancellato pagamento. in realtÃ  un user non puÃ² essere cancellato dopo che c'Ã¨ stato un pagamento, che a sua volta non puÃ² essere cancellato. deve rimanere traccia. inoltre si bloccherebbe l'applicazione che non trova corrispondenza tra pagamenti e user, ecc. ecc.
    - #214 : Invio SOLLECITO A SINGOLO UTENTE
    - Visualizzazione SOCI limitata ai soli Attivi. Pulsante per visualizzare tutti, anche i non paganti, scaduti, ecc.

    [wip]
    - da completare mail x pagamenti in scadenza

#### 03.07.2019
    [bugfix]
    #229 :modifica settings account commerciante,
    #224 :nuovo negozio la provincia Ã¨ sempre sbagliata,
    #228 :complimenti pos riceverÃ  ai,
    #225 :guida creazione pos, errore indicazione menu in alto a dx,
    #223 :sitebehind tutto minuscolo,
    #226 :inserire guida nelle notifiche,
    #227 :menu: links a wallet e pos

#### 02.07.2019
    [bugfix]
    #222 :user impostazioni gateway: non modificabile da utente! readonly!!
    #210 :help in linea,
    #221 :link al pos con jpg e invio sin tramite get,
    #217 :dettaglio transazione conto manca n. ordine,
    #216 :lista transazioni conto: adeguamento transazioni,
    #213 :grafico sui tipi di pagamento

#### 01.07.2019
    new README & LICENSE

    [issues]
        - #219 :admin inserisce nuovo socio

    [help in linea]
      - wip...

#### 25.06.2019
    [issues]
        - #211 :togliere # da lista transazioni
          #212 :togliere #xx in dettaglio transazione

#### 21.06.2019
    [pagamenti]
        - stato in `paid` su fatture immesse manualmente
        - mail su ipn pagamenti iscrizione in bitcoin
        - modificata tabella st_pagamenti
        - allineati pulsanti
        - nuovo grafico

#### 20.06.2019
    - modificato Ngatepay => NaPay
    - corretto pulsanti dashboard
    - inserito Impostazioni PayPal

#### 18.06.2019
    [POS SIN]
    1. Utente inserisce Master Public Key
    2. Admin riceve mail di notifica
    3. Admin effettua Pairing
    4. User riceve mail e visualizza il SIN.

    - modificata tabella np_pos: aggiunto campo MPK (varchar 250)

    [DaSH]
    1. Lista transazioni scorrevoli su mobile.
    2. Lista transazioni bitcoin e token: Data cliccabile

    [issues]
    #202 :show notifiche mobile non Ã¨ centrato,
    #183 :NUOVA DASH X SOLI SOCI,
    #205 :pulsante pagamenti con Badge non Ã¨ allineato agli altri,
    #206 :data registrazione operazione pagamento nn deve essere modificabile,
    #207 :facilitare click sulle liste,
    #201 :dashboard: lista trans e token nn scorre su mobile,
    #174 :shopping: le immagini vanno suddivise x merchant,
    #33  :Nuovo Prodotto salva: in caso di assenza immagini l'errore viene scritto 2 volte,
    #140 :se i dati in gdpr_ (ad esempio fax ) sono vuoti esce errore in privacy,
    #204 :visualizza/STAMPA SCHEDA UTENTE con parametri di timestamp vari,
    #203 :users con numero di telefono


#### 14.06.2019
    [products]
    - se sei un associazione di categoria non puoi visualizzare i prodotti
    - le categorie prodotti vanno per STORE e non per Merchants. (modificata
      tabella np_products_categories); eliminati campi id_merchants e deleted
    - cambiata la tabella np_products: aggiunto id_store

#### 12.06.2019
    [Login page]
        - nuova pagina di login

    [service worker]
        - impostazione sw solo per installazione app PWA. Logout funzionante!

    [transactions]    
        - link su invoice di btcpayserver

#### 05.06.2019
    [Impostazioni WebApp]
        - aggiunti 2 nuovi campi di impostazioni progressivo Ricevute per i pagamenti

#### 03.06.2019
    [APPROVE USER]
        - Quando l'admin approva un utente, se questo Ã¨ corporate viene creato in automatico l'account commerciante

#### 31.05.2019
    - tolta pagina about
    - tolta pagina contatti
    - modificate immagini/loghi etc.
    - abilitato download pagamenti solo x effettivamente pagati
    - uniformati colori notiche con wallet

    issue #178 : bagde su pulsante pagamenti


#### 30.05.2019
    [register user]
        - Fine

    [merchant/create]    
        - eliminata generazione indirizzo token!
        - abilitato caricamento dati giÃ  presenti in anagrafe per non ripetere immissione dati
        - mostrata maschera di logout e login x nuovo commerciante in autonomia

    [wallet bitcoin]    
        - eliminato dal menu

#### 29.05.2019
    [register user]
        - wip...

#### 28.05.2019
  [token]
    -  link per explorer su hash e address

#### 26.05.2019
  [poa]
    - adeguamento utilizzo nuovo url settings->poa_url

#### 24.05.2019
    [Mail]
        - configurata nuova password invio mail Register.it

    [Registrazione]
        - Nuovi check point regole Statuto e termini di utilizzo

    [Users]    
        - email rifiuto fix
        - fix bug visualizzazione utenti in attesa di registrazione


#### 20.05.2019
    [new db model]
        - creata nuova tabella PushSubscriptions (file in mysql)

#### 17.05.2019
    [issues]
        issue #173 : adeguamento selezione provincia e comune ad altre views
        issue #53 : wallet notifiche: x l'admin non vede chi invia e riceve
        issue #72 : users: permetterne la cancellazione
        issue #163 : eliminato pulsante Wallet Bitcoin. dopo test estrazione wallet bitcoin in nuova applicazione


    [Associations]
        - bugfix: creazione nuovo token
        - adeguamento province - comuni

    [Merchants]
        - bugfix: creazione nuovo token
        - adeguamento province - comuni

    [Stores]
        - bugfix: creazione nuovo token
        - adeguamento province - comuni    

    [Token]    
        - adeguamento json response al Wallet-TTS



#### 16.05.2019
    [mail]
        - new class sendmail
        - invio mail a user in fase di registrazione account
        - invio mail agli admin in fase di registrazione nuovo utente

    [Soci]
        - nuovo menÃ¹ `richieste iscrizione` mostra gli utenti che si sono iscritti ma
          non ancora attivi. L'admin seleziona l'utente e:
            a. approva la sua iscrizione -> parte email per user con istruzioni di pagamento
            b. nega l'iscrizione -> chiede motivazione e parte email per user

        - Lista soci mostra solo quelli attivati
        - issue #167 : gestione soci: pulsante quote. Dettaglio Socio, mostra pulsante pagamenti
            da cui si accede alla lista dei pagamenti del solo socio selezionato.

        - Nel dettaglio socio, se non Ã¨ mai stato attivato Ã¨ presente il pulsante di Eliminazione
        - Eliminazione utente   
        - issue #171 : users - cambio carica: cambia solo users_type ma non id_carica

    [Pagamenti]
        - visualizzazzione lista per singolo utente
        - Update Pagamenti
        - create Pagamenti da pulsante Soci

    [generale]     
        - issue #169 : transazioni token/bitcoin/pagamenti cliccabili

    [Register user]    
        - prevista seleziona prima della provincia e poi del comune



#### 15.05.2019
    [User Register Form]
    ... to be continue...

    [POS]
    - chiusura branch POS...


## Cambio workflow
#### 14.05.2019
    [Iscrizione] -
        1. User si iscrive (salvataggio timestamp conferma privacy)
        2a. User riceve mail di attesa verifica iscrizione
        2b. Admin riceve mail di verifica iscrizione
        3. Amministratore approva o annulla iscrizione
            a. [Non Approva] User riceve mail istruzioni su cosa deve correggere
            b. [Approva] User riceve mail istruzioni come pagare
        4. User effettua pagamento
            a. bitcoin/paypal : inserimento quota automatica.
                I. User riceve mail per effettuare il login
                II. Admin riceve mail di pagamento ricevuto
            b. bonifico/contanti : iscrizione manuale da parte di Administrator
                I. User riceve mail per effettuare il login


#### 08.05.2019
    [POS]
        - creazione del branch POS. Inizio estrazione POS. La cancellazione
            dei file, viene rimandata alla successiva fase di testing della
            app POS forkata all'occorrenza
        - rimodulazione della pagina di Login

    [Notifications]
        - Nuova gestione delle notifiche WebApp

    [Transactions/token]
    - Nuova funzione di aggiornamento STATO Transazioni Tokens         

#### 06.05.2019
    [Site/Activate]
        - issue #168 : google 2fa nn funziona

#### 03.05.2019
    [Pagamento quota]
        - preparato ipn for Paypal
        - Paypal: inserite chiavi per "Produzione"
        - bugfix messaggio errore bitcoin
    [Merchant]    
        - bugfix 'nuovo indirizzo token'

#### 02.05.2019
    - issue #166 : register administrator - non visualizzare modulo cartaceo
    - issue #162 : nuovi controller SiteBackendController e SiteBehindController
    - validatore response getBalance Bitstamp
    - nuovo DATABASE VUOTO PER INSTALLAZIONE DA ZERO

#### 04.04.2019 Paypal Integration
    - added PayPal-PHP-SDK Library
    - set permission=0 a st_tipo_pagamenti 'Paypal', id_tipo_pagamento MUST BE (2)

#### 01.04.2019
    - google reCaptcha2 al posto del codice di conferma su tutti i Login
        - LOGIN
        - Register
        - Recupera password
        - Paga iscrizione
        - Contatti
        - POS
    - issue #160 : wallet: eliminato wallet da n-pay
    - rimodulato menÃ¹: spostata Quota Associativa nel menÃ¹ Amministrazione per tutti
    - ripristinato funzionamento Keypad Desktop
    - issue #145 : pos desktop e mobile hanno diversi controllers?

#### 29.03.2019
    - bugfix nuovo socio vede vecchie notifiche
    - bugfix User register form
    - issue #148 : wallet: da separare e accesso solo con two factor authentication

#### 26.03.2019
    - bugfix new wallet

#### 25.03.2019
    - issue #156 : cambio password NON CAMBIA PASSWORD
    - wallet balance error: cancello messaggio errore su nuova selezione wallet
    - exporta Tokens Excel
    - esporta Transazioni Conto Excel
    - esporta lista Fatture Excel
    - esporta quota Associativa Excel
    - issue #151 : quote: in modifica l'importo Ã¨ 0
    - esporta lista SOCI Excel
    - issue #150 : quote: segretario non puÃ² modificare nÃ© cancellare la quota
    - segretario non puÃ² modificare impostazioni webapp

#### 22.03.2019
    - wallet eth e token SEND + ipn
    - Esporta Transazioni in excel

#### 21.03.2019
    - NUOVA GESTIONE ETH E TOKENS : modificata tabella np_tokens aggiunto campo
        type, per gestire ether o token
        modificati gli inserimenti in type_notifications nelle notifiche

        type_notifications :    1. token
                                2. ether
                                3. crypto
                                4. fattura

        np_tokens -> type:      1. token
                                2. ether

    - modificati i Command token e wallet in Receive e Send
    - issue #152 : quote: icona pdf +piccola                            

#### 19.03.2019
    - FATTURE: cosÃ¬ come sono concepite servono all'Associazione a fatturare
    gli importi (in percentuale) sulle transazioni dei clienti.
    L'Associazione genera le fatture selezionando le transazioni desiderate e il
    commerciante le puÃ² visualizzare.
    Al momento questa funzione si attiva esclusivamente compilando il campo Percentuale
    e indirizzo bitcoin di ricezione nelle impostazioni della webapp.

    - PAGAMENTI QUOTA ASSOCIATIVA: i pagamenti riguardano le ricevute che l'Associazione
    rilascia in seguito ad una iscrizione di un socio. Viene generata manualmente in
    caso di pagamenti cash, altrimenti Ã¨ il sistema stesso che la genera (ad esempio
    dopo un pagamento in bitcoin). Queste ricevute sono esenti da imposte.

#### 18.03.2019
    - issue #149 : wallet btc - velocizzare accesso
    - 2fa google auth - cambiare tabella np_users (aggiungere ga_secret_key)
    - completato in settings utenti creazione e rimozione 2fa
    - bugfix nuovo socio

#### 14.03.2019 - 15.03
    - wallet token: separazione funzioni eth_ erc20_
    - ERC20_Token.php modifica x funzionare in ufficio (decimals, 2);
    - lavorazione ERC20 ...
    - some bugfixes su ipn wallet e tokens
    - issue #146 - update.sh
    - issue #147 : nuova libreria

#### 11.03.2019
    - issue #144 : aggiunto poa_abi e poa_bytecode per lo smart contract del token
    - inserito modello cartaceo ISCRIZIONE SOCIO

#### 07.03.2019
    - issue 139 : wallet token: funzione di controllo sull'indirizzo inserito
    - nuovi settings GDPR per Associazione
    - informativa sulla privacy secondo GDPR
    - stampa Informativa e consenso trattamento dati personali
    - issue #136 : Informativa sui cookies Cookie law

#### 06.03.2019 [persona-giuridica]
    E' necessario modificare la tabella np_users con diversi campi...
    1. persona_giuridica (si/no) 1/0
    7. denominazione: varchar (250)
    2. codice fisclae/p.iva: vat varchar(250)
    3. indirizzo: address varchar (250)
    4. cap: cap varchar (250)
    5. city: varchar (250)
    6. country (stavolta scritto bene): varchar (250)

    - Settings webapp: quota d'iscrizione differenziata per Privato o societÃ (persona fisica/giuridica)
    - issue #135 : impostata Ricevuta per iscrizione socio

#### 06.03.2019
    - issue #134 : Script configurazione
    - issue #138 : settings user : banca, cambiare colore ad avviso
    - riorganizzato immagini in main.php

#### 05.03.2019
    - aggiunto in impostazioni webapp smart_contract
    - issue #131 : Favicon associazione
    - issue #130 : Impostazioni visualizzare IBAN
    - issue #129 : Wallet bitcoin TESTNET TOGLIERE!!!
    - issue #125 : Lista fatture solo se presente % associazione
    - issue #127 : Lista pagamenti - stampa ricevuta

#### 04.03.2019
    - issue #133 : Orologio con nuovo tema Ã¨ disallineato
    - pagamenti quota. lista differenziata se utente o amministratore! (aggiunto campo in st_tipo_pagamenti, permission (int 11))
    - issue #132 : Email su pagamento quota associativa

#### 02.03.2019
  - issue #116 : nuovo commerciante, Nel caso in cui non ci sono utenti soci selezionare esce errore costituenti
  - issue #117 : nuova associazione, Deve selezionare solo gli utenti soci. Fare attenzione All'errore se mancano utenti soci
  - issue #118 : modifica negozio, Nn esce il menÃ¹ a tendina su cittÃ
  - risolto bug visualizzazione cittÃ  su associazione in presenza di NO ASSOCIAZIONE con valori non impostati
  - issue #119 : Socio type 5, Il menÃ¹ Ã¨ tutto sballato. Probabile che funzioni x desktop ma x mobile nn l'ho corretto
  - issue #121 : Lo user non diventa merchant (2) ma resta socio(5)
  - issue #122 : Mettere avviso che bisogna scollegarsi e rifare il login x rendere attivo lo stato di merchant.
  - issue #123 : Wallet Token mobile, il logo Ã¨ quello vecchio
  - issue #126 : Merchant Ã¨ anche socio, mostrata la lista dei pagamenti x l'iscrizione.
  - issue #128 : nuovo negozio, cittÃ  numerico

#### 01.03.2019
    - issue #114 : keypad logo va su dash
    - cambio tema con lumen.css + configurazione nuovi colori!
    - issue #115 : logo npay troppo lungo
    - token command con numeri float
    - issue #112 : ipn full
    - issue #7 : DECIMALI TOKEN: Dipende dalla POA o dal pos ?

#### 28.02.2019
    - nuovo LOGO Associazione Napoli Blockchain e N-Pay

#### 27.02.2019
    - Socio: visualizzazione propri pagamenti. Creazione commerciante.
    - Pagina login con pulsanti a scomparsa!
    - issue #110 : LOGIN SOCIO: CONCLUSO!

#### 26.02.2019
    - issue #108 : Lista notifiche esce confirmed. Aggiornare funzione
    - modificata visualizzazione testo su dashboard con diverse risoluzioni
    - cambiate icone menu utente
    - prodotto documentazione software
    - issue #70 : categorie vanno divise x merchant
    - issue #71 : prodotti  vanno divisi x merchant
    - issue #110 : LOGIN SOCIO dopo pagamento. Gestione visualizzazione pulsanti ed azioni
        per il singolo socio NON commerciante!

    - Administrator crea commerciante da lista in cui compaiono SOLO i soci!
    - Administrator non cambia password, bensÃ¬ invia un reset link all'utente    
    - Socio: gestione e creazione Commerciante...

#### 25.02.2019
    - issue #111 : Utente/commerciante settings token separato in pulsante
    - issue #103 : merchant user impostazioni: non salva il wallet principale!!!
    - issue #104 : Admin puÃ² cambiare la carica dell'utente
    - issue #106 : Nuova fattura importo. Al posto di prezzo
    - issue #107 : Nuova fattura inserisci. Il campo city Ã¨ numerico. Anche nel pdf

#### 20.02.2019
    - keypad new font & layout changes
    - keypad shopping: nascosti impostazioni utente! visibile solo logout
    - keypad shopping: schermata modal dopo pressione tasto "Conferma" acquisto

#### 18.02.2019
    - issue #102 : grafici separati token e btc
    - issue #101 : errore onlyforbitstamp liquidation address
    - issue #100 : versioning software obbligatorio
    - Processo di stampa: per stampare la ricevuta dell'invoice pagata DEVO salvare
        per prima cosa in locale la transazione che sta avvenendo. Quindi il procedimento
        sarÃ :
            1. creo transazione su db vuota e recupero il solo id_transaction
            2. imposto il redirectUrl con l'id della transazione vuota (new)
            3. creo transazione su btcpayserver
            4. aggiorno la transazione su db con i dati di btcpayserver
            5. adesso il redirect url contiene l'id della transazione
            6. quando ritorno su webpos/keypad?id=id_transaction verifico che sia stata effettivamente
                pagata. In tal caso stampo la ricevuta.

#### 16.02.2019
    - issue #98 : grafico pos step errato
    - issue #97 : Settings visualizza valido!!! ;-)
    - wallet btc - confirm cambiato colori
    - issue # 95 : Dettagli negozio vanno aggiornati
    - cambio password for administrators & users
    - dettaglio utente: stato dei pagamenti
    - issue #92 : Recupero password: email cambiare object benvenuto!!!
    - issue #73 : recupero password schermata modificata
    - settings account commerciante anche per commerciante e nn solo per administrators
    - issue #94 : Lista commercianti: attivo deve far riferimento ai pagamenti e nn all'account

#### 15.02.2019
    - layout sin pos
    - new electrum Class

#### 11.02.2019
    - creazione docker electrum versione 3.3.3
        git clone https://github.com/osminogin/docker-electrum-daemon.git
        cd docker-electrum-daemon
        docker-compose build --build-arg VERSION=3.3.3
        docker tag 638a2b976ddc  _[ngatepay/electrum:latest]_
        docker rmi docker-electrum-daemon_electrum

        //QUESTO Ã¨ IL COMANDO CHE VA IN DockerController.php
        docker run --rm --name electrum-iduser[xy] --publish 127.0.0.1:70xy:70xy --volume /srv/electrum:/data  _[ngatepay/electrum:latest]_

#### 08.02.2019 v1.2.14
    - [//rimossi  e rimessi dati bancari da user settings]
    - bugfix Salvataggio Usersettings in Merchants
    - creata classe Electrum per unificare i comandi docker
    - inserita tabella Comuni Italiani
    - pulsante iscrizione in home page login
    [HISTORY]
    {
        "summary": {
            "end_balance": "0.10460817 BTC",
            "end_date": null,
            "expenditures": "0. BTC",
            "income": "0.10460817 BTC",
            "start_balance": "0. BTC",
            "start_date": null
        },
        "transactions": [
            {
                "balance": "0.10460817 BTC",
                "confirmations": 7,
                "date": "2019-02-08 20:19",
                "height": 1456326,
                "label": "",
                "timestamp": 1549653561,
                "txid": "442123b68baf367dc7d46c85077c25ad09480fa74705cb9d52e714a3c1df8910",
                "txpos_in_block": 7,
                "value": "0.10460817 BTC"
            }
        ]
    }


    [PAYTO]
    {
    "complete": true,
    "final": true,
    "hex": "010000000311521a6233fef5da24e120b7b25f40e4115ef7704cf3bd0982b827ce68125613000000006a47304402202331b0f1550e56f3945a359dba4974a1d5c3882154c95044982dd6a43fea3a7f02203c75d320c614d6a32db652321d68d53d9b6e8e1962cee21e78d8a13629dc126301210304af19f024e173b51548ecc0d2ad839861e0f54221fc741181276c1c26d5d346feffffff5c379d4446b43a99e2cd9c8f29527adfe4242bcc337160ab69ad324861daa08c000000006a47304402206e1e81ecad69dd2c1b5dec7e32f86ae10d684beb94fa6a2bcf9a8e08f5447c220220140f063a6facec7880ee173d5fd25a276ac9cfd6571f376cbbab5403ce8825d601210213d467f4b11eea4e4a4cb45887643d25f204a9d99fa4deef8aeface22545b29afeffffff3100d7d36983915ab7db013943fcdb60ed043760a3feec61f8944f1cf3e0dc8e000000006a47304402201a8686df200d65b2333b5fea379a3b6ce4125676eecba446edb278317ff3f9a8022043525095a69814599a49105f6abcbb8bf5d22f03a64e3f2e63e38f390d3a112601210304af19f024e173b51548ecc0d2ad839861e0f54221fc741181276c1c26d5d346feffffff028e1c0000000000001976a914e809d414a942c3eb0319c0e760149094066855ae88ac409c00000000000017a914fc6046284bffbb8da5c838f9bfbf5fdab8d8c6298707940800"
    }

    resta da verificare la tx e il broadcast della tx con electrum...
    serve un wallet collegato ad internet !!!!!!!!!!!!!!!!!!!

#### 07.02.2019 v1.2.13
    - settings: dati bancari x trasferimento su proprio conto corrente
    - unificato dati country con nuova funzione in merchants, stores , banks
    - visualizza indirizzi in configurazione wallet merchant
    - wallet btc - invio btc...

#### 06.02.2019 v1.2.12
    - #83 : settings utenti: trasforma come SettingsWebapp
    - password regenerate
    - wallet btc
    - send mail

#### 05.02.2019 v1.2.11
    - creata visualizzazione transaction su conto exchange
    - gestione wallet btc->cambio su exchange

#### 04.02.2019 v1.2.10
    - Gestione Impostazioni webapp a step
    - issue #84 : settings webapp: distinguere 2 btcpayserver(1 x associazione l'altro x l'utente)
    - issue #86 : settings wallet bitcoin user spostati in settings webapp
    - modificata gestione creazione wallet bitcoin Merchant con nuove disposizioni Settings WebApp
    - modificata tabella docker_wallets eliminati i campi  
                 * @property string $rpcuser
                 * @property string $rpcpassword
                 * @property string $rpchost
                 * @property string $rpcport
    - issue #85 : settings web app: impostare a step come x il wallet bitcoin del merchant
    - issue #89 : notifiche. token da keypad si aggiorna status ma non riceve notifica             
    - issue #88 : nuova mail ngatepay, configurata pwd per accesso da app. configurato main.php

#### 01.02.2019 v1.2.9 - Master Public Key - Wallet bitcoin
    - Gestione/Creazione Wallet Bitcoin personalizzato per Merchant. Questa funzione
        crea l'immagine docker personalizzata per utente, crea il wallet electrum,
        visualizza il seed, attiva il wallet, visualizza la Master Public Key.
    - Creata nuova tabella docker_wallets
    - Necessario installazione tmux (apt-get install tmux)

#### 31.01.2019 v1.2.8
    - registrato nuovo ipn per btcpayserver e pagamenti
    - nuovo login per utente non pagante
    - creata funzione Contatti per invio yiiMail
    - pulsanti di TEST per admin per verificare ipn
    - riorganizzate cartelle x activate, contact, homepage, pagaiscrizione, about, recoverypassword, register
    - modificata visualizzazione Registrazione, Activate,
    - preparato documento di presentazione NaPay
