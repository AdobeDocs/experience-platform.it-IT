---
keywords: Experience Platform;home;argomenti popolari;elenco identità;elenco cluster
solution: Experience Platform
title: Elencare tutte le identità in un cluster
description: Le identità correlate in un grafico delle identità, indipendentemente dallo spazio dei nomi, sono considerate parte dello stesso "cluster" in tale grafico delle identità. Le opzioni seguenti consentono di accedere a tutti i membri del cluster.
role: Developer
exl-id: 0fb9eac9-2dc2-4881-8598-02b3053d0b31
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 2%

---

# Elenca tutte le identità in un cluster

Le identità correlate in un grafico delle identità, indipendentemente dallo spazio dei nomi, sono considerate parte dello stesso &quot;cluster&quot; in tale grafico delle identità. Le opzioni seguenti consentono di accedere a tutti i membri del cluster.

## Ottenere identità associate per una singola identità

Recuperare tutti i membri del cluster per una singola identità.

È possibile utilizzare il parametro facoltativo `graph-type` per indicare il grafico delle identità da cui ottenere il cluster. Le opzioni sono:

- Nessuno: non eseguire alcuna unione di identità.
- Private Graph (Grafico privato): esegue l’unione delle identità in base al grafico delle identità private. Se non viene fornito alcun `graph-type`, questo è il valore predefinito.

**Formato API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/members?{PARAMETERS}
```

**Richiesta**

Opzione 1: specificare l&#39;identità come spazio dei nomi (`nsId`, per ID) e valore ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opzione 2: specificare l&#39;identità come spazio dei nomi (`ns`, per nome) e valore ID (`id`).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Opzione 3: specificare l&#39;identità come XID (`xid`). Per ulteriori informazioni su come ottenere XID di un&#39;identità, consulta la sezione di questo documento che descrive [come ottenere XID per un&#39;identità](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/members?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## Ottieni identità associate per più identità

Utilizzare `POST` come equivalente batch del metodo `GET` descritto in precedenza per restituire le identità nei cluster di più identità.

>[!NOTE]
>
>La richiesta non deve indicare più di 1000 identità. Le richieste che superano le 1000 identità restituiranno il codice di stato 400.

**Formato API**

```http
POST https://platform-{REGION}.adobe.io/data/core/identity/clusters/members
```

**Richiesta**

Nella richiesta seguente viene illustrato come specificare un elenco di XID per i quali recuperare i membri del cluster.

**Richiesta stub**

L&#39;utilizzo dell&#39;intestazione `x-uis-cst-ctx: stub` restituirà una risposta con stubbed. Si tratta di una soluzione temporanea per agevolare il rapido progresso dello sviluppo dell’integrazione, durante il completamento dei servizi. Se non sarà più necessario, diventerà obsoleto.

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-uis-cst-ctx: stub' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"]
}'
```

**Chiamata tramite XIDs**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
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

**Chiamata tramite UID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/members \
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

**risposta &#39;Stubbed&#39;**

```json
{
   "version": 1,
   "clusters": [{
           "xid": "GZsBQnHQaGtL46ZKSvO9bNRE1DcUyQA",
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": ["e8138f65-d3d3-4485-a7e1-6712e047349d", "21312343536983537571245438594"],
           "members": [{
                   "nsid": 0,
                   "id": "27064814400205787570627663430729680462"
               },
               {
                   "nsid": 411,
                   "id": "86826386186182763871263871263876128612"
               }
           ]
       },
       {
           "xid": "CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8",
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": [],
           "members": []
       }
   ],
   "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
   "unprocessedNids": [{
       "nsid": 411,
       "id": "WY-RNgAAArI4rGBo"
   }]
}
```

**Risposta completa**

```json
{
   "unprocessedXids": [],
   "unprocessedNids": [],
   "version": "1.0.0",
   "clusters": [{
           "xid": "411|WRbM7AAAAJ_PBZHl",
           "members": [
               "411|WRbM7AAAAJ_PBZHl",
               "0|47713142741924778930324734610798294416"
           ],
           "compositeXid": {
               "nsid": 411,
               "id": "WRbM7AAAAJ_PBZHl"
           },
           "members": [{
                   "nsid": 411,
                   "id": "WRbM7AAAAJ_PBZHl"
               },
               {
                   "nsid": 0,
                   "id": "47713142741924778930324734610798294416"
               }
           ]
       },
       {
           "xid": "411|WY-RNgAAArI4rGBo",
           "compositeXid": {
               "nsid": 411,
               "id": "WY-RNgAAArI4rGBo"
           },
           "members": [
               "411|WY-RNgAAArI4rGBo",
               "411|WY-RNgAAArI4rGGy"
           ],
           "members": [{
                   "nsid": 411,
                   "id": "WY-RNgAAArI4rGBo"
               },
               {
                   "nsid": 411,
                   "id": "WY-RNgAAArI4rGGy"
               }
           ]

       }
   ]
}
```

>[!NOTE]
>
>La risposta avrà sempre una voce per ogni XID fornito nella richiesta, indipendentemente dal fatto che gli XID di una richiesta appartengano allo stesso cluster o che a uno o più di essi sia associato un cluster.

## Passaggi successivi

Procedi all&#39;esercitazione successiva per [elencare la cronologia cluster di un&#39;identità](./list-cluster-history.md)
