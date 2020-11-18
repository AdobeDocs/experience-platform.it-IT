---
keywords: airship tags;airship destination
title: Destinazione tag di volo
seo-title: Destinazione dei tag di volo
description: Trasmettete senza problemi  dati Adobi di pubblico a Airship come tag di pubblico per il targeting all'interno di Airship.
seo-description: Trasmettete senza problemi  dati Adobi di pubblico a Airship come tag di pubblico per il targeting all'interno di Airship.
translation-type: tm+mt
source-git-commit: 4b1bf5bbce57a22529c5d025c5bae10557400d54
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 1%

---


# (Beta) [!DNL Airship Tags] destinazione {#airship-tags-destination}

>[!IMPORTANT]
>
>La [!DNL Airship Tags] destinazione in Adobe Experience Platform è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

## Panoramica

[!DNL Airship] è la principale piattaforma di coinvolgimento dei clienti, che ti consente di distribuire messaggi omnicanale significativi e personalizzati agli utenti in ogni fase del ciclo di vita del cliente.

Questa integrazione trasmette i dati del segmento Adobe Experience Platform [!DNL Airship] come [tag](https://docs.airship.com/guides/audience/tags/) per il targeting o l&#39;attivazione.

Per ulteriori informazioni [!DNL Airship], vedere i [Documenti](https://docs.airship.com)di volo.


>[!TIP]
>
>Questa pagina della documentazione è stata creata dal [!DNL Airship] team. Per qualsiasi richiesta di informazioni o di aggiornamento, contattateli direttamente su [support.airship.com](https://support.airship.com/).

## Prerequisiti  

Prima di inviare i segmenti Adobe Experience Platform a [!DNL Airship], devi:

* Create un gruppo di tag nel [!DNL Airship] progetto.
* Generare un token al portatore per l&#39;autenticazione.

>[!TIP]
> 
>Se non avete ancora creato un [!DNL Airship] account tramite [questo collegamento](https://go.airship.eu/accounts/register/plan/starter/) di registrazione.

### Gruppi di tag

Il concetto di segmenti in Adobe Experience Platform è simile ai [tag](https://docs.airship.com/guides/audience/tags/) in Airship, con lievi differenze nell&#39;implementazione. Questa integrazione mappa lo stato dell&#39; [appartenenza di un utente in un segmento](https://experienceleague.adobe.com/docs/experience-platform/xdm/mixins/profile/segmentation.html?lang=en#mixins) di Experience Platform  alla presenza o alla non presenza di un [!DNL Airship] tag. Ad esempio, in un segmento della piattaforma in cui `xdm:status` si modifica, il tag viene aggiunto al `realized`[!DNL Airship] canale o all&#39;utente con nome a cui questo profilo viene mappato. Se il tag `xdm:status` cambia in `exited`, viene rimosso.

Per abilitare questa integrazione, create un gruppo *di* tag in [!DNL Airship] denominato `adobe-segments`.

>[!IMPORTANT]
>
>Quando create un nuovo gruppo di tag **Non selezionate** il pulsante di scelta che riporta &quot;[!DNL Allow these tags to be set only from your server]&quot;. In questo modo l&#39;integrazione dei tag di Adobe  non riuscirà.

Consultate [Gestire i gruppi](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) di tag per istruzioni sulla creazione del gruppo di tag.

### Token portatore

1. Vai a **[!UICONTROL Settings]** &quot; **[!UICONTROL APIs & Integrations]** nel [Pannello](https://go.airship.com) di controllo **[!UICONTROL Tokens]** e selezionanel menu a sinistra.
1. Fai clic su **[!UICONTROL Create Token]**.
1. Immettete un nome di facile utilizzo per il token, ad esempio &quot;Destinazione tag di Adobe &quot;, quindi selezionate &quot;Accesso completo&quot; per il ruolo.
1. Fai clic su **[!UICONTROL Create Token]** e salva i dettagli come confidenziali.


## Casi di utilizzo

Per comprendere meglio come e quando utilizzare la [!DNL Airship Tags] destinazione, ecco alcuni esempi di casi di utilizzo che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Caso di utilizzo n. 1

I retailer o le piattaforme di intrattenimento possono creare profili utente sui clienti fedeli e trasmettere tali segmenti [!DNL Airship] per il targeting dei messaggi sulle campagne mobili.

### Caso di utilizzo n. 2

Attiva messaggi uno-a-uno in tempo reale quando gli utenti entrano o escono da segmenti specifici in Adobe Experience Platform.

Ad esempio, un rivenditore imposta un segmento specifico del marchio jeans in Platform. Il rivenditore può ora attivare un messaggio mobile non appena qualcuno imposta la propria preferenza jeans su un marchio specifico.

## Connetti a [!DNL Airship Tags] {#connect-airship-tags}

1. In **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, scorrete fino alla **[!UICONTROL Mobile Engagement]** categoria. Selezionate **[!DNL Airship Tags]**, quindi **[!UICONTROL Configure]**.

   >[!NOTE]
   >
   >Se esiste già una connessione con questa destinazione, è possibile visualizzare un **[!UICONTROL Activate]** pulsante sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consultate la sezione [Catalogo](/help/rtcdp/destinations/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.

   ![Connetti ai tag del volo](/help/rtcdp/destinations/assets/airship-tags-in-catalog.png)

2. Nel passaggio **Account** , se in precedenza avete impostato una connessione alla [!DNL Airship Tags] destinazione, selezionate **[!UICONTROL Existing Account]** e selezionate la connessione esistente. In alternativa, potete selezionare **[!UICONTROL New Account]** di impostare una nuova connessione a [!DNL Airship Tags]. Selezionate **[!UICONTROL Connect to destination]** per collegare Adobe Experience Platform al [!DNL Airship] progetto utilizzando il token del portatore generato dal [!DNL Airship] dashboard.

   >[!NOTE]
   >
   >Adobe Experience Platform supporta la convalida delle credenziali nel processo di autenticazione e visualizza un messaggio di errore se vengono immesse credenziali non corrette nel [!DNL Airship] proprio account. In questo modo si evita di completare il flusso di lavoro con credenziali non corrette.

   ![Connetti ai tag del volo](/help/rtcdp/destinations/assets/airshiptags1-connect-account.png)

3. Una volta confermate le credenziali e che Adobe Experience Platform è connesso al [!DNL Airship] progetto, potete scegliere **[!UICONTROL Next]** di procedere al **[!UICONTROL Setup]** passaggio.

4. Nel **[!UICONTROL Authentication]** passaggio, immettete un **[!UICONTROL Name]** e un **[!UICONTROL Description]** per il flusso di attivazione. <br> Inoltre, in questo passaggio è possibile selezionare un centro dati USA o UE, a seconda del centro [!DNL Airship] dati applicato a questa destinazione. Infine, selezionare uno o più casi di utilizzo del marketing per i quali i dati verranno esportati nella destinazione. Puoi scegliere tra  casi di utilizzo di marketing definiti dal Adobe o creare un tuo. Per ulteriori informazioni sui casi di utilizzo del marketing, consulta la pagina [Governance dei dati in CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) in tempo reale. Per informazioni sui singoli casi di utilizzo marketing definiti dal Adobe , consulta la panoramica [sui criteri di utilizzo dei](/help/data-governance/policies/overview.md#core-actions)dati. <br> Selezionate **[!UICONTROL Create Destination]** dopo aver compilato i campi riportati sopra.

   ![Connetti ai tag del volo](/help/rtcdp/destinations/assets/airshiptags2-select-domain.png)

5. La destinazione è stata creata. Puoi scegliere **[!UICONTROL Save & Exit]** se attivare i segmenti in un secondo momento oppure puoi selezionare **[!UICONTROL Next]** per continuare il flusso di lavoro e selezionare i segmenti da attivare. In entrambi i casi, consulta la sezione successiva, [Attivare i segmenti](#activate-segments), per il resto del flusso di lavoro.

## Attivare i segmenti {#activate-segments}

Per attivare i segmenti in [!DNL Airship Tags], attenetevi alla procedura seguente:

1. In **[!UICONTROL Destinations > Browse]**, seleziona la [!DNL Airship Tags] destinazione in cui vuoi attivare i segmenti. ![activate-flow](/help/rtcdp/destinations/assets/airship-tags-activate1.png)
2. Fare clic sul nome della destinazione. Viene quindi visualizzato il flusso Activate (Attiva).
Se esiste già un flusso di attivazione per una destinazione, puoi vedere i segmenti attualmente inviati alla destinazione. Selezionate **[!UICONTROL Edit activation]** nella barra a destra e seguite i passaggi descritti di seguito per modificare i dettagli di attivazione.  ![activate-flow](/help/rtcdp/destinations/assets/airship-tags-activate2.png)
3. Seleziona **[!UICONTROL Activate]**;
4. Nel **[!UICONTROL Activate destination]** flusso di lavoro, nella **[!UICONTROL Select Segments]** pagina, seleziona i segmenti a cui inviare [!DNL Airship Tags].
   ![segmenti-a-destinazione](/help/rtcdp/destinations/assets/airshiptags3-select-segments.png)
5. Nel **[!UICONTROL Mapping]** passaggio, selezionare gli attributi e le identità dallo schema [XDM](https://docs.adobe.com/content/help/it-IT/experience-platform/xdm/home.html) da associare allo schema di destinazione. Selezionare **[!UICONTROL Add new mapping]** per esplorare lo schema e mapparlo sull&#39;identità di destinazione corrispondente.
   ![schermata iniziale mappatura identità](/help/rtcdp/destinations/assets/gcm-identity-mapping.png)
   [!DNL Airship] i tag possono essere impostati su un canale, che rappresenta l&#39;istanza del dispositivo, ad esempio l&#39;iPhone, o un utente con nome, che mappa tutti i dispositivi di un utente con un identificatore comune, ad esempio un ID cliente. Se nello schema sono presenti indirizzi e-mail di testo normale (senza hash) come identità principale, selezionare il campo e-mail **[!UICONTROL Source Attributes]** e mappare l&#39;utente [!DNL Airship] denominato nella colonna destra sotto **[!UICONTROL Target Identities]**, come mostrato di seguito.
   ![Mapping](/help/rtcdp/destinations/assets/airshiptags7-mappingoption2.png)utente denominato Per gli identificatori che devono essere mappati su un canale, ad esempio un dispositivo, vengono mappati sul canale appropriato in base all&#39;origine. Le immagini seguenti mostrano come mappare un Google Advertising ID su un canale [!DNL Airship] Android.
   ![Connetti ai tag del volo](/help/rtcdp/destinations/assets/airshiptags4-select-source-identity.png)
   ![Connetti ai tag del volo](/help/rtcdp/destinations/assets/airshiptags5-select-target-identity.png)
   ![Mappatura canale](/help/rtcdp/destinations/assets/airshiptags6-mappingoption1.png)

6. Sulla **[!UICONTROL Segment schedule]** pagina, la pianificazione è attualmente disattivata. Fare clic **[!UICONTROL Next]** per continuare il passaggio di revisione.
7. Nella **[!UICONTROL Review]** pagina viene visualizzato un riepilogo della selezione. Selezionare **[!UICONTROL Cancel]** per interrompere il flusso, **[!UICONTROL Back]** modificare le impostazioni o **[!UICONTROL Finish]** per confermare la selezione e iniziare a inviare i dati alla destinazione.

>[!IMPORTANT]
>
>In questo passaggio, Adobe Experience Platform verifica la presenza di violazioni dei criteri di utilizzo dei dati. Di seguito è riportato un esempio di violazione di un criterio. Non puoi completare il flusso di lavoro di attivazione del segmento finché non hai risolto la violazione. Per informazioni su come risolvere le violazioni dei criteri, consulta [Applicazione](/help/rtcdp/privacy/data-governance-overview.md#enforcement) dei criteri nella sezione relativa alla governance dei dati.

![conferma selezione](/help/rtcdp/destinations/assets/data-policy-violation.png)

Se non sono state rilevate violazioni dei criteri, selezionate **[!UICONTROL Finish]** per confermare la selezione e iniziare a inviare i dati alla destinazione.

![conferma selezione](/help/rtcdp/destinations/assets/Airship-tags-review.png)


## Utilizzo e governance dei dati {#data-usage-governance}

Tutte [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applicare la governance dei dati, vedi [Governance dei dati in CDP](/help/rtcdp/privacy/data-governance-overview.md)in tempo reale.

