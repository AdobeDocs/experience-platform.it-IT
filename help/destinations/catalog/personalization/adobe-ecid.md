---
Keywords: ECID;ecid
title: Estensione del servizio Experience Cloud ID
description: L'estensione del servizio Experience Cloud ID è una destinazione di personalizzazione in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, consulta la pagina dell'estensione in Adobe Exchange.
exl-id: 4cc49c14-66ec-43e0-a106-70d9c3646d87
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 4%

---

# [!DNL Experience Cloud] Estensione del servizio ID {#adobe-ecid-extension}

## Panoramica {#overview}

Questa estensione implementa il [!DNL Experience Cloud] Servizio ID, che identifica i visitatori in tutti [!DNL Experience Cloud] soluzioni.

[!DNL Experience Cloud] Il servizio ID è un&#39;estensione di personalizzazione in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, consulta la sezione [Pagina dell&#39;estensione del servizio Experience Cloud ID](../../../tags/extensions/client/id-service/overview.md) nella documentazione sui tag.

Questa destinazione è un&#39;estensione tag. Per ulteriori informazioni sul funzionamento delle estensioni dei tag in Platform, consulta la sezione [panoramica delle estensioni di tag](../launch-extensions/overview.md).

![Estensione Adobe ECID](../../assets/catalog/personalization/adobe-ecid/catalog.png)

## Prerequisiti {#prerequisites}

Questa estensione è disponibile nel catalogo Destinazioni per tutti i clienti che hanno acquistato Platform.

Per utilizzare questa estensione, devi accedere ai tag in Platform. I tag sono offerti ai clienti Adobe Experience Cloud come funzionalità inclusa a valore aggiunto. Contatta l’amministratore della tua organizzazione per accedere all’interfaccia utente di raccolta dati e chiedi loro di concederti il **[!UICONTROL manage_properties]** per poter installare le estensioni.

## Installa estensione {#install-extension}

Per installare [!DNL Experience Cloud] Estensione del servizio ID:

In [Interfaccia di Platform](https://platform.adobe.com/), vai a **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**.

Seleziona l’estensione dal catalogo o utilizza la barra di ricerca.

Fai clic sulla destinazione per evidenziarla, quindi seleziona **[!UICONTROL Configura]** nella barra a destra. Se la **[!UICONTROL Configura]** il controllo è disabilitato, manca il **[!UICONTROL manage_properties]** autorizzazione. Vedi [Prerequisiti](#prerequisites).

Seleziona la proprietà tag in cui desideri installare l&#39;estensione . Puoi anche creare una nuova proprietà. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Informazioni sulle proprietà in [documentazione sui tag](../../../tags/ui/administration/companies-and-properties.md).

Il flusso di lavoro ti porta all’interfaccia utente di raccolta dati per completare l’installazione.

Per informazioni sulle opzioni di configurazione dell&#39;estensione e sul supporto per l&#39;installazione, consulta la sezione [Pagina dell&#39;estensione del servizio Experience Cloud ID](../../../tags/extensions/client/id-service/overview.md) nella documentazione sui tag.

Puoi anche installare l’estensione direttamente nel [Interfaccia utente per la raccolta dati](https://experience.adobe.com/#/data-collection/). Consulta la guida su [aggiunta di una nuova estensione](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) per ulteriori informazioni.

## Come utilizzare l&#39;estensione {#how-to-use}

Dopo aver installato l&#39;estensione, puoi avviare l&#39;impostazione delle regole. Nell’interfaccia utente di raccolta dati, puoi impostare regole per le estensioni installate per inviare dati evento alla destinazione dell’estensione solo in determinate situazioni. Per ulteriori informazioni sull&#39;impostazione delle regole per le estensioni, consulta la panoramica su [regole](../../../tags/ui/managing-resources/rules.md) nella documentazione sui tag.

## Configurare, aggiornare ed eliminare l&#39;estensione {#configure-upgrade-delete}

Puoi configurare, aggiornare ed eliminare le estensioni nell’interfaccia utente Raccolta dati.

>[!TIP]
>
>Se l&#39;estensione è già installata su una delle tue proprietà, l&#39;interfaccia utente continua a visualizzare **[!UICONTROL Installa]** per l&#39;estensione . Spegnere il flusso di lavoro di installazione come descritto in [Installa estensione](#install-extension) per configurare o eliminare l&#39;estensione.

Per aggiornare l&#39;estensione, consulta la guida [processo di aggiornamento delle estensioni](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) nella documentazione sui tag.
