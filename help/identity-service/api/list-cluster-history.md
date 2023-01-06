---
keywords: Experience Platform;home;argomenti popolari;identità;cronologia cluster
solution: Experience Platform
title: Recupero della cronologia cluster di un'identità
description: Le identità possono spostare i cluster nel corso di varie esecuzioni di grafici dei dispositivi. Il servizio Identity fornisce visibilità alle associazioni cluster di una determinata identità nel tempo.
exl-id: e52edb15-e3d6-4085-83d5-212bbd952632
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 3%

---

# Recupero della cronologia cluster di un&#39;identità

Le identità possono spostare i cluster nel corso di varie esecuzioni di grafici dei dispositivi. [!DNL Identity Service] fornisce visibilità alle associazioni cluster di una determinata identità nel tempo.

Usa facoltativo `graph-type` per indicare il tipo di output da cui ottenere il cluster. Le opzioni sono:

- `None` - Non eseguire alcuna unione di identità.
- `Private Graph` - Eseguire unione delle identità in base al grafico di identità privata. Se no `graph-type` è fornito, è l’impostazione predefinita.

## Acquisire la cronologia del cluster di una singola identità

**Formato API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/history
```

**Richiesta**

Opzione 1: Fornisci l’identità come spazio dei nomi (`nsId`, per ID) e il valore ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opzione 2: Fornisci l’identità come spazio dei nomi (`ns`, per nome) e valore ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opzione 3: Fornisci l&#39;identità come XID (`xid`). Per ulteriori informazioni su come ottenere un XID di un&#39;identità, consulta la sezione di questo documento che tratta [ottenimento di un XID per un&#39;identità](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## Ottenere la cronologia cluster di una molteplicità di identità

Utilizza la `POST` come equivalente del lotto `GET` metodo descritto in precedenza per restituire la cronologia cluster di più identità.

>[!NOTE]
>
>La richiesta non deve indicare più di un massimo di 1000 identità. Le richieste che superano 1000 identità risulteranno in un codice di stato 400.

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

Opzione 2: Fornisci un elenco di identità come ID compositi, in cui ognuno dei nomi dei valori ID e dello spazio dei nomi in base al codice dello spazio dei nomi.

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

Utilizzo di `x-uis-cst-ctx: stub` l’intestazione restituirà una risposta con stub. Si tratta di una soluzione temporanea per agevolare lo sviluppo dell&#39;integrazione in tempi brevi, mentre i servizi sono in fase di completamento. Questa opzione diventerà obsoleta se non più necessaria.

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
        "graph-type": "Private Graph"
      }' | json_pp
```

**Utilizzo degli UID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
>La risposta avrà sempre una voce per ogni XID fornito nella richiesta, indipendentemente dal fatto che gli XID di una richiesta appartengano allo stesso cluster o se uno o più hanno un cluster associato affatto.

## Passaggi successivi

Procedi all’esercitazione successiva su [elenco mappature identità](./list-identity-mappings.md)
