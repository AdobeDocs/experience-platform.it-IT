---
title: Dati di identità nell’SDK per web di Platform
description: Scopri come recuperare e gestire gli ID Adobe Experience Cloud (ECID) utilizzando l’SDK web Adobe Experience Platform.
keywords: identità;identità di prima parte;servizio Identity;identità di terze parti;migrazione ID;ID visitatore;identità di terze parti;cookie di terze partiabilitati;idMigrationEnabled;getIdentity;identità di sincronizzazione;syncIdentity;sendEvent;identityMap;primario;ecid;spazio dei nomi;ID spazio dei nomi;authenticationState;hashEnabled;
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 85ff35e0e7f7e892de5252e8f3ad069eff83aa15
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 1%

---

# Dati di identità nell’SDK per web di Platform

L&#39;SDK Web di Adobe Experience Platform sfrutta [ID Adobe Experience Cloud (ECID)](../../identity-service/ecid.md) per tenere traccia del comportamento dei visitatori. Utilizzando gli ECID, puoi garantire che ogni dispositivo abbia un identificatore univoco che possa persistere in più sessioni, legando tutti gli hit che si verificano durante e tra sessioni web a un dispositivo specifico.

Questo documento fornisce una panoramica sulla gestione degli ECID tramite l’SDK per web di Platform.

## Tracciamento degli ECID tramite l’SDK

L’SDK per web di Platform assegna e tiene traccia degli ECID tramite l’uso dei cookie, con diversi metodi disponibili per configurare la modalità di generazione di tali cookie.

Quando un nuovo utente arriva sul tuo sito web, il servizio Adobe Experience Cloud Identity tenta di impostare un cookie di identificazione del dispositivo per tale utente. Per i nuovi visitatori, viene generato e restituito un ECID nella prima risposta da Adobe Experience Platform Edge Network. Per i visitatori ripetuti, l’ECID viene recuperato dal `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` e aggiunto al payload da Edge Network.

Una volta impostato il cookie contenente l’ECID, ogni richiesta successiva generata dall’SDK per web includerà un ECID codificato nel `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` cookie.

Quando si utilizzano i cookie per l’identificazione del dispositivo, è possibile interagire con la rete Edge in due modi:

