---
keywords: Estensione Audience Manager DIL;audience manager di destinazione;estensione dil
title: Estensione Audience Manager DIL
description: L’estensione Audience Manager DIL è una destinazione DMP (Data Management Platform) in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, consulta la pagina dell'estensione in Adobe Exchange.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 3%

---


# Estensione Audience Manager DIL {#aam-dil-extension}

## Panoramica {#overview}

Questa è l&#39;estensione Adobe Audience Manager Data Integration Library (implementazione lato client). Nota: Questa estensione non è destinata all&#39;inoltro lato server (SSF) dei dati Adobe Analytics. Per SSF, utilizza l’estensione Adobe Analytics. Importante: A partire dalla versione 8.0, DIL dipende direttamente dal servizio [!DNL Experience Cloud] ID, versione 3.3 o successiva. Implementa sia il servizio [!DNL Experience Cloud] ID che DIL per funzionalità complete di integrazione dei dati [!DNL Audience Manager].

[!DNL Audience Manager] DIL è un’estensione Data Management Platform (DMP) in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, consulta la [pagina dell&#39;estensione di Audience Manager](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html) nella documentazione del Experience Platform Launch.

Questa destinazione è un&#39;estensione [!DNL Experience Platform Launch]. Per ulteriori informazioni sul funzionamento delle estensioni Launch in Platform, consulta [Panoramica delle estensioni di Experience Platform Launch](../launch-extensions/overview.md).

![Estensione Audience Manager DIL](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Prerequisiti {#prerequisites}

Questa estensione è disponibile nel catalogo [!DNL Destinations] per tutti i clienti che hanno acquistato Platform.

Per utilizzare questa estensione, devi accedere a [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] è offerto ai clienti Adobe Experience Cloud come funzionalità inclusa a valore aggiunto. Contatta l’amministratore dell’organizzazione per accedere a [!DNL Platform Launch] e chiedere loro di concedere l’autorizzazione **[!UICONTROL manage_properties]** in modo da poter installare le estensioni.

## Installa l&#39;estensione {#install-extension}

Per installare l&#39;estensione DIL [!DNL Audience Manager]:

Nell’ [Interfaccia piattaforma](http://platform.adobe.com/), vai a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Seleziona l’estensione dal catalogo o utilizza la barra di ricerca.

Fai clic sulla destinazione per evidenziarla, quindi seleziona **[!UICONTROL Configure]** nella barra a destra. Se il controllo **[!UICONTROL Configure]** è disabilitato, manca l&#39;autorizzazione **[!UICONTROL manage_properties]**. Consulta [Prerequisiti](#prerequisites).

Nella finestra **[!UICONTROL Select available Launch property]**, seleziona la proprietà [!DNL Launch] in cui desideri installare l&#39;estensione. Puoi anche creare una nuova proprietà in Launch. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Ulteriori informazioni sulle proprietà nella sezione [Proprietà pagina](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) della documentazione [!DNL Launch].

Il flusso di lavoro ti porta a [!DNL Launch] per completare l’installazione.

Per informazioni sulle opzioni di configurazione dell&#39;estensione, consulta la [pagina dell&#39;estensione dell&#39;Audience Manager](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html) nella documentazione [!DNL Experience Launch].

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



