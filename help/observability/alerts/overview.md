---
keywords: Experience Platform;home;argomenti popolari;intervallo di date
title: Panoramica degli avvisi
description: Scopri gli avvisi in Adobe Experience Platform, inclusa la struttura della definizione delle regole di avviso.
feature: Alerts
exl-id: c38a93c6-1618-4ef9-8f94-41c7ab4af43c
source-git-commit: d82487f34c0879ed27ac55e42d70346f45806131
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 3%

---

# Panoramica sugli avvisi

Adobe Experience Platform ti consente di abbonarti a avvisi basati su eventi relativi alle attività Adobe Experience Platform. Gli avvisi riducono o eliminano la necessità di eseguire il polling dell&#39; [[!DNL Observability Insights] API](../api/overview.md) per verificare se un processo è stato completato, se è stata raggiunta una determinata fase cardine all&#39;interno di un flusso di lavoro o se si sono verificati errori.

Quando viene raggiunto un certo set di condizioni nelle operazioni di Platform (ad esempio un potenziale problema in caso di superamento di una soglia), Platform può inviare messaggi di avviso a tutti gli utenti dell’organizzazione che si sono abbonati. Questi messaggi possono ripetersi in un intervallo di tempo predefinito fino alla risoluzione dell’avviso.

Questo documento fornisce una panoramica degli avvisi in Adobe Experience Platform, inclusa la struttura della definizione delle regole di avviso.

## Avvisi una tantum e avvisi ripetuti

Gli avvisi della piattaforma possono essere inviati una sola volta oppure possono essere ripetuti in un intervallo predefinito fino a quando non vengono risolti. I casi d’uso di ciascuna di queste opzioni sono destinati a differire nei seguenti modi:

| Avviso una tantum | Avviso ripetuto |
| --- | --- |
| Non indica necessariamente un problema. | Indica uno stato potenzialmente indesiderato. |
| Non viene ripetuto. | Può ripetersi se la condizione anomala persiste. |
| Gli esempi includono:<ul><li>Acquisizione dati completata.</li><li>Esecuzione di una query completata.</li><li>I dati sono stati eliminati.</li></ul> | Gli esempi includono:<ul><li>La durata dell&#39;acquisizione supera l&#39;accordo sul livello di servizio (SLA).</li><li>L&#39;ingestione giornaliera non è avvenuta nelle ultime 24 ore.</li><li>Il tasso di errore del processore di flusso è superiore alla soglia configurata.</li><li>Il numero totale di profili supera l&#39;adesione.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Anatomia di un avviso

Un avviso può essere suddiviso nei seguenti componenti:

| Componente | Descrizione |
| --- | --- |
| **Metrica** | Osservabilità [metrica](../api/metrics.md#available-metrics) il cui valore attiva l’avviso, ad esempio il numero di eventi di inserimento batch non riusciti (`timeseries.ingestion.dataset.batchfailed.count`). |
| **Condizione** | Una condizione correlata alla metrica che attiva l’avviso se si risolve in true, ad esempio una metrica di conteggio che supera un determinato numero. Questa condizione può essere associata a una finestra temporale predefinita. |
| **Finestra** | (Facoltativo) La condizione per un avviso può essere vincolata a una finestra temporale predefinita. Ad esempio, un avviso può essere attivato a seconda del numero di batch con errore negli ultimi cinque minuti. |
| **Azione** | Quando viene attivato un avviso, viene eseguita un’azione. In particolare, i messaggi vengono inviati ai destinatari applicabili tramite un canale di consegna, ad esempio un webhook preconfigurato o l’interfaccia utente di Experience Platform. |
| **Frequenza** | (Facoltativo) Un avviso può essere configurato per ripetere la propria azione a un intervallo definito se la sua condizione rimane vera o se non viene risolta. |

{style=&quot;table-layout:auto&quot;}

## Ricezione e gestione degli avvisi

Gli avvisi possono essere ricevuti e gestiti tramite due canali:

* [Adobe I/O eventi](#events)
* [Interfaccia utente della piattaforma](#ui)

### Eventi I/O {#events}

Gli avvisi possono essere inviati a un webhook configurato per facilitare l&#39;automazione efficiente del monitoraggio delle attività. Per ricevere avvisi tramite webhook, è necessario registrare il webhook per gli avvisi relativi alla piattaforma in Adobe Developer Console. Per passaggi specifici, consulta la guida sull’ [abbonamento alle notifiche degli eventi di Adobe I/O](./subscribe.md) .

### Interfaccia utente della piattaforma {#ui}

L’interfaccia utente di Platform consente di visualizzare gli avvisi ricevuti e di gestire le regole per gli avvisi. Il video seguente fornisce un’introduzione a queste funzionalità.

>[!VIDEO](https://video.tv.adobe.com/v/336218?quality=12&learn=on)

Per utilizzare gli avvisi nell’interfaccia utente di Platform, è necessario che le seguenti autorizzazioni di controllo accessi siano abilitate tramite Adobe Admin Console:

| Autorizzazione | Descrizione |
| --- | --- |
| Visualizzare gli avvisi | Consente di visualizzare i messaggi di avviso ricevuti. |
| Visualizza cronologia avvisi* | Consente di visualizzare la cronologia degli avvisi ricevuti tramite la scheda [!UICONTROL Avvisi]. |
| Gestisci avvisi* | Consente di abilitare e disabilitare le regole di avviso tramite la scheda [!UICONTROL Avvisi] . |
| Risolvi avvisi* | Consente di risolvere gli avvisi attivati tramite la scheda [!UICONTROL Avvisi] . |

{style=&quot;table-layout:auto&quot;}

**Per accedere alla scheda [!UICONTROL Avvisi], è necessario concedere anche l&#39;autorizzazione Visualizza avvisi in combinazione con una delle altre autorizzazioni.*

>[!NOTE]
>
>Per ulteriori informazioni su come gestire le autorizzazioni in Platform, consulta la [documentazione sul controllo accessi](../../access-control/ui/overview.md).

Con l&#39;autorizzazione Visualizza avvisi, è possibile visualizzare gli avvisi ricevuti selezionando l&#39;icona della campana (![Icona campana](../images/alerts/overview/icon.png)) nell&#39;angolo in alto a destra.

![](../images/alerts/overview/ui.png)

Inoltre, la scheda [!UICONTROL Avvisi] nell’interfaccia utente consente ai singoli utenti di iscriversi a tipi di avvisi specifici e consente agli amministratori di abilitare o disabilitare completamente le regole di avviso. Per ulteriori informazioni sulla gestione degli avvisi, consulta la [guida all’interfaccia utente](./ui.md) .

## Passaggi successivi

Leggendo questo documento, sei stato introdotto agli avvisi di Platform e al loro ruolo nell’ecosistema di Platform. Per informazioni su come ricevere e gestire gli avvisi, consulta la documentazione sul processo collegata a in questa panoramica.
