---
title: LiveRamp - Connessione di distribuzione
description: Scopri come utilizzare il connettore LiveRamp - Distribuzione per attivare i tipi di pubblico precedentemente integrati in LiveRamp, per altre destinazioni pubblicitarie.
hide: true
hidefromtoc: true
source-git-commit: c04c7ff4f1ab45d944f4ab516d7842df536fae40
workflow-type: tm+mt
source-wordcount: '1475'
ht-degree: 40%

---


# Connessione [!DNL LiveRamp - Distribution] {#liveramp-onboarding}

Il [!DNL LiveRamp - Distribution] La connessione consente di attivare i tipi di pubblico da Experienci Platform a publisher premium su dispositivi mobili, web, display e TV connesse.

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti da LiveRamp. Per qualsiasi richiesta o richiesta di aggiornamento, contatta direttamente LiveRamp [qui](mailto:example@email.com).

## Destinazioni supportati {#supported-destinations}

[!DNL LiveRamp - Distribution] attualmente supporta l’attivazione del pubblico per le seguenti piattaforme:

* [!DNL 4C Insights]
* [!DNL Acast]
* [!DNL Amobee]
* [!DNL Ampersand.tv]
* [!DNL Captify]
* [!DNL Cardlytics]
* [[!DNL Disney (Hulu/ESPN/ABC)]](#disney)
* [!DNL iHeartMedia]
* [!DNL Index Exchange]
* [!DNL Magnite CTV Platform]
* [!DNL Magnite DV+ (Rubicon Project)]
* [!DNL One Fox]
* [!DNL Pandora]
* [!DNL Reddit]
* [[!DNL Roku]](#roku)
* [!DNL Spotify]
* [!DNL Taboola]
* [!DNL TargetSpot]
* [!DNL Teads]
* [!DNL WB Discovery]

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare il [!DNL LiveRamp - Distribution] destinazione: ecco un caso d’uso di esempio che i clienti di Adobe Experience Platform possono risolvere utilizzando questa destinazione.

Il team marketing di un rivenditore di abbigliamento sportivo ha utilizzato [LiveRamp - Onboarding](liveramp-onboarding.md) connessione per inviare tipi di pubblico da Experienci Platform al loro account LiveRamp.

Attraverso il [!DNL LiveRamp - Distribution] connessione ora possono attivare l’attivazione dei tipi di pubblico onboarded per le destinazioni menzionate nella parte superiore di questa pagina, in modo da poter indirizzare gli utenti su dispositivi mobili, open web, social e [!DNL CTV] piattaforme.

## Onboarding del pubblico in LiveRamp {#onboarding}

Prima di attivare i tipi di pubblico tramite [!DNL LiveRamp - Distribution] connessione, utilizza [LiveRamp - Onboarding](liveramp-onboarding.md) per esportare i tipi di pubblico di Experienci Platform in LiveRamp.

Dopo aver effettuato l’onboarding dei tipi di pubblico in LiveRamp, continua il flusso di lavoro di attivazione da [connettersi alla destinazione](#connect) passaggio.

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

* **[!UICONTROL URL token]**: URL del token LiveRamp.
* **[!UICONTROL ID organizzazione LiveRamp]**: ID organizzazione dell’account LiveRamp.
* **[!UICONTROL Nome utente]**: nome utente del tuo account LiveRamp.
* **[!UICONTROL Password]**: password del tuo account LiveRamp.

### Configurare i dettagli della destinazione {#destination-details}

Dopo aver effettuato correttamente la connessione all’account LiveRamp, inserisci le informazioni necessarie per connettersi alla destinazione a cui desideri attivare i tipi di pubblico.

![Immagine dell’interfaccia utente di Platform che mostra la schermata dei dettagli della destinazione.l](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-destination-details.png)

* **[!UICONTROL Nome]**: inserisci il nome preferito per la connessione di destinazione.
* **[!UICONTROL Descrizione]**: immetti una descrizione per la destinazione. Utilizza una descrizione che ti aiuterà a identificare facilmente lo scopo di questa destinazione.
* **[!UICONTROL Destinazione]**: utilizza il menu a discesa per selezionare la destinazione in cui desideri attivare i tipi di pubblico. La destinazione selezionata influisce direttamente su ciò che viene visualizzato in [impostazioni specifiche per la destinazione](#destination-settings) schermo.
* **[!UICONTROL Integrazione]**: seleziona l’account di integrazione da utilizzare per la destinazione.
* **[!UICONTROL Identificatore]**: seleziona gli identificatori supportati dalla destinazione. Attualmente, tutti gli identificatori supportati nelle destinazioni sono precompilati nel menu a discesa.

## Impostazioni specifiche per la destinazione {#destination-settings}

Ognuna delle destinazioni [supportato](#supported-destinations) da [!DNL LiveRamp - Onboarding] richiede di compilare opzioni di configurazione specifiche.

Consulta le sezioni seguenti per istruzioni dettagliate su come configurare ciascuna destinazione.

### [!DNL 4C Insights] {#insights}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_4cinsights_profile_id"
>title="ID profilo marchio 4C"
>abstract="Immetti l’ID numerico associato al tuo profilo marchio 4C. Se non disponi di questo ID, contatta il rappresentante dei servizi del cliente 4C."

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

### [!DNL Acast] {#acast}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_acast_client"
>title="Nome cliente"
>abstract="Il nome dell’account dell’inserzionista, come desideri che appaia al partner di destinazione. Utilizza il nome della tua azienda. Non utilizzare spazi o caratteri speciali."

### [!DNL Amobee] {#amobee}

### [!DNL Ampersand.tv] {#ampersand-tv}

### [!DNL Captify] {#captify}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_captify_client"
>title="Nome cliente"
>abstract="Il nome dell’account dell’inserzionista, come desideri che appaia al partner di destinazione. Utilizza il nome della tua azienda. Non utilizzare spazi o caratteri speciali."

### [!DNL Cardlytics] {#cardlytics}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_cardlytics_client"
>title="Nome cliente"
>abstract="Il nome dell’account dell’inserzionista, come desideri che appaia al partner di destinazione. Utilizza il nome della tua azienda. Non utilizzare spazi o caratteri speciali."

### [!DNL Disney (Hulu/ESPN/ABC)] {#disney}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_agreement"
>title="Accordo sui termini di destinazione dei dati per gli inserzionisti"
>abstract="Digita `I AGREE` per confermare il riconoscimento e l’accordo alle condizioni dei dati degli inserzionisti Disney."
>additional-url="https://www.disneyadvertising.com/ADVERTISER-DATA-DESTINATION-TERMS/" text="Leggi l’accordo"

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

### [!DNL Index Exchange] {#index-exchange}

### [!DNL Magnite CTV Platform] {#magnite}

### [!DNL Magnite DV+ (Rubicon Project)] {#magnite-dv}

### [!DNL One Fox] {#fox}

### [!DNL Pandora] {#pandora}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_data_provider_name"
>title="Nome provider dati"
>abstract="Il nome della tua azienda come desideri che venga mostrato a Pandora. Il nome può contenere un massimo di 40 caratteri alfanumerici e minuscoli (ad esempio, My_Company)."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_rep_email"
>title="Indirizzo e-mail rappresentante account"
>abstract="L’indirizzo e-mail del rappresentante del tuo account Pandora. Questo indirizzo viene utilizzato per inviare aggiornamenti della tassonomia. Per immettere più indirizzi, separali con virgole."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_email"
>title="Indirizzo e-mail"
>abstract="Questo indirizzo viene utilizzato per inviare aggiornamenti della tassonomia. Per immettere più indirizzi, separali con virgole."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_account_name"
>title="Nome account"
>abstract="Il nome del tuo account Pandora. Contatta il rappresentante del tuo account Pandora se non sai con certezza quale sia il nome del tuo account. Non utilizzare spazi o caratteri speciali."

### [!DNL Reddit] {#reddit}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_reddit_advertiser_id"
>title="ID inserzionista Reddit"
>abstract="Il tuo ID inserzionista Reddit. Deve iniziare con “t2_” o “a2_”. Se non conosci il tuo ID inserzionista, contatta il rappresentante Reddit."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_reddit_advertiser_name"
>title="Nome inserzionista Reddit"
>abstract="Il tuo nome inserzionista Reddit. Non utilizzare spazi o caratteri speciali."

### Roku {#roku}

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

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_spotify_account_token"
>title="Token account"
>abstract="Identificatore alfanumerico che indica a Spotify dove trasferire i dati e che l’utente è autorizzato all’utilizzo di questo flusso di lavoro. Per ottenere questo token, contatta il tuo account manager Spotify."

### [!DNL Taboola] {#taboola}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_taboola_rep_email"
>title="Indirizzo e-mail dell’account manager"
>abstract="Indirizzo e-mail del tuo account manager Taboola."

### [!DNL TargetSpot] {#targetspot}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_targetspot_client"
>title="Nome cliente"
>abstract="Il nome dell’account dell’inserzionista, come desideri che appaia al partner di destinazione. Utilizza il nome della tua azienda. Non utilizzare spazi o caratteri speciali."

### [!DNL Teads] {#teads}

### [!DNL WB Discovery] {#wb-discovery}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_wb_client"
>title="Nome cliente"
>abstract="Il nome dell’account dell’inserzionista, come desideri che appaia al partner di destinazione. Utilizza il nome della tua azienda. Non utilizzare spazi o caratteri speciali."

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva il pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Il [!DNL LiveRamp - Distribution] attiva i tipi di pubblico già caricati sul tuo account LiveRamp tramite [LiveRamp - Onboarding](liveramp-onboarding.md) connessione.

Per attivare correttamente i tipi di pubblico, in questo passaggio devi selezionare **stesso pubblico** che hai precedentemente effettuato l&#39;onboarding in LiveRamp.

>[!IMPORTANT]
>
>La selezione di tipi di pubblico che non sono stati precedentemente caricati su LiveRamp non attiva l&#39;onboarding dei nuovi tipi di pubblico.

## Dati esportati / Convalida esportazione dati {#exported-data}

Per verificare e monitorare l&#39;attivazione dei tipi di pubblico, accedi al tuo account LiveRamp e controlla le metriche di attivazione.

Se hai domande sull’attivazione del pubblico, contatta il rappresentante del tuo account LiveRamp.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

Per ulteriori dettagli su come configurare [!DNL LiveRamp - Onboarding] di archiviazione, vedere [documentazione ufficiale](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).
