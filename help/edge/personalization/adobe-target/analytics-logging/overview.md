---
title: Registrazione di Adobe Analytics for Target (A4T) nell’SDK per web di Platform
description: Scopri come controllare la raccolta di dati di Adobe Analytics for Target (A4T) utilizzando l’SDK per web di Experience Platform.
seo-title: Adobe Analytics for Target (A4T) Logging in the Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;logging;analytics;sdk;sdk web;
exl-id: f1c90ccd-48a9-4668-b2ac-eacd5bec0b91
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---

# Registrazione di Adobe Analytics for Target (A4T) nell’SDK per web di Platform

Quando utilizzi Adobe Target per la personalizzazione, puoi scegliere il sistema da utilizzare per la misurazione delle prestazioni. Ogni [Attività Target](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) consente di scegliere tra il reporting di Target e il reporting di Adobe Analytics.

Se utilizzi il reporting di Analytics, Adobe Target deve comunicare quanto segue ad Analytics:

* Quale attività di Adobe Target i visitatori hanno inserito
* Quale esperienza hanno visto
* Quale conversione è stata raggiunta

L’SDK per web di Adobe Experience Platform supporta due tipi di log di Analytics per i casi d’uso di Analytics for Target (A4T):

| Metodo di registrazione | Descrizione |
| --- | --- |
| Registrazione Analytics lato server | Tutti gli hit di Analytics inviati tramite la rete Edge vengono aumentati con i dettagli di Target sul lato server, senza dover passare attraverso il processo di unione degli hit. |
| Registrazione Analytics lato client | I dati di Target vengono restituiti sul lato client, consentendoti di integrare e inviare manualmente i dati ad Analytics utilizzando il comando [API di inserimento dati](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html). |

Il metodo di registrazione è determinato dal fatto che Adobe Analytics sia abilitato o meno nella configurazione [datastream](../../../datastreams/overview.md):

![Flusso decisionale del metodo di registrazione](../assets/analytics-logging.png)

## Passaggi successivi

Questo documento fornisce una breve introduzione ai diversi metodi di registrazione per i dati A4T nell’SDK per web. Per informazioni più dettagliate su ciascuno di questi metodi, consulta la seguente documentazione:

* [Registrazione lato server per i dati A4T nell’SDK per web di Platform](./server-side.md)
* [Registrazione lato client per i dati A4T nell’SDK per web di Platform](./client-side.md)
