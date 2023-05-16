---
description: Per utilizzare Destination SDK, una società partner deve soddisfare i prerequisiti elencati in questo documento.
title: Prerequisiti per l’integrazione
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# Prerequisiti per l’integrazione

Per utilizzare Destination SDK, assicurati di soddisfare i prerequisiti tecnici e di partnership elencati nelle sezioni seguenti.

## Prerequisiti tecnici/API per le destinazioni di streaming {#streaming-prerequisites}

1. Hai un endpoint API REST per Adobe Experience Platform per fornire i seguenti tipi di dati a:
   * informazioni sull’appartenenza al segmento;
   * Informazioni sull’identità del profilo;
   * (Facoltativo) Attributi aggiuntivi per l’arricchimento del profilo.
2. L’endpoint API REST supporta i protocolli di autenticazione di base, il token portatore o OAuth 2.0.
3. (Facoltativo) Per la gestione programmatica dei metadati è disponibile un endpoint API o API per la creazione/aggiornamento/eliminazione di segmenti.

## Prerequisiti tecnici per le destinazioni batch {#batch-prerequisites}

1. Hai una posizione di destinazione ospitata su [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage], [!DNL SFTP], [!DNL Google Cloud]o un privato [!DNL Data Landing Zone], in cui puoi ricevere i file esportati da Experience Platform.
2. La piattaforma di destinazione può acquisire i file nel formato configurato tramite il [opzioni di formattazione dei file](functionality/destination-server/file-formatting.md) in Destination SDK per le destinazioni batch.
3. (Facoltativo) Hai un segmento creato/recuperato/aggiornato/eliminato ([!DNL CRUD]) Endpoint API o API per la gestione programmatica dei metadati.

## Prerequisiti per la partnership {#partnership-prerequisites}

Se sei un fornitore di software indipendente (ISV) o un integratore di sistema (SI) che desidera utilizzare Destination SDK, leggi i requisiti di partnership per gli ISV e gli SI nella [sezione accesso](overview.md#get-access).
