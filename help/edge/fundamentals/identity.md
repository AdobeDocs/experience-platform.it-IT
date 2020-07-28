---
title: Recupero  ID Experience Cloud
seo-title: ' Adobe Experience Platform SDK Web Recupero  ID Experience Cloud'
description: Scoprite come ottenere l'ID Adobe Experience Cloud.
seo-description: Scoprite come ottenere l'ID Adobe Experience Cloud.
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 6%

---


# Identità - Recupero dell&#39;ID Experience Cloud 

Il Adobe Experience Platform  [!DNL Web SDK] sfrutta il [Servizio](../../identity-service/ecid.md)identità Adobe. In questo modo, ogni dispositivo ha un identificatore univoco persistente sul dispositivo, in modo che l&#39;attività tra le pagine possa essere legata insieme.

## Identità della prima parte

L&#39; [!DNL Identity Service] identità viene memorizzata in un cookie in un dominio di prime parti. Il cookie [!DNL Identity Service] tenta di impostarlo utilizzando un&#39;intestazione HTTP sul dominio. In caso contrario, [!DNL Identity Service] torneranno a impostare i cookie tramite Javascript.  Adobe consiglia di impostare un CNAME in modo che i cookie non siano limitati dalle restrizioni ITP lato client.

## Identità di terze parti

L&#39; [!DNL Identity Service] utente può sincronizzare un ID con un dominio di terze parti (demdex.net) per abilitare il tracciamento tra siti. Quando questa opzione è attivata, la prima richiesta per un visitatore (ad esempio, un utente senza un ECID) verrà effettuata su demdex.net. Questo verrà fatto solo sui browser che lo consentono (ad es. Chrome) ed è controllato dal `thirdPartyCookiesEnabled` parametro nella configurazione. Se desiderate disattivare questa funzione tutte insieme, impostate `thirdPartyCookiesEnabled` su false.

## Recupero dell’ID visitatore

Se desiderate utilizzare questo ID univoco, usate il `getIdentity` comando. `getIdentity` restituisce l’ECID esistente per il visitatore corrente. Per i nuovi visitatori che non dispongono ancora di un ECID, questo comando genera un nuovo ECID.

>[!NOTE]
>
>Questo metodo viene in genere utilizzato con soluzioni personalizzate che richiedono la lettura dell&#39; [!DNL Experience Cloud] ID. Non viene utilizzata da un’implementazione standard.

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

Inoltre, [!DNL Identity Service] consente di sincronizzare i propri identificatori con l&#39;ECID utilizzando il `syncIdentity` comando.

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

La chiave dell&#39;oggetto è il simbolo [Identity Namespace](../../identity-service/namespaces.md) . Potete trovarlo elencato nell&#39;interfaccia utente del Adobe Experience Platform  in [!UICONTROL Identities].

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

Determina se questa identità deve essere utilizzata come frammento principale nel profilo unificato. Per impostazione predefinita, l’ECID è impostato come identificatore principale per l’utente.

#### `hashEnabled`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | optional | false |

Se abilitata, l&#39;identità verrà hash utilizzando l&#39;hash SHA256.
