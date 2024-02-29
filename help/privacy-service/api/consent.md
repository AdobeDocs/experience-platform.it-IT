---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Endpoint API di consenso
description: Scopri come gestire le richieste di consenso dei clienti per le applicazioni Experience Cloud utilizzando l’API Privacy Service.
role: Developer
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 2%

---

# Endpoint di consenso

Alcune normative richiedono il consenso esplicito del cliente prima che i suoi dati personali possano essere raccolti. Il `/consent` endpoint nella [!DNL Privacy Service] API ti consente di elaborare le richieste di consenso dei clienti e di integrarle nel flusso di lavoro sulla privacy.

Prima di utilizzare questa guida, consultare [introduzione](./getting-started.md) guida per informazioni sulle intestazioni di autenticazione richieste presentate nella chiamata API di esempio di seguito.

## Elaborare una richiesta di consenso del cliente

Le richieste di consenso vengono elaborate effettuando una richiesta POST al `/consent` endpoint.

**Formato API**

```http
POST /consent
```

**Richiesta**

La seguente richiesta crea un nuovo processo di consenso per gli ID utente forniti in `entities` array.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/consent \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
        "optOutOfSale": true,
        "entities": [
          {
            "nameSpace": "email",
            "values": [
              "dsmith@acme.com",
              "ajones@acme.com"
            ]
          },
          {
            "nameSpace": "ECID",
            "values": [
              "443636576799758681021090721276"
            ]
          }
        ]
      }'
```

| Proprietà | Descrizione |
| --- | --- |
| `optOutOfSale` | Se impostato su true, indica che gli utenti forniti in `entities` desiderano rinunciare alla vendita o alla condivisione dei loro dati personali. |
| `entities` | Array di oggetti che indica gli utenti a cui si applica la richiesta di consenso. Ogni oggetto contiene un `namespace` e un array di `values` affinché i singoli utenti corrispondano a quello spazio dei nomi. |
| `nameSpace` | Ogni oggetto in `entities` l&#39;array deve contenere uno dei [spazi dei nomi di identità standard](./appendix.md#standard-namespaces) riconosciuto dall’API Privacy Service. |
| `values` | Un array di valori per ogni utente, corrispondente al fornito `nameSpace`. |

{style="table-layout:auto"}

>[!NOTE]
>
>Per ulteriori informazioni su come determinare quali valori di identità cliente inviare a [!DNL Privacy Service], consulta la guida [fornitura di dati di identità](../identity-data.md).

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 202 (Accepted) senza payload, indicando che la richiesta è stata accettata da [!DNL Privacy Service] e sono in fase di elaborazione.
