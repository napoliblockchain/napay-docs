# Aggiornamenti


------------------------------------------------
#### 17.07.2020 - ALLINEAMENTO
------------------------------------------------

- ce79cc3 Closing Institutes Management




#### versione 1.3

	**new features**
	- #52 Napay: prorogare scadenza iscrizione al 28 febbraio
	- #48 Napay: gestione/visualizzazione dei log delle applicazioni
  - #32 Napay: mailing list ai soci x comunicazioni generiche
	- #28 Napay: Consensi: il socio deve poter modificare quello sul marketing

	**fix**
	- #62 Napay: Settings, social compare in tutte le maschere
	- #61 Push: i messaggi sono tutti [bolt]
	- #59 Napay: click su logo esce dall'applicazione
	- #57 Napay: togli copyright nel footer e metti powered by
	- #55 Napay : impostazioni pos_sin
	- #54 Napay: transaction details
	- #27 Napay: inserire recaptha2 in ripristino pwd, form, bugs e login
	- #24 Napay: col nuovo sistema di notifiche mancano le notifiche agli admin


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

    - Eliminata gestione Associazioni di Categoria
    - Creata gestione Verbali di Assemblea
    - Aggiunto allarme in caso di scadenza iscrizione.
    - Aggiunta ricerca delle province tramite inserimento del CAP
    - Aggiunti filtri di ricerca su liste transazioni, token e pagamenti
    - Aggiunta Stampa ed estrazione Excel delle liste transazioni, token, pagamenti e soci (solo per gli admin)
    - Aggiunta possibilità di pagamento quota senza effettuare operazione di logout/login


    - risolti bug

------------------------------------------------
#### 30.07.2019 - ALLINEAMENTO PRODUZIONE E TEST
------------------------------------------------
**Nuove features**

    - Aggiunto widget con i link alle applicazioni POS e Wallet TTS
    - Aggiunti nuovi grafici sulla dashboard
    - Possibilità di verificare in [Realtime] lo stato di una transazione cliccando sul pulsante dello stato relativo
    - Aggiornamento visualizzazione dello status della transazione in automatico, quando si è nel contesto do visualizzazione
    - Abilitazione dei messaggi Push nelle impostazioni utente
    - Aggiunta guida alla creazione del Wallet e del POS
    - inserito link alla GUIDA di estrazione MPK dal wallet
    - Aggiunta gestione scadenze e sollecito pagamento per gli amministratori
    - **CREAZIONE AUTOMATICA USER SU BTCPAY SERVER**
    - Inserita personalizzazione per i pagamenti tramite Paypal
    - Creata nuova dashboard per soli soci semplici
    - Completata gestione prodotti per i commercianti che utilizzano POS Desktop

    - Aggiunta installazione PWA

    - risolti bug


------------------------------------------------
#### 12.07.2019 - ALLINEAMENTO PRODUZIONE E TEST
------------------------------------------------

**dalla versione d16b85d (16.06.2019) alla versione 34afab6 (12.07.2019)**

	[new features]
	- Lista soci aggiunti FILTRI su attivi, in scadenza, scaduti
	- CREAZIONE AUTOMATICA USER, STORE e POS SU BTCPAY SERVER
	- solo admins tranne segretario, possono visualizzare pulsante per mostrare in chiaro la pwd di accesso a BPS
	  sulla lista mostrare un icona (°-°)
	- Aggiunto nuovo menù con i link al Wallet e al POS   
	- inserite guida crezione store e pos nelle notifiche
	- help in linea per la creazione di store e pos
	- mail su ipn pagamenti iscrizione in bitcoin
	- nuovo grafico pagamenti
	- corretto pulsanti dashboard
	- #183 :NUOVA DASH X SOLI SOCI,
	- Lista transazioni bitcoin e token: Data cliccabile
	- se sei un associazione di categoria non puoi visualizzare i prodotti
	- le categorie prodotti vanno per STORE e non per Merchants.
	- [admin] Nel menù impostazioni inseriti nuovi campi Vapid keys for push subscription

	[fix]
	- #229 :modifica settings account commerciante,
	- #224 :nuovo negozio la provincia è sempre sbagliata,
	- #228 :complimenti pos riceverà ai,
	- #225 :guida creazione pos, errore indicazione menu in alto a dx,
	- #223 :sitebehind tutto minuscolo,
	- #222 :user impostazioni gateway: non modificabile da utente! readonly!!
	- #221 :link al pos con jpg e invio sin tramite get,
	- #217 :dettaglio transazione conto manca n. ordine,
	- #216 :lista transazioni conto: adeguamento transazioni,
	- #219 :admin inserisce nuovo socio
	- #202 :show notifiche mobile non è centrato,
	- #205 :pulsante pagamenti con Badge non è allineato agli altri,
	- #206 :data registrazione operazione pagamento nn deve essere modificabile,
	- #207 :facilitare click sulle liste,
	- #174 :shopping: le immagini vanno suddivise x merchant,
	- #33  :Nuovo Prodotto salva: in caso di assenza immagini l'errore viene scritto 2 volte,
	- #140 :se i dati in gdpr_ (ad esempio fax ) sono vuoti esce errore in privacy,
	- #204 :visualizza/STAMPA SCHEDA UTENTE con parametri di timestamp vari,
	- #203 :users con numero di telefono    


------------------------------------------------
#### 16.05.2019 - ALLINEAMENTO PRODUZIONE E TEST
------------------------------------------------
**Nuove features**

    - Nuova Gestione `iscrizione socio` da parte degli amministratori che possono approvare o meno una nuova iscrizione
    - Salvataggio dei consensi in fase di iscrizione dei soci.

    - **Creato nuovo repository POS, esterno all'applicazione Napay principale**
    - Aggiunto pagamento iscrizione tramite Paypal
    - Aggiunto Google reCaptcha
    - Aggiunta Autenticazione a 2 fattori per il collegamento al Wallet TTS
    - Aggiunta gestione pagamenti quota associativa all'Associazione
    - Aggiunta stampa Informativa e consenso trattamento dati personali e informativa sulla privacy secondo GDPR

    - Differenziazione iscrizione tra persona giuridica e persona fisica

    - nuovo LOGO Associazione Napoli Blockchain e NaPay


------------------------------------------------
#### 06.02.2019 - ALLINEAMENTO PRODUZIONE E TEST
------------------------------------------------
    - Gestione ripristino password
    - Gestione transazioni da conto Exchange
    - Gestione Impostazioni webapp a singoli step
    - Gestione/Creazione Wallet Bitcoin personalizzato per Merchant.



## v0.0.1
**10/10/2018**
- Initial Release
