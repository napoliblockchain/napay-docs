# Napay TTS Wallet

#### PWA - v. 0.4

![Screenshot of Napay TTS PWA app](images/screenshot-wallet.png)



❤️❤️❤️ A wallet using Naples Payment Token, implementing a lot of PWA love. ❤️❤️❤️

[![License: MIT](https://img.shields.io/badge/License-MIT-lightgrey.svg)](https://opensource.org/licenses/MIT)



## Authors

- [Sergio Casizzone](https://sergiocasizzone.it)
- [Antonio Della Porta](mailto:antonio@dellaporta.it)



## Features

###### **Wallet**

- [x] Mobile Layout
- [x] `Token` & `Gas` Balance
- [x] Token send & receive
- [x] Gas receive only feature
- [ ] Available in many languages
- [x] Transactions list
- [x] Transaction details
- [ ] Multi wallet manager (coming soon)
- [x] Select predefined wallet to use
- [x] Blockchain sync & rescan

###### PWA

- [x] Service Worker

- [x] Push messages

- [x] Use of indexedDB

- [x] Static precache & dynamic cache

- [x] Save coin send requests for offline use

  [^1]: when the app returns on-line, memorized requests will be executed!

###### Security

- [x] PIN protected access
- [x] Google 2FA Login
- [x] Seed management with recovery wallet
- [x] BIP32 passphrase


## Info

Il **Wallet TTS** è il software con cui il commerciante gestisce i token ricevuti dalle vendite effettuate tramite POS. Trattandosi di un'applicazione web si può utilizzare anche da PC, ma per una migliore esperienza d'uso **si consiglia di utilizzare uno smartphone**.



## Login

Per accedere, basta cliccare sul pulsante **Wallet TTS** visibile nel widget di Napay, oppure digitare direttamente l'URL [wallet.napoliblockchain.it](https://wallet.napoliblockchain.it) nella barra degli indirizzi del browser dello smartphone.

Nella pagina di *Login* inserire lo **username** e la **password**.
Se in **Napay** abbiamo abilitato l'autenticazione a 2 fattori nelle impostazioni, non potremo accedere al Wallet finché non avremo inserito il codice di sicurezza richiesto.



## Primo accesso

Se è la prima volta che si effettua l'accesso al wallet, dovremo scegliere se generare un nuovo **seed** oppure inserirne uno già in nostro possesso. 
