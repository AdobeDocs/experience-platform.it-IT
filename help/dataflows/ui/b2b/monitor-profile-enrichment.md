---
description: Utilizzare il dashboard [!UICONTROL Profile Enrichment] per verificare se i processi di arricchimento dei profili sono stati eseguiti e completati correttamente e per visualizzare le metriche di base per misurare l'efficacia degli arricchimenti.
solution: Experience Platform
title: Monitorare i processi di arricchimento dei profili
type: Tutorial
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 0e993f7d0791f5f6f9dce63eb3848609d892e788
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 1%

---

# Monitorare i processi di arricchimento dei profili nell’interfaccia utente {#monitor-profile-enrichment}

Utilizzare il dashboard [!UICONTROL Profile Enrichment] per verificare se i processi di arricchimento dei profili sono stati eseguiti e completati correttamente e per visualizzare le metriche di base per misurare l&#39;efficacia degli arricchimenti.

Nell&#39;interfaccia utente di [Experience Platform](https://platform.adobe.com), seleziona **[!UICONTROL Monitoring]** dal menu di navigazione a sinistra per accedere al dashboard di [!UICONTROL Monitoring]. Nel selettore di visualizzazione, selezionare **Flusso B2B** per visualizzare gli elementi del dashboard specifici di [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  Il dashboard [!UICONTROL Monitoring] include le metriche di base dell&#39;ultima esecuzione riuscita e lo stato del processo giornaliero fino a 90 giorni nel passato.

## Arricchimento del profilo account correlati {#related-accounts}

Il dashboard [!UICONTROL Related accounts] mostra le metriche di base e lo stato del processo giornaliero specifico per l&#39;arricchimento del profilo [Account correlati](/help/rtcdp/b2b-ai-ml-services/related-accounts.md).

![Indicazione visiva di come accedere alla schermata di monitoraggio dei processi di arricchimento dei profili nell&#39;interfaccia utente di Experience Platform.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

I dati nella scheda **[!UICONTROL Metrics]** includono le metriche di base dell&#39;ultima esecuzione riuscita del processo Account correlati.

Per i processi di arricchimento dei profili degli account correlati sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| --------- | ---------- |
| **[!UICONTROL Total account profiles]** | Indica i profili account totali a cui la tua organizzazione ha accesso. |
| **[!UICONTROL Account groups]** | Indica il numero di gruppi di account raggruppati dal processo di apprendimento automatico degli account correlati. |
| **[!UICONTROL Single-account groups]** | Indica il numero di account non raggruppati con altri account. |
| **[!UICONTROL Largest group size]** | Indica le dimensioni del gruppo di conti correlati più grande. La dimensione massima consentita del gruppo è 30. |
| **[!UICONTROL Median group size]** | Indica la dimensione mediana dei gruppi di account correlati nell&#39;organizzazione. |
| **[!UICONTROL Last successful run]** | Indica la data e l&#39;ora dell&#39;ultima esecuzione riuscita del processo relativo agli account. |
| **[!UICONTROL Status]** | Indica lo stato (riuscito, non riuscito o elaborazione) del processo account correlato. |
| **[!UICONTROL Message]** | Indica un errore o un messaggio di avviso per una determinata esecuzione del processo. |

## Lead per l’arricchimento del profilo di corrispondenza dell’account {#lead-to-account-matching}

Il dashboard [!UICONTROL Lead to account matching] mostra le metriche di base e lo stato di esecuzione dei processi giornalieri specifici per l&#39;arricchimento del profilo [Lead to account matching](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md).

![Lead per l&#39;arricchimento del profilo di corrispondenza dell&#39;account](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

Per i processi di arricchimento dei profili di corrispondenza lead-account sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| --------- | ---------- |
| **[!UICONTROL Total persons with accounts]** | Indica il numero totale di persone associate a un account. |
| **[!UICONTROL Total accounts]** | Indica il numero totale di account. |
| **[!UICONTROL Existing persons with accounts]** | Indica il numero di persone già associate a un account dalle origini dati. |
| **[!UICONTROL Persons matched]** | Indica il numero di persone associate a un account. |
| **[!UICONTROL Persons unmatched]** | Indica il numero di persone che non corrispondono a un account. |
| **[!UICONTROL Last successful run]** | Indica la data e l&#39;ora dell&#39;ultima esecuzione del processo di corrispondenza lead-account completata. |
| **[!UICONTROL Status]** | Indica lo stato (riuscito, non riuscito o elaborazione) del processo di corrispondenza lead-account. |

## Arricchimento del profilo di punteggio lead predittivo e account {#predictive-lead-to-account-scoring}

Il dashboard [!UICONTROL Predictive lead and account scoring] mostra le metriche di base e lo stato dell&#39;esecuzione giornaliera dei processi specifici per l&#39;arricchimento del profilo [Predictive lead and account scoring](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md).

![Arricchimento del profilo del lead predittivo e del punteggio account](/help/dataflows/assets/ui/b2b/predictive-lead-and-account-scoring.png)

Per i processi di arricchimento del profilo di punteggio lead predittivo e account sono disponibili le metriche seguenti:

| Metrica | Descrizione |
| --------- | ---------- |
| **[!UICONTROL Job start]** | Indica la data e l&#39;ora di inizio dell&#39;esecuzione del processo di valutazione del lead predittivo e dell&#39;account. |
| **[!UICONTROL Processing time]** | Tempo totale impiegato per il completamento del processo. |
| **[!UICONTROL Score name]** | Il nome del punteggio del processo. |
| **[!UICONTROL Profile type]** | Tipo di punteggio: <ul><li>Persona</li><li>Account</li></ul>. |
| **[!UICONTROL Job type]** | Tipo di processo:<ul><li>Punteggio</li><li>Addestramento</li>. |
| **[!UICONTROL Status]** | Indica lo stato (completato, non riuscito o in elaborazione) del processo predittivo di valutazione del lead e dell’account. |

## Controlli dell’interfaccia utente {#ui-controls}

In questa sezione vengono descritte diverse opzioni dell’interfaccia utente (UI) nell’interfaccia di monitoraggio, che consentono di filtrare le metriche visualizzate nella pagina.

Utilizza l&#39;icona freccia (![icona freccia](/help/images/icons/chevron-up.png)) per espandere o chiudere la scheda nella parte superiore dello schermo, che mostra immediatamente le informazioni sui processi di arricchimento del profilo.

![Registrazione dello schermo con l&#39;icona freccia Controllo dell&#39;interfaccia utente.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Utilizza l&#39;interruttore **[!UICONTROL Metrics and graphs]** per chiudere la visualizzazione che mostra le metriche più recenti.

![Registrazione dello schermo che mostra l&#39;interruttore delle metriche e dei grafici.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Utilizzare l&#39;interruttore **[!UICONTROL Show failures only]** per visualizzare solo i processi di arricchimento del profilo non riusciti.

![Registrazione dello schermo che mostra solo l&#39;interruttore Mostra errori.](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, ora puoi monitorare e comprendere correttamente le metriche per i processi di arricchimento dei profili. Per ulteriori informazioni, consulta i seguenti documenti:

* [Account correlati in Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Scheda Account correlati nella guida dell’interfaccia utente del profilo account](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Lead per la corrispondenza dell’account in Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
* [Punteggio predittivo di lead e account in Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
