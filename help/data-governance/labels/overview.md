---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Panoramica delle etichette di utilizzo dei dati
topic: labels
translation-type: tm+mt
source-git-commit: f4b3148db3b4a17d071c1c8ad2aff8dd64ddd0b7
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---


# Panoramica delle etichette di utilizzo dei dati

L&#39;etichettatura e l&#39;applicazione dell&#39;uso dei dati (DULE) è il meccanismo fondamentale  governance dei dati del Adobe Experience Platform. Le funzioni DULE consentono di applicare etichette di utilizzo dei dati a set di dati e campi, suddividendo ciascuna in categorie in base ai relativi criteri di utilizzo dei dati.

Questo documento fornisce una panoramica delle etichette di utilizzo dei dati (dette anche etichette DULE) in [!DNL Experience Platform]. Prima di leggere questa guida, consulta la panoramica [sulla governance dei](../home.md) dati per un&#39;introduzione più efficace al quadro DULE.

## Informazioni sulle etichette di utilizzo dei dati

Le etichette di utilizzo dei dati consentono di classificare set di dati e campi in base ai criteri di utilizzo applicabili ai dati. Le etichette possono essere applicate in qualsiasi momento, fornendo la flessibilità nella modalità di gestione dei dati. Le best practice incoraggiano i dati di etichettatura non appena vengono ingeriti [!DNL Experience Platform]o non appena i dati diventano disponibili per l&#39;uso in [!DNL Platform].

Le etichette di utilizzo dei dati applicate a livello di dataset vengono propagate a tutti i campi all&#39;interno del dataset. Le etichette possono anche essere applicate direttamente a singoli campi (intestazioni di colonna) di un dataset, senza propagazione.

[!DNL Platform] fornisce diverse etichette di utilizzo dei dati di base pronte all&#39;uso, che coprono un&#39;ampia gamma di limitazioni comuni applicabili alla governance dei dati. Per ulteriori informazioni su queste etichette e sui criteri di utilizzo che rappresentano, consultare la guida sulle etichette [di utilizzo dei dati di](reference.md)base.

Oltre alle etichette fornite da Adobe, potete anche definire le vostre etichette personalizzate. Per informazioni su come eseguire questa operazione nell&#39;interfaccia utente, consulta la guida [utente relativa alle etichette di utilizzo dei](./user-guide.md)dati. Per i passaggi su come eseguire questa operazione utilizzando le chiamate API, fare riferimento alla guida [API delle etichette di utilizzo](./api.md)dei dati.

## Ereditarietà delle etichette per i segmenti di pubblico

Tutti i segmenti di pubblico creati da [servizio](../../segmentation/home.md) di segmentazione Adobe Experience Platform ereditano le etichette di utilizzo dei set di dati corrispondenti. Questo consente alle applicazioni integrate [!DNL Experience Platform] (come [!DNL Real-time Customer Data Platform]) di fornire l&#39;applicazione automatica dei criteri di utilizzo dei dati durante l&#39;attivazione dei segmenti nelle destinazioni.

Oltre a ereditare le etichette a livello di set di dati, per impostazione predefinita i segmenti ereditano tutte le etichette a livello di campo dai set di dati associati. A seconda del modo in cui l’applicazione [!DNL Platform]basata sui segmenti utilizza i segmenti, è possibile specificare quali campi vengono utilizzati, impedendo al segmento di ereditare le etichette dai campi esclusi.

Per ulteriori informazioni sul funzionamento dell’applicazione automatica in CDP in tempo reale, consultate la panoramica [sulla governance dei dati in tempo reale di](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)Adobe.

### Ereditarietà dai controlli di esportazione dei dati  Adobe Audience Manager

 Experience Platform è in grado di condividere segmenti con  Adobe Audience Manager. Eventuali controlli sull&#39;esportazione dei dati applicati  segmenti Audience Manager vengono convertiti in etichette e azioni di marketing equivalenti riconosciute  gestione dei dati Experience Platform.

Per un riferimento alla modalità in cui specifici controlli di esportazione dei dati vengono mappati sulle etichette di utilizzo dei dati in Platform, consultare la documentazione [di](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep)Audience Manager.


## Passaggi successivi

Ora che sono state introdotte etichette sull’uso dei dati, potete continuare a leggere la guida [](user-guide.md) utente per apprendere come gestire le etichette nell’ [!DNL Experience Platform] interfaccia utente. Per informazioni sulla gestione delle etichette tramite API, consultate la guida [API delle etichette di](./api.md)utilizzo.