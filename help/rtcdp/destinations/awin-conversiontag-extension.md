---
keywords: Awin Advertiser Conversion Tag extension;conversion tag;Awin;awin;AWIN
title: Estensione Tag di conversione dell'inserzionista Awin
seo-title: Estensione Tag di conversione dell'inserzionista Awin
description: L'estensione Awin Advertiser Conversion Tag è una destinazione pubblicitaria nella Real-time Customer Data Platform. Per ulteriori informazioni sulla funzionalità di estensione, vedere la pagina di estensione in  Adobe Exchange.
seo-description: L'estensione Awin Advertiser Conversion Tag è una destinazione pubblicitaria nella Real-time Customer Data Platform. Per ulteriori informazioni sulla funzionalità di estensione, vedere la pagina di estensione in  Adobe Exchange.
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 4%

---


# Estensione Tag di conversione dell&#39;inserzionista Awin {#awin-conversiontag-extension}

## Panoramica {#overview}

Il Tag Conversion è la dichiarazione dell&#39;oggetto JavaScript AWIN.Tracking.Sale, che viene eseguita nella pagina di conferma per indicare al tag Mastertag che è stata eseguita una conversione. In seguito, eseguirà le richieste di tracciamento necessarie.

Il tag Conversione inserzionista Awin è un&#39;estensione pubblicitaria nella piattaforma dati cliente in tempo reale. Per ulteriori informazioni sulla funzionalità di estensione, consultate la pagina dell&#39;estensione in [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103240.awin-conversion-tag.html).

Questa destinazione è un&#39; [!DNL Adobe Experience Platform Launch] estensione. Per ulteriori informazioni sul funzionamento [!DNL Platform Launch] delle estensioni  Adobe CDP in tempo reale, consultate Panoramica sulle estensioni [di Experience Platform Launch](/help/rtcdp/destinations/experience-platform-launch-extensions.md).

![Estensione Awin Advertiser Conversiontag nell’interfaccia utente](/help/rtcdp/destinations/assets/awin-conversiontag-extension.png)

## Prerequisiti   {#prerequisites}

Questa estensione è disponibile nel catalogo Destinazioni per tutti i clienti che hanno acquistato  CDP in tempo reale Adobe.

Per utilizzare questa estensione, è necessario accedere a [!DNL Experience Platform Launch]. [!DNL Experience Platform Launch] viene offerta ai clienti Adobe Experience Cloud come funzione inclusa a valore aggiunto. Contattate l’amministratore dell’organizzazione per ottenere l’accesso [!DNL Launch] e chiedete loro di concedervi l’ **[!UICONTROL manage_properties]** autorizzazione necessaria per installare le estensioni.

## Installa estensione {#install-extension}

Per installare l’ [!DNL Awin Advertiser Conversion Tag] estensione:

1. Nell&#39;interfaccia CDP in tempo reale del [Adobe](http://platform.adobe.com/), passare a **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.
2. Selezionate l’estensione dal catalogo o usate la barra di ricerca.
3. Fai clic sulla destinazione per evidenziarla, quindi selezionala **[!UICONTROL Configure]** nella barra a destra. Se il **[!UICONTROL Configure]** controllo è disattivato, manca l&#39; **[!UICONTROL manage_properties]** autorizzazione. Consultate [Prerequisiti](#prerequisites).
4. Nella **[!UICONTROL Select available Platform Launch property]** finestra, selezionate la [!DNL Platform Launch] proprietà in cui desiderate installare l’estensione. È inoltre possibile creare una nuova proprietà in [!DNL Platform Launch]. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Ulteriori informazioni sulle proprietà sono disponibili nella sezione [della pagina](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Proprietà della [!DNL Launch] documentazione.
5. Il flusso di lavoro consente di completare [!DNL Platform Launch] l’installazione.

Per informazioni sulle opzioni di configurazione dell&#39;estensione e sul supporto dell&#39;installazione, consultate la pagina Tag Conversione [Awin Advertiser in  Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103240.awin-conversion-tag.html).

È inoltre possibile installare l’estensione direttamente nell’interfaccia [](https://launch.adobe.com/)Adobe Experience Platform Launch. Consultate [Aggiungere una nuova estensione](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) nella [!DNL Platform Launch] documentazione.


## Come utilizzare l&#39;estensione {#how-to-use}

Una volta installata l’estensione, potete avviare l’impostazione delle relative regole direttamente in [!DNL Platform Launch].

In [!DNL Platform Launch], potete impostare le regole per le estensioni installate per inviare i dati dell&#39;evento alla destinazione dell&#39;estensione solo in alcune situazioni. Per ulteriori informazioni sulla configurazione delle regole per le estensioni, consulta la documentazione [sulle](https://docs.adobe.com/help/it-IT/launch/using/reference/manage-resources/rules.html)regole.

## Configurare, aggiornare ed eliminare l&#39;estensione {#configure-upgrade-delete}

È possibile configurare, aggiornare ed eliminare le estensioni nell&#39; [!DNL Platform Launch] interfaccia.

>[!TIP]
>
>Se l’estensione è già installata su una delle proprietà, l’interfaccia utente CDP in tempo reale del Adobe  continua a essere visualizzata **[!UICONTROL Install]** per l’estensione. Per accedere al flusso di lavoro di installazione e configurarlo o eliminarlo, fate clic su [Installa estensione](#install-extension) [!DNL Platform Launch] .

Per aggiornare l’estensione, consultate Aggiornamento [dell’](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) estensione nella [!DNL Platform Launch] documentazione.
