




# Bolt Technical Manual

##### Repository

- Source code: https://bitbucket.org/jambtc/bolt/src/master
- Manuali utente: https://github.com/napoliblockchain/napay-docs

##### Librerie esterne

- Javascript Ethereum wallet: https://github.com/ConsenSys/eth-lightwallet
- JavaScript AES block cipher algorithm: https://github.com/ricmoo/aes-js
- Php interface with Ethereum blockchain: https://github.com/sc0Vu/web3.php
- Yii Framework: https://github.com/yiisoft/yii
- Librerie comuni alle applicazioni Napay (libs): https://bitbucket.org/jambtc/libs/src/master


<div style="page-break-after: always;"></div>
Il software Bolt è costituito da parti di programma in php ed altre parti in Java e html. Viene utilizzato il framework Yii nella versione 1.1.20 per cui l'architettura è formata dal pattern MVC (Model-View-Controller) secondo l'immagine seguente:



![img](https://github.com/napoliblockchain/napay-docs/blob/master/docs/images/patternMVC.jpg) 





Normalmente, salvo forzature, nel controller e nel model viene gestita la programmazione php, mentre nelle view viene gestito il codice Javascript.
Il software è modulare, pertanto si possono estrarre singole porzioni che possono essere implementate o modificate a seconda delle proprie necessità.
Il software è stato implementato anche con funzioni PWA (Progressive Web App), pertanto saranno attivi anche moduli Javascript quali il service worker (SW). La PWA permette anche la gestione dei messaggi Push.
Viene, inoltre, utilizzato `l'indexedDb`, lo storage locale del browser, al cui interno vengono salvati ad esempio il pin di sicurezza, il seed e le informazioni di invio token. Il local storage viene utilizzato per questione di sicurezza quale il salvataggio in locale dei dati dell'utente, questo per evitare che essi siano salvati sul server centrale. In tal modo l'utente è l'unico responsabile della conservazione e trattazione delle proprie informazioni di sicurezza relative al wallet. Questo evita anche che il gestore del server possa essere chiamato in causa per questioni relative al salvataggio e ripristino dei token di un utente.







##### Il modulo di Login

Il login all'applicazione può essere effettuato in quattro diverse modalità. La soluzione classica è quella di effettuare la registrazione di username e password ed usare queste due componenti per utilizzare il wallet. È stato previsto anche l'utilizzo di social per effettuare il login ed in particolare si possono usare gli account social di:

- Facebook
- Telegram
- Google

Le librerie per l'utilizzo di questi social ho pensato di non integrarle, ma di creare un repository esterno che ho chiamato [**libs/oauth**](https://bitbucket.org/jambtc/libs/src/master/oauth/) così da poterle utilizzare anche per altre applicazioni. Ecco un esempio di utilizzo della libreria:

```php
include ('js_login.php');
include ('js_google.php');
include ('js_facebook.php');

require_once Yii::app()->params['libsPath'] . '/oauth/telegram/login.php';
$checkTelegramAuthorization = Yii::app()->createUrl('telegram/CheckAuthorization');
$bot_username = Settings::load()->telegramBotName;
$bot_token = Settings::load()->telegramToken;

require_once Yii::app()->params['libsPath'] . '/oauth/google/login.php';
$checkGoogleAuthorization = Yii::app()->createUrl('google/CheckAuthorization');

require_once Yii::app()->params['libsPath'] . '/oauth/facebook/login.php';
$facebookAppID = $settings->facebookAppID;
$facebookAppVersion = $settings->facebookAppVersion;
$sourceLanguage = explode('_',Yii::app()->sourceLanguage);
$lingua = $sourceLanguage[0];
$paese = strtoupper($sourceLanguage[1]);
```





##### Il controller del wallet

Andiamo ora a vedere come è gestita la creazione/verifica del wallet a seconda che si utilizzi il software per la prima volta o in quelle successive.

Una volta effettuato il login tramite il modulo di Login, il walletController verifica se nella tabella `bolt_wallets` (gestita dalla classe protected\models\Wallet.php) è presente un address appartenente allo user connesso. Se non è presente inizializza la variabile *$from_address* al valore di 0x00...  altrimenti assegna il valore caricandolo dal db.

file: `protected/Controllers/WalletController.php`

```php
// carico il wallet selezionato nei settings
$settings=Settings::loadUser(Yii::app()->user->objUser['id_user']);
if (empty($settings->id_wallet)){
	$from_address = '0x0000000000000000000000000000000000000000';
}else{
	$wallet = Wallets::model()->findByPk($settings->id_wallet);
	$from_address = $wallet->wallet_address;
}
$modelc->from_address = $from_address;
```

Carico i contatti

```php
// carico i contatti dell'utente
$criteria = new CDbCriteria();
$criteria->compare('id_user',Yii::app()->user->objUser['id_user'],false);
$dataProvider=new CActiveDataProvider('Contacts',array(
	'criteria' => $criteria,
	'pagination' => array(
		'pageSize' => 10,
	),
));

```

Quindi viene richiesto di mostrare la schermata principale del wallet con le informazioni necessarie al suo corretto funzionamento.

```php
// visualizzo la schermata
$this->render('index',array(
	'modelc'=>$modelc, //lista transazioni tokens
	'walletForm'=>$walletForm, //form per invio dati
	'from_address'=>$from_address, // indirizzo del wallet dell'utente
	'actualBlockNumberDec' => eth::latestBlockNumberDec(), // blocco attuale su blockchain
	'dataProvider' => $dataProvider, // lista contatti
));
```

Finora il software ha lavorato lato server.



##### La view principale (wallet/index)

La view mostra la maschera principale e carica diversi file Java. In Yii è possibile generare dinamicamente i file Java, cosa molto utile perché così è possibile modificarne i parametri a seconda delle diverse richieste di funzionamento.

```php+HTML
<div class="form">

<?php
$form=$this->beginWidget('CActiveForm', array(
	'id'=>'wallet-form',
	'enableAjaxValidation'=>false,
));

//richiamo tutte le funzioni javascript
include ('js_pin.php');
include ('js_eth.php'); // viene prima di initiazlie
include ('js_walletInitialize.php');
include ('js_wallet.php');
include ('js_cgridview.php');
include ('js_qr-scanner.php');
include ('js_nfc.php');
```

Il file che gestisce la generazione del seed è `views\wallet\js_walletInitialize.php`

Una funzione  interviene per verificare che all'interno dello storage del browser ci sia salvato l'address inviato dal Controller e reagisce in questo modo:

- address non salvato: vai a generazione seed
- address trovato ma diverso: vai a generazione seed
- address trovato e identico: carica il resto della pagina

```javascript
// LEGGO LE INFORMAZIONI DEL WALLET DA IndexedDB
var isEquel = null;
var my_address;

readFromId('wallet',"{$from_address}")
	.then(function(data) {
		if (typeof data[0] !== 'undefined') {
			for (var dt of data) {
				if (null === data.id){
					$('#initializeWallet').modal({backdrop: 'static',keyboard: false});
					break;
				}else{
					var address_1 = new String("{$from_address}");
					var iduser_1 = new String(cryptedIdUser);
					var address_2 = new String(dt.id);
					var iduser_2 = new String(dt.id_user);
					isEquel_1 = JSON.stringify(address_1) === JSON.stringify(address_2);
					isEquel_2 = JSON.stringify(iduser_1) === JSON.stringify(iduser_2);
					isEquel = isEquel_1 * isEquel_2;
				}
				if ( isEquel ){
					/*  START 	*/
					my_address = data[0].id;
					break;
				}else{
					$('#initializeWallet').modal({backdrop: 'static',keyboard: false});
					break;
				}
             }

```



##### Generazione del seed

Viene visualizzata una finestra Modal dove inserire e/o generare un nuovo seed. La pagina di layout (`protected/views/layout/main.php`) carica il file Javascript lightwallet.min.js (https://github.com/ConsenSys/eth-lightwallet) che è, in breve, la libreria che permette la generazione e il salvataggio delle chiavi private ethereum.



La funzione <span style="color:blue;">keystore.generateRandomSeed</span> genera un seed con entropia casuale di lunghezza variabile da 1000 a 2000 caratteri.

```javascript
// questa funzione genera il nuovo seed del wallet
function newWallet()
{
	seed = lw.keystore.generateRandomSeed(generateEntropy(Math.floor(Math.random() * 1001)+1000));
	testo = "<p class='alert alert-light text-danger'><strong>"+seed+"</strong></p>";
	testo += Yii.t('js',"<b>Write the seed and keep it in a safe place; if you lose it you will not be able to restore your wallet and you will lose all the funds.</b>");

	$('#seedText').html(testo);
	$('#seedInput').val(seed);
}
```

Premendo il pulsante di salvataggio del seed, viene verificata la validità dello stesso e la funzione <span style="color:blue;">generateEntropy</span> genera anche una password di 32 caratteri per criptare il seed prima di effettuare la chiamata alla funzione <span style="color:blue;">initializeVault</span> che inizializza il wallet.

```javascript
// verifico validità del seed
$("button[id='cryptConferma']").click(function(){
	var seed = $('#seedInput').val();
	var confirm_seed = $('#repeat_seed').val();

	if (WordCount(confirm_seed) != 12 || !(isSeedValid(confirm_seed)) || confirm_seed != seed){
		$('#repeat_seed_em_').show().text(Yii.t('js','Invalid Seed!'));
		return;
	}
	$('#repeat_seed_em_').hide().text('');

	// la password viene generata in automatico dal sistema
	var password = generateEntropy(32);

	initializeVault(password,seed);
});
```

Nella funzione <span style="color:blue;">initializeVault</span>:

- La password e il seed vengono criptati e viene richiamata la funzione <span style="color:blue;">keystore.createVault</span>.
- Dalla password e dal seed viene estratta la Derived Key con cui viene generato ed estratto l'address n. 0
- Con address e derived key viene  esportata la chiave privata
- Address e chiave privata criptata vengono salvati in indexedDb del browser nella tabella wallet. 
- Address viene salvato nella tabella mysql bolt_wallets
- id_address relativo alla tabella bolt_wallets viene salvato nei settings dell'user
- Il seed viene salvato criptato in indexedDb del browser nella tabella mseed
- La pagina viene ricaricata e si ripete il processo dall'inizio 

```javascript
// adesso salviamo in local storage il seed e la password
function initializeVault(password, seed) {
	$.ajax({
		url:'{$cryptURL}',
		type: "POST",
		data: {
			'pass': password,
			'seed': seed
		},
		dataType: "json",
		success:function(data){
			var pwd_crypted  = data.cryptedpass;
			var seed_crypted  = data.cryptedseed;
			var iduser_crypted  = data.cryptediduser;
			lw.keystore.createVault({
			    password: password,
			    seedPhrase: seed,
			    hdPathString: "m/0'/0'/0'"
				}, function (err, ks) {
				    ks.keyFromPassword(password, function (err, pwDerivedKey) {
				        if (!ks.isDerivedKeyCorrect(pwDerivedKey)) {
				            throw new Error("Incorrect derived key!");
				        }

				        try {
				            ks.generateNewAddress(pwDerivedKey, 1);
				        } catch (err) {
				            console.log(err);
				            console.trace();
				        }
				        var address = ks.getAddresses()[0];
				        var prv_key = ks.exportPrivateKey(address, pwDerivedKey);

						var post = {
							id			: address, // id of indexedDB
							id_user		: iduser_crypted,
							prv_php 	: CryptoJS.AES.encrypt(JSON.stringify(prv_key), password, {format: CryptoJSAesJson}).toString(),
							prv_pas		: pwd_crypted,
						};
						
						writeData('wallet', post)
							.then(function() {
								//save at mysql a user's wallet address
								$.ajax({
									url:'{$saveAddress}',
									type: "POST",
									data: {'address': address},
									dataType: "json",
									success:function(data){
										var post2 = {
											id : new Date().toISOString(), // id of indexedDB
											cryptedseed : seed_crypted,
										}
										writeData('mseed', post2)
										.then(function() {
											setTimeout(function(){ location.reload() }, 250);
										});
									},
									error: function(j){
										console.log('error',j);
									}
								});
							})
							.catch(function(err) {
								console.log(err);
							});
				    });
				});
			// Quindi, chiedo di installare la webapp sulla home del cell
			saveOnDesktop();
		},
		error: function(j){
			console.log('error',j);
		}
	});
}
```



##### Seed già generato e address trovato negli User Settings

Quando l'utente effettua il login, abbiamo visto che il software controlla se nell'indexedDb è presente lo stesso address salvato nei settings dell'user richiamando, in caso di diversità, il processo di generazione del seed. Nel caso in cui siano uguali vengono richiamati i processi che possiamo anche vedere nel blocco di codice che segue:

```javascript
.then(function() {
	if (isEquel){
		backend.checkPin();
		erc20.Balance(my_address);
		eth.Balance(my_address);
		blockchain.sync(my_address);
		setTimeout(function(){ blockchain.scanForNew(my_address) }, 2000);
	}
});
```

Viene eseguita la funzione backend.checkPin per verificare che sia stato immesso il pin per sbloccare l'applicazione. Anche il pin è salvato in formato criptato nell'indexedDb nella tabella pin.

Vengono chiamate le funzioni erc20.Balance e eth.Balance (inserite nel file js_eth.php) che verificano sulla blockchain il saldo sull'address. 

Vengono poi chiamate due funzioni che sincronizzano la blockchain in questo modo:

- blockchain.sync - ricerca nei nuovi blocchi transazioni in cui sia presente l'address dell'utente. Nelle pagine successive spiegherò nel dettaglio il funzionamento delle funzioni che si interfacciano con la blockchain Ethereum. Per il momento basti sapere che nella nostra POA, generalmente, ciascun blocco viene generato ogni 15 secondi, quindi questa funzione viene richiamata ogni 7 secondi secondo la formula seguente:
  -  (T2 - T1) / E dove 
    - t2-t1 è l'intervallo di tempo di 15 secondi
    - E è il numero di eventi certi che desideriamo accadano
  - Quindi abbiamo (15 - 0) / 2 = 7,5 arrotondata a 7 secondi.
- blockchain.scanForNew - cerca nel db eventuali transazioni nello stato "new" e, nel caso in cui è presente la txhash (hash della transazione), verifica sulla blockchain lo stato della stessa aggiornando di conseguenza il db. Nel caso in cui la txhash è vuota la transazione viene segnalata come "failed". In pratica questa funzione agisce da "resume" nel caso in cui il software del wallet si sia bloccato o lo smartphone abbia avuto problemi di qualsiasi genere. 
