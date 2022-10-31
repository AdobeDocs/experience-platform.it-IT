---
keywords: Experience Platform;home;argomenti popolari;intervallo di date
title: Panoramica degli avvisi
description: Scopri gli avvisi di Adobe Experience Platform, inclusa la struttura della definizione delle regole di avviso.
feature: Alerts
exl-id: c38a93c6-1618-4ef9-8f94-41c7ab4af43c
source-git-commit: b1c82169056e66b9cdcf99f73daa7d37a3a01600
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 5%

---

# Panoramica sugli avvisi

Adobe Experience Platform ti consente di abbonarti a avvisi basati su eventi relativi alle attività Adobe Experience Platform. Gli avvisi riducono o eliminano la necessità di eseguire il polling [[!DNL Observability Insights] API](../api/overview.md) per verificare se un processo è stato completato, se è stata raggiunta una determinata fase cardine all’interno di un flusso di lavoro o se si sono verificati errori.

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

Gli avvisi possono essere inviati a un webhook configurato per facilitare l&#39;automazione efficiente del monitoraggio delle attività. Per ricevere avvisi tramite webhook, è necessario registrare il webhook per gli avvisi Platform in Adobe Developer Console. Consulta la guida su [sottoscrizione ad Adobi I/O notifiche evento](./subscribe.md) per passaggi specifici.

### Interfaccia utente della piattaforma {#ui}

L’interfaccia utente di Platform consente di visualizzare gli avvisi ricevuti e di gestire le regole per gli avvisi. Il video seguente fornisce un’introduzione a queste funzionalità.

>[!VIDEO](https://video.tv.adobe.com/v/336218?quality=12&learn=on)

Per utilizzare gli avvisi nell’interfaccia utente di Platform, è necessario che le seguenti autorizzazioni di controllo accessi siano abilitate tramite Adobe Admin Console:

| Autorizzazione | Descrizione |
| --- | --- |
| Visualizzare gli avvisi | Consente di visualizzare i messaggi di avviso ricevuti. |
| Visualizza cronologia avvisi* | Consente di visualizzare la cronologia degli avvisi ricevuti tramite [!UICONTROL Avvisi] scheda . |
| Gestisci avvisi* | Consente di abilitare e disabilitare le regole di avviso tramite la [!UICONTROL Avvisi] scheda . |
| Risolvi avvisi* | Consente di risolvere gli avvisi attivati tramite [!UICONTROL Avvisi] scheda . |

{style=&quot;table-layout:auto&quot;}

**Per accedere al [!UICONTROL Avvisi] È inoltre necessario disporre dell’autorizzazione Visualizza avvisi in combinazione con una delle altre autorizzazioni.*

>[!NOTE]
>
>Per ulteriori informazioni su come gestire le autorizzazioni in Platform, consulta la [documentazione sul controllo degli accessi](../../access-control/ui/overview.md).

Con l&#39;autorizzazione Visualizza avvisi, è possibile visualizzare gli avvisi ricevuti selezionando l&#39;icona della campana (![Icona Bell](../images/alerts/overview/icon.png)) nell’angolo in alto a destra.

![](../images/alerts/overview/ui.png)

>[!NOTE]
>
> Seleziona un avviso per passare a un dashboard correlato e ottenere informazioni più dettagliate sul motivo per cui l’avviso è stato attivato.

Inoltre, il [!UICONTROL Avvisi] La scheda nell’interfaccia utente consente ai singoli utenti di effettuare l’abbonamento a specifici tipi di avvisi e consente agli amministratori di abilitare o disabilitare completamente le regole di avviso. Consulta la sezione [Guida all’interfaccia utente](./ui.md) per ulteriori informazioni sulla gestione degli avvisi.

## Passaggi successivi

Leggendo questo documento, sei stato introdotto agli avvisi di Platform e al loro ruolo nell’ecosistema di Platform. Per informazioni su come ricevere e gestire gli avvisi, consulta la documentazione sul processo collegata a in questa panoramica.
