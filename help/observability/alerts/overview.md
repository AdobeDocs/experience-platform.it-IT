---
keywords: Experience Platform;home;argomenti popolari;intervallo date
title: Panoramica degli avvisi
description: Scopri gli avvisi di Adobe Experience Platform, inclusa la struttura della definizione delle regole di avviso.
feature: Alerts
exl-id: c38a93c6-1618-4ef9-8f94-41c7ab4af43c
source-git-commit: cb889a169aa42b761b0eeff5aa7fb771ad6ed4be
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 3%

---

# Panoramica degli avvisi

>[!NOTE]
>
>Gli avvisi non sono supportati nelle sandbox non di produzione. Per abbonarti agli avvisi, devi assicurarti di utilizzare una sandbox di produzione. Tutti gli avvisi di abbonamento verranno reimpostati quando la sandbox viene reimpostata. Tutti gli avvisi di abbonamento verranno eliminati anche quando viene eliminata una sandbox.

Adobe Experience Platform ti consente di abbonarti agli avvisi basati su eventi relativi alle attività di Adobe Experience Platform. Gli avvisi riducono o eliminano la necessità di eseguire il polling [[!DNL Observability Insights] API](../api/overview.md) per verificare se un processo è stato completato, se è stata raggiunta una determinata fase cardine all’interno di un flusso di lavoro o se si sono verificati errori.

Quando viene raggiunto un determinato set di condizioni nelle operazioni di Platform (ad esempio un potenziale problema quando il sistema supera una soglia), Platform può inviare messaggi di avviso a tutti gli utenti dell’organizzazione che si sono iscritti a tali condizioni. Questi messaggi possono ripetersi in un intervallo di tempo predefinito fino alla risoluzione dell&#39;avviso.

Questo documento fornisce una panoramica degli avvisi in Adobe Experience Platform, inclusa la struttura della definizione delle regole di avviso.

## Avvisi una tantum e avvisi ripetuti

Gli avvisi di Platform possono essere inviati una sola volta oppure possono essere ripetuti in un intervallo predefinito finché non vengono risolti. I casi di utilizzo di ciascuna di queste opzioni sono destinati a differire nei seguenti modi:

| Avviso una tantum | Avviso ripetuto |
| --- | --- |
| Non indica necessariamente un problema. | Indica uno stato potenzialmente indesiderato. |
| Non si ripete. | Può ripetere se la condizione anomala persiste. |
| Gli esempi includono:<ul><li>Acquisizione dei dati completata.</li><li>Esecuzione di una query completata.</li><li>I dati sono stati eliminati.</li></ul> | Gli esempi includono:<ul><li>La durata dell’acquisizione supera il contratto del livello di servizio (SLA).</li><li>L’ingestione giornaliera non si è verificata nelle ultime 24 ore.</li><li>Il tasso di errore del processore di flusso è superiore alla soglia configurata.</li><li>Il numero totale di profili supera l’adesione.</li></ul> |

{style="table-layout:auto"}

## Anatomia di un avviso

Un avviso può essere suddiviso nei seguenti componenti:

| Componente | Descrizione |
| --- | --- |
| **Metrica** | Un&#39;osservabilità [metrica](../api/metrics.md#available-metrics) il cui valore attiva l’avviso, ad esempio il numero di eventi di acquisizione batch non riusciti (`timeseries.ingestion.dataset.batchfailed.count`). |
| **Condizione** | Condizione correlata alla metrica che attiva l’avviso se viene risolto in true, ad esempio una metrica di conteggio che supera un determinato numero. Questa condizione può essere associata a un intervallo di tempo predefinito. |
| **Finestra** | (Facoltativo) La condizione per un avviso può essere vincolata a un intervallo di tempo predefinito. Ad esempio, un avviso può essere attivato a seconda del numero di batch non riusciti negli ultimi cinque minuti. |
| **Azione** | Quando viene attivato un avviso, viene eseguita un’azione. In particolare, i messaggi vengono inviati ai destinatari applicabili tramite un canale di consegna, ad esempio un webhook preconfigurato o l’interfaccia utente di Experienci Platform. |
| **Frequenza** | (Facoltativo) Un avviso può essere configurato per ripetere l’azione a un intervallo definito se la sua condizione rimane true o non è altrimenti risolta. |

{style="table-layout:auto"}

## Ricezione e gestione degli avvisi

Gli avvisi possono essere ricevuti e gestiti tramite due canali:

* [Eventi Adobe I/O](#events)
* [Interfaccia utente di Platform](#ui)

### Eventi I/O {#events}

Gli avvisi possono essere inviati a un webhook configurato per facilitare l’automazione efficiente del monitoraggio delle attività. Per ricevere gli avvisi tramite webhook, devi registrarlo per gli avvisi di Platform nella console Adobe Developer. Consulta la guida su [abbonamento a notifiche Adobe I/O Event](./subscribe.md) per passaggi specifici.

### Interfaccia utente di Platform {#ui}

L’interfaccia utente di Platform consente di visualizzare gli avvisi ricevuti e gestire le regole degli avvisi. Il video seguente fornisce un’introduzione a queste funzionalità.

>[!VIDEO](https://video.tv.adobe.com/v/336218?quality=12&learn=on)

Per utilizzare gli avvisi nell’interfaccia utente di Platform, è necessario disporre delle seguenti autorizzazioni di controllo degli accessi abilitate tramite Adobe Admin Console:

| Autorizzazione | Descrizione |
| --- | --- |
| Visualizza avvisi | Consente di visualizzare i messaggi di avviso ricevuti. |
| Visualizza cronologia avvisi* | Consente di visualizzare una cronologia degli avvisi ricevuti tramite [!UICONTROL Avvisi] scheda. |
| Gestione avvisi* | Consente di abilitare e disabilitare le regole di avviso tramite [!UICONTROL Avvisi] scheda. |
| Risolvi avvisi* | Consente di risolvere gli avvisi attivati tramite [!UICONTROL Avvisi] scheda. |

{style="table-layout:auto"}

**Per accedere al [!UICONTROL Avvisi] , è necessario disporre anche dell&#39;autorizzazione Visualizza avvisi in combinazione con una delle altre autorizzazioni.*

>[!NOTE]
>
>Per ulteriori informazioni su come gestire le autorizzazioni in Platform, consulta [documentazione sul controllo degli accessi](../../access-control/ui/overview.md).

Con l’autorizzazione Visualizza avvisi, puoi visualizzare gli avvisi ricevuti selezionando l’icona a forma di campana (![Icona campana](../images/alerts/overview/icon.png)) in alto a destra.

![](../images/alerts/overview/ui.png)

>[!NOTE]
>
> Seleziona un avviso per passare a un dashboard correlato e ottenere informazioni più dettagliate sul motivo per cui è stato attivato l’avviso.

Inoltre, la [!UICONTROL Avvisi] Questa scheda dell’interfaccia utente consente ai singoli utenti di abbonarsi a tipi di avviso specifici e agli amministratori di abilitare o disabilitare completamente le regole degli avvisi. Consulta la [Guida all’interfaccia utente](./ui.md) per ulteriori informazioni sulla gestione degli avvisi.

## Passaggi successivi

Una volta letto questo documento, potrai conoscere gli avvisi di Platform e il loro ruolo nell’ecosistema di Platform. Per informazioni su come ricevere e gestire gli avvisi, consulta la documentazione del processo collegata a in questa panoramica.
