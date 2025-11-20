---
title: Monitorare i tipi di pubblico in streaming
description: Scopri come utilizzare il dashboard di monitoraggio per monitorare i tipi di pubblico valutati utilizzando la segmentazione in streaming
hide: true
hidefromtoc: true
source-git-commit: 6fe0a36a8f2ac2cb954935ee8fe64432442b6e84
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 6%

---


# Monitorare i tipi di pubblico in streaming

intro blurb

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Flussi dati](../home.md): i flussi dati rappresentano processi di dati che trasferiscono informazioni in Experience Platform. Sono configurati in vari servizi per facilitare lo spostamento di dati dai connettori di origine ai set di dati di destinazione, nonché al servizio Identity, al profilo cliente in tempo reale e alle destinazioni.
* [Servizio di segmentazione](../../segmentation/home.md):
* [Capacità](../../landing/license-usage-and-guardrails/capacity.md): in Experience Platform, le capacità ti informano se la tua organizzazione ha superato uno dei tuoi guardrail e ti forniscono informazioni su come risolvere questi problemi.

## Metriche di monitoraggio per il pubblico in streaming {#streaming-audience-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_audience_evaluation_rate"
>title="Tasso di valutazione"
>abstract="Questa metrica rappresenta il numero di record valutati al secondo."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_audience_p95_latency"
>title="Latenza di acquisizione P95"
>abstract="Questa metrica misura la latenza del 95° percentile di un evento in arrivo in Adobe Experience Platform per una valutazione corretta nel pubblico."
>text="Learn more in documentation"

La tabella seguente fornisce informazioni più dettagliate sulle metriche utilizzate per i tipi di pubblico in streaming.

| Metrica | Descrizione | Dimensioni |
| ------ | ----------- | ---------- |
| Tasso di valutazione | Numero di valutazioni del pubblico elaborate al secondo. | Sandbox, set di dati |
| Latenza di acquisizione P95 | Latenza del 95° percentile dell’arrivo dell’evento di successo nel pubblico. | Sandbox, set di dati |
| Record ricevuti | Numero totale di record ricevuti dall’acquisizione in streaming per la segmentazione in streaming durante l’intervallo di tempo selezionato. | Set di dati |
| Record valutati | Numero totale di record valutati **correttamente** tramite segmentazione streaming durante l&#39;intervallo di tempo selezionato. | Set di dati |
| Record con errori | Numero totale di record in cui la valutazione **non è riuscita** nella segmentazione in streaming a causa di errori durante l&#39;intervallo di tempo selezionato. | Set di dati, esecuzione del flusso |
| Record ignorati | Numero totale di record che **hanno saltato** la valutazione nella segmentazione in streaming a causa di errori durante l&#39;intervallo di tempo selezionato. | Set di dati, esecuzione del flusso |
| Profili qualificati | Il numero di profili qualificati per il pubblico durante l’intervallo di tempo selezionato. | Sandbox, pubblico |
| Profili non qualificati | Il numero di profili che sono stati esclusi dal pubblico durante l’intervallo di tempo selezionato. | Sandbox, pubblico |

{style="table-layout:auto"}

## Utilizzare il dashboard di monitoraggio per i tipi di pubblico in streaming {#monitoring-dashboard}

Per accedere al dashboard di monitoraggio per i tipi di pubblico in streaming, passa all&#39;interfaccia utente di Experience Platform, seleziona **[!UICONTROL Monitoring]** dal menu di navigazione a sinistra, quindi seleziona **[!UICONTROL Streaming end-to-end]**.

IMMAGINE

Nella parte superiore del dashboard è presente la scheda della metrica **[!UICONTROL Audiences]**. Visualizza informazioni sul **Tasso di valutazione** per i tipi di pubblico.