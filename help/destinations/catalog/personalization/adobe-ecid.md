---
Keywords: ECID;ecid
title: Estensione del servizio Experience Cloud ID
description: L'estensione del servizio ID di Experience Cloud è una destinazione di personalizzazione in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità dell’estensione, consulta la pagina dell’estensione nell’Adobe Exchange.
exl-id: 4cc49c14-66ec-43e0-a106-70d9c3646d87
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 4%

---

# Estensione del servizio ID [!DNL Experience Cloud] {#adobe-ecid-extension}

## Panoramica {#overview}

Questa estensione implementa il servizio ID [!DNL Experience Cloud], che identifica i visitatori in tutte le soluzioni [!DNL Experience Cloud].

Il servizio ID [!DNL Experience Cloud] è un&#39;estensione di personalizzazione in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità dell&#39;estensione, consulta la [pagina dell&#39;estensione del servizio ID Experience Cloud](../../../tags/extensions/client/id-service/overview.md) nella documentazione dei tag.

Questa destinazione è un’estensione tag. Per ulteriori informazioni sul funzionamento delle estensioni tag in Platform, consulta la [panoramica sulle estensioni tag](../launch-extensions/overview.md).

![Estensione ECID Adobe](../../assets/catalog/personalization/adobe-ecid/catalog.png)

## Prerequisiti {#prerequisites}

Questa estensione è disponibile nel catalogo Destinazioni per tutti i clienti che hanno acquistato Platform.

Per utilizzare questa estensione, devi accedere ai tag in Platform. I tag sono offerti ai clienti di Adobe Experience Cloud come funzionalità inclusa a valore aggiunto. Contatta l&#39;amministratore dell&#39;organizzazione per accedere all&#39;interfaccia utente di Data Collection e chiedere di concederti l&#39;autorizzazione **[!UICONTROL manage_properties]** in modo da poter installare le estensioni.

## Installa estensione {#install-extension}

Per installare l&#39;estensione del servizio ID [!DNL Experience Cloud]:

Nell&#39;interfaccia [Platform](https://platform.adobe.com/), vai a **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**.

Seleziona l’estensione dal catalogo o utilizza la barra di ricerca.

Fai clic sulla destinazione per evidenziarla, quindi seleziona **[!UICONTROL Configura]** nella barra a destra. Se il controllo **[!UICONTROL Configure]** è disattivato, manca l&#39;autorizzazione **[!UICONTROL manage_properties]**. Consulta [Prerequisiti](#prerequisites).

Seleziona la proprietà tag in cui desideri installare l’estensione. Puoi anche creare una nuova proprietà. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Scopri le proprietà nella [documentazione sui tag](../../../tags/ui/administration/companies-and-properties.md).

Il flusso di lavoro ti porta all’interfaccia utente di Data Collection per completare l’installazione.

Per informazioni sulle opzioni di configurazione dell&#39;estensione e sul supporto per l&#39;installazione, consulta la [pagina dell&#39;estensione del servizio ID Experience Cloud](../../../tags/extensions/client/id-service/overview.md) nella documentazione dei tag.

Puoi anche installare l&#39;estensione direttamente nell&#39;[interfaccia utente di Data Collection](https://experience.adobe.com/it#/data-collection/). Per ulteriori informazioni, consulta la guida in [aggiunta di una nuova estensione](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension).

## Come utilizzare l’estensione {#how-to-use}

Dopo aver installato l&#39;estensione, puoi avviare la configurazione delle regole. Nell’interfaccia utente di Data Collection, puoi impostare regole per le estensioni installate in modo da inviare dati evento alla destinazione dell’estensione solo in determinate situazioni. Per ulteriori informazioni sulla configurazione delle regole per le estensioni, consulta la panoramica su [regole](../../../tags/ui/managing-resources/rules.md) nella documentazione dei tag.

## Configurare, aggiornare ed eliminare l’estensione {#configure-upgrade-delete}

Puoi configurare, aggiornare ed eliminare le estensioni nell’interfaccia utente di Data Collection.

>[!TIP]
>
>Se l&#39;estensione è già installata in una delle tue proprietà, nell&#39;interfaccia utente viene comunque visualizzato **[!UICONTROL Installa]** per l&#39;estensione. Avvia il flusso di lavoro di installazione come descritto in [Installa estensione](#install-extension) per configurare o eliminare l&#39;estensione.

Per aggiornare l&#39;estensione, consulta la guida al [processo di aggiornamento dell&#39;estensione](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) nella documentazione dei tag.
