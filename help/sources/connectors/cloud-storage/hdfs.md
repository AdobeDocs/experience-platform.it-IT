---
keywords: Experience Platform;home;argomenti popolari;HDFS;hdfs;Apache HDFS;apache hdfs
solution: Experience Platform
title: Panoramica del connettore Source Apache HDFS
description: Scopri come collegare Apache HDFS a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 1f156f7b-a19d-4dcf-a51d-ab6cb396d8f7
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 0%

---

# Connettore HDFS [!DNL Apache] (Beta)

>[!NOTE]
>
>Il connettore Apache HDFS è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica origini](../../home.md#terms-and-conditions).

Adobe Experience Platform fornisce connettività nativa per i provider di cloud come AWS, [!DNL Google Cloud Platform] e [!DNL Azure], consentendo di portare i dati da questi sistemi. I dati acquisiti possono essere formattati come JSON, Parquet o delimitati. Il supporto per i provider di archiviazione cloud include [!DNL Apache] HDFS.

## Indirizzo IP inserisco nell&#39;elenco Consentiti

Prima di collegare le origini a Experience Platform, è necessario aggiungere al elenco Consentiti di indirizzi IP specifici per l’area geografica. Per ulteriori informazioni, leggere la guida in [inserire nell&#39;elenco Consentiti degli indirizzi IP per la connessione ad Experience Platform](../../ip-address-allow-list.md).

## Vincoli di denominazione per file e directory

Di seguito è riportato un elenco di vincoli di cui è necessario tenere conto per la denominazione del file di archiviazione cloud o della directory.

- I nomi dei componenti di directory e file non possono superare i 255 caratteri.
- I nomi di file e directory non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
- I seguenti caratteri URL riservati devono essere correttamente preceduti dall&#39;escape: `! ' ( ) ; @ & = + $ , % # [ ]`
- I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
- Caratteri di percorso URL non validi non consentiti. I punti di codice come `\uE000`, sebbene validi nei nomi di file NTFS, non sono caratteri Unicode validi. Inoltre, alcuni caratteri ASCII o Unicode, come i caratteri di controllo (da 0x00 a 0x1F, \u0081, ecc.), non sono consentiti. Per le regole che regolano le stringhe Unicode in HTTP/1.1, vedere [RFC 2616, Sezione 2.2: Regole di base](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Non sono consentiti i seguenti nomi di file: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carattere punto (.) e due caratteri punto (..).

## Connetti [!DNL Apache] HDFS a [!DNL Experience Platform]

La documentazione seguente fornisce informazioni su come collegare [!DNL Apache] HDFS a [!DNL Experience Platform] utilizzando le API o l&#39;interfaccia utente:

### Utilizzo delle API

- [Creare una connessione di base HDFS utilizzando l&#39;API del servizio Flow](../../tutorials/api/create/cloud-storage/hdfs.md)
- [Esplorare la struttura dati e il contenuto di un’origine di archiviazione cloud utilizzando l’API del servizio Flusso](../../tutorials/api/explore/cloud-storage.md)
- [Creare un flusso di dati per un’origine di archiviazione cloud utilizzando l’API del servizio Flusso](../../tutorials/api/collect/cloud-storage.md)

### Utilizzo dell’interfaccia utente

- [Creare una connessione sorgente Apache HDFS nell’interfaccia utente](../../tutorials/ui/create/cloud-storage/hdfs.md)
- [Creare un flusso di dati per una connessione all’archiviazione cloud nell’interfaccia utente](../../tutorials/ui/dataflow/batch/cloud-storage.md)
