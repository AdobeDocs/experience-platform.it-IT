---
description: Per utilizzare Destination SDK, una società partner deve soddisfare i prerequisiti elencati in questo documento.
title: Prerequisiti per l’integrazione
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: d7c9623619e989a59d72aba74903ffc0e64e7d3c
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Prerequisiti per l’integrazione

Per utilizzare Destination SDK, assicurati di soddisfare i prerequisiti tecnici e di partnership elencati nelle sezioni seguenti.

## Prerequisiti tecnici/API per le destinazioni di streaming {#streaming-prerequisites}

1. Hai un endpoint API REST per Adobe Experience Platform per fornire i seguenti tipi di dati a:
   * informazioni sull’appartenenza al segmento;
   * Informazioni sull’identità del profilo;
   * (Facoltativo) Attributi aggiuntivi per l’arricchimento del profilo.
2. L’endpoint API REST supporta l’autenticazione del portatore di token API o il protocollo di autenticazione OAuth 2.0.
3. (Facoltativo) Per la gestione programmatica dei metadati è disponibile un endpoint API o API per la creazione/aggiornamento/eliminazione di segmenti.

## Prerequisiti tecnici per le destinazioni batch {#batch-prerequisites}

1. Hai una posizione di destinazione ospitata su [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage], SFTP, [!DNL Google Cloud]o un privato [!DNL Data Landing Zone], in cui puoi ricevere i file esportati da Experience Platform.
2. La piattaforma di destinazione può acquisire i file nel formato configurato tramite il [opzioni di formattazione dei file](/help/destinations/destination-sdk/server-and-file-configuration.md#file-configuration) in Destination SDK per le destinazioni batch.
3. (Facoltativo) Hai un segmento per creare/recuperare/aggiornare/eliminare (CRUD) API o un endpoint API per la gestione programmatica dei metadati.

## Prerequisiti per la partnership {#partnership-prerequisites}

Se sei un fornitore di software indipendente (ISV) o un integratore di sistema (SI) che desidera utilizzare Destination SDK, leggi i requisiti di partnership per gli ISV e gli SI nella [sezione accesso](./overview.md#get-access).
