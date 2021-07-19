---
keywords: gtag;google gtag;estensione google;estensione google gtag;GTAG
title: Estensione Google Gtag
description: L'estensione Google gtag è una destinazione pubblicitaria in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, consulta la pagina dell'estensione in Adobe Exchange.
exl-id: 14a466f2-78a0-4493-93cd-3dcdae048042
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 3%

---

# Estensione Google Gtag {#gtag-advertising-extension}

## Panoramica {#overview}

Carica `gtag.js` di Google nel tuo sito per inviare dati evento a [!DNL Google Analytics], Google Ads e [!DNL Google Marketing Platform]. Questa estensione aggiunge solo il codice tag al tuo sito. Sarà necessario utilizzare altre estensioni Google per aggiungere eventi e azioni che utilizzeranno gtag.

Google gtag è un&#39;estensione pubblicitaria in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, consulta la pagina dell&#39;estensione in [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

Questa destinazione è un&#39;estensione Adobe Experience Platform Launch. Per ulteriori informazioni sul funzionamento delle estensioni di Platform launch in Platform, consulta [Panoramica delle estensioni Adobe Experience Platform Launch](../launch-extensions/overview.md).

![Estensione Google Gtag](../../assets/catalog/advertising/gtag-advertising/catalog.png)

## Prerequisiti {#prerequisites}

Questa estensione è disponibile nel catalogo [!DNL Destinations] per tutti i clienti che hanno acquistato Platform.

Per utilizzare questa estensione, devi accedere ad Adobe Experience Platform Launch. Il platform launch è offerto ai clienti Adobe Experience Cloud come funzionalità inclusa a valore aggiunto. Contatta l&#39;amministratore dell&#39;organizzazione per accedere al Platform launch e chiedi loro di concederti l&#39;autorizzazione **[!UICONTROL manage_properties]** per poter installare le estensioni.

## Installa estensione {#install-extension}

Per installare l’estensione Google Gtag:

Nell’ [Interfaccia piattaforma](http://platform.adobe.com/), vai a **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**.

Seleziona l’estensione dal catalogo o utilizza la barra di ricerca.

Fai clic sulla destinazione per evidenziarla, quindi seleziona **[!UICONTROL Configura]** nella barra a destra. Se il controllo **[!UICONTROL Configura]** è disabilitato, manca l&#39;autorizzazione **[!UICONTROL manage_properties]**. Consulta [Prerequisiti](#prerequisites).

Nella finestra **[!UICONTROL Seleziona la proprietà del Platform launch disponibile]**, seleziona la proprietà del Platform launch in cui desideri installare l&#39;estensione. È inoltre possibile creare una nuova proprietà in Platform launch. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Scopri le proprietà nella sezione [Proprietà pagina](../../../tags/ui/administration/companies-and-properties.md#properties-page) della documentazione del Platform launch.

Il flusso di lavoro ti porta al Platform launch per completare l’installazione.

Per informazioni sulle opzioni di configurazione dell&#39;estensione e sul supporto dell&#39;installazione, consulta la pagina [Google gtag sull&#39;Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

Puoi anche installare l&#39;estensione direttamente nell&#39; [interfaccia Adobe Experience Platform Launch](https://launch.adobe.com/). Consulta [Aggiungi una nuova estensione](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) nella documentazione del Platform launch.

## Come utilizzare l&#39;estensione {#how-to-use}

Una volta installata l&#39;estensione, puoi avviare l&#39;impostazione delle regole per essa direttamente nel Platform launch.

Al Platform launch, puoi impostare regole per le estensioni installate per inviare dati evento alla destinazione dell&#39;estensione solo in determinate situazioni. Per ulteriori informazioni sull&#39;impostazione delle regole per le estensioni, consulta la [documentazione sulle regole](../../../tags/ui/managing-resources/rules.md).

## Configurare, aggiornare ed eliminare l&#39;estensione {#configure-upgrade-delete}

Puoi configurare, aggiornare ed eliminare le estensioni nell’interfaccia di Platform launch.

>[!TIP]
>
>Se l&#39;estensione è già installata su una delle tue proprietà, l&#39;interfaccia utente di Platform visualizza ancora **[!UICONTROL Install]** per l&#39;estensione. Per accedere al Platform launch e configurare o eliminare l&#39;estensione, fai clic sul flusso di lavoro di installazione come descritto in [Installa estensione](#install-extension) .

Per aggiornare l&#39;estensione, consulta [Aggiornamento dell&#39;estensione](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) nella documentazione del Platform launch.
