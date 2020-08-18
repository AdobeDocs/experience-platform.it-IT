---
title: Destinazione di corrispondenza cliente Google
seo-title: Destinazione di corrispondenza cliente Google
description: Google Customer Match consente di utilizzare i dati online e offline per raggiungere e coinvolgere nuovamente i clienti nelle proprietà di Google possedute e gestite, come ad esempio Cerca, Shopping, Gmail e YouTube.
seo-description: Google Customer Match consente di utilizzare i dati online e offline per raggiungere e coinvolgere nuovamente i clienti nelle proprietà di Google possedute e gestite, come ad esempio Cerca, Shopping, Gmail e YouTube.
translation-type: tm+mt
source-git-commit: a251d843401d2f092e368a4cdac217171fa4687f
workflow-type: tm+mt
source-wordcount: '1490'
ht-degree: 0%

---


# Destinazione di corrispondenza cliente Google

## Panoramica {#overview}

[Google Customer Match](https://support.google.com/google-ads/answer/6379332?hl=en) consente di utilizzare i dati online e offline per raggiungere e coinvolgere nuovamente i clienti nelle proprietà di Google possedute e gestite, ad esempio: [!DNL Search], [!DNL Shopping], [!DNL Gmail], e [!DNL YouTube].

![Destinazione di corrispondenza cliente Google nell’interfaccia utente CDP in tempo reale](/help/rtcdp/destinations/assets/google-customer-match-catalog.png)

## Casi d’uso

Per comprendere meglio come e quando utilizzare la [!DNL Google Customer Match] destinazione, ecco alcuni esempi di casi di utilizzo che  clienti della piattaforma dati cliente in tempo reale del Adobe possono risolvere utilizzando questa funzione.


### Caso di utilizzo n. 1

Un marchio di abbigliamento atletico vuole raggiungere i clienti esistenti attraverso [!DNL Google Search] e [!DNL Google Shopping] personalizzare le offerte e gli articoli in base ai loro acquisti passati e la cronologia di navigazione. Il marchio dell&#39;abbigliamento può acquisire indirizzi e-mail da CRM a  CDP in tempo reale Adobe, creare segmenti dai propri dati offline e inviare questi segmenti [!DNL Google Customer Match] da utilizzare in tutto [!DNL Search] e [!DNL Shopping], ottimizzando le spese pubblicitarie.

### Caso di utilizzo n. 2

Un&#39;importante azienda tecnologica ha appena lanciato un nuovo telefono. Nel tentativo di promuovere questo nuovo modello di telefono, stanno cercando di sensibilizzare i clienti sulle nuove funzionalità e caratteristiche del telefono ai clienti che possiedono modelli precedenti dei loro telefoni.

Per promuovere il rilascio, caricano gli indirizzi e-mail dal proprio database CRM nel CDP in tempo reale  Adobe, utilizzando gli indirizzi e-mail come identificatori. I segmenti vengono creati in base ai clienti che possiedono modelli di telefono meno recenti e li inviano a clienti [!DNL Google Customer Match] che possono essere indirizzati a clienti correnti, clienti che possiedono modelli di telefono più vecchi, nonché a clienti simili su [!DNL YouTube].

## Gestione dei dati per [!DNL Google Customer Match] le destinazioni {#data-governance}

Le destinazioni nel  Adobe CDP in tempo reale possono avere determinate regole e obblighi per i dati inviati o ricevuti dalla piattaforma di destinazione. L&#39;Utente è tenuto a comprendere i limiti e gli obblighi dei propri dati e come li utilizza in Adobe Experience Platform e nella piattaforma di destinazione. Adobe Experience Platform offre strumenti per la gestione dei dati che consentono di gestire alcuni di questi obblighi di utilizzo dei dati. [Ulteriori](/help/data-governance/labels/overview.md) informazioni sugli strumenti e sulle politiche per la gestione dei dati.

## Tipo di attivazione e identità {#activation-type}

**Esportazione** segmento - vengono esportati tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono, ecc.) utilizzato nella [!DNL Google Customer Match] destinazione.

**Identità** : puoi utilizzare e-mail non elaborate o con hash come ID cliente in Google

