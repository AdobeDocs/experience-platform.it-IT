---
keywords: Experience Platform;home;argomenti popolari;catalogo;protezione dati;crittografia data lake
solution: Experience Platform
title: Protezione dei dati in Adobe Experience Platform
topic-legacy: data protection
description: Tutti i dati persistenti nel Data Lake vengono crittografati, memorizzati e gestiti in un account Microsoft Azure Data Lake Storage isolato univoco per la tua organizzazione. Il diagramma di flusso di processo seguente illustra il modo in cui i dati vengono acquisiti, elaborati, crittografati e mantenuti per Experience Platform.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Protezione dei dati in Adobe Experience Platform

Tutti i dati acquisiti e utilizzati da Adobe Experience Platform vengono memorizzati in [!DNL Data Lake], un archivio dati altamente granulare contenente tutti i dati gestiti da [!DNL Platform], indipendentemente dall’origine o dal formato del file. Tutti i dati memorizzati in [!DNL Data Lake] vengono crittografati, memorizzati e gestiti in un account di archiviazione [!DNL Microsoft Azure Data Lake] isolato univoco per la tua organizzazione.

Il diagramma di flusso di processo seguente illustra come i dati vengono acquisiti, elaborati, crittografati e mantenuti da [!DNL Experience Platform]:

![](images/data-protection/flow.png)

Per informazioni dettagliate su come i dati a riposo sono crittografati in [!DNL Data Lake Storage], consulta il documento sulla crittografia dei dati in Azure Data Lake Storage](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption). [ Per informazioni su come i dati a riposo sono crittografati in [!DNL Cosmos DB], consulta il documento sulla crittografia dei dati in [Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest).
