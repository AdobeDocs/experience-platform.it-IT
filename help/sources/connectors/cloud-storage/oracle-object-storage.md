---
keywords: ' Experience Platform;home;argomenti più comuni; Archiviazione oggetti Oracli; archiviazione oggetti oracle'
solution: Experience Platform
title: Panoramica del connettore origine archivio oggetti  Oracle
topic: ' - Panoramica'
description: Scoprite come collegare  Archiviazione oggetti di Oracle ad Adobe Experience Platform utilizzando le API o l'interfaccia utente.
translation-type: tm+mt
source-git-commit: 04c605aedd4c52b54d0f075c169ce919650cdee9
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---


# Connettore  Oracle di archiviazione oggetti

Adobe Experience Platform fornisce connettività nativa per i fornitori di cloud come AWS, [!DNL Google Cloud Platform], consentendo di portare i dati da questi sistemi in Piattaforma per l&#39;utilizzo in servizi e destinazioni a valle.

Le origini di archiviazione cloud possono importare i dati in Platform senza bisogno di scaricare, formattare o caricare. I dati ingeriti possono essere formattati come JSON XDM, Parquet XDM o delimitati. Ogni fase del processo è integrata nel flusso di lavoro delle origini. La piattaforma consente di inserire i dati da [!DNL Oracle Object Storage] attraverso i batch.

## Indirizzo IP  elenco consentiti

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti . Se non si aggiungono al elenco consentiti  gli indirizzi IP specifici per la regione, potrebbero verificarsi errori o prestazioni insufficienti quando si utilizzano le origini. Per ulteriori informazioni, vedere il documento [Indirizzo IP  elenco consentiti](../../ip-address-allow-list.md).

## Limitazioni per la denominazione di file e directory

Di seguito è riportato un elenco di vincoli per i quali è necessario tenere conto al momento di denominare il file di archiviazione o la directory cloud:

- I nomi di directory e componenti file non possono superare i 255 caratteri.
- I nomi di directory e file non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
- I seguenti caratteri URL riservati devono essere preceduti da una corretta escape: `! ' ( ) ; @ & = + $ , % # [ ]`
- I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
- Caratteri di percorso URL non validi. I punti di codice come `\uE000`, mentre validi nei nomi file NTFS, non sono caratteri Unicode validi. Inoltre, alcuni caratteri ASCII o Unicode non sono consentiti, come i caratteri di controllo (da 0x00 a 0x1F, \u0081, ecc.). Per le regole che governano le stringhe Unicode in HTTP/1.1, vedere [RFC 2616, Sezione 2.2: Regole di base](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- I seguenti nomi di file non sono consentiti: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, punto (..) e due punti (..).

## Connetti [!DNL Oracle Object Storage] alla piattaforma

La documentazione seguente fornisce informazioni su come collegare  Archiviazione oggetti di Oracle ad Adobe Experience Platform utilizzando le API o l&#39;interfaccia utente:

### Utilizzo delle API

- [Creare una connessione di origine archivio oggetti oggetto di Oracle  utilizzando l&#39;API del servizio di flusso](../../tutorials/api/create/cloud-storage/oracle-object-storage.md)
- [Esplora un sistema di archiviazione cloud utilizzando l&#39;API del servizio di flusso](../../tutorials/api/explore/cloud-storage.md)
- [Raccolta di dati di archiviazione cloud tramite l&#39;API del servizio di flusso](../../tutorials/api/collect/cloud-storage.md)

### Utilizzo dell’interfaccia

- [Creazione di una connessione di origine Archiviazione oggetto  Oracle nell&#39;interfaccia utente](../../tutorials/ui/create/cloud-storage/oracle-object-storage.md)
- [Configurare un flusso di dati per una connessione di archiviazione cloud nell&#39;interfaccia utente](../../tutorials/ui/dataflow/batch/cloud-storage.md)