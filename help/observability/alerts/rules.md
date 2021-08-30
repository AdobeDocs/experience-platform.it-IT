---
keywords: Experience Platform;home;argomenti popolari;intervallo di date
title: Regole di avviso standard
description: 'Il presente documento illustra le regole di avviso predefinite fornite dall''Experience Platform. '
source-git-commit: de8d8d92622abc75f2d09f4bb771dbe4268d0b38
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 11%

---


# Regole di avviso standard

Adobe Experience Platform fornisce diverse regole di avviso predefinite che è possibile abilitare per la propria organizzazione. La tabella seguente illustra i dettagli delle regole di segnalazione fornite in Adobe. Per informazioni generali sugli avvisi nell&#39;Experience Platform, consulta la [panoramica degli avvisi](./overview.md).

| Regola | Descrizione | Frequenza di valutazione | Ripeti finestra |
| --- | --- | --- | --- |
| Esecuzione flusso origini completata | Questo avviso viene attivato quando i dati vengono acquisiti correttamente da una connessione sorgente. | N/D | N/D |
| Errore di esecuzione del flusso di origini | Questo avviso viene attivato quando si verifica un errore durante l’acquisizione dei dati da una connessione sorgente. | N/D | N/D |
| Ritardo processo segmento | Questo avviso viene attivato quando il completamento di un processo del segmento richiede più di 150 minuti. | 30 secondi | 3 ore |
| Definizione del segmento disabilitata | Questo avviso viene attivato quando la definizione di un segmento è disabilitata. | N/D | N/D |

{style=&quot;table-layout:auto&quot;}

<!-- (Definitions to be added once available)
| Entitlement Threshold Exceeded | This alert triggers when the number of created profiles exceeds 80% of your organization's entitlement. | 30 seconds | N/A |
| No ingestion activity in past 24 hours | This alert triggers when no new data has been ingested in the last 24-hour period. | 1 day | 1 day |
| SFTP source has not ingested data | This alert triggers when an [SFTP source](../../sources/connectors/cloud-storage/sftp.md) has not ingested any data within a certain time period. | 1 day | 1 day |
| Ingestion error rate exceeded | This alert triggers when the error rate for data ingestion exceeds 20%. | 30 seconds | 30 seconds |
| Feed Message | This alert when an identity sharing feed message has been sent to a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Access Revoked | This alert triggers when another Platform user revokes access to an identity sharing feed using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Modified | This alert triggers when an identity sharing feed is modified by a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Shared | This alert triggers when a user shares a new feed in [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Link Request | This alert triggers when a user requests to connect for partner sharing. | N/A | N/A |
| Link Action | This alert triggers when a user accepts a request to connect for partner sharing. | N/A | N/A |
-->
