---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Panoramica della libreria JavaScript per la privacy di Adobe
topic: overview
translation-type: tm+mt
source-git-commit: 3b916ac5529db6ca383bf8bad56961bb1b8a0b0c

---


# Panoramica della libreria JavaScript per la privacy di Adobe

In qualità di elaboratore di dati, Adobe elabora i dati personali in conformità con le autorizzazioni e le istruzioni della tua azienda. In qualità di Titolare del trattamento dei dati, l’utente determina i dati personali che Adobe tratta e memorizza per suo conto. A seconda delle informazioni che scegli di inviare tramite le soluzioni Adobe Experience Cloud, Adobe può archiviare informazioni private applicabili alle normative sulla privacy, come il Regolamento generale sulla protezione dei dati (GDPR) e l&#39;Atto sulla privacy dei consumatori della California (CCPA). Consulta il documento sulla [privacy in Adobe Experience Cloud](https://www.adobe.com/privacy/marketing-cloud.html) per ulteriori informazioni su come le soluzioni Experience Cloud raccolgono i dati privati.

La libreria **JavaScript per la privacy di** Adobe consente ai controller di dati di automatizzare il recupero di tutte le identità degli oggetti dati generate dalle soluzioni Experience Cloud per un dominio specifico. Utilizzando l&#39;API fornita dal servizio [per la privacy di](home.md)Adobe Experience Platform, queste identità possono essere utilizzate per creare richieste di accesso ed eliminazione di dati privati appartenenti a tali soggetti.

>[!NOTE] In genere, la Libreria JS per la privacy deve essere installata solo sulle pagine relative alla privacy e non deve essere installata su tutte le pagine di un sito Web o di un dominio.

## Funzioni

La Privacy JS Library offre diverse funzioni per la gestione delle identità nel servizio Privacy. Queste funzioni possono essere utilizzate solo per gestire le identità memorizzate nel browser per un visitatore specifico. Non possono essere utilizzati per inviare informazioni direttamente al servizio Experience Cloud Central.

Nella tabella seguente sono illustrate le diverse funzioni fornite dalla libreria:

| Funzione | Descrizione |
| --- | --- |
| `retrieveIdentities` | Restituisce un array di identità corrispondenti (`validIds`) recuperate dal servizio Privacy, oltre a un array di identità non trovate (`failedIds`). |
| `removeIdentities` | Rimuove ogni identità corrispondente (valida) dal browser. Restituisce un array di identità corrispondenti (`validIds`), con ogni identità contenente un valore `isDeleteClientSide` booleano che indica se l&#39;ID è stato eliminato. |
| `retrieveThenRemoveIdentities` | Recupera un array di identità corrispondenti (`validIds`), quindi rimuove tali identità dal browser. Anche se questa funzione è simile a `removeIdentities`, è meglio utilizzarla quando la soluzione Adobe in uso richiede una richiesta di accesso prima che sia possibile eliminarla (ad esempio quando è necessario recuperare un identificatore univoco prima di distribuirlo in una richiesta di eliminazione). |

>[!NOTE] e `removeIdentities` `retrieveThenRemoveIdentities` rimuovete dal browser le identità solo per le soluzioni Adobe specifiche che le supportano. Ad esempio, Adobe Audience Manager non elimina gli ID demdex memorizzati nei cookie di terze parti, mentre Adobe Target elimina tutti i cookie che memorizzano i loro ID.

Poiché tutte e tre le funzioni rappresentano processi asincroni, tutte le identità recuperate devono essere gestite mediante callback o promesse.


## Installazione

Per iniziare a utilizzare la libreria JS Privacy, è necessario installarla nel computer utilizzando uno dei seguenti metodi:

