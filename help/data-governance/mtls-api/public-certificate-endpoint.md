---
title: Endpoint certificato pubblico
description: Scopri come recuperare i certificati pubblici utilizzando l’endpoint /public-certificate dell’API del servizio MTLS.
role: Developer
exl-id: 8369c783-e595-476f-9546-801cf4f10f71
source-git-commit: d74353e70e992150c031397009d0c8add3df5e7b
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 2%

---

# Endpoint di certificato pubblico

>[!NOTE]
>
>Adobe non supporta più il download statico dei certificati mTLS pubblici. Utilizza questa API per recuperare certificati validi per le integrazioni. Il recupero automatico è ora necessario per evitare interruzioni del servizio.

Questa guida spiega come utilizzare l’endpoint del certificato pubblico per recuperare in modo sicuro i certificati pubblici per le applicazioni Adobe della tua organizzazione. Include una chiamata API di esempio e istruzioni dettagliate per aiutare gli sviluppatori ad autenticare e verificare gli scambi di dati.

## Introduzione

Prima di continuare, consulta la [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste e su come interpretare le chiamate API di esempio.

## Percorsi API {#paths}

Le seguenti informazioni sono i percorsi API essenziali necessari per utilizzare l’API del servizio mTLS. Questi includono l’URL del gateway della piattaforma, il percorso di base per l’API e un esempio di percorso completo per il recupero di un certificato pubblico.

- URL del gateway della piattaforma: `https://platform.adobe.io/`
- Percorso base per questa API: `/data/core/mtls`
- Esempio di percorso completo: `https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate`

## Recuperare i certificati pubblici {#list}

Effettua una richiesta GET all&#39;endpoint `/v1/certificate/public-certificate` per recuperare i certificati pubblici per le applicazioni Adobe della tua organizzazione.

**Formato API**

```http
GET /v1/certificate/public-certificate
```

Per recuperare i certificati pubblici è possibile utilizzare i seguenti parametri di query facoltativi.

| Parametri query | Descrizione | Esempio |
| --------------- | ----------- | ------- |
| `page` | Specifica da quale pagina inizieranno i risultati della richiesta. | `page=5` |
| `limit` | Il numero massimo di certificati pubblici che si desidera recuperare per pagina. | `limit=20` |

{style="table-layout:auto"}

**Richiesta**

Un esempio di richiesta per restituire i certificati pubblici associati alla tua organizzazione è riportato nella sezione comprimibile seguente.

+++Richiesta di esempio

```shell
curl -X GET https://platform.adobe.io/data/core/mtls/v1/certificate/public-certificate
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

## Automazione del ciclo di vita dei certificati {#certificate-lifecycle-automation}

Adobe automatizza il ciclo di vita dei certificati mTLS pubblici per garantire la continuità e ridurre le interruzioni del servizio.

- I certificati vengono rilasciati nuovamente 60 giorni prima della scadenza.
- I certificati vengono revocati 30 giorni prima della scadenza.

>[!NOTE]
>
>Queste tempistiche si accorceranno nel tempo in linea con le [linee guida per forum CA/B](https://www.digicert.com/blog/tls-certificate-lifetimes-will-officially-reduce-to-47-days), che mirano a ridurre la durata dei certificati a un massimo di 47 giorni.

È necessario aggiornare le integrazioni per supportare il recupero automatico tramite l’API. Non fare affidamento su download manuali di certificati o copie statiche, in quanto potrebbero causare certificati scaduti o revocati.

## Passaggi successivi

Dopo aver recuperato i certificati pubblici utilizzando l’API, aggiorna le integrazioni per chiamare regolarmente questo endpoint prima della scadenza dei certificati. Per verificare questa chiamata in modo interattivo, visita la [pagina di riferimento API MTLS](https://developer.adobe.com/experience-platform-apis/references/mtls-service/). Per maggiori informazioni sulle integrazioni basate su certificati, consulta [Data encryption in Adobe Experience Platform overview](../../landing/governance-privacy-security/encryption.md) o [Data Governance overview](../home.md).
