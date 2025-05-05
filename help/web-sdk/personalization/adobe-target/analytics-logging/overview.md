---
title: Registrazione di Adobe Analytics for Target (A4T) in Experience Platform Web SDK
description: Scopri come controllare la raccolta di dati di Adobe Analytics for Target (A4T) utilizzando Experience Platform Web SDK.
seo-title: Adobe Analytics for Target (A4T) Logging in the Experience Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;registrazione;analytics;sdk;web sdk;
exl-id: f1c90ccd-48a9-4668-b2ac-eacd5bec0b91
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---

# Registrazione di Adobe Analytics for Target (A4T) in Experience Platform Web SDK

Quando utilizzi Adobe Target per la personalizzazione, puoi scegliere quale sistema utilizzare per la misurazione delle prestazioni. Ogni [attività Target](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html?lang=it) ti consente di selezionare tra reporting di Target e reporting di Adobe Analytics.

Se utilizzi la generazione rapporti di Analytics, Adobe Target deve comunicare ad Analytics quanto segue:

* Quale attività Adobe Target sono state immesse dai visitatori
* Quale esperienza hanno visto
* Quale conversione è stata raggiunta

Adobe Experience Platform Web SDK supporta due tipi di registrazione di Analytics per i casi d’uso di Analytics for Target (A4T):

| Metodo di registrazione | Descrizione |
| --- | --- |
| Registrazione Analytics lato server | Tutti gli hit di Analytics inviati tramite Edge Network vengono potenziati con i dettagli di Target sul lato server, senza dover passare attraverso il processo di unione degli hit. |
| Registrazione Analytics lato client | I dati di destinazione vengono restituiti sul lato client, consentendo di aumentare e inviare manualmente i dati ad Analytics utilizzando l&#39;[API di inserimento dati](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html?lang=it). |

Il metodo di registrazione è determinato dall&#39;abilitazione di Adobe Analytics nel [flusso di dati](../../../../datastreams/overview.md) configurato:

![Flusso di decisione del metodo di registrazione](../assets/analytics-logging.png)

## Passaggi successivi

Questo documento fornisce una breve introduzione ai diversi metodi di registrazione per i dati A4T nel Web SDK. Per informazioni più dettagliate su ciascuno di questi metodi, consulta la seguente documentazione:

* [Registrazione lato server per i dati A4T in Experience Platform Web SDK](./server-side.md)
* [Registrazione lato client dei dati A4T in Experience Platform Web SDK](./client-side.md)
