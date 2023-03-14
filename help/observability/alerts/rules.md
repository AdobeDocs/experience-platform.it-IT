---
keywords: Experience Platform;home;argomenti popolari;intervallo date
title: Regole di avviso standard
description: Questo documento descrive le regole di avviso predefinite fornite dall’Experience Platform.
feature: Alerts
exl-id: b4af1c15-b1bc-4e4b-a447-09cc17a63988
source-git-commit: 6650894c145fd1f42731fd5ed8aeb6e38062aa61
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 1%

---

# Regole di avviso standard

Adobe Experience Platform fornisce diverse regole di avviso predefinite che è possibile abilitare per l’organizzazione. Il presente documento descrive i dettagli di queste regole di avviso fornite dagli Adobi. Per informazioni più generali sugli avvisi in Experience Platform, consulta la sezione [panoramica degli avvisi](./overview.md).

Quando [visualizzazione delle regole di avviso nell’interfaccia utente di Platform](./ui.md), puoi abbonarti a ogni regola singolarmente. Quando si sottoscrivono avvisi tramite [Notifiche di eventi di I/O](./subscribe.md)Tuttavia, le regole di avviso sono organizzate in pacchetti di abbonamento diversi. Nelle tabelle seguenti, ogni regola viene visualizzata con il nome dell’abbonamento all’evento di I/O corrispondente.

## Acquisizione dei dati

Le seguenti regole di avviso sono specifiche per [Acquisizione dei dati](../../ingestion/home.md) e  [sorgenti](../../sources/home.md):

| Iscrizione evento di I/O | Regola di avviso | Descrizione |
| --- | --- | --- |
| Informazioni esecuzione flusso di origine | Inizio esecuzione flusso origini | Questo avviso viene attivato quando una connessione di origine inizia a elaborare i dati. |
| Informazioni esecuzione flusso di origine | Esecuzione del flusso di origini completata | Questo avviso viene attivato quando i dati vengono acquisiti correttamente da una connessione di origine. |
| Ritardi, errori ed errori dell’esecuzione del flusso di origine | Errore di esecuzione del flusso origini | Questo avviso viene attivato quando si verifica un errore durante l’acquisizione dei dati da una connessione di origine. |
| Ritardi, errori ed errori dell’esecuzione del flusso di origine | Ritardo acquisizione | Questo avviso viene attivato quando l’elaborazione di un flusso di acquisizione batch richiede più di 150 minuti. |
| Ritardi, errori ed errori dell’esecuzione del flusso di origine | Acquisizione non riuscita | Questo avviso viene attivato quando il rapporto tra i record non riusciti e tutti i record supera la soglia dello 0,5%. |

{style="table-layout:auto"}

Se in precedenza è stato eseguito l&#39;abbonamento al tipo di avviso seguente, non verranno più ricevuti avvisi in quanto l&#39;avviso è diventato obsoleto:

| Iscrizione evento di I/O | Regola di avviso | Descrizione |
| --- | --- | --- |
| Ritardi, errori ed errori dell’esecuzione del flusso di origine | Mancanza di acquisizione | Questo avviso ti invia un messaggio se l’acquisizione subisce un ritardo di oltre sette ore e nessun dato viene acquisito in Platform. |

{style="table-layout:auto"}

## Servizio Identity

Le seguenti regole di avviso sono specifiche per [Servizio identità](../../identity-service/home.md):

| Iscrizione evento di I/O | Regola di avviso | Descrizione |
| --- | --- | --- |
| Info acquisizione identità | Inizio esecuzione flusso servizio Identity | Questo avviso viene attivato quando un flusso del servizio Identity avvia l’elaborazione dei dati. In altre parole, i dati acquisiti vengono caricati dal Data Lake al servizio Identity. |
| Info acquisizione identità | Esecuzione del flusso del servizio Identity completata | Questo avviso viene attivato quando i dati vengono caricati correttamente dal Data Lake nel servizio Identity. |
| Ritardi, errori ed errori nell’acquisizione dell’identità | Ritardo esecuzione flusso servizio identità | Questo avviso viene attivato quando l’elaborazione di un flusso del servizio Identity richiede più di 150 minuti. |
| Ritardi, errori ed errori nell’acquisizione dell’identità | Errore di esecuzione del flusso del servizio Identity | Questo avviso viene attivato quando si verifica un errore durante l’acquisizione dei dati in Identity Service. |

{style="table-layout:auto"}

## Profilo cliente in tempo reale

Le seguenti regole di avviso sono specifiche per [Profilo cliente in tempo reale](../../profile/home.md):

