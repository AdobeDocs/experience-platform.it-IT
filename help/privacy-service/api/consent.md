---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Consenso
topic: developer guide
translation-type: tm+mt
source-git-commit: a3178ab54a7ab5eacd6c5f605b8bd894779f9e85
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 1%

---


# Consenso

Alcune normative richiedevano il consenso esplicito dei clienti prima di poter raccogliere i loro dati personali. L&#39; `/consent` endpoint nell&#39;API del servizio Privacy consente di elaborare le richieste di consenso dei clienti e integrarle nel flusso di lavoro per la privacy.

Prima di utilizzare questa guida, fate riferimento alla sezione [introduttiva](./getting-started.md) per informazioni sulle intestazioni di autenticazione richieste, presentate nella chiamata API di esempio di seguito.

## Elaborazione di una richiesta di consenso del cliente

Le richieste di consenso vengono elaborate effettuando una richiesta POST all&#39; `/consent` endpoint.

**Formato API**

```http
POST /consent
```

**Richiesta**

La richiesta seguente crea un nuovo processo di consenso per gli ID utente forniti nell’ `entities` array.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/consent \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `optOutOfSale` | Se impostato su true, indica che gli utenti forniti `entities` desiderano rinunciare alla vendita o alla condivisione dei loro dati personali. |
| `entities` | Un array di oggetti che indica gli utenti a cui si applica la richiesta di consenso. Ciascun oggetto contiene un `namespace` e un array di oggetti `values` che corrispondono ai singoli utenti con tale spazio dei nomi. |
| `nameSpace` | Ogni oggetto dell&#39; `entities` array deve contenere uno degli spazi dei nomi [standard riconosciuti dall&#39;API del servizio Privacy](./appendix.md#standard-namespaces) . |
| `values` | Un array di valori per ciascun utente, corrispondente al valore fornito `nameSpace`. |

>[!NOTE] Per ulteriori informazioni su come determinare quali valori di identità del cliente inviare al Servizio per la privacy, consulta la guida sulla [fornitura dei dati](../identity-data.md)di identità.

**Risposta**

Una risposta di successo restituisce lo stato HTTP 202 (Accettato) senza payload, a indicare che la richiesta è stata accettata dal servizio Privacy ed è in corso di elaborazione.