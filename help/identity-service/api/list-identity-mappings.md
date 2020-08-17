---
keywords: Experience Platform;home;popular topics;identity;Identity
solution: Experience Platform
title: Elenca mappature identità
topic: API guide
description: Una mappatura è una raccolta di tutte le identità in un cluster, per uno spazio dei nomi specificato.
translation-type: tm+mt
source-git-commit: c081a7521be9715ca32d35504922a70767924fd7
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 1%

---


# Elenca mappature identità

Una mappatura è una raccolta di tutte le identità in un cluster, per uno spazio dei nomi specificato.

## Ottenere una mappatura identità per una singola identità

Data un&#39;identità, recuperate tutte le identità correlate dallo stesso spazio nomi rappresentato dall&#39;identità nella richiesta.

**Formato API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/mapping
```

**Richiesta**

Opzione 1: Specificate l&#39;identità come spazio dei nomi (`nsId`, per ID) e come valore ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opzione 2: Specificate l&#39;identità come spazio dei nomi (`ns`, per nome) e come valore ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opzione 3: Specificate l&#39;identità come XID (`xid`). Per ulteriori informazioni su come ottenere l&#39;XID di un&#39;identità, consulta la sezione di questo documento relativa al [recupero dell&#39;XID per un&#39;identità](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### Ottenere le mappature di identità per più identità

Utilizzate il `POST` metodo come equivalente batch del `GET` metodo descritto sopra per recuperare mappature per più identità.

>[!NOTE]
>
>La richiesta non deve contenere più di 1000 identità. Le richieste che superano 1000 identità genereranno un codice di stato di 400.

**Formato API**

```http
POST https://platform.adobe.io/data/core/identity/mappings
```

**Corpo della richiesta**

Opzione 1: Fornire un elenco di XID per i quali recuperare le mappature.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

Opzione 2: Fornite un elenco di identità come ID compositi, in cui ogni nome indica il valore ID e lo spazio nomi per ID namespace. Questo esempio illustra come utilizzare questo metodo per sovrascrivere il valore predefinito `graph-type` di &quot;Grafico privato&quot;.

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
        "xids" : ["GesCQXX0CAESEE8wHpswUoLXXmrYy8KBTVgA"],
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

Se non viene trovata alcuna identità correlata con l&#39;input fornito, viene restituito un codice di `HTTP 204` risposta senza contenuto.

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

- `lastAssociationTime`: Il timestamp dell&#39;ultima associazione dell&#39;identità di input a questa identità.
- `regions`: Fornisce il `regionId` e `lastAssociationTime` la posizione in cui è stata visualizzata l&#39;identità.

## Passaggi successivi

Passate all&#39;esercitazione successiva per [elencare gli spazi dei nomi](./list-namespaces.md)disponibili.
