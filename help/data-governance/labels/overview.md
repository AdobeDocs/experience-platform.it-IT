---
keywords: Experience Platform;home;argomenti popolari;governance dei dati;api dell'etichetta di utilizzo dati;api del servizio criteri;panoramica delle etichette di utilizzo dati
solution: Experience Platform
title: Panoramica delle etichette di utilizzo dei dati
topic-legacy: labels
description: La governance dei dati di Adobe Experience Platform consente di applicare etichette di utilizzo dei dati ai set di dati e ai campi, suddivisi in categorie in base ai criteri di utilizzo dei dati correlati. Questo documento fornisce una panoramica delle etichette di utilizzo dei dati in Experience Platform.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# Panoramica delle etichette di utilizzo dei dati

La governance dei dati di Adobe Experience Platform ti consente di applicare etichette di utilizzo dei dati ai set di dati e ai campi, suddivisi in categorie in base ai criteri di utilizzo dei dati correlati.

Questo documento fornisce una panoramica delle etichette di utilizzo dei dati in [!DNL Experience Platform]. Prima di leggere questa guida, consulta la [Panoramica sulla governance dei dati](../home.md) per un’introduzione più solida al framework per la governance dei dati.

## Informazioni sulle etichette di utilizzo dei dati

Le etichette di utilizzo dei dati ti consentono di classificare set di dati e campi in base ai criteri di utilizzo applicati a tali dati. Le etichette possono essere applicate in qualsiasi momento, fornendo flessibilità nella scelta della modalità di gestione dei dati. Le best practice incoraggiano l’etichettatura dei dati non appena vengono acquisiti in [!DNL Experience Platform], o non appena i dati diventano disponibili per l&#39;utilizzo in [!DNL Platform].

Le etichette di utilizzo dei dati applicate a livello di set di dati vengono propagate a tutti i campi all’interno del set di dati. Le etichette possono anche essere applicate direttamente ai singoli campi (intestazioni di colonna) di un set di dati, senza propagazione.

[!DNL Platform] fornisce diverse etichette predefinite per l’utilizzo dei dati di base, che coprono un’ampia varietà di restrizioni comuni applicabili alla governance dei dati. Per ulteriori informazioni su queste etichette e sui criteri di utilizzo che rappresentano, consulta la guida su [etichette di utilizzo dei dati di base](reference.md).

Oltre alle etichette fornite dall’Adobe, puoi anche definire etichette personalizzate per la tua organizzazione. Vedi la sezione su [gestione delle etichette](#manage-labels) per ulteriori informazioni.

## Ereditarietà delle etichette per i segmenti di pubblico

Tutti i segmenti di pubblico creati da [Servizio di segmentazione di Adobe Experience Platform](../../segmentation/home.md) eredita le etichette di utilizzo dei set di dati corrispondenti. Questo consente ad Experience Platform di fornire un’applicazione automatica dei criteri di utilizzo dei dati quando si attivano i segmenti sulle destinazioni.

Oltre a ereditare le etichette a livello di set di dati, per impostazione predefinita i segmenti ereditano tutte le etichette a livello di campo dai set di dati associati. Di conseguenza, puoi identificare più facilmente quali attributi devono essere esclusi dai segmenti e impedire loro di ereditare etichette dai campi esclusi.

Per ulteriori informazioni sul funzionamento dell’applicazione automatica in Platform, consulta la panoramica su [applicazione automatica delle politiche](../enforcement/auto-enforcement.md).

### Ereditarietà dai controlli di esportazione dei dati di Adobe Audience Manager

[!DNL Experience Platform] può condividere segmenti con Adobe Audience Manager. Eventuali controlli sull’esportazione dei dati applicati ai segmenti di Audience Manager vengono tradotti in etichette equivalenti e in azioni di marketing riconosciute da [!DNL Experience Platform] Governance dei dati.

Per un riferimento su come specifiche etichette di utilizzo dei dati in Controlli sull’esportazione dei dati vengono mappate in [!DNL Platform], si prega di fare riferimento al [Documentazione di Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## Gestione delle etichette di utilizzo dei dati in [!DNL Experience Platform] {#manage-labels}

Puoi gestire le etichette di utilizzo dei dati utilizzando [!DNL Experience Platform] API o interfaccia utente. Fai riferimento alle sottosezioni seguenti per i dettagli su ciascuna.

### Utilizzo dell’interfaccia

La **[!UICONTROL Criteri]** nell&#39;area di lavoro [!DNL Experience Platform] L’interfaccia utente ti consente di visualizzare e gestire le etichette core e personalizzate per la tua organizzazione. La **[!DNL Datasets]** workspace consente di applicare etichette ai set di dati e ai campi. Per ulteriori informazioni, consulta la [guida utente sulle etichette](user-guide.md).

### Utilizzo delle API

La `/labels` punto finale [API del servizio criteri](https://www.adobe.io/experience-platform-apis/references/policy-service/) consente di gestire in modo programmatico le etichette di utilizzo dei dati, inclusa la creazione di etichette personalizzate. Fai riferimento a [guida all’endpoint delle etichette](../api/labels.md) per ulteriori informazioni.

La [API del servizio set di dati](https://www.adobe.io/experience-platform-apis/references/dataset-service/) viene utilizzato per gestire le etichette per set di dati e campi. Consulta la guida su [gestione delle etichette dei set di dati](./dataset-api.md) per ulteriori informazioni.

## Passaggi successivi

Questo documento fornisce un’introduzione alle etichette di utilizzo dei dati e al loro ruolo all’interno del framework di governance dei dati. Per ulteriori informazioni su come gestire le etichette in , consulta la documentazione collegata a in questa guida [!DNL Experience Platform].
