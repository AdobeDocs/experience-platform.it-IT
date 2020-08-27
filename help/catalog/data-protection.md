---
keywords: Experience Platform;home;popular topics;catalog;data protection;encryption data lake
solution: Experience Platform
title: Protezione dei dati in Adobe Experience Platform
topic: data protection
description: Tutti i dati persistenti nel Data Lake sono crittografati, memorizzati e gestiti in un account Microsoft Azure Data Lake Storage isolato univoco per l'organizzazione. Il diagramma di flusso del processo seguente illustra come i dati vengono assimilati, elaborati, crittografati e persistenti da  Experience Platform.
translation-type: tm+mt
source-git-commit: 14f99c23cd82894fee5eb5c4093b3c50b95c52e8
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# Protezione dei dati in Adobe Experience Platform

Tutti i dati acquisiti e utilizzati da Adobe Experience Platform sono memorizzati in [!DNL Data Lake], un archivio dati altamente granulare contenente tutti i dati gestiti da [!DNL Platform], indipendentemente dall&#39;origine o dal formato del file. Tutti i dati persistenti nell&#39; [!DNL Data Lake] archivio sono crittografati, memorizzati e gestiti in un account [!DNL Microsoft Azure Data Lake] di archiviazione isolato univoco per l&#39;organizzazione.

Il diagramma di flusso del processo seguente illustra come i dati vengono assimilati, elaborati, crittografati e persistenti tramite [!DNL Experience Platform]:

![](images/data-protection/flow.png)

Per informazioni dettagliate sulla cifratura dei dati a riposo in [!DNL Data Lake Storage], vedere il documento sulla cifratura [dei dati in Azure Data Lake Storage](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption). Per informazioni su come i dati a riposo vengono crittografati in [!DNL Cosmos DB], vedere il documento sulla crittografia [dei dati nel database](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)Cosmos di Azure.