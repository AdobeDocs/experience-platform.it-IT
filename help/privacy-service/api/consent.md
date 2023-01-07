---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Endpoint API per il consenso
description: Scopri come gestire le richieste di consenso dei clienti per applicazioni di Experience Cloud utilizzando l’API di Privacy Service.
exl-id: ec505749-c0a9-4050-be56-4c0657807ec7
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 3%

---

# Endpoint di consenso

Alcune normative richiedono un consenso esplicito dei clienti prima che i loro dati personali possano essere raccolti. La `/consent` punto finale [!DNL Privacy Service] L’API ti consente di elaborare le richieste di consenso dei clienti e di integrarle nel flusso di lavoro per la privacy.

Prima di utilizzare questa guida, fai riferimento alla [guida introduttiva](./getting-started.md) per informazioni sulle intestazioni di autenticazione richieste presentate nella chiamata API di esempio di seguito.

## Elabora una richiesta di consenso del cliente

Le richieste di consenso vengono elaborate effettuando una richiesta di POST al `/consent` punto finale.

**Formato API**

```http
POST /consent
```

**Richiesta**

La seguente richiesta crea un nuovo processo di consenso per gli ID utente forniti nella `entities` array.

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
| `optOutOfSale` | Quando è impostato su true, indica che gli utenti forniti in `entities` desidera rinunciare alla vendita o alla condivisione dei propri dati personali. |
| `entities` | Matrice di oggetti che indica gli utenti a cui si applica la richiesta di consenso. Ogni oggetto contiene un `namespace` e una matrice di `values` per far corrispondere i singoli utenti a tale namespace. |
| `nameSpace` | Ogni oggetto nel `entities` l&#39;array deve contenere una delle [spazi dei nomi delle identità standard](./appendix.md#standard-namespaces) riconosciuto dall’API di Privacy Service. |
| `values` | Matrice di valori per ogni utente, corrispondente al `nameSpace`. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Per ulteriori informazioni su come determinare i valori di identità del cliente a cui inviare [!DNL Privacy Service], consulta la guida su [fornitura di dati di identità](../identity-data.md).

**Risposta**

Una risposta corretta restituisce lo stato HTTP 202 (Accettato) senza payload, a indicare che la richiesta è stata accettata da [!DNL Privacy Service] ed è in fase di elaborazione.
