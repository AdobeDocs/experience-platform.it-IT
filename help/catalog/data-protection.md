---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Protezione dei dati in Adobe Experience Platform
topic: data protection
translation-type: tm+mt
source-git-commit: edf7cef0991ceef0465d5c1d750bd1885754f716

---


# Protezione dei dati in Adobe Experience Platform

Tutti i dati acquisiti e utilizzati da Adobe Experience Platform sono memorizzati nel Data Lake, un archivio dati altamente granulare contenente tutti i dati gestiti dalla Piattaforma, indipendentemente dall&#39;origine o dal formato di file. Tutti i dati persistenti nel Data Lake sono crittografati, memorizzati e gestiti in un account Microsoft Azure Data Lake Storage isolato univoco per l&#39;organizzazione.

Il seguente diagramma di flusso del processo illustra come i dati vengono assimilati, elaborati, crittografati e memorizzati da Experience Platform:

![](images/data-protection/flow.png)

Per informazioni dettagliate sulla cifratura dei dati a riposo in Archiviazione Data Lake, vedere il documento sulla crittografia [dei dati in Archiviazione](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)Azure Data Lake. Per informazioni su come i dati a riposo sono crittografati nel database Cosmos, vedere il documento sulla crittografia [dei dati nel database](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)Cosmos di Azure.