---
keywords: Personalizzazione Web Marketo;marketing per la personalizzazione Web;Estensione Personalizzazione Web Marketo;marketing per l'estensione della personalizzazione Web;marketo;Marketo
title: Estensione Marketo Web Personalization
seo-title: Estensione Marketo Web Personalization
description: L’estensione Marketing Web Personalization (Personalizzazione Web Marketo) è una destinazione di personalizzazione in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, vedere la pagina di estensione in  Adobe Exchange.
seo-description: L’estensione Marketing Web Personalization (Personalizzazione Web Marketo) è una destinazione di personalizzazione in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, vedere la pagina di estensione in  Adobe Exchange.
translation-type: tm+mt
source-git-commit: 7aadb4b7e7c36b659490d155ad4cfa7ef0a24306
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 3%

---


# [!DNL Marketo Web Personalization] Estensione {#marketo-web-personalization-extension}

## Panoramica {#overview}

Questa estensione distribuisce lo script per le applicazioni [!DNL Marketo’s] Web Personalization e ContentAI. [!DNL Marketo] Web Personalization identifica e personalizza in modo univoco il contenuto in base alle caratteristiche dei visitatori Web, come la grafica per i visitatori anonimi e un&#39;ampia gamma di attributi comportamentali all&#39;interno della piattaforma  [!DNL Marketo] di coinvolgimento per i visitatori noti. [!DNL Marketo] ContentAI contiene funzionalità per le raccomandazioni basate sull&#39;intelligenza artificiale e la personalizzazione per le campagne Web ed e-mail che sono uniche per i clienti B2B.

[!DNL Marketo Web Personalization] è un’estensione di personalizzazione in Adobe Experience Platform. Per ulteriori informazioni sulla funzionalità di estensione, vedere la pagina dell&#39;estensione in [ Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101232.marketo-web-personalization.html).

Questa destinazione è un&#39;estensione Adobe Experience Platform Launch . Per ulteriori informazioni sul funzionamento delle estensioni Platform Launch in Platform, vedere [ panoramica delle estensioni Adobe Experience Platform Launch](../launch-extensions/overview.md).

![Estensione Marketo Web Personalization](../../assets/catalog/personalization/marketo-web-personalization/catalog.png)

## Prerequisiti {#prerequisites}

Questa estensione è disponibile nel catalogo [!DNL Destinations] per tutti i clienti che hanno acquistato la piattaforma.

Per utilizzare questa estensione, è necessario accedere a  Adobe Experience Platform Launch. Launch piattaforma è disponibile per i clienti Adobe Experience Cloud come funzione inclusa a valore aggiunto. Contattate l&#39;amministratore dell&#39;organizzazione per ottenere l&#39;accesso a Platform Launch e chiedete loro di concedere l&#39;autorizzazione **[!UICONTROL manage_properties]** in modo da poter installare le estensioni.

## Installare l&#39;estensione {#install-extension}

Per installare l&#39;estensione [!DNL Marketo Web Personalization]:

Nell&#39;interfaccia [Piattaforma](http://platform.adobe.com/), passare a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Selezionate l’estensione dal catalogo o usate la barra di ricerca.

Fare clic sulla destinazione per evidenziarla, quindi selezionare **[!UICONTROL Configure]** nella barra a destra. Se il controllo **[!UICONTROL Configure]** è disattivato, manca l&#39;autorizzazione **[!UICONTROL manage_properties]**. Vedere [Prerequisiti](#prerequisites).

Nella finestra **[!UICONTROL Select available Platform Launch property]**, selezionate la proprietà Lancio piattaforma in cui desiderate installare l&#39;estensione. È inoltre possibile creare una nuova proprietà in Lancio piattaforma. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Ulteriori informazioni sulle proprietà nella sezione [Proprietà della pagina](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) della documentazione di Launch piattaforma.

Il flusso di lavoro consente di passare al lancio della piattaforma per completare l’installazione.

Per informazioni sulle opzioni di configurazione dell&#39;estensione e sul supporto dell&#39;installazione, vedere la pagina [Marketing Web Personalization (Personalizzazione Web marketing) in  Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101232.marketo-web-personalization.html).

È inoltre possibile installare l&#39;estensione direttamente nell&#39; [ interfaccia Adobe Experience Platform Launch](https://launch.adobe.com/). Consultate [Aggiungere una nuova estensione](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) nella documentazione di Launch piattaforma.

## Come utilizzare l&#39;estensione {#how-to-use}

Una volta installata l’estensione, potete avviare la configurazione delle relative regole direttamente in Launch piattaforma.

In Avvio piattaforma, potete impostare le regole per le estensioni installate per inviare i dati dell&#39;evento alla destinazione dell&#39;estensione solo in alcune situazioni. Per ulteriori informazioni sull&#39;impostazione delle regole per le estensioni, vedere la [documentazione sulle regole](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Configurare, aggiornare ed eliminare l&#39;estensione {#configure-upgrade-delete}

Puoi configurare, aggiornare ed eliminare le estensioni nell&#39;interfaccia Launch piattaforma.

>[!TIP]
>
>Se l&#39;estensione è già installata su una delle proprietà, l&#39;interfaccia utente della piattaforma continua a visualizzare **[!UICONTROL Install]** per l&#39;estensione. Per accedere al lancio della piattaforma e configurare o eliminare l&#39;estensione, selezionate il flusso di lavoro di installazione come descritto in [Installa estensione](#install-extension).

Per aggiornare l&#39;estensione, consultare [Aggiornamento dell&#39;estensione](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) nella documentazione di Launch piattaforma.