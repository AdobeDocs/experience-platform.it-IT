---
keywords: Experience Platform;home;argomenti comuni;archiviazione file di Azure;archiviazione file di Azure
solution: Experience Platform
title: Panoramica del connettore origine archiviazione file di Azure
topic-legacy: overview
description: Scopri come collegare Azure File Storage a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 0a5e9df6-9760-4eeb-86d5-d92d77df3d2b
source-git-commit: 1f9948d6e419ee5d6a021a589378f7aa990b7291
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# Connettore di archiviazione file di Azure

Adobe Experience Platform fornisce connettività nativa per provider di cloud come AWS, [!DNL Google Cloud Platform] e [!DNL Azure], consentendo di estrarre i dati da questi sistemi.

Le origini di archiviazione cloud possono inserire i tuoi dati in [!DNL Platform] senza dover scaricare, formattare o caricare. I dati acquisiti possono essere formattati come JSON XDM, Parquet XDM o delimitati. Ogni passaggio del processo viene integrato nel flusso di lavoro Origini . [!DNL Platform] consente di inserire dati da  [!DNL Azure File Storage] batch.

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori sorgente, è necessario aggiungere a un elenco consentiti un elenco di indirizzi IP. Se l’utente non aggiunge all’elenco consentiti gli indirizzi IP specifici per l’area geografica, potrebbero verificarsi errori o prestazioni non soddisfacenti durante l’utilizzo delle origini. Per ulteriori informazioni, consulta la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md) .

>[!IMPORTANT]
>
>Il connettore di origine [!DNL Azure File Storage] al momento non supporta la connettività della stessa regione a Platform. Ciò significa che, se l’istanza di Azure utilizza la stessa area di rete di Platform, non è possibile stabilire una connessione alle origini di Platform. Al momento, è supportata solo la connettività tra aree geografiche. Per ulteriori informazioni, contatta il tuo Adobe account manager.

## Vincoli di denominazione per file e directory

Di seguito è riportato un elenco di vincoli di cui è necessario tenere conto per la denominazione del file di archiviazione cloud o della directory.

- I nomi dei componenti di directory e file non possono superare i 255 caratteri.
- I nomi di directory e file non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
- I seguenti caratteri URL riservati devono essere correttamente preceduti: `! ' ( ) ; @ & = + $ , % # [ ]`
- I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
- Caratteri di percorso URL non validi. I punti di codice come `\uE000`, mentre sono validi nei nomi di file NTFS, non sono caratteri Unicode validi. Inoltre, non sono consentiti alcuni caratteri ASCII o Unicode, come caratteri di controllo (da 0x00 a 0x1F, \u0081, ecc.). Per le regole che governano le stringhe Unicode in HTTP/1.1, consulta [RFC 2616, Sezione 2.2: Regole di base](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- I seguenti nomi di file non sono consentiti: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carattere punto (..) e due caratteri punto (.).

## Connetti [!DNL Azure File Storage] a [!DNL Platform]

La documentazione seguente fornisce informazioni su come connettersi a [!DNL Azure File Storage] utilizzando le API o l&#39;interfaccia utente:[!DNL Platform]

### Utilizzo delle API

- [Creare una connessione di base Azure File Storage utilizzando l’API del servizio di flusso](../../tutorials/api/create/cloud-storage/azure-file-storage.md)
- [Esplorare la struttura dati e il contenuto di un’origine di archiviazione cloud utilizzando l’API del servizio di flusso](../../tutorials/api/explore/cloud-storage.md)
- [Creare un flusso di dati per un’origine di archiviazione cloud utilizzando l’API del servizio di flusso](../../tutorials/api/collect/cloud-storage.md)

### Utilizzo dell’interfaccia

- [Creare una connessione sorgente Azure File Storage nell’interfaccia utente](../../tutorials/ui/create/cloud-storage/azure-file-storage.md)
- [Creare un flusso di dati per una connessione di archiviazione cloud nell’interfaccia utente](../../tutorials/ui/dataflow/batch/cloud-storage.md)
