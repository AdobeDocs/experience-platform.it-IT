---
title: Recupero  ID Experience Cloud
seo-title: Adobe Experience Platform Web SDK Recupero  ID Experience Cloud
description: Scoprite come ottenere l'ID Adobe Experience Cloud.
seo-description: Scoprite come ottenere l'ID Adobe Experience Cloud.
translation-type: tm+mt
source-git-commit: d2870df230811486c09ae29bf9f600beb24fe4f8
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 3%

---


# Identità - Recupero dell&#39;ID Experience Cloud 

L&#39;Adobe Experience Platform [!DNL Web SDK] sfrutta il [Servizio](../../identity-service/ecid.md)identità Adobe. In questo modo, ogni dispositivo ha un identificatore univoco persistente sul dispositivo, in modo che l&#39;attività tra le pagine possa essere legata insieme.

## Identità della prima parte

L&#39; [!DNL Identity Service] identità viene memorizzata in un cookie in un dominio di prime parti. Il cookie [!DNL Identity Service] tenta di impostarlo utilizzando un&#39;intestazione HTTP sul dominio. In caso contrario, [!DNL Identity Service] torneranno a impostare i cookie tramite Javascript.  Adobe consiglia di impostare un CNAME in modo che i cookie non siano limitati dalle restrizioni ITP lato client.

## Identità di terze parti

L&#39; [!DNL Identity Service] utente può sincronizzare un ID con un dominio di terze parti (demdex.net) per abilitare il tracciamento tra siti. Quando questa opzione è attivata, la prima richiesta per un visitatore (ad esempio, un utente senza un ECID) verrà effettuata su demdex.net. Questo verrà fatto solo sui browser che lo consentono (ad es. Chrome) ed è controllato dal `thirdPartyCookiesEnabled` parametro nella configurazione. Se desiderate disattivare questa funzione tutte insieme, impostate `thirdPartyCookiesEnabled` su false.

## Migrazione ID

Durante la migrazione dall’utilizzo dell’API Visitor, puoi anche migrare i cookie AMCV esistenti. Per abilitare la migrazione ECID, imposta il `idMigrationEnabled` parametro nella configurazione. La migrazione degli ID è configurata per attivare alcuni casi di utilizzo:

* Quando alcune pagine di un dominio utilizzano l’API del visitatore e altre pagine utilizzano questo SDK. Per supportare questo caso, l’SDK legge i cookie AMCV esistenti e scrive un nuovo cookie con l’ECID esistente. Inoltre, l’SDK scrive i cookie AMCV in modo che, se l’ECID viene ottenuto per primo su una pagina dotata di strumenti AEP Web SDK, le pagine successive strumentalizzate con l’API del visitatore abbiano lo stesso ECID.
* Quando l’SDK Web AEP è impostato su una pagina che include anche l’API Visitor. Per supportare questo caso, se il cookie AMCV non è impostato, l’SDK cerca l’API del visitatore sulla pagina e la chiama per ottenere l’ECID.
* Quando l’intero sito utilizza l’SDK Web AEP e non dispone dell’API Visitor, è utile migrare gli ECID in modo da mantenere le informazioni sul visitatore di ritorno. Dopo che l’SDK è stato distribuito con `idMigrationEnabled` per un periodo di tempo tale da consentire la migrazione della maggior parte dei cookie del visitatore, l’impostazione può essere disattivata.

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

>[!NOTE]
>
>Il `syncIdentity` metodo è stato rimosso nella versione 2.1.0, oltre alla funzione di hashing. Se si utilizza la versione 2.1.0+ e si desidera sincronizzare le identità, è possibile inviarle direttamente nell&#39; `xdm` opzione del `sendEvent` comando, sotto il `identityMap` campo.

Inoltre, [!DNL Identity Service] consente di sincronizzare i propri identificatori con l&#39;ECID utilizzando il `syncIdentity` comando.

>[!NOTE]
>
>Si consiglia vivamente di trasmettere tutte le identità disponibili su ogni `sendEvent` comando. Questo consente di aprire una serie di casi di utilizzo, inclusa la personalizzazione. Ora che puoi trasmettere queste identità nel `sendEvent` comando, puoi posizionarle direttamente nel tuo DataLayer.

La sincronizzazione delle identità consente di identificare un dispositivo/utente utilizzando più identità, impostarne lo stato di autenticazione e decidere quale identificatore è considerato principale. Se non è stato impostato alcun identificatore, `primary`il valore predefinito principale sarà il `ECID`.

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Notice how each namespace can contain multiple identifiers.
        {
          "id": "1234",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    }
  }
})
```


### Opzioni Identità sincronizzazione

#### Simbolo di identità

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Stringa | Sì | none |

La chiave dell&#39;oggetto è il simbolo [Identity Namespace](../../identity-service/namespaces.md) . Potete trovare questo elemento nell’interfaccia utente di Adobe Experience Platform in [!UICONTROL Identities].

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
