---
title: Visualizzazione Adobe Analytics in Assurance
description: Questa guida spiega come utilizzare Adobe Analytics con Adobe Experience Platform Assurance.
exl-id: e5cc72b0-d6d6-430b-9321-4835c1f77581
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 3%

---

# Vista Adobe Analytics in Assurance

L’integrazione di Adobe Experience Platform Assurance con Adobe Analytics offre agli utenti una visione più completa degli eventi SDK per il debug e la convalida dell’implementazione di Adobe Analytics. La visualizzazione ora mostra gli eventi del ciclo di vita e di azione/stato inviati ad Adobe Analytics dalla sezione [SDK per Adobe Experience Platform](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/). La visualizzazione include anche i dettagli di &quot;risposta&quot; che forniscono informazioni su come gli eventi sono stati elaborati dopo l’applicazione delle regole di elaborazione di ogni suite di rapporti.

![](./images/adobe-analytics/overview.png)

## Introduzione

Prima di continuare, assicurati di disporre dei seguenti servizi:

- Il [Interfaccia utente di Adobe Experience Platform Data Collection](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Per informazioni su come installare Assurance nell’applicazione, leggi [guida all’implementazione di Assurance](../tutorials/implement-assurance.md).

## Stato post-elaborazione

Dopo che l’SDK ha effettuato una richiesta di rete con Adobe Analytics, lo stato ti dirà se Assurance è stato in grado di recuperare le informazioni di post-elaborazione per la richiesta di Adobe Analytics.

Per recuperare le informazioni di post-elaborazione, l’utente connesso deve avere accesso alla suite di rapporti corrispondente.

| Stato | Descrizione |
| :----- | :---------- |
| `Queued` | La richiesta di rete sta recuperando le informazioni di post-elaborazione. |
| `Processed` | La richiesta di rete è riuscita e vengono ricevute le informazioni di post-elaborazione. |
| `Delayed` | È stato superato il numero massimo di tentativi per recuperare le informazioni di post-elaborazione. |
| `Error` | Un errore ha causato un errore nella richiesta di rete. Maggiori dettagli sull’errore vengono visualizzati nella visualizzazione dei dettagli dell’evento. |
| `Unauthorized` | L’utente non ha accesso alla suite di rapporti di Adobe Analytics. |
| `Unavailable` | La richiesta di Adobe Analytics non ha un corrispondente `AnalyticsResponse` evento. |
| `No Debug Flag` | La versione corrente di Adobe Analytics o Assurance SDK potrebbe non supportare la funzione di debug di Analytics. Per ulteriori informazioni, leggere [Guida alla risoluzione dei problemi](../troubleshooting.md). |
| `Expired` | Il `AnalyticsTrack` o `LifecycleStart` è più vecchio di 24 ore. |

## Visualizzazione dettagli evento

Per un evento di tracciamento di Analytics, la vista dettagliata contiene le seguenti parti importanti:

- Un evento di richiesta SDK Analytics di origine.
- Metadati e dati contestuali OOTB della richiesta, come ID suite di rapporti, versioni dell’estensione SDK, dati contestuali OOTB e così via.
- Informazioni post-elaborate sull’evento Analytics che contiene la mappatura di revar, evar, prop e così via.