## [!DNL Google Customer Match] prerequisiti account {#google-account-prerequisites}

Prima di impostare una [!DNL Google Customer Match] destinazione in  CDP in tempo reale del Adobe, accertatevi di leggere e aderire ai criteri di Google per l&#39;utilizzo [!DNL Customer Match], descritti nella documentazione [di supporto di](https://support.google.com/google-ads/answer/6299717)Google.

### elenco consentiti  {#allowlist}

>[!NOTE]
>
>È obbligatorio essere aggiunti al elenco consentiti  Google prima di configurare la prima [!DNL Google Customer Match] destinazione  Adobe CDP in tempo reale. Prima di creare una destinazione, verificare che il processo di elenco consentiti  descritto di seguito sia stato completato da Google.

Prima di creare la [!DNL Google Customer Match] destinazione in CDP in tempo reale  Adobe, è necessario contattare Google e seguire le istruzioni  elenco consentiti in [Usa partner di corrispondenza cliente per caricare i dati](https://support.google.com/google-ads/answer/7361372?hl=en&amp;ref_topic=6296507) nella documentazione di Google.


### Requisiti di hashing e-mail {#hashing-requirements}

<!--

>[!IMPORTANT]
>
> When using mobile device IDs as identifiers, an AppId must be provided in the activation flow. For more information, see step 6 in the [Activate segments](#activate-segments) section of this page.

-->

Google richiede che non vengano inviate informazioni personali (PII). Di conseguenza, i tipi di pubblico a cui si [!DNL Google Customer Match] è attivato devono essere cancellati dagli indirizzi e-mail *con hash* . Potete scegliere di hash gli indirizzi e-mail prima di inviarli in Adobe Experience Platform, oppure potete scegliere di lavorare con gli indirizzi e-mail in  Experience Platform e ottenere l&#39;hash del nostro algoritmo al momento dell&#39;attivazione.

Per ulteriori informazioni sui requisiti di hashing di Google e altre restrizioni all&#39;attivazione, consulta le sezioni seguenti nella documentazione di Google:

* [[!DNL Customer Match] con indirizzo e-mail, indirizzo o ID utente](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] considerazioni](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)

<!--

Links to be added when activation based on phone number and device IDs becomes available.

* [Customer Match with phone number](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [Customer Match with mobile device IDs](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)

-->

Per informazioni sull’assimilazione degli indirizzi e-mail in  Experience Platform, consultate la panoramica [sull’assimilazione](/help/ingestion/batch-ingestion/overview.md) batch e la panoramica [sull’assimilazione](/help/ingestion/streaming-ingestion/overview.md)accattivante.

Se selezionate di hash gli indirizzi e-mail, accertatevi di soddisfare i requisiti di Google, descritti nei collegamenti sopra.


>[!IMPORTANT]
>
>Se si sceglie di non utilizzare l&#39;hash degli indirizzi e-mail,  CDP in tempo reale Adobe lo farà automaticamente quando si attivano i segmenti in [!DNL Google Customer Match]. Nel flusso di lavoro [di](/help/rtcdp/destinations/google-customer-match-destination.md#activate-segments) attivazione (vedere il punto 5), selezionate l’ `Email` opzione come illustrato di seguito per gli indirizzi *e-mail di testo* normale e `Email_LC_SHA256` per gli indirizzi e-mail con *hash*.


![Hashing all&#39;attivazione](/help/rtcdp/destinations/assets/identity-mapping.png)

## Connetti alla destinazione {#connect-destination}

1. In **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, scorrete fino alla **[!UICONTROL Advertising]** categoria. Selezionate [!DNL Google Customer Match], quindi **[!UICONTROL Configure]**.

   ![Connessione alla destinazione di corrispondenza cliente Google](/help/rtcdp/destinations/assets/connect-google-customer-match.png)

   >[!NOTE]
   >
   >Se esiste già una connessione con questa destinazione, è possibile visualizzare un **[!UICONTROL Activate]** pulsante sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consultate la sezione [Catalogo](/help/rtcdp/destinations/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.

2. Nel passaggio **Account** , se in precedenza avete impostato una connessione alla [!DNL Google Customer Match] destinazione, selezionate **[!UICONTROL Existing Account]** e selezionate la connessione esistente. In alternativa, potete selezionare **[!UICONTROL New Account]** di impostare una nuova connessione a [!DNL Google Customer Match]. Selezionate **[!UICONTROL Connect to destination]** per accedere e collegare Adobe Experience Cloud al vostro [!DNL Google Ad] account.

   >[!NOTE]
   >
   > Adobe CDP in tempo reale supporta la convalida delle credenziali nel processo di autenticazione e visualizza un messaggio di errore se nel tuo [!DNL Google Ad] account vengono immesse credenziali non corrette. In questo modo si evita di completare il flusso di lavoro con credenziali non corrette.

   ![Connessione alla destinazione di corrispondenza cliente Google - passaggio di autenticazione](/help/rtcdp/destinations/assets/google-customer-match-pre-connect-view.png)

3. Una volta confermate le credenziali e che Adobe Experience Cloud è connesso al tuo account Google, puoi scegliere **[!UICONTROL Next]** di procedere con il **[!UICONTROL Setup]** passaggio.

   ![Credenziali confermate](/help/rtcdp/destinations/assets/google-customer-match-connection-success.png)

4. Nel **[!UICONTROL Authentication]** passaggio, immettete un **[!UICONTROL Name]** e un **[!UICONTROL Description]** per il flusso di attivazione e riempite Google **[!UICONTROL Account ID]**. <br> Inoltre, in questo passaggio potete selezionare tutte le opzioni **[!UICONTROL Marketing use case]** che devono essere applicate a questa destinazione. I casi di utilizzo del marketing indicano l&#39;intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra  casi di utilizzo di marketing definiti dal Adobe o creare un caso di utilizzo di marketing personale. Per ulteriori informazioni sui casi di utilizzo del marketing, consulta la pagina [Governance dei dati in CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) in tempo reale. Per informazioni sui singoli casi di utilizzo marketing definiti dal Adobe , consulta la panoramica [sui criteri di utilizzo dei](/help/data-governance/policies/overview.md#core-actions)dati. <br> Selezionate **[!UICONTROL Create Destination]** dopo aver compilato i campi riportati sopra.

   >[!IMPORTANT]
   >
   > * Il caso di utilizzo **[!UICONTROL Combine with PII]** marketing è selezionato per impostazione predefinita per la [!DNL Google Customer Match] destinazione e non può essere rimosso.
   > * Per [!DNL Google Customer Match] le destinazioni. **[!UICONTROL Account ID]** è l&#39;ID cliente con Google. Il formato dell&#39;ID è xxx-xxx-xxxx.


   ![Corrispondenza cliente Google Connect - passaggio di autenticazione](/help/rtcdp/destinations/assets/google-customer-match-authentication-step.png)

5. La destinazione è stata creata. Puoi scegliere **[!UICONTROL Save & Exit]** se attivare i segmenti in un secondo momento oppure puoi selezionare **[!UICONTROL Next]** per continuare il flusso di lavoro e selezionare i segmenti da attivare. In entrambi i casi, consulta la sezione successiva, [Attivare [!DNL Google Customer Match]](#activate-segments)i segmenti per il resto del flusso di lavoro.


## Attiva i segmenti in [!DNL Google Customer Match] {#activate-segments}

Per attivare i segmenti in [!DNL Google Customer Match], attenetevi alla procedura seguente:

1. In **[!UICONTROL Destinations > Browse]**, seleziona la [!DNL Google Customer Match] destinazione in cui vuoi attivare i segmenti.
2. Fare clic sul nome della destinazione. Viene quindi visualizzato il flusso Activate (Attiva).
   ![activate-flow](/help/rtcdp/destinations/assets/google-customer-match-activate-flow.png)Si noti che se esiste già un flusso di attivazione per una destinazione, è possibile visualizzare i segmenti attualmente inviati alla destinazione. Selezionate **[!UICONTROL Edit activation]** nella barra a destra e seguite i passaggi descritti di seguito per modificare i dettagli di attivazione.
3. Seleziona **[!UICONTROL Activate]**;
4. Nel **[!UICONTROL Activate destination]** flusso di lavoro, nella **[!UICONTROL Select Segments]** pagina, seleziona i segmenti a cui inviare [!DNL Google Customer Match].
   ![segmenti-a-destinazione](/help/rtcdp/destinations/assets/activate-segments-google-customer-match.png)
5. Nel **[!UICONTROL Identity mapping]** passaggio, selezionate gli attributi da includere come identità in questa destinazione. Selezionate **[!UICONTROL Add new mapping]** e sfogliate lo schema, selezionate e-mail e/o indirizzi e-mail con hash, quindi mapparli sull&#39;identità di destinazione corrispondente
   ![schermata iniziale mappatura identità](/help/rtcdp/destinations/assets/gcm-identity-mapping.png) <br> 
   *Indirizzo e-mail in testo semplice come identità* principale: Se nello schema sono presenti indirizzi e-mail di testo normale (senza hash) come identità principale, selezionate il campo e-mail **[!UICONTROL Source Attributes]** e mappatelo sul campo E-mail nella colonna di destra sotto **[!UICONTROL Target Identities]**, come illustrato di seguito:
   ![seleziona identità e-mail in testo normale](/help/rtcdp/destinations/assets/gcm-raw-email.gif) <br> 
   *Indirizzo e-mail con hash come identità* principale: Se nello schema sono presenti indirizzi e-mail con hash come identità principale, selezionare il campo e-mail con hash **[!UICONTROL Source Attributes]** e mapparlo sul campo Email_LC_SHA256 nella colonna di destra sotto **[!UICONTROL Target Identities]**, come illustrato di seguito:
   ![seleziona identità e-mail con hash](/help/rtcdp/destinations/assets/gcm-hashed-emails.gif) <br> 
6. Sulla **[!UICONTROL Segment schedule]** pagina è possibile impostare la data di inizio per l&#39;invio dei dati alla destinazione.
7. Nella **[!UICONTROL Review]** pagina viene visualizzato un riepilogo della selezione. Selezionare **[!UICONTROL Cancel]** per interrompere il flusso, **[!UICONTROL Back]** modificare le impostazioni o **[!UICONTROL Finish]** per confermare la selezione e iniziare a inviare i dati alla destinazione.

>[!IMPORTANT]
>
>In questo passaggio, la funzione CDP in tempo reale verifica la presenza di violazioni dei criteri di utilizzo dei dati. Di seguito è riportato un esempio di violazione di un criterio. Non puoi completare il flusso di lavoro di attivazione del segmento finché non hai risolto la violazione. Per informazioni su come risolvere le violazioni dei criteri, consulta [Applicazione](/help/rtcdp/privacy/data-governance-overview.md#enforcement) dei criteri nella sezione relativa alla governance dei dati.

![conferma selezione](/help/rtcdp/destinations/assets/data-policy-violation.png)

Se non sono state rilevate violazioni dei criteri, selezionate **[!UICONTROL Finish]** per confermare la selezione e iniziare a inviare i dati alla destinazione.

![conferma selezione](/help/rtcdp/destinations/assets/gcm-review.png)


<!--

Insert in Step 6 when mobile device ID activation is available

    >[!IMPORTANT]
    >
    >If you select mobile device IDs (GAID or IDFA) as primary identity in the Identity mapping step, you must also provide an Application Id in this step. If you selected GAID as identity, see [Set the Application ID](https://developer.android.com/studio/build/application-id) in the Android developer documentation. IF you selected IDFA as identity, see [App ID](https://developer.android.com/studio/build/application-id) in the Apple developer documentation.

    ![segment schedule page](/help/rtcdp/destinations/assets/gcm-segment-schedule.png) 

-->

## Verificare che l&#39;attivazione del segmento sia stata eseguita correttamente {#verify-activation}

Dopo aver completato il flusso di attivazione, passate al vostro **[!UICONTROL Google Ads]** account. I segmenti attivati verranno ora visualizzati nel tuo account Google come elenchi di clienti. A seconda delle dimensioni del segmento, alcuni tipi di pubblico non verranno popolati a meno che non ci siano più di 100 utenti attivi da distribuire.

## Risorse aggiuntive {#additional-resources}

* [Integrare Google Customer Match - Esercitazione video](https://docs.adobe.com/content/help/en/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)