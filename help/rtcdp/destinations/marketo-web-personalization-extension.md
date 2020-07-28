---
title: Estensione Marketo Web Personalization
seo-title: Estensione Marketo Web Personalization
description: L'estensione Marketing Web Personalization (Personalizzazione Web Marketo) è una destinazione di personalizzazione nell'Platform dati cliente in tempo reale  Adobe. Per ulteriori informazioni sulla funzionalità di estensione, vedere la pagina di estensione in  Adobe Exchange.
seo-description: L'estensione Marketing Web Personalization (Personalizzazione Web Marketo) è una destinazione di personalizzazione nell'Platform dati cliente in tempo reale  Adobe. Per ulteriori informazioni sulla funzionalità di estensione, vedere la pagina di estensione in  Adobe Exchange.
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 4%

---


# [!DNL Marketo Web Personalization] Estensione {#marketo-web-personalization-extension}

## Panoramica {#overview}

Questa estensione distribuisce lo script per le applicazioni [!DNL Marketo’s] Web Personalization e ContentAI. [!DNL Marketo] Web Personalization (Personalizzazione Web) identifica e personalizza in modo univoco il contenuto in base alle caratteristiche del visitatore Web, come la grafica per visitatori anonimi e un&#39;ampia gamma di attributi comportamentali all&#39;interno dell&#39;Platform [!DNL Marketo] Engagement per i visitatori noti. [!DNL Marketo] ContentAI contiene funzionalità per le raccomandazioni basate sull&#39;intelligenza artificiale e la personalizzazione per le campagne Web ed e-mail che sono uniche per i clienti B2B.

[!DNL Marketo Web Personalization] è un&#39;estensione di personalizzazione in  Adobe Real-time Customer Data Platform. Per ulteriori informazioni sulla funzionalità di estensione, consultate la pagina dell&#39;estensione in [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101232.marketo-web-personalization.html).

Questa destinazione è un&#39;estensione di Experience Platform Launch. Per ulteriori informazioni sul funzionamento delle estensioni Launch  Adobe CDP in tempo reale, vedere Panoramica [sulle estensioni](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Experience Platform Launch.

![Estensione Marketo Web Personalization](assets/marketo-web-personalization-extension.png)

## Prerequisiti  {#prerequisites}

Questa estensione è disponibile nel [!DNL Destinations] catalogo per tutti i clienti che hanno acquistato  Adobe CDP in tempo reale.

Per utilizzare questa estensione, è necessario accedere al Experience Platform Launch. Il Experience Platform Launch è offerto ai clienti Adobe Experience Cloud come una funzione inclusa a valore aggiunto. Contatta l’amministratore dell’organizzazione per ottenere l’accesso a Launch e chiedi loro di concederti l’ **[!UICONTROL manage_properties]** autorizzazione necessaria per installare le estensioni.

## Installa estensione {#install-extension}

Per installare l’ [!DNL Marketo Web Personalization] estensione:

1. Nell&#39;interfaccia CDP in tempo reale del [Adobe](http://platform.adobe.com/), passare a **[!UICONTROL Destinations > Catalog]**.
2. Selezionate l’estensione dal catalogo o usate la barra di ricerca.
3. Fai clic sulla destinazione per evidenziarla, quindi selezionala **[!UICONTROL Install Extension]** nella barra a destra. Se il **[!UICONTROL Install Extension]** controllo è disattivato, manca l&#39; **[!UICONTROL manage_properties]** autorizzazione. Consultate [Prerequisiti](#prerequisites).
4. Nella **[!UICONTROL Select available Launch property]** finestra, selezionate la proprietà Launch in cui desiderate installare l&#39;estensione. È inoltre possibile creare una nuova proprietà in Launch. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Ulteriori informazioni sulle proprietà sono disponibili nella sezione [della pagina](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Proprietà della documentazione di Launch.
5. Per completare l’installazione, passa a Launch.

Per informazioni sulle opzioni di configurazione dell&#39;estensione e sul supporto dell&#39;installazione, consultate la pagina [Marketing Web Personalization in  Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101232.marketo-web-personalization.html).

Potete anche installare l’estensione direttamente nell’interfaccia [del](https://launch.adobe.com/)Experience Platform Launch. Consultate [Aggiungere una nuova estensione](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) nella documentazione di Launch.

## Come utilizzare l&#39;estensione {#how-to-use}

Una volta installata l’estensione, potete avviare la configurazione delle relative regole direttamente in Launch.

In Launch, puoi impostare le regole per le estensioni installate per inviare i dati dell&#39;evento alla destinazione dell&#39;estensione solo in alcune situazioni. Per ulteriori informazioni sulla configurazione delle regole per le estensioni, consulta la documentazione [sulle](https://docs.adobe.com/help/it-IT/launch/using/reference/manage-resources/rules.html)regole.

## Configurare, aggiornare ed eliminare l&#39;estensione {#configure-upgrade-delete}

Puoi configurare, aggiornare ed eliminare le estensioni nell&#39;interfaccia Launch.

>[!TIP]
>
>Se l’estensione è già installata su una delle proprietà, l’interfaccia utente CDP in tempo reale del Adobe  continua a essere visualizzata **[!UICONTROL Install]** per l’estensione. Per accedere a Launch e configurare o eliminare l’estensione, scegli il flusso di lavoro di installazione come descritto in Estensione [di](#install-extension) installazione.

Per aggiornare l’estensione, consulta Aggiornamento [](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) estensione nella documentazione di Launch.