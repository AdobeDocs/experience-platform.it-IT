---
keywords: Experience Platform;home;argomenti popolari;intervallo di date
title: Regole di avviso standard
description: Il presente documento illustra le regole di avviso predefinite fornite dall'Experience Platform.
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: df79ecac33314cc73ba8ad2508516be706bac767
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 3%

---

# Regole di avviso standard

Adobe Experience Platform fornisce diverse regole di avviso predefinite che è possibile abilitare per la propria organizzazione. Il presente documento illustra i dettagli di queste regole di avviso fornite in Adobe. Per informazioni più generali sugli avvisi in Experience Platform, consulta la sezione [panoramica degli avvisi](./overview.md).

Quando [visualizzazione delle regole di avviso nell’interfaccia utente di Platform](./ui.md), puoi abbonarti a ogni regola singolarmente. Durante l’abbonamento agli avvisi tramite [Notifiche evento I/O](./subscribe.md)Tuttavia, le regole di avviso sono organizzate in diversi pacchetti di abbonamento. Nelle tabelle seguenti, ogni regola viene visualizzata con il nome di sottoscrizione dell’evento I/O corrispondente.

## Acquisizione dei dati

Le seguenti regole di avviso sono specifiche per [Acquisizione dei dati](../../ingestion/home.md) e  [origini](../../sources/home.md):

| Abbonamento evento I/O | Regola di avviso | Descrizione |
| --- | --- | --- |
| Informazioni sull’esecuzione del flusso di origine | Avvio esecuzione flusso origini | Questo avviso viene attivato quando una connessione sorgente avvia l&#39;elaborazione dei dati. |
| Informazioni sull’esecuzione del flusso di origine | Esecuzione flusso origini completata | Questo avviso viene attivato quando i dati vengono acquisiti correttamente da una connessione sorgente. |
| Ritardi, errori ed errori di esecuzione del flusso di origine | Errore di esecuzione del flusso di origini | Questo avviso viene attivato quando si verifica un errore durante l’acquisizione dei dati da una connessione sorgente. |
| Ritardi, errori ed errori di esecuzione del flusso di origine | Ritardo di acquisizione | Questo avviso viene attivato quando l’elaborazione di un flusso di acquisizione batch richiede più di 150 minuti. |
| Ritardi, errori ed errori di esecuzione del flusso di origine | Errore di acquisizione | Questo avviso si attiva quando il rapporto tra record non riusciti e tutti i record supera la soglia dello 0,5%. |

{style=&quot;table-layout:auto&quot;}

Se in precedenza hai effettuato la sottoscrizione al seguente tipo di avviso, non riceverai più avvisi in quanto questo avviso è stato dichiarato obsoleto:

| Abbonamento evento I/O | Regola di avviso | Descrizione |
| --- | --- | --- |
| Ritardi, errori ed errori di esecuzione del flusso di origine | Mancanza di ingestione | Questo avviso invia un messaggio se l’acquisizione viene ritardata di più di sette ore e non vengono acquisiti dati in Platform. |

{style=&quot;table-layout:auto&quot;}

## Servizio Identity

Le seguenti regole di avviso sono specifiche per [Servizio identità](../../identity-service/home.md):

| Abbonamento evento I/O | Regola di avviso | Descrizione |
| --- | --- | --- |
| Informazioni sull’acquisizione di identità | Avvio dell’esecuzione del flusso del servizio Identity | Questo avviso viene attivato quando un’esecuzione di un flusso del servizio Identity avvia l’elaborazione dei dati. In altre parole, i dati acquisiti vengono caricati dal Data Lake nel servizio Identity. |
| Informazioni sull’acquisizione di identità | Esecuzione del flusso del servizio Identity completata | Questo avviso viene attivato quando i dati vengono caricati correttamente dal Data Lake nel servizio Identity. |
| Ritardi, errori ed errori di acquisizione delle identità | Ritardo nell’esecuzione del flusso del servizio Identity | Questo avviso viene attivato quando l’elaborazione di un flusso del servizio Identity richiede più di 150 minuti. |
| Ritardi, errori ed errori di acquisizione delle identità | Errore di esecuzione del flusso del servizio Identity | Questo avviso viene attivato quando si verifica un errore durante l’acquisizione dei dati nel servizio Identity. |

{style=&quot;table-layout:auto&quot;}

## Real-time Customer Profile

Le seguenti regole di avviso sono specifiche per [Profilo cliente in tempo reale](../../profile/home.md):

| Abbonamento evento I/O | Regola di avviso | Descrizione |
| --- | --- | --- |
| Informazioni sull’acquisizione del profilo | Inizio esecuzione flusso profilo | Questo avviso viene attivato quando un’esecuzione di flusso di profilo avvia l’elaborazione dei dati. |
| Informazioni sull’acquisizione del profilo | Flusso di profilo eseguito correttamente | Questo avviso si attiva quando i dati vengono caricati correttamente in Profilo dal Data Lake. |
| Ritardi, errori ed errori di acquisizione del profilo | Ritardo esecuzione flusso profilo | Questo avviso viene attivato quando il caricamento dei dati dal Data Lake nel profilo richiede più di 150 minuti per l’elaborazione. |
| Ritardi, errori ed errori di acquisizione del profilo | Errore di esecuzione del flusso di profilo | Questo avviso si attiva quando si verifica un errore durante l’acquisizione dei dati in Profilo. |

{style=&quot;table-layout:auto&quot;}

## Segmentazione

Le seguenti regole di avviso sono specifiche per [Servizio di segmentazione](../../segmentation/home.md):

| Abbonamento evento I/O | Regola di avviso | Descrizione |
| --- | --- | --- |
| Informazioni sul processo di valutazione del segmento | Avvio processo segmento | Questo avviso viene attivato quando un processo di valutazione dei segmenti avvia l’elaborazione dei dati. |
| Informazioni sul processo di valutazione del segmento | Processo del segmento riuscito | Questo avviso viene attivato quando un processo di valutazione dei segmenti viene completato correttamente. |
| Ritardi, errori ed errori del processo di valutazione del segmento | Ritardo processo segmento | Questo avviso viene attivato quando il completamento di un processo di valutazione dei segmenti richiede più di 150 minuti. |
| Ritardi, errori ed errori del processo di valutazione del segmento | Errore del processo del segmento | Questo avviso si attiva quando un processo di valutazione del segmento genera un errore. |
| Ritardi, errori ed errori del processo di valutazione del segmento | Definizione del segmento disabilitata | Questo avviso si attiva quando una definizione di segmento è disabilitata a causa di un errore interno. Questo attiva automaticamente una stanza di guerra per un team di ingegneri Adobe per indagare il problema. Questo avviso è inteso solo come informativo e non richiede alcuna azione da parte tua. |

{style=&quot;table-layout:auto&quot;}

## Destinazioni

Le seguenti regole di avviso sono specifiche per [destinazioni](../../destinations/home.md):

| Abbonamento evento I/O | Regola di avviso | Descrizione |
| --- | --- | --- |
| Informazioni sull’esecuzione del flusso di destinazione | Inizio esecuzione flusso di destinazione | Questo avviso viene attivato quando un’esecuzione di un flusso di destinazione avvia l’attivazione di un segmento. |
| Informazioni sull’esecuzione del flusso di destinazione | Esecuzione flusso di destinazione completata | Questo avviso viene attivato quando un segmento viene attivato correttamente in una destinazione. |
| Ritardi, errori ed errori di esecuzione del flusso di destinazione | Ritardo esecuzione flusso di destinazione | Questo avviso viene attivato quando un’esecuzione del flusso di destinazione richiede più di 150 minuti per attivare un segmento. |
| Ritardi, errori ed errori di esecuzione del flusso di destinazione | Errore di esecuzione del flusso di destinazione | Questo avviso si attiva quando si verifica un errore durante l&#39;attivazione di un segmento a una destinazione. |
| Ritardi, errori ed errori di esecuzione del flusso di destinazione | Il tasso di Skippage supera la soglia | Questo avviso si attiva quando il rapporto tra ID ignorati e ID totali supera una soglia. |

{style=&quot;table-layout:auto&quot;}

<!-- (Definitions to be added once available)
| Segment Job Delay | This alert triggers when a segment job takes longer than 150 minutes to complete. | N/A | 30 seconds | 3 hours |
| No Ingestion Activity in Past 24 Hours | This alert triggers when no new data has been ingested in the last 24-hour period. | N/A | 1 day | 1 day |
| Ingestion Error Rate Exceeded | This alert triggers when the error rate for data ingestion exceeds the allotted threshold. | 20% | 30 seconds | 30 seconds |
| Entitlement Threshold Exceeded | This alert triggers when the number of created profiles exceeds 80% of your organization's entitlement. | 30 seconds | N/A |
| SFTP source has not ingested data | This alert triggers when an [SFTP source](../../sources/connectors/cloud-storage/sftp.md) has not ingested any data within a certain time period. | 1 day | 1 day |
| Feed Message | This alert when an identity sharing feed message has been sent to a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Access Revoked | This alert triggers when another Platform user revokes access to an identity sharing feed using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Modified | This alert triggers when an identity sharing feed is modified by a user using [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Feed Shared | This alert triggers when a user shares a new feed in [Segment Match](../../segmentation/ui/segment-match.md). | N/A | N/A |
| Link Request | This alert triggers when a user requests to connect for partner sharing. | N/A | N/A |
| Link Action | This alert triggers when a user accepts a request to connect for partner sharing. | N/A | N/A |
-->
