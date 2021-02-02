---
keywords: targhette di bordo;destinazione di volo
title: Destinazione tag di volo
seo-title: Destinazione dei tag di volo
description: Trasmettete senza problemi  dati Adobi di pubblico a Airship come tag di pubblico per il targeting all'interno di Airship.
seo-description: Trasmettete senza problemi  dati Adobi di pubblico a Airship come tag di pubblico per il targeting all'interno di Airship.
translation-type: tm+mt
source-git-commit: 95f57f9d1b3eeb0b16ba209b9774bd94f5758009
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 1%

---


# (Beta) [!DNL Airship Tags] destinazione {#airship-tags-destination}

>[!IMPORTANT]
>
>La destinazione [!DNL Airship Tags] in Adobe Experience Platform è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

## Panoramica

[!DNL Airship] è la principale piattaforma di coinvolgimento dei clienti, che ti consente di distribuire messaggi omnicanale significativi e personalizzati agli utenti in ogni fase del ciclo di vita del cliente.

Questa integrazione trasmette i dati del segmento Adobe Experience Platform in [!DNL Airship] come [Tag](https://docs.airship.com/guides/audience/tags/) per il targeting o l&#39;attivazione.

Per ulteriori informazioni su [!DNL Airship], vedere la [Airship Docs](https://docs.airship.com).


>[!TIP]
>
>Questa pagina della documentazione è stata creata dal team [!DNL Airship]. Per qualsiasi richiesta di informazioni o di aggiornamento, contattateli direttamente all&#39;indirizzo [support.airship.com](https://support.airship.com/).

## Prerequisiti

Prima di inviare i segmenti Adobe Experience Platform a [!DNL Airship], è necessario:

* Create un gruppo di tag nel progetto [!DNL Airship].
* Generare un token al portatore per l&#39;autenticazione.

>[!TIP]
> 
>Crea un account [!DNL Airship] tramite [questo collegamento di registrazione](https://go.airship.eu/accounts/register/plan/starter/), se non lo hai già fatto.

### Gruppi di tag

Il concetto di segmenti in Adobe Experience Platform è simile a [Tags](https://docs.airship.com/guides/audience/tags/) in Airship, con lievi differenze nell&#39;implementazione. Questa integrazione mappa lo stato dell&#39;appartenenza di un utente [in un segmento di Experience Platform ](https://experienceleague.adobe.com/docs/experience-platform/xdm/mixins/profile/segmentation.html?lang=en#mixins) alla presenza o alla non presenza di un tag [!DNL Airship]. Ad esempio, in un segmento della piattaforma in cui `xdm:status` diventa `realized`, il tag viene aggiunto al canale [!DNL Airship] o all&#39;utente con nome a cui è associato questo profilo. Se il tag `xdm:status` viene modificato in `exited`, il tag viene rimosso.

Per abilitare questa integrazione, create un *gruppo di tag* in [!DNL Airship] denominato `adobe-segments`.

>[!IMPORTANT]
>
>Quando create il nuovo gruppo di tag **Non selezionate** il pulsante di scelta che riporta &quot;[!DNL Allow these tags to be set only from your server]&quot;. In questo modo l&#39;integrazione dei tag di Adobe  non riuscirà.

Per istruzioni sulla creazione del gruppo di tag, consultate [Gestisci gruppi di tag](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups).

### Token portatore

Passare a **[!UICONTROL Settings]**&quot; **[!UICONTROL APIs & Integrations]** nel [Pannello di navigazione](https://go.airship.com) e selezionare **[!UICONTROL Tokens]** nel menu a sinistra.

Fai clic su **[!UICONTROL Create Token]**.

Immettete un nome di facile utilizzo per il token, ad esempio &quot;Destinazione tag di Adobe &quot;, quindi selezionate &quot;Accesso completo&quot; per il ruolo.

Fare clic su **[!UICONTROL Create Token]** e salvare i dettagli come riservati.

## Casi di utilizzo

Per comprendere meglio come e quando utilizzare la destinazione [!DNL Airship Tags], di seguito sono riportati alcuni esempi di casi di utilizzo che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Caso di utilizzo n. 1

I retailer o le piattaforme di intrattenimento possono creare profili utente sui clienti fedeli e trasferire tali segmenti in [!DNL Airship] per il targeting dei messaggi sulle campagne mobili.

### Caso di utilizzo n. 2

Attiva messaggi uno-a-uno in tempo reale quando gli utenti entrano o escono da segmenti specifici in Adobe Experience Platform.

Ad esempio, un rivenditore imposta un segmento specifico del marchio jeans in Platform. Il rivenditore può ora attivare un messaggio mobile non appena qualcuno imposta la propria preferenza jeans su un marchio specifico.

## Connetti a [!DNL Airship Tags] {#connect-airship-tags}

In **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, scorrere fino alla categoria **[!UICONTROL Mobile Engagement]**. Selezionare **[!DNL Airship Tags]**, quindi selezionare **[!UICONTROL Configure]**.

>[!NOTE]
>
>Se esiste già una connessione con questa destinazione, è possibile visualizzare un pulsante **[!UICONTROL Activate]** sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, fare riferimento alla sezione [Catalog](../../ui/destinations-workspace.md#catalog) della documentazione relativa all&#39;area di lavoro di destinazione.

![Connetti ai tag del volo](../../assets/catalog/mobile-engagement/airship-tags/catalog.png)

Nel passaggio **Account**, se in precedenza è stata impostata una connessione alla destinazione [!DNL Airship Tags], selezionare **[!UICONTROL Existing Account]** e selezionare la connessione esistente. In alternativa, è possibile selezionare **[!UICONTROL New Account]** per impostare una nuova connessione a [!DNL Airship Tags]. Selezionare **[!UICONTROL Connect to destination]** per collegare Adobe Experience Platform al progetto [!DNL Airship] utilizzando il token del portatore generato dal dashboard [!DNL Airship].

>[!NOTE]
>
>Adobe Experience Platform supporta la convalida delle credenziali nel processo di autenticazione e visualizza un messaggio di errore se vengono immesse credenziali non corrette nell&#39;account [!DNL Airship]. In questo modo si evita di completare il flusso di lavoro con credenziali non corrette.

![Connetti ai tag del volo](../../assets/catalog/mobile-engagement/airship-tags/connect-account.png)

Una volta confermate le credenziali e che Adobe Experience Platform è connesso al progetto [!DNL Airship], puoi selezionare **[!UICONTROL Next]** per passare al passaggio **[!UICONTROL Setup]**.

Nel passaggio **[!UICONTROL Authentication]**, immettete un **[!UICONTROL Name]** e un **[!UICONTROL Description]** per il flusso di attivazione.

Inoltre, in questo passaggio è possibile selezionare un centro dati USA o UE, a seconda del centro dati [!DNL Airship] applicato a questa destinazione. Infine, selezionare uno o più casi di utilizzo del marketing per i quali i dati verranno esportati nella destinazione. Puoi scegliere tra  casi di utilizzo di marketing definiti dal Adobe o creare un tuo. Per ulteriori informazioni sui casi di utilizzo del marketing, vedere la [panoramica dei criteri di utilizzo dei dati](../../../data-governance/policies/overview.md).

Selezionare **[!UICONTROL Create Destination]** dopo aver compilato i campi riportati sopra.

![Connetti ai tag del volo](../../assets/catalog/mobile-engagement/airship-tags/select-domain.png)

La destinazione è stata creata. È possibile selezionare **[!UICONTROL Save & Exit]** se si desidera attivare i segmenti in un secondo momento oppure selezionare **[!UICONTROL Next]** per continuare il flusso di lavoro e selezionare i segmenti da attivare. In entrambi i casi, vedere la sezione successiva, [Attivare i segmenti](#activate-segments), per il resto del flusso di lavoro.

## Attivare i segmenti {#activate-segments}

Per attivare i segmenti in [!DNL Airship Tags], segui i passaggi seguenti:

In **[!UICONTROL Destinations > Browse]**, selezionare la destinazione [!DNL Airship Tags] in cui si desidera attivare i segmenti.

![activate-flow](../../assets/catalog/mobile-engagement/airship-tags/browse.png)

Fare clic sul nome della destinazione. Viene quindi visualizzato il flusso Activate (Attiva).

Se esiste già un flusso di attivazione per una destinazione, puoi vedere i segmenti attualmente inviati alla destinazione. Selezionate **[!UICONTROL Edit activation]** nella barra a destra e seguite i passaggi indicati di seguito per modificare i dettagli di attivazione.

![activate-flow](../../assets/catalog/mobile-engagement/airship-tags/activate.png)

Seleziona **[!UICONTROL Activate]**. Nel flusso di lavoro **[!UICONTROL Activate destination]**, nella pagina **[!UICONTROL Select Segments]**, selezionare i segmenti da inviare a [!DNL Airship Tags].

![segmenti-a-destinazione](../../assets/catalog/mobile-engagement/airship-tags/select-segments.png)

Nel passaggio **[!UICONTROL Mapping]**, selezionare gli attributi e le identità dallo schema [XDM](../../../xdm/home.md) da mappare allo schema di destinazione. Selezionare **[!UICONTROL Add new mapping]** per esplorare lo schema e mapparlo sull&#39;identità di destinazione corrispondente.

![schermata iniziale mappatura identità](../../assets/catalog/mobile-engagement/airship-tags/identity-mapping.png)

[!DNL Airship] i tag possono essere impostati su un canale, che rappresenta l&#39;istanza del dispositivo, ad esempio l&#39;iPhone, o un utente con nome, che mappa tutti i dispositivi di un utente con un identificatore comune, ad esempio un ID cliente. Se nello schema sono presenti indirizzi e-mail di testo normale (senza hash) come identità principale, selezionare il campo e-mail in **[!UICONTROL Source Attributes]** e mappare l&#39;utente [!DNL Airship] denominato nella colonna destra sotto **[!UICONTROL Target Identities]**, come mostrato di seguito.

![Mappatura utente con nome](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Per gli identificatori che devono essere mappati su un canale, ad esempio un dispositivo, mappati sul canale appropriato in base all&#39;origine. Le immagini seguenti mostrano come mappare un Google Advertising ID su un canale [!DNL Airship] Android.

![Connessione a ](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![TagsConnetti a ](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![TagsMappatura canale nave aerea](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

Nella pagina **[!UICONTROL Segment schedule]**, la pianificazione è attualmente disattivata. Fare clic su **[!UICONTROL Next]** per continuare con il passaggio di revisione.

Nella pagina **[!UICONTROL Review]** è possibile visualizzare un riepilogo della selezione. Selezionare **[!UICONTROL Cancel]** per interrompere il flusso, **[!UICONTROL Back]** per modificare le impostazioni, oppure **[!UICONTROL Finish]** per confermare la selezione e iniziare a inviare i dati alla destinazione.

>[!IMPORTANT]
>
>In questo passaggio, Adobe Experience Platform verifica la presenza di violazioni dei criteri di utilizzo dei dati. Di seguito è riportato un esempio di violazione di un criterio. Non puoi completare il flusso di lavoro di attivazione del segmento finché non hai risolto la violazione. Per informazioni su come risolvere le violazioni dei criteri, vedere [Applicazione dei criteri](../../../data-governance/enforcement/auto-enforcement.md) nella sezione della documentazione sulla governance dei dati.

![conferma selezione](../../assets/common/data-policy-violation.png)

Se non sono state rilevate violazioni dei criteri, selezionare **[!UICONTROL Finish]** per confermare la selezione e iniziare a inviare i dati alla destinazione.

![conferma selezione](../../assets/catalog/mobile-engagement/airship-tags/review.png)


## Utilizzo e governance dei dati {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedere [Panoramica sulla governance dei dati](../../../data-governance/home.md).

