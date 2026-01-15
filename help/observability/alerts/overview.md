---
keywords: Experience Platform;home;argomenti popolari;intervallo date
title: Panoramica degli avvisi
description: Scopri gli avvisi di Adobe Experience Platform, inclusa la struttura della definizione delle regole di avviso.
feature: Alerts
exl-id: c38a93c6-1618-4ef9-8f94-41c7ab4af43c
source-git-commit: f33bcf982216d25e514992d5ebf978b5535abd77
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 12%

---

# Panoramica sugli avvisi

>[!NOTE]
>
>Poiché gli avvisi sono supportati sia nelle sandbox di produzione che in quelle di sviluppo, è possibile abbonarsi a essi in qualsiasi sandbox. Quando viene reimpostata una sandbox, vengono reimpostati anche tutti gli avvisi di abbonamento e, quando viene eliminata una sandbox, tutti gli avvisi di abbonamento vengono eliminati.

Adobe Experience Platform consente di iscriverti agli avvisi basati su eventi per varie attività di Experience Platform. Gli avvisi riducono o eliminano la necessità di interrogare l’[[!DNL Observability Insights] API](../api/overview.md) per verificare se un processo è stato completato, se è stata raggiunta una determinata milestone all’interno di un flusso di lavoro o se si sono verificati errori.

Quando viene raggiunto un determinato set di condizioni nelle operazioni di Experience Platform (ad esempio un potenziale problema quando il sistema supera una soglia), Experience Platform può inviare messaggi di avviso a tutti gli utenti dell’organizzazione che si sono iscritti a tali condizioni. Questi messaggi possono ripetersi in un intervallo di tempo predefinito fino alla risoluzione dell&#39;avviso.

Questo documento fornisce una panoramica degli avvisi in Adobe Experience Platform, inclusa la struttura della definizione delle regole di avviso.

## Confronto tra avvisi una tantum e ripetuti

Gli avvisi di Experience Platform possono essere inviati una sola volta oppure possono essere ripetuti in un intervallo predefinito finché non vengono risolti. I casi di utilizzo di ciascuna di queste opzioni sono destinati a differire nei seguenti modi:

| Avviso una tantum | Avviso ripetuto |
| --- | --- |
| Non indica necessariamente un problema. | Indica uno stato potenzialmente indesiderato. |
| Non si ripete. | Può ripetere se la condizione anomala persiste. |
| Gli esempi includono:<ul><li>Acquisizione dei dati completata.</li><li>Esecuzione di una query completata.</li><li>I dati sono stati eliminati.</li></ul> | Gli esempi includono:<ul><li>La durata dell’acquisizione supera il livello di servizio concordato (SLA).</li><li>L’ingestione giornaliera non si è verificata nelle ultime 24 ore.</li><li>Il tasso di errore del processore di flusso è superiore alla soglia configurata.</li></ul> |

{style="table-layout:auto"}

## Anatomia di un avviso

Un avviso può essere suddiviso nei seguenti componenti:

| Componente | Descrizione |
| --- | --- |
| **Metrica** | Un oggetto Observability [metric](../api/metrics.md#available-metrics) il cui valore attiva l&#39;avviso, ad esempio il numero di eventi di acquisizione batch non riusciti (`timeseries.ingestion.dataset.batchfailed.count`). |
| **Condizione** | Condizione correlata alla metrica che attiva l’avviso se viene risolto in true, ad esempio una metrica di conteggio che supera un determinato numero. Questa condizione può essere associata a un intervallo di tempo predefinito. |
| **Finestra** | (Facoltativo) La condizione per un avviso può essere vincolata a un intervallo di tempo predefinito. Ad esempio, un avviso può essere attivato a seconda del numero di batch non riusciti negli ultimi cinque minuti. |
| **Azione** | Quando viene attivato un avviso, viene eseguita un’azione. In particolare, i messaggi vengono inviati ai destinatari applicabili tramite un canale di consegna, ad esempio un webhook preconfigurato o l’interfaccia utente di Experience Platform. |
| **Frequenza** | (Facoltativo) Un avviso può essere configurato per ripetere l’azione a un intervallo definito se la sua condizione rimane true o non è altrimenti risolta. |

{style="table-layout:auto"}

## Ricezione e gestione degli avvisi

Gli avvisi possono essere ricevuti e gestiti tramite due canali:

* [Adobe I/O Events](#events)
* [Interfaccia utente di Experience Platform](#ui)

### Eventi I/O {#events}

Gli avvisi possono essere inviati a un webhook configurato per facilitare l’automazione efficiente del monitoraggio delle attività. Per ricevere gli avvisi tramite webhook, devi registrarlo per gli avvisi di Experience Platform in Adobe Developer Console. Per i passaggi specifici, consulta la guida su [abbonamento alle notifiche degli eventi di Adobe I/O](./subscribe.md).

### Interfaccia utente di Experience Platform {#ui}

L’interfaccia utente di Experience Platform ti consente di visualizzare gli avvisi ricevuti e di gestire le regole degli avvisi. Il video seguente fornisce un’introduzione a queste funzionalità.

>[!VIDEO](https://video.tv.adobe.com/v/336218?quality=12&learn=on)

Per lavorare con gli avvisi nell’interfaccia utente di Experience Platform, è necessario disporre delle seguenti autorizzazioni di controllo degli accessi abilitate tramite Adobe Admin Console:

| Autorizzazione | Descrizione |
| --- | --- |
| Visualizza avvisi | Consente di visualizzare i messaggi di avviso ricevuti. |
| Visualizza cronologia avvisi* | Consente di visualizzare una cronologia degli avvisi ricevuti tramite la scheda [!UICONTROL Alerts]. |
| Gestione avvisi* | Consente di abilitare e disabilitare le regole di avviso tramite la scheda [!UICONTROL Alerts]. |
| Risolvi avvisi* | Consente di risolvere gli avvisi attivati tramite la scheda [!UICONTROL Alerts]. |

{style="table-layout:auto"}

**Per accedere alla scheda [!UICONTROL Alerts], è inoltre necessario disporre dell&#39;autorizzazione Visualizza avvisi in combinazione con una delle altre autorizzazioni.*

>[!NOTE]
>
>Per ulteriori informazioni su come gestire le autorizzazioni in Experience Platform, consulta la [documentazione sul controllo degli accessi](../../access-control/ui/overview.md).

Con l&#39;autorizzazione Visualizza avvisi, è possibile visualizzare gli avvisi ricevuti selezionando l&#39;icona a forma di campana (![icona campana](/help/images/icons/bell.png)) nell&#39;angolo in alto a destra.

![](../images/alerts/overview/ui.png)

>[!NOTE]
>
> Seleziona un avviso per passare a un dashboard correlato e ottenere informazioni più dettagliate sul motivo per cui è stato attivato l’avviso.

Inoltre, la scheda [!UICONTROL Alerts] nell&#39;interfaccia utente consente ai singoli utenti di abbonarsi a tipi di avviso specifici e agli amministratori di abilitare o disabilitare completamente le regole di avviso. Per ulteriori informazioni sulla gestione degli avvisi, consulta la [Guida dell&#39;interfaccia utente](./ui.md).

## Passaggi successivi

Una volta letto questo documento, potrai conoscere gli avvisi di Experience Platform e il loro ruolo nell’ecosistema Experience Platform. Per informazioni su come ricevere e gestire gli avvisi, consulta la documentazione del processo collegata a in questa panoramica.
