---
keywords: ' Experience Platform;home;argomenti popolari'
solution: Experience Platform
title: Endpoint di consenso
topic: developer guide
description: Scoprite come gestire le richieste di consenso dei clienti per  applicazioni di Experience Cloud utilizzando l'API Privacy Service.
translation-type: tm+mt
source-git-commit: 238a9200e4b43d41335bed0efab079780b252717
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 1%

---


# Endpoint di consenso

Alcune normative richiedono un consenso esplicito da parte dei clienti prima che i loro dati personali possano essere raccolti. L&#39;endpoint `/consent` nell&#39;API [!DNL Privacy Service] consente di elaborare le richieste di consenso dei clienti e integrarle nel flusso di lavoro per la privacy.

Prima di utilizzare questa guida, fare riferimento alla sezione [guida introduttiva](./getting-started.md) per informazioni sulle intestazioni di autenticazione richieste presentate nella chiamata API di esempio di seguito.

## Elaborazione di una richiesta di consenso del cliente

Le richieste di consenso vengono elaborate effettuando una richiesta di POST all&#39;endpoint `/consent`.

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
| `entities` | Un array di oggetti che indica gli utenti a cui si applica la richiesta di consenso. Ogni oggetto contiene un `namespace` e un array di `values` per far corrispondere i singoli utenti a tale spazio nomi. |
| `nameSpace` | Ogni oggetto nell&#39;array `entities` deve contenere uno degli [spazi dei nomi di identità standard](./appendix.md#standard-namespaces) riconosciuti dall&#39;API Privacy Service. |
| `values` | Un array di valori per ciascun utente, corrispondente al valore `nameSpace` fornito. |

>[!NOTE]
>
>Per ulteriori informazioni su come determinare quali valori di identità del cliente inviare a [!DNL Privacy Service], consultare la guida in [provider di dati di identità](../identity-data.md).

**Risposta**

Una risposta corretta restituisce lo stato HTTP 202 (Accettato) senza payload, a indicare che la richiesta è stata accettata da [!DNL Privacy Service] ed è in corso di elaborazione.