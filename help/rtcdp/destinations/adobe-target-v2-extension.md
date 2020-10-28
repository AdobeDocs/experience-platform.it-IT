---
keywords: target extension;target;target v2;target v2 extension
title: Estensione Adobe Target v2
seo-title: Estensione Adobe Target v2
description: L'estensione  Adobe Target v2 è una destinazione di personalizzazione  piattaforma dati cliente in tempo reale del Adobe. Per ulteriori informazioni sulla funzionalità di estensione, vedere la pagina di estensione in  Adobe Exchange.
seo-description: L'estensione  Adobe Target v2 è una destinazione di personalizzazione  piattaforma dati cliente in tempo reale del Adobe. Per ulteriori informazioni sulla funzionalità di estensione, vedere la pagina di estensione in  Adobe Exchange.
translation-type: tm+mt
source-git-commit: 511d64d1555151a70bdb9f71e4b50ec461c8a2e7
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 16%

---


# Estensione Adobe Target v2 {#adobe-target-v2-extension}

## Panoramica {#overview}

Adobe Target è la soluzione di Adobe Experience Cloud che offre tutto il necessario per adattare e personalizzare l’esperienza dei clienti al fine di massimizzare le entrate sui siti web e mobili, le app, i social media e altri canali digitali.

 Adobe Target v2 è un&#39;estensione di personalizzazione nella piattaforma dati cliente in tempo reale  Adobe. Per ulteriori informazioni sulla funzionalità di estensione, consultate la pagina dell&#39;estensione in [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102722.adobe-target-v2-launch-extension.html).

Questa destinazione è un&#39;estensione Adobe Experience Platform Launch . Per ulteriori informazioni sul funzionamento delle estensioni Platform Launch  Adobe CDP in tempo reale, consultate [panoramica](/help/rtcdp/destinations/experience-platform-launch-extensions.md)delle estensioni Adobe Experience Platform Launch.

![Estensione Adobe Target v2](/help/rtcdp/destinations/assets/adobe-target-v2-extension.png)

## Prerequisiti   {#prerequisites}

Questa estensione è disponibile nel [!DNL Destinations] catalogo per tutti i clienti che hanno acquistato  Adobe CDP in tempo reale.

Per utilizzare questa estensione, è necessario accedere a [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] viene offerta ai clienti Adobe Experience Cloud come funzione inclusa a valore aggiunto. Contattate l’amministratore dell’organizzazione per ottenere l’accesso [!DNL Platform Launch] e chiedete loro di concedervi l’ **[!UICONTROL manage_properties]** autorizzazione necessaria per installare le estensioni.

## Installa estensione {#install-extension}

Per installare l&#39;estensione  Adobe Target v2:

1. Nell&#39;interfaccia CDP in tempo reale del [Adobe](http://platform.adobe.com/), passare a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.
2. Selezionate l’estensione dal catalogo o usate la barra di ricerca.
3. Fai clic sulla destinazione per evidenziarla, quindi selezionala **[!UICONTROL Configure]** nella barra a destra. Se il **[!UICONTROL Configure]** controllo è disattivato, manca l&#39; **[!UICONTROL manage_properties]** autorizzazione. Consultate [Prerequisiti](#prerequisites).
4. Nella **[!UICONTROL Select available Launch property]** finestra, selezionate la [!DNL Launch] proprietà in cui desiderate installare l’estensione. È inoltre possibile creare una nuova proprietà in [!DNL Launch]. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Ulteriori informazioni sulle proprietà sono disponibili nella sezione [della pagina](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Proprietà della [!DNL Launch] documentazione.
5. Il flusso di lavoro consente di completare [!DNL Launch] l’installazione.

Per informazioni sulle opzioni di configurazione dell&#39;estensione, consultate la [pagina](https://docs.adobe.com/content/help/it-IT/launch/using/extensions-ref/adobe-extension/targetv2-extension/adobe-target-extension-v2.html) dell&#39;estensione Adobe Target v2 nella [!DNL Experience Launch] documentazione.

È inoltre possibile installare l’estensione direttamente nell’interfaccia [](https://launch.adobe.com/)Adobe Experience Platform Launch. Consultate [Aggiungere una nuova estensione](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) nella [!DNL Platform Launch] documentazione.


## Come utilizzare l&#39;estensione {#how-to-use}

Una volta installata l’estensione, potete avviare l’impostazione delle relative regole direttamente in [!DNL Platform Launch].

In [!DNL Platform Launch], potete impostare le regole per le estensioni installate per inviare i dati dell&#39;evento alla destinazione dell&#39;estensione solo in alcune situazioni. Per ulteriori informazioni sulla configurazione delle regole per le estensioni, consulta la documentazione [sulle](https://docs.adobe.com/help/it-IT/launch/using/reference/manage-resources/rules.html)regole.

## Configurare, aggiornare ed eliminare l&#39;estensione {#configure-upgrade-delete}

È possibile configurare, aggiornare ed eliminare le estensioni nell&#39; [!DNL Platform Launch] interfaccia.

>[!TIP]
>
>Se l’estensione è già installata su una delle proprietà, l’interfaccia utente CDP in tempo reale del Adobe  continua a essere visualizzata **[!UICONTROL Install]** per l’estensione. Per accedere al flusso di lavoro di installazione e configurarlo o eliminarlo, fate clic su [Installa estensione](#install-extension) [!DNL Platform Launch] .

Per aggiornare l’estensione, consultate Aggiornamento [dell’](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) estensione nella [!DNL Platform Launch] documentazione.
