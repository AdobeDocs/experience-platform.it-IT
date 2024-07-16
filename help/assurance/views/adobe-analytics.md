---
title: Vista di Adobe Analytics in Assurance
description: Questa guida spiega come utilizzare Adobe Analytics con Adobe Experience Platform Assurance.
exl-id: e5cc72b0-d6d6-430b-9321-4835c1f77581
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 100%

---

# Vista di Adobe Analytics in Assurance

L’integrazione di Adobe Experience Platform Assurance con Adobe Analytics offre agli utenti una visione più completa degli eventi SDK per il debug e della convalida dell’implementazione di Adobe Analytics. La vista ora mostra gli eventi del ciclo di vita e di azione/stato inviati ad Adobe Analytics da [Adobe Experience Platform SDK](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/). La vista include anche i dettagli di &quot;risposta&quot; che forniscono informazioni su come gli eventi sono stati elaborati dopo l’applicazione delle regole di elaborazione di ogni suite di rapporti.

![](./images/adobe-analytics/overview.png)

## Introduzione

Prima di continuare, assicurati di disporre dei seguenti servizi:

- L’[interfaccia utente Raccolta dati di Adobe Experience Platform](https://experience.adobe.com/it#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/it/assurance)

Per informazioni su come installare Assurance nell’applicazione, consulta la [guida all’implementazione di Assurance](../tutorials/implement-assurance.md).

## Stato post-elaborazione

Dopo che l’SDK ha effettuato una richiesta di rete con Adobe Analytics, lo stato ti dirà se Assurance è stato in grado di recuperare le informazioni di post-elaborazione per la richiesta di Adobe Analytics.

Per recuperare le informazioni di post-elaborazione, l’utente connesso deve avere accesso alla suite di rapporti corrispondente.

| Stato | Descrizione |
| :----- | :---------- |
| `Queued` | La richiesta di rete sta recuperando le informazioni di post-elaborazione. |
| `Processed` | La richiesta di rete è riuscita e vengono ricevute le informazioni di post-elaborazione. |
| `Delayed` | È stato superato il numero massimo di tentativi per recuperare le informazioni di post-elaborazione. |
| `Error` | Un errore ha causato un errore nella richiesta di rete. Maggiori dettagli sull’errore vengono visualizzati nella vista dettagli dell’evento. |
| `Unauthorized` | L’utente non ha accesso alla suite di rapporti di Adobe Analytics. |
| `Unavailable` | La richiesta di Adobe Analytics non ha un evento `AnalyticsResponse` corrispondente. |
| `No Debug Flag` | La versione corrente di Adobe Analytics o Assurance SDK potrebbe non supportare la funzione di debug di Analytics. Per ulteriori informazioni, consulta la [Guida alla risoluzione dei problemi](../troubleshooting.md). |
| `Expired` | L’evento `AnalyticsTrack` o `LifecycleStart` è precedente alle 24 ore. |

## Vista dettagli dell’evento

Per un evento di tracciamento di Analytics, la vista dettagliata contiene le seguenti parti importanti:

- Un evento di richiesta dell’SDK di Analytics di origine.
- Metadati e dati contestuali OOTB della richiesta, come l’ID della suite di rapporti, le versioni dell’estensione SDK, i dati contestuali OOTB e così via.
- Informazioni della fase di post-elaborazione sull’evento di Analytics che contengono la mappatura di revar, evar, prop e così via.
