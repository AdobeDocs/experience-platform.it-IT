---
description: Utilizza il [!UICONTROL Arricchimento del profilo] dashboard per capire se i processi di arricchimento dei profili sono stati eseguiti e completati correttamente e per visualizzare le metriche di base per misurare l’efficacia degli arricchimenti.
solution: Experience Platform
title: Monitorare i processi di arricchimento dei profili
type: Tutorial
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 2%

---

# Monitorare i processi di arricchimento dei profili nell’interfaccia utente {#monitor-profile-enrichment}

Utilizza il [!UICONTROL Arricchimento del profilo] dashboard per capire se i processi di arricchimento dei profili sono stati eseguiti e completati correttamente e per visualizzare le metriche di base per misurare l’efficacia degli arricchimenti.

In [Interfaccia utente di Platform](https://platform.adobe.com), seleziona **[!UICONTROL Monitorare]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Monitorare] dashboard. Nel selettore della vista, seleziona **Flusso B2B** per visualizzare gli elementi del dashboard specifici di [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  Il [!UICONTROL Monitorare] la dashboard include le metriche di base dell’ultima esecuzione riuscita e lo stato del processo giornaliero fino a 90 giorni nel passato.

## Arricchimento del profilo account correlati {#related-accounts}

Il [!UICONTROL Account correlati] Il dashboard mostra le metriche di base e lo stato del processo giornaliero specifico del [Account correlati](/help/rtcdp/b2b-ai-ml-services/related-accounts.md) arricchimento del profilo.

![Indicazione visiva di come accedere alla schermata di monitoraggio dei processi di arricchimento dei profili nell’interfaccia utente di Experience Platform.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

I dati in **[!UICONTROL Metriche]** La scheda include le metriche di base dell’ultima esecuzione riuscita del processo Account correlati.

Per i processi di arricchimento dei profili degli account correlati sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| --------- | ---------- |
| **[!UICONTROL Profili account totali]** | Indica i profili account totali a cui la tua organizzazione ha accesso. |
| **[!UICONTROL Gruppi di account]** | Indica il numero di gruppi di account raggruppati dal processo di apprendimento automatico degli account correlati. |
| **[!UICONTROL Gruppi per un singolo account]** | Indica il numero di account non raggruppati con altri account. |
| **[!UICONTROL Dimensione gruppo più grande]** | Indica le dimensioni del gruppo di conti correlati più grande. La dimensione massima consentita del gruppo è 30. |
| **[!UICONTROL Dimensione gruppo mediano]** | Indica la dimensione mediana dei gruppi di account correlati nell&#39;organizzazione. |
| **[!UICONTROL Ultima esecuzione riuscita]** | Indica la data e l&#39;ora dell&#39;ultima esecuzione riuscita del processo relativo agli account. |
| **[!UICONTROL Stato]** | Indica lo stato (riuscito, non riuscito o elaborazione) del processo account correlato. |
| **[!UICONTROL Messaggio]** | Indica un errore o un messaggio di avviso per una determinata esecuzione del processo. |

## Lead per l’arricchimento del profilo di corrispondenza dell’account {#lead-to-account-matching}

Il [!UICONTROL Lead per corrispondenza account] il dashboard mostra le metriche di base e lo stato dell’esecuzione giornaliera dei processi specifici del [Lead per corrispondenza account](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md) arricchimento del profilo.

![Lead per l’arricchimento del profilo di corrispondenza dell’account](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

Per i processi di arricchimento dei profili di corrispondenza lead-account sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| --------- | ---------- |
| **[!UICONTROL Totale persone con account]** | Indica il numero totale di persone associate a un account. |
| **[!UICONTROL Account totali]** | Indica il numero totale di account. |
| **[!UICONTROL Persone esistenti con account]** | Indica il numero di persone già associate a un account dalle origini dati. |
| **[!UICONTROL Persone con corrispondenza]** | Indica il numero di persone associate a un account. |
| **[!UICONTROL Persone senza corrispondenza]** | Indica il numero di persone che non corrispondono a un account. |
| **[!UICONTROL Ultima esecuzione riuscita]** | Indica la data e l&#39;ora dell&#39;ultima esecuzione del processo di corrispondenza lead-account completata. |
| **[!UICONTROL Stato]** | Indica lo stato (riuscito, non riuscito o elaborazione) del processo di corrispondenza lead-account. |

## Arricchimento del profilo di punteggio lead predittivo e account {#predictive-lead-to-account-scoring}

Il [!UICONTROL Punteggio predittivo di lead e account] il dashboard mostra le metriche di base e lo stato dell’esecuzione giornaliera dei processi specifici del [Punteggio predittivo di lead e account](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md) arricchimento del profilo.

![Arricchimento del profilo di punteggio lead predittivo e account](/help/dataflows/assets/ui/b2b/predictive-lead-and-account-scoring.png)

Per i processi di arricchimento del profilo di punteggio lead predittivo e account sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| --------- | ---------- |
| **[!UICONTROL Inizio processo]** | Indica la data e l&#39;ora di inizio dell&#39;esecuzione del processo di valutazione del lead predittivo e dell&#39;account. |
| **[!UICONTROL Tempo di elaborazione]** | Tempo totale impiegato per il completamento del processo. |
| **[!UICONTROL Nome punteggio]** | Il nome del punteggio del processo. |
| **[!UICONTROL Tipo di profilo]** | Tipo di punteggio: <ul><li>Persona</li><li>Account</li></ul>. |
| **[!UICONTROL Tipo di processo]** | Tipo di processo:<ul><li>Punteggio</li><li>Formazione</li>. |
| **[!UICONTROL Stato]** | Indica lo stato (completato, non riuscito o in elaborazione) del processo predittivo di valutazione del lead e dell’account. |

## Controlli dell’interfaccia utente {#ui-controls}

In questa sezione vengono descritte diverse opzioni dell’interfaccia utente (UI) nell’interfaccia di monitoraggio, che consentono di filtrare le metriche visualizzate nella pagina.

Utilizza l’icona freccia (![icona freccia](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png)) per espandere o chiudere la scheda nella parte superiore dello schermo, che mostra immediatamente informazioni sui processi di arricchimento del profilo.

![Registrazione dello schermo che mostra l&#39;icona freccia Controllo dell&#39;interfaccia utente.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Utilizza il **[!UICONTROL Metriche e grafici]** attiva per ignorare la visualizzazione che mostra le metriche più recenti.

![Registrazione dello schermo che mostra l’interruttore di metriche e grafici.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Utilizza il **[!UICONTROL Mostra solo errori]** attiva per visualizzare solo i processi di arricchimento del profilo non riusciti.

![Registrazione dello schermo che mostra l’interruttore Mostra solo errori.](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, ora puoi monitorare e comprendere correttamente le metriche per i processi di arricchimento dei profili. Per ulteriori informazioni, consulta i seguenti documenti:

* [Account correlati in Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Scheda Account correlati nella guida dell’interfaccia utente del profilo account](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Lead per la corrispondenza dell’account in Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
* [Punteggio predittivo di lead e account in Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
