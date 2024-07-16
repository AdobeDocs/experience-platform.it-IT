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

Alcune normative richiedono il consenso esplicito del cliente prima che i suoi dati personali possano essere raccolti. L&#39;endpoint `/consent` nell&#39;API [!DNL Privacy Service] consente di elaborare le richieste di consenso dei clienti e di integrarle nel flusso di lavoro per la privacy.

Prima di utilizzare questa guida, consulta la [guida introduttiva](./getting-started.md) per informazioni sulle intestazioni di autenticazione richieste presentate nella chiamata API di esempio seguente.

## Elaborare una richiesta di consenso del cliente

Le richieste di consenso vengono elaborate effettuando una richiesta POST all&#39;endpoint `/consent`.

**Formato API**

```http
POST /consent
```

**Richiesta**

La richiesta seguente crea un nuovo processo di consenso per gli ID utente forniti nell&#39;array `entities`.

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
| `optOutOfSale` | Se impostato su true, indica che gli utenti forniti in `entities` desiderano rinunciare alla vendita o alla condivisione dei propri dati personali. |
| `entities` | Array di oggetti che indica gli utenti a cui si applica la richiesta di consenso. Ogni oggetto contiene un `namespace` e un array di `values` che corrispondono ai singoli utenti con tale spazio dei nomi. |
| `nameSpace` | Ogni oggetto nell&#39;array `entities` deve contenere uno dei [spazi dei nomi di identità standard](./appendix.md#standard-namespaces) riconosciuti dall&#39;API Privacy Service. |
| `values` | Matrice di valori per ogni utente, corrispondente al valore `nameSpace` specificato. |

{style="table-layout:auto"}

>[!NOTE]
>
>Per ulteriori informazioni su come determinare quali valori di identità cliente inviare a [!DNL Privacy Service], vedere la guida relativa a [fornitura dei dati di identità](../identity-data.md).

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 202 (Accepted) senza payload, a indicare che la richiesta è stata accettata da [!DNL Privacy Service] ed è in fase di elaborazione.
