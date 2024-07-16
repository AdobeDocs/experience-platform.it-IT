---
keywords: Experience Platform;home;argomenti popolari;identità;identità
solution: Experience Platform
title: Elenca mappature identità
description: Una mappatura è una raccolta di tutte le identità in un cluster, per uno spazio dei nomi specificato.
role: Developer
exl-id: db80c783-620b-4ba3-b55c-75c1fd6e90b1
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 3%

---

# Elencare mappature identità

Una mappatura è una raccolta di tutte le identità in un cluster, per uno spazio dei nomi specificato.

## Ottenere una mappatura identità per una singola identità

Considerata un’identità, recupera tutte le identità correlate dallo stesso spazio dei nomi rappresentato dall’identità nella richiesta.

**Formato API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/mapping
```

**Richiesta**

Opzione 1: specificare l&#39;identità come spazio dei nomi (`nsId`, per ID) e valore ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opzione 2: specificare l&#39;identità come spazio dei nomi (`ns`, per nome) e valore ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opzione 3: specificare l&#39;identità come XID (`xid`). Per ulteriori informazioni su come ottenere XID di un&#39;identità, consulta la sezione di questo documento che descrive [come ottenere XID per un&#39;identità](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### Ottenere mappature di identità per più identità

Utilizzare il metodo `POST` come equivalente batch del metodo `GET` descritto in precedenza per recuperare mappature per più identità.

>[!NOTE]
>
>La richiesta non deve indicare più di 1000 identità. Le richieste che superano le 1000 identità restituiranno il codice di stato 400.

**Formato API**

```http
POST https://platform.adobe.io/data/core/identity/mappings
```

**Corpo della richiesta**

Opzione 1: fornire un elenco di XID per i quali recuperare le mappature.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

Opzione 2: fornisci un elenco di identità come ID compositi, in cui ciascuna di esse nomina il valore ID e lo spazio dei nomi in base all’ID dello spazio dei nomi. In questo esempio viene illustrato l&#39;utilizzo di questo metodo durante la sovrascrittura del valore predefinito `graph-type` di &quot;Private Graph&quot;.

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

**Utilizzo di UID**

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

Se non sono state trovate identità correlate con l&#39;input fornito, viene restituito un codice di risposta `HTTP 204` senza contenuto.

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

- `lastAssociationTime`: il timestamp dell&#39;ultima associazione dell&#39;identità di input a questa identità.
- `regions`: fornisce `regionId` e `lastAssociationTime` per la posizione in cui è stata visualizzata l&#39;identità.

## Passaggi successivi

Procedi all&#39;esercitazione successiva per [elencare gli spazi dei nomi disponibili](./list-namespaces.md).
