---
title: Recupero dell’ID di Experience Cloud
seo-title: SDK Web per Adobe Experience Platform per il recupero dell'Experience Cloud ID
description: Scopri come ottenere Adobe Experience Cloud Id.
seo-description: Scopri come ottenere Adobe Experience Cloud Id.
translation-type: tm+mt
source-git-commit: fc48c11cb1f8a88f9fec8a36646f59f39ac3819f
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 7%

---


# (Beta) Ottenimento dell&#39;Experience Cloud ID

>[!IMPORTANT]
>
>L’SDK Web per Adobe Experience Platform è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e la funzionalità sono soggette a modifiche.

Adobe Experience Cloud utilizza un ID univoco per ogni consumatore. Se desiderate utilizzare questo ID univoco, usate il `getIdentity` comando. `getIdentity` restituisce l’ECID esistente per il visitatore corrente. Per i nuovi visitatori che non dispongono ancora di un ECID, questo comando genera un nuovo ECID.

>[!NOTE]
>
>Questo metodo viene in genere utilizzato con soluzioni personalizzate che richiedono la lettura del Experience Cloud ID. Non viene utilizzato da un&#39;implementazione standard.

```javascript
alloy("getIdentity")
  .then(function(ecid) {
    // This function will get called with Adobe Experience Cloud Id when the command promise is resolved
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information
  })
```