| Iscrizione evento di I/O | Regola di avviso | Descrizione |
| --- | --- | --- |
| Informazioni sull’acquisizione del profilo | Inizio esecuzione flusso profilo | Questo avviso viene attivato quando un flusso di profilo inizia l’elaborazione dei dati. |
| Informazioni sull’acquisizione del profilo | Esecuzione del flusso di profilo completata | Questo avviso viene attivato quando i dati vengono caricati correttamente nel profilo dal Data Lake. |
| Ritardi, errori ed errori nell’acquisizione del profilo | Ritardo esecuzione flusso profilo | Questo avviso viene attivato quando l’elaborazione del caricamento dei dati dal Data Lake al profilo richiede più di 150 minuti. |
| Ritardi, errori ed errori nell’acquisizione del profilo | Errore di esecuzione del flusso di profilo | Questo avviso viene attivato quando si verifica un errore durante l’acquisizione dei dati nel profilo. |

{style="table-layout:auto"}

## Segmentazione

Le seguenti regole di avviso sono specifiche per [Servizio di segmentazione](../../segmentation/home.md):

| Iscrizione evento di I/O | Regola di avviso | Descrizione |
| --- | --- | --- |
| Informazioni processo valutazione segmento | Inizio processo segmento | Questo avviso viene attivato quando un processo di valutazione del segmento inizia a elaborare i dati. |
| Informazioni processo valutazione segmento | Segment Job Success | Questo avviso viene attivato quando un processo di valutazione del segmento viene completato correttamente. |
| Ritardi, errori ed errori del processo di valutazione del segmento | Ritardo processo segmento | Questo avviso viene attivato quando il completamento di un processo di valutazione di un segmento richiede più di 150 minuti. <br> Verrà visualizzato uno dei seguenti stati: <br>- ATTIVAZIONE - La condizione per il guasto o il ritardo è stata soddisfatta (considerarla in uno stato ATTIVO). <br>- INATTIVO - La condizione non è stata soddisfatta o non è stata risolta (considerarla nello stato RISOLTO). |
| Ritardi, errori ed errori del processo di valutazione del segmento | Errore processo segmento | Questo avviso viene attivato quando un processo di valutazione del segmento genera un errore. |
| Ritardi, errori ed errori del processo di valutazione del segmento | Definizione segmento disabilitata | Questo avviso viene attivato quando la definizione di un segmento è disabilitata a causa di un errore interno. Questo attiva automaticamente una sala da guerra per un team di ingegneri Adobi per indagare sul problema. Questo avviso ha solo scopo informativo e non richiede alcuna azione da parte dell&#39;utente. |

{style="table-layout:auto"}

## Destinazioni

Le seguenti regole di avviso sono specifiche per [destinazioni](../../destinations/home.md):

| Iscrizione evento di I/O | Regola di avviso | Descrizione |
| --- | --- | --- |
| Informazioni sull&#39;esecuzione del flusso di destinazione | Inizio esecuzione flusso di destinazione | Questo avviso viene attivato quando l’esecuzione di un flusso di destinazione inizia ad attivare un segmento. |
| Informazioni sull&#39;esecuzione del flusso di destinazione | Esecuzione del flusso di destinazione completata | Questo avviso viene attivato quando un segmento viene attivato correttamente in una destinazione. |
| Ritardi, errori ed errori dell’esecuzione del flusso di destinazione | Ritardo esecuzione flusso di destinazione | Questo avviso viene attivato quando l’esecuzione di un flusso di destinazione richiede più di 150 minuti per attivare un segmento. |
| Ritardi, errori ed errori dell’esecuzione del flusso di destinazione | Errore di esecuzione del flusso di destinazione | Questo avviso viene attivato quando si verifica un errore durante l’attivazione di un segmento in una destinazione. |
| Ritardi, errori ed errori dell’esecuzione del flusso di destinazione | La frequenza di salto supera la soglia | Questo avviso viene attivato quando il rapporto tra gli ID saltati e gli ID totali supera una soglia. |

{style="table-layout:auto"}

## Servizio query

Le seguenti regole di avviso sono specifiche per [Servizio query](../../query-service/home.md):

| Iscrizione evento di I/O | Regola di avviso | Descrizione |
| --- | --- | --- |
| Informazioni query pianificate da Query Service | Avvio query pianificato di Query Service | Questo avviso viene attivato all&#39;avvio di una query pianificata. |
| Informazioni query pianificate da Query Service | Query Service: query pianificata completata | Questo avviso viene attivato quando un processo di query pianificato viene completato correttamente. |
| Query Service ha pianificato ritardi, errori ed errori nelle query | errore di query pianificata del servizio query | Questo avviso viene attivato quando un processo di query pianificato non riesce. |

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
