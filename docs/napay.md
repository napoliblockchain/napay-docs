# Napay

Progressive Web App - v. 1.2













[![Screenshot of NaPay PWA app](images/screenshot-napay.png)](https://napay.napoliblockchain.it)

Napay è un'applicazione web nata per gestire facilmente i pagamenti in bitcoin e in TTS, il Token del Comune di Napoli.



<div style="page-break-after: always;"></div>

## Premessa

Napay (acronimo di Napoli Payments) è un software sviluppato all'interno del Progetto Blockchain Napoli da volontari e appassionati, di consolidata esperienza nei vari ambiti tecnologici (programmatori, sistemisti, ecc.), la cui sinergia ha fornito le basi per la creazione di un nuovo sistema di pagamento per le attività commerciali ed i professionisti.



### Progetto Blockchain Napoli

Nel mese di aprile 2018, il Comune di Napoli ha effettuato una chiamata pubblica per il reclutamento di volontari al fine di realizzare alcuni progetti in ambito blockchain e cryptovalute. A questa chiamata hanno risposto piú di 300 persone. Per quanto riguarda i pagamenti in cryptovaluta, si è formato un ristretto gruppo di tecnici il cui obiettivo è stato la realizzazione di un sistema di pagamento virtuale che permetta agli esercenti di accettare Bitcoin presso la propria attività.

L'Associazione Napoli Blockchain nasce sulla spinta dell’iniziativa del Comune di Napoli e si propone di:
- diffondere la conoscenza della Blockchain e delle cryptovalute
- aiutare i soci a creare un senso di consapevolezza sull'utilità di tali tecnologie nella vita
- promuovere la tecnologia Blockchain come veicolo per l'inclusione sociale, per il rafforzamento della partecipazione civica
- supportare il Comune di Napoli nello sviluppo, diffusione ed implementazione dell'utilizzo della Blockchain.



<div style="page-break-after: always;"></div>

## Iscrizione Socio

1. Il commerciante che vuole diventare socio deve iscriversi attraverso il form di registrazione presente sul sito inserendo le informazioni necessarie richieste per la registrazione dell’utenza.

   Con l’iscrizione, l’utente:

   - conferma di aver letto lo ***Statuto***;

   - conferma di aver letto l'***INFORMATIVA SULLA PRIVACY*** e autorizza al trattamento dei dati personali;

   - accetta le ***Condizioni generali di utilizzo*** del software;

   - può acconsentire o meno al  ***trattamento dei dati per finalità di marketing***

   -  accetta i ***Termini e le Condizioni di utilizzo del POS***

     > [^]: I ***termini e le condizioni di utilizzo del POS*** riguardano **esclusivamente** i commercianti. Per i soci non commercianti quest'autorizzazione non è richiesta.

2. L'iscrizione è subordinata all'accettazione da parte del Consiglio Direttivo che ne ratifica l'ammissione in sede di assemblea (art. 3, c. 3 dello Statuto)

3. Una volta approvata l'iscrizione, il socio, se non ha già provveduto al pagamento della quota associativa, provvederà al pagamento della stessa tramite la sezione `Paga Quota Iscrizione`



## Pagamento Quota Iscrizione

1. Per effettuare il pagamento della quota di iscrizione è necessario effettuare il login nella sezione apposita presente sulla pagina di login dell'applicazione. La quota di iscrizione è diversa nel caso in cui il socio sia un commerciante oppure no, ed è stabilita secondo il Regolamento interno dell'Associazione.

2. Il pagamento può avvenire tramite transazione in
   - Bitcoin o Litecoin
   - Paypal

3. Quando si effettua il pagamento, il socio viene abilitato all'utilizzo della procedura fino al 31 dicembre dell'anno solare in corso.

<div style="page-break-after: always;"></div>

## Abilitazione Ricezione Cryptovaluta

### Creazione Negozio

1. Per rendere operativo il software, cioè essere capaci di ricevere bitcoin, è necessario creare un Negozio a cui sia associato uno o più POS. Una volta cliccato nel menù su `Nuovo Negozio`, basta seguire queste regole:
    - Se l'indirizzo della sede del negozio combacia con quello inserito in fase di registrazione, inserire solo la denominazione del Negozio e salvare;
    - Se invece gli indirizzi sono diversi (ad es. sede legale e sede operativa differenti), inserire il nuovo indirizzo, quindi confermare il salvataggio.

#### Configurazione Negozio

Una volta creato il Negozio è necessario impostare i parametri di configurazione dello stesso.

- Impostazioni generali
- Exchange Rate
- Inserimento Master Public Key (per ciascuna cryptovaluta abilitata nelle impostazioni del Commerciante). Se non si conosce il metodo di estrazione della MPK da un wallet, seguire la guida a questo link: [Guida estrazione MPK](https://napoliblockchain.it/esportare-la-chiave-pubblica-mpk-dal-wallet-coinomi/). Al termine di questa operazione, verranno mostrati 10 indirizzi bitcoin generati dall'applicazione web utilizzando la MPK dell'utente. Verificare che gli indirizzi generati corrispondano con quelli presenti sul proprio wallet per **certificare** il corretto funzionamento della MPK.
- Personalizzazione Invoice

### Creazione POS

1. Appena creato il Negozio, il software ci informa se si vuole generare il POS. Clicchiamo sul pulsante `Nuovo POS` e inseriamo:
   -  la descrizione del POS per identificarlo secondo l'organizzazione interna *(es. POS principale, POS piano terra, POS reparto 1, ecc…)*;
2. Una volta creato il POS, viene generato un **"pairing code"** che serve per l'attivazione dello stesso. Questo codice ha una durata di 15 minuti. Se si prova ad attivare il POS oltre i 15 minuti si otterrà un messaggio di errore. Sarà necessario, pertanto, richiedere un altro codice cliccando sul pulsante **"MODIFICA"** e salvare nuovamente le informazioni richieste.
3. L'attivazione del POS si ottiene cliccando sul pulsante **"ATTIVA"** che lo renderà fruibile dal negoziante. Questa operazione genera un *token*, una coppia di chiavi pubblica/privata che servono per inviare le richieste di pagamento e un ***SIN*** (Server INitiating Pairing) che verrà utilizzato per effettuare la connessione sulla pagina di login del POS.

<div style="page-break-after: always;"></div>

## Abilitazione Ricezione Token TTS

1. Tramite questo link: [Recovery Sheet](RECOVERY_SHEET.pdf), stampare innanzitutto il Recovery Sheet, il documento su cui andremo a scrivere il seme che l'applicazione genererà.

2. Per ricevere il token TTS, bisogna prima di tutto accedere al wallet tramite il *link* presente nel *Widget* dell'applicazione **Napay**, oppure digitando direttamente questo URL [wallet.napoliblockchain.it](https://wallet.napoliblockchain.it/?r=wallet/index) nella barra degli indirizzi del browser dello smartphone.

3. Effettuare il login con le credenziali di accesso all'applicazione **Napay**. Se abbiamo abilitato la **Sicurezza a 2 Fattori per il Wallet TTS** nelle impostazioni utente, ci verrà richiesto anche il codice di controllo per proseguire.

4. Scegliere se generare un nuovo wallet o ripristinarne uno creato precedentemente. Se la scelta è quella di generare un nuovo wallet, scrivere immediatamente le parole del **seed** nello stesso ordine in cui vengono mostrate sul Recovery Sheet stampato in precedenza e conservarlo in un luogo **sicuro**. In caso di smarrimento, non è più possibile ripristinare e recuperare i fondi presenti su quell'indirizzo.

5. Una volta collegati avremo (ad esempio) la seguente schermata:

<img src="images/screenshot-wallet.png" alt="POS screenshot" style="zoom: 67%;" />
<div style="page-break-after: always;"></div>

## Utilizzo del POS

1. Collegarsi tramite il *link* presente nel *Widget* dell'applicazione **Napay**, oppure digitando direttamente questo URL [pos.napoliblockchain.it](https://pos.napoliblockchain.it/?r=site/login) nella barra degli indirizzi del browser dello smartphone.

2. Il codice **SIN** (Server-Initiated Pairing) che viene richiesto è il codice che è stato generato in fase di attivazione del POS e che è stato inviato anche sulla mail del commerciante. Possiamo recuperare questo codice anche all'interno dell'applicazione **Napay**, selezionando `POS` nel menù `"Gestione Applicazione"`.

3. Una volta effettuato il login avremo la schermata seguente:

<img src="images/screenshot-pos.png" alt="POS screenshot" style="zoom:67%;" />



4. Inseriamo l'importo da richiedere e clicchiamo su **"bitcoin"** se vogliamo essere pagati in cryptovaluta, altrimenti clicchiamo su **"token"** se vogliamo ricevere il **Token TTS**.

<div style="page-break-after: always;"></div>

## Gestione di Napay

*Napay* permette la gestione di tutte le operazioni che un *Amministratore* o un *Commerciante* compiono per il lavoro quotidiano. Queste attività sono svolte tramite l'utilizzo delle seguenti funzioni:

- **Dashboard**: presenta una sintesi grafica dell'andamento delle vendite
- **Transazioni**: lista delle transazioni del POS e dell'ATM
- **Notifiche**: lista delle notifiche
- **Impostazioni**: dell'account personale

Uno user con lo status di *Amministratore* ha la visione completa di tutte le transazioni avvenute nell'applicazione. Uno user *Commerciante* ha la visione delle sole transazioni di propria competenza.

<div style="page-break-after: always;"></div>

### Header dell'Applicazione**

- #### :green_book: ​Widget

  Nel widget sono visualizzati i link alle altre due applicazioni integrate con Napay: POS e Wallet-tts

- #### :bell: Notifiche

  Mostra le ultime tre notifiche e il numero totale da archiviare. Cliccando sulla singola notifica si accede alla transazione relativa. Cliccando invece su `"Vedi tutte le notifiche"`si accede alla funzione di archiviazione delle stesse. Selezionare le notifiche che si vuole archiviare e premere il pulsante `"Archivia notifiche"`

- #### :bust_in_silhouette: ​Account utente

  Mostra i dettagli dell'utente collegato ed è possibile modificarli. Mostra, inoltre, le autorizzazioni ai consensi e le date in cui sono stati concessi. E' possibile, infine,

  - cambiare la password
  - abilitare/disabilitare la **Sicurezza a 2 Fattori per il Wallet TTS**
  - abilitare/disabilitare la ricezione dei messaggi **push**
  - Scaricare il Recovery Sheet per il salvataggio del seed di recupero del Wallet-tts

- #### :gear: Impostazioni

  Visualizza le impostazioni e ne permette la modifica. In particolare è possibile visualizzare/modificare:

  - Per l'amministratore:
    1. Dati anagrafici dell'Associazione.
    2. Quote per l'iscrizione.
    3. Informazioni del server host
    4. Informazioni sulla POA
    5. Negozio dell'Associazione per ricevere le iscrizioni in Cryptovaluta
    6. Pos per la ricezione in crypto delle iscrizioni.
    7. API dell'exchange di riferimento della Web application.
    8. API per il servizio di invio messaggi Push dell'applicazione.
    9. API per il servizio di pagamento tramite PayPal.
   10. API per il login social di Bolt
   11. API per reCaptcha2 di Google

 - Per il commerciante:
    1. Processore dei pagamenti in uso.
    2. API dell'exchange di riferimento dell'utente.
    3. Dati Bancari. Devono corrispondere a quelli inseriti sull'exchange per poter ricevere euro dalla compravendita dei bitcoin.


<div style="page-break-after: always;"></div>

## Gestione Pagamenti

In questo menù sono racchiusi tutti i collegamenti ai comandi che servono a gestire i pagamenti dell’applicazione, dalle transazioni alle notifiche.

### Transazioni

Con `“Transazioni”` è possibile visualizzare la lista di tutte le richieste di pagamento in cryptovaluta e lo stato in cui si trovano. Cliccando sulla singola transazione si possono visualizzare tutti i dettagli.

Nella schermata dettagli, cliccando sul pulsante dello stato della transazione, il sistema verifica se ci sono stati cambiamenti nello stato della transazione. Questa funzione è utile soprattutto se la transazione si trova nello stato `"in corso..."` e sono trascorsi più di 15 minuti dalla sua creazione.

E' possibile stampare la lista delle transazioni oppure estrarle in formato Excel.

### Tokens

Con `“Tokens”` è possibile visualizzare la lista di tutte le richieste di pagamento effettuate in token
tramite POS . Cliccando sulla singola transazione si possono visualizzare tutti i dettagli.

Nella schermata dettagli, cliccando sul pulsante dello stato della transazione, il sistema verifica se ci sono stati cambiamenti nello stato della transazione. Questa funzione è utile soprattutto se la transazione si trova nello stato `"in corso..."` e sono trascorsi più di 15 minuti dalla sua creazione.

E' possibile stampare la lista delle transazioni oppure estrarle in formato Excel.

### Notifiche

Con `“Lista Notifiche”` è possibile visualizzare la lista di tutte le notifiche ricevute non ancora visualizzate. Le notifiche si possono archiviare singolarmente o complessivamente, spuntando il checkbox relativo e cliccando sul pulsante `“Archivia notifiche”`.



<div style="page-break-after: always;"></div>

## Applicazione

In questo menù sono raccolti i comandi necessari al funzionamento dell’applicazione.


### Commercianti

*Solo per Amministratori*

Con `Commercianti` si gestiscono i Commercianti. In fase di inserimento si sceglie il *Server blockchain* e le cryptovalute da gestire. E' possibile assegnare un solo account commerciante per ciascun utente creato. Non si possono assegnare account commerciante agli utenti amministratori.

### Negozi

Con `“Negozi”` si gestiscono i negozi del commerciante. Non esiste un limite ai negozi che si possono creare. Si possono eliminare solo i Negozi a cui non è associato alcun POS.

### POS (Point of Sale)

Con `“POS”` si gestiscono i POS (Point of Sale) dei singoli negozi. Non esiste limite ai POS che si possono creare. Eliminare un POS significa che non potremo più utilizzare il codice SIN ad esso associato per ricevere cryptovaluta. Questa operazione non incide in alcun modo sul wallet dove sono `“conservati”` i bitcoin

### Self POS

Si gestisce il Pos in stile Shopping Cart, inserendo i prodotti che verranno mostrati per la vendita da Desktop o Tablet. Anche se è naturalmente possibile usarlo da smartphone.


<div style="page-break-after: always;"></div>

## Amministrazione

### Soci

1. Gestisce la lista dei soci. Si possono filtrare per

- `Attivi: ` sono tutti i soci in regola con i pagamenti (anche quelli in scadenza)
- `In scadenza: ` filtro per i soci la cui iscrizione è in scadenza entro il limite di 45 giorni
- `Scaduti: ` filtro per i soci la cui iscrizione è scaduta. I nominativi restano in questo filtro fino ad un massimo di 365 giorni

2. Per ciascun socio è possibile:
   - effettuare il reset della password
   - verificare i consensi concessi in fase di registrazione
   - controllare i pagamenti effettuati
   - inviare un sollecito per il pagamento della quota di iscrizione


### Quote associative

Lista dei versamenti effettuati all’Associazione. E' possibile stampare la lista, estrarre un file Excel, scaricare la ricevuta del pagamento.


### Richieste di iscrizione

Gestisce le nuove richieste di iscrizione all'Associazione. L'amministratore può accettare o rifiutare la richiesta. Il diniego deve essere motivato. (art. 3, c. 4 dello Statuto)


### Promemoria

Gestisce l'invio massivo dei solleciti per gli utenti con l'adesione all'Associazione in scadenza.


### Verbali

Lista dei verbali dell'Associazione. E' possibile visualizzare e scaricare i verbali di assemblea dell'Associazione. (art. 10, c.2 dello Statuto)

Il compito di caricare i verbali è affidato al socio con la carica di Segretario. (art. 10, c.1 dello Statuto)


### Menù Tabelle

1. Server blockchain
2. Assets
3. Exchanges
4. Gateway
5. Tipo utenti
6. Cariche
7. Tipo quote
8. Tipo pagamenti
