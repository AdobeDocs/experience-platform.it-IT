---
keywords: ' Experience Platform;home;argomenti popolari;catalogo;protezione dei dati;dati di crittografia lago'
solution: Experience Platform
title: Protezione dei dati in Adobe Experience Platform
topic: data protection
description: Tutti i dati persistenti nel Data Lake sono crittografati, memorizzati e gestiti in un account Microsoft Azure Data Lake Storage isolato univoco per l'organizzazione. Il diagramma di flusso del processo seguente illustra come i dati vengono assimilati, elaborati, crittografati e persistenti da  Experience Platform.
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---


# Protezione dei dati in Adobe Experience Platform

Tutti i dati acquisiti e utilizzati da Adobe Experience Platform vengono memorizzati in [!DNL Data Lake], un archivio dati altamente granulare contenente tutti i dati gestiti da [!DNL Platform], indipendentemente dall&#39;origine o dal formato del file. Tutti i dati persistenti in [!DNL Data Lake] sono crittografati, memorizzati e gestiti in un account [!DNL Microsoft Azure Data Lake] di storage isolato, univoco per l&#39;organizzazione.

Il diagramma di flusso del processo seguente illustra come i dati vengono assimilati, elaborati, crittografati e persistenti da [!DNL Experience Platform]:

![](images/data-protection/flow.png)

Per informazioni dettagliate sulla cifratura dei dati a riposo in [!DNL Data Lake Storage], consultare il documento relativo alla crittografia dei dati in Azure Data Lake Storage](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption). [ Per informazioni su come i dati a riposo vengono crittografati in [!DNL Cosmos DB], vedere il documento sulla crittografia [dei dati in Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest).