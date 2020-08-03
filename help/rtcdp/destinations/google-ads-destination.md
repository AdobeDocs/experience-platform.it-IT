---
title: Google AdsDestination
seo-title: Destinazione annunci Google
description: Google Ads, precedentemente noto come Google AdWords, è un servizio pubblicitario online che consente alle aziende di pagare per clic pubblicità tra ricerche basate su testo, display grafici, video YouTube e display mobili in-app.
seo-description: Google Ads, precedentemente noto come Google AdWords, è un servizio pubblicitario online che consente alle aziende di pagare per clic pubblicità tra ricerche basate su testo, display grafici, video YouTube e display mobili in-app.
translation-type: tm+mt
source-git-commit: 570c627672439a5ee0f4215b7bf7915ec3dd2bb3
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---


# [!DNL Google Ads] Destinazione

## Panoramica

[!DNL Google Ads], precedentemente noto come [!DNL Google AdWords], è un servizio pubblicitario online che consente alle aziende di effettuare pubblicità pay-per-click tra ricerche basate su testo, display grafici, [!DNL YouTube] video e display mobili in-app.

## Specifiche di destinazione

Tenete presenti i seguenti dettagli specifici per [!DNL Google Ads] le destinazioni:

* Puoi inviare le seguenti [identità](../../identity-service/namespaces.md) alle [!DNL Google Ads] destinazioni: **ID di cookie Google, IDFA, GAID, Roku ID, Microsoft ID,  Amazon Fire TV ID**.
* I tipi di pubblico attivati vengono creati a livello di programmazione nella [!DNL Google] piattaforma.
*  CDP in tempo reale del Adobe attualmente non include una metrica di misurazione per convalidare l’attivazione. Per convalidare l&#39;integrazione e comprendere le dimensioni del targeting dell&#39;audience, fare riferimento ai conteggi dell&#39;audience in Google.

>[!IMPORTANT]
>
>Se stai cercando di creare la tua prima destinazione con [!DNL Google Ads] e non hai attivato la funzionalità [di sincronizzazione](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID in  Experience Cloud ID Service in passato (con  Audience Manager o altre applicazioni), contatta  Consulenza Adobe o l’Assistenza clienti per abilitare le sincronizzazioni ID. Se in precedenza avevate impostato integrazioni Google in  Audience Manager, le sincronizzazioni ID che avevate impostato per il riporto  CDP in tempo reale del Adobe.

## Prerequisiti

### Account [!DNL Google Ads] esistente

[!DNL Google] ha messo in pausa qualsiasi nuova [!DNL Google Ads] integrazione con fornitori di terze parti. Per poter eseguire i passaggi del elenco consentiti  nella sezione successiva e creare una [!DNL Google Ads] destinazione in  CDP in tempo reale Adobe, è necessario disporre di un&#39;integrazione esistente con [!DNL Google Ads] il sistema.

### Elenco consentiti 

>[!NOTE]
>
>Il elenco consentiti  è obbligatorio prima di impostare la prima [!DNL Google Ads] destinazione  CDP in tempo reale Adobe. Assicurarsi che il processo di elenco consentiti  descritto di seguito sia stato completato [!DNL Google] prima di creare una destinazione.

Prima di creare la [!DNL Google Ads] destinazione in CDP in tempo reale  Adobe, è necessario contattare [!DNL Google] affinché  Adobe venga inserito nell&#39;elenco dei provider di dati consentiti e che il vostro account venga aggiunto al elenco consentiti di . Contattate [!DNL Google] e fornite le seguenti informazioni:

* **ID** account:  ID account  Adobe con [!DNL Google]. Per ottenere questo ID, contatta &#39;Assistenza clienti di Adobe o il rappresentante del Adobe .
* **ID** cliente: si tratta  ID account  cliente con [!DNL Google]. Per ottenere questo ID, contatta &#39;Assistenza clienti di Adobe o il rappresentante del Adobe .
* Tipo di account: **AdWords**
* **ID** Google AdWords: Questo è il tuo ID con [!DNL Google]. Il formato ID è in genere 123-456-7890.

## Crea destinazione

1. In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selezionare [!DNL Google Ads], quindi **[!UICONTROL Create destination]**.
   ![Destinazione di Connect Google Ads](/help/rtcdp/destinations/assets/google-2-destination.png)

2. Nel passaggio **Configurazione** del flusso di lavoro di creazione della destinazione, compila il modulo [!UICONTROL Basic Information] per la destinazione. <br>

   ![Informazioni di base Google Ads](/help/rtcdp/destinations/assets/google-2-destination-setup-step.png)
* **[!UICONTROL Name]**: Compila il nome preferito per questa destinazione.
* **[!UICONTROL Description]**: Facoltativo. Ad esempio, potete specificare per quale campagna state utilizzando questa destinazione.
* **[!UICONTROL Account Type]**: AdWords è l&#39;unica opzione disponibile.
* **[!UICONTROL Account ID]**: Compila il tuo ID account con [!DNL Google Ads]. Il formato ID è in genere 123-456-7890.
* **[!UICONTROL Marketing use case]**: I casi di utilizzo del marketing indicano l&#39;intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra  casi di utilizzo di marketing definiti dal Adobe o creare un caso di utilizzo di marketing personale. Per ulteriori informazioni sui casi di utilizzo del marketing, consulta la pagina [Governance dei dati in CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) in tempo reale. Per informazioni sui singoli casi di utilizzo marketing definiti dal Adobe , consulta la panoramica [sui criteri di utilizzo dei](/help/data-governance/policies/overview.md#core-actions)dati.

## Attiva i segmenti in [!DNL Google Ads]

Per istruzioni su come attivare i segmenti in [!DNL Google Ads], consulta [Attivare i dati sulle destinazioni](/help/rtcdp/destinations/activate-destinations.md).

## Dati esportati

Per verificare se i dati sono stati esportati correttamente nella [!DNL Google Ads] destinazione, controlla il tuo [!DNL Google Ads] account. Se l&#39;attivazione ha avuto esito positivo, l&#39;audience viene popolata nel vostro account.