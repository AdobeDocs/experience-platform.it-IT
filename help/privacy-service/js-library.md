---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Panoramica della libreria JavaScript di Adobe Privacy
description: L’Adobe Privacy JavaScript Library consente di recuperare le identità delle persone interessate da utilizzare in Privacy Service.
exl-id: 757bf69e-25bf-4ef9-9787-3e74b213908a
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 3%

---

# Panoramica della libreria JavaScript di Adobe Privacy

In qualità di responsabile del trattamento dei dati, Adobe tratta i dati personali in conformità alle autorizzazioni e alle istruzioni dell’azienda. In qualità di titolare del trattamento dei dati, l’utente determina i dati personali che Adobe tratta e archivia per suo conto. A seconda delle informazioni che scegli di inviare tramite le soluzioni Adobe Experience Cloud, Adobe può memorizzare informazioni private applicabili alle normative sulla privacy come [!DNL General Data Protection Regulation] (RGPD) e [!DNL California Consumer Privacy Act] (CCPA). Per ulteriori informazioni sulla raccolta di dati privati da parte delle soluzioni Experience Cloud, consulta il documento sulla [privacy in Adobe Experience Cloud](https://www.adobe.com/it/privacy/marketing-cloud.html).

La **Adobe Privacy JavaScript Library** consente ai titolari del trattamento dei dati di automatizzare il recupero di tutte le identità delle persone interessate generate dalle soluzioni [!DNL Experience Cloud] per un dominio specifico. Utilizzando l&#39;API fornita da [Adobe Experience Platform Privacy Service](home.md), queste identità possono quindi essere utilizzate per creare richieste di accesso ed eliminazione per dati privati appartenenti a tali interessati.

>[!NOTE]
>
>[!DNL Privacy JS Library] in genere deve essere installato solo nelle pagine relative alla privacy e non in tutte le pagine di un sito Web o di un dominio.

## Funzioni

[!DNL Privacy JS Library] fornisce diverse funzioni per la gestione delle identità in [!DNL Privacy Service]. Queste funzioni possono essere utilizzate solo per gestire le identità memorizzate nel browser per un visitatore specifico. Non possono essere utilizzati per inviare informazioni direttamente a [!DNL Experience Cloud Central Service].

La tabella seguente illustra le diverse funzioni fornite dalla libreria:

| Funzione | Descrizione |
| --- | --- |
| `retrieveIdentities` | Restituisce una matrice di identità corrispondenti (`validIds`) recuperate da [!DNL Privacy Service], nonché una matrice di identità non trovate (`failedIds`). |
| `removeIdentities` | Rimuove ogni identità (valida) corrispondente dal browser. Restituisce una matrice di identità corrispondenti (`validIds`), con ogni identità contenente un valore booleano `isDeletedClientSide` che indica se questo ID è stato eliminato. |
| `retrieveThenRemoveIdentities` | Recupera un array di identità corrispondenti (`validIds`), quindi rimuove tali identità dal browser. Questa funzione è simile a `removeIdentities` ma è preferibile utilizzarla quando la soluzione di Adobe in uso richiede una richiesta di accesso prima dell&#39;eliminazione (ad esempio quando è necessario recuperare un identificatore univoco prima di fornirlo in una richiesta di eliminazione). |

>[!NOTE]
>
>`removeIdentities` e `retrieveThenRemoveIdentities` rimuovono identità dal browser solo per specifiche soluzioni di Adobe che le supportano. Ad esempio, Adobe Audience Manager non elimina gli ID demdex memorizzati nei cookie di terze parti, mentre Adobe Target elimina tutti i cookie che memorizzano i loro ID.

Poiché tutte e tre le funzioni rappresentano processi asincroni, tutte le identità recuperate devono essere gestite utilizzando callback o promesse.


## Installazione

Per iniziare a utilizzare [!DNL Privacy JS Library], è necessario installarlo nel computer utilizzando uno dei metodi seguenti:

* Eseguire l&#39;installazione utilizzando npm eseguendo il comando seguente: `npm install @adobe/adobe-privacy`
* Scarica dall&#39;archivio GitHub [Experience Cloud](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

Puoi anche installare la libreria tramite un’estensione tag. Per ulteriori informazioni, consulta la panoramica sull&#39;estensione tag [Adobe Privacy](../tags/extensions/client/privacy/overview.md).

## Crea istanza di [!DNL Privacy JS Library]

Tutte le app che utilizzano [!DNL Privacy JS Library] devono creare un&#39;istanza di un nuovo oggetto `AdobePrivacy`, che deve essere configurato per una soluzione di Adobe specifica. Ad esempio, la creazione di un’istanza per Adobe Analytics sarà simile alla seguente:

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{ORG_ID}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Per un elenco completo dei parametri supportati per le diverse soluzioni Adobe, consulta la sezione dell&#39;appendice sui [parametri di configurazione della soluzione Adobe supportati](#adobe-solution-configuration-parameters).

## Esempi di codice {#samples}

Negli esempi di codice seguenti viene illustrato come utilizzare [!DNL Privacy JS Library] per diversi scenari comuni, purché non si utilizzino i tag.

### Recupera identità

Questo esempio illustra come recuperare un elenco di identità da [!DNL Experience Cloud].

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

| Variable | Descrizione |
| --- | --- |
| `validIds` | Oggetto JSON contenente tutti gli ID recuperati correttamente. |
| `failedIDs` | Impossibile trovare un oggetto JSON contenente tutti gli ID non recuperati da [!DNL Privacy Service]. |

#### Risultato

Se il codice viene eseguito correttamente, `validIDs` viene popolato con un elenco di identità recuperate.

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

Il codice seguente definisce una funzione, `handleRemovedIDs`, da utilizzare come callback o promessa per gestire le identità recuperate da `removeIdentities` dopo che sono state rimosse dal browser.

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
| `failedIDs` | Impossibile trovare un oggetto JSON contenente tutti gli ID non recuperati da [!DNL Privacy Service]. |

#### Risultato

Se il codice viene eseguito correttamente, `validIDs` viene popolato con un elenco di identità recuperate.

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

Dopo aver letto questo documento, potrai conoscere le funzionalità principali di [!DNL Privacy JS Library]. Dopo aver utilizzato la libreria per recuperare un elenco di identità, è possibile utilizzare tali identità per creare richieste di accesso e di eliminazione dei dati per l&#39;API [!DNL Privacy Service]. Per ulteriori informazioni, consulta la [guida dell&#39;API Privacy Service](api/overview.md).

## Appendice

Questa sezione contiene informazioni supplementari per l&#39;utilizzo di [!DNL Privacy JS Library].

### Adobe di parametri di configurazione della soluzione {#config-params}

Di seguito è riportato un elenco dei parametri di configurazione accettati per le soluzioni Adobe supportate, utilizzati durante la creazione di un&#39;istanza di un oggetto AdobePrivacy](#instantiate-the-privacy-js-library).[

**Tutte le soluzioni**

| Parametro | Descrizione |
| --- | --- |
| `key` | Un ID univoco che identifica l’utente o l’interessato. Questa proprietà è destinata all’utilizzo per scopi di tracciamento interni e non viene utilizzata da Adobe. |

**Adobe Analytics**

| Parametro | Descrizione |
| --- | --- |
| `cookieDomainPeriods` | Il numero di periodi in un dominio utilizzato per il tracciamento dei cookie (impostazione predefinita: `2`, ad esempio `.domain.com`). Non definirlo qui a meno che non sia specificato nel beacon web JavaScript. |
| `dataCenter` | L’Adobe di data collection center. Questo deve essere incluso solo se è specificato nel beacon web JavaScript. I valori potenziali sono: <ul><li>`d1`: data center di San Jose</li><li>`d2`: datacenter di Dallas</li></ul> |
| `reportSuite` | ID suite di rapporti come specificato nel beacon Web JavaScript (ad esempio, `s_code.js` o `dtm`). |
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
| `imsOrgID` | ID organizzazione. |

**Adobe Target**

| Parametro | Descrizione |
| --- | --- |
| `clientCode` | Codice client che identifica un client in Adobe Target System. |
