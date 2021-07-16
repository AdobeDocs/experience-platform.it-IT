---
keywords: estensione target;target
title: Estensione Adobe Target
description: L'estensione Adobe Target è una destinazione di personalizzazione in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, consulta la pagina dell'estensione in Adobe Exchange.
exl-id: 62f8c641-7942-41d5-bd86-681c2c5efa6c
source-git-commit: 573c13f5136a4efc3accf2838783a91ea914e949
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 12%

---

# Estensione Adobe Target

## Panoramica {#overview}

Adobe Target è la soluzione di Adobe Experience Cloud che offre tutto il necessario per adattare e personalizzare l’esperienza dei clienti al fine di massimizzare le entrate sui siti web e mobili, le app, i social media e altri canali digitali.

Adobe Target è un’estensione di personalizzazione in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, consulta la pagina dell&#39;estensione in [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100162.html).

Questa destinazione è un&#39;estensione [!DNL Adobe Experience Platform Launch]. Per ulteriori informazioni sul funzionamento delle estensioni [!DNL Platform Launch] in Platform, consulta [Panoramica delle estensioni di Experience Platform Launch](../launch-extensions/overview.md).

![Estensione Adobe Target](../../assets/catalog/personalization/adobe-target/catalog.png)

## Prerequisiti {#prerequisites}

Questa estensione è disponibile nel catalogo [!DNL Destinations] per tutti i clienti che hanno acquistato Platform.

Per utilizzare questa estensione, devi accedere a [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] è offerto ai clienti Adobe Experience Cloud come funzionalità inclusa a valore aggiunto. Contatta l’amministratore dell’organizzazione per accedere a [!DNL Platform Launch] e chiedi loro di concederti l’autorizzazione **[!UICONTROL manage_properties]** per installare le estensioni.

## Installa estensione {#install-extension}

Per installare l’estensione Adobe Target:

Nell’ [Interfaccia piattaforma](http://platform.adobe.com/), vai a **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**.

Seleziona l’estensione dal catalogo o utilizza la barra di ricerca.

Fai clic sulla destinazione per evidenziarla, quindi seleziona **[!UICONTROL Configura]** nella barra a destra. Se il controllo **[!UICONTROL Configura]** è disabilitato, manca l&#39;autorizzazione **[!UICONTROL manage_properties]**. Consulta [Prerequisiti](#prerequisites).

Nella finestra **[!UICONTROL Seleziona la proprietà del Platform launch disponibile]**, seleziona la proprietà [!DNL Platform Launch] in cui desideri installare l&#39;estensione. Puoi anche creare una nuova proprietà in [!DNL Platform Launch]. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Ulteriori informazioni sulle proprietà nella sezione [Proprietà pagina](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) della documentazione [!DNL Launch].

Il flusso di lavoro ti porta a [!DNL Platform Launch] per completare l’installazione.

Per informazioni sulle opzioni di configurazione dell&#39;estensione, consulta la [pagina dell&#39;estensione Adobe Target](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/target-extension/overview.html) nella documentazione Experience [!DNL Launch] .

Puoi anche installare l&#39;estensione direttamente nell&#39; [interfaccia Adobe Experience Platform Launch](https://launch.adobe.com/). Consulta [Aggiungi una nuova estensione](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) nella documentazione [!DNL Platform Launch] .

## Come utilizzare l&#39;estensione {#how-to-use}

Dopo aver installato l&#39;estensione, puoi avviare l&#39;impostazione delle regole per essa direttamente in [!DNL Platform Launch].

In [!DNL Platform Launch], puoi impostare regole per le estensioni installate per inviare dati evento alla destinazione dell&#39;estensione solo in determinate situazioni. Per ulteriori informazioni sull&#39;impostazione delle regole per le estensioni, consulta la [documentazione sulle regole](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Configurare, aggiornare ed eliminare l&#39;estensione {#configure-upgrade-delete}

Puoi configurare, aggiornare ed eliminare le estensioni nell&#39;interfaccia [!DNL Platform Launch] .

>[!TIP]
>
>Se l&#39;estensione è già installata su una delle tue proprietà, l&#39;interfaccia utente di Platform visualizza ancora **[!UICONTROL Install]** per l&#39;estensione. Per passare a [!DNL Platform Launch] e configurare o eliminare l&#39;estensione, fai clic sul flusso di lavoro di installazione come descritto in [Installa l&#39;estensione](#install-extension) .

Per aggiornare l&#39;estensione, consulta [Aggiornamento dell&#39;estensione](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) nella documentazione [!DNL Platform Launch] .
