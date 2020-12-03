---
keywords: Advertising Cloud;advertising cloud extension; advertising cloud destination
title: Estensione Adobe Advertising Cloud
seo-title: Estensione Adobe Advertising Cloud
description: L'estensione Adobe Advertising Cloud è una destinazione pubblicitaria nella piattaforma dati cliente in tempo reale. Per ulteriori informazioni sulla funzionalità di estensione, vedere la pagina di estensione in  Adobe Exchange.
seo-description: L'estensione Adobe Advertising Cloud è una destinazione pubblicitaria nella piattaforma dati cliente in tempo reale. Per ulteriori informazioni sulla funzionalità di estensione, vedere la pagina di estensione in  Adobe Exchange.
translation-type: tm+mt
source-git-commit: c24676970629f5a39297001357f8af40895533d9
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 3%

---


# Adobe Advertising Cloud Extension {#adobe-advertising-cloud-extension}

## Panoramica {#overview}

Questa è l&#39; [!DNL Advertising Cloud] [!DNL Advertising Cloud] estensione per l&#39;implementazione dei tag di conversione e segmento per i tag DSP e Search (DCO non è attualmente supportato).

Adobe Advertising Cloud è un&#39;estensione pubblicitaria in Real-time Customer Data Platform.

Questa destinazione è un&#39; [!DNL Adobe Experience Platform Launch] estensione. Per ulteriori informazioni sul funzionamento [!DNL Platform Launch] delle estensioni in CDP in tempo reale, consultate Panoramica [sulle estensioni di](../launch-extensions/overview.md)Experience Platform Launch.

![Estensione Adobe Advertising Cloud](../../assets/catalog/advertising/adobe-advertising-cloud/catalog.png)

## Prerequisiti   {#prerequisites}

Questa estensione è disponibile nel catalogo Destinazioni per tutti i clienti che hanno acquistato CDP in tempo reale.

Per utilizzare questa estensione, è necessario accedere a [!DNL Experience Platform Launch]. [!DNL Experience Platform Launch] viene offerta ai clienti Adobe Experience Cloud come funzione inclusa a valore aggiunto. Contattate l’amministratore dell’organizzazione per ottenere l’accesso [!DNL Launch] e chiedete loro di concedervi l’ **[!UICONTROL manage_properties]** autorizzazione necessaria per installare le estensioni.

## Installa estensione {#install-extension}

Per installare l’estensione Adobe Advertising Cloud:

Nell’interfaccia [CDP in tempo](http://platform.adobe.com/)reale, passare a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Selezionate l’estensione dal catalogo o usate la barra di ricerca.

Fai clic sulla destinazione per evidenziarla, quindi selezionala **[!UICONTROL Configure]** nella barra a destra. Se il **[!UICONTROL Configure]** controllo è disattivato, manca l&#39; **[!UICONTROL manage_properties]** autorizzazione. Consultate [Prerequisiti](#prerequisites).

Nella **[!UICONTROL Select available Platform Launch property]** finestra, selezionate la [!DNL Platform Launch] proprietà in cui desiderate installare l’estensione. È inoltre possibile creare una nuova proprietà in [!DNL Platform Launch]. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Ulteriori informazioni sulle proprietà sono disponibili nella sezione [della pagina](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) Proprietà della [!DNL Launch] documentazione.

Il flusso di lavoro consente di completare [!DNL Platform Launch] l’installazione.

È inoltre possibile installare l’estensione direttamente nell’interfaccia [](https://launch.adobe.com/)Adobe Experience Platform Launch. Consultate [Aggiungere una nuova estensione](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) nella [!DNL Platform Launch] documentazione.


## Come utilizzare l&#39;estensione {#how-to-use}

Una volta installata l’estensione, potete avviare l’impostazione delle relative regole direttamente in [!DNL Platform Launch].

In [!DNL Platform Launch], potete impostare le regole per le estensioni installate per inviare i dati dell&#39;evento alla destinazione dell&#39;estensione solo in alcune situazioni. Per ulteriori informazioni sulla configurazione delle regole per le estensioni, consulta la documentazione [sulle](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html)regole.

## Configurare, aggiornare ed eliminare l&#39;estensione {#configure-upgrade-delete}

È possibile configurare, aggiornare ed eliminare le estensioni nell&#39; [!DNL Platform Launch] interfaccia.

>[!TIP]
>
>Se l’estensione è già installata su una delle proprietà, l’interfaccia utente CDP in tempo reale continua a essere visualizzata **[!UICONTROL Install]** per l’estensione. Per accedere al flusso di lavoro di installazione e configurarlo o eliminarlo, fate clic su [Installa estensione](#install-extension) [!DNL Platform Launch] .

Per aggiornare l’estensione, consultate Aggiornamento [dell’](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) estensione nella [!DNL Platform Launch] documentazione.
