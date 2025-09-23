---
title: Panoramica degli eventi di streaming capillare
description: Scopri come inviare dati da Capillary ad Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: 7b733831932c48240340b0a2136e15f5d2144635
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 4%

---

# [!DNL Capillary Streaming Events]

[!DNL Capillary Technologies] è una piattaforma di fidelizzazione e coinvolgimento leader, affidabile da oltre 300 marchi in tutto il mondo. Utilizza l&#39;origine [!DNL Capillary Streaming Events] per consentire alla tua azienda di trasferire in streaming i profili dei clienti, i dati sulla fedeltà e gli eventi transazionali da [!DNL Capillary] a Adobe Experience Platform. Connetti l&#39;origine [!DNL Capillary] per abilitare la personalizzazione in tempo reale, la segmentazione avanzata del pubblico e l&#39;orchestrazione omnicanale delle campagne.

Integrando [!DNL Capillary] con Experience Platform, è possibile:

* Sincronizza **punti fedeltà, livelli e premi** in tempo reale.
* Invia **dati transazionali** ad Experience Platform per l&#39;analisi e l&#39;attivazione.
* Sfrutta Real-Time CDP, Experience Platform e Adobe Journey Optimizer per la segmentazione, l’orchestrazione del percorso e la personalizzazione.

## Prerequisiti

Prima di connettere [!DNL Capillary] a Adobe Experience Platform, assicurati di disporre di:

* Un **ID organizzazione Adobe** valido e l&#39;accesso a una sandbox Experience Platform abilitata.
* **[!DNL Capillary]credenziali di origine** (ID client e segreto client).
* Le autorizzazioni necessarie in Adobe Admin Console per creare origini e flussi di dati.

### Raccogli le credenziali richieste

Per connettere l&#39;account [!DNL Capillary] ad Experience Platform è necessario fornire i valori per le credenziali seguenti:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| ID client | Identificatore client per l&#39;origine [!DNL Capillary]. | `321c8a8fee0d4a06838d46f9d3109e8a` |
| Segreto client | Segreto client rilasciato con l’ID client | `xxxxxxxxxxxxxxxxxx` |
| ID organizzazione | Il tuo Adobe Organization ID | `0A7D42FC5DB9D3360A495FD3@AdobeOrg` |

Per ulteriori informazioni sulla generazione dei token di accesso, leggere la [guida all&#39;autenticazione di Adobe](https://developer.adobe.com/developer-console/docs/guides/authentication/).

### Generare un token di accesso

Quindi, utilizza l’ID client e il segreto client per generare un token di accesso da Adobe.

**Richiesta**

```shell
curl -X POST 'https://ims-na1.adobelogin.com/ims/token' \
  -d 'client_id={CLIENT_ID}' \
  -d 'client_secret={CLIENT_SECRET}' \
  -d 'grant_type=client_credentials' \
  -d 'scope=openid AdobeID read_organizations additional_info.projectedProductContext session'
```

**Risposta**

```json
{
  "access_token": "eyJhbGciOi...",
  "token_type": "bearer",
  "expires_in": 86399994
}
```

## Passaggi successivi

Dopo aver completato la configurazione dei prerequisiti per [!DNL Capillary], leggi la seguente documentazione per scoprire come collegare il tuo account e avviare lo streaming dei dati da [!DNL Capillary] ad Experience Platform.

* [Connetti [!DNL Capillary Streaming Events] ad Experience Platform utilizzando l&#39;API](../../tutorials/api/create/loyalty/capillary.md)
* [Connetti [!DNL Capillary Streaming Events] ad Experience Platform tramite l&#39;interfaccia utente](../../tutorials/ui/create/loyalty/capillary.md)