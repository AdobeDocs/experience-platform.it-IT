---
keywords: Google ads;google ads;google adwords;Google AdWords;Google Adwords;Google Adwords
title: Google AdsDestination
seo-title: Destinazione annunci Google
description: Google Ads, precedentemente noto come Google AdWords, è un servizio pubblicitario online che consente alle aziende di pagare per clic pubblicità tra ricerche basate su testo, display grafici, video YouTube e display mobili in-app.
seo-description: Google Ads, precedentemente noto come Google AdWords, è un servizio pubblicitario online che consente alle aziende di pagare per clic pubblicità tra ricerche basate su testo, display grafici, video YouTube e display mobili in-app.
translation-type: tm+mt
source-git-commit: bb2fc2658d32c59b476dd9d526eb8bc2f055a1af
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 0%

---


# [!DNL Google Ads] Destinazione

## Panoramica

[!DNL Google Ads], precedentemente noto come  [!DNL Google AdWords], è un servizio pubblicitario online che consente alle aziende di effettuare pubblicità pay-per-click tra ricerche basate su testo, display grafici,  [!DNL YouTube] video e display mobili in-app.

## Specifiche di destinazione

Tenete presenti i seguenti dettagli specifici per le destinazioni [!DNL Google Ads]:

* È possibile inviare le seguenti [identità](../../../identity-service/namespaces.md) alle [!DNL Google Ads] destinazioni: [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en), ID cookie Google, IDFA, GAID, ID Roku, ID Microsoft e ID  Amazon Fire TV.
   * Google utilizzerà [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) per eseguire il targeting degli utenti in California e il Google Cookie ID per tutti gli altri utenti.
* I tipi di pubblico attivati vengono creati a livello di programmazione nella piattaforma [!DNL Google].
* Al momento la piattaforma non include una metrica di misura per convalidare l&#39;attivazione. Per convalidare l&#39;integrazione e comprendere le dimensioni del targeting dell&#39;audience, fare riferimento ai conteggi dell&#39;audience in Google.

>[!IMPORTANT]
>
>Se stai cercando di creare la tua prima destinazione con [!DNL Google Ads] e non hai attivato la [funzionalità di sincronizzazione ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) in  Experience Cloud ID Service in passato (con  Audience Manager o altre applicazioni), contatta  Consulente Adobe o l&#39;Assistenza clienti per abilitare le sincronizzazioni ID. Se in precedenza avevate impostato integrazioni Google in  Audience Manager, le sincronizzazioni ID che avevate configurato per il passaggio alla piattaforma.

### Tipo di esportazione {#export-type}

**Esportazione**  segmento: tutti i membri di un segmento (pubblico) vengono esportati nella destinazione Google.

## Prerequisiti

### Account [!DNL Google Ads] esistente

>[!IMPORTANT]
>
> [!DNL Google] ha dichiarato obsolete le nuove integrazioni di  [!DNL Google Ads] cookie con fornitori di terze parti. Per eseguire i passaggi  elenco consentiti nella sezione successiva, è necessario disporre di un&#39;integrazione esistente con [!DNL Google Ads]. Di conseguenza, l&#39;approccio consigliato per utilizzare [!DNL Google Ads] consiste nell&#39;impostare un&#39;integrazione [!DNL Google Customer Match]. Per ulteriori dettagli sulla creazione di un&#39;integrazione [!DNL Google Customer Match], leggete l&#39;esercitazione sulla creazione di una connessione [[!DNL Google Customer Match]](./google-customer-match.md).

### elenco consentiti 

>[!NOTE]
>
>Il elenco consentiti  è obbligatorio prima di configurare la prima [!DNL Google Ads] destinazione in Platform. Prima di creare una destinazione, verificare che il processo di elenco consentiti  descritto di seguito sia stato completato da [!DNL Google].

Prima di creare la destinazione [!DNL Google Ads] nella piattaforma, è necessario contattare [!DNL Google] per  Adobe nell&#39;elenco dei provider di dati consentiti e per aggiungere l&#39;account al elenco consentiti . Contattare [!DNL Google] e fornire le seguenti informazioni:

* **ID**  account:  ID account  Adobe con  [!DNL Google]. Per ottenere questo ID, contatta &#39;Assistenza clienti di Adobe o il rappresentante del Adobe .
* **ID**  cliente: si tratta  ID account  cliente con  [!DNL Google]. Per ottenere questo ID, contatta &#39;Assistenza clienti di Adobe o il rappresentante del Adobe .
* Tipo di account: **AdWords**
* **ID**  Google AdWords: Questo è il tuo ID con  [!DNL Google]. Il formato ID è in genere 123-456-7890.

## Configura destinazione

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selezionare [!DNL Google Ads], quindi selezionare **[!UICONTROL Configure]**.

![Destinazione di Connect Google Ads](../../assets/catalog/advertising/google-ads-destination/catalog.png)

>[!NOTE]
>
>Se esiste già una connessione con questa destinazione, è possibile visualizzare un pulsante **[!UICONTROL Activate]** sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, fare riferimento alla sezione [Catalog](../../ui/destinations-workspace.md#catalog) della documentazione relativa all&#39;area di lavoro di destinazione.

Nel passaggio **Setup** del flusso di lavoro di creazione della destinazione, compilare il [!UICONTROL Basic Information] per la destinazione.

![Informazioni di base Google Ads](../../assets/catalog/advertising/google-ads-destination/setup.png)

* **[!UICONTROL Name]**: Compila il nome preferito per questa destinazione.
* **[!UICONTROL Description]**: Facoltativo. Ad esempio, potete specificare per quale campagna state utilizzando questa destinazione.
* **[!UICONTROL Account Type]**: AdWords è l&#39;unica opzione disponibile.
* **[!UICONTROL Account ID]**: Compila il tuo ID account con  [!DNL Google Ads]. Il formato ID è in genere 123-456-7890.
* **[!UICONTROL Marketing use case]**: I casi di utilizzo del marketing indicano l&#39;intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra  casi di utilizzo di marketing definiti dal Adobe o creare un caso di utilizzo di marketing personale. Per ulteriori informazioni sui casi di utilizzo del marketing, vedere la [panoramica dei criteri di utilizzo dei dati](../../../data-governance/policies/overview.md).

## Attivare i segmenti in [!DNL Google Ads]

Per istruzioni su come attivare i segmenti in [!DNL Google Ads], vedere [Attivare i dati sulle destinazioni](../../ui/activate-destinations.md).

## Dati esportati

Per verificare se i dati sono stati esportati correttamente nella destinazione [!DNL Google Ads], controlla il tuo account [!DNL Google Ads]. Se l&#39;attivazione ha avuto esito positivo, l&#39;audience viene popolata nel vostro account.