---
title: Google AdsDestination
seo-title: Destinazione annunci Google
description: Google Ads, precedentemente noto come Google AdWords, è un servizio pubblicitario online che consente alle aziende di pagare per clic pubblicità tra ricerche basate su testo, display grafici, video YouTube e display mobili in-app.
seo-description: Google Ads, precedentemente noto come Google AdWords, è un servizio pubblicitario online che consente alle aziende di pagare per clic pubblicità tra ricerche basate su testo, display grafici, video YouTube e display mobili in-app.
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---


# [!DNL Google Ads] Destinazione

## Panoramica

[!DNL Google Ads], precedentemente noto come [!DNL Google AdWords], è un servizio pubblicitario online che consente alle aziende di effettuare pubblicità pay-per-click tra ricerche basate su testo, display grafici, [!DNL YouTube] video e display mobili in-app.

## Specifiche di destinazione

Tenete presenti i seguenti dettagli specifici per [!DNL Google Ads] le destinazioni:

* Puoi inviare le seguenti [identità](../../identity-service/namespaces.md) alle [!DNL Google Ads] destinazioni: **ID cookie Google, IDFA, GAID, ID Roku, ID Microsoft, ID Amazon Fire TV**.
* I tipi di pubblico attivati vengono creati a livello di programmazione nella [!DNL Google] piattaforma.
* Adobe Real-time CDP al momento non include una metrica di misurazione per convalidare l’attivazione. Per convalidare l&#39;integrazione e comprendere le dimensioni del targeting dell&#39;audience, fare riferimento ai conteggi dell&#39;audience in Google.

>[!IMPORTANT]
>
>Se stai cercando di creare la tua prima destinazione con [!DNL Google Ads] e non hai attivato la funzionalità [di sincronizzazione](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID in  servizio ID Experience Cloud in passato (con  Audience Manager o altre applicazioni), contatta il servizio Consulenza Adobe o l&#39;Assistenza clienti per abilitare la sincronizzazione degli ID. Se in precedenza avevate impostato integrazioni Google in  Audience Manager, le sincronizzazioni ID che avevate configurato riportano ad Adobe Real-time CDP.

## Prerequisiti

### Account [!DNL Google Ads] esistente

[!DNL Google] ha messo in pausa qualsiasi nuova [!DNL Google Ads] integrazione con fornitori di terze parti. È necessario disporre di un&#39;integrazione esistente con [!DNL Google Ads] per poter eseguire i passi  elenco consentiti nella sezione successiva e creare una [!DNL Google Ads] destinazione in Adobe Real-time CDP.

### Elenco consentiti 

>[!NOTE]
>
>Il elenco consentiti  è obbligatorio prima di configurare la prima [!DNL Google Ads] destinazione in Adobe Real-time CDP. Assicurarsi che il processo di elenco consentiti  descritto di seguito sia stato completato [!DNL Google] prima di creare una destinazione.

Prima di creare la [!DNL Google Ads] destinazione in Adobe Real-time CDP, è necessario contattare Adobe [!DNL Google] per essere incluso nell&#39;elenco dei provider di dati consentiti e per aggiungere l&#39;account al elenco consentiti . Contattate [!DNL Google] e fornite le seguenti informazioni:

* **ID** account: questo è l&#39;ID account di Adobe con [!DNL Google]. Per ottenere questo ID, contatta l’Assistenza clienti Adobe o il tuo rappresentante Adobe.
* **ID** cliente: questo è l&#39;ID account cliente di Adobe con [!DNL Google]. Per ottenere questo ID, contatta l’Assistenza clienti Adobe o il tuo rappresentante Adobe.
* Tipo di account: **AdWords**
* **ID** Google AdWords: Questo è il tuo ID con [!DNL Google]. Il formato ID è in genere 123-456-7890.

## Crea destinazione

1. In **[!UICONTROL Connections > Destinations]**, selezionate [!DNL Google Ads], quindi **[!UICONTROL Create destination]**.
   ![Destinazione di Connect Google Ads](/help/rtcdp/destinations/assets/google-2-destination.png)

2. Nel passaggio **Configurazione** del flusso di lavoro di creazione della destinazione, compila il modulo [!UICONTROL Basic Information] per la destinazione. <br>

   ![Informazioni di base Google Ads](/help/rtcdp/destinations/assets/google-2-destination-setup-step.png)
* **[!UICONTROL Name]**: Compila il nome preferito per questa destinazione.
* **[!UICONTROL Description]**: Facoltativo. Ad esempio, potete specificare per quale campagna state utilizzando questa destinazione.
* **[!UICONTROL Account Type]**: AdWords è l&#39;unica opzione disponibile.
* **[!UICONTROL Account ID]**: Compila il tuo ID account con [!DNL Google Ads]. Il formato ID è in genere 123-456-7890.
* **[!UICONTROL Marketing use case]**: I casi di utilizzo del marketing indicano l&#39;intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra i casi di utilizzo di marketing definiti da Adobe oppure creare un tuo caso di utilizzo di marketing. Per ulteriori informazioni sui casi di utilizzo del marketing, consulta la pagina [Governance dei dati in CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) in tempo reale. Per informazioni sui singoli casi di utilizzo marketing definiti da Adobe, consulta la panoramica [dei criteri di utilizzo dei](/help/data-governance/policies/overview.md#core-actions)dati.

## Attiva i segmenti in [!DNL Google Ads]

Per istruzioni su come attivare i segmenti in [!DNL Google Ads], consulta [Attivare i dati sulle destinazioni](/help/rtcdp/destinations/activate-destinations.md).

