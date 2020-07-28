---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Consenso
topic: developer guide
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 1%

---


# Consenso

Alcune normative richiedevano il consenso esplicito dei clienti prima di poter raccogliere i loro dati personali. L&#39; `/consent` endpoint nell&#39; [!DNL Privacy Service] API consente di elaborare le richieste di consenso dei clienti e integrarle nel flusso di lavoro per la privacy.

Prima di utilizzare questa guida, fate riferimento alla sezione [introduttiva](./getting-started.md) per informazioni sulle intestazioni di autenticazione richieste, presentate nella chiamata API di esempio di seguito.

## Elaborazione di una richiesta di consenso del cliente

Le richieste di consenso vengono elaborate effettuando una richiesta di POST all&#39; `/consent` endpoint.

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
| `nameSpace` | Ogni oggetto nell&#39; `entities` array deve contenere uno degli spazi dei nomi [](./appendix.md#standard-namespaces) standard riconosciuti dall&#39;API Privacy Service. |
| `values` | Un array di valori per ciascun utente, corrispondente al valore fornito `nameSpace`. |

>[!NOTE]
>
>Per ulteriori informazioni su come determinare a quali valori di identità cliente inviare [!DNL Privacy Service], consultare la guida sulla [fornitura dei dati](../identity-data.md)di identità.

**Risposta**

Una risposta corretta restituisce lo stato HTTP 202 (Accettato) senza payload, a indicare che la richiesta è stata accettata da [!DNL Privacy Service] e sta attraversando un processo di elaborazione.