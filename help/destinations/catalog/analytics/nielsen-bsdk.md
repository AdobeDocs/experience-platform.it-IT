---
keywords: Nielsen BSDK;nielsen bsdk;nielsen BSDK
title: Estensione Nielsen BSDK
seo-title: Estensione Nielsen BSDK
description: L’estensione Nielsen BSDK è una destinazione di analisi nella piattaforma dati cliente in tempo reale. Per ulteriori informazioni sulla funzionalità di estensione, vedere la pagina di estensione in  Adobe Exchange.
seo-description: L’estensione Nielsen BSDK è una destinazione di analisi nella piattaforma dati cliente in tempo reale. Per ulteriori informazioni sulla funzionalità di estensione, vedere la pagina di estensione in  Adobe Exchange.
translation-type: tm+mt
source-git-commit: 80db19822551883da272787affb6f7dc9dc3a745
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 3%

---


# [!DNL Nielsen BSDK] Estensione {#nielsen-bsdk-extension}

## Panoramica {#overview}

[!DNL Nielsen Digital SDK] L&#39;estensione launch offre la misurazione del pubblico tramite i seguenti prodotti di misurazione digitale:

DCR: Una soluzione di misurazione che fornisce misurazioni giornaliere dei contenuti digitali non lineari, compresi i contenuti con annunci pubblicitari, consentirà di visualizzare in modo completo il consumo di contenuti digitali tra Desktop, Mobile, Tablet e Dispositivi collegati.

DTVR: Questo account consente la visualizzazione lineare della TV su computer desktop e dispositivi mobili per le origini di programmazione partecipanti. Questa è la prima soluzione a ricevere l&#39;accreditamento dal MRC per il suo contributo alla misurazione del pubblico TV per la programmazione visualizzata su computer e dispositivi mobili.

[!DNL Nielsen BSDK] è un&#39;estensione di analisi in Real-time Customer Data Platform. Per ulteriori informazioni sulla funzionalità di estensione, consultate la pagina dell&#39;estensione in [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101361.html).

Questa destinazione è un&#39;estensione Adobe Experience Platform Launch . Per ulteriori informazioni sul funzionamento delle estensioni Platform Launch in CDP in tempo reale, consultate [panoramica](../launch-extensions/overview.md)delle estensioni Adobe Experience Platform Launch.

![Estensione Nielsen BSDK](../../assets/catalog/analytics/nielsen-bsdk/catalog.png)

## Prerequisiti   {#prerequisites}

Questa estensione è disponibile nel [!DNL Destinations] catalogo per tutti i clienti che hanno acquistato CDP in tempo reale.

Per utilizzare questa estensione, è necessario accedere a  Adobe Experience Platform Launch. Launch piattaforma è disponibile per i clienti Adobe Experience Cloud come funzione inclusa a valore aggiunto. Contatta l’amministratore dell’organizzazione per ottenere l’accesso a Platform Launch e chiedi loro di concederti l’ **[!UICONTROL manage_properties]** autorizzazione per l’installazione delle estensioni.

## Installa estensione {#install-extension}

Per installare l’ [!DNL Nielsen BSDK] estensione:

Nell’interfaccia [CDP in tempo](http://platform.adobe.com/)reale, passare a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Selezionate l’estensione dal catalogo o usate la barra di ricerca.

Fai clic sulla destinazione per evidenziarla, quindi selezionala **[!UICONTROL Configure]** nella barra a destra. Se il **[!UICONTROL Configure]** controllo è disattivato, manca l&#39; **[!UICONTROL manage_properties]** autorizzazione. Consultate [Prerequisiti](#prerequisites).

Nella **[!UICONTROL Select available Platform Launch property]** finestra, selezionate la proprietà Lancio piattaforma in cui desiderate installare l&#39;estensione. È inoltre possibile creare una nuova proprietà in Lancio piattaforma. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Ulteriori informazioni sulle proprietà sono disponibili nella sezione [della pagina](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) Proprietà della documentazione Lancio piattaforma.

Il flusso di lavoro consente di passare al lancio della piattaforma per completare l’installazione.

Per informazioni sulle opzioni di configurazione dell&#39;estensione e sul supporto dell&#39;installazione, consultate la pagina [Nielsen BSDK in  Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101361.html).

È inoltre possibile installare l’estensione direttamente nell’interfaccia [](https://launch.adobe.com/)Adobe Experience Platform Launch. Consultate [Aggiungere una nuova estensione](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) nella documentazione di Launch piattaforma.

## Come utilizzare l&#39;estensione {#how-to-use}

Una volta installata l’estensione, potete avviare la configurazione delle relative regole direttamente in Launch piattaforma.

In Avvio piattaforma, potete impostare le regole per le estensioni installate per inviare i dati dell&#39;evento alla destinazione dell&#39;estensione solo in alcune situazioni. Per ulteriori informazioni sulla configurazione delle regole per le estensioni, consulta la documentazione [sulle](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html)regole.

## Configurare, aggiornare ed eliminare l&#39;estensione {#configure-upgrade-delete}

Puoi configurare, aggiornare ed eliminare le estensioni nell&#39;interfaccia Launch piattaforma.

>[!TIP]
>
>Se l’estensione è già installata su una delle proprietà, l’interfaccia utente CDP in tempo reale continua a essere visualizzata **[!UICONTROL Install]** per l’estensione. Per accedere al lancio della piattaforma e configurare o eliminare l’estensione, selezionate il flusso di lavoro di installazione come descritto in [Installazione estensione](#install-extension) .

Per aggiornare l’estensione, consultate Aggiornamento [dell’](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) estensione nella documentazione di avvio della piattaforma.