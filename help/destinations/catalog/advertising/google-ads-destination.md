---
keywords: annunci Google;annunci google;parole adwords Google;Google AdWords;Google Adwords
title: Connessione Google Ads
description: Google Ads, precedentemente noto come Google AdWords, è un servizio di pubblicità online che consente alle aziende di effettuare pubblicità a pagamento per clic tra ricerche basate su testo, visualizzazioni grafiche, video YouTube e display mobili in-app.
translation-type: tm+mt
source-git-commit: 0759919dc458798ca4bc5f233a9cb319194ea534
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 0%

---


# [!DNL Google Ads] connection

[!DNL Google Ads], precedentemente noto come  [!DNL Google AdWords], è un servizio pubblicitario online che consente alle aziende di effettuare pubblicità a pagamento per clic tra ricerche basate su testo, visualizzazioni grafiche,  [!DNL YouTube] video e display mobili in-app.

## Specifiche di destinazione

Tieni presente i seguenti dettagli specifici delle destinazioni [!DNL Google Ads]:

* I tipi di pubblico attivati vengono creati a livello di programmazione nella piattaforma [!DNL Google] .
* Al momento, Platform non include una metrica di misurazione per convalidare l’attivazione. Consulta i conteggi del pubblico in Google per convalidare l’integrazione e comprendere le dimensioni del targeting del pubblico.

>[!IMPORTANT]
>
>Se stai cercando di creare la tua prima destinazione con [!DNL Google Ads] e non hai abilitato in passato la [funzionalità di sincronizzazione ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) nel servizio ID di Experience Cloud (con Audience Manager o altre applicazioni), contatta la Consulenza di Adobe o l’Assistenza clienti per abilitare le sincronizzazioni degli ID. Se in precedenza hai configurato le integrazioni Google in Audience Manager, le sincronizzazioni ID che avevi configurato per il passaggio a Platform.

### Identità supportate {#supported-identities}

[!DNL Google Ad Manager] supporta l’attivazione delle identità descritte nella tabella seguente.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi IDFA. |
| UUID AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), noto anche come  [!DNL Device ID]. Un ID dispositivo numerico a 38 cifre associato a ciascun dispositivo con cui interagisce. | Google utilizza [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) per eseguire il targeting degli utenti in California e l&#39;ID cookie di Google per tutti gli altri utenti. |
| [!DNL Google] ID cookie | [!DNL Google] ID cookie | [!DNL Google] utilizza questo ID per eseguire il targeting degli utenti al di fuori della California. |
| RIDA | ID Roku per la pubblicità. Questo ID identifica in modo univoco i dispositivi Roku. |  |
| MAID | ID pubblicità Microsoft. Questo ID identifica in modo univoco i dispositivi con Windows 10. |  |
| Amazon Fire TV ID | Questo ID identifica in modo univoco i Amazon Fire TV. |  |

### Tipo di esportazione {#export-type}

**Esportazione segmento** : stai esportando tutti i membri di un segmento (pubblico) nella destinazione Google.

## Prerequisiti

### Account [!DNL Google Ads] esistente

>[!IMPORTANT]
>
> [!DNL Google] ha dichiarato obsolete le nuove integrazioni di  [!DNL Google Ads] cookie con fornitori di terze parti. Per eseguire i passaggi dell’elenco consentiti nella sezione successiva, è necessario disporre di un’integrazione esistente con [!DNL Google Ads]. Di conseguenza, l&#39;approccio consigliato per l&#39;utilizzo di [!DNL Google Ads] consiste nell&#39;impostare un&#39;integrazione [!DNL Google Customer Match]. Per ulteriori informazioni sulla creazione di un&#39;integrazione [!DNL Google Customer Match], leggi l&#39;esercitazione sulla creazione di una connessione [[!DNL Google Customer Match]](./google-customer-match.md).

### Elenco consentiti

>[!NOTE]
>
>L’elenco consentiti è obbligatorio prima di configurare la tua prima destinazione [!DNL Google Ads] in Platform. Prima di creare una destinazione, assicurati che il processo di elenco consentiti descritto di seguito sia stato completato da [!DNL Google].

Prima di creare la destinazione [!DNL Google Ads] in Platform, è necessario contattare [!DNL Google] per Adobe per essere inserito nell’elenco dei provider di dati consentiti e per aggiungere l’account all’elenco consentiti. Contatta [!DNL Google] e fornisci le seguenti informazioni:

* **ID**  account: questo è l&#39;ID account di Adobe con  [!DNL Google]. Per ottenere questo ID, contatta l’Assistenza clienti Adobe o il tuo rappresentante Adobe.
* **ID**  cliente: questo è l&#39;ID account cliente Adobe con  [!DNL Google]. Per ottenere questo ID, contatta l’Assistenza clienti Adobe o il tuo rappresentante Adobe.
* Tipo di account: **AdWords**
* **ID**  di Google AdWords: Questo è il tuo ID con  [!DNL Google]. Il formato ID è tipicamente 123-456-7890.

## Configurare la destinazione

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selezionare [!DNL Google Ads] e selezionare **[!UICONTROL Configure]**.

![Connetti destinazione Google Ads](../../assets/catalog/advertising/google-ads-destination/catalog.png)

>[!NOTE]
>
>Se esiste già una connessione con questa destinazione, è possibile visualizzare un pulsante **[!UICONTROL Activate]** sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consulta la sezione [Catalogo](../../ui/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.

Nel passaggio **Configurazione** del flusso di lavoro di creazione della destinazione, compila il [!UICONTROL Basic Information] per la destinazione.

![Informazioni di base Google Ads](../../assets/catalog/advertising/google-ads-destination/setup.png)

* **[!UICONTROL Name]**: Compila il nome preferito per questa destinazione.
* **[!UICONTROL Description]**: Facoltativo. Ad esempio, è possibile indicare per quale campagna si utilizza questa destinazione.
* **[!UICONTROL Account Type]**: AdWords è l’unica opzione disponibile.
* **[!UICONTROL Account ID]**: Compila il tuo ID account con  [!DNL Google Ads]. Il formato ID è tipicamente 123-456-7890.
* **[!UICONTROL Marketing action]**: Le azioni di marketing indicano l’intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra azioni di marketing definite da Adobi o creare una tua azione di marketing. Per ulteriori informazioni sulle azioni di marketing, consulta la [Panoramica sui criteri di utilizzo dei dati](../../../data-governance/policies/overview.md).

## Attiva i segmenti in [!DNL Google Ads]

Per istruzioni su come attivare i segmenti su [!DNL Google Ads], consulta [Attivare i dati sulle destinazioni](../../ui/activate-destinations.md).

## Dati esportati

Per verificare se i dati sono stati esportati correttamente nella destinazione [!DNL Google Ads], controlla il tuo account [!DNL Google Ads]. Se l&#39;attivazione ha avuto successo, i tipi di pubblico vengono compilati nel tuo account.