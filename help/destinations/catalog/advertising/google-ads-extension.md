---
keywords: Google ads;google ads;estensione google ads;estensione Google Ads
title: Estensione Google Ads
description: L'estensione Google Ads è una destinazione pubblicitaria in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità dell’estensione, consulta la pagina dell’estensione in Adobe Exchange.
exl-id: b563ce68-7b04-4cfb-b0c3-151f34ec7c1a
source-git-commit: b4e869f9bc29122db4fc66ccda752a50c7db729f
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 3%

---

# [!DNL Google Ads] Estensione

## Panoramica {#overview}

Questa estensione tiene traccia delle conversioni dagli utenti che fanno clic sul [!DNL Google Ads]. Dovrai anche installare l’estensione gtag.js e aggiungerla alla libreria, come [!DNL Google Ads] dipende da esso.

[!DNL Google Ads] è un’estensione per annunci pubblicitari in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità dell&#39;estensione, consulta la pagina dell&#39;estensione in [Scambio Adobe](https://www.adobeexchange.com/experiencecloud.details.101383.google-ads.html).

Questa destinazione è un’estensione tag. Per ulteriori informazioni sul funzionamento delle estensioni tag in Platform, consulta [panoramica delle estensioni tag](../launch-extensions/overview.md).

![Estensione Google Ads](../../assets/catalog/advertising/google-ads-extension/catalog.png)

## Prerequisiti {#prerequisites}

Questa estensione è disponibile nel catalogo Destinazioni per tutti i clienti che hanno acquistato Platform.

Per utilizzare questa estensione, è necessario accedere ai tag in Adobe Experience Platform. I tag sono offerti ai clienti di Adobe Experience Cloud come funzionalità inclusa a valore aggiunto. Contatta l’amministratore dell’organizzazione per accedere ai tag e chiedere loro di concederti il **[!UICONTROL manage_properties]** in modo da poter installare estensioni.

## Installa estensione {#install-extension}

Per installare [!DNL Google Ads] estensione:

In [Interfaccia della piattaforma](https://platform.adobe.com/), vai a **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**.

Seleziona l’estensione dal catalogo o utilizza la barra di ricerca.

Fai clic sulla destinazione per evidenziarla, quindi seleziona **[!UICONTROL Configura]** nella barra a destra. Se il **[!UICONTROL Configura]** il controllo è disattivato, manca il **[!UICONTROL manage_properties]** autorizzazione. Consulta [Prerequisiti](#prerequisites).

Seleziona la proprietà in cui desideri installare l’estensione. Puoi anche creare una nuova proprietà. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Scopri le proprietà in [Sezione pagina delle proprietà](../../../tags/ui/administration/companies-and-properties.md#properties-page) di nella documentazione dei tag.

Il flusso di lavoro illustra i passaggi necessari per completare l’installazione.

Per informazioni sulle opzioni di configurazione dell’estensione e sul supporto per l’installazione, consulta [Pagina Google Ads su Adobe Exchange](https://www.adobeexchange.com/experiencecloud.details.101383.google-ads.html).

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
