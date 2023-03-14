---
keywords: gtag;google gtag;estensione google;estensione google gtag;GTAG
title: Estensione Google gtag
description: L’estensione gtag Google è una destinazione pubblicitaria in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità dell’estensione, consulta la pagina dell’estensione in Adobe Exchange.
exl-id: 14a466f2-78a0-4493-93cd-3dcdae048042
source-git-commit: c3f6650df5fabe9736e4b11a43c41ae39f014425
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 3%

---

# Estensione Google gtag {#gtag-advertising-extension}

>[!IMPORTANT]
>
>L’estensione Google gtag qui descritta è stata dichiarata obsoleta e sostituita dalla [[!DNL Google Global Site Tag (gtag)]](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) estensione sviluppata da [!DNL Acronym]. È possibile trovare [!DNL Google Global Site Tag (gtag)] estensione all&#39;interno di [[!UICONTROL Tag]](../../../tags/home.md) nell’interfaccia di Data Collection o nell’interfaccia di Experience Platform.

## Panoramica {#overview}

Carica Google `gtag.js` nel sito per inviare i dati dell’evento a [!DNL Google Analytics], Google Ads e [!DNL Google Marketing Platform]. Questa estensione aggiunge solo il codice gtag al sito. Per aggiungere eventi e azioni che utilizzeranno gtag, dovrai utilizzare altre estensioni Google.

Google gtag è un’estensione pubblicitaria in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità dell&#39;estensione, consulta la pagina dell&#39;estensione in [Scambio Adobe](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

Questa destinazione è un’estensione tag. Per ulteriori informazioni sul funzionamento delle estensioni tag in Platform, consulta [panoramica delle estensioni tag](../launch-extensions/overview.md).

![Estensione Google gtag](../../assets/catalog/advertising/gtag-advertising/catalog.png)

## Prerequisiti {#prerequisites}

Questa estensione è disponibile nel [!DNL Destinations] catalogo per tutti i clienti che hanno acquistato Platform.

Per utilizzare questa estensione, è necessario accedere ai tag in Adobe Experience Platform. I tag sono offerti ai clienti di Adobe Experience Cloud come funzionalità inclusa a valore aggiunto. Contatta l’amministratore dell’organizzazione per accedere ai tag e chiedere loro di concederti il **[!UICONTROL manage_properties]** in modo da poter installare estensioni.

## Installa estensione {#install-extension}

Per installare l’estensione Gtag Google:

In [Interfaccia della piattaforma](https://platform.adobe.com/), vai a **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**.

Seleziona l’estensione dal catalogo o utilizza la barra di ricerca.

Fai clic sulla destinazione per evidenziarla, quindi seleziona **[!UICONTROL Configura]** nella barra a destra. Se il **[!UICONTROL Configura]** il controllo è disattivato, manca il **[!UICONTROL manage_properties]** autorizzazione. Consulta [Prerequisiti](#prerequisites).

Seleziona la proprietà in cui desideri installare l’estensione. Puoi anche creare una nuova proprietà. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Scopri le proprietà in [Sezione pagina delle proprietà](../../../tags/ui/administration/companies-and-properties.md#properties-page) di nella documentazione dei tag.

Il flusso di lavoro illustra i passaggi necessari per completare l’installazione.

Per informazioni sulle opzioni di configurazione dell’estensione e sul supporto per l’installazione, consulta [Pagina Gtag Google su Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

Puoi anche installare l’estensione direttamente nel [Interfaccia utente di Data Collection](https://experience.adobe.com/#/data-collection/). Per ulteriori informazioni, consulta la sezione su [aggiunta di una nuova estensione](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) nella documentazione sui tag.

## Come utilizzare l’estensione {#how-to-use}

Dopo aver installato l&#39;estensione, puoi avviare la configurazione delle regole.

Puoi impostare regole per le estensioni installate in modo da inviare dati evento alla destinazione dell&#39;estensione solo in determinate situazioni. Per ulteriori informazioni sulla configurazione delle regole per le estensioni, vedi [documentazione sui tag](../../../tags/ui/managing-resources/rules.md).

## Configurare, aggiornare ed eliminare l’estensione {#configure-upgrade-delete}

Puoi configurare, aggiornare ed eliminare le estensioni nell’interfaccia utente di Data Collection.

>[!TIP]
>
>Se l’estensione è già installata in una delle tue proprietà, viene comunque visualizzata l’interfaccia utente di Platform **[!UICONTROL Installa]** per l’estensione. Avvia il flusso di lavoro di installazione come descritto in [Installa estensione](#install-extension) per configurare o eliminare l’estensione.

Per aggiornare l’estensione, consulta la guida sulla [processo di aggiornamento delle estensioni](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) nella documentazione sui tag.
