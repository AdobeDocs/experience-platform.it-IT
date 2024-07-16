---
keywords: Experience Platform;home;argomenti popolari;spazio dei nomi;spazio dei nomi;spazi dei nomi;spazio dei nomi;spazio dei nomi identità;spazio dei nomi identità;identità;identità;identità
solution: Experience Platform
title: Creare uno spazio dei nomi personalizzato nell’API del servizio Identity
description: Utilizzando l’API Spazio dei nomi identità, puoi creare uno spazio dei nomi identità personalizzato che sarà disponibile solo per la tua organizzazione.
role: Developer
exl-id: 6015a225-4508-49cc-9dda-fb9f73a8746c
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 5%

---

# Creare uno spazio dei nomi personalizzato nell’API del servizio Identity

Utilizzando l&#39;API [!DNL Identity Namespace], puoi creare uno spazio dei nomi di identità personalizzato che sarà disponibile solo per la tua organizzazione.

Per raccomandazioni sulla creazione di spazi dei nomi personalizzati, consulta [la documentazione delle domande frequenti sul servizio Identity](../troubleshooting-guide.md).

>[!NOTE]
>
>Gli spazi dei nomi sono un qualificatore per le identità. Una volta creato, lo spazio dei nomi non può essere eliminato.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Procedi all&#39;esercitazione successiva per [elencare l&#39;ID nativo di un&#39;identità](./list-native-id.md)
