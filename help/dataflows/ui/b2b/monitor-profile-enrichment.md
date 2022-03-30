---
description: Utilizza la [!UICONTROL Arricchimento del profilo] dashboard per capire se i processi di arricchimento dei profili sono stati eseguiti e completati correttamente e per visualizzare le metriche di base per misurare l’efficacia degli arricchimenti.
solution: Experience Platform
title: Monitorare i processi di arricchimento dei profili
type: Tutorial
source-git-commit: f3389ef2c2bd9ff52ecde2a4f5fd55e5b86783fc
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---

# Monitorare i processi di arricchimento dei profili nell’interfaccia utente

Utilizza la [!UICONTROL Arricchimento del profilo] dashboard per capire se i processi di arricchimento dei profili sono stati eseguiti e completati correttamente e per visualizzare le metriche di base per misurare l’efficacia degli arricchimenti.

In [Interfaccia utente della piattaforma](https://platform.adobe.com), seleziona **[!UICONTROL Monitoraggio]** dalla navigazione a sinistra per accedere al [!UICONTROL Monitoraggio] dashboard. Nel selettore di visualizzazione, seleziona **Flusso B2B** per visualizzare gli elementi del dashboard specifici per [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  La [!UICONTROL Monitoraggio] Il dashboard include le metriche di base dell&#39;esecuzione riuscita più recente e lo stato del processo giornaliero fino a 90 giorni nel passato. La [!UICONTROL Account correlati] il dashboard mostra le metriche di base e lo stato del lavoro giornaliero specifico per [Account correlati](/help/rtcdp/b2b-ai-ml-services/related-accounts.md) arricchimento del profilo.

![Indicazione visiva su come accedere alla schermata di monitoraggio dei processi di arricchimento del profilo nell’interfaccia utente di Experience Platform.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

I dati nel **[!UICONTROL Metriche]** include le metriche di base dell&#39;ultima esecuzione riuscita del processo Account correlati.

Le metriche seguenti sono disponibili per i processi correlati di arricchimento del profilo di account:

| Metrica | Descrizione |
---------|----------|
| **[!UICONTROL Profili account totali]** | Indica i profili account totali a cui la tua organizzazione ha accesso. |
| **[!UICONTROL Gruppi di account]** | Indica il numero di gruppi di account raggruppati dal processo di apprendimento automatico degli account correlati. |
| **[!UICONTROL Gruppi a account singolo]** | Indica il numero di conti non raggruppati insieme ad altri conti. |
| **[!UICONTROL Dimensioni gruppo più grandi]** | Indica la dimensione del gruppo di account correlati più grande. La dimensione massima consentita del gruppo è 30. |
| **[!UICONTROL Dimensione media del gruppo]** | Indica la dimensione media dei gruppi di account correlati nell&#39;organizzazione. |
| **[!UICONTROL Ultima esecuzione riuscita]** | Indica la data e l&#39;ora dell&#39;ultima esecuzione del processo Account correlati riuscita. |
| **[!UICONTROL Stato]** | Indica lo stato (riuscito, non riuscito o elaborazione) del processo Account correlati. |
| **[!UICONTROL Messaggio]** | Indica un messaggio di errore o di avviso per una particolare esecuzione di un processo. |

## Controlli dell&#39;interfaccia utente {#ui-controls}

Questa sezione descrive diverse opzioni dell’interfaccia utente nell’interfaccia di monitoraggio, che consentono di filtrare le metriche visualizzate sulla pagina.

Usa l’icona a forma di freccia (![icona a forma di freccia](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png)) per espandere o ignorare la scheda nella parte superiore dello schermo, che mostra immediatamente informazioni sui processi di arricchimento del profilo.

![Registrazione dello schermo che mostra il controllo dell’interfaccia utente dell’icona a forma di freccia.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Utilizza la **[!UICONTROL Metriche e grafici]** per ignorare la visualizzazione che visualizza le metriche più recenti.

![Registrazione su schermo che mostra l’interruttore metriche e grafici.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Utilizza la **[!UICONTROL Mostra solo errori]** per visualizzare solo i processi di arricchimento del profilo non riusciti.

![Registrazione dello schermo che mostra solo l’interruttore Show Failure (Mostra errori).](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, ora puoi monitorare e comprendere correttamente le metriche per i processi correlati di arricchimento dei profili degli account. Per ulteriori informazioni, consulta i seguenti documenti:

* [Account correlati in Real-time CDP B2B](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Scheda Account correlati nella guida dell’interfaccia utente del profilo account](/help/rtcdp/accounts/account-profile-ui-guide.md)