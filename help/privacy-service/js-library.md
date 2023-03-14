---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Panoramica della libreria JavaScript di Adobe Privacy
description: L’Adobe Libreria JavaScript per la privacy consente di recuperare le identità della persona interessata da utilizzare in Privacy Service.
exl-id: 757bf69e-25bf-4ef9-9787-3e74b213908a
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 6%

---

# Panoramica della libreria JavaScript di Adobe Privacy

In qualità di responsabile del trattamento dei dati, Adobe tratta i dati personali in conformità alle autorizzazioni e alle istruzioni dell’azienda. In qualità di Titolare del trattamento dei dati, l’utente determina i dati personali che Adobe tratta e memorizza per suo conto. A seconda delle informazioni che scegli di inviare tramite le soluzioni Adobe Experience Cloud, Adobe può memorizzare informazioni private applicabili alle normative sulla privacy come [!DNL General Data Protection Regulation] (RGPD) e [!DNL California Consumer Privacy Act] (CCPA) Vedi il documento su [privacy in Adobe Experience Cloud](https://www.adobe.com/it/privacy/marketing-cloud.html) per ulteriori informazioni su come le soluzioni Experience Cloud raccolgono dati privati.

Il **Libreria JavaScript di Adobe Privacy** consente ai titolari del trattamento dei dati di automatizzare il recupero di tutte le identità delle persone interessate generate da [!DNL Experience Cloud] soluzioni per un dominio specifico. Utilizzando l’API fornita da [Adobe Experience Platform Privacy Service](home.md), queste identità possono quindi essere utilizzate per creare richieste di accesso ed eliminazione di dati privati appartenenti a tali persone interessate.

>[!NOTE]
>
>Il [!DNL Privacy JS Library] in genere deve essere installato solo su pagine relative alla privacy e non su tutte le pagine di un sito web o di un dominio.

## Funzioni

Il [!DNL Privacy JS Library] fornisce diverse funzioni per la gestione delle identità in [!DNL Privacy Service]. Queste funzioni possono essere utilizzate solo per gestire le identità memorizzate nel browser per un visitatore specifico. Non possono essere utilizzati per inviare informazioni al [!DNL Experience Cloud Central Service] direttamente.

La tabella seguente illustra le diverse funzioni fornite dalla libreria:

| Funzione | Descrizione |
| --- | --- |
| `retrieveIdentities` | Restituisce una matrice di identità corrispondenti (`validIds`) recuperati da [!DNL Privacy Service], nonché un array di identità che non sono state trovate (`failedIds`). |
| `removeIdentities` | Rimuove ogni identità (valida) corrispondente dal browser. Restituisce una matrice di identità corrispondenti (`validIds`), con ogni identità contenente un `isDeletedClientSide` booleano che indica se questo ID è stato eliminato. |
| `retrieveThenRemoveIdentities` | Recupera un array di identità corrispondenti (`validIds`) e rimuove tali identità dal browser. Questa funzione è simile a `removeIdentities`, è indicato quando la soluzione di Adobe in uso richiede una richiesta di accesso prima che sia possibile eliminarla (ad esempio quando è necessario recuperare un identificatore univoco prima di fornirlo in una richiesta di eliminazione). |

>[!NOTE]
>
>`removeIdentities` e `retrieveThenRemoveIdentities` rimuovi le identità dal browser solo per specifiche soluzioni di Adobe che le supportano. Ad esempio, Adobe Audience Manager non elimina gli ID demdex memorizzati nei cookie di terze parti, mentre Adobe Target elimina tutti i cookie che memorizzano i loro ID.

Poiché tutte e tre le funzioni rappresentano processi asincroni, tutte le identità recuperate devono essere gestite utilizzando callback o promesse.


## Installazione

Per iniziare a utilizzare [!DNL Privacy JS Library], è necessario installarlo nel computer utilizzando uno dei seguenti metodi:

* Eseguire l&#39;installazione utilizzando npm eseguendo il comando seguente: `npm install @adobe/adobe-privacy`
* Scarica da [Experience Cloud archivio GitHub](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

Puoi anche installare la libreria tramite un’estensione tag. Consulta la panoramica su [Estensione tag Adobe Privacy](../tags/extensions/client/privacy/overview.md) per ulteriori informazioni.

## Crea un&#39;istanza di [!DNL Privacy JS Library]

Tutte le app che utilizzano [!DNL Privacy JS Library] deve creare un&#39;istanza di un nuovo `AdobePrivacy` oggetto, che deve essere configurato per una soluzione di Adobe specifica. Ad esempio, la creazione di un’istanza per Adobe Analytics sarà simile alla seguente:

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{ORG_ID}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Per un elenco completo dei parametri supportati per le diverse soluzioni Adobe, consulta la sezione dell’appendice relativa ai parametri supportati [Adobe di parametri di configurazione della soluzione](#adobe-solution-configuration-parameters).

## Esempi di codice {#samples}

Gli esempi di codice seguenti mostrano come utilizzare [!DNL Privacy JS Library] per diversi scenari comuni, purché non si utilizzino i tag.

### Recupera identità

Questo esempio illustra come recuperare un elenco di identità da [!DNL Experience Cloud].

#### JavaScript

Il codice che segue definisce una funzione, `handleRetrievedIDs`, da utilizzare come callback o promessa per la gestione delle identità recuperate da `retrieveIdentities`.

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

| Variable | Descrizione |
| --- | --- |
| `validIds` | Oggetto JSON contenente tutti gli ID recuperati correttamente. |
| `failedIDs` | Un oggetto JSON contenente tutti gli ID che non sono stati recuperati da [!DNL Privacy Service]o non è stato possibile trovarli. |

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

Il codice che segue definisce una funzione, `handleRemovedIDs`, da utilizzare come callback o promessa per la gestione delle identità recuperate da `removeIdentities` dopo che sono stati rimossi dal browser.

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

| Variable | Descrizione |
| --- | --- |
| `validIds` | Oggetto JSON contenente tutti gli ID recuperati correttamente. |
| `failedIDs` | Un oggetto JSON contenente tutti gli ID che non sono stati recuperati da [!DNL Privacy Service]o non è stato possibile trovarli. |

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

Una volta letto questo documento, potrai conoscere le funzionalità principali di [!DNL Privacy JS Library]. Dopo aver utilizzato la libreria per recuperare un elenco di identità, puoi utilizzarle per creare richieste di accesso e di cancellazione dei dati a [!DNL Privacy Service] API. Consulta la [Guida all’API di Privacy Service](api/overview.md) per ulteriori informazioni.

## Appendice

Questa sezione contiene informazioni supplementari sull&#39;utilizzo di [!DNL Privacy JS Library].

### Adobe di parametri di configurazione della soluzione {#config-params}

Di seguito è riportato un elenco dei parametri di configurazione accettati per le soluzioni Adobe supportate, utilizzati quando [creazione di un&#39;istanza di un oggetto AdobePrivacy](#instantiate-the-privacy-js-library).

**Tutte le soluzioni**

| Parametro | Descrizione |
| --- | --- |
| `key` | Un ID univoco che identifica l’utente o l’interessato. Questa proprietà è destinata all’utilizzo per scopi di tracciamento interni e non viene utilizzata da Adobe. |

**Adobe Analytics**

| Parametro | Descrizione |
| --- | --- |
| `cookieDomainPeriods` | Il numero di periodi in un dominio utilizzato per il tracciamento dei cookie (impostazione predefinita: `2`, ad es. `.domain.com`). Non definirlo qui a meno che non sia specificato nel beacon web JavaScript. |
| `dataCenter` | L’Adobe di data collection center. Questo deve essere incluso solo se è specificato nel beacon web JavaScript. I valori potenziali sono: <ul><li>`d1`: data center di San Jose</li><li>`d2`: datacenter di Dallas</li></ul> |
| `reportSuite` | L’ID suite di rapporti come specificato nel beacon web JavaScript (ad esempio, `s_code.js` o `dtm`). |
| `trackingServer` | Un dominio di raccolta dati non SSL. Questo deve essere incluso solo se è specificato nel beacon web JavaScript. |
| `trackingServerSecure` | Un dominio di raccolta dati SSL. Questo deve essere incluso solo se è specificato nel beacon web JavaScript. |
| `visitorNamespace` | Lo spazio dei nomi utilizzato per raggruppare i visitatori. Questo deve essere incluso solo se è specificato nel beacon web JavaScript. |

**Adobe Audience Manager**

| Parametro | Descrizione |
| --- | --- |
| `aamUUIDCookieName` | Nome del cookie di prima parte contenente l’ID utente univoco restituito da Adobe Audience Manager. |

**Servizio Adobe Experience Cloud Identity (ECID)**

| Parametro | Descrizione |
| --- | --- |
| `imsOrgID` | ID organizzazione IMS. |

**Adobe Target**

| Parametro | Descrizione |
| --- | --- |
| `clientCode` | Codice client che identifica un client in Adobe Target System. |
