---
title: Monitorare l’acquisizione del profilo di streaming
description: Scopri come utilizzare la dashboard di monitoraggio per monitorare l’acquisizione del profilo di streaming
hide: true
hidefromtoc: true
source-git-commit: 2f78b70761ef676fe4ab61b89b6cbb261c99e9ca
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 3%

---

# Monitorare l’acquisizione del profilo di streaming

Puoi utilizzare il dashboard di monitoraggio nell’interfaccia utente di Adobe Experience Platform per eseguire il monitoraggio in tempo reale dei tassi di acquisizione dei profili di streaming nella tua organizzazione. Utilizza questa funzione per migliorare la trasparenza della velocità effettiva, della latenza e delle metriche di qualità dei dati che circondano i dati in streaming. Inoltre, puoi utilizzare questa funzione per avvisi proattivi e per il recupero di informazioni fruibili al fine di identificare potenziali violazioni della capacità e problemi di acquisizione dei dati.

Leggi la guida seguente per scoprire come utilizzare la dashboard di monitoraggio per monitorare i tassi e le metriche dei processi di acquisizione dei profili di streaming nella tua organizzazione.

## Informazioni sul dashboard di acquisizione del profilo di streaming

Puoi utilizzare tre diverse categorie di metriche nel dashboard di monitoraggio per l&#39;acquisizione del profilo di streaming: [!UICONTROL Throughput], [!UICONTROL Acquisizione] e [!UICONTROL Latenza].

* **Throughput**: selezionare **[!UICONTROL Throughput]** per visualizzare informazioni sulla quantità di dati elaborati da Experience Platform in un periodo di tempo configurato. Fai riferimento a questa metrica per valutare l’efficienza e la capacità del sistema.
   * **Capacità**: la quantità massima di dati che la sandbox può elaborare in condizioni definite.
   * **Throughput richieste**: frequenza con cui gli eventi vengono ricevuti dal sistema di acquisizione, misurata in eventi al secondo.
   * **Velocità effettiva di elaborazione**: velocità alla quale il sistema acquisisce ed elabora correttamente i payload degli eventi in ingresso, misurata in eventi al secondo.
* **Acquisizione**: seleziona [!UICONTROL Acquisizione] per visualizzare informazioni sui processi di acquisizione nella sandbox. Questi processi di acquisizione vengono misurati in tre metriche diverse:
   * **Record creati**: la quantità totale di record creati in un determinato periodo di tempo. Questa metrica rappresenta i processi di acquisizione dei dati corretti nella sandbox.
   * **Record non riusciti**: numero totale di record che non sono stati acquisiti a causa di errori.
   * **Record eliminati**: il numero totale di record eliminati a causa della violazione dei limiti di capacità.
* **Latenza**: selezionare [!UICONTROL Latenza] per visualizzare informazioni sul tempo impiegato da Experience Platform per rispondere a una richiesta o completare un&#39;operazione in un determinato periodo di tempo.

## Metriche di monitoraggio per l’acquisizione del profilo di streaming {#streaming-profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile"
>title="Monitorare l’acquisizione del profilo di streaming"
>abstract="La dashboard di monitoraggio per i profili di streaming visualizza informazioni su velocità effettiva, tassi di acquisizione e latenza. Utilizza questo dashboard per visualizzare, comprendere e analizzare le metriche di elaborazione dei dati. dei profili di streaming in Experience Platform."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_request_throughput"
>title="Velocità effettiva di richiesta"
>abstract="Questa metrica rappresenta il numero di eventi che entrano nel sistema di acquisizione al secondo."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_processing_throughput"
>title="Velocità effettiva di elaborazione"
>abstract="Questa metrica rappresenta il numero di eventi correttamente acquisiti dal sistema ogni secondo."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_p95_ingestion_latency"
>title="Latenza di acquisizione P95"
>abstract="Questa metrica misura la latenza del 95° percentile dal momento in cui un evento arriva in Experience Platform al momento in cui viene correttamente acquisito nell’archivio Profili."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_max_throughput"
>title="Velocità effettiva massima"
>abstract="Questa metrica rappresenta il numero massimo di richieste in entrata al secondo che entrano nell’acquisizione del profilo di streaming."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_ingested"
>title="Record acquisiti"
>abstract="Questa metrica rappresenta il numero totale di record acquisiti nell’archivio profili all’interno di un intervallo di tempo configurato."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_failed"
>title="Record con errori"
>abstract="Questa metrica rappresenta il numero totale di record che, a causa di errori, non sono stati acquisiti nell’archivio profili entro un intervallo di tempo configurato."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_skipped"
>title="Record ignorati"
>abstract="Questa metrica rappresenta il numero totale di record eliminati in un intervallo di tempo configurato a causa di violazioni della configurazione o della capacità."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_error_details"
>title="Dettagli errore"
>abstract="Questa metrica rappresenta il numero di eventi non riusciti a causa di errori."
>text="Learn more in documentation"

| Metrica | Descrizione | Dimensioni | Frequenza di misurazione |
| --- | --- | --- | --- |
| Velocità effettiva di richiesta | Questa metrica rappresenta il numero di eventi che entrano nel sistema di acquisizione al secondo. | Sandbox/Flusso di dati | Monitoraggio in tempo reale con aggiornamento dei dati ogni 60 secondi. |
| Velocità effettiva di elaborazione | Questa metrica rappresenta il numero di eventi correttamente acquisiti dal sistema ogni secondo. | Sandbox/Flusso di dati | Monitoraggio in tempo reale con aggiornamento dei dati ogni 60 secondi. |
| Latenza di acquisizione P95 | Questa metrica misura la latenza del 95° percentile dal momento in cui un evento arriva in Experience Platform al momento in cui viene correttamente acquisito nell’archivio Profili. | Sandbox/Flusso di dati | Monitoraggio in tempo reale con aggiornamento dei dati ogni 60 secondi. |
| Velocità effettiva massima |
| Record acquisiti | Questa metrica rappresenta il numero totale di record acquisiti nell’archivio profili all’interno di un intervallo di tempo configurato. | <ul><li>Sandbox/Flusso di dati</li><li>Esecuzione flusso di dati</li></ul> | <ul><li>Sandbox/Flusso di dati: monitoraggio in tempo reale con aggiornamento dei dati ogni 60 secondi.</li><li>Esecuzione del flusso di dati: raggruppato in 15 minuti.</li></ul> |
| Record con errori | Questa metrica rappresenta il numero totale di record che, a causa di errori, non sono stati acquisiti nell’archivio profili entro un intervallo di tempo configurato. | <ul><li>Sandbox/Flusso di dati</li><li>Esecuzione flusso di dati</li></ul> | <ul><li>Sandbox/Flusso di dati: monitoraggio in tempo reale con aggiornamento dei dati ogni 60 secondi.</li><li>Esecuzione del flusso di dati: raggruppato in 15 minuti.</li></ul> |
| Record ignorati | Questa metrica rappresenta il numero totale di record eliminati in un intervallo di tempo configurato a causa di violazioni della configurazione o della capacità. | <ul><li>Sandbox/Flusso di dati</li><li>Esecuzione flusso di dati</li></ul> | <ul><li>Sandbox/Flusso di dati: monitoraggio in tempo reale con aggiornamento dei dati ogni 60 secondi.</li><li>Esecuzione del flusso di dati: raggruppato in 15 minuti.</li></ul> |
| Dettagli errore | Questa metrica rappresenta il numero di eventi non riusciti a causa di errori. | Esecuzione flusso di dati | Raggruppati in una finestra oraria. |

{style="table-layout:auto"}