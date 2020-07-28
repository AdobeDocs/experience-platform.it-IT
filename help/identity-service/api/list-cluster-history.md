---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ottenere la cronologia cluster di un'identità
topic: API guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 1%

---


# Ottenere la cronologia cluster di un&#39;identità

Le identità possono spostare i cluster nel corso di diverse esecuzioni del grafico del dispositivo. [!DNL Identity Service] fornisce visibilità alle associazioni cluster di una determinata identità nel tempo.

Utilizzate `graph-type` il parametro opzionale per indicare il tipo di output da cui ottenere il cluster. Le opzioni sono:

- `None` - Non eseguire cuciture di identità.
- `Private Graph` - Eseguire la cucitura dell&#39;identità in base al grafico dell&#39;identità privata. Se non `graph-type` viene fornito alcun valore, questo è il valore predefinito.

## Ottenere la cronologia del cluster di una singola identità

**Formato API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/history
```

**Richiesta**

Opzione 1: Specificate l&#39;identità come spazio dei nomi (`nsId`, per ID) e come valore ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opzione 2: Specificate l&#39;identità come spazio dei nomi (`ns`, per nome) e come valore ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opzione 3: Specificate l&#39;identità come XID (`xid`). Per ulteriori informazioni su come ottenere l&#39;XID di un&#39;identità, consulta la sezione di questo documento relativa al [recupero dell&#39;XID per un&#39;identità](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## Ottenere la cronologia del cluster di più identità

Utilizzate il `POST` metodo come equivalente batch del `GET` metodo descritto sopra per restituire le storie cluster di identità multiple.

>[!NOTE]
>
>La richiesta non deve contenere più di 1000 identità. Le richieste che superano 1000 identità genereranno un codice di stato di 400.

**Formato API**

```http
POST https://platform-va7.adobe.io/data/core/identity/clusters/history
```

**Corpo della richiesta**

Opzione 1: Fornire un elenco di XID per i quali recuperare i membri del cluster.

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

Opzione 2: Fornite un elenco di identità come ID compositi, in cui ogni nome indica il valore ID e lo spazio dei nomi per codice dello spazio dei nomi.

```shell
{
    "compositeXids": [{
            "ns": "AdCloud",
            "id": "WRbM7AAAAJ_PBZHl"
        },
        {
            "ns": "AddCloud",
            "id": "WY-RNgAAArI4rGBo"
        }
    ]
}
```

**Richiesta**

**Richiesta stub**

L’utilizzo dell’ `x-uis-cst-ctx: stub` intestazione restituirà una risposta con stub. Si tratta di una soluzione temporanea per facilitare i primi progressi nello sviluppo dell&#39;integrazione, mentre i servizi sono in fase di completamento. Questa opzione verrà rimossa quando non sarà più necessario.

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-uis-cst-ctx: stub' \
  -d '{
        "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
        "graph-type": "Private Graph"
      }'
```

**Utilizzo di XID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
        "graph-type": "Private Graph"
      }' | json_pp
```

**Utilizzo di UID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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
        "graph-type": "Private Graph"
      }' | json_pp
```

**Risposta**

```json
{
    "version": 1,
    "xidsClusterHistory": [{
            "xid": "GZsBQnHQaGtL46ZKSvO9bNRE1DcUyQA",
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNgAAArI4rGBo"
            },
            "clusterHistory": [{
                    "clusterId": "4c686f23-0871-41c2-b4f4-adef89f6bd2c",
                    "cRecordedTS": "1504741401382"
                },
                {
                    "clusterId": "29bf066c-971a-11e7-abc4-cec278b6b50a",
                    "cRecordedTS": "1502063001629"
                },
                {
                    "clusterId": "aeb2f60c-b0f1-446a-91dd-d28ab6a44ff9",
                    "cRecordedTS": "1499384601763"
                }
            ]
        },
        {
            "xid": "CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8",
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNgAAArI4rGBo"
            },
            "clusterHistory": [{
                "clusterId": "4c686f23-0871-41c2-b4f4-adef89f6bd2c",
                "cRecordedTS": "1504741401937"
            }]
        }
    ],
    "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
    "unprocessedNids": [{
        "nsid": 411,
        "id": "WY-RNgAAArI4rGBo"
    }]

}
```

>[!NOTE]
>
>La risposta avrà sempre una voce per ogni XID fornito nella richiesta, a prescindere dal fatto che gli XID di una richiesta appartengano allo stesso cluster o che uno o più di essi abbiano alcun cluster associato.

## Passaggi successivi

Passare all&#39;esercitazione successiva per [elencare i mapping di identità](./list-identity-mappings.md)