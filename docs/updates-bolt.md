# Aggiornamenti

#### versione 1.3.1

    - generate auto-random password to crypt seed #79
    - Testo pagina primo accesso #76
    - Testi Schermata invio #75
    - NFC to share tokens #73
    - Il tasto segnala bug non ha tutti i campi #64


#### versione 1.3

    **new features**
    - #74 Logout from create/restore seed
    - #71 Bolt: you can backup master seed only if pin is enabled
    - #57 Napay: togli copyright nel footer e metti powered by
    - #48 Napay: gestione/visualizzazione dei log delle applicazioni

    **fix**
    - #72 Bolt: remove pin don't ask pin (only on 1st set)
    - #68 [Bolt] servizio watchtower deve ripartire in automatico se va giù
    - #65 [Bolt] Non si aggiorna subito a transazione OK
    - #61 Push: i messaggi sono tutti [bolt]
    - #60 Bolt: oauth parametri per produzione
    - #56 Bolt: error qrcode
    - #49 Napay: settings, mancano impostazioni social di Bolt
    - #42 Bolt: INGRESSO CON FACEBOOK
    - #38 Bolt: Firefox Anonimo
    - #37 Bolt: Log Off mancante
    - #34 Pos/Bolt: non si aggiorna messaggio memo dalla transazione ipn
    - #27 Napay: inserire recaptha2 in ripristino pwd, form, bugs e login
    - #22 Bolt: gestione address legato all' id user



### Lista Commit

#### febbraio 2020

    c380718	fix #57	2020‑02‑07
    a96a008	fix #49	2020‑02‑06
    d94514c	fix #56	2020‑02‑06
    4162f3f	Esternalizzate tutte le funzioni da Yii::app()->controller in WebApp	2020‑02‑05

#### Gennaio 2020

    4522a4e	mpk	2020‑01‑31
    9ddf7e5	update sh0	2020‑01‑30
    3b629e9	FB php Login, fix #42	2020‑01‑29
    07f26c5	Merge branch 'master' of https://bitbucket.org/jambtc/bolt	2020‑01‑29
    ba251ca	update sh	2020‑01‑29
    1ea01ba	fix contacts username	2020‑01‑28
    64c53b4	google php login	2020‑01‑28
    3429b45	refix empty telegram datas	2020‑01‑24
    2dda3ad	fix telegram empty data	2020‑01‑24
    337E206	fix telegram php login	2020‑01‑24
    bf51724	wip php telegram login	2020‑01‑23
    fb39352	new entropy for generated seed	2020‑01‑23
    f63da53	fix notify link	2020‑01‑22
    7d453a0	update all messages to read	2020‑01‑22
    3063d7a	update all news wip	2020‑01‑21
    9b38a1c	fix watchtower	2020‑01‑21
    456b0e8	fix console config	2020‑01‑21
    72a6b8f	qr-scanner internal	2020‑01‑21
    6174753	pin fixed	2020‑01‑21
    d48aec3	user profile change	2020‑01‑21
    a0a057f	fix notify message	2020‑01‑21
    3944a75	fix messages list	2020‑01‑21
    3102413	external libs	2020‑01‑21
    1c0983c	vix view qrcode scanner	2020‑01‑21
    8f73d43	new qrcode camera scanner	2020‑01‑21
    d30f743	fix details	2020‑01‑20
    826e842	some fixes	2020‑01‑20
    7b53b52	fix balance for betatester	2020‑01‑20
    4c772f7	fix contacts image	2020‑01‑20
    4370a56	temp fix login	2020‑01‑20
    ea45381	load GAS Fixed!	2020‑01‑20
    232f0f2	fix backend	2020‑01‑20
    dbfa3a7	sw static cache	2020‑01‑20
    22c400e	fix repeat new seed	2020‑01‑20
    bb4cfd1	fix oauth login	2020‑01‑20
    514d7ce	master seed backup	2020‑01‑20
    2852cee	fix telegram userid	2020‑01‑20
    8c52cfe	f.maglia	2020‑01‑18
    8c3b0a8	fix no contacts	2020‑01‑18
    1a49173	camera select 0	2020‑01‑18
    3b0bdf0	fix console	2020‑01‑15
    3b6fc85	fix command	2020‑01‑15
    7dbfb26	fix max decimals	2020‑01‑15
    0bbccfb	ether send ok, ethereum external	2020‑01‑14
    b9acb6e	WIP ETHER send	2020‑01‑13
    bf1bc8f	fix notify	2020‑01‑09
    e4018d9	Merge branch 'master' of https://bitbucket.org/jambtc/bolt	2020‑01‑09
    07f7665	hide login debug	2020‑01‑09

