---
title: Panoramica Del Connettore Source Di Azure Data Lake Storage Gen2
description: Scopri come collegare Azure Data Lake Storage Gen2 a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 424d7278-44d9-4653-82c0-eb21cbb9b623
source-git-commit: 8877e7dceeebfb1d4f31b63fef4544a69c72b38e
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---

# Connettore di archiviazione Azure Data Lake Gen2

Adobe Experience Platform fornisce connettività nativa per i provider di cloud come AWS, [!DNL Google Cloud Platform] e [!DNL Azure], consentendo di portare i dati da questi sistemi.

Le origini di archiviazione cloud possono salvare i tuoi dati in Experience Platform senza dover scaricare, formattare o caricare. I dati acquisiti possono essere formattati come XDM JSON, XDM Parquet o delimitati. Ogni passaggio del processo viene integrato nel flusso di lavoro Origini. Experience Platform consente di inserire dati da [!DNL Azure Data Lake Storage Gen2] (ADLS Gen2) tramite batch.

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Per ulteriori informazioni, vedere la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md).

>[!IMPORTANT]
>
>L&#39;origine [!DNL Azure Data Lake Storage Gen2] non supporta la connettività della stessa area per Experience Platform. Se l&#39;istanza [!DNL Azure] utilizza la stessa area di rete di Experience Platform, non è possibile stabilire una connessione alle origini Experience Platform. Attualmente, è supportata solo la connettività tra aree geografiche.

## Vincoli di denominazione per file e directory

Di seguito è riportato un elenco di vincoli di cui è necessario tenere conto per la denominazione del file di archiviazione cloud o della directory.

- I nomi dei componenti di directory e file non possono superare i 255 caratteri.
- I nomi di file e directory non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
- I seguenti caratteri URL riservati devono essere correttamente preceduti dall&#39;escape: `! ' ( ) ; @ & = + $ , % # [ ]`
- I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
- Caratteri di percorso URL non validi non consentiti. I punti di codice come `\uE000`, sebbene validi nei nomi di file NTFS, non sono caratteri Unicode validi. Inoltre, alcuni caratteri ASCII o Unicode, come i caratteri di controllo (da 0x00 a 0x1F, \u0081, ecc.), non sono consentiti. Per le regole che regolano le stringhe Unicode in HTTP/1.1, vedere [RFC 2616, Sezione 2.2: Regole di base](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Non sono consentiti i seguenti nomi di file: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carattere punto (.) e due caratteri punto (..).

## Connetti [!DNL Azure Data Lake Storage Gen2] a Experience Platform

>[!NOTE]
>
>L&#39;entità servizio utilizzata per la creazione di un account [!DNL Azure Data Lake Storage Gen2] deve avere almeno il ruolo **Reader dati BLOB di archiviazione** assegnato dal controllo di accesso (IAM)

La documentazione seguente fornisce informazioni su come connettere [!DNL Azure Data Lake Storage Gen2] ad Experience Platform utilizzando le API o l&#39;interfaccia utente:

### Utilizzo delle API

- [Crea una connessione di base  [!DNL Azure Data Lake Storage Gen2]  utilizzando l&#39;API del servizio Flusso](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [Esplorare la struttura dati e il contenuto di un’origine di archiviazione cloud utilizzando l’API del servizio Flusso](../../tutorials/api/explore/cloud-storage.md)
- [Creare un flusso di dati per un’origine di archiviazione cloud utilizzando l’API del servizio Flusso](../../tutorials/api/collect/cloud-storage.md)

### Utilizzo dell’interfaccia utente

- [Crea una connessione di origine  [!DNL Azure Data Lake Storage Gen2]  nell&#39;interfaccia utente](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [Creare un flusso di dati per una connessione all’archiviazione cloud nell’interfaccia utente](../../tutorials/ui/dataflow/batch/cloud-storage.md)
