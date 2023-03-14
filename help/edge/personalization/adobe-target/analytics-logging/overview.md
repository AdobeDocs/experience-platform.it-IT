---
title: Registrazione di Adobe Analytics for Target (A4T) in Platform Web SDK
description: Scopri come controllare la raccolta di dati di Adobe Analytics for Target (A4T) utilizzando Experience Platform Web SDK.
seo-title: Adobe Analytics for Target (A4T) Logging in the Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;registrazione;analytics;sdk;web sdk;
exl-id: f1c90ccd-48a9-4668-b2ac-eacd5bec0b91
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---

# Registrazione di Adobe Analytics for Target (A4T) in Platform Web SDK

Quando utilizzi Adobe Target per la personalizzazione, puoi scegliere quale sistema utilizzare per la misurazione delle prestazioni. Ogni [Attività Target](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) consente di scegliere tra reporting di Target e reporting di Adobe Analytics.

Se utilizzi la generazione rapporti di Analytics, Adobe Target deve comunicare ad Analytics quanto segue:

* Quale attività Adobe Target sono state immesse dai visitatori
* Quale esperienza hanno visto
* Quale conversione è stata raggiunta

Adobe Experience Platform Web SDK supporta due tipi di registrazione di Analytics per i casi d’uso di Analytics for Target (A4T):

| Metodo di registrazione | Descrizione |
| --- | --- |
| Registrazione Analytics lato server | Tutti gli hit di Analytics inviati tramite la rete Edge vengono potenziati con i dettagli di Target sul lato server, senza dover passare attraverso il processo di unione degli hit. |
| Registrazione Analytics lato client | I dati di Target vengono restituiti sul lato client, consentendoti di migliorare e inviare manualmente i dati ad Analytics utilizzando [API di inserimento dati](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html). |

Il metodo di registrazione è determinato dalla presenza o meno di Adobe Analytics abilitato nella configurazione [flusso di dati](../../../datastreams/overview.md):

![Flusso di decisione del metodo di registrazione](../assets/analytics-logging.png)

## Passaggi successivi

Questo documento fornisce una breve introduzione ai diversi metodi di registrazione per i dati A4T nell’SDK per web. Per informazioni più dettagliate su ciascuno di questi metodi, consulta la seguente documentazione:

* [Registrazione lato server per i dati A4T in Platform Web SDK](./server-side.md)
* [Registrazione lato client per i dati A4T in Platform Web SDK](./client-side.md)
