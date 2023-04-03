---
title: Visualizzazione Adobe Analytics in Assurance
description: Questa guida spiega come utilizzare Adobe Analytics con Adobe Experience Platform Assurance.
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 2%

---


# Vista Adobe Analytics in Assurance

L’integrazione di Adobe Experience Platform Assurance con Adobe Analytics fornisce una visualizzazione più dettagliata degli eventi SDK agli utenti che eseguono il debug e la convalida della loro implementazione Adobe Analytics. La visualizzazione ora mostra gli eventi del ciclo di vita e dell’azione/stato inviati ad Adobe Analytics dal [SDK per Adobe Experience Platform](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/). La visualizzazione presenta anche i dettagli di &quot;risposta&quot; che forniscono informazioni su come sono stati elaborati gli eventi dopo l’applicazione delle rispettive regole di elaborazione della suite di rapporti.

![](./images/adobe-analytics/overview.png)

## Introduzione

Prima di continuare, assicurati di disporre dei seguenti servizi:

- La [Interfaccia utente di raccolta dati di Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Per informazioni su come installare Assurance nella tua applicazione, leggi la [guida all’implementazione di Assurance](../tutorials/implement-assurance.md).

## Stato post-elaborazione

Dopo che l’SDK ha effettuato una richiesta di rete con Adobe Analytics, lo stato indica se Assurance è stata in grado di recuperare le informazioni di post-elaborazione per la richiesta Adobe Analytics.

Tieni presente che per recuperare le informazioni post-elaborazione, l’utente connesso deve avere accesso alla suite di rapporti corrispondente.

| Stato | Descrizione |
| :----- | :---------- |
| `Queued` | Recupero delle informazioni post-elaborazione da parte della richiesta di rete. |
| `Processed` | Richiesta di rete riuscita e ricezione delle informazioni post-elaborazione. |
| `Delayed` | È stato superato il numero massimo di tentativi di recupero delle informazioni post-elaborazione. |
| `Error` | Errore che ha causato un errore nella richiesta di rete. Ulteriori dettagli sull&#39;errore vengono visualizzati nella visualizzazione dei dettagli dell&#39;evento. |
| `Unauthorized` | L’utente non ha accesso alla suite di rapporti di Adobe Analytics. |
| `Unavailable` | La richiesta Adobe Analytics non ha un `AnalyticsResponse` evento. |
| `No Debug Flag` | La versione corrente dell’SDK Adobe Analytics o Assurance potrebbe non supportare la funzione di debug di Analytics. Per ulteriori informazioni, leggere il [Guida alla risoluzione dei problemi](../troubleshooting.md). |
| `Expired` | La `AnalyticsTrack` o `LifecycleStart` è più vecchio di 24 ore. |

## Visualizzazione dettagli evento

Per un evento di tracciamento di Analytics, la visualizzazione dettagliata contiene le seguenti parti importanti:

- Un evento di richiesta SDK Analytics di origine.
- Metadati OOTB e dati contestuali della richiesta, ad esempio ID suite di rapporti, versioni dell’estensione SDK, dati contestuali OOTB e così via.
- Informazioni post-elaborazione sull’evento Analytics che contiene la mappatura di revar, evar, prop e così via.
