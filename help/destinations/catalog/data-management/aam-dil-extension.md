---
keywords: estensione Audience Manager DIL;audience manager destinazione;estensione dil
title: Estensione Audience Manager DIL
description: L’estensione Audience Manager DIL è una destinazione DMP (Data Management Platform) in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità dell’estensione, consulta la pagina dell’estensione in Adobe Exchange.
exl-id: 7e1099de-0650-4ee2-b746-721afe194097
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 3%

---

# Estensione Audience Manager DIL {#aam-dil-extension}

## Panoramica {#overview}

Si tratta dell’estensione Adobe Audience Manager Data Integration Library (implementazione lato client). Nota: questa estensione non è destinata all&#39;inoltro lato server (SSF) dei dati di Adobe Analytics. Per SSF, utilizza l’estensione Adobe Analytics. Importante: a partire dalla versione 8.0, DIL ha una forte dipendenza dal [!DNL Experience Cloud] Servizio ID, versione 3.3 o successiva. Implementare entrambi [!DNL Experience Cloud] Servizio ID e DIL per una gamma completa [!DNL Audience Manager] funzionalità di integrazione dei dati.

[!DNL Audience Manager] DIL è un’estensione di Data Management Platform (DMP) in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità dell&#39;estensione, vedi [Pagina dell’estensione di Audience Manager](../../../tags/extensions/client/audience-manager/overview.md) nella documentazione sui tag.

Questa destinazione è un’estensione tag. Per ulteriori informazioni sul funzionamento delle estensioni in Platform, consulta [panoramica delle estensioni tag](../launch-extensions/overview.md).

![Estensione Audience Manager DIL](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Prerequisiti {#prerequisites}

Questa estensione è disponibile nel [!DNL Destinations] catalogo per tutti i clienti che hanno acquistato Platform.

Per utilizzare questa estensione, è necessario accedere ai tag in Adobe Experience Platform. I tag sono offerti ai clienti di Adobe Experience Cloud come funzionalità inclusa a valore aggiunto. Contatta l’amministratore dell’organizzazione per accedere ai tag e chiedere loro di concederti il **[!UICONTROL manage_properties]** in modo da poter installare estensioni.

## Installa estensione {#install-extension}

Per installare [!DNL Audience Manager] Estensione DIL:

In [Interfaccia della piattaforma](https://platform.adobe.com/), vai a **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**.

Seleziona l’estensione dal catalogo o utilizza la barra di ricerca.

Fai clic sulla destinazione per evidenziarla, quindi seleziona **[!UICONTROL Configura]** nella barra a destra. Se il **[!UICONTROL Configura]** il controllo è disattivato, manca il **[!UICONTROL manage_properties]** autorizzazione. Consulta [Prerequisiti](#prerequisites).

Seleziona la proprietà in cui desideri installare l’estensione. Puoi anche creare una nuova proprietà. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Scopri le proprietà in [documentazione sui tag](../../../tags/ui/administration/companies-and-properties.md#properties-page).

Il flusso di lavoro illustra i passaggi necessari per completare l’installazione.

Per informazioni sulle opzioni di configurazione dell&#39;estensione, vedi [Pagina dell’estensione di Audience Manager](../../../tags/extensions/client/audience-manager/overview.md) nella documentazione sui tag.

Puoi anche installare l’estensione direttamente nel [Interfaccia utente di Data Collection](https://experience.adobe.com/#/data-collection/). Consulta la guida su [aggiunta di una nuova estensione](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) per ulteriori informazioni.

## Come utilizzare l’estensione {#how-to-use}

Dopo aver installato l&#39;estensione, puoi avviare la configurazione delle regole. Nell’interfaccia utente di Data Collection, puoi impostare regole per le estensioni installate in modo da inviare dati evento alla destinazione dell’estensione solo in determinate situazioni. Per ulteriori informazioni sulla configurazione delle regole per le estensioni, consulta la panoramica su [regole](../../../tags/ui/managing-resources/rules.md) nella documentazione sui tag.

## Configurare, aggiornare ed eliminare l’estensione {#configure-upgrade-delete}

Puoi configurare, aggiornare ed eliminare le estensioni nell’interfaccia utente di Data Collection.

>[!TIP]
>
>Se l&#39;estensione è già installata in una delle tue proprietà, l&#39;interfaccia utente viene comunque visualizzata **[!UICONTROL Installa]** per l’estensione. Avvia il flusso di lavoro di installazione come descritto in [Installa estensione](#install-extension) per configurare o eliminare l’estensione.

Per aggiornare l’estensione, consulta la guida sulla [processo di aggiornamento delle estensioni](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) nella documentazione sui tag.
