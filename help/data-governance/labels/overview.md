---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Panoramica delle etichette di utilizzo dei dati
topic: labels
translation-type: tm+mt
source-git-commit: 4b6b9ca5ae7861f8e8b974550be14fbce6efdcf1
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---


# Panoramica delle etichette di utilizzo dei dati

L’etichettatura e l’applicazione dell’uso dei dati (DULE) è il meccanismo fondamentale di governance dei dati della piattaforma Adobe Experience. Le funzioni DULE consentono di applicare etichette di utilizzo dei dati a set di dati e campi, suddividendo ciascuna in categorie in base ai relativi criteri di utilizzo dei dati.

Questo documento fornisce una panoramica delle etichette di utilizzo dei dati (dette anche etichette DULE) in Experience Platform (Piattaforma esperienza). Prima di leggere questa guida, consulta la panoramica [sulla governance dei](../home.md) dati per un&#39;introduzione più efficace al quadro DULE.

## Informazioni sulle etichette di utilizzo dei dati

Le etichette di utilizzo dei dati consentono di classificare set di dati e campi in base ai criteri di utilizzo applicabili ai dati. Le etichette possono essere applicate in qualsiasi momento, fornendo la flessibilità nella modalità di gestione dei dati. Le best practice incoraggiano l’etichettatura dei dati non appena vengono trasferiti nella piattaforma Experience o non appena i dati diventano disponibili per l’uso in tale piattaforma.

Le etichette di utilizzo dei dati applicate a livello di dataset vengono propagate a tutti i campi all&#39;interno del dataset. Le etichette possono anche essere applicate direttamente a singoli campi (intestazioni di colonna) di un dataset, senza propagazione.

Per ulteriori informazioni sulle etichette di utilizzo dei dati disponibili in Experience Platform e sui criteri di utilizzo che rappresentano, consulta la guida sulle etichette [di utilizzo dei dati](reference.md)supportate.

## Ereditarietà delle etichette per i segmenti di pubblico

Tutti i segmenti di pubblico creati da [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) ereditano le etichette di utilizzo dei set di dati corrispondenti. Questo consente alle applicazioni basate sulla piattaforma Experience Platform (come la piattaforma dati cliente in tempo reale) di fornire l&#39;applicazione automatica dei criteri di utilizzo dei dati quando si attivano i segmenti alle destinazioni.

Oltre a ereditare le etichette a livello di set di dati, per impostazione predefinita i segmenti ereditano tutte le etichette a livello di campo dai set di dati associati. A seconda del modo in cui l’applicazione basata sulla piattaforma consuma i segmenti, potete potenzialmente specificare quali campi vengono utilizzati, impedendo al segmento di ereditare le etichette dai campi esclusi.

Per ulteriori informazioni sul funzionamento dell’applicazione automatica in CDP in tempo reale, consulta la panoramica [sulla governance dei dati CDP in tempo](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)reale.

## Passaggi successivi

Dopo aver introdotto le etichette di utilizzo dei dati, puoi continuare a leggere la guida [](user-guide.md) utente per apprendere come gestire le etichette nell’interfaccia utente della piattaforma Experience. Per i passaggi relativi alla gestione delle etichette mediante le API, consultate la sezione appropriata nella guida [per gli sviluppatori di](../../catalog/api/labels.md)Catalog Service.