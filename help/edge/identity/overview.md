---
title: Recupero  ID Experience Cloud
seo-title: Adobe Experience Platform Web SDK Recupero  ID Experience Cloud
description: Scoprite come ottenere l'ID Adobe Experience Cloud.
seo-description: Scoprite come ottenere l'ID Adobe Experience Cloud.
keywords: Identità;Identità di prima parte;Identità di terza parte;Migrazione ID;ID visitatore;identità di terza parte;identità di terza parte;terze partiCookiesEnabled;idMigrationEnabled;getIdentity;Syncing Identities;sendEvent;identityMap;primario;ecid;Identity Namespace;namespace id;authenticationState;hashEnabled;
translation-type: tm+mt
source-git-commit: 60945f7f3a87568b82d968692cc7a6e07593fa01
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 2%

---


# Identità - Recupero dell&#39;ID Experience Cloud 

Adobe Experience Platform Web SDK utilizza [ Adobe Identity Service](../../identity-service/ecid.md). In questo modo, ogni dispositivo ha un identificatore univoco persistente sul dispositivo, in modo che l&#39;attività tra le pagine possa essere legata insieme.

## Identità di prima parte

L&#39; [!DNL Identity Service] memorizza l&#39;identità in un cookie in un dominio di prime parti. Il [!DNL Identity Service] tenta di impostare il cookie utilizzando un&#39;intestazione HTTP sul dominio. In caso contrario, la [!DNL Identity Service] tornerà a impostare i cookie tramite Javascript.  Adobe consiglia di impostare un CNAME in modo che i cookie non siano limitati dalle restrizioni ITP lato client.

## identità di terze parti

[!DNL Identity Service] è in grado di sincronizzare un ID con un dominio di terze parti (demdex.net) per abilitare il tracciamento tra i siti. Quando questa opzione è attivata, la prima richiesta per un visitatore (ad esempio, un utente senza un ECID) verrà effettuata su demdex.net. Questo verrà fatto solo sui browser che lo consentono (ad es. Chrome) ed è controllato dal parametro `thirdPartyCookiesEnabled` nella configurazione. Se desiderate disattivare questa funzione tutte insieme, impostate `thirdPartyCookiesEnabled` su false.

## Migrazione ID

Durante la migrazione dall’utilizzo dell’API Visitor, puoi anche migrare i cookie AMCV esistenti. Per abilitare la migrazione ECID, imposta il parametro `idMigrationEnabled` nella configurazione. La migrazione degli ID abilita i seguenti casi di utilizzo:

* Quando alcune pagine di un dominio utilizzano l’API del visitatore e altre pagine utilizzano questo SDK. Per supportare questo caso, l’SDK legge i cookie AMCV esistenti e scrive un nuovo cookie con l’ECID esistente. Inoltre, l’SDK scrive i cookie AMCV in modo che, se l’ECID viene ottenuto per primo su una pagina dotata di strumenti SDK, le pagine successive strumentalizzate con l’API del visitatore abbiano lo stesso ECID.
* Quando Adobe Experience Platform Web SDK è impostato su una pagina che dispone anche di Visitor API. Per supportare questo caso, se il cookie AMCV non è impostato, l’SDK cerca l’API del visitatore sulla pagina e la chiama per ottenere l’ECID.
* Se l’intero sito utilizza Adobe Experience Platform Web SDK e non dispone di API visitatore, è utile migrare gli ECID in modo da mantenere le informazioni sul visitatore di ritorno. Dopo che l&#39;SDK è stato distribuito con `idMigrationEnabled` per un periodo di tempo che consente di migrare la maggior parte dei cookie del visitatore, l&#39;impostazione può essere disattivata.

## Aggiornamento delle caratteristiche per la migrazione

