---
keywords: estensione target;target
title: Estensione Adobe Target
seo-title: Estensione Adobe Target
description: L’estensione Adobe Target  è una destinazione di personalizzazione in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, vedere la pagina di estensione in  Adobe Exchange.
seo-description: L’estensione Adobe Target  è una destinazione di personalizzazione in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, vedere la pagina di estensione in  Adobe Exchange.
translation-type: tm+mt
source-git-commit: 7aadb4b7e7c36b659490d155ad4cfa7ef0a24306
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 12%

---


# Estensione Adobe Target {#adobe-target-extension}

## Panoramica {#overview}

Adobe Target è la soluzione di Adobe Experience Cloud che offre tutto il necessario per adattare e personalizzare l’esperienza dei clienti al fine di massimizzare le entrate sui siti web e mobili, le app, i social media e altri canali digitali.

 Adobe Target è un’estensione di personalizzazione in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, vedere la pagina dell&#39;estensione in [ Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100162.html).

Questa destinazione è un&#39;estensione [!DNL Adobe Experience Platform Launch]. Per ulteriori informazioni sul funzionamento delle [!DNL Platform Launch] estensioni in Piattaforma, vedere [Panoramica sulle estensioni di Experience Platform Launch](../launch-extensions/overview.md).

![Estensione Adobe Target](../../assets/catalog/personalization/adobe-target/catalog.png)

## Prerequisiti {#prerequisites}

Questa estensione è disponibile nel catalogo [!DNL Destinations] per tutti i clienti che hanno acquistato la piattaforma.

Per utilizzare questa estensione, è necessario accedere a [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] viene offerta ai clienti Adobe Experience Cloud come funzione inclusa a valore aggiunto. Contattate l&#39;amministratore dell&#39;organizzazione per ottenere l&#39;accesso a [!DNL Platform Launch] e chiedete loro di concedervi l&#39;autorizzazione **[!UICONTROL manage_properties]** in modo da poter installare le estensioni.

## Installare l&#39;estensione {#install-extension}

Per installare l&#39;estensione Adobe Target :

Nell&#39;interfaccia [Piattaforma](http://platform.adobe.com/), passare a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Selezionate l’estensione dal catalogo o usate la barra di ricerca.

Fare clic sulla destinazione per evidenziarla, quindi selezionare **[!UICONTROL Configure]** nella barra a destra. Se il controllo **[!UICONTROL Configure]** è disattivato, manca l&#39;autorizzazione **[!UICONTROL manage_properties]**. Vedere [Prerequisiti](#prerequisites).

Nella finestra **[!UICONTROL Select available Platform Launch property]**, selezionate la proprietà [!DNL Platform Launch] in cui desiderate installare l&#39;estensione. È inoltre possibile creare una nuova proprietà in [!DNL Platform Launch]. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Ulteriori informazioni sulle proprietà nella sezione [Proprietà pagina](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) della documentazione [!DNL Launch].

Il flusso di lavoro porta a [!DNL Platform Launch] per completare l&#39;installazione.

Per informazioni sulle opzioni di configurazione dell&#39;estensione, consultate la sezione [ pagina dell&#39;estensione Adobe Target](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/target-extension/overview.html) nella documentazione relativa all&#39;esperienza [!DNL Launch].

È inoltre possibile installare l&#39;estensione direttamente nell&#39; [ interfaccia Adobe Experience Platform Launch](https://launch.adobe.com/). Vedere [Aggiungere una nuova estensione](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) nella documentazione di [!DNL Platform Launch].

## Come utilizzare l&#39;estensione {#how-to-use}

Una volta installata l&#39;estensione, potete avviare l&#39;impostazione delle relative regole direttamente in [!DNL Platform Launch].

In [!DNL Platform Launch], potete impostare le regole per le estensioni installate per inviare i dati dell&#39;evento alla destinazione dell&#39;estensione solo in alcune situazioni. Per ulteriori informazioni sull&#39;impostazione delle regole per le estensioni, vedere la [documentazione sulle regole](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Configurare, aggiornare ed eliminare l&#39;estensione {#configure-upgrade-delete}

È possibile configurare, aggiornare ed eliminare le estensioni nell&#39;interfaccia [!DNL Platform Launch].

>[!TIP]
>
>Se l&#39;estensione è già installata su una delle proprietà, l&#39;interfaccia utente della piattaforma continua a visualizzare **[!UICONTROL Install]** per l&#39;estensione. Per accedere a [!DNL Platform Launch] e configurare o eliminare l&#39;estensione, selezionate il flusso di lavoro di installazione come descritto in [Installa estensione](#install-extension).

Per aggiornare l&#39;estensione, vedere [Aggiornamento dell&#39;estensione](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) nella documentazione di [!DNL Platform Launch].
