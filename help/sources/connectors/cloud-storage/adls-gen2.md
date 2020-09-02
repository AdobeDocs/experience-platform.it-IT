---
keywords: Experience Platform;home;popular topics;Azure Data Lake Storage Gen2;ADLS-Gen2;adls gen2;ADLS Gen2
solution: Experience Platform
title: Connettore Azure Data Lake Storage Gen2
topic: overview
description: La documentazione seguente fornisce informazioni su come collegare Azure Data Lake Storage Gen2 alla piattaforma utilizzando le API o l'interfaccia utente.
translation-type: tm+mt
source-git-commit: d42351c194bb5a11f3175535de83fbd3b6ac58d2
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---


# Connettore Azure Data Lake Storage Gen2

Adobe Experience Platform offre connettività nativa per fornitori di cloud come AWS [!DNL Google Cloud Platform]e [!DNL Azure], consentendo di portare i dati da questi sistemi.

Le origini di archiviazione cloud possono importare i tuoi dati [!DNL Platform] senza bisogno di scaricare, formattare o caricare. I dati ingeriti possono essere formattati come JSON XDM, parquet XDM o delimitati. Ogni fase del processo è integrata nel flusso di lavoro Origini. [!DNL Platform] consente di inserire i dati da [!DNL Azure Data Lake Storage Gen2] (ADLS-Gen2) attraverso i batch.

## Indirizzo IP  elenco consentiti

I seguenti indirizzi IP devono essere aggiunti a un elenco consentiti  prima di utilizzare i connettori di origine. Se non si aggiungono al elenco consentiti  gli indirizzi IP specifici per la regione, potrebbero verificarsi errori o prestazioni insufficienti quando si utilizzano le origini.

### Regione degli Stati Uniti d&#39;America

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### Europa occidentale

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### Australia Est

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

## Limitazioni per la denominazione di file e directory

Di seguito è riportato un elenco di vincoli per i quali è necessario tenere conto al momento di denominare il file di archiviazione o la directory cloud.

- I nomi di directory e componenti file non possono superare i 255 caratteri.
- I nomi di directory e file non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
- I seguenti caratteri URL riservati devono essere preceduti da una corretta escape: `! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
- Caratteri di percorso URL non validi. I punti di codice come `\uE000`, pur essendo validi nei nomi file NTFS, non sono caratteri Unicode validi. Inoltre, non sono consentiti caratteri ASCII o Unicode, come caratteri di controllo (da 0x00 a 0x1F, \u0081, ecc.). Per le regole che governano le stringhe Unicode in HTTP/1.1, vedere [RFC 2616, Sezione 2.2: Regole](https://www.ietf.org/rfc/rfc2616.txt) di base e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- I seguenti nomi di file non sono consentiti: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punto (..) e due punti (..).

## Connetti [!DNL Azure Data Lake Storage Gen2] a [!DNL Platform]

La documentazione seguente fornisce informazioni su come connettersi [!DNL Azure Data Lake Storage Gen2] all&#39; [!DNL Platform] utilizzo delle API o dell&#39;interfaccia utente:

### Utilizzo delle API

- [Creare un connettore ADLS-Gen2 utilizzando l&#39;API del servizio di flusso](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [Esplora un sistema di archiviazione cloud utilizzando l&#39;API del servizio di flusso](../../tutorials/api/explore/cloud-storage.md)
- [Raccolta di dati di archiviazione cloud tramite l&#39;API del servizio di flusso](../../tutorials/api/collect/cloud-storage.md)

## Utilizzo dell’interfaccia

- [Creare un connettore di origine ADLS-Gen2 nell&#39;interfaccia utente](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [Configurare un flusso di dati per un connettore di archiviazione cloud nell&#39;interfaccia utente](../../tutorials/ui/dataflow/batch/cloud-storage.md)