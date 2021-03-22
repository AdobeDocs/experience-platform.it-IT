---
Keywords: ECID;ecid
title: Estensione del servizio Experience Cloud ID
description: L'estensione del servizio Experience Cloud ID è una destinazione di personalizzazione in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, consulta la pagina dell'estensione in Adobe Exchange.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 4%

---


# [!DNL Experience Cloud] Estensione del servizio ID  {#adobe-ecid-extension}

## Panoramica {#overview}

Questa estensione implementa il servizio [!DNL Experience Cloud] ID , che identifica i visitatori in tutte le soluzioni [!DNL Experience Cloud] .

[!DNL Experience Cloud] Il servizio ID è un&#39;estensione di personalizzazione in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, consulta la [pagina di estensione del servizio ID di Experience Cloud](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html) nella documentazione [!DNL Experience Platform Launch] .

Questa destinazione è un&#39;estensione [!DNL Adobe Experience Platform Launch]. Per ulteriori informazioni sul funzionamento delle estensioni [!DNL Platform Launch] in Platform, consulta [Panoramica delle estensioni di Experience Platform Launch](../launch-extensions/overview.md).

![Estensione Adobe ECID](../../assets/catalog/personalization/adobe-ecid/catalog.png)

## Prerequisiti {#prerequisites}

Questa estensione è disponibile nel catalogo Destinazioni per tutti i clienti che hanno acquistato Platform.

Per utilizzare questa estensione, devi accedere a [!DNL Experience Platform Launch]. [!DNL Experience Platform Launch] è offerto ai clienti Adobe Experience Cloud come funzionalità inclusa a valore aggiunto. Contatta l’amministratore dell’organizzazione per accedere a [!DNL Launch] e chiedere loro di concedere l’autorizzazione **[!UICONTROL manage_properties]** in modo da poter installare le estensioni.

## Installa l&#39;estensione {#install-extension}

Per installare l&#39;estensione del servizio ID [!DNL Experience Cloud]:

Nell’ [Interfaccia piattaforma](http://platform.adobe.com/), vai a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Seleziona l’estensione dal catalogo o utilizza la barra di ricerca.

Fai clic sulla destinazione per evidenziarla, quindi seleziona **[!UICONTROL Configure]** nella barra a destra. Se il controllo **[!UICONTROL Configure]** è disabilitato, manca l&#39;autorizzazione **[!UICONTROL manage_properties]**. Consulta [Prerequisiti](#prerequisites).

Nella finestra **[!UICONTROL Select available Platform Launch property]**, seleziona la proprietà [!DNL Platform Launch] in cui desideri installare l&#39;estensione. Puoi anche creare una nuova proprietà in [!DNL Platform Launch]. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Ulteriori informazioni sulle proprietà nella sezione [Proprietà pagina](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) della documentazione [!DNL Launch].

Il flusso di lavoro ti porta a [!DNL Platform Launch] per completare l’installazione.

Per informazioni sulle opzioni di configurazione dell&#39;estensione e sul supporto per l&#39;installazione, consulta la [pagina dell&#39;estensione del servizio ID di Experience Cloud](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html) nella documentazione [!DNL Experience Launch] .

Puoi anche installare l&#39;estensione direttamente nell&#39; [interfaccia Adobe Experience Platform Launch](https://launch.adobe.com/). Consulta [Aggiungi una nuova estensione](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) nella documentazione [!DNL Platform Launch] .

## Come utilizzare l&#39;estensione {#how-to-use}

Dopo aver installato l&#39;estensione, puoi avviare l&#39;impostazione delle regole per essa direttamente in [!DNL Platform Launch].

In [!DNL Platform Launch], puoi impostare regole per le estensioni installate per inviare dati evento alla destinazione dell&#39;estensione solo in determinate situazioni. Per ulteriori informazioni sull&#39;impostazione delle regole per le estensioni, consulta la [documentazione sulle regole](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Configura, aggiorna ed elimina l&#39;estensione {#configure-upgrade-delete}

Puoi configurare, aggiornare ed eliminare le estensioni nell&#39;interfaccia [!DNL Platform Launch] .

>[!TIP]
>
>Se l’estensione è già installata su una delle tue proprietà, l’interfaccia utente di Platform visualizza ancora **[!UICONTROL Install]** per l’estensione. Per passare a [!DNL Platform Launch] e configurare o eliminare l&#39;estensione, fai clic sul flusso di lavoro di installazione come descritto in [Installa l&#39;estensione](#install-extension) .

Per aggiornare l&#39;estensione, consulta [Aggiornamento dell&#39;estensione](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) nella documentazione [!DNL Platform Launch] .