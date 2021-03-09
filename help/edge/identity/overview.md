---
title: Recuperare gli ID di Experience Cloud tramite l’SDK per web di Adobe Experience Platform
description: Scopri come recuperare gli ID Adobe Experience Cloud (ECID) utilizzando Adobe Experience Platform Web SDK.
seo-description: Scopri come ottenere l’ID Adobe Experience Cloud.
keywords: identità;identità di prima parte;servizio Identity;identità di terze parti;migrazione ID;ID visitatore;identità di terze parti;cookie di terze partiabilitati;idMigrationEnabled;getIdentity;identità di sincronizzazione;syncIdentity;sendEvent;identityMap;primario;ecid;spazio dei nomi;ID spazio dei nomi;authenticationState;hashEnabled;
translation-type: tm+mt
source-git-commit: 882bcd2f9aa7a104270865783eed82089862dea3
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 2%

---


# Recupera ID Adobe Experience Cloud

Adobe Experience Platform Web SDK sfrutta [Adobe Identity Service](../../identity-service/ecid.md). In questo modo, ogni dispositivo dispone di un identificatore univoco persistente sul dispositivo, in modo che l’attività tra le pagine possa essere legata tra loro.

## Identità di prima parte

L’ [!DNL Identity Service] memorizza l’identità in un cookie in un dominio di prime parti. Il [!DNL Identity Service] tenta di impostare il cookie utilizzando un&#39;intestazione HTTP sul dominio. Se questo non riesce, il [!DNL Identity Service] tornerà a impostare i cookie tramite Javascript. L’Adobe consiglia di impostare un CNAME per garantire che i cookie non siano limitati dalle restrizioni ITP lato client.

## identità di terze parti

Il [!DNL Identity Service] può sincronizzare un ID con un dominio di terze parti (demdex.net) per abilitare il tracciamento tra siti. Quando questa funzione è abilitata, la prima richiesta di un visitatore (ad esempio, un utente senza un ECID) verrà effettuata su demdex.net. Questo verrà fatto solo sui browser che lo consentono, come Chrome) ed è controllato dal parametro `thirdPartyCookiesEnabled` nella configurazione. Se desideri disattivare questa funzione tutti insieme, imposta `thirdPartyCookiesEnabled` su false.

## Migrazione degli ID

Durante la migrazione dall’utilizzo dell’API visitatore, puoi anche eseguire la migrazione dei cookie AMCV esistenti. Per abilitare la migrazione ECID, imposta il parametro `idMigrationEnabled` nella configurazione. La migrazione degli ID abilita i seguenti casi d’uso:

* Quando alcune pagine di un dominio utilizzano l’API Visitor e altre pagine utilizzano questo SDK. Per supportare questo caso, l&#39;SDK legge i cookie AMCV esistenti e scrive un nuovo cookie con l&#39;ECID esistente. Inoltre, l’SDK scrive i cookie AMCV in modo che, se l’ECID viene ottenuto per primo su una pagina dotata di strumenti SDK, le pagine successive strumentalizzate con l’API visitatore abbiano lo stesso ECID.
* Quando Adobe Experience Platform Web SDK è configurato in una pagina che dispone anche di API visitatore. Per supportare questo caso, se il cookie AMCV non è impostato, l’SDK cerca l’API visitatore sulla pagina e la chiama per ottenere l’ECID.
* Quando l’intero sito utilizza Adobe Experience Platform Web SDK e non dispone di API visitatore, è utile migrare gli ECID in modo da mantenere le informazioni sul visitatore restituito. Una volta implementato l’SDK con `idMigrationEnabled` per un periodo di tempo che consente di eseguire la migrazione della maggior parte dei cookie dei visitatori, l’impostazione può essere disattivata.

## Aggiornamento delle caratteristiche per la migrazione

