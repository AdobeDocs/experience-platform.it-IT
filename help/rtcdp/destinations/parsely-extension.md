---
keywords: Parse. ly;parsely;Parsely;parse.ly;Parse.ly
title: Estensione Parse.ly Analytics
seo-title: Estensione Parse.ly Analytics
description: L'estensione Parse.ly Analytics è una destinazione di analisi in  Adobe Real-time Customer Data Platform (Piattaforma dati cliente in tempo reale). Per ulteriori informazioni sulla funzionalità di estensione, vedere la pagina di estensione in  Adobe Exchange.
seo-description: L'estensione Parse.ly Analytics è una destinazione di analisi in  Adobe Real-time Customer Data Platform (Piattaforma dati cliente in tempo reale). Per ulteriori informazioni sulla funzionalità di estensione, vedere la pagina di estensione in  Adobe Exchange.
translation-type: tm+mt
source-git-commit: 511d64d1555151a70bdb9f71e4b50ec461c8a2e7
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 5%

---


# [!DNL Parse.ly Analytics] Estensione {#parsely-analytics-extension}

## Panoramica {#overview}

[!DNL Parse.ly Analytics] aiuta più di 2.500 aziende a utilizzare i dati per comprendere il pubblico online. Questa estensione installa uno snippet JavaScript che tiene traccia del modo in cui i visitatori interagiscono con il contenuto del sito.

Parse.ly è un&#39;estensione di analisi nel  Adobe Real-time Customer Data Platform. Per ulteriori informazioni sulla funzionalità di estensione, vedi [Parse.ly Analytics](https://www.parse.ly/).

Questa destinazione è un&#39;estensione Adobe Experience Platform Launch . Per ulteriori informazioni sul funzionamento delle estensioni Platform Launch  Adobe CDP in tempo reale, consultate [panoramica](/help/rtcdp/destinations/experience-platform-launch-extensions.md)delle estensioni Adobe Experience Platform Launch.

![Estensione Parse.ly Analytics](assets/parsely-extension.png)

## Prerequisiti   {#prerequisites}

Questa estensione è disponibile nel [!DNL Destinations] catalogo per tutti i clienti che hanno acquistato  Adobe CDP in tempo reale.

Per utilizzare questa estensione, è necessario accedere a  Adobe Experience Platform Launch. Launch piattaforma è disponibile per i clienti Adobe Experience Cloud come funzione inclusa a valore aggiunto. Contatta l’amministratore dell’organizzazione per ottenere l’accesso a Platform Launch e chiedi loro di concederti l’ **[!UICONTROL manage_properties]** autorizzazione per l’installazione delle estensioni.

## Installa estensione {#install-extension}

Per installare l’ [!DNL Parse.ly] estensione:

1. Nell&#39;interfaccia CDP in tempo reale del [Adobe](http://platform.adobe.com/), passare a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.
2. Selezionate l’estensione dal catalogo o usate la barra di ricerca.
3. Fai clic sulla destinazione per evidenziarla, quindi selezionala **[!UICONTROL Configure]** nella barra a destra. Se il **[!UICONTROL Configure]** controllo è disattivato, manca l&#39; **[!UICONTROL manage_properties]** autorizzazione. Consultate [Prerequisiti](#prerequisites).
4. Nella **[!UICONTROL Select available Platform Launch property]** finestra, selezionate la proprietà Lancio piattaforma in cui desiderate installare l&#39;estensione. È inoltre possibile creare una nuova proprietà in Lancio piattaforma. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Ulteriori informazioni sulle proprietà sono disponibili nella sezione [della pagina](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Proprietà della documentazione Lancio piattaforma.
5. Il flusso di lavoro consente di passare al lancio della piattaforma per completare l’installazione.

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