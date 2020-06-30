---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare uno spazio dei nomi personalizzato
topic: API guide
translation-type: tm+mt
source-git-commit: 6ffdcc2143914e2ab41843a52dc92344ad51bcfb
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 5%

---


# Creazione di uno spazio dei nomi personalizzato

Utilizzando l&#39; [!DNL Identity Namespace] API, potete creare uno spazio nomi identità personalizzato che sarà disponibile solo per la vostra organizzazione.

Per consigli sulla creazione di spazi dei nomi personalizzati, consultate [la documentazione](../troubleshooting-guide.md)Domande frequenti sul servizio identità.

>[!NOTE] Gli spazi dei nomi sono un qualificatore per le identità. Pertanto, una volta creato, lo spazio nomi non può essere eliminato.

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

Passate all&#39;esercitazione successiva per [elencare l&#39;ID nativo di un&#39;identità](./list-native-id.md)