---
keywords: Experience Platform; sicurezza; accesso ip; QS-Auth; guida API; servizio query; intervalli IP
title: Endpoint di accesso IP
description: Scopri come gestire gli intervalli IP per l’accesso sandbox in Query Service utilizzando l’endpoint API per l’accesso IP.
role: Developer
exl-id: fc15ab50-c125-4f00-a311-81fd41697c7d
source-git-commit: bf696c8836407a2fea82e9078201cb1f5004bcf8
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 5%

---

# Endpoint di accesso IP

>[!AVAILABILITY]
>
>Questa funzionalità è disponibile per i clienti che hanno acquistato il componente aggiuntivo Data Distiller. Per ulteriori informazioni, contatta il tuo rappresentante Adobe.

Per proteggere l’accesso ai dati all’interno di una sandbox di Query Service specificata, utilizza l’endpoint di accesso IP per gestire gli intervalli IP consentiti. Puoi utilizzare questa API per recuperare, configurare o eliminare gli intervalli IP associati all’ID della tua organizzazione.

Con l’API di accesso IP puoi eseguire le seguenti azioni:

- **Recupera tutti gli intervalli IP**
- **Imposta nuovi intervalli IP**
- **Elimina intervalli IP esistenti**

Questo documento descrive le richieste e le risposte che è possibile effettuare e ricevere dall&#39;endpoint `/security/ip-access`.

>[!NOTE]
>
>Per chiamare questa API è necessario disporre di un token utente. Consulta la [guida introduttiva](./getting-started.md) per informazioni sull&#39;acquisizione dei valori richiesti per ciascuna intestazione.

## Recupera tutti gli intervalli IP {#fetch-all-ip-ranges}

Recupera un elenco di tutti gli intervalli IP configurati per la sandbox. Se non è impostato alcun intervallo IP, per impostazione predefinita sono consentiti tutti gli IP e la risposta restituisce un elenco vuoto in `allowedIpRanges`.

**Formato API**

```http
GET /security/ip-access
```

**Richiesta**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un elenco degli intervalli IP consentiti della sandbox.

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "allowedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "101.10.1.1"}
  ]
}
```

La tabella seguente fornisce una descrizione ed un esempio delle proprietà dello schema di risposta:

| Proprietà | Descrizione | Esempio |
|------------------|---------------------------------------------|-----------------------------------------------------------------------------------------------|
| `imsOrg` | ID organizzazione per la sandbox. | `{ORG_ID}` |
| `sandboxName` | Nome della sandbox a cui si applicano le restrizioni IP. | `prod` |
| `channel` | Modalità di accesso per le restrizioni IP. Attualmente l&#39;unico valore accettato è `data_distiller`. Questo valore indica che le restrizioni IP vengono applicate alle connessioni PSQL o JDBC. | `data_distiller` |
| `allowedIpRanges` | Elenco degli IP consentiti in formato CIDR o IP fisso. Ciascuna voce può includere una descrizione facoltativa. | `[{"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"}]` |

>[!NOTE]
>
>Il campo `allowedIpRanges` può includere due tipi di specifiche IP:<br><ul><li>**CIDR**: notazione CIDR standard (ad esempio, `"136.23.110.0/23"`) per definire gli intervalli IP.</li><li>**IP fisso**: IP singoli per singole autorizzazioni di accesso (ad esempio, `"101.10.1.1"`).</li></ul>

## Imposta nuovi intervalli IP

Sovrascrivi gli intervalli IP esistenti impostando un nuovo elenco per la sandbox. Questa operazione richiede un elenco completo di intervalli IP, compresi quelli che rimangono invariati.

**Formato API**

```http
PUT /security/ip-access
```

**Richiesta**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "ipRanges": [
       {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
       {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
       {"ipRange": "101.10.1.1"},
       {"ipRange": "163.77.30.9", "description": "Test server IP"}
     ]
   }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli degli intervalli IP appena configurati.

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "allowedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
    {"ipRange": "101.10.1.1"},
    {"ipRange": "163.77.30.9", "description": "Test server IP"}
  ]
}
```

## Elimina intervalli IP {#delete-ip-ranges}

Rimuovi tutti gli intervalli IP configurati per la sandbox. Questa azione elimina gli intervalli IP e restituisce l’elenco IP eliminato.

>[!NOTE]
>
>L&#39;operazione di eliminazione si applica all&#39;ID organizzazione (`imsOrg`) e interessa tutti gli intervalli IP configurati per la sandbox.

**Formato API**

```http
DELETE /security/ip-access
```

**Richiesta**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli degli intervalli IP eliminati.

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "deletedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
    {"ipRange": "101.10.1.1"},
    {"ipRange": "163.77.30.9", "description": "Test server IP"}
  ]
}
```
