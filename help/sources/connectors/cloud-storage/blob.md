---
keywords: Experience Platform;home;argomenti popolari;BLOB;BLOB di Azure;BLOB di Azure
solution: Experience Platform
title: Panoramica del connettore di origine BLOB di Azure
description: Scopri come collegare BLOB di Azure a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 62adc74f-3570-42c7-9ae6-3ddbc09eccc7
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Connettore BLOB di Azure

Adobe Experience Platform fornisce connettività nativa per i provider di cloud come AWS, [!DNL Google Cloud Platform], e [!DNL Azure]. È possibile inserire i dati da questi sistemi in [!DNL Platform].

Le origini di archiviazione cloud possono inserire i tuoi dati in [!DNL Platform] senza dover scaricare, formattare o caricare. I dati acquisiti possono essere formattati come XDM JSON, XDM Parquet o delimitati. Ogni passaggio del processo viene integrato nel flusso di lavoro Origini. [!DNL Platform] consente di inserire dati da [!DNL Azure Blob] attraverso i batch.

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Consulta la [ELENCO CONSENTITI di indirizzo IP](../../ip-address-allow-list.md) per ulteriori informazioni.

>[!IMPORTANT]
>
>Il [!DNL Azure Blob] l&#39;origine non supporta la connettività della stessa area a Experience Platform. Se l’istanza di Azure utilizza la stessa area di rete di Experience Platform, non è possibile stabilire una connessione alle origini di Experience Platform. Non utilizzare le aree geografiche di Azure East US 2, Azure West Europe e Azure Australia East durante la configurazione [!DNL Azure Blob] sorgente. Attualmente, è supportata solo la connettività tra aree geografiche.

## Vincoli di denominazione per file e directory

Di seguito è riportato un elenco di vincoli di cui è necessario tenere conto per la denominazione del file di archiviazione cloud o della directory.

- I nomi dei componenti di directory e file non possono superare i 255 caratteri.
- I nomi di file e directory non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
- I seguenti caratteri URL riservati devono avere un escape corretto: `! ' ( ) ; @ & = + $ , % # [ ]`
- I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
- Caratteri di percorso URL non validi non consentiti. Punti di codice come `\uE000`, anche se valido nei nomi di file NTFS, non è costituito da caratteri Unicode validi. Inoltre, alcuni caratteri ASCII o Unicode, come i caratteri di controllo (da 0x00 a 0x1F, \u0081, ecc.), non sono consentiti. Per le regole che disciplinano le stringhe Unicode in HTTP/1.1, consulta [RFC 2616, sezione 2.2: regole di base](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Non sono consentiti i seguenti nomi di file: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carattere punto (.) e due caratteri punto (..).

## Connetti [!DNL Azure Blob] a [!DNL Platform]

La documentazione seguente fornisce informazioni su come collegare BLOB di Azure a Adobe Experience Platform utilizzando le API o l’interfaccia utente:

### Utilizzo delle API

- [Creare una connessione di base Azure Blob utilizzando l’API del servizio Flusso](../../tutorials/api/create/cloud-storage/blob.md)
- [Esplorare la struttura dati e il contenuto di un’origine di archiviazione cloud utilizzando l’API del servizio Flusso](../../tutorials/api/explore/cloud-storage.md)
- [Creare un flusso di dati per un’origine di archiviazione cloud utilizzando l’API del servizio Flusso](../../tutorials/api/collect/cloud-storage.md)

### Utilizzo dell’interfaccia utente

- [Creare una connessione di origine BLOB di Azure nell’interfaccia utente](../../tutorials/ui/create/cloud-storage/blob.md)
- [Creare un flusso di dati per una connessione all’archiviazione cloud nell’interfaccia utente](../../tutorials/ui/dataflow/batch/cloud-storage.md)
