---
description: Utilizza la [!UICONTROL Arricchimento del profilo] dashboard per capire se i processi di arricchimento dei profili sono stati eseguiti e completati correttamente e per visualizzare le metriche di base per misurare l’efficacia degli arricchimenti.
solution: Experience Platform
title: Monitorare i processi di arricchimento dei profili
type: Tutorial
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 1fed0cf37e7297c21330ebf51ae15054aa21c781
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 2%

---

# Monitorare i processi di arricchimento dei profili nell’interfaccia utente {#monitor-profile-enrichment}

Utilizza la [!UICONTROL Arricchimento del profilo] dashboard per capire se i processi di arricchimento dei profili sono stati eseguiti e completati correttamente e per visualizzare le metriche di base per misurare l’efficacia degli arricchimenti.

In [Interfaccia utente della piattaforma](https://platform.adobe.com), seleziona **[!UICONTROL Monitoraggio]** dalla navigazione a sinistra per accedere al [!UICONTROL Monitoraggio] dashboard. Nel selettore di visualizzazione, seleziona **Flusso B2B** per visualizzare gli elementi del dashboard specifici per [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  La [!UICONTROL Monitoraggio] Il dashboard include le metriche di base dell&#39;esecuzione riuscita più recente e lo stato del processo giornaliero fino a 90 giorni nel passato.

## Arricchimento del profilo di account correlati {#related-accounts}

La [!UICONTROL Account correlati] il dashboard mostra le metriche di base e lo stato del processo giornaliero specifico per [Account correlati](/help/rtcdp/b2b-ai-ml-services/related-accounts.md) arricchimento del profilo.

![Indicazione visiva su come accedere alla schermata di monitoraggio dei processi di arricchimento del profilo nell’interfaccia utente di Experience Platform.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

I dati nel **[!UICONTROL Metriche]** include le metriche di base dell&#39;ultima esecuzione riuscita del processo Account correlati.

Le metriche seguenti sono disponibili per i processi correlati di arricchimento del profilo di account:

| Metrica | Descrizione |
| --------- | ---------- |
| **[!UICONTROL Profili account totali]** | Indica i profili account totali a cui la tua organizzazione ha accesso. |
| **[!UICONTROL Gruppi di account]** | Indica il numero di gruppi di account raggruppati dal processo di apprendimento automatico degli account correlati. |
| **[!UICONTROL Gruppi a account singolo]** | Indica il numero di conti non raggruppati insieme ad altri conti. |
| **[!UICONTROL Dimensioni gruppo più grandi]** | Indica la dimensione del gruppo di account correlati più grande. La dimensione massima consentita del gruppo è 30. |
| **[!UICONTROL Dimensione media del gruppo]** | Indica la dimensione media dei gruppi di account correlati nell&#39;organizzazione. |
| **[!UICONTROL Ultima esecuzione riuscita]** | Indica la data e l&#39;ora dell&#39;ultima esecuzione del processo di account correlati completata. |
| **[!UICONTROL Stato]** | Indica lo stato (riuscito, non riuscito o elaborazione) del processo di account correlato. |
| **[!UICONTROL Messaggio]** | Indica un messaggio di errore o di avviso per una particolare esecuzione di un processo. |

## Lead per l’arricchimento del profilo corrispondente al conto {#lead-to-account-matching}

La [!UICONTROL Corrispondenza lead a conto] il dashboard mostra le metriche di base e lo stato giornaliero di esecuzione dei processi specifico per [Corrispondenza lead a conto](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md) arricchimento del profilo.

![Lead per l’arricchimento del profilo corrispondente al conto](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

Le metriche seguenti sono disponibili per i processi di arricchimento dei profili che corrispondono a quelli per lead to account:

| Metrica | Descrizione |
| --------- | ---------- |
| **[!UICONTROL Totale persone con conti]** | Indica il numero totale di persone associate a un account. |
| **[!UICONTROL Conti totali]** | Indica il numero totale di conti. |
| **[!UICONTROL Persone esistenti con contabilità]** | Indica il numero di persone già associate a un account dalle origini dati. |
| **[!UICONTROL Persone confrontate]** | Indica il numero di persone a cui è stato effettuato il confronto con un account. |
| **[!UICONTROL Persone senza pari]** | Indica il numero di persone non associate a un account. |
| **[!UICONTROL Ultima esecuzione riuscita]** | Indica la data e l&#39;ora dell&#39;ultimo lead riuscito per l&#39;esecuzione del processo di corrispondenza del conto. |
| **[!UICONTROL Stato]** | Indica lo stato (riuscito, non riuscito o elaborazione) del processo di corrispondenza del conto clienti lead a. |

## Arricchimento del profilo di punteggio predittivo del lead e del conto {#predictive-lead-to-account-scoring}

La [!UICONTROL Punteggio predittivo di lead e account] il dashboard mostra le metriche di base e lo stato giornaliero di esecuzione dei processi specifico per [Punteggio predittivo di lead e account](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md) arricchimento del profilo.

![Arricchimento del profilo di punteggio predittivo del lead e del conto](/help/dataflows/assets/ui/b2b/predictive-lead-and-account-scoring.png)

Le metriche seguenti sono disponibili per i processi di arricchimento del profilo di lead predittivi e di punteggio dell’account:

| Metrica | Descrizione |
| --------- | ---------- |
| **[!UICONTROL Inizio processo]** | Indica la data e l&#39;ora di inizio dell&#39;esecuzione del processo di valutazione predittiva del lead e del conto. |
| **[!UICONTROL Tempo di elaborazione]** | Tempo totale impiegato per il completamento del processo. |
| **[!UICONTROL Nome punteggio]** | Nome del punteggio del processo. |
| **[!UICONTROL Tipo di profilo]** | Il tipo di punteggio: <ul><li>Utente</li><li>Account</li></ul>. |
| **[!UICONTROL Tipo di processo]** | Tipo di processo:<ul><li>Punteggio</li><li>Formazione</li>. |
| **[!UICONTROL Stato]** | Indica lo stato (riuscito, non riuscito o elaborazione) del processo di valutazione predittiva del lead e del conto. |

## Controlli dell&#39;interfaccia utente {#ui-controls}

Questa sezione descrive diverse opzioni dell’interfaccia utente nell’interfaccia di monitoraggio, che consentono di filtrare le metriche visualizzate sulla pagina.

Usa l’icona a forma di freccia (![icona a forma di freccia](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png)) per espandere o ignorare la scheda nella parte superiore dello schermo, che mostra immediatamente informazioni sui processi di arricchimento del profilo.

![Registrazione dello schermo che mostra il controllo dell’interfaccia utente dell’icona a forma di freccia.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Utilizza la **[!UICONTROL Metriche e grafici]** per ignorare la visualizzazione che visualizza le metriche più recenti.

![Registrazione su schermo che mostra l’interruttore metriche e grafici.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Utilizza la **[!UICONTROL Mostra solo errori]** per visualizzare solo i processi di arricchimento del profilo non riusciti.

![Registrazione dello schermo che mostra solo l’interruttore Show Failure (Mostra errori).](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, ora puoi monitorare e comprendere correttamente le metriche per i processi di arricchimento dei profili. Per ulteriori informazioni, consulta i seguenti documenti:

* [Account correlati in Real-time CDP B2B](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Scheda Account correlati nella guida dell’interfaccia utente del profilo account](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Lead per corrispondenza account in Real-time CDP B2B](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
* [Punteggio predittivo di lead e account in Real-time CDP B2B](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
