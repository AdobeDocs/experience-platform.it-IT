---
keywords: Experience Platform;home;argomenti popolari;spazio dei nomi;spazio dei nomi;spazi dei nomi;spazi dei nomi;spazio dei nomi;spazio dei nomi identità;spazio dei nomi identità;identità;identità;identità
solution: Experience Platform
title: Creare un namespace personalizzato nell’API del servizio Identity
topic-legacy: API guide
description: Utilizzando l’API dello spazio dei nomi identità, puoi creare uno spazio dei nomi di identità personalizzato che sarà disponibile solo per la tua organizzazione.
exl-id: 6015a225-4508-49cc-9dda-fb9f73a8746c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 3%

---

# Creare uno spazio dei nomi personalizzato nell’API del servizio Identity

Utilizzando l’API [!DNL Identity Namespace], puoi creare uno spazio dei nomi di identità personalizzato che sarà disponibile solo per la tua organizzazione.

Per raccomandazioni sulla creazione di spazi dei nomi personalizzati, consulta la [documentazione sulle domande frequenti del servizio Identity](../troubleshooting-guide.md).

>[!NOTE]
>
>I namespace sono un qualificatore per le identità. Una volta creato uno spazio dei nomi, questo non può essere eliminato.

**Formato API**

```http
POST /idnamespace/identities
```

**Richiesta**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/idnamespace/identities \
  -H 'Accept-Encoding: gzip, deflate' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
        "name": "Loyalty Member",
        "code": "Loyalty",
        "description": "Loyalty Program Member ID",
        "idType": "Cross_device"
      }'
```

**Risposta**

```json
{
    "updateTime": 1576286879075,
    "code": "Loyalty",
    "status": "ACTIVE",
    "description": "Loyalty Program Member ID",
    "id": 10093197,
    "createTime": 1576286879075,
    "idType": "Cross_device",
    "name": "Loyalty Member",
    "custom": true
}
```

## Passaggi successivi

Procedi all&#39;esercitazione successiva su [elencare l&#39;ID nativo di un&#39;identità](./list-native-id.md)
