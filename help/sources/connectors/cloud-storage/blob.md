---
keywords: Experience Platform;home;argomenti popolari;BLOB;BLOB di Azure;BLOB di azzurro
solution: Experience Platform
title: Panoramica del connettore sorgente BLOB di Azure
description: Scopri come collegare Azure Blob a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 62adc74f-3570-42c7-9ae6-3ddbc09eccc7
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Connettore BLOB di Azure

Adobe Experience Platform fornisce connettività nativa per fornitori di cloud come AWS, [!DNL Google Cloud Platform]e [!DNL Azure]. È possibile inserire i dati di questi sistemi in [!DNL Platform].

Le origini di archiviazione cloud possono importare i tuoi dati [!DNL Platform] senza dover scaricare, formattare o caricare. I dati acquisiti possono essere formattati come JSON XDM, Parquet XDM o delimitati. Ogni passaggio del processo viene integrato nel flusso di lavoro Origini . [!DNL Platform] consente di inserire dati da [!DNL Azure Blob] in batch.

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori sorgente, è necessario aggiungere a un elenco consentiti un elenco di indirizzi IP. Se l’utente non aggiunge all’elenco consentiti gli indirizzi IP specifici per l’area geografica, potrebbero verificarsi errori o prestazioni non soddisfacenti durante l’utilizzo delle origini. Consulta la sezione [ELENCO CONSENTITI di indirizzo IP](../../ip-address-allow-list.md) per ulteriori informazioni.

>[!IMPORTANT]
>
>La [!DNL Azure Blob] l&#39;origine non supporta la connettività all&#39;Experience Platform della stessa area. Se l’istanza di Azure utilizza la stessa area di rete di Experience Platform, non è possibile stabilire una connessione alle origini di Experience Platform. Non utilizzare le aree Azure East US 2, Azure West Europe e Azure Australia East durante la configurazione della [!DNL Azure Blob] sorgente. Al momento, è supportata solo la connettività tra aree geografiche.

## Vincoli di denominazione per file e directory

Di seguito è riportato un elenco di vincoli di cui è necessario tenere conto per la denominazione del file di archiviazione cloud o della directory.

- I nomi dei componenti di directory e file non possono superare i 255 caratteri.
- I nomi di directory e file non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
- I seguenti caratteri URL riservati devono essere correttamente preceduti: `! ' ( ) ; @ & = + $ , % # [ ]`
- I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
- Caratteri di percorso URL non validi. Punti di codice come `\uE000`, anche se valido nei nomi file NTFS, non sono caratteri Unicode validi. Inoltre, non sono consentiti alcuni caratteri ASCII o Unicode, come caratteri di controllo (da 0x00 a 0x1F, \u0081, ecc.). Per le regole che governano le stringhe Unicode in HTTP/1.1 vedi [RFC 2616, sezione 2.2: Regole di base](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- I seguenti nomi di file non sono consentiti: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carattere punto (..) e due caratteri punto (.).

## Connetti [!DNL Azure Blob] a [!DNL Platform]

La documentazione seguente fornisce informazioni su come collegare Azure Blob a Adobe Experience Platform utilizzando le API o l’interfaccia utente:

### Utilizzo delle API

- [Creare una connessione di base BLOB di Azure utilizzando l’API del servizio di flusso](../../tutorials/api/create/cloud-storage/blob.md)
- [Esplorare la struttura dati e il contenuto di un’origine di archiviazione cloud utilizzando l’API del servizio di flusso](../../tutorials/api/explore/cloud-storage.md)
- [Creare un flusso di dati per un’origine di archiviazione cloud utilizzando l’API del servizio di flusso](../../tutorials/api/collect/cloud-storage.md)

### Utilizzo dell’interfaccia

- [Creare una connessione sorgente Azure Blob nell’interfaccia utente](../../tutorials/ui/create/cloud-storage/blob.md)
- [Creare un flusso di dati per una connessione di archiviazione cloud nell’interfaccia utente](../../tutorials/ui/dataflow/batch/cloud-storage.md)
