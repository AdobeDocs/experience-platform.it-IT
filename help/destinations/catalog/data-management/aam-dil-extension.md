---
keywords: Estensione Audience Manager DIL;audience manager di destinazione;estensione dil
title: Estensione Audience Manager DIL
description: L’estensione Audience Manager DIL è una destinazione DMP (Data Management Platform) in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, consulta la pagina dell'estensione in Adobe Exchange.
exl-id: 7e1099de-0650-4ee2-b746-721afe194097
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 3%

---

# Estensione Audience Manager DIL {#aam-dil-extension}

## Panoramica {#overview}

Questa è l&#39;estensione Adobe Audience Manager Data Integration Library (implementazione lato client). Nota: Questa estensione non è destinata all&#39;inoltro lato server (SSF) dei dati Adobe Analytics. Per SSF, utilizza l’estensione Adobe Analytics. Importante: A partire dalla versione 8.0, DIL è fortemente dipendente dalla [!DNL Experience Cloud] Servizio ID, versione 3.3 o successiva. Implementare entrambi [!DNL Experience Cloud] Servizio ID e DIL per la versione completa [!DNL Audience Manager] funzionalità di integrazione dei dati.

[!DNL Audience Manager] DIL è un’estensione Data Management Platform (DMP) in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, consulta la sezione [Pagina dell&#39;estensione di Audience Manager](../../../tags/extensions/client/audience-manager/overview.md) nella documentazione sui tag.

Questa destinazione è un&#39;estensione tag. Per ulteriori informazioni sul funzionamento delle estensioni in Platform, consulta la sezione [panoramica delle estensioni di tag](../launch-extensions/overview.md).

![Estensione Audience Manager DIL](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Prerequisiti {#prerequisites}

Questa estensione è disponibile in [!DNL Destinations] catalogo per tutti i clienti che hanno acquistato Platform.

Per utilizzare questa estensione, devi accedere ai tag in Adobe Experience Platform. I tag sono offerti ai clienti Adobe Experience Cloud come funzionalità inclusa a valore aggiunto. Contatta l’amministratore dell’organizzazione per accedere ai tag e chiedi loro di concederti il **[!UICONTROL manage_properties]** per poter installare le estensioni.

## Installa estensione {#install-extension}

Per installare [!DNL Audience Manager] Estensione DIL:

In [Interfaccia di Platform](https://platform.adobe.com/), vai a **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**.

Seleziona l’estensione dal catalogo o utilizza la barra di ricerca.

Fai clic sulla destinazione per evidenziarla, quindi seleziona **[!UICONTROL Configura]** nella barra a destra. Se la **[!UICONTROL Configura]** il controllo è disabilitato, manca il **[!UICONTROL manage_properties]** autorizzazione. Vedi [Prerequisiti](#prerequisites).

Seleziona la proprietà in cui desideri installare l&#39;estensione. Puoi anche creare una nuova proprietà. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Informazioni sulle proprietà in [documentazione sui tag](../../../tags/ui/administration/companies-and-properties.md#properties-page).

Il flusso di lavoro descrive i passaggi necessari per completare l’installazione.

Per informazioni sulle opzioni di configurazione dell&#39;estensione, vedi la [Pagina dell&#39;estensione di Audience Manager](../../../tags/extensions/client/audience-manager/overview.md) nella documentazione sui tag.

Puoi anche installare l’estensione direttamente nel [Interfaccia utente per la raccolta dati](https://experience.adobe.com/#/data-collection/). Consulta la guida su [aggiunta di una nuova estensione](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) per ulteriori informazioni.

## Come utilizzare l&#39;estensione {#how-to-use}

Dopo aver installato l&#39;estensione, puoi avviare l&#39;impostazione delle regole. Nell’interfaccia utente di raccolta dati, puoi impostare regole per le estensioni installate per inviare dati evento alla destinazione dell’estensione solo in determinate situazioni. Per ulteriori informazioni sull&#39;impostazione delle regole per le estensioni, consulta la panoramica su [regole](../../../tags/ui/managing-resources/rules.md) nella documentazione sui tag.

## Configurare, aggiornare ed eliminare l&#39;estensione {#configure-upgrade-delete}

Puoi configurare, aggiornare ed eliminare le estensioni nell’interfaccia utente Raccolta dati.

>[!TIP]
>
>Se l&#39;estensione è già installata su una delle tue proprietà, l&#39;interfaccia utente continua a visualizzare **[!UICONTROL Installa]** per l&#39;estensione . Spegnere il flusso di lavoro di installazione come descritto in [Installa estensione](#install-extension) per configurare o eliminare l&#39;estensione.

Per aggiornare l&#39;estensione, consulta la guida [processo di aggiornamento delle estensioni](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) nella documentazione sui tag.
