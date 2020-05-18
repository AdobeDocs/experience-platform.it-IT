---
title: Recupero dell’ID di Experience Cloud
seo-title: SDK Web per Adobe Experience Platform per il recupero dell'Experience Cloud ID
description: Scopri come ottenere Adobe Experience Cloud Id.
seo-description: Scopri come ottenere Adobe Experience Cloud Id.
translation-type: tm+mt
source-git-commit: a9dd5fd93397e57d0876bec334d54c517fa86939
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 4%

---


# Recupero dell’ID di Experience Cloud

L’SDK Web di Adobe Experience Platform sfrutta [Adobe Identity Service](../../identity-service/ecid.md). In questo modo, ogni dispositivo ha un identificatore univoco persistente sul dispositivo, in modo che l&#39;attività tra le pagine possa essere legata insieme.

## Identità della prima parte

Il servizio ID memorizza l’identità in un cookie in un dominio di prime parti. Il servizio ID tenta di impostare il cookie utilizzando un’intestazione HTTP sul dominio in caso di errore, il servizio ID tornerà a impostare i cookie tramite Javascript. Adobe consiglia di impostare un CNAME in modo che i cookie non vengano limitati dalle restrizioni ITP lato client.

## Identità di terze parti

I servizi ID possono sincronizzare un ID con un dominio di terze parti (demdex.net) per abilitare il tracciamento tra i siti. Quando questa opzione è attivata, la prima richiesta per un visitatore (ad esempio, un utente senza un ECID) verrà effettuata su demdex.net. Questo verrà fatto solo sui browser che lo consentono (ad es. Chrome) ed è controllato dal `thirdPartyCookiesEnabled` parametro nella configurazione. Se desiderate disattivare questa funzione, impostate tutti insieme `thirdPartyCookiesEnabled` su false.

## Recupero dell’ID visitatore

Se desiderate utilizzare questo ID univoco, usate il `getIdentity` comando. `getIdentity` restituisce l’ECID esistente per il visitatore corrente. Per i nuovi visitatori che non dispongono ancora di un ECID, questo comando genera un nuovo ECID.

>[!NOTE]
>
>Questo metodo viene in genere utilizzato con soluzioni personalizzate che richiedono la lettura del Experience Cloud ID. Non viene utilizzato da un&#39;implementazione standard.

```javascript
alloy("getIdentity")
  .then(function(result.identity.ECID) {
    // This function will get called with Adobe Experience Cloud Id when the command promise is resolved
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information
  })
```

## Identità di sincronizzazione

Inoltre, il servizio Identità consente di sincronizzare i propri identificatori con l&#39;ECID utilizzando il `syncIdentity` comando.

```javascript
alloy("syncIdentity",{
    identity:{
      "AppNexus":{
        "id":"123456,
        "authenticationState":"ambiguous",
        "primary":false,
        "hashEnabled": true,
      }
    }
})
```

### Opzioni Identità sincronizzazione

#### Simbolo di identità

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Stringa | Sì | none |

La chiave dell&#39;oggetto è il simbolo [Identity Namespace](../../identity-service/namespaces.md) . Puoi trovarlo nell’interfaccia utente di Adobe Experience Platform in Identità.

#### `id`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Stringa | Sì | none |

Questo è l&#39;ID che si desidera sincronizzare per lo spazio dei nomi specificato.

#### `authenticationState`

| **Tipo** | **Obbligatorio** | **Valore predefinito** | **Valori possibili** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| Stringa | Sì | ambiguo | ambiguo, autenticato e logout |

Stato di autenticazione dell’ID.

#### `primary`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | optional | false |

Se questa identità deve essere utilizzata come frammento principale nel profilo unificato. Per impostazione predefinita, l’ECID è impostato come identificatore principale per l’utente.

#### `hashEnabled`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | optional | false |

Se abilitata, l&#39;identità verrà hash utilizzando l&#39;hash SHA256.
