---
description: Per utilizzare Destination SDK, un'azienda partner deve soddisfare i prerequisiti elencati in questo documento.
title: Prerequisiti per l’integrazione
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: c1ba465a8a866bd8bdc9a2b294ec5d894db81e11
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# Prerequisiti per l’integrazione

Per utilizzare Destination SDK, accertati di soddisfare i prerequisiti tecnici e di partnership elencati nelle sezioni seguenti.

## Prerequisiti tecnici/API per le destinazioni di streaming {#streaming-prerequisites}

1. Hai un endpoint REST API per Adobe Experience Platform per fornire i seguenti tipi di dati a:
   * Informazioni sull’iscrizione del pubblico;
   * Informazioni sull’identità del profilo;
   * (Facoltativo) Attributi aggiuntivi per l’arricchimento del profilo.
2. L’endpoint REST API supporta i protocolli di autenticazione di base, bearer token o OAuth 2.0.
3. (Facoltativo) Disponi di un endpoint API o API per la creazione/aggiornamento/eliminazione di tipi di pubblico per la gestione dei metadati programmatici.

## Prerequisiti tecnici per le destinazioni batch {#batch-prerequisites}

1. Hai una posizione di destinazione ospitata su [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage], [!DNL SFTP], [!DNL Google Cloud], o privato [!DNL Data Landing Zone], dove puoi ricevere i file esportati da Experience Platform.
2. La piattaforma di destinazione può acquisire i file nel formato configurato tramite [opzioni di formattazione file](functionality/destination-server/file-formatting.md) in Destination SDK per le destinazioni batch.
3. (Facoltativo) Hai un pubblico che crea/recupera/aggiorna/elimina ([!DNL CRUD]) Endpoint API o API per la gestione dei metadati programmatici.

## Prerequisiti del partenariato {#partnership-prerequisites}

Se sei un fornitore di software indipendente (ISV) o un integratore di sistemi (SI) che desidera utilizzare Destination SDK, leggi i requisiti di partnership per ISV e SI in [sezione recupero dell’accesso](overview.md#get-access).
