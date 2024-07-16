---
keywords: gtag;google gtag;estensione google;estensione google gtag;GTAG
title: Estensione Google gtag
description: L’estensione gtag Google è una destinazione pubblicitaria in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità dell’estensione, consulta la pagina dell’estensione nell’Adobe Exchange.
exl-id: 14a466f2-78a0-4493-93cd-3dcdae048042
source-git-commit: c3f6650df5fabe9736e4b11a43c41ae39f014425
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 3%

---

# Estensione Google gtag {#gtag-advertising-extension}

>[!IMPORTANT]
>
>L&#39;estensione Gtag Google descritta qui è stata rimossa e sostituita dall&#39;estensione [[!DNL Google Global Site Tag (gtag)]](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) sviluppata da [!DNL Acronym]. Puoi trovare l&#39;estensione [!DNL Google Global Site Tag (gtag)] nell&#39;area di lavoro [[!UICONTROL Tag]](../../../tags/home.md) nell&#39;interfaccia utente di Data Collection o nell&#39;interfaccia utente di Experience Platform.

## Panoramica {#overview}

Carica `gtag.js` di Google nel tuo sito per inviare i dati evento a [!DNL Google Analytics], Google Ads e [!DNL Google Marketing Platform]. Questa estensione aggiunge solo il codice gtag al sito. Per aggiungere eventi e azioni che utilizzeranno gtag, dovrai utilizzare altre estensioni Google.

Google gtag è un’estensione pubblicitaria in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità dell&#39;estensione, vedere la pagina dell&#39;estensione nell&#39;[Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

Questa destinazione è un’estensione tag. Per ulteriori informazioni sul funzionamento delle estensioni tag in Platform, consulta la [panoramica sulle estensioni tag](../launch-extensions/overview.md).

![Estensione Gtag Google](../../assets/catalog/advertising/gtag-advertising/catalog.png)

## Prerequisiti {#prerequisites}

Questa estensione è disponibile nel catalogo [!DNL Destinations] per tutti i clienti che hanno acquistato Platform.

Per utilizzare questa estensione, è necessario accedere ai tag in Adobe Experience Platform. I tag sono offerti ai clienti di Adobe Experience Cloud come funzionalità inclusa a valore aggiunto. Contatta l&#39;amministratore dell&#39;organizzazione per ottenere l&#39;accesso ai tag e chiedi loro di concederti l&#39;autorizzazione **[!UICONTROL manage_properties]** in modo da poter installare le estensioni.

## Installa estensione {#install-extension}

Per installare l’estensione Gtag Google:

Nell&#39;interfaccia [Platform](https://platform.adobe.com/), vai a **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**.

Seleziona l’estensione dal catalogo o utilizza la barra di ricerca.

Fai clic sulla destinazione per evidenziarla, quindi seleziona **[!UICONTROL Configura]** nella barra a destra. Se il controllo **[!UICONTROL Configure]** è disattivato, manca l&#39;autorizzazione **[!UICONTROL manage_properties]**. Consulta [Prerequisiti](#prerequisites).

Seleziona la proprietà in cui desideri installare l’estensione. Puoi anche creare una nuova proprietà. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Scopri le proprietà nella sezione [Proprietà](../../../tags/ui/administration/companies-and-properties.md#properties-page) della documentazione dei tag.

Il flusso di lavoro illustra i passaggi necessari per completare l’installazione.

Per informazioni sulle opzioni di configurazione dell&#39;estensione e sul supporto per l&#39;installazione, consulta la pagina Gtag [Google nell&#39;Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

Puoi anche installare l&#39;estensione direttamente nell&#39;[interfaccia utente di Data Collection](https://experience.adobe.com/it#/data-collection/). Per ulteriori informazioni, vedere la sezione relativa all&#39;[aggiunta di una nuova estensione](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) nella documentazione dei tag.

## Come utilizzare l’estensione {#how-to-use}

Dopo aver installato l&#39;estensione, puoi avviare la configurazione delle regole.

Puoi impostare regole per le estensioni installate in modo da inviare dati evento alla destinazione dell&#39;estensione solo in determinate situazioni. Per ulteriori informazioni sulla configurazione delle regole per le estensioni, consulta la [documentazione sui tag](../../../tags/ui/managing-resources/rules.md).

## Configurare, aggiornare ed eliminare l’estensione {#configure-upgrade-delete}

Puoi configurare, aggiornare ed eliminare le estensioni nell’interfaccia utente di Data Collection.

>[!TIP]
>
>Se l&#39;estensione è già installata in una delle tue proprietà, nell&#39;interfaccia utente di Platform verrà comunque visualizzato **[!UICONTROL Installa]** per l&#39;estensione. Avvia il flusso di lavoro di installazione come descritto in [Installa estensione](#install-extension) per configurare o eliminare l&#39;estensione.

Per aggiornare l&#39;estensione, consulta la guida al [processo di aggiornamento dell&#39;estensione](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) nella documentazione dei tag.