* Installate utilizzando npm eseguendo il comando seguente: `npm install @adobe/adobe-privacy`
* Utilizzate Adobe Launch Extension con il nome `AdobePrivacy`
* Scarica da [https://github.com/Adobe-Marketing-Cloud/adobe-privacy](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

## Creare un&#39;istanza della libreria JS per la privacy

Tutte le app che utilizzano la libreria JS per la privacy devono creare un&#39;istanza di un nuovo `AdobePrivacy` oggetto, che deve essere configurato in una soluzione Adobe specifica. Ad esempio, un&#39;istanza per Adobe Analytics sarà simile all&#39;esempio seguente:

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{IMS_ORG}",
    key: "{DATA_SUBJECT_ID}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Per un elenco completo dei parametri supportati per diverse soluzioni Adobe, vedete la sezione appendice sui parametri [di configurazione della soluzione](#adobe-solution-configuration-parameters)Adobe supportati.

## Esempi di codice

Gli esempi di codice riportati di seguito illustrano come utilizzare la libreria JS per la privacy per diversi scenari comuni, a condizione che non si utilizzi Launch o DTM.

### Recupera identità

Questo esempio illustra come recuperare un elenco di identità da Experience Cloud.

#### JavaScript

Il codice seguente definisce una funzione, `handleRetrievedIDs`, da utilizzare come callback o promessa per gestire le identità recuperate da `retrieveIdentities`.

```javascript
function handleRetrievedIDs(ids) {
    const validIDs = ids.validIDs;
    const failedIDs = ids.failedIDs;
}

// If using callbacks:
adobePrivacy.retrieveIdentities(handleRetrievedIDs);

// If using promises:
adobePrivacy.retrieveIdentities().then(handleRetrievedIDs);
```

| Variabile | Descrizione |
| --- | --- |
| `validIds` | Un oggetto JSON contenente tutti gli ID recuperati. |
| `failedIDs` | Un oggetto JSON contenente tutti gli ID che non sono stati recuperati dal servizio per la privacy o che altrimenti non potevano essere trovati. |

#### Risultato

Se il codice viene eseguito correttamente, `validIDs` viene compilato con un elenco di identità recuperate.

```json
{
    "company": "adobe",
    "namespace": "ECID",
    "namespaceId": 4,
    "type": "standard",
    "name": "Experience Cloud ID",
    "description": "This is the ID generated by the ID Service.",
    "value": "79352169365966186342525781172209986543"
},
{
    "company": "adobe",
    "namespace": "gsurfer_id",
    "namespaceId": 411,
    "type": "standard",
    "value": "WqmIJQAAB669Ciao"
}
```

### Rimuovi le identità

Questo esempio illustra come rimuovere un elenco di identità dal browser.

#### JavaScript

Il codice seguente definisce una funzione, `handleRemovedIDs`, da utilizzare come callback o promessa di gestire le identità recuperate da `removeIdentities` dopo che sono state rimosse dal browser.

```javascript
function handleRemovedIDs(ids) {
    const validIDs = ids.validIDs;
    const failedIDs = ids.failedIDs;
}

// If using callbacks:
adobePrivacy.removeIdentities(handleRemovedIDs);

// If using promises:
adobePrivacy.removeIdentities().then(handleRemovedIDs)…
```

| Variabile | Descrizione |
| --- | --- |
| `validIds` | Un oggetto JSON contenente tutti gli ID recuperati. |
| `failedIDs` | Un oggetto JSON contenente tutti gli ID che non sono stati recuperati dal servizio per la privacy o che altrimenti non potevano essere trovati. |

#### Risultato

Se il codice viene eseguito correttamente, `validIDs` viene compilato con un elenco di identità recuperate.

```json
{
    "company": "adobe",
    "namespace": "ECID",
    "namespaceId": 4,
    "type": "standard",
    "name": "Experience Cloud ID",
    "description": "This is the ID generated by the ID Service.",
    "value": "79352169365966186342525781172209986543",
    "isDeletedClientSide": false
},
{
    "company": "adobe",
    "namespace": "AMO",
    "namespaceId": 411,
    "type": "standard",
    "value": "WqmIJQAAB669Ciao",
    "isDeletedClientSide": true
}
```

## Passaggi successivi

Leggendo questo documento, ti sono state introdotte le funzionalità di base della Privacy JS Library. Dopo aver utilizzato la libreria per recuperare un elenco di identità, è possibile utilizzare tali identità per creare l&#39;accesso ai dati ed eliminare le richieste all&#39;API del servizio Privacy. Per ulteriori informazioni, consulta la guida [per gli sviluppatori del servizio](api/getting-started.md) Privacy.

## Appendice

Questa sezione contiene informazioni supplementari per l&#39;utilizzo della libreria JS Privacy.

### Parametri di configurazione della soluzione Adobe

Di seguito è riportato un elenco dei parametri di configurazione accettati per le soluzioni Adobe supportate, utilizzati per [creare un&#39;istanza di un oggetto](#instantiate-the-privacy-js-library)AdobePrivacy.

**Adobe Analytics** 

| Parametro | Descrizione |
| --- | --- |
| `cookieDomainPeriods` | Il numero di periodi in un dominio per il tracciamento dei cookie (impostazione predefinita: 2). |
| `dataCenter` | Centro dati di raccolta dati Adobe. Deve essere incluso solo se specificato nel beacon Web JavaScript. I valori potenziali sono: <ul><li>&quot;d1&quot;: Centro dati San Jose.</li><li>&quot;d2&quot;: Centro dati di Dallas.</li></ul> |
| `reportSuite` | ID suite di rapporti come specificato nel beacon Web JavaScript (ad esempio, &quot;s_code.js&quot; o &quot;dtm&quot;). |
| `trackingServer` | Dominio di raccolta dati (non SSL). Deve essere incluso solo se specificato nel beacon Web JavaScript. |
| `trackingServerSecure` | Dominio di raccolta dati (SSL). Deve essere incluso solo se specificato nel beacon Web JavaScript. |
| `visitorNamespace` | Spazio dei nomi utilizzato per raggruppare i visitatori. Deve essere incluso solo se specificato nel beacon Web JavaScript. |

**Adobe Target**

| Parametro | Descrizione |
| --- | --- |
| `clientCode` | Codice client che identifica un client in Adobe Target System. |

**Adobe Audience Manager**

| Parametro | Descrizione |
| --- | --- |
| `aamUUIDCookieName` | Nome del cookie di prima parte contenente l’ID utente univoco restituito da Adobe Audience Manager. |

**Adobe ID Service (ECID)**

| Parametro | Descrizione |
| --- | --- |
| `imsOrgID` | L’ID organizzazione IMS. |