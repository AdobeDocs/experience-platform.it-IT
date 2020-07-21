---
title: Estensione Google Gtag
seo-title: Estensione Google Gtag
description: L'estensione Google Gtag è una destinazione pubblicitaria in Adobe Real-time Customer Data Platform. Per ulteriori informazioni sulla funzionalità di estensione, consultate la pagina dell'estensione in Adobe Exchange.
seo-description: null
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 5%

---


# Estensione Google Gtag {#gtag-advertising-extension}

## Panoramica {#overview}

Caricate Google&#39;s `gtag.js` nel vostro sito per inviare i dati dell&#39;evento a [!DNL Google Analytics], Google Ads e [!DNL Google Marketing Platform]. Questa estensione aggiunge al sito solo il codice del tag. Dovrete utilizzare altre estensioni Google per aggiungere eventi e azioni che utilizzeranno gtag.

Google gtag è un&#39;estensione pubblicitaria in Adobe Real-time Customer Data Platform. Per ulteriori informazioni sulla funzionalità di estensione, consultate la pagina dell&#39;estensione in [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

Questa destinazione è un&#39;estensione di Experience Platform Launch. Per ulteriori informazioni sul funzionamento delle estensioni Launch in Adobe Real-time CDP, consultate Panoramica [delle estensioni](/help/rtcdp/destinations/experience-platform-launch-extensions.md)di Experience Platform Launch.

![Estensione Google Gtag](/help/rtcdp/destinations/assets/gtag-advertising-extension.png)

## Prerequisiti  {#prerequisites}

Questa estensione è disponibile nel [!DNL Destinations] catalogo per tutti i clienti che hanno acquistato Adobe Real-time CDP.

Per utilizzare questa estensione, è necessario accedere al Experience Platform Launch. L’Experience Platform Launch viene offerto ai clienti Adobe Experience Cloud come funzione inclusa a valore aggiunto. Contatta l’amministratore dell’organizzazione per ottenere l’accesso a Launch e chiedi loro di concederti l’ **[!UICONTROL manage_properties]** autorizzazione necessaria per installare le estensioni.

## Installa estensione {#install-extension}

Per installare l’estensione Google Gtag:

1. Nell’interfaccia CDP [Adobe Real-time, passate a](http://platform.adobe.com/)**[!UICONTROL Destinations > Catalog]**.
2. Selezionate l’estensione dal catalogo o usate la barra di ricerca.
3. Fai clic sulla destinazione per evidenziarla, quindi selezionala **[!UICONTROL Install Extension]** nella barra a destra. Se il **[!UICONTROL Install Extension]** controllo è disattivato, manca l&#39; **[!UICONTROL manage_properties]** autorizzazione. Consultate [Prerequisiti](#prerequisites).
4. Nella **[!UICONTROL Select available Launch property]** finestra, selezionate la proprietà Launch in cui desiderate installare l&#39;estensione. È inoltre possibile creare una nuova proprietà in Launch. Una proprietà è una raccolta di regole, elementi di dati, estensioni configurate, ambienti e librerie. Ulteriori informazioni sulle proprietà sono disponibili nella sezione [della pagina](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Proprietà della documentazione di Launch.
5. Per completare l’installazione, passa a Launch.

Per informazioni sulle opzioni di configurazione dell&#39;estensione e sul supporto dell&#39;installazione, consultate la pagina [Google gtag in Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

Potete anche installare l’estensione direttamente nell’interfaccia [del](https://launch.adobe.com/)Experience Platform Launch. Consultate [Aggiungere una nuova estensione](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) nella documentazione di Launch.


## Come utilizzare l&#39;estensione {#how-to-use}

Una volta installata l’estensione, potete avviare la configurazione delle relative regole direttamente in Launch.

In Launch, puoi impostare le regole per le estensioni installate per inviare i dati dell&#39;evento alla destinazione dell&#39;estensione solo in alcune situazioni. Per ulteriori informazioni sulla configurazione delle regole per le estensioni, consulta la documentazione [sulle](https://docs.adobe.com/help/it-IT/launch/using/reference/manage-resources/rules.html)regole.

## Configurare, aggiornare ed eliminare l&#39;estensione {#configure-upgrade-delete}

Puoi configurare, aggiornare ed eliminare le estensioni nell&#39;interfaccia Launch.

>[!TIP]
>
>Se l’estensione è già installata su una delle proprietà, l’interfaccia utente Adobe Real-time CDP viene visualizzata **[!UICONTROL Install]** per l’estensione. Per accedere a Launch e configurare o eliminare l’estensione, scegli il flusso di lavoro di installazione come descritto in Estensione [di](#install-extension) installazione.

Per aggiornare l’estensione, consulta Aggiornamento [](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) estensione nella documentazione di Launch.