#### Dicembre 2019

    d09d705	fix from/at user napay wallet	2019‑12‑24
    16ab4f2	fix messages	2019‑12‑24
    743445f	minor fix	2019‑12‑23
    ad041a0	contatti in ordine alfabetico	2019‑12‑22
    df33b2e	console.log eth balance	2019‑12‑21
    8c6ea7f	hotfix push	2019‑12‑21
    5f12003	fix english message push	2019‑12‑21
    a1e53c5	wip deferredprompt save button	2019‑12‑20
    f6778f9	pay to contact	2019‑12‑20
    264048e	fix issue #115 Da: a: cambiare con i nominativi	2019‑12‑20
    6f20849	fix issue #116 Salvataggio in home	2019‑12‑20
    d5af15d	fix issue #122 Abbassare n. Blocchi syncronizzazione	2019‑12‑20
    5cf7172	fix camera, Wait a little, so that Android has time to populate select	2019‑12‑20
    95cd579	fix camera & lang	2019‑12‑20
    8a75bbb	fix camera	2019‑12‑20
    5588181	fix issue #113 Partire con camera2 retro	2019‑12‑20
    c82073a	fix issue# 114 Click su indirizzo va su pagina errore	2019‑12‑20
    eb012c0	fix issue #111 invio/ricevi compare COMPLETE	2019‑12‑20
    3bc22fa	fix issue #121 errore in registrazione via mail	2019‑12‑20
    10516a6	fix issue #112 Lettura qrcode non funziona	2019‑12‑19
    13c0d0b	fix send status	2019‑12‑19
    abaf6bf	test send command	2019‑12‑19
    ee940ea	update check permission on logs	2019‑12‑19
    58135c8	fix get user address	2019‑12‑19
    90dcd37	fix notifications & contacts	2019‑12‑19
    65df8b4	new pc cgf6135t	2019‑12‑11
    74802ca	testing social login	2019‑12‑10
    5464ecc	database link update to npay	2019‑12‑10
    415672	oauth google testing	2019‑12‑10
    0613ada	wip sw bi	2019‑12‑10
    3782d21	wip bi	2019‑12‑09
    ae319af	wip integration	2019‑12‑09
    87bc819	integration	2019‑12‑09
    839f6bf	wip integration	2019‑12‑08
    2220c1a	fix tts integration	2019‑12‑06
    6697445	fix user search self-contact	2019‑12‑05
    18a8d81	fix user view	2019‑12‑05
    ff3a336	hide google response	2019‑12‑05
    90a5a4d	twitter wip	2019‑12‑05
    5b8d605	solved issue #106 (gas btn) & #107	2019‑12‑05
    6c94f8f	fix issue #105	2019‑12‑05
    afad354	solved issue #105	2019‑12‑05
    474a99e	Merged in WalletTTS_Integration (pull request #2) chidere...	2019‑12‑05
    6412cb9	AHEMM CLOSE BRANCH	2019‑12‑05
    a0d40d6	fix prima gli italiani	2019‑12‑05
    3b43b21	new branch WalletTTS_Integration	2019‑12‑04
    c47fa97	fix first italian issue	2019‑12‑04
    fb779be	2fa for social	2019‑12‑04
    aee9998	reset mail fix	2019‑12‑04
    5f66d63	issue #102	2019‑12‑04
    a16cdec	readme update	2019‑12‑03
    2fe913b	fix empty contact search	2019‑12‑03
    2054cf9	update reset pwd	2019‑12‑03
    3f8a194	Reset password	2019‑12‑03
    80e377e	Merge branch 'master' of https://bitbucket.org/jambtc/bolt	2019‑12‑03
    b8677e1	transaction messages	2019‑12‑03
    a3cdf9b	fix jsTrans in send	2019‑12‑03
    68d4b06	fix issue #99	2019‑12‑03
    399667f	You have no messages to read.	2019‑12‑02
    6a30a63	english messages js	2019‑12‑02

#### Novembre 2019

    97d9012	fixed	2019‑11‑29
    6caf651	fix wallet renew	2019‑11‑29
    f2e9db6	lingua in settings	2019‑11‑29
    b3e1e4d	fix issue #66	2019‑11‑29
    15d0050	fix duplicated notifications	2019‑11‑29
    8314394	footer	2019‑11‑28
    76ea883	2fa	2019‑11‑28
    80d323f	settings	2019‑11‑28
    b46e510	it translation complete (php,java)	2019‑11‑28
    942ce28	js i18n fixed	2019‑11‑28
    5449eec	fix users/view	2019‑11‑27
    588d1c5	js fix	2019‑11‑27
    83bfa3c	push link url	2019‑11‑27
    f0bff25	new webcodecamjs	2019‑11‑27
    971b6b2	fix link to contact	2019‑11‑27
    190a1d2	cGridView fixed	2019‑11‑27
    e3bdc9a	wip cgridview	2019‑11‑26
    337324b	wip yiigridview	2019‑11‑26
    ccd7950	yiiGridView ajax update for contacts	2019‑11‑26
    cfc968b	piccole cose	2019‑11‑25
    3fdc04c	cards	2019‑11‑25
    b12de53	fix bug report in home	2019‑11‑25
    e7bcd48	header contact provider	2019‑11‑25
    31e5d78	fix immagine social login	2019‑11‑25
    98beef3	FIX GOOGLE OAUTH	2019‑11‑25
    d7402a0	fixed google logout, 0x000000 address	2019‑11‑25
    e7e6c0f	only logout	2019‑11‑22
    73ca89d	fix logout google	2019‑11‑22
    b32805b	google oauth	2019‑11‑22
    8ce7e7b	js trans	2019‑11‑22
    9cf699b	final stage	2019‑11‑22
    a22cad0	fix header tx	2019‑11‑22
    ecaeda8	lingua	2019‑11‑22
    1152b6e	no descri	2019‑11‑22
    4c724f3	change header logo	2019‑11‑22
    7a2d8b1	wip google	2019‑11‑21
    bfe9f2f	google oauth	2019‑11‑21
    d6bcd65	prepared controller lang	2019‑11‑21
    1f4deb5	prepared model lang	2019‑11‑21
    7cf69c5	fix users view	2019‑11‑21
    bf7d45d	provider image	2019‑11‑21
    ebcfaf9	fix contacts	2019‑11‑21
    e09bdf4	ContactsController.php edited online with Bitbucket	2019‑11‑21
    c605e02	ContactsController.php edited online with Bitbucket	2019‑11‑21
    870036	fix contact message	2019‑11‑21
    183183c	fix pagination e language	2019‑11‑21
    34cc671	i18n file	2019‑11‑21
    c76144a	Internationalization	2019‑11‑21
    26e5d1d	fix contacts	2019‑11‑21
    c9f5a5d	wip internationalization	2019‑11‑20
    9cf3a90	contact fixed	2019‑11‑20
    39e8a08	header account	2019‑11‑20
    e1de686	update fb e telegram	2019‑11‑20
    4790a3f	test fb	2019‑11‑20
    d7d32cb	test fb	2019‑11‑20
    f947952	fb login	2019‑11‑19
    40f5683	fixes	2019‑11‑19
    ceb4e49	scanfornew ok	2019‑11‑19
    0d55c76	da rivedere scanForNew	2019‑11‑19
    3387e8b	logomail	2019‑11‑19
    4a3a941	fix new user registrazion mail	2019‑11‑19
    c3151f4	fix email signup	2019‑11‑19
    b68fac5	fix select address	2019‑11‑19
    46c1e67	fix notifi wallet_address	2019‑11‑19
    f46dc0e	fix contact - offline	2019‑11‑19
    0adec7c	fix contact search error	2019‑11‑18
    af005e3	css fix	2019‑11‑18
    36025d5	pulse button	2019‑11‑18
    073e680	send & receive notifications	2019‑11‑18
    e514b49	refix	2019‑11‑17
    5264d32	fix getShhPassword	2019‑11‑17
    5ed38ed	change sw	2019‑11‑17
    6b5e5ad	fix checktransaction	2019‑11‑17
    2f5c34c	wip send eth	2019‑11‑17
    cb0a6b4	fix email registered usr	2019‑11‑17
    7eec601	fix tx view	2019‑11‑17
    fe3d5f5	don't show address in mobile	2019‑11‑17
    819330a	fix invalid nonce	2019‑11‑17
    9987c11	new css card	2019‑11‑16
    8775cdf	fix issue css	2019‑11‑16
    457affc	n issues	2019‑11‑16
    3e26109	maxBlocksToScan, push	2019‑11‑16
    920eb5a	send token & istant notification	2019‑11‑16
    aed0556	new transactions logic	2019‑11‑15
    3527ffc	fix transactions	2019‑11‑14
    d450fd3	lavoraccio...	2019‑11‑14
    3ba98af	2 step mm	2019‑11‑13
    92e060e	manage messages	2019‑11‑13
    a87416f	Merge branch 'master' of https://bitbucket.org/jambtc/bolt	2019‑11‑13
    503948b	notify to follow/unfollow contact	2019‑11‑13
    6bfdfb0	fix user	2019‑11‑12
    202f364	fix	2019‑11‑12
    3090d64	go blockchain	2019‑11‑12
    cdff89d	fix get contact address	2019‑11‑12
    8aa811b	minor fixes	2019‑11‑12
    05f8dbc	fixes pin e contact views	2019‑11‑12
    ecb30b5	fix fa-check	2019‑11‑12
    a1ef338	select contact from address book	2019‑11‑12
    ae4b5be	end manage contacts	2019‑11‑12
    43561b2	fix controller	2019‑11‑11
    503a7fb	contacts delete ?	2019‑11‑11
    e22df4e	fix contacts list	2019‑11‑11
    40f039c	manage contacts	2019‑11‑11
    5fe8d05	list contacts image	2019‑11‑09
    c6b866a	add concact	2019‑11‑09
    69727ec	contacts management	2019‑11‑08
    3060fb2	SW pre-cache wip	2019‑11‑08
    4b076d1	received/sent	2019‑11‑08
    4f02c49	...	2019‑11‑08
    4ca4724	gauth	2019‑11‑07
    137d7de	tguserbot	2019‑11‑07
    987ffdb	new telegram class	2019‑11‑06
    6d3fc25	reset mail	2019‑11‑06
    d8e8ee7	fix web-app class + watchtower	2019‑11‑06
    7924d5c	update.sh	2019‑11‑05
    24aec87	header	2019‑11‑05
    edaee39	images	2019‑11‑05
    274c464	fix telegram	2019‑11‑05
    4054523	settings, user, erc20, blockchain	2019‑11‑05
    b472c2e	[sw] logout solved!	2019‑11‑05
    db44b26	solving problems in progress...	2019‑11‑05
    060d31a	bolt danneggiato	2019‑11‑05
    9b827ff	pinutils	2019‑11‑04
    27f4273	settings	2019‑11‑04
    4023e7f	new css mobile	2019‑11‑03
    acd756a	no contacts	2019‑11‑03
    cee2c4c	telegram api	2019‑11‑03
    a2be207	transaction view & details	2019‑11‑03
    0a3578c	fix css, push, logout	2019‑11‑02
    7e33727	other fixes	2019‑11‑01
    fedd6d0	fix css	2019‑11‑01

#### Ottobre 2019

    1b08d15	fixing	2019‑10‑30
    b1cb1c7	SiteController.php edited online with Bitbucket	2019‑10‑29
    526007c	telegram settings & css	2019‑10‑29
    61fa080	bot domain	2019‑10‑29
    251ea82	telegram login successful	2019‑10‑29
    5ac4f84	update.sh	2019‑10‑29
    40a721f	save telegram id	2019‑10‑29
    2724464	Merged in bolt (pull request #1) Bolt Approved-by: jam bitcoin jambtc@gmail.com	2019‑10‑29
    ca01f79	telegram	2019‑10‑29
    936a540	no logout	2019‑10‑28
    943789	hamburger for desktop	2019‑10‑28
    1bb83c8	signup user	2019‑10‑28
    7698076	login wip	2019‑10‑25
    a98a823	1st commit for Bolt	2019‑10‑15


## v0.0.1

**15/10/2019**
    - Initial Release
