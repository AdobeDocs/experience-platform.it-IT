---
title: Endpoint certificato pubblico
description: Scopri come recuperare i certificati pubblici utilizzando l’endpoint /public-certificate dell’API del servizio MTLS.
role: Developer
source-git-commit: ce02c1a15d4e87c130de5e6133edda6b66cc2196
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 3%

---

# Endpoint di certificato pubblico

Questa guida spiega come utilizzare l’endpoint del certificato pubblico per recuperare in modo sicuro i certificati pubblici per le applicazioni di Adobe della tua organizzazione. Include una chiamata API di esempio e istruzioni dettagliate per aiutare gli sviluppatori ad autenticare e verificare gli scambi di dati.

## Introduzione

Prima di continuare, consulta la [guida introduttiva](./getting-started.md) per informazioni importanti che devi conoscere per effettuare correttamente chiamate all&#39;API, incluse le intestazioni richieste e la lettura delle chiamate API di esempio.

## Percorsi API {#paths}

Le seguenti informazioni sono i percorsi API essenziali necessari per utilizzare l’API del servizio mTLS. Questi includono l’URL del gateway della piattaforma, il percorso di base per l’API e un esempio di percorso completo per il recupero di un certificato pubblico.

- URL del gateway della piattaforma: `https://platform.adobe.io/`
- Percorso base per questa API: `/data/core/mtls`
- Esempio di percorso completo: `https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate`

## Recuperare i certificati pubblici {#list}

È possibile recuperare i certificati pubblici per qualsiasi applicazione di Adobe dell&#39;organizzazione effettuando una richiesta di GET all&#39;endpoint `/v1/certificate/public-certificate`.

**Formato API**

```http
GET /v1/certificate/public-certificate
```

Per recuperare i certificati pubblici è possibile utilizzare i seguenti parametri di query facoltativi.

| Parametro query | Descrizione | Esempio |
| --------------- | ----------- | ------- |
| `page` | Specifica da quale pagina inizieranno i risultati della richiesta. | `page=5` |
| `limit` | Il numero massimo di certificati pubblici che si desidera recuperare per pagina. | `limit=20` |

{style="table-layout:auto"}

**Richiesta**

Un esempio di richiesta per restituire i certificati pubblici associati alla tua organizzazione è riportato nella sezione comprimibile seguente.

+++Richiesta di esempio

```shell
curl -X GET https://experience.adobe.io/data/core/mtls/v1/certificate/public-certificate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' 
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 ed elenca i certificati pubblici per la tua organizzazione.

+++Un esempio di risposta corretta

```json
{
   "results":[
      {
         "certCommonName":"Adobe Experience Platform",
         "publicCertificate":"-----BEGIN CERTIFICATE-----\nMIIDQTCCAimgAwIBAgITBmyfACAfma......KJY5u89CjAwj\n-----END CERTIFICATE-----",
         "expiryDate":"2024-07-17T21:27:57.434Z"
      }
   ],
   "total":0,
   "count":0,
   "_links":{
      "next":{
         "href":"string",
         "templated":true
      },
      "prev":{
         "href":"string",
         "templated":true
      },
      "page":{
         "href":"string",
         "templated":true
      }
   }
}
```

| Proprietà | Descrizione |
| --- | --- |
| `certCommonName` | Il nome comune (CN) del certificato, che in genere rappresenta il nome o l’identità del server o dell’entità a cui viene rilasciato il certificato. |
| `publicCertificate` | Il certificato pubblico effettivo in formato stringa, utilizzato per l&#39;autenticazione e la crittografia delle comunicazioni. |
| `expiryDate` | La data e l’ora di scadenza del certificato pubblico, formattato in ISO 8601 (UTC). |

{style="table-layout:auto"}

+++

## Passaggi successivi

Dopo aver letto questa guida, saprai come recuperare i certificati pubblici utilizzando l’API di Adobe Experience Platform. Per ulteriori informazioni sulla gestione dei dati dei clienti per garantire la conformità alle normative e ai criteri organizzativi, consulta la [Panoramica sulla governance dei dati](../home.md).

<!-- To test this API call, navigate to the [MTLS API reference page]() to interact with the Experience Platform API endpoints. -->

<!-- Add link after developer page is live -->