Quando i dati in formato XDM vengono inviati  Audience Manager, questi dati dovranno essere convertiti in segnali durante la migrazione. Le caratteristiche dovranno essere aggiornate in modo da riflettere le nuove chiavi fornite da XDM. Questo processo è reso più semplice utilizzando il [strumento BAAAM](https://docs.adobe.com/content/help/en/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) creato  Audience Manager.

## Inoltro lato server

Se al momento l&#39;inoltro lato server è abilitato e si utilizza `appmeasurement.js`. e `visitor.js` è possibile mantenere attivata la funzionalità di inoltro lato server, senza causare problemi. Nel backend,  Adobe recupera tutti i segmenti AAM e li aggiunge alla chiamata ad Analytics. Se la chiamata ad Analytics contiene tali segmenti, Analytics non chiamerà  Audience Manager per inoltrare i dati, pertanto non è disponibile alcuna raccolta dati doppia. Non è inoltre necessario Location Hint quando si utilizza l’SDK per Web, perché gli stessi endpoint di segmentazione sono richiamati nel backend.

## Recupero dell’ID visitatore

Se desiderate utilizzare questo ID univoco, utilizzate il comando `getIdentity`. `getIdentity` restituisce l’ECID esistente per il visitatore corrente. Per i nuovi visitatori che non dispongono ancora di un ECID, questo comando genera un nuovo ECID.

>[!NOTE]
>
>Questo metodo viene in genere utilizzato con soluzioni personalizzate che richiedono la lettura dell&#39;ID [!DNL Experience Cloud]. Non viene utilizzata da un’implementazione standard.

```javascript
alloy("getIdentity")
  .then(function(result) {
    // The command succeeded.
    console.log(result.identity.ECID);
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information.
  });
```

## Sincronizzazione delle identità

>[!NOTE]
>
>Il metodo `syncIdentity` è stato rimosso nella versione 2.1.0, oltre alla funzione di hashing. Se utilizzate la versione 2.1.0+ e desiderate sincronizzare le identità, potete inviarle direttamente nell&#39;opzione `xdm` del comando `sendEvent`, nel campo `identityMap`.

Inoltre, [!DNL Identity Service] consente di sincronizzare i propri identificatori con l&#39;ECID utilizzando il comando `syncIdentity`.

>[!NOTE]
>
>Si consiglia vivamente di trasmettere tutte le identità disponibili su ogni comando `sendEvent`. Questo consente di aprire una serie di casi di utilizzo, inclusa la personalizzazione. Ora che è possibile trasmettere tali identità nel comando `sendEvent`, è possibile inserirle direttamente in DataLayer.

La sincronizzazione delle identità consente di identificare un dispositivo/utente utilizzando più identità, impostarne lo stato di autenticazione e decidere quale identificatore è considerato principale. Se non è stato impostato alcun identificatore come `primary`, il valore predefinito principale sarà `ECID`.

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
});
```

Ogni proprietà all&#39;interno di `identityMap` rappresenta identità appartenenti a uno specifico [spazio dei nomi identità](../../identity-service/namespaces.md). Il nome della proprietà deve essere il simbolo dello spazio dei nomi dell&#39;identità, elencato nell&#39;interfaccia utente di Adobe Experience Platform in &quot;[!UICONTROL Identities]&quot;. Il valore della proprietà deve essere un array di identità appartenenti a tale namespace di identità.

Ciascun oggetto identity nell&#39;array identities è strutturato come segue:

### `id`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Stringa | Sì | Nessuno |

Questo è l&#39;ID che si desidera sincronizzare per lo spazio dei nomi specificato.

### `authenticationState`

| **Tipo** | **Obbligatorio** | **Valore predefinito** | **Valori possibili** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| Stringa | Sì | ambiguo | ambiguo, autenticato e logout |

Stato di autenticazione dell’ID.

### `primary`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | optional | false |

Determina se questa identità deve essere utilizzata come frammento principale nel profilo unificato. Per impostazione predefinita, l’ECID è impostato come identificatore principale per l’utente.
