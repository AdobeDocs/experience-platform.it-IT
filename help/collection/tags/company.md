---
title: azienda
description: Ottieni informazioni sull’organizzazione IMS proprietaria della proprietà tag implementata.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 3%

---

# `company`

L&#39;oggetto `_satellite.company` visualizza informazioni relative all&#39;organizzazione IMS proprietaria della proprietà tag.

```ts
readonly _satellite.company: Company
```

## Campi disponibili

I campi seguenti sono disponibili quando si chiama questo oggetto:

```json
{
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "dynamicCdnEnabled": true,
  "cdnAllowList": [
    "assets.adoberesources.cn",
    "assets.adobedtm.com"
  ]
}
```

| Nome | Tipo | Descrizione |
| --- | --- | --- |
| **`orgId`** | `string` | ID dell’organizzazione IMS della proprietà tag. |
| **`dynamicCdnEnabled`** | `boolean` | Determina se la proprietà tag utilizza la funzione di commutazione CDN dinamica di Adobe. Se è impostato su `true`, cambia automaticamente la rete CDN da cui un visitatore richiede il tag in base alla sua posizione. |
| **`cdnAllowList`** | `string[]` | Le CDN consentite da cui caricare la proprietà tag. |

Informazioni simili sono contenute anche in `_satellite._container.company`. Per ulteriori informazioni, vedere [`_container`](container.md).
