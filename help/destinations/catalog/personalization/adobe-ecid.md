---
Keywords: ECID;ecid
title: Estensione del servizio Experience Cloud ID
description: L'estensione del servizio Experience Cloud ID è una destinazione di personalizzazione in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, consulta la pagina dell'estensione in Adobe Exchange.
exl-id: 4cc49c14-66ec-43e0-a106-70d9c3646d87
source-git-commit: c8d6c156b3351324fe1be11144afeae91f7a2a59
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 4%

---

# [!DNL Experience Cloud] Estensione del servizio ID {#adobe-ecid-extension}

## Panoramica {#overview}

Questa estensione implementa il servizio [!DNL Experience Cloud] ID , che identifica i visitatori in tutte le soluzioni [!DNL Experience Cloud] .

[!DNL Experience Cloud] Il servizio ID è un&#39;estensione di personalizzazione in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, consulta la [pagina dell&#39;estensione del servizio ID di Experience Cloud](../../../tags/extensions/web/id-service/overview.md) nella documentazione dei tag.

Questa destinazione è un&#39;estensione tag. Per ulteriori informazioni sul funzionamento delle estensioni dei tag in Platform, consulta la [panoramica sulle estensioni dei tag](../launch-extensions/overview.md).

![Estensione Adobe ECID](../../assets/catalog/personalization/adobe-ecid/catalog.png)

## Prerequisiti {#prerequisites}

Questa estensione è disponibile nel catalogo Destinazioni per tutti i clienti che hanno acquistato Platform.

Per utilizzare questa estensione, devi accedere ai tag in Platform. I tag sono offerti ai clienti Adobe Experience Cloud come funzionalità inclusa a valore aggiunto. Contatta l’amministratore dell’organizzazione per accedere all’interfaccia utente di raccolta dati e chiedi di concederti l’autorizzazione **[!UICONTROL manage_properties]** per installare le estensioni.

## Installa estensione {#install-extension}

Per installare l&#39;estensione del servizio ID [!DNL Experience Cloud]:

Nell’ [Interfaccia piattaforma](https://platform.adobe.com/), vai a **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**.

Seleziona l’estensione dal catalogo o utilizza la barra di ricerca.

Fai clic sulla destinazione per evidenziarla, quindi seleziona **[!UICONTROL Configura]** nella barra a destra. Se il controllo **[!UICONTROL Configura]** è disabilitato, manca l&#39;autorizzazione **[!UICONTROL manage_properties]**. Consulta [Prerequisiti](#prerequisites).

Seleziona la proprietà tag in cui desideri installare l&#39;estensione . Puoi anche creare una nuova proprietà. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Ulteriori informazioni sulle proprietà nella [documentazione tag](../../../tags/ui/administration/companies-and-properties.md).

Il flusso di lavoro ti porta all’interfaccia utente di raccolta dati per completare l’installazione.

Per informazioni sulle opzioni di configurazione dell&#39;estensione e sul supporto per l&#39;installazione, consulta la [pagina dell&#39;estensione del servizio ID di Experience Cloud](../../../tags/extensions/web/id-service/overview.md) nella documentazione dei tag.

Puoi anche installare l’estensione direttamente nell’ [Interfaccia di raccolta dati](https://experience.adobe.com/#/data-collection/). Per ulteriori informazioni, consulta la guida sull’ [aggiunta di una nuova estensione](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) .

## Come utilizzare l&#39;estensione {#how-to-use}

Dopo aver installato l&#39;estensione, puoi avviare l&#39;impostazione delle regole. Nell’interfaccia utente di raccolta dati, puoi impostare regole per le estensioni installate per inviare dati evento alla destinazione dell’estensione solo in determinate situazioni. Per ulteriori informazioni sull&#39;impostazione delle regole per le estensioni, consulta la panoramica su [rules](../../../tags/ui/managing-resources/rules.md) nella documentazione sui tag.

## Configurare, aggiornare ed eliminare l&#39;estensione {#configure-upgrade-delete}

Puoi configurare, aggiornare ed eliminare le estensioni nell’interfaccia utente Raccolta dati.

>[!TIP]
>
>Se l&#39;estensione è già installata su una delle tue proprietà, l&#39;interfaccia utente visualizza ancora **[!UICONTROL Install]** per l&#39;estensione. Per configurare o eliminare l&#39;estensione, fai clic sul flusso di lavoro di installazione come descritto in [Installa estensione](#install-extension) .

Per aggiornare l&#39;estensione, consulta la guida al [processo di aggiornamento dell&#39;estensione](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) nella documentazione sui tag.
