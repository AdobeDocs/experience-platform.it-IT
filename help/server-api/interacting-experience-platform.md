---
title: Interazione con Adobe Experience Platform
description: Scopri come utilizzare l’API server di rete Edge per interagire con Adobe Experience Platform
seo-description: Learn how to use the Edge Network Server API to interact with Adobe Experience Platform
keywords: raccolta dei dati; uscita; analisi; API di rete Adobe Experience Platform Edge;aep
exl-id: c49e40b7-9653-40f1-9db5-8941b20de8a3
source-git-commit: 422f859bef8faf292fd7e5fd8b6a8d31967421c1
workflow-type: tm+mt
source-wordcount: '71'
ht-degree: 1%

---

# Interazione con Adobe Experience Platform

## Panoramica {#overview}

Per abilitare la raccolta dati di Experience Platform, devi prima [configurare il datastream](../edge/fundamentals/datastreams.md) inoltrare gli eventi in set di dati di Experience Platform.

Una volta configurata, la configurazione del datastream deve includere le impostazioni per `com_adobe_experience_platform`, come illustrato nell’esempio seguente:


```json
{
  // datastream config header

  "settings": {
    "com_adobe_experience_platform": {
      "sandboxName": "prod",
      "enabled": true,
      "datasets": {
        "event": {
          "xdmSchema": "https://ns.adobe.com/atag/schemas/35a31609b6d3242736751df469ade031",
          "datasetId": "5f67e6ad9501b0194b5aafb6"
        }
      }
    }

    // other settings
  }
}
```
