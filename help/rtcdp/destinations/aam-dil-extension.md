---
title: ' estensione DIL Audience Manager'
seo-title: ' estensione DIL Audience Manager'
description: L’estensione  Audience Manager DIL è una destinazione Platform per la gestione dei dati (DMP) in Adobe Real-time Customer Data Platform. Per ulteriori informazioni sulla funzionalità di estensione, consultate la pagina dell'estensione in Adobe Exchange.
seo-description: L’estensione  Audience Manager DIL è una destinazione Platform per la gestione dei dati (DMP) in Adobe Real-time Customer Data Platform. Per ulteriori informazioni sulla funzionalità di estensione, consultate la pagina dell'estensione in Adobe Exchange.
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 7%

---


#  estensione DIL Audience Manager {#aam-dil-extension}

## Panoramica {#overview}

Questa è l&#39;estensione  Adobe Audience Manager Data Integration Library (implementazione lato client). Nota: Questa estensione non è destinata all&#39;inoltro lato server (SSF) di dati Adobe  Analytics. Per SSF, utilizzate l&#39;estensione Adobe  Analytics. Importante: A partire dalla versione 8.0, DIL dipende dal servizio [!DNL Experience Cloud] ID, versione 3.3 o successiva. Implementa sia il servizio [!DNL Experience Cloud] ID che il codice DIL per funzionalità complete di integrazione dei [!DNL Audience Manager] dati.

[!DNL Audience Manager] DIL è un’estensione DMP (Data Management Platform) in Adobe Real-time Customer Data Platform. Per ulteriori informazioni sulla funzionalità di estensione, consultate la [pagina](https://docs.adobe.com/content/help/it-IT/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html) dell&#39;estensione Audience Manager nella documentazione dell&#39;Experience Platform Launch.

Questa destinazione è un&#39; [!DNL Experience Platform Launch] estensione. Per ulteriori informazioni sul funzionamento delle estensioni Launch in Adobe Real-time CDP, consultate Panoramica [delle estensioni](/help/rtcdp/destinations/experience-platform-launch-extensions.md)di Experience Platform Launch.

![estensione DIL Audience Manager](/help/rtcdp/destinations/assets/aam-dil-extension.png)

## Prerequisiti  {#prerequisites}

Questa estensione è disponibile nel [!DNL Destinations] catalogo per tutti i clienti che hanno acquistato Adobe Real-time CDP.

Per utilizzare questa estensione, è necessario accedere a [!DNL Experience Platform Launch]. [!DNL Experience Platform Launch] viene offerta ai clienti Adobe Experience Cloud come funzione inclusa a valore aggiunto. Contattate l’amministratore dell’organizzazione per ottenere l’accesso [!DNL Launch] e chiedete loro di concedervi l’ **[!UICONTROL manage_properties]** autorizzazione necessaria per installare le estensioni.

## Installa estensione {#install-extension}

Per installare l’estensione [!DNL Audience Manager] DIL:

1. Nell’interfaccia CDP [Adobe Real-time, passate a](http://platform.adobe.com/)**[!UICONTROL Destinations > Catalog]**.
2. Selezionate l’estensione dal catalogo o usate la barra di ricerca.
3. Fai clic sulla destinazione per evidenziarla, quindi selezionala **[!UICONTROL Install Extension]** nella barra a destra. Se il **[!UICONTROL Install Extension]** controllo è disattivato, manca l&#39; **[!UICONTROL manage_properties]** autorizzazione. Consultate [Prerequisiti](#prerequisites).
4. Nella **[!UICONTROL Select available Launch property]** finestra, selezionate la [!DNL Launch] proprietà in cui desiderate installare l’estensione. È inoltre possibile creare una nuova proprietà in Launch. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Ulteriori informazioni sulle proprietà sono disponibili nella sezione [della pagina](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Proprietà della [!DNL Launch] documentazione.
5. Il flusso di lavoro consente di completare [!DNL Launch] l’installazione.

Per informazioni sulle opzioni di configurazione dell&#39;estensione, consultate la pagina [dell&#39;estensione](https://docs.adobe.com/content/help/it-IT/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html) Audience Manager nella [!DNL Experience Launch] documentazione.

Potete anche installare l’estensione direttamente nell’interfaccia [del](https://launch.adobe.com/)Experience Platform Launch. Consultate [Aggiungere una nuova estensione](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) nella [!DNL Launch] documentazione.


## Come utilizzare l&#39;estensione {#how-to-use}

Una volta installata l’estensione, potete avviare l’impostazione delle relative regole direttamente in [!DNL Launch].

In [!DNL Launch], potete impostare le regole per le estensioni installate per inviare i dati dell&#39;evento alla destinazione dell&#39;estensione solo in alcune situazioni. Per ulteriori informazioni sulla configurazione delle regole per le estensioni, consulta la documentazione [sulle](https://docs.adobe.com/help/it-IT/launch/using/reference/manage-resources/rules.html)regole.

## Configurare, aggiornare ed eliminare l&#39;estensione {#configure-upgrade-delete}

È possibile configurare, aggiornare ed eliminare le estensioni nell&#39; [!DNL Launch] interfaccia.

>[!TIP]
>
>Se l’estensione è già installata su una delle proprietà, l’interfaccia utente Adobe Real-time CDP viene visualizzata **[!UICONTROL Install]** per l’estensione. Per accedere al flusso di lavoro di installazione e configurarlo o eliminarlo, fate clic su [Installa estensione](#install-extension) [!DNL Launch] .

Per aggiornare l’estensione, consultate Aggiornamento [dell’](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) estensione nella [!DNL Launch] documentazione.



