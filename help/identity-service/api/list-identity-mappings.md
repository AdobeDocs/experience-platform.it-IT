---
keywords: Experience Platform;home;argomenti popolari;identità;identità
solution: Experience Platform
title: Elencare mappature identità
topic-legacy: API guide
description: Una mappatura è una raccolta di tutte le identità in un cluster, per uno spazio dei nomi specificato.
exl-id: db80c783-620b-4ba3-b55c-75c1fd6e90b1
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 4%

---

# Elencare mappature di identità

Una mappatura è una raccolta di tutte le identità in un cluster, per uno spazio dei nomi specificato.

## Ottenere una mappatura di identità per una singola identità

Dato un&#39;identità, recupera tutte le identità correlate dallo stesso spazio dei nomi rappresentato dall&#39;identità nella richiesta.

**Formato API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/mapping
```

**Richiesta**

Opzione 1: Fornisci l’identità come spazio dei nomi (`nsId`, per ID) e il valore ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opzione 2: Fornisci l’identità come spazio dei nomi (`ns`, per nome) e valore ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opzione 3: Fornisci l&#39;identità come XID (`xid`). Per ulteriori informazioni su come ottenere un XID di un&#39;identità, consulta la sezione di questo documento che tratta [ottenimento di un XID per un&#39;identità](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### Ottieni mappature di identità per più identità

Utilizza la `POST` come equivalente del lotto `GET` metodo descritto in precedenza per recuperare le mappature per più identità.

>[!NOTE]
>
>La richiesta non deve indicare più di un massimo di 1000 identità. Le richieste che superano 1000 identità risulteranno in un codice di stato 400.

**Formato API**

```http
POST https://platform.adobe.io/data/core/identity/mappings
```

**Corpo della richiesta**

Opzione 1: Fornisci un elenco di XID per i quali recuperare le mappature.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

Opzione 2: Fornisci un elenco di identità come ID compositi, in cui ognuno dei nomi dei valori ID e dello spazio dei nomi per ID dello spazio dei nomi. Questo esempio illustra l&#39;utilizzo di questo metodo durante la sovrascrittura dell&#39;impostazione predefinita `graph-type` di &quot;Private Graph&quot;.

```shell
{
    "compositeXids": [{
            "nsid": 411,
            "id": "WRbM7AAAAJ_PBZHl"
        },
        {
            "nsid": 411,
            "id": "WY-RNgAAArI4rGBo"
        }
    ],
    "graph-type": "None"
}
```

**Richiesta**

**Utilizzo di XID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/mappings \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: 111111@AdobeOrg' \
  -d '{
        "xids": ["GesCQXX0CAESEE8wHpswUoLXXmrYy8KBTVgA"],
        "targetNs": "0",
        "graph-type": "Private Graph"
      }' | json_pp
```

**Utilizzo degli UID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/mappings \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: 111111@AdobeOrg' \
  -d '{
            "compositeXids": [{
                    "nsid": 411,
                    "id": "WRbM7AAAAJ_PBZHl"
                },
                {
                    "nsid": 411,
                    "id": "WY-RNgAAArI4rGBo"
                }
            ],
        "targetNs": "0",
        "graph-type": "Private Graph"
      }' | json_pp
```

Se non è stata trovata alcuna identità correlata con l&#39;input fornito, un `HTTP 204` il codice di risposta viene restituito senza contenuto.

**Risposta**

```json
{
    "version": 1,
    "mappings": [{
        "xid": "CAESEPl1uYyma1kMDWxx7dhbwGo",
        "mapping": [{
            "xid": "81218968060697815473313992060878182012",
            "lastAssociationTime": "1493310475047"
        }],
        "compositeXid": {
            "nsid": 411,
            "id": "WY-RNgAAArI4rGBo"
        },
        "mapping": [{
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNchvdsTSJS"
            },
            "lastAssociationTime": "1493310475047"
        }],

        "regions": [{
            "regionId": "10",
            "lastAssociationTime": "1493310475047"
        }]
    }],
    "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
    "unprocessedNids": [{
        "nsid": 411,
        "id": "WY-RNgAAArI4rGBo"
    }]
}
```

- `lastAssociationTime`: La marca temporale all’ultima volta che l’identità di input è stata associata a questa identità.
- `regions`: Fornisce la `regionId` e `lastAssociationTime` per dove è stata vista l&#39;identità.

## Passaggi successivi

Procedi all’esercitazione successiva su [elenco dei namespace disponibili](./list-namespaces.md).
