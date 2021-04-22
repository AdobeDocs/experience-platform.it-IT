---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Endpoint API per il consenso
topic-legacy: developer guide
description: Scopri come gestire le richieste di consenso dei clienti per applicazioni di Experience Cloud utilizzando l’API di Privacy Service.
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
translation-type: tm+mt
source-git-commit: e226990fc84926587308077b32b128bfe334e812
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

---

# Endpoint di consenso

Alcune normative richiedono un consenso esplicito dei clienti prima che i loro dati personali possano essere raccolti. L’ endpoint `/consent` nell’ API [!DNL Privacy Service] consente di elaborare le richieste di consenso dei clienti e di integrarle nel flusso di lavoro per la privacy.

Prima di utilizzare questa guida, consulta la sezione [guida introduttiva](./getting-started.md) per informazioni sulle intestazioni di autenticazione richieste presentate nella chiamata API di esempio di seguito.

## Elabora una richiesta di consenso del cliente

Le richieste di consenso vengono elaborate effettuando una richiesta POST all’endpoint `/consent` .

**Formato API**

```http
POST /consent
```

**Richiesta**

La seguente richiesta crea un nuovo processo di consenso per gli ID utente forniti nell&#39;array `entities` .

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
| `optOutOfSale` | Se impostato su true, indica che gli utenti forniti in `entities` desiderano rinunciare alla vendita o alla condivisione dei propri dati personali. |
| `entities` | Matrice di oggetti che indica gli utenti a cui si applica la richiesta di consenso. Ogni oggetto contiene un `namespace` e una matrice di `values` per far corrispondere i singoli utenti a tale spazio dei nomi. |
| `nameSpace` | Ogni oggetto dell&#39;array `entities` deve contenere uno dei [namespace di identità standard](./appendix.md#standard-namespaces) riconosciuti dall&#39;API Privacy Service. |
| `values` | Matrice di valori per ogni utente, corrispondente al valore `nameSpace` fornito. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Per ulteriori informazioni su come determinare i valori di identità del cliente da inviare a [!DNL Privacy Service], consulta la guida [fornitura di dati di identità](../identity-data.md).

**Risposta**

Una risposta corretta restituisce lo stato HTTP 202 (Accettato) senza payload, a indicare che la richiesta è stata accettata da [!DNL Privacy Service] ed è in corso di elaborazione.
