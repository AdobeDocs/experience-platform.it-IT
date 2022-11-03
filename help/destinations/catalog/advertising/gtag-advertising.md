---
keywords: gtag;google gtag;estensione google;estensione google gtag;GTAG
title: Estensione tag Google
description: L'estensione tag di Google è una destinazione pubblicitaria in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, consulta la pagina dell'estensione in Adobe Exchange.
exl-id: 14a466f2-78a0-4493-93cd-3dcdae048042
source-git-commit: c3f6650df5fabe9736e4b11a43c41ae39f014425
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 3%

---

# Estensione tag Google {#gtag-advertising-extension}

>[!IMPORTANT]
>
>L’estensione tag Google descritta qui è stata deprecata e sostituita dalla [[!DNL Google Global Site Tag (gtag)]](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) estensione sviluppata da [!DNL Acronym]. È possibile trovare le [!DNL Google Global Site Tag (gtag)] all&#39;interno di [[!UICONTROL Tag]](../../../tags/home.md) nell’interfaccia utente Raccolta dati o Experience Platform.

## Panoramica {#overview}

Carica Google `gtag.js` nel tuo sito per inviare i dati dell’evento a [!DNL Google Analytics], Google Ads e [!DNL Google Marketing Platform]. Questa estensione aggiunge solo il codice tag al tuo sito. Sarà necessario utilizzare altre estensioni Google per aggiungere eventi e azioni che utilizzeranno gtag.

Google gtag è un&#39;estensione pubblicitaria in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, consulta la pagina dell&#39;estensione in [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

Questa destinazione è un&#39;estensione tag. Per ulteriori informazioni sul funzionamento delle estensioni di tag in Platform, consulta la sezione [panoramica delle estensioni di tag](../launch-extensions/overview.md).

![Estensione tag Google](../../assets/catalog/advertising/gtag-advertising/catalog.png)

## Prerequisiti {#prerequisites}

Questa estensione è disponibile in [!DNL Destinations] catalogo per tutti i clienti che hanno acquistato Platform.

Per utilizzare questa estensione, devi accedere ai tag in Adobe Experience Platform. I tag sono offerti ai clienti Adobe Experience Cloud come funzionalità inclusa a valore aggiunto. Contatta l’amministratore dell’organizzazione per accedere ai tag e chiedi loro di concederti il **[!UICONTROL manage_properties]** per poter installare le estensioni.

## Installa estensione {#install-extension}

Per installare l’estensione tag di Google:

In [Interfaccia di Platform](https://platform.adobe.com/), vai a **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**.

Seleziona l’estensione dal catalogo o utilizza la barra di ricerca.

Fai clic sulla destinazione per evidenziarla, quindi seleziona **[!UICONTROL Configura]** nella barra a destra. Se la **[!UICONTROL Configura]** il controllo è disabilitato, manca il **[!UICONTROL manage_properties]** autorizzazione. Vedi [Prerequisiti](#prerequisites).

Seleziona la proprietà in cui desideri installare l&#39;estensione. Puoi anche creare una nuova proprietà. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Informazioni sulle proprietà in [Sezione della pagina Proprietà](../../../tags/ui/administration/companies-and-properties.md#properties-page) nella documentazione dei tag di .

Il flusso di lavoro descrive i passaggi necessari per completare l’installazione.

Per informazioni sulle opzioni di configurazione dell&#39;estensione e sul supporto per l&#39;installazione, consulta la sezione [Pagina tag Google in Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

Puoi anche installare l’estensione direttamente nel [Interfaccia utente per la raccolta dati](https://experience.adobe.com/#/data-collection/). Per ulteriori informazioni, consulta la sezione su [aggiunta di una nuova estensione](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) nella documentazione sui tag.

## Come utilizzare l&#39;estensione {#how-to-use}

Dopo aver installato l&#39;estensione, puoi avviare l&#39;impostazione delle regole.

Puoi impostare regole per le estensioni installate per inviare dati evento alla destinazione dell&#39;estensione solo in determinate situazioni. Per ulteriori informazioni sull&#39;impostazione delle regole per le estensioni, consulta la sezione [documentazione sui tag](../../../tags/ui/managing-resources/rules.md).

## Configurare, aggiornare ed eliminare l&#39;estensione {#configure-upgrade-delete}

Puoi configurare, aggiornare ed eliminare le estensioni nell’interfaccia utente Raccolta dati.

>[!TIP]
>
>Se l’estensione è già installata su una delle tue proprietà, l’interfaccia utente di Platform continua a essere visualizzata **[!UICONTROL Installa]** per l&#39;estensione . Spegnere il flusso di lavoro di installazione come descritto in [Installa estensione](#install-extension) per configurare o eliminare l&#39;estensione.

Per aggiornare l&#39;estensione, consulta la guida [processo di aggiornamento delle estensioni](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) nella documentazione sui tag.
