# Napay

### Progressive Web App - v. 1.4

##### Informazioni tecniche

L’applicazione ha ~~6~~ **5** diversi profili utente con privilegi differenti.

- *Amministratore*
- ~~*Associazione di categoria*~~
- *Commerciante*
- *Socio*
- *POS (profilo associato al commerciante)*
- *WALLET (profilo associato al commerciante)*

Ogni utente può avere **uno** solo dei citati profili.

I profili Amministratore ~~e Associazione di categoria~~ non possono essere utilizzati per l’operatività del programma, non sono abilitati cioè ad operare per ricevere bitcoin nè Token TTS.

~~Mentre i~~Il profilo Amministratore può gestire tutte le impostazioni del software.~~, chi ha un profilo Associazione di categoria è abilitato alla sola visualizzazione delle transazioni dei commercianti ad essa collegati.~~

I profili Commerciante, POS e WALLET sono strettamente collegati tra di loro. Mentre con l’account Commerciante potrò visualizzare le transazioni, gestire i wallet bitcoin e del token, visualizzare le fatture, caricare le immagini dei prodotti, ecc. ecc. il profilo POS serve a generare le transazioni per ricevere le cryptovalute. Il profilo WALLET mi permette di utilizzare il wallet del Token TTS.

I soci possono avere le seguenti cariche statutarie:


| Amministratore  | Commerciante/Socio |
| :-------------: | :----------------: |
|   Presidente    |  Socio fondatore   |
| Vice-presidente |  Socio ordinario   |
|    Tesoriere    |   Socio onorario   |
|   Segretario    | Socio sostenitore  |


I soci con la carica di Presidente, Vice-presidente, Tesoriere e Segretario hanno la funzione di amministrazione del sito ~~e possono essere collegati al profilo Associazione di categoria~~.

Al Segretario è inibita la possibilità di modificare i pagamenti ricevuti e non può effettuare modifiche sulle impostazioni della Webapp. Il Segretario può, invece inserire nuovi soci e creare nuovi pagamenti.

I profili di amministrazione non possono essere legati in nessun caso a quelli operativi di commerciante, negozio o ad un POS. Gli utenti con la carica di socio fondatore, onorario, ordinario e sostenitore possono essere utilizzati sia per il profilo di socio semplice ~~Associazione di categoria~~ che per quello di Commerciante.

I profili di amministrazione sono esentati dal versamento della quota di iscrizione.

Gli altri 4 profili, dovranno ottenere l'approvazione da parte dell'Amministratore. I soci dovranno effettuare il pagamento della quota associativa in bitcoin o altra forma di pagamento. L'amministratore può anche rifiutare di approvare un nuovo iscritto, con la dovuta motivazione.



## Guida operativa per gli amministratori

### Amministrazione
Nel menù Amministrazione sono presenti i comandi necessari alla gestione delle attività dell'Associazione quali l'iscrizione dei nuovi soci, la gestione dei pagamenti, la gestione dei verbali di assemblea, ecc.

#### Soci
1. Gestisce la lista dei soci. Si possono filtrare per
-  `Attivi: ` sono tutti i soci in regola con i pagamenti (anche quelli in scadenza)
-  `In scadenza: ` filtro per i soci la cui iscrizione è in scadenza entro il limite di 45 giorni
-  `Scaduti: ` filtro per i soci la cui iscrizione è scaduta. I nominativi restano in questo filtro fino ad un massimo di 365 giorni

2. Per ciascun socio è possibile:
    a. effettuare il reset della password
    b. verificare i consensi concessi in fase di registrazione
    c. controllare i pagamenti effettuati
    d. inviare un sollecito per il pagamento della quota di iscrizione

#### Quote associative
Lista dei versamenti ricevuti dall’Associazione. E' possibile stampare la lista, estrarre un file Excel, scaricare la ricevuta del pagamento.


#### Richieste di iscrizione
Gestisce le nuove richieste di iscrizione all'Associazione. L'amministratore può accettare o rifiutare la richiesta. Il diniego deve essere motivato. (art. 3, c. 4 dello Statuto)

#### Promemoria
Gestisce l'invio massivo dei solleciti per gli utenti con l'adesione all'Associazione in scadenza.

#### Tabelle
Gestisce le tabelle necessarie al corretto funzionamento dell'applicazione.


### Header

- #### :bell: Notifiche

  Mostra le ultime tre notifiche e il numero totale da archiviare. Cliccando sulla singola notifica si accede alla transazione relativa. Cliccando invece su `"Vedi tutte le notifiche"`si accede alla funzione di archiviazione delle stesse. Selezionare le notifiche che si vuole archiviare e premere il pulsante `"Archivia notifiche"`

- #### :bust_in_silhouette: ​Account utente

  Mostra i dettagli dell'utente di amministrazione ed in particolare dei dati dell'Associazione. E' possibile:

  - cambiare la password
  - abilitare/disabilitare la ricezione dei messaggi **push**


- #### :gear: Impostazioni Associazione

  Visualizza le impostazioni dell'intera applicazione e ne permette la modifica. In particolare, è previsto l'inserimento di questi parametri:

  - `GDPR:` Inserire le informazioni del Titolare del Trattamento dei dati sulla privacy
  - `Quote:` Specificare le quote di iscrizione per le persone fisiche e giuridiche
  - `Server Host:` Indicare i parametri per l'accesso al server Host
  - `POA & Token:` Inserire i parametri per il collegamento al nodo POA del Token TTS (url, nodo, ChainID, Smart Contract, ecc.)
  - `BTCPay Server:` Url dei server per gli utenti e per l'Associazione con gli accessi per il collegamento
  - `SIN Pairing Associazione:` SIN dell'Associazione per ricevere i pagamenti delle iscrizioni dei soci in bitcoin
  - `Exchange:` API dell'exchange dell'Associazione
  - `Vapid Push:` Chiave pubblica e privata per identificare l'applicazione ed inviare/ricevere messaggi push
  - `Paypal:` Chiave pubblica e privata dell'account merchant di Paypal per ricevere i pagamenti delle iscrizioni dei soci
