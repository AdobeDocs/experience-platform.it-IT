---
keywords: Estensione Audience Manager DIL;audience manager di destinazione;estensione dil
title: Estensione Audience Manager DIL
description: L’estensione Audience Manager DIL è una destinazione DMP (Data Management Platform) in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, consulta la pagina dell'estensione in Adobe Exchange.
exl-id: 7e1099de-0650-4ee2-b746-721afe194097
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 3%

---

# Estensione Audience Manager DIL {#aam-dil-extension}

## Panoramica {#overview}

Questa è l&#39;estensione Adobe Audience Manager Data Integration Library (implementazione lato client). Nota: Questa estensione non è destinata all&#39;inoltro lato server (SSF) dei dati Adobe Analytics. Per SSF, utilizza l’estensione Adobe Analytics. Importante: A partire dalla versione 8.0, DIL dipende direttamente dal servizio [!DNL Experience Cloud] ID, versione 3.3 o successiva. Implementa sia il servizio [!DNL Experience Cloud] ID che DIL per funzionalità complete di integrazione dei dati [!DNL Audience Manager].

[!DNL Audience Manager] DIL è un’estensione Data Management Platform (DMP) in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, consulta la [pagina dell&#39;estensione di Audience Manager](../../../tags/extensions/web/audience-manager/overview.md) nella documentazione dei tag.

Questa destinazione è un&#39;estensione tag. Per ulteriori informazioni sul funzionamento delle estensioni in Platform, consulta la [panoramica sulle estensioni dei tag](../launch-extensions/overview.md).

![Estensione Audience Manager DIL](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Prerequisiti {#prerequisites}

Questa estensione è disponibile nel catalogo [!DNL Destinations] per tutti i clienti che hanno acquistato Platform.

Per utilizzare questa estensione, devi accedere ai tag in Adobe Experience Platform. I tag sono offerti ai clienti Adobe Experience Cloud come funzionalità inclusa a valore aggiunto. Contatta l’amministratore dell’organizzazione per accedere ai tag e chiedi loro di concederti l’autorizzazione **[!UICONTROL manage_properties]** per installare le estensioni.

## Installa estensione {#install-extension}

Per installare l&#39;estensione DIL [!DNL Audience Manager]:

Nell’ [Interfaccia piattaforma](http://platform.adobe.com/), vai a **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**.

Seleziona l’estensione dal catalogo o utilizza la barra di ricerca.

Fai clic sulla destinazione per evidenziarla, quindi seleziona **[!UICONTROL Configura]** nella barra a destra. Se il controllo **[!UICONTROL Configura]** è disabilitato, manca l&#39;autorizzazione **[!UICONTROL manage_properties]**. Consulta [Prerequisiti](#prerequisites).

Seleziona la proprietà in cui desideri installare l&#39;estensione. Puoi anche creare una nuova proprietà. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Ulteriori informazioni sulle proprietà nella [documentazione tag](../../../tags/ui/administration/companies-and-properties.md#properties-page).

Il flusso di lavoro descrive i passaggi necessari per completare l’installazione.

Per informazioni sulle opzioni di configurazione dell&#39;estensione, consulta la [pagina dell&#39;estensione dell&#39;Audience Manager](../../../tags/extensions/web/audience-manager/overview.md) nella documentazione dei tag.

Puoi anche installare l’estensione direttamente nell’ [Interfaccia di raccolta dati](https://experience.adobe.com/#/data-collection/). Per ulteriori informazioni, consulta la guida sull’ [aggiunta di una nuova estensione](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) .

## Come utilizzare l&#39;estensione {#how-to-use}

Dopo aver installato l&#39;estensione, puoi avviare l&#39;impostazione delle regole. Nell’interfaccia utente di raccolta dati, puoi impostare regole per le estensioni installate per inviare dati evento alla destinazione dell’estensione solo in determinate situazioni. Per ulteriori informazioni sull&#39;impostazione delle regole per le estensioni, consulta la panoramica su [rules](../../../tags/ui/managing-resources/rules.md) nella documentazione sui tag.

## Configurare, aggiornare ed eliminare l&#39;estensione {#configure-upgrade-delete}

Puoi configurare, aggiornare ed eliminare le estensioni nell’interfaccia utente Raccolta dati.

>[!TIP]
>
>Se l&#39;estensione è già installata su una delle tue proprietà, l&#39;interfaccia utente visualizza ancora **[!UICONTROL Install]** per l&#39;estensione. Per configurare o eliminare l&#39;estensione, fai clic sul flusso di lavoro di installazione come descritto in [Installa estensione](#install-extension) .

Per aggiornare l&#39;estensione, consulta la guida al [processo di aggiornamento dell&#39;estensione](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) nella documentazione sui tag.