1. Invia i dati direttamente al dominio di Edge Network `adobedc.net`. Questo metodo è indicato come [raccolta dati di terze parti](#third-party).
1. Crea un CNAME sul tuo dominio che punta a `adobedc.net`. Questo metodo è indicato come [raccolta dati di prime parti](#first-party).

Come spiegato nelle sezioni seguenti, il metodo di raccolta dati che scegli di utilizzare ha un impatto diretto sulla durata dei cookie nei vari browser.

### Raccolta di dati di terze parti {#third-party}

La raccolta dati di terze parti comporta l’invio diretto di dati al dominio Edge Network `adobedc.net`.

Negli ultimi anni, i browser web stanno diventando sempre più restrittivi nella gestione dei cookie impostati da terze parti. Per impostazione predefinita, alcuni browser bloccano i cookie di terze parti. Se utilizzi cookie di terze parti per identificare i visitatori del sito, la durata di questi cookie è quasi sempre inferiore a quella altrimenti disponibile utilizzando i cookie di prime parti. In alcuni casi, un cookie di terze parti scadrà in appena sette giorni.

Inoltre, quando si utilizza la raccolta dati di terze parti, alcuni ad blocker limitano del tutto il traffico agli endpoint di raccolta dati di Adobe.

### Raccolta di dati di prime parti {#first-party}

La raccolta dati di prime parti comporta l’impostazione di cookie tramite un CNAME sul tuo dominio che punta a `adobedc.net`.

Sebbene i browser abbiano trattato a lungo i cookie impostati dagli endpoint CNAME in modo simile a quelli impostati dagli endpoint di proprietà del sito, le modifiche recenti implementate dai browser hanno creato una distinzione nel modo in cui vengono gestiti i cookie CNAME. Anche se non ci sono browser che attualmente bloccano i cookie CNAME di prime parti per impostazione predefinita, alcuni browser limitano la durata dei cookie impostati con un CNAME a soli sette giorni.

### Effetti della durata dei cookie sulle applicazioni Adobe Experience Cloud {#lifespans}

Indipendentemente dalla scelta della raccolta dati di prime parti o terze parti, il periodo di tempo in cui un cookie può persistere ha un impatto diretto sui conteggi dei visitatori in Adobe Analytics e Customer Journey Analytics. Inoltre, gli utenti finali possono riscontrare esperienze di personalizzazione incoerenti quando si utilizza Adobe Target o Offer Decisioning sul sito.

Ad esempio, considera una situazione in cui hai creato un’esperienza di personalizzazione che promuoverà qualsiasi elemento nella home page se un utente lo ha visualizzato tre volte negli ultimi sette giorni.

Se un utente finale visita il sito tre volte alla settimana e poi non torna al sito per sette giorni, tale uso potrebbe essere considerato un nuovo utente quando torna al sito, perché i suoi cookie potrebbero essere stati cancellati da un criterio del browser (a seconda del browser utilizzato quando visitava il sito). In questo caso, il tuo strumento Analytics tratterà il visitatore come un nuovo utente anche se ha visitato il sito poco più di sette giorni fa. Inoltre, inizierà di nuovo qualsiasi tentativo di personalizzare l’esperienza per l’utente.

### ID dispositivo di prime parti

Per tenere conto degli effetti delle espansioni dei cookie come descritto in precedenza, puoi impostare e gestire gli identificatori dei dispositivi. Consulta la guida su [ID dispositivo di prime parti](./first-party-device-ids.md) per ulteriori informazioni.

## Recupero dell&#39;ECID e della regione per l&#39;utente corrente

Per recuperare l’ECID univoco per il visitatore corrente, utilizza il `getIdentity` comando. Per i nuovi visitatori che non dispongono ancora di un ECID, questo comando genera un nuovo ECID. `getIdentity` restituisce anche l’ID di regione del visitatore.

>[!NOTE]
>
>Questo metodo viene generalmente utilizzato con soluzioni personalizzate che richiedono la lettura del [!DNL Experience Cloud] ID o richiede un hint di posizione per Adobe Audience Manager. Non viene utilizzata da un’implementazione standard.

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

## Utilizzando `identityMap`

Utilizzo di un XDM [`identityMap` field](../../xdm/schema/composition.md#identityMap), puoi identificare un dispositivo/utente utilizzando più identità, impostarne lo stato di autenticazione e decidere quale identificatore è considerato quello principale. Se non è stato impostato alcun identificatore come `primary`, il valore predefinito principale è `ECID`.

`identityMap` i campi vengono aggiornati utilizzando `sentEvent` comando.

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

Ogni proprietà all&#39;interno di `identityMap` rappresenta le identità appartenenti a un determinato [spazio dei nomi identità](../../identity-service/namespaces.md). Il nome della proprietà deve essere il simbolo dello spazio dei nomi identità, che è possibile trovare elencato nell&#39;interfaccia utente di Adobe Experience Platform in &quot;[!UICONTROL Identità]&quot;. Il valore della proprietà deve essere un array di identità relative a tale spazio dei nomi di identità.

Ogni oggetto identity nell&#39;array identity contiene le seguenti proprietà:

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `id` | Stringa | **(Obbligatorio)** ID che si desidera impostare per lo spazio dei nomi specificato. |
| `authenticationState` | Stringa | **(Obbligatorio)** Lo stato di autenticazione dell&#39;ID. I valori possibili sono `ambiguous`, `authenticated`e `loggedOut`. |
| `primary` | Booleano | Determina se questa identità deve essere utilizzata come frammento principale nel profilo. Per impostazione predefinita, l’ECID è impostato come identificatore principale dell’utente. Se omesso, il valore predefinito sarà `false`. |

## Migrazione da API visitatore a ECID

Durante la migrazione dall’utilizzo dell’API visitatore, puoi anche eseguire la migrazione dei cookie AMCV esistenti. Per abilitare la migrazione ECID, imposta la variabile `idMigrationEnabled` nella configurazione. La migrazione degli ID abilita i seguenti casi d’uso:

* Quando alcune pagine di un dominio utilizzano l’API Visitor e altre pagine utilizzano questo SDK. Per supportare questo caso, l&#39;SDK legge i cookie AMCV esistenti e scrive un nuovo cookie con l&#39;ECID esistente. Inoltre, l’SDK scrive i cookie AMCV in modo che, se l’ECID viene ottenuto per primo su una pagina dotata di strumenti SDK, le pagine successive strumentalizzate con l’API visitatore abbiano lo stesso ECID.
* Quando Adobe Experience Platform Web SDK è configurato in una pagina che dispone anche di API visitatore. Per supportare questo caso, se il cookie AMCV non è impostato, l’SDK cerca l’API visitatore sulla pagina e la chiama per ottenere l’ECID.
* Quando l’intero sito utilizza Adobe Experience Platform Web SDK e non dispone di API visitatore, è utile migrare gli ECID in modo da mantenere le informazioni sul visitatore restituito. Dopo che l&#39;SDK è stato distribuito con `idMigrationEnabled` per un periodo di tempo che consenta la migrazione della maggior parte dei cookie del visitatore, l’impostazione può essere disattivata.

### Aggiornamento delle caratteristiche per la migrazione

Quando i dati in formato XDM vengono inviati in Audience Manager, questi dovranno essere convertiti in segnali durante la migrazione. Le caratteristiche dovranno essere aggiornate per riflettere le nuove chiavi fornite da XDM. Questo processo è reso più semplice utilizzando [Strumento BAAAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) questo Audience Manager ha creato.

## Utilizzo nell&#39;inoltro eventi

Se hai [inoltro eventi](../../tags/ui/event-forwarding/overview.md) abilitato e in uso `appmeasurement.js` e `visitor.js`, puoi mantenere abilitata la funzione di inoltro eventi e questo non causerà problemi. Nel back-end, Adobe recupera eventuali segmenti AAM e li aggiunge alla chiamata ad Analytics. Se la chiamata ad Analytics contiene tali segmenti, Analytics non chiamerà Audience Manager per inoltrare alcun dato, quindi non vi è alcuna raccolta dati doppia. Non è necessario alcun suggerimento sulla posizione quando si utilizza l’SDK per web, perché gli stessi endpoint di segmentazione vengono chiamati nel backend.
