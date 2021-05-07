---
keywords: targhette di bordo;destinazione di volo
title: Collegamento dei tag dell'aeroporto
description: Trasmetti facilmente i dati di pubblico Adobe a Airship come tag di pubblico per il targeting all’interno di Airship.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 1%

---

# (Beta) [!DNL Airship Tags] connessione {#airship-tags-destination}

>[!IMPORTANT]
>
>La destinazione [!DNL Airship Tags] in Adobe Experience Platform è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

## Panoramica

[!DNL Airship] è la piattaforma leader di Customer Engagement che ti aiuta a fornire messaggi omnicanale significativi e personalizzati ai tuoi utenti in ogni fase del ciclo di vita del cliente.

Questa integrazione trasmette i dati del segmento Adobe Experience Platform in [!DNL Airship] come [Tag](https://docs.airship.com/guides/audience/tags/) per il targeting o l’attivazione.

Per ulteriori informazioni su [!DNL Airship], consulta le [Documenti di navigazione aerea](https://docs.airship.com).


>[!TIP]
>
>Questa pagina della documentazione è stata creata dal team [!DNL Airship]. Per qualsiasi richiesta di informazioni o di aggiornamento, contattali direttamente su [support.airship.com](https://support.airship.com/).

## Prerequisiti

Prima di inviare i segmenti Adobe Experience Platform a [!DNL Airship], devi:

* Crea un gruppo di tag nel progetto [!DNL Airship] .
* Genera un token portatore per l’autenticazione.

>[!TIP]
> 
>Crea un account [!DNL Airship] tramite [questo collegamento di registrazione](https://go.airship.eu/accounts/register/plan/starter/) se non lo hai già fatto.

## Gruppi di tag

Il concetto di segmenti in Adobe Experience Platform è simile a [Tag](https://docs.airship.com/guides/audience/tags/) in Airship, con lievi differenze nell’implementazione. Questa integrazione mappa lo stato dell’ [appartenenza di un utente in un segmento di Experience Platform](../../../xdm/field-groups/profile/segmentation.md) alla presenza o alla non presenza di un tag [!DNL Airship]. Ad esempio, in un segmento di Platform in cui `xdm:status` cambia in `realized`, il tag viene aggiunto al canale [!DNL Airship] o all’utente con nome a cui è mappato questo profilo. Se il tag `xdm:status` diventa `exited`, viene rimosso.

Per abilitare questa integrazione, crea un *gruppo di tag* in [!DNL Airship] denominato `adobe-segments`.

>[!IMPORTANT]
>
>Durante la creazione del nuovo gruppo di tag **Non selezionare** il pulsante di scelta &quot;[!DNL Allow these tags to be set only from your server]&quot;. In questo modo l’integrazione dei tag di Adobe avrà esito negativo.

Per istruzioni sulla creazione del gruppo di tag, consulta [Gestione gruppi di tag](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) .

## Genera token portatore

Vai a **[!UICONTROL Settings]**&quot; **[!UICONTROL APIs & Integrations]** nel [Dashboard di bordo](https://go.airship.com) e seleziona **[!UICONTROL Tokens]** nel menu a sinistra.

Fai clic su **[!UICONTROL Create Token]**.

Specifica un nome descrittivo per il token, ad esempio &quot;Destinazione tag di Adobe&quot;, quindi seleziona &quot;Accesso completo&quot; per il ruolo.

Fai clic su **[!UICONTROL Create Token]** e salva i dettagli come riservati.

## Casi di utilizzo

Per comprendere meglio come e quando utilizzare la destinazione [!DNL Airship Tags], di seguito sono riportati alcuni esempi di casi d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Caso d&#39;uso n. 1

I rivenditori o le piattaforme di intrattenimento possono creare profili utente sui loro clienti fidelizzati e passare tali segmenti in [!DNL Airship] per il targeting dei messaggi sulle campagne mobili.

### Caso d&#39;uso n. 2

Attiva messaggi uno-a-uno in tempo reale quando gli utenti rientrano in o fuori segmenti specifici all’interno di Adobe Experience Platform.

Ad esempio, un rivenditore imposta un segmento specifico del marchio jeans in Platform. Il rivenditore può ora attivare un messaggio mobile non appena qualcuno imposta la propria preferenza jeans su un marchio specifico.

## Connetti a [!DNL Airship Tags] {#connect-airship-tags}

In **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, scorri fino alla categoria **[!UICONTROL Mobile Engagement]** . Selezionare **[!DNL Airship Tags]**, quindi selezionare **[!UICONTROL Configure]**.

>[!NOTE]
>
>Se esiste già una connessione con questa destinazione, è possibile visualizzare un pulsante **[!UICONTROL Activate]** sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consulta la sezione [Catalogo](../../ui/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.

![Connetti ai tag di volo](../../assets/catalog/mobile-engagement/airship-tags/catalog.png)

Nel passaggio **Account**, se in precedenza hai impostato una connessione alla destinazione [!DNL Airship Tags], seleziona **[!UICONTROL Existing Account]** e seleziona la connessione esistente. In alternativa, è possibile selezionare **[!UICONTROL New Account]** per impostare una nuova connessione a [!DNL Airship Tags]. Seleziona **[!UICONTROL Connect to destination]** per collegare Adobe Experience Platform al progetto [!DNL Airship] utilizzando il token portatore generato dal dashboard [!DNL Airship].

>[!NOTE]
>
>Adobe Experience Platform supporta la convalida delle credenziali nel processo di autenticazione e visualizza un messaggio di errore se immetti credenziali errate nel tuo account [!DNL Airship]. In questo modo non completa il flusso di lavoro con credenziali errate.

![Connetti ai tag di volo](../../assets/catalog/mobile-engagement/airship-tags/connect-account.png)

Una volta confermate le credenziali e quando Adobe Experience Platform è connesso al progetto [!DNL Airship], puoi selezionare **[!UICONTROL Next]** per procedere al passaggio **[!UICONTROL Setup]**.

Nel passaggio **[!UICONTROL Authentication]** immetti un **[!UICONTROL Name]** e un **[!UICONTROL Description]** per il flusso di attivazione.

Anche in questo passaggio, è possibile selezionare un centro dati US o EU, a seconda di quale [!DNL Airship] centro dati si applica a questa destinazione. Infine, seleziona uno o più **[!UICONTROL Marketing Actions]** per i quali verranno esportati i dati nella destinazione. Puoi scegliere tra le azioni di marketing definite da Adobe o crearne una tua. Per ulteriori informazioni sulle azioni di marketing, consulta la [Panoramica sui criteri di utilizzo dei dati](../../../data-governance/policies/overview.md).

Seleziona **[!UICONTROL Create Destination]** dopo aver compilato i campi precedenti.

![Connetti ai tag di volo](../../assets/catalog/mobile-engagement/airship-tags/select-domain.png)

La destinazione viene ora creata. Puoi selezionare **[!UICONTROL Save & Exit]** se desideri attivare i segmenti in un secondo momento oppure puoi selezionare **[!UICONTROL Next]** per continuare il flusso di lavoro e selezionare i segmenti da attivare. In entrambi i casi, consulta la sezione successiva [Attivare i segmenti](#activate-segments) per il resto del flusso di lavoro.

## Attiva segmenti {#activate-segments}

Per attivare i segmenti su [!DNL Airship Tags], segui i passaggi seguenti:

In **[!UICONTROL Destinations > Browse]**, seleziona la destinazione [!DNL Airship Tags] in cui desideri attivare i segmenti.

![flusso di attivazione](../../assets/catalog/mobile-engagement/airship-tags/browse.png)

Fare clic sul nome della destinazione. Viene visualizzato il flusso Attiva .

Se esiste già un flusso di attivazione per una destinazione, puoi vedere i segmenti attualmente inviati alla destinazione. Seleziona **[!UICONTROL Edit activation]** nella barra a destra e segui i passaggi riportati di seguito per modificare i dettagli di attivazione.

![flusso di attivazione](../../assets/catalog/mobile-engagement/airship-tags/activate.png)

Seleziona **[!UICONTROL Activate]**. Nel flusso di lavoro **[!UICONTROL Activate destination]**, nella pagina **[!UICONTROL Select Segments]** seleziona i segmenti da inviare a [!DNL Airship Tags].

![da segmenti a destinazione](../../assets/catalog/mobile-engagement/airship-tags/select-segments.png)

Nel passaggio **[!UICONTROL Mapping]** , seleziona gli attributi e le identità dallo schema [XDM](../../../xdm/home.md) da mappare allo schema di destinazione. Seleziona **[!UICONTROL Add new mapping]** per sfogliare lo schema e mapparlo sull&#39;identità di destinazione corrispondente.

![schermata iniziale della mappatura identità](../../assets/catalog/mobile-engagement/airship-tags/identity-mapping.png)

[!DNL Airship] I tag possono essere impostati su un canale, che rappresenta l’istanza del dispositivo, ad esempio l’iPhone, o un utente con nome, che mappa tutti i dispositivi di un utente con un identificatore comune, ad esempio un ID cliente. Se nello schema sono presenti indirizzi e-mail in testo normale (con hash) come identità principale, seleziona il campo e-mail nel **[!UICONTROL Source Attributes]** e mappalo sull’ [!DNL Airship] utente denominato nella colonna di destra sotto **[!UICONTROL Target Identities]**, come mostrato di seguito.

![Mapping utente denominato](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Per gli identificatori che devono essere mappati su un canale, cioè un dispositivo, mappati sul canale appropriato in base all&#39;origine. Le immagini seguenti mostrano come mappare un Google Advertising ID su un canale [!DNL Airship] Android.

![Connetti a ](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![TagsConnetti a ](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![TagsMappatura canale](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

Nella pagina **[!UICONTROL Segment schedule]** la pianificazione è attualmente disabilitata. Fai clic su **[!UICONTROL Next]** per continuare il passaggio di revisione.

Nella pagina **[!UICONTROL Review]** è disponibile un riepilogo della selezione. Seleziona **[!UICONTROL Cancel]** per interrompere il flusso, **[!UICONTROL Back]** per modificare le impostazioni oppure **[!UICONTROL Finish]** per confermare la selezione e iniziare a inviare dati alla destinazione.

>[!IMPORTANT]
>
>In questo passaggio, Adobe Experience Platform verifica la presenza di violazioni dei criteri di utilizzo dei dati. Di seguito è riportato un esempio di violazione di un criterio. Non puoi completare il flusso di lavoro di attivazione dei segmenti finché non avrai risolto la violazione. Per informazioni su come risolvere le violazioni dei criteri, consulta [Applicazione dei criteri](../../../data-governance/enforcement/auto-enforcement.md) nella sezione relativa alla governance dei dati .

![confirm-selection](../../assets/common/data-policy-violation.png)

Se non sono state rilevate violazioni dei criteri, seleziona **[!UICONTROL Finish]** per confermare la selezione e iniziare a inviare dati alla destinazione.

![confirm-selection](../../assets/catalog/mobile-engagement/airship-tags/review.png)


## Utilizzo e governance dei dati {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, consulta [Panoramica sulla governance dei dati](../../../data-governance/home.md).
