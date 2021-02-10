---
keywords: gtag;google gtag;google gtag extension;google gtag extension;GTAG
title: Estensione Google Gtag
description: L'estensione Google Gtag è una destinazione pubblicitaria in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, vedere la pagina di estensione in  Adobe Exchange.
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 3%

---


# Estensione Google gtag {#gtag-advertising-extension}

Caricate l&#39;elemento `gtag.js` di Google nel sito per inviare i dati dell&#39;evento a [!DNL Google Analytics], Google Ads e [!DNL Google Marketing Platform]. Questa estensione aggiunge al sito solo il codice del tag. Dovrete utilizzare altre estensioni Google per aggiungere eventi e azioni che utilizzeranno gtag.

Google gtag è un&#39;estensione pubblicitaria in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, vedere la pagina dell&#39;estensione in [ Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

Questa destinazione è un&#39;estensione Adobe Experience Platform Launch . Per ulteriori informazioni sul funzionamento delle estensioni Platform Launch in Platform, vedere [ panoramica delle estensioni Adobe Experience Platform Launch](../launch-extensions/overview.md).

![Estensione Google Gtag](../../assets/catalog/advertising/gtag-advertising/catalog.png)

## Prerequisiti {#prerequisites}

Questa estensione è disponibile nel catalogo [!DNL Destinations] per tutti i clienti che hanno acquistato la piattaforma.

Per utilizzare questa estensione, è necessario accedere a  Adobe Experience Platform Launch. Launch piattaforma è disponibile per i clienti Adobe Experience Cloud come funzione inclusa a valore aggiunto. Contattate l&#39;amministratore dell&#39;organizzazione per ottenere l&#39;accesso a Platform Launch e chiedete loro di concedere l&#39;autorizzazione **[!UICONTROL manage_properties]** in modo da poter installare le estensioni.

## Installare l&#39;estensione {#install-extension}

Per installare l’estensione Google Gtag:

Nell&#39;interfaccia [Piattaforma](http://platform.adobe.com/), passare a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Selezionate l’estensione dal catalogo o usate la barra di ricerca.

Fare clic sulla destinazione per evidenziarla, quindi selezionare **[!UICONTROL Configure]** nella barra a destra. Se il controllo **[!UICONTROL Configure]** è disattivato, manca l&#39;autorizzazione **[!UICONTROL manage_properties]**. Vedere [Prerequisiti](#prerequisites).

Nella finestra **[!UICONTROL Select available Platform Launch property]**, selezionate la proprietà Lancio piattaforma in cui desiderate installare l&#39;estensione. È inoltre possibile creare una nuova proprietà in Lancio piattaforma. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Ulteriori informazioni sulle proprietà nella sezione [Proprietà della pagina](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) della documentazione di Launch piattaforma.

Il flusso di lavoro consente di passare al lancio della piattaforma per completare l’installazione.

Per informazioni sulle opzioni di configurazione dell&#39;estensione e sul supporto dell&#39;installazione, vedere la pagina [Google gtag in  Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

È inoltre possibile installare l&#39;estensione direttamente nell&#39; [ interfaccia Adobe Experience Platform Launch](https://launch.adobe.com/). Consultate [Aggiungere una nuova estensione](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) nella documentazione di Launch piattaforma.

## Come utilizzare l&#39;estensione {#how-to-use}

Una volta installata l’estensione, potete avviare la configurazione delle relative regole direttamente in Launch piattaforma.

In Avvio piattaforma, potete impostare le regole per le estensioni installate per inviare i dati dell&#39;evento alla destinazione dell&#39;estensione solo in alcune situazioni. Per ulteriori informazioni sull&#39;impostazione delle regole per le estensioni, vedere la [documentazione sulle regole](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Configurare, aggiornare ed eliminare l&#39;estensione {#configure-upgrade-delete}

Puoi configurare, aggiornare ed eliminare le estensioni nell&#39;interfaccia Launch piattaforma.

>[!TIP]
>
>Se l&#39;estensione è già installata su una delle proprietà, l&#39;interfaccia utente della piattaforma continua a visualizzare **[!UICONTROL Install]** per l&#39;estensione. Per accedere al lancio della piattaforma e configurare o eliminare l&#39;estensione, selezionate il flusso di lavoro di installazione come descritto in [Installa estensione](#install-extension).

Per aggiornare l&#39;estensione, consultare [Aggiornamento dell&#39;estensione](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) nella documentazione di Launch piattaforma.
