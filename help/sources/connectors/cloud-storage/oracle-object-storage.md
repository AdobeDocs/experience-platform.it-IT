---
keywords: Experience Platform;home;argomenti comuni;Oracle Object Storage;oracle object storage
solution: Experience Platform
title: Panoramica del connettore Source di Oracle Object Storage
description: Scopri come collegare Oracle Object Storage a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 5e8b85c8-9f01-49a6-9556-7b9c7518fb4b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# Connettore Oracle Object Storage

Adobe Experience Platform fornisce connettività nativa per i provider cloud come AWS, [!DNL Google Cloud Platform], consentendo di inserire in Experience Platform i dati di tali sistemi per l&#39;utilizzo in servizi e destinazioni downstream.

Le origini di archiviazione cloud possono inserire i dati in Experience Platform senza dover scaricare, formattare o caricare. I dati acquisiti possono essere formattati come XDM JSON, XDM Parquet o delimitati. Ogni fase del processo viene integrata nel flusso di lavoro delle origini. Experience Platform consente di inserire dati da [!DNL Oracle Object Storage] tramite batch.

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Per ulteriori informazioni, consulta il documento [elenco consentiti indirizzo IP](../../ip-address-allow-list.md).

## Vincoli di denominazione per file e directory

Di seguito è riportato un elenco di vincoli di cui è necessario tenere conto per la denominazione del file di archiviazione cloud o della directory:

- I nomi dei componenti di directory e file non possono superare i 255 caratteri.
- I nomi di file e directory non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
- I seguenti caratteri URL riservati devono essere correttamente preceduti dall&#39;escape: `! ' ( ) ; @ & = + $ , % # [ ]`
- I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
- Caratteri di percorso URL non validi non consentiti. I punti di codice come `\uE000`, sebbene validi nei nomi di file NTFS, non sono caratteri Unicode validi. Inoltre, alcuni caratteri ASCII o Unicode non sono consentiti, ad esempio i caratteri di controllo (da 0x00 a 0x1F, \u0081, ecc.). Per le regole che regolano le stringhe Unicode in HTTP/1.1, vedere [RFC 2616, Sezione 2.2: Regole di base](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Non sono consentiti i seguenti nomi di file: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carattere punto (.) e due caratteri punto (..).

## Connetti [!DNL Oracle Object Storage] ad Experience Platform

La documentazione seguente fornisce informazioni su come collegare Oracle Object Storage a Adobe Experience Platform utilizzando le API o l’interfaccia utente:

### Utilizzo delle API

- [Creare una connessione di base di Oracle Object Storage utilizzando l’API del servizio Flow](../../tutorials/api/create/cloud-storage/oracle-object-storage.md)
- [Esplorare la struttura dati e il contenuto di un’origine di archiviazione cloud utilizzando l’API del servizio Flusso](../../tutorials/api/explore/cloud-storage.md)
- [Creare un flusso di dati per un’origine di archiviazione cloud utilizzando l’API del servizio Flusso](../../tutorials/api/collect/cloud-storage.md)

### Utilizzo dell’interfaccia utente

- [Creare una connessione sorgente di Oracle Object Storage nell’interfaccia utente](../../tutorials/ui/create/cloud-storage/oracle-object-storage.md)
- [Creare un flusso di dati per una connessione all’archiviazione cloud nell’interfaccia utente](../../tutorials/ui/dataflow/batch/cloud-storage.md)
