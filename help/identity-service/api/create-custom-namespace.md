---
keywords: ' Experience Platform;home;argomenti comuni;spazio dei nomi;spazio dei nomi;spazi dei nomi;spazi dei nomi;spazio dei nomi identità;spazio dei nomi identità;identità;identità'
solution: Experience Platform
title: Creare uno spazio dei nomi personalizzato nell'API del servizio identità
topic: API guide
description: Utilizzando l'API Identity Namespace (Spazio nomi identità), potete creare uno spazio nomi identità personalizzato che sarà disponibile solo per la vostra organizzazione.
translation-type: tm+mt
source-git-commit: 73035aec86297cfc4ee9337cf922d599001379c3
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 3%

---


# Creare uno spazio dei nomi personalizzato nell&#39;API del servizio identità

Utilizzando l&#39;API [!DNL Identity Namespace], potete creare uno spazio nomi identità personalizzato che sarà disponibile solo per la vostra organizzazione.

Per le raccomandazioni sulla creazione di spazi dei nomi personalizzati, consultate [la documentazione Domande frequenti sul servizio identità](../troubleshooting-guide.md).

>[!NOTE]
>
>Gli spazi dei nomi sono un qualificatore per le identità. Pertanto, una volta creato, lo spazio nomi non può essere eliminato.

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

Procedete con l&#39;esercitazione successiva su [elencare l&#39;ID nativo di un&#39;identità](./list-native-id.md)