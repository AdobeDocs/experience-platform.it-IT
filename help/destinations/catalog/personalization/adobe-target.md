---
keywords: estensione target;target
title: Estensione Adobe Target
description: L'estensione Adobe Target è una destinazione di personalizzazione in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità dell’estensione, consulta la pagina dell’estensione in Adobe Exchange.
exl-id: 62f8c641-7942-41d5-bd86-681c2c5efa6c
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 13%

---

# Estensione Adobe Target

## Panoramica {#overview}

Adobe Target è la soluzione di Adobe Experience Cloud che offre tutto il necessario per adattare e personalizzare l’esperienza dei clienti al fine di massimizzare le entrate sui siti web e mobili, le app, i social media e altri canali digitali.

Adobe Target è un’estensione di personalizzazione in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità dell&#39;estensione, consulta la pagina dell&#39;estensione in [Scambio Adobe](https://exchange.adobe.com/experiencecloud.details.100162.html).

Questa destinazione è un’estensione tag. Per ulteriori informazioni sul funzionamento delle estensioni dei tag in Platform, consulta [panoramica delle estensioni tag](../launch-extensions/overview.md).

![Estensione Adobe Target](../../assets/catalog/personalization/adobe-target/catalog.png)

## Prerequisiti {#prerequisites}

Questa estensione è disponibile nel [!DNL Destinations] catalogo per tutti i clienti che hanno acquistato Platform.

Per utilizzare questa estensione, è necessario accedere ai tag in Adobe Experience Platform. I tag sono offerti ai clienti di Adobe Experience Cloud come funzionalità inclusa a valore aggiunto. Contatta l’amministratore dell’organizzazione per accedere ai tag e chiedere loro di concederti il **[!UICONTROL manage_properties]** in modo da poter installare estensioni.

## Installa estensione {#install-extension}

Per installare l&#39;estensione Adobe Target:

In [Interfaccia della piattaforma](https://platform.adobe.com/), vai a **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**.

Seleziona l’estensione dal catalogo o utilizza la barra di ricerca.

Fai clic sulla destinazione per evidenziarla, quindi seleziona **[!UICONTROL Configura]** nella barra a destra. Se il **[!UICONTROL Configura]** il controllo è disattivato, manca il **[!UICONTROL manage_properties]** autorizzazione. Consulta [Prerequisiti](#prerequisites).

Seleziona la proprietà tag in cui desideri installare l’estensione. Puoi anche creare una nuova proprietà. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Scopri le proprietà in [documentazione sui tag](../../../tags/ui/administration/companies-and-properties.md).

Il flusso di lavoro ti porta all’interfaccia utente di Data Collection per completare l’installazione.

Per informazioni sulle opzioni di configurazione dell&#39;estensione, vedi [Pagina dell’estensione Adobe Target](../../../tags/extensions/client/target/overview.md) nella documentazione sui tag.

Puoi anche installare l’estensione direttamente nel [Interfaccia utente di Data Collection](https://experience.adobe.com/#/data-collection/). Consulta la guida su [aggiunta di una nuova estensione](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) per ulteriori informazioni.

## Come utilizzare l’estensione {#how-to-use}

Dopo aver installato l&#39;estensione, puoi avviare la configurazione delle regole. Nell’interfaccia utente di Data Collection, puoi impostare regole per le estensioni installate in modo da inviare dati evento alla destinazione dell’estensione solo in determinate situazioni. Per ulteriori informazioni sulla configurazione delle regole per le estensioni, consulta la panoramica su [regole](../../../tags/ui/managing-resources/rules.md) nella documentazione sui tag.

## Configurare, aggiornare ed eliminare l’estensione {#configure-upgrade-delete}

Puoi configurare, aggiornare ed eliminare le estensioni nell’interfaccia utente di Data Collection.

>[!TIP]
>
>Se l&#39;estensione è già installata in una delle tue proprietà, l&#39;interfaccia utente viene comunque visualizzata **[!UICONTROL Installa]** per l’estensione. Avvia il flusso di lavoro di installazione come descritto in [Installa estensione](#install-extension) per configurare o eliminare l’estensione.

Per aggiornare l’estensione, consulta la guida sulla [processo di aggiornamento delle estensioni](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) nella documentazione sui tag.
