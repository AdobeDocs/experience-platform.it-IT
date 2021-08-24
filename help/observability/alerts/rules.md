---
keywords: Experience Platform;home;argomenti popolari;intervallo di date
title: Regole di avviso standard
description: 'Il presente documento illustra le regole di avviso predefinite fornite dall''Experience Platform. '
source-git-commit: 8c00fb98a213b578f6970c1e1978f0159f8f38df
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 13%

---


# Regole di avviso standard

Adobe Experience Platform fornisce diverse regole di avviso predefinite che è possibile abilitare per la propria organizzazione. La tabella seguente illustra i dettagli delle regole di segnalazione fornite in Adobe. Per informazioni generali sugli avvisi nell&#39;Experience Platform, consulta la [panoramica degli avvisi](./overview.md).

| Regola | Descrizione | Frequenza di valutazione | Ripeti finestra |
| --- | --- | --- | --- |
| Soglia di adesione superata | Questo avviso viene attivato quando il numero di profili creati supera l’80% dell’adesione dell’organizzazione. | 30 secondi | N/D |
| Nessuna attività di acquisizione nelle ultime 24 ore | Questo avviso viene attivato quando non sono stati acquisiti nuovi dati negli ultimi 24 ore. | 1 giorno | 1 giorno |
| L&#39;origine SFTP non ha acquisito dati | Questo avviso viene attivato quando un [sorgente SFTP](../../sources/connectors/cloud-storage/sftp.md) non ha acquisito dati entro un determinato periodo di tempo. | 1 giorno | 1 giorno |
| Tasso di errore di acquisizione superato | Questo avviso viene attivato quando il tasso di errore per l’inserimento dei dati supera il 20%. | 30 secondi | 30 secondi |
| Messaggio feed | Questo avviso si verifica quando un messaggio di feed di condivisione delle identità è stato inviato a un utente utilizzando [Segment Match](../../segmentation/ui/segment-match.md). | N/D | N/D |
| Accesso ai feed revocato | Questo avviso viene attivato quando un altro utente di Platform revoca l’accesso a un feed di condivisione delle identità utilizzando [Segment Match](../../segmentation/ui/segment-match.md). | N/D | N/D |
| Feed modificato | Questo avviso viene attivato quando un feed di condivisione delle identità viene modificato da un utente che utilizza [Corrispondenza segmento](../../segmentation/ui/segment-match.md). | N/D | N/D |
| Feed condivisi | Questo avviso viene attivato quando un utente condivide un nuovo feed in [Corrispondenza segmento](../../segmentation/ui/segment-match.md). | N/D | N/D |
| Richiesta di collegamento | Questo avviso si attiva quando un utente richiede di connettersi per la condivisione di partner. | N/D | N/D |
| Azione collegamento | Questo avviso si attiva quando un utente accetta una richiesta di connessione per la condivisione di partner. | N/D | N/D |
| Definizione del segmento disabilitata | Questo avviso viene attivato quando la definizione di un segmento è disabilitata. | N/D | N/D |
| Ritardo processo segmento | Questo avviso viene attivato quando il completamento di un processo del segmento richiede più di 150 minuti. | 30 secondi | 3 ore |
| Errore di esecuzione del flusso di origini | Questo avviso viene attivato quando si verifica un errore durante l’acquisizione dei dati da una connessione sorgente. | N/D | N/D |
| Esecuzione flusso origini completata | Questo avviso viene attivato quando i dati vengono acquisiti correttamente da una connessione sorgente. | N/D | N/D |

{style=&quot;table-layout:auto&quot;}