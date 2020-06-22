---
title: Google AdsDestination
seo-title: Destinazione annunci Google
description: Google Ads, precedentemente noto come Google AdWords, è un servizio pubblicitario online che consente alle aziende di pagare per clic pubblicità tra ricerche basate su testo, display grafici, video YouTube e display mobili in-app.
seo-description: Google Ads, precedentemente noto come Google AdWords, è un servizio pubblicitario online che consente alle aziende di pagare per clic pubblicità tra ricerche basate su testo, display grafici, video YouTube e display mobili in-app.
translation-type: tm+mt
source-git-commit: 3c598454a868139b7604c5c7ca2b98fa0f1bb961
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# Destinazione annunci Google

## Panoramica

Google Ads, precedentemente noto come Google AdWords, è un servizio pubblicitario online che consente alle aziende di pagare per clic pubblicità tra ricerche basate su testo, display grafici, video YouTube e display mobili in-app.

## Specifiche di destinazione

Nota i seguenti dettagli specifici per le destinazioni Google Ads:

* Puoi inviare le seguenti [identità](../../identity-service/namespaces.md) alle destinazioni Google Ads: **ID cookie Google, IDFA, GAID, ID Roku, ID Microsoft, ID Amazon Fire TV**.
* I tipi di pubblico attivati vengono creati a livello di programmazione nella piattaforma Google.
* Adobe Real-time CDP al momento non include una metrica di misurazione per convalidare l’attivazione. Per convalidare l&#39;integrazione e comprendere le dimensioni del targeting dell&#39;audience, fare riferimento ai conteggi dell&#39;audience in Google.

>[!IMPORTANT]
>
>Se stai cercando di creare la tua prima destinazione con Google Ads e non hai attivato la funzionalità [di sincronizzazione](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) ID in  Experience Cloud ID Service in passato (con  Audience Manager o altre applicazioni), contatta Adobe Consulting o l’Assistenza clienti per abilitare la sincronizzazione degli ID. Se in precedenza avevate impostato integrazioni Google in  Audience Manager, le sincronizzazioni ID che avevate configurato riportano ad Adobe Real-time CDP.

## Prerequisiti

### Account Google Ads esistente

Google ha messo in pausa tutte le nuove integrazioni Google Ads con fornitori di terze parti. Devi disporre di un&#39;integrazione esistente con Google Ads per poter eseguire i passaggi di elenco di autorizzazioni nella sezione successiva e per creare una destinazione Google Ads in Adobe Real-time CDP.

### Consenti elenco

>[!NOTE]
>
>L&#39;elenco di autorizzazioni è obbligatorio prima di configurare la prima destinazione Google Ads in Adobe Real-time CDP. Prima di creare una destinazione, verificare che la procedura di autorizzazione elenco descritta di seguito sia stata completata da Google.

Prima di creare la destinazione Google Ads in Adobe Real-time CDP, è necessario contattare Google affinché Adobe sia incluso nell&#39;elenco dei provider di dati consentiti e che il tuo account sia aggiunto all&#39;elenco dei provider di dati consentiti. Contattate Google e fornite le seguenti informazioni:

* **ID** account: questo è l&#39;ID account di Adobe con Google. Per ottenere questo ID, contatta l’Assistenza clienti Adobe o il tuo rappresentante Adobe.
* **ID** cliente: questo è l&#39;ID account cliente di Adobe con Google. Per ottenere questo ID, contatta l’Assistenza clienti Adobe o il tuo rappresentante Adobe.
* Tipo di account: **AdWords**
* **ID** Google AdWords: Questo è il tuo ID con Google. Il formato ID è in genere 123-456-7890.

## Crea destinazione

1. In **[!UICONTROL Connections > Destinations]**, selezionate Google Ads, quindi **[!UICONTROL Create destination]**.
   ![Destinazione di Connect Google Ads](/help/rtcdp/destinations/assets/google-2-destination.png)

2. Nel passaggio **Configurazione** del flusso di lavoro di creazione della destinazione, compila il modulo [!UICONTROL Basic Information] per la destinazione. <br>
   ![Informazioni di base Google Ads](/help/rtcdp/destinations/assets/google-ads-setup-step.png)
* **[!UICONTROL Name]**: Compila il nome preferito per questa destinazione.
* **[!UICONTROL Description]**: Facoltativo. Ad esempio, potete specificare per quale campagna state utilizzando questa destinazione.
* **[!UICONTROL Account Type]**: AdWords è l&#39;unica opzione disponibile.
* **[!UICONTROL Account ID]**: Compila il tuo ID account con Google Ads. Il formato ID è in genere 123-456-7890.
* **[!UICONTROL Marketing use case]**: I casi di utilizzo del marketing indicano l&#39;intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra i casi di utilizzo di marketing definiti da Adobe oppure creare un tuo caso di utilizzo di marketing. Per ulteriori informazioni sui casi di utilizzo del marketing, consulta la pagina [Governance dei dati in CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) in tempo reale. Per informazioni sui singoli casi di utilizzo marketing definiti da Adobe, consulta la panoramica [dei criteri di utilizzo dei](/help/data-governance/policies/overview.md#core-actions)dati.

## Attivare i segmenti su Google Ads

Per istruzioni su come attivare i segmenti in Google Ads, consulta [Attivare i dati sulle destinazioni](/help/rtcdp/destinations/activate-destinations.md).

