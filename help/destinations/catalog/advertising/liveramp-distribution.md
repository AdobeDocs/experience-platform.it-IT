---
title: LiveRamp - Connessione di distribuzione
description: Scopri come utilizzare il connettore LiveRamp - Distribuzione per orchestrare e attivare i tipi di pubblico precedentemente integrati in LiveRamp, per le destinazioni pubblicitarie a valle.
exl-id: 1b11a743-1ef9-4b01-90ef-cc072bc03c91
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '2716'
ht-degree: 38%

---

# Connessione [!DNL LiveRamp - Distribution]

Il [!DNL LiveRamp - Distribution] La connessione consente di attivare i tipi di pubblico da Experienci Platform a publisher premium su dispositivi mobili, web, display e TV connesse.

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti da LiveRamp. Per qualsiasi richiesta o richiesta di aggiornamento, contatta direttamente LiveRamp [qui](mailto:adobertcdp@liveramp.com).

## Destinazioni supportati {#supported-destinations}

[!DNL LiveRamp - Distribution] attualmente supporta l’attivazione del pubblico per le seguenti piattaforme:

* [[!DNL 4C Insights]](#insights)
* [[!DNL Acast]](#acast)
* [[!DNL Nexxen]](#nexxen)
* [[!DNL Ampersand.tv]](#ampersand-tv)
* [[!DNL Captify]](#captify)
* [[!DNL Cardlytics]](#cardlytics)
* [[!DNL Disney (Hulu/ESPN/ABC)]](#disney)
* [[!DNL iHeartMedia]](#iheartmedia)
* [[!DNL Index Exchange]](#index-exchange)
* [[!DNL Magnite CTV Platform]](#magnite)
* [[!DNL Magnite DV+ (Rubicon Project)]](#magnite-dv)
* [[!DNL One Fox]](#fox)
* [[!DNL Pandora]](#pandora)
* [[!DNL Reddit]](#reddit)
* [[!DNL Roku]](#roku)
* [[!DNL Spotify]](#spotify)
* [[!DNL Taboola]](#taboola)
* [[!DNL TargetSpot]](#targetspot)
* [[!DNL Teads]](#teads)
* [[!DNL WB Discovery]](#wb-discovery)

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare il [!DNL LiveRamp - Distribution] destinazione: ecco un caso d’uso di esempio che i clienti di Adobe Experience Platform possono risolvere utilizzando questa destinazione.

Il team marketing di un rivenditore di abbigliamento sportivo ha utilizzato [LiveRamp - Onboarding](liveramp-onboarding.md) connessione per inviare tipi di pubblico da Experienci Platform al loro account LiveRamp.

Attraverso il [!DNL LiveRamp - Distribution] ora possono attivare l&#39;attivazione dei tipi di pubblico integrati al [destinazioni supportate](#supported-destinations). Quindi, possono eseguire il targeting degli utenti su dispositivi mobili, open web, social e [!DNL CTV] piattaforme.

## Onboarding del pubblico in LiveRamp {#onboarding}

Prima di attivare i tipi di pubblico tramite [!DNL LiveRamp - Distribution] connessione, utilizza [LiveRamp - Onboarding](liveramp-onboarding.md) per esportare i tipi di pubblico di Experienci Platform in LiveRamp.

Dopo aver effettuato l’onboarding dei tipi di pubblico in LiveRamp, continua il flusso di lavoro di attivazione da [connettersi alla destinazione](#connect) per selezionare e configurare le piattaforme di destinazione target per l&#39;attivazione dei dati.

## Connetti alla destinazione {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_identifier_settings"
>title="Impostazioni identificatore"
>abstract="Seleziona gli identificatori supportati dalla destinazione. Consulta la documentazione per l’elenco completo degli identificatori supportati per ogni destinazione."

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autentica su LiveRamp {#authenticate}

Per autenticare nella destinazione, compila i campi obbligatori e seleziona **[!UICONTROL Connetti alla destinazione]**.

![Immagine dell’interfaccia utente di Platform che mostra la schermata di connessione di destinazione.l](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-new-connection.png)

* **[!UICONTROL ID organizzazione LiveRamp]**: ID organizzazione dell’account LiveRamp (elencato come _owner_org_ nelle credenziali LiveRamp).
* **[!UICONTROL Password]**: password del tuo account LiveRamp (elencata come _chiave_segreta_ nelle credenziali LiveRamp).
* **[!UICONTROL URL token]**: URL del token LiveRamp.
* **[!UICONTROL Nome utente]**: nome utente del tuo account LiveRamp (elencato come _account_id_ nelle credenziali LiveRamp).

### Configurare i dettagli della destinazione {#destination-details}

Dopo aver effettuato correttamente la connessione all’account LiveRamp, inserisci le informazioni necessarie per connettersi alla destinazione a cui desideri attivare i tipi di pubblico.

![Immagine dell’interfaccia utente di Platform che mostra la schermata dei dettagli della destinazione.l](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-destination-details.png)

* **[!UICONTROL Nome]**: inserisci il nome preferito per la connessione di destinazione.

>[!NOTE]
>
>Per la denominazione della destinazione, Adobe consiglia di seguire questo formato: `LiveRamp - Downstream Destination Name`. Questo modello di denominazione consente di identificare rapidamente le destinazioni in [Sfoglia](../../ui/destinations-workspace.md#browse) dell’area di lavoro destinazioni.
><br>
>Esempio: `LiveRamp - Roku`.

* **[!UICONTROL Descrizione]**: immetti una descrizione per la destinazione. Utilizza una descrizione che ti aiuta a identificare facilmente lo scopo di questa destinazione.
* **[!UICONTROL Destinazione]**: utilizza il menu a discesa per selezionare la destinazione in cui desideri attivare i tipi di pubblico. La destinazione selezionata influisce direttamente su ciò che viene visualizzato in [impostazioni specifiche per la destinazione](#destination-settings) schermo.
* **[!UICONTROL Integrazione]**: seleziona l’account di integrazione da utilizzare per la destinazione.
* **[!UICONTROL Identificatore]**: seleziona gli identificatori supportati dalla destinazione. Attualmente, tutti gli identificatori supportati nelle destinazioni sono precompilati nel menu a discesa.

## Impostazioni specifiche per la destinazione {#destination-settings}

Ognuna delle destinazioni [supportato](#supported-destinations) da [!DNL LiveRamp - Distribution] richiede di compilare opzioni di configurazione specifiche.

Consulta le sezioni seguenti per istruzioni dettagliate su come configurare ciascuna destinazione.

### [!DNL 4C Insights] {#insights}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_4cinsights_profile_id"
>title="ID profilo marchio 4C"
>abstract="Immetti l’ID numerico associato al tuo profilo marchio 4C. Se non disponi di questo ID, contatta il rappresentante dei servizi del cliente 4C."

Per configurare i dettagli per la destinazione, compila i campi seguenti.

![Immagine dell’interfaccia utente di Platform che mostra i campi dati del cliente per la destinazione 4C Insights.](../../assets/catalog/advertising/liveramp-distribution/LR_4C_DestSpecific.png)

* **[!UICONTROL ID profilo marchio 4C]**: immetti l’ID numerico associato al tuo profilo marchio 4C. Se non disponi di questo ID, contatta il rappresentante dei servizi del cliente 4C.

### [!DNL Acast] {#acast}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_acast_client"
>title="Nome cliente"
>abstract="Il nome dell’account dell’inserzionista, come desideri che appaia al partner di destinazione. Utilizza il nome della tua azienda. Non utilizzare spazi o caratteri speciali."

Per configurare i dettagli per la destinazione, compila i campi seguenti.

![Immagine dell’interfaccia utente di Platform che mostra i campi dati del cliente per la destinazione Acast.](../../assets/catalog/advertising/liveramp-distribution/LR_Acast_DestSpecific.png)

* **[!UICONTROL Nome client]**: nome dell’account dell’inserzionista, che desideri mostrare al partner di destinazione. Utilizza il nome della tua azienda. Non utilizzare spazi o caratteri speciali.

### [!DNL Ampersand.tv] {#ampersand-tv}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_ampersand_company_name"
>title="Nome società"
>abstract="Il nome della società, come desideri che appaia al partner di destinazione. Non utilizzare spazi o caratteri speciali."

Per configurare i dettagli per la destinazione, compila i campi seguenti.

![Immagine dell’interfaccia utente di Platform che mostra i campi dati del cliente per la destinazione e commerciale.](../../assets/catalog/advertising/liveramp-distribution/LR_Ampersand_DestSpecific.png)

* **[!UICONTROL Nome società]**: nome della tua azienda, come desideri che venga mostrato al partner di destinazione. Non utilizzare spazi o caratteri speciali.

### [!DNL Captify] {#captify}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_captify_client"
>title="Nome cliente"
>abstract="Il nome dell’account dell’inserzionista, come desideri che appaia al partner di destinazione. Utilizza il nome della tua azienda. Non utilizzare spazi o caratteri speciali."

Per configurare i dettagli per la destinazione, compila i campi seguenti.

![Immagine dell’interfaccia utente di Platform che mostra i campi dati del cliente per la destinazione Captify.](../../assets/catalog/advertising/liveramp-distribution/LR_Captify_DestSpecific.png)

* **[!UICONTROL Nome client]**: nome dell’account dell’inserzionista, che desideri mostrare al partner di destinazione. Utilizza il nome della tua azienda. Non utilizzare spazi o caratteri speciali.

### [!DNL Cardlytics] {#cardlytics}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_cardlytics_client"
>title="Nome cliente"
>abstract="Il nome dell’account dell’inserzionista, come desideri che appaia al partner di destinazione. Utilizza il nome della tua azienda. Non utilizzare spazi o caratteri speciali."

Per configurare i dettagli per la destinazione, compila i campi seguenti.

![Immagine dell’interfaccia utente di Platform che mostra i campi dati del cliente per la destinazione CardAnalytics.](../../assets/catalog/advertising/liveramp-distribution/LR_Cardlytics_DestSpecific.png)

* **[!UICONTROL Nome client]**: nome dell’account dell’inserzionista, che desideri mostrare al partner di destinazione. Utilizza il nome della tua azienda. Non utilizzare spazi o caratteri speciali.

### [!DNL Disney (Hulu/ESPN/ABC)] {#disney}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_agreement"
>title="Accordo sui termini di destinazione dei dati per gli inserzionisti"
>abstract="Digita `I AGREE` per confermare l’accettazione e l’accordo alle condizioni dei dati degli inserzionisti Disney."

<!-- >additional-url="<https://www.disneyadvertising.com/ADVERTISER-DATA-DESTINATION-TERMS/>" text="Read the agreement" -->

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_disney_client"
>title="Nome cliente"
>abstract="Il nome dell’account dell’inserzionista, come desideri che appaia al partner di destinazione. Utilizza il nome della tua azienda. Non utilizzare spazi o caratteri speciali."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_disney_email"
>title="Indirizzo e-mail"
>abstract="Inserisci un indirizzo e-mail associato a un individuo. Questo indirizzo e-mail funge da firma per il contratto sulle condizioni dei dati dell’inserzionista. Se necessario, questo indirizzo e-mail verrà utilizzato anche per contattarti."

Per configurare i dettagli per la destinazione, compila i campi seguenti.

![Immagine dell’interfaccia utente della piattaforma che mostra i campi dati del cliente per la destinazione Disney.](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-disney-fields.png)

* **[!UICONTROL Accordo sui termini di destinazione dei dati per gli inserzionisti]**: digita `I AGREE` confermare il riconoscimento e l&#39;accordo ai termini di dati degli inserzionisti Disney.
* **[!UICONTROL Nome client]**: inserisci il nome della tua società come desideri che venga mostrato al partner di destinazione.
* **[!UICONTROL Indirizzo e-mail]**: immetti un indirizzo e-mail associato a un individuo. Questo indirizzo e-mail funge da firma per il contratto sulle condizioni dei dati dell’inserzionista.

### [!DNL iHeartMedia] {#iheartmedia}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_iheartmedia_client"
>title="Nome cliente"
>abstract="Il nome dell’account dell’inserzionista, come desideri che appaia al partner di destinazione. Utilizza il nome della tua azienda. Non utilizzare spazi o caratteri speciali."

Per configurare i dettagli per la destinazione, compila i campi seguenti.

![Immagine dell’interfaccia utente di Platform che mostra i campi dati del cliente per la destinazione iHeartMedia.](../../assets/catalog/advertising/liveramp-distribution/LR_iHeart_DestSpecific.png)

* **[!UICONTROL Nome client]**: nome dell’account dell’inserzionista, che desideri mostrare al partner di destinazione. Utilizza il nome della tua azienda. Non utilizzare spazi o caratteri speciali.

### [!DNL Index Exchange] {#index-exchange}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_index_advertiseraccountname"
>title="Nome account"
>abstract="Nome dell’account cliente di Index Exchange. Non utilizzare spazi o caratteri speciali."

Per configurare i dettagli per la destinazione, compila i campi seguenti.

![Immagine dell’interfaccia utente di Platform che mostra i campi dati del cliente per la destinazione Index Exchange.](../../assets/catalog/advertising/liveramp-distribution/LR_IndexExchange_DestSpecific.png)

* **[!UICONTROL Nome account]**: nome dell’account client di Exchange dell’indice. Non utilizzare spazi o caratteri speciali.

### [!DNL Magnite CTV Platform] {#magnite}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_magnitectv_client"
>title="Client"
>abstract="Il nome dell’account, come desideri che appaia al partner di destinazione. Utilizza il nome della tua azienda. Non utilizzare spazi o caratteri speciali."

Per configurare i dettagli per la destinazione, compila i campi seguenti.

![Immagine dell&#39;interfaccia utente di Platform che mostra i campi dati cliente per la destinazione Magnite CTV.](../../assets/catalog/advertising/liveramp-distribution/LR_MagniteCTV_DestSpecific.png)

* **[!UICONTROL Client]**: il nome del cliente, come desideri che venga mostrato al partner di destinazione. Utilizza il nome della tua azienda. Non utilizzare spazi o caratteri speciali.

### [!DNL Magnite DV+ (Rubicon Project)] {#magnite-dv}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_magnitedv+_partnerid"
>title="ID partner"
>abstract="L’ID partner di Rubicon Project associato all’editore a cui appartiene il segmento o i dati. Contatta il rappresentante account di Rubicon Project in caso di dubbi sul valore da utilizzare."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_magnitedv+_seatid"
>title="ID postazione"
>abstract="ID postazione Magnite DV+ fornito dal tuo account manager Magnite"

Per configurare i dettagli per la destinazione, compila i campi seguenti.

![Immagine dell&#39;interfaccia utente di Platform che mostra i campi dati del cliente per la destinazione Magnite DV+.](../../assets/catalog/advertising/liveramp-distribution/LR_MagniteDV_DestSpecific.png)

* **[!UICONTROL ID partner]**: ID partner del progetto Rubicon associato all’editore proprietario del segmento o dei dati. Contatta il rappresentante account di Rubicon Project in caso di dubbi sul valore da utilizzare.
* **[!UICONTROL ID posto]**: Magnite DV+ Seat ID fornito dall&#39;account manager Magnite

### [!DNL Nexxen (formerly known as [!DNL Amobee])] {#nexxen}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_nexxen_ratetype"
>title="Tipo di tariffa"
>abstract="Il tipo di tariffa rappresenta il modo in cui l’utilizzo dei dati deve essere fatturato. Tutte le tariffe 0,00$ devono essere a prezzo fisso. Se non sai con certezza quale tipo di tariffa utilizzare, contatta il rappresentante Nexxen."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_nexxen_marketid"
>title="ID mercato"
>abstract="Immetti l’ID di mercato numerico in cui creare il contratto dati Nexxen. Se stai facendo la sindacazione “AlwaysOn” in ogni mercato della piattaforma Nexxen, immetti -1."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_nexxen_advertiserid"
>title="ID inserzionista"
>abstract="Se invii dati a un singolo inserzionista sulla piattaforma Nexxen, immetti l’ID inserzionista numerico Amobee. Se desideri rendere i dati disponibili a tutti gli inserzionisti in un mercato o se questi segmenti sono “AlwaysOn”, immetti -1."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_nexxen_contactemail"
>title="E-mail di contatto"
>abstract="Inserisci l’indirizzo e-mail che Nexxen deve utilizzare per inviare i dettagli del contratto dati. Probabilmente si tratta del tuo indirizzo e-mail, ma può anche essere un alias e-mail. Per più destinatari, separa utilizzando le virgole (`email1@domain.com`, `email2@domain.com` e così via.)."

Per configurare i dettagli per la destinazione, compila i campi seguenti.

![Immagine dell’interfaccia utente di Platform che mostra i campi dati del cliente per la destinazione Nexxen.](../../assets/catalog/advertising/liveramp-distribution/LR_Nexxen_DestSpecific.png)

* **[!UICONTROL Tipo di tariffa]**: il tipo di tariffa rappresenta il modo in cui l’utilizzo dei dati deve essere fatturato. Tutte le tariffe 0,00$ devono essere a prezzo fisso. Se non sai con certezza quale tipo di tariffa utilizzare, contatta il rappresentante Nexxen.
* **[!UICONTROL ID mercato]**: immetti l’ID di mercato numerico in cui creare il contratto dati Nexxen. Se stai facendo la sindacazione “AlwaysOn” in ogni mercato della piattaforma Nexxen, immetti -1.
* **[!UICONTROL ID inserzionista]**: se invii dati a un singolo inserzionista sulla piattaforma Nexxen, immetti l’ID inserzionista numerico Nexxen. Se si desidera rendere i dati disponibili a tutti gli inserzionisti in un mercato o se questi segmenti sono &quot;AlwaysOn&quot;, immettere -1.
* **[!UICONTROL E-mail di contatto]**: immetti l’indirizzo e-mail che Nexxen deve utilizzare per inviare i dettagli del contratto dei dati. Probabilmente si tratta del tuo indirizzo e-mail, ma può anche essere un alias e-mail. Per più destinatari, separa utilizzando le virgole ( `email1@domain.com`, `email2@domain.com`).

### [!DNL One Fox] {#fox}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_fox_client"
>title="Client"
>abstract="Il nome dell’azienda/account di distribuzione che si desidera venga visualizzato al partner. In caso di dubbi sul nome da utilizzare, contatta il rappresentante del tuo account partner. Non utilizzare spazi o caratteri speciali."

Per configurare i dettagli per la destinazione, compila i campi seguenti.

![Immagine dell’interfaccia utente di Platform che mostra i campi dati del cliente per la destinazione One Fox.](../../assets/catalog/advertising/liveramp-distribution/LR_Fox_DestSpecific.png)

* **[!UICONTROL Client]**: nome dell’azienda/account di distribuzione che desideri venga visualizzato al partner. Utilizza il nome della tua azienda per impostazione predefinita. In caso di dubbi sul nome da utilizzare, contatta il rappresentante del tuo account partner. Non utilizzare spazi o caratteri speciali.

### [!DNL Pandora] {#pandora}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_account_name"
>title="Nome account"
>abstract="Il nome del tuo account Pandora. Contatta il rappresentante del tuo account Pandora se non sai con certezza quale sia il nome del tuo account. Non utilizzare spazi o caratteri speciali."

Per configurare i dettagli per la destinazione, compila i campi seguenti.

![Immagine dell’interfaccia utente di Platform che mostra i campi dati del cliente per la destinazione Pandora.](../../assets/catalog/advertising/liveramp-distribution/LR_Pandora_DestSpecific.png)

* **[!UICONTROL Nome account]**: nome del tuo account Pandora. Contatta il rappresentante del tuo account Pandora se non sai con certezza quale sia il nome del tuo account. Non utilizzare spazi o caratteri speciali.

### [!DNL Reddit] {#reddit}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_reddit_advertiser_id"
>title="ID inserzionista Reddit"
>abstract="Il tuo ID inserzionista Reddit. Deve iniziare con “t2_” o “a2_”. Se non conosci il tuo ID inserzionista, contatta il rappresentante Reddit."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_reddit_advertiser_name"
>title="Nome inserzionista Reddit"
>abstract="Il tuo nome inserzionista Reddit. Non utilizzare spazi o caratteri speciali."

Per configurare i dettagli per la destinazione, compila i campi seguenti.

![Immagine dell’interfaccia utente di Platform che mostra i campi dati del cliente per la destinazione Reddit.](../../assets/catalog/advertising/liveramp-distribution/LR_Reddit_DestSpecific.png)

* **[!UICONTROL ID inserzionista Reddit]**: ID inserzionista Reddit. Deve iniziare con “t2_” o “a2_”. Se non conosci il tuo ID inserzionista, contatta il rappresentante Reddit.
* **[!UICONTROL Modifica nome inserzionista]**: nome dell’inserzionista Reddit. Non utilizzare spazi o caratteri speciali.

### [!DNL Roku] {#roku}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_roku_email"
>title="Indirizzo e-mail dell’account Roku"
>abstract="Inserisci l’indirizzo e-mail associato al tuo account Roku."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_roku_representative_email"
>title="Indirizzo e-mail del rappresentante dell’account Roku"
>abstract="Inserisci l’indirizzo e-mail del rappresentante del tuo account Roku. Questo indirizzo viene utilizzato per inviare aggiornamenti della tassonomia. Per immettere più indirizzi, separali con virgole."

Per configurare i dettagli per la destinazione, compila i campi seguenti.

![Immagine dell’interfaccia utente di Platform che mostra gli identificatori supportati per la destinazione Roku.](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-roku-fields.png)

* **[!UICONTROL Indirizzo e-mail dell’account Roku]**: immetti l’indirizzo e-mail associato al tuo account Roku.
* **[!UICONTROL Indirizzo e-mail del rappresentante dell’account Roku]**: immetti l’indirizzo e-mail del rappresentante del tuo account Roku. Per immettere più indirizzi, separali con virgole.

### [!DNL Spotify] {#spotify}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_spotify_client"
>title="Nome cliente"
>abstract="Il nome dell’account dell’inserzionista, come desideri che appaia al partner di destinazione. Utilizza il nome della tua azienda. Non utilizzare spazi o caratteri speciali."

Per configurare i dettagli per la destinazione, compila i campi seguenti.

![Immagine dell’interfaccia utente di Platform che mostra gli identificatori supportati per la destinazione Spotify.](../../assets/catalog/advertising/liveramp-distribution/LR_Spotify_DestSpecific.png)

* **[!UICONTROL Nome client]**: nome dell’account dell’inserzionista, che desideri mostrare al partner di destinazione. Utilizza il nome della tua azienda. Non utilizzare spazi o caratteri speciali.

### [!DNL Taboola] {#taboola}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_taboola_rep_email"
>title="Indirizzo e-mail dell’account manager"
>abstract="Indirizzo e-mail del tuo account manager Taboola."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_taboola_seg_type"
>title="Tipo di segmento"
>abstract="Il tipo di segmento. Al momento sono supportati solo i segmenti di prime parti."

Per configurare i dettagli per la destinazione, compila i campi seguenti.

![Immagine dell’interfaccia utente di Platform che mostra gli identificatori supportati per la destinazione Tabula.](../../assets/catalog/advertising/liveramp-distribution/LR_Taboola_DestSpecific.png)

* **[!UICONTROL Indirizzo e-mail dell’account manager]**: indirizzo e-mail dell’account manager Tabula.
* **[!UICONTROL Tipo di segmento]**: tipo di segmento. Al momento sono supportati solo i segmenti di prime parti.

### [!DNL TargetSpot] {#targetspot}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_targetspot_client"
>title="Nome cliente"
>abstract="Il nome dell’account dell’inserzionista, come desideri che appaia al partner di destinazione. Utilizza il nome della tua azienda. Non utilizzare spazi o caratteri speciali."

Per configurare i dettagli per la destinazione, compila i campi seguenti.

![Immagine dell’interfaccia utente di Platform che mostra gli identificatori supportati per la destinazione TargetSpot.](../../assets/catalog/advertising/liveramp-distribution/LR_TargetSpot_DestSpecific.png)

* **[!UICONTROL Nome client]**: nome dell’account dell’inserzionista, che desideri mostrare al partner di destinazione. Utilizza il nome della tua azienda. Non utilizzare spazi o caratteri speciali.

### [!DNL Teads] {#teads}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_teads_teadsid"
>title="ID Teads"
>abstract="Il tuo ID Teads"

Per configurare i dettagli per la destinazione, compila i campi seguenti.

![Immagine dell’interfaccia utente di Platform che mostra gli identificatori supportati per la destinazione TargetSpot.](../../assets/catalog/advertising/liveramp-distribution/LR_Teads_DestSpecific.png)

* **[!UICONTROL ID teads]**: ID Teads

### [!DNL WB Discovery] {#wb-discovery}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_wb_client"
>title="Nome cliente"
>abstract="Il nome dell’account dell’inserzionista, come desideri che appaia al partner di destinazione. Utilizza il nome della tua azienda. Non utilizzare spazi o caratteri speciali."

Per configurare i dettagli per la destinazione, compila i campi seguenti.

![Immagine dell&#39;interfaccia utente di Platform che mostra gli identificatori supportati per la destinazione WB Discovery.](../../assets/catalog/advertising/liveramp-distribution/LR_WBD_DestSpecific.png)

* **[!UICONTROL Nome client]**: nome dell’account dell’inserzionista, che desideri mostrare al partner di destinazione. Utilizza il nome della tua azienda. Non utilizzare spazi o caratteri speciali.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Per ricevere notifiche sullo stato del flusso di dati, seleziona un avviso dall’elenco. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva il pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Il [!DNL LiveRamp - Distribution] attiva i tipi di pubblico già caricati sul tuo account LiveRamp tramite [LiveRamp - Onboarding](liveramp-onboarding.md) connessione.

Per attivare correttamente i tipi di pubblico, devi selezionare **stesso pubblico** che hai [precedentemente onboarded](liveramp-onboarding.md) su LiveRamp.

>[!IMPORTANT]
>
>Selezione di tipi di pubblico per i quali non è stato eseguito l’onboarding in precedenza tramite [LiveRamp - Onboarding](liveramp-onboarding.md) la connessione non attiva l’onboarding dei nuovi tipi di pubblico.

## Dati esportati / Convalida esportazione dati {#exported-data}

Per verificare e monitorare l&#39;attivazione dei tipi di pubblico, accedi al tuo account LiveRamp e controlla le metriche di attivazione.

Se hai domande sull&#39;attivazione del pubblico, contatta il rappresentante del tuo account LiveRamp.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

Per ulteriori dettagli su come configurare [!DNL LiveRamp - Onboarding] destinazione, vedere [LiveRamp - Documentazione di onboarding](liveramp-onboarding.md).
