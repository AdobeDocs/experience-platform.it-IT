---
title: Impostazioni di sostituzione della configurazione dello stream di dati
description: Modificare le impostazioni di configurazione quando vengono soddisfatte determinate condizioni.
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 3%

---

# Impostazioni di sostituzione della configurazione dello stream di dati

Le sostituzioni dello stream di dati consentono di definire configurazioni aggiuntive per i flussi di dati, che vengono passate ad Edge Network tramite Web SDK. Questa funzione consente di attivare in modo condizionale diversi comportamenti dello stream di dati senza creare un nuovo stream di dati o modificare le impostazioni esistenti.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Extensions]**, quindi seleziona **[!UICONTROL Configure]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Scorri verso il basso fino alla sezione **[!UICONTROL Datastream configuration overrides]**.

L’override della configurazione dello stream di dati è un processo costituito da due passaggi:

1. Innanzitutto, devi definire la sostituzione della configurazione dello stream di dati quando [configuri uno stream di dati](/help/datastreams/configure.md) nell&#39;interfaccia utente dello stream di dati. Per istruzioni su come configurare le sostituzioni, consulta [Le sostituzioni della configurazione dello stream di dati](/help/datastreams/overrides.md) nella documentazione dello stream di dati.
1. Dopo aver configurato la sostituzione dello stream di dati nell’interfaccia utente dello stream di dati, puoi configurare l’estensione tag.

Le sostituzioni dello stream di dati devono essere configurate in base all’ambiente. Gli ambienti di sviluppo, staging e produzione hanno tutti sostituzioni separate. È possibile copiare le impostazioni di sostituzione tra qualsiasi ambiente desiderato:

![Immagine che mostra le sostituzioni della configurazione dello stream di dati tramite la pagina dell&#39;estensione tag di Web SDK.](../assets/datastream-overrides.png)

Per impostazione predefinita, le sostituzioni della configurazione dello stream di dati sono disabilitate. L&#39;opzione **[!UICONTROL Match datastream configuration]** è selezionata per impostazione predefinita.

![L&#39;interfaccia utente dell&#39;estensione tag Web SDK che mostra la configurazione dello stream di dati sostituisce l&#39;impostazione predefinita.](../assets/datastream-override-default.png)

Per abilitare le sostituzioni dello stream di dati nell&#39;estensione tag, selezionare **[!UICONTROL Enabled]** dal menu a discesa.

![Interfaccia utente dell&#39;estensione tag Web SDK che mostra le sostituzioni della configurazione dello stream di dati nell&#39;impostazione Abilitata.](../assets/datastream-override-enabled.png)

Dopo aver abilitato le sostituzioni della configurazione dello stream di dati, puoi configurare le sostituzioni per ciascun servizio descritto di seguito. Queste impostazioni di sostituzione dello stream di dati sovrascrivono tutte le configurazioni e le regole dello stream di dati lato server per l’ambiente selezionato.

## Adobe Analytics

Sostituisci il routing dei dati al servizio Adobe Analytics.

![Immagine dell&#39;interfaccia utente dell&#39;estensione tag Web SDK con le impostazioni di sostituzione dello stream di dati di Adobe Analytics.](../assets/datastream-override-analytics.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**: abilita o disabilita il routing dei dati ad Adobe Analytics.
* **[!UICONTROL Report suites]**: ID per le suite di rapporti di destinazione in Adobe Analytics. Il valore deve essere una suite di rapporti di sostituzione preconfigurata (o un elenco di suite di rapporti separato da virgole) dalla configurazione dello stream di dati. Questa impostazione sostituisce le suite di rapporti principali.
* **[!UICONTROL Add Report Suite]**: selezionare questa opzione per aggiungere altre suite di rapporti.

## Adobe Audience Manager

Sostituisci il routing dei dati a Adobe Audience Manager.

![Immagine dell&#39;interfaccia utente dell&#39;estensione tag Web SDK con le impostazioni di sostituzione dello stream di dati di Adobe Audience Manager.](../assets/datastream-override-audience-manager.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**: abilita o disabilita il routing dei dati a Adobe Audience Manager.
* **[!UICONTROL Third-party ID sync container]**: ID per il contenitore di sincronizzazione ID di terze parti di destinazione in Audience Manager. Il valore deve essere un contenitore secondario preconfigurato dalla configurazione dello stream di dati e sostituisce il contenitore principale.

## Adobe Experience Platform

Sostituisci il routing dei dati a Adobe Experience Platform.

![Immagine dell&#39;interfaccia utente dell&#39;estensione tag Web SDK con le impostazioni di sostituzione dello stream di dati di Adobe Experience Platform.](../assets/datastream-override-experience-platform.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**: abilita o disabilita il routing dei dati a Adobe Experience Platform.
* **[!UICONTROL Event dataset]**: ID per il set di dati dell&#39;evento di destinazione in Adobe Experience Platform. Il valore deve essere un set di dati secondario preconfigurato dalla configurazione dello stream di dati.
* **[!UICONTROL Offer Decisioning]**: abilita o disabilita il routing dei dati al servizio [!DNL Offer Decisioning].
* **[!UICONTROL Edge Segmentation]**: abilita o disabilita il routing dei dati al servizio [!DNL Edge Segmentation].
* **[!UICONTROL Personalization Destinations]**: abilita o disabilita il routing dei dati alle destinazioni di personalizzazione.
* **[!UICONTROL Adobe Journey Optimizer]**: abilita o disabilita il routing dei dati a [!DNL Adobe Journey Optimizer].

## Inoltro eventi lato server di Adobe

Sostituisci il routing dei dati con il servizio di inoltro eventi lato server di Adobe.

![Immagine dell&#39;interfaccia utente dell&#39;estensione tag Web SDK che mostra le impostazioni di sostituzione dello stream di dati di inoltro eventi lato server di Adobe.](../assets/datastream-override-ssf.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**: abilita o disabilita il routing dei dati al servizio di inoltro eventi lato server di Adobe.

## Adobe Target {#target}

Sostituisci il routing dei dati con Adobe Target.

![Immagine dell&#39;interfaccia utente dell&#39;estensione tag Web SDK con le impostazioni di sostituzione dello stream di dati di Adobe Target.](../assets/datastream-override-target.png)

* **[!UICONTROL Enabled]** / **[!UICONTROL Disabled]**: abilita o disabilita il routing dei dati ad Adobe Target.
