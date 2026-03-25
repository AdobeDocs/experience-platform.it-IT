---
description: Per utilizzare Destination SDK, un’azienda partner deve soddisfare i prerequisiti elencati in questo documento.
title: Prerequisiti per l’integrazione
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Prerequisiti per l’integrazione

Per utilizzare Destination SDK, accertati di soddisfare i prerequisiti tecnici e di partnership elencati nelle sezioni seguenti.

## Prerequisiti tecnici/API per le destinazioni di streaming {#streaming-prerequisites}

1. È disponibile un endpoint REST API per [!DNL Adobe Experience Platform] per inviare i seguenti tipi di dati a:
   * Informazioni sull’iscrizione del pubblico;
   * Informazioni sull’identità del profilo;
   * (Facoltativo) Attributi aggiuntivi per l’arricchimento del profilo.
2. L’endpoint REST API supporta i protocolli di autenticazione di base, bearer token o OAuth 2.0.
3. (Facoltativo) Disponi di un endpoint API o API per la creazione/aggiornamento/eliminazione di tipi di pubblico per la gestione dei metadati programmatici.

## Prerequisiti tecnici per le destinazioni batch {#batch-prerequisites}

1. Si dispone di una posizione di destinazione ospitata su [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage], [!DNL SFTP], [!DNL Google Cloud] o una [!DNL Data Landing Zone] privata, in cui è possibile ricevere i file esportati da Experience Platform.
2. La piattaforma di destinazione può acquisire i file nel formato configurato tramite le [opzioni di formattazione dei file](functionality/destination-server/file-formatting.md) in Destination SDK per le destinazioni batch.
3. (Facoltativo) Hai un endpoint API o API per creare/recuperare/aggiornare/eliminare ([!DNL CRUD]) tipi di pubblico per la gestione dei metadati programmatici.

## Prerequisiti del partenariato {#partnership-prerequisites}

Se sei un fornitore di software indipendente (ISV) o un integratore di sistemi (SI) che desidera utilizzare Destination SDK, consulta i requisiti di partnership per ISV e SI nella [sezione per ottenere l&#39;accesso](overview.md#get-access).
