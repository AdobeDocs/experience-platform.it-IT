---
keywords: Marketo Web Personalization;marketo web personalization;Marketo Web Personalization extension;marketo web personalization extension;marketo;Marketo
title: Estensione Marketo Web Personalization
seo-title: Estensione Marketo Web Personalization
description: L’estensione Marketing Web Personalization (Personalizzazione Web Marketo) è una destinazione di personalizzazione nella piattaforma dati cliente in tempo reale. Per ulteriori informazioni sulla funzionalità di estensione, vedere la pagina di estensione in  Adobe Exchange.
seo-description: L’estensione Marketing Web Personalization (Personalizzazione Web Marketo) è una destinazione di personalizzazione nella piattaforma dati cliente in tempo reale. Per ulteriori informazioni sulla funzionalità di estensione, vedere la pagina di estensione in  Adobe Exchange.
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 4%

---


# [!DNL Marketo Web Personalization] Estensione {#marketo-web-personalization-extension}

## Panoramica {#overview}

Questa estensione distribuisce lo script per le applicazioni [!DNL Marketo’s] Web Personalization e ContentAI. [!DNL Marketo] Web Personalization identifica e personalizza in modo univoco il contenuto in base alle caratteristiche dei visitatori Web, come la grafica per i visitatori anonimi e un&#39;ampia gamma di attributi comportamentali all&#39;interno della piattaforma [!DNL Marketo] di coinvolgimento per i visitatori noti. [!DNL Marketo] ContentAI contiene funzionalità per le raccomandazioni basate sull&#39;intelligenza artificiale e la personalizzazione per le campagne Web ed e-mail che sono uniche per i clienti B2B.

[!DNL Marketo Web Personalization] è un&#39;estensione di personalizzazione in Real-time Customer Data Platform. Per ulteriori informazioni sulla funzionalità di estensione, consultate la pagina dell&#39;estensione in [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101232.marketo-web-personalization.html).

Questa destinazione è un&#39;estensione Adobe Experience Platform Launch . Per ulteriori informazioni sul funzionamento delle estensioni Platform Launch  Adobe CDP in tempo reale, consultate [panoramica](/help/rtcdp/destinations/experience-platform-launch-extensions.md)delle estensioni Adobe Experience Platform Launch.

![Estensione Marketo Web Personalization](assets/marketo-web-personalization-extension.png)

## Prerequisiti   {#prerequisites}

Questa estensione è disponibile nel [!DNL Destinations] catalogo per tutti i clienti che hanno acquistato  Adobe CDP in tempo reale.

Per utilizzare questa estensione, è necessario accedere a  Adobe Experience Platform Launch. Launch piattaforma è disponibile per i clienti Adobe Experience Cloud come funzione inclusa a valore aggiunto. Contatta l’amministratore dell’organizzazione per ottenere l’accesso a Platform Launch e chiedi loro di concederti l’ **[!UICONTROL manage_properties]** autorizzazione per l’installazione delle estensioni.

## Installa estensione {#install-extension}

Per installare l’ [!DNL Marketo Web Personalization] estensione:

1. Nell&#39;interfaccia CDP in tempo reale del [Adobe](http://platform.adobe.com/), passare a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.
2. Selezionate l’estensione dal catalogo o usate la barra di ricerca.
3. Fai clic sulla destinazione per evidenziarla, quindi selezionala **[!UICONTROL Configure]** nella barra a destra. Se il **[!UICONTROL Configure]** controllo è disattivato, manca l&#39; **[!UICONTROL manage_properties]** autorizzazione. Consultate [Prerequisiti](#prerequisites).
4. Nella **[!UICONTROL Select available Platform Launch property]** finestra, selezionate la proprietà Lancio piattaforma in cui desiderate installare l&#39;estensione. È inoltre possibile creare una nuova proprietà in Lancio piattaforma. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Ulteriori informazioni sulle proprietà sono disponibili nella sezione [della pagina](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Proprietà della documentazione Lancio piattaforma.
5. Il flusso di lavoro consente di passare al lancio della piattaforma per completare l’installazione.

Per informazioni sulle opzioni di configurazione dell&#39;estensione e sul supporto dell&#39;installazione, consultate la pagina [Marketing Web Personalization in  Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101232.marketo-web-personalization.html).

È inoltre possibile installare l’estensione direttamente nell’interfaccia [](https://launch.adobe.com/)Adobe Experience Platform Launch. Consultate [Aggiungere una nuova estensione](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) nella documentazione di Launch piattaforma.

## Come utilizzare l&#39;estensione {#how-to-use}

Una volta installata l’estensione, potete avviare la configurazione delle relative regole direttamente in Launch piattaforma.

In Avvio piattaforma, potete impostare le regole per le estensioni installate per inviare i dati dell&#39;evento alla destinazione dell&#39;estensione solo in alcune situazioni. Per ulteriori informazioni sulla configurazione delle regole per le estensioni, consulta la documentazione [sulle](https://docs.adobe.com/help/it-IT/launch/using/reference/manage-resources/rules.html)regole.

## Configurare, aggiornare ed eliminare l&#39;estensione {#configure-upgrade-delete}

Puoi configurare, aggiornare ed eliminare le estensioni nell&#39;interfaccia Launch piattaforma.

>[!TIP]
>
>Se l’estensione è già installata su una delle proprietà, l’interfaccia utente CDP in tempo reale del Adobe  continua a essere visualizzata **[!UICONTROL Install]** per l’estensione. Per accedere al lancio della piattaforma e configurare o eliminare l’estensione, selezionate il flusso di lavoro di installazione come descritto in [Installazione estensione](#install-extension) .

Per aggiornare l’estensione, consultate Aggiornamento [dell’](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) estensione nella documentazione di avvio della piattaforma.