---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Panoramica della libreria JavaScript sulla privacy di Adobe
description: La libreria JavaScript per la privacy di Adobe consente di recuperare le identità dell’interessato da utilizzare in Privacy Service.
exl-id: 757bf69e-25bf-4ef9-9787-3e74b213908a
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 6%

---

# Panoramica della libreria JavaScript per la privacy di Adobe

In qualità di responsabile del trattamento dei dati, Adobe tratta i dati personali secondo le autorizzazioni e le istruzioni della tua azienda. In qualità di Titolare del trattamento dei dati, l’utente determina i dati personali che Adobe tratta e memorizza per suo conto. A seconda delle informazioni che scegli di inviare tramite le soluzioni Adobe Experience Cloud, Adobe può memorizzare informazioni private applicabili alle normative sulla privacy come [!DNL General Data Protection Regulation] (RGPD) e [!DNL California Consumer Privacy Act] (CCPA). Visualizza il documento in [privacy in Adobe Experience Cloud](https://www.adobe.com/it/privacy/marketing-cloud.html) per ulteriori informazioni su come le soluzioni Experience Cloud raccolgono dati privati.

La **Adobe Libreria JavaScript per la privacy** consente ai titolari del trattamento di automatizzare il recupero di tutte le identità delle persone interessate generate da [!DNL Experience Cloud] soluzioni per un dominio specifico. Utilizzo dell’API fornita da [Adobe Experience Platform Privacy Service](home.md), queste identità possono quindi essere utilizzate per creare richieste di accesso ed eliminazione per i dati privati appartenenti a tali soggetti.

>[!NOTE]
>
>La [!DNL Privacy JS Library] in genere deve essere installato solo su pagine relative alla privacy e non deve essere installato su tutte le pagine di un sito web o di un dominio.

## Funzioni

La [!DNL Privacy JS Library] fornisce diverse funzioni per la gestione delle identità in [!DNL Privacy Service]. Queste funzioni possono essere utilizzate solo per gestire le identità memorizzate nel browser per un visitatore specifico. Non possono essere utilizzati per inviare informazioni al [!DNL Experience Cloud Central Service] direttamente.

La tabella seguente illustra le diverse funzioni fornite dalla libreria:

| Funzione | Descrizione |
| --- | --- |
| `retrieveIdentities` | Restituisce una matrice di identità corrispondenti (`validIds`) recuperate da [!DNL Privacy Service], nonché una serie di identità non trovate (`failedIds`). |
| `removeIdentities` | Rimuove ogni identità corrispondente (valida) dal browser. Restituisce una matrice di identità corrispondenti (`validIds`), con ogni identità contenente un `isDeletedClientSide` booleano che indica se l&#39;ID è stato eliminato. |
| `retrieveThenRemoveIdentities` | Recupera un array di identità corrispondenti (`validIds`) e quindi rimuove tali identità dal browser. Anche se questa funzione è simile a `removeIdentities`, viene utilizzato al meglio quando la soluzione di Adobe in uso richiede una richiesta di accesso prima che sia possibile eliminarla (ad esempio quando è necessario recuperare un identificatore univoco prima di fornirlo in una richiesta di eliminazione). |

>[!NOTE]
>
>`removeIdentities` e `retrieveThenRemoveIdentities` rimuovi le identità solo dal browser per specifiche soluzioni di Adobe che le supportano. Ad esempio, Adobe Audience Manager non elimina gli ID demdex memorizzati nei cookie di terze parti, mentre Adobe Target elimina tutti i cookie che memorizzano gli ID.

Poiché tutte e tre le funzioni rappresentano processi asincroni, tutte le identità recuperate devono essere gestite utilizzando callback o promesse.


## Installazione

Per iniziare a utilizzare [!DNL Privacy JS Library], è necessario installarlo nel computer utilizzando uno dei seguenti metodi:

* Installare utilizzando npm eseguendo il seguente comando: `npm install @adobe/adobe-privacy`
* Scarica da [Archivio Experience Cloud GitHub](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

Puoi anche installare la libreria tramite un’estensione tag. Vedi la panoramica sul [Estensione del tag Privacy di Adobe](../tags/extensions/client/privacy/overview.md) per ulteriori informazioni.

## Creare un&#39;istanza del [!DNL Privacy JS Library]

Tutte le app che utilizzano [!DNL Privacy JS Library] deve creare un&#39;istanza nuova `AdobePrivacy` oggetto , che deve essere configurato in una soluzione di Adobe specifica. Ad esempio, un’istanza per Adobe Analytics avrà un aspetto simile al seguente:

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{ORG_ID}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Per un elenco completo dei parametri supportati per diverse soluzioni di Adobe, vedi la sezione appendice sul supporto [Adobe di parametri di configurazione della soluzione](#adobe-solution-configuration-parameters).

## Esempi di codice {#samples}

Gli esempi di codice seguenti mostrano come utilizzare il [!DNL Privacy JS Library] per diversi scenari comuni, purché non si utilizzino tag.

### Recupera identità

Questo esempio illustra come recuperare un elenco di identità da [!DNL Experience Cloud].

#### JavaScript

Il codice seguente definisce una funzione, `handleRetrievedIDs`, da utilizzare come callback o promessa di gestire le identità recuperate da `retrieveIdentities`.

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
| `validIds` | Un oggetto JSON contenente tutti gli ID recuperati correttamente. |
| `failedIDs` | Un oggetto JSON contenente tutti gli ID non recuperati da [!DNL Privacy Service]oppure non è stato possibile trovarli. |

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

Il codice seguente definisce una funzione, `handleRemovedIDs`, da utilizzare come callback o promessa di gestire le identità recuperate da `removeIdentities` dopo essere stati rimossi dal browser.

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
| `validIds` | Un oggetto JSON contenente tutti gli ID recuperati correttamente. |
| `failedIDs` | Un oggetto JSON contenente tutti gli ID non recuperati da [!DNL Privacy Service]oppure non è stato possibile trovarli. |

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

Leggendo questo documento, sei stato introdotto alle funzionalità principali di [!DNL Privacy JS Library]. Dopo aver utilizzato la libreria per recuperare un elenco di identità, puoi utilizzarle per creare le richieste di accesso e di cancellazione dei dati per il [!DNL Privacy Service] API. Consulta la sezione [Guida all’API di Privacy Service](api/overview.md) per ulteriori informazioni.

## Appendice

Questa sezione contiene informazioni supplementari per l&#39;utilizzo del [!DNL Privacy JS Library].

### Adobe di parametri di configurazione della soluzione {#config-params}

Di seguito è riportato un elenco dei parametri di configurazione accettati per le soluzioni Adobe supportate, utilizzati quando [creazione di un&#39;istanza di un oggetto AdobePrivacy](#instantiate-the-privacy-js-library).

**Tutte le soluzioni**

| Parametro | Descrizione |
| --- | --- |
| `key` | Un ID univoco che identifica l&#39;utente o la persona interessata. Questa proprietà è destinata all&#39;uso a scopi di tracciamento interni e non viene utilizzata da Adobe. |

**Adobe Analytics**

| Parametro | Descrizione |
| --- | --- |
| `cookieDomainPeriods` | Il numero di periodi in un dominio utilizzato per il tracciamento dei cookie (impostazione predefinita: `2`ad esempio `.domain.com`). Non definirlo qui a meno che non sia specificato nel beacon web JavaScript. |
| `dataCenter` | Il data center di raccolta dati di Adobe. Deve essere incluso solo se è specificato nel beacon web JavaScript. I valori potenziali sono: <ul><li>`d1`: Centro dati San Jose</li><li>`d2`: Centro dati di Dallas</li></ul> |
| `reportSuite` | L’ID suite di rapporti specificato nel beacon web JavaScript (ad esempio, `s_code.js` o `dtm`). |
| `trackingServer` | Un dominio di raccolta dati non SSL. Deve essere incluso solo se è specificato nel beacon web JavaScript. |
| `trackingServerSecure` | Un dominio di raccolta dati SSL. Deve essere incluso solo se è specificato nel beacon web JavaScript. |
| `visitorNamespace` | Lo spazio dei nomi utilizzato per raggruppare i visitatori. Deve essere incluso solo se è specificato nel beacon web JavaScript. |

**Adobe Audience Manager**

| Parametro | Descrizione |
| --- | --- |
| `aamUUIDCookieName` | Nome del cookie di prime parti contenente l’ID utente univoco restituito da Adobe Audience Manager. |

**Servizio Adobe Experience Cloud Identity (ECID)**

| Parametro | Descrizione |
| --- | --- |
| `imsOrgID` | Il tuo ID organizzazione. |

**Adobe Target**

| Parametro | Descrizione |
| --- | --- |
| `clientCode` | Codice client che identifica un client in Adobe Target System. |