Quando i dati in formato XDM vengono inviati in Audience Manager, questi dovranno essere convertiti in segnali durante la migrazione. Le caratteristiche dovranno essere aggiornate per riflettere le nuove chiavi fornite da XDM. Questo processo viene semplificato utilizzando lo [strumento BAAAM](https://docs.adobe.com/content/help/en/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) creato dall&#39;Audience Manager.

## Server Side Forwarding

Se al momento hai abilitato l&#39;inoltro lato server e stai utilizzando `appmeasurement.js`. e `visitor.js` puoi mantenere attivata la funzionalità di inoltro lato server, senza problemi. Nel back-end, Adobe recupera eventuali segmenti AAM e li aggiunge alla chiamata ad Analytics. Se la chiamata ad Analytics contiene tali segmenti, Analytics non chiamerà Audience Manager per inoltrare alcun dato, quindi non vi è alcuna raccolta dati doppia. Non è necessario alcun suggerimento sulla posizione quando si utilizza l’SDK per web, perché gli stessi endpoint di segmentazione vengono chiamati nel backend.

## Recupero ID visitatore e ID di regione

Se desideri utilizzare l’ID visitatore univoco, utilizza il comando `getIdentity` . `getIdentity` restituisce l&#39;ECID esistente per il visitatore corrente. Per i nuovi visitatori che non dispongono ancora di un ECID, questo comando genera un nuovo ECID. `getIdentity` restituisce anche l’ID di regione del visitatore. Per ulteriori informazioni, consulta la [Guida utente di Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html) .

>[!NOTE]
>
>Questo metodo viene in genere utilizzato con soluzioni personalizzate che richiedono la lettura dell&#39; [!DNL Experience Cloud] ID o richiedono l&#39;hint di posizione Adobe Audience Manager. Non viene utilizzata da un’implementazione standard.

```javascript
alloy("getIdentity")
  .then(function(result) {
    // The command succeeded.
    console.log("ECID:", result.identity.ECID);
    console.log("RegionId:", result.edge.regionId);
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information.
  });
```

## Sincronizzazione delle identità

>[!NOTE]
>
>Il metodo `syncIdentity` è stato rimosso nella versione 2.1.0, oltre alla funzione di hashing. Se utilizzi la versione 2.1.0+ e desideri sincronizzare le identità, puoi inviarle direttamente nell&#39;opzione `xdm` del comando `sendEvent`, nel campo `identityMap` .

Inoltre, [!DNL Identity Service] consente di sincronizzare i propri identificatori con l&#39;ECID utilizzando il comando `syncIdentity` .

>[!NOTE]
>
>Si consiglia vivamente di trasmettere tutte le identità disponibili su ogni comando `sendEvent`. Questo consente di aprire una serie di casi d’uso, inclusa la personalizzazione. Ora che è possibile passare tali identità nel comando `sendEvent`, è possibile posizionarle direttamente nel DataLayer.

La sincronizzazione delle identità consente di identificare un dispositivo/utente utilizzando più identità, di impostarne lo stato di autenticazione e di decidere quale identificatore è considerato quello principale. Se non è stato impostato alcun identificatore come `primary`, il valore predefinito principale sarà `ECID`.

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

Ogni proprietà all&#39;interno di `identityMap` rappresenta le identità appartenenti a un particolare [namespace Identity](../../identity-service/namespaces.md). Il nome della proprietà deve essere il simbolo dello spazio dei nomi identità, che è possibile trovare nell&#39;interfaccia utente di Adobe Experience Platform in &quot;[!UICONTROL Identities]&quot;. Il valore della proprietà deve essere un array di identità relative a tale spazio dei nomi di identità.

Ciascun oggetto identity nell&#39;array identity è strutturato come segue:

### `id`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Stringa | Sì | Nessuno |

ID da sincronizzare per lo spazio dei nomi specificato.

### `authenticationState`

| **Tipo** | **Obbligatorio** | **Valore predefinito** | **Valori possibili** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| Stringa | Sì | ambiguo | ambiguo, autenticato e disconnesso |

Lo stato di autenticazione dell&#39;ID.

### `primary`

| **Tipo** | **Obbligatorio** | **Valore predefinito** |
| -------- | ------------ | ----------------- |
| Booleano | facoltativo | false |

Determina se questa identità deve essere utilizzata come frammento principale nel profilo unificato. Per impostazione predefinita, l’ECID è impostato come identificatore principale dell’utente.
