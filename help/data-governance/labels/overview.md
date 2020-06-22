---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Panoramica delle etichette di utilizzo dei dati
topic: labels
translation-type: tm+mt
source-git-commit: e3c69589e0d4f8224b74a663b23f67e6731ddec4
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---


# Panoramica delle etichette di utilizzo dei dati

L&#39;etichettatura e l&#39;applicazione dell&#39;uso dei dati (DULE) è il meccanismo fondamentale  governance dei dati del Adobe Experience Platform. Le funzioni DULE consentono di applicare etichette di utilizzo dei dati a set di dati e campi, suddividendo ciascuna in categorie in base ai relativi criteri di utilizzo dei dati.

Questo documento fornisce una panoramica delle etichette di utilizzo dei dati (dette anche etichette DULE) in  Experience Platform. Prima di leggere questa guida, consulta la panoramica [sulla governance dei](../home.md) dati per un&#39;introduzione più efficace al quadro DULE.

## Informazioni sulle etichette di utilizzo dei dati

Le etichette di utilizzo dei dati consentono di classificare set di dati e campi in base ai criteri di utilizzo applicabili ai dati. Le etichette possono essere applicate in qualsiasi momento, fornendo la flessibilità nella modalità di gestione dei dati. Le best practice incoraggiano l&#39;etichettatura dei dati non appena vengono trasferiti  Experience Platform, o non appena i dati diventano disponibili per l&#39;uso in Platform.

Le etichette di utilizzo dei dati applicate a livello di dataset vengono propagate a tutti i campi all&#39;interno del dataset. Le etichette possono anche essere applicate direttamente a singoli campi (intestazioni di colonna) di un dataset, senza propagazione.

Per ulteriori informazioni sulle etichette di utilizzo dei dati disponibili in  Experience Platform e sui criteri di utilizzo che rappresentano, consultare la guida sulle etichette [di utilizzo dei dati](reference.md)supportate.

## Ereditarietà delle etichette per i segmenti di pubblico

Tutti i segmenti di pubblico creati da [servizio](../../segmentation/home.md) di segmentazione Adobe Experience Platform ereditano le etichette di utilizzo dei set di dati corrispondenti. Questo consente alle applicazioni integrate  Experience Platform (come Real-time Customer Data Platform) di fornire l&#39;applicazione automatica dei criteri di utilizzo dei dati quando si attivano i segmenti alle destinazioni.

Oltre a ereditare le etichette a livello di set di dati, per impostazione predefinita i segmenti ereditano tutte le etichette a livello di campo dai set di dati associati. A seconda del modo in cui l’applicazione basata su Platform consuma i segmenti, è possibile specificare quali campi vengono utilizzati, impedendo al segmento di ereditare le etichette dai campi esclusi.

Per ulteriori informazioni sul funzionamento dell’applicazione automatica in CDP in tempo reale, consulta la panoramica [sulla governance dei dati CDP in tempo](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)reale.

<!-- (Add after DEC mapping reference is added to AAM docs to link out to)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent labels and marketing actions recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to data usage labels in Platform, please refer to the [Audience Manager documentation](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/data-export-controls.html).
-->

## Passaggi successivi

Ora che sono state introdotte etichette sull’uso dei dati, potete continuare a leggere la guida [](user-guide.md) utente per apprendere come gestire le etichette nell’interfaccia  Experience Platform. Per i passaggi relativi alla gestione delle etichette mediante le API, consultate la sezione appropriata nella guida [per gli sviluppatori di](../../catalog/api/labels.md)Catalog Service.