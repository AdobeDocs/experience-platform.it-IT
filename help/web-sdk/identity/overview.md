---
title: Dati di identità in Web SDK
description: Scopri come recuperare e gestire gli ID Adobe Experience Cloud (ECID) utilizzando Adobe Experience Platform Web SDK.
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 6b58d72628b58b75a950892e7c16d397e3c107e2
workflow-type: tm+mt
source-wordcount: '1481'
ht-degree: 0%

---

# Dati di identità in Web SDK

Adobe Experience Platform Web SDK utilizza [Adobe Experience Cloud ID (ECID)](../../identity-service/features/ecid.md) per tenere traccia del comportamento del visitatore. Utilizzando gli ECID, puoi garantire che ogni dispositivo abbia un identificatore univoco che possa persistere in più sessioni, collegando a un dispositivo specifico tutti gli hit che si verificano durante e tra sessioni web.

Questo documento fornisce una panoramica su come gestire gli ECID utilizzando Platform Web SDK.

## Tracciamento degli ECID tramite l’SDK

Platform Web SDK assegna e tiene traccia degli ECID utilizzando i cookie, con diversi metodi disponibili per configurare la modalità di generazione di questi cookie.

Quando un nuovo utente arriva sul sito web, Adobe Experience Cloud Identity Service tenta di impostare un cookie di identificazione del dispositivo per tale utente. Per i visitatori nuovi, viene generato un ECID che viene restituito nella prima risposta dall’Edge Network di Adobe Experience Platform. Per i visitatori ripetuti, l’ECID viene recuperato da `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` e aggiunti al payload dall’Edge Network.

Una volta impostato il cookie contenente l’ECID, ogni richiesta successiva generata dall’SDK web include un ECID codificato nel `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` cookie.

Quando si utilizzano i cookie per l’identificazione del dispositivo, è possibile interagire con l’Edge Network in due modi:

1. Inviare dati direttamente al dominio Edge Network `adobedc.net`. Questo metodo è denominato [raccolta dati di terze parti](#third-party).
1. Crea un CNAME sul tuo dominio che punti a `adobedc.net`. Questo metodo è denominato [raccolta dati di prime parti](#first-party).

Come spiegato nelle sezioni seguenti, il metodo di raccolta dei dati che scegli di utilizzare ha un impatto diretto sulla durata dei cookie nei vari browser.

### Raccolta di dati di terze parti {#third-party}

La raccolta di dati di terze parti comporta l’invio diretto di dati al dominio Edge Network `adobedc.net`.

Negli ultimi anni, i browser web sono diventati sempre più restrittivi nella gestione dei cookie impostati da terze parti. Per impostazione predefinita, alcuni browser bloccano i cookie di terze parti. Se utilizzi cookie di terze parti per identificare i visitatori del sito, la durata di tali cookie è quasi sempre più breve di quella che sarebbe altrimenti disponibile utilizzando i cookie di prima parte. A volte, un cookie di terze parti scade entro appena sette giorni.

Inoltre, quando si utilizza la raccolta dati di terze parti, alcuni ad blocker limitano il traffico agli endpoint di raccolta dati di Adobe.

### Raccolta di dati di prime parti {#first-party}

La raccolta dati di prime parti comporta l’impostazione di cookie tramite un CNAME sul tuo dominio che punta a `adobedc.net`.

Anche se i browser trattano i cookie impostati dagli endpoint CNAME in modo simile a quelli impostati dagli endpoint di proprietà del sito, le recenti modifiche implementate dai browser hanno creato una distinzione nel modo in cui vengono gestiti i cookie CNAME. Sebbene non vi siano browser che attualmente bloccano i cookie CNAME di prime parti per impostazione predefinita, alcuni browser limitano la durata dei cookie impostati utilizzando un CNAME a soli sette giorni.

### Effetti della durata dei cookie sulle applicazioni Adobe Experience Cloud {#lifespans}

Indipendentemente dal fatto che si scelga la raccolta dati di prima parte o di terze parti, il periodo di tempo in cui un cookie può persistere ha un impatto diretto sul numero di visitatori in Adobe Analytics e nel Customer Journey Analytics. Inoltre, gli utenti finali possono riscontrare esperienze di personalizzazione incoerenti quando sul sito vengono utilizzati Adobe Target o Offer Decisioning.

Ad esempio, considera una situazione in cui hai creato un’esperienza di personalizzazione che promuove qualsiasi elemento nella home page se un utente lo ha visualizzato tre volte negli ultimi sette giorni.

Se un utente finale visita il sito tre volte alla settimana e poi non vi ritorna per sette giorni, potrebbe essere considerato un nuovo utente quando ritorna sul sito, perché i suoi cookie potrebbero essere stati eliminati da una policy del browser (a seconda del browser che stava utilizzando quando ha visitato il sito). In questo caso, lo strumento Analytics tratta il visitatore come un nuovo utente, anche se ha visitato il sito poco più di sette giorni fa. Inoltre, ricomincia qualsiasi tentativo di personalizzare l’esperienza per l’utente.

### ID dispositivo di prime parti

Per tenere conto degli effetti delle durate dei cookie come descritto in precedenza, puoi invece scegliere di impostare e gestire gli identificatori dei tuoi dispositivi. Consulta la guida su [ID dispositivo di prime parti](./first-party-device-ids.md) per ulteriori informazioni.

## Recupera l’ECID e l’area geografica dell’utente corrente {#retrieve-ecid}

A seconda del caso d’uso, esistono due modi in cui puoi accedere al [!DNL ECID]:

* [Recupera il [!DNL ECID] tramite Preparazione per la raccolta dati](#retrieve-ecid-data-prep): questo è il metodo consigliato da utilizzare.
* [Recupera il [!DNL ECID] tramite `getIdentity()` comando](#retrieve-ecid-getidentity): utilizza questo metodo solo quando hai bisogno del [!DNL ECID] informazioni sul lato client.

### Recupera il [!DNL ECID] tramite Preparazione per la raccolta dati {#retrieve-ecid-data-prep}

Utilizzare [Preparazione per la raccolta dati](../../datastreams/data-prep.md) per mappare [!DNL ECID] a un [!DNL XDM] campo. Questo è il modo consigliato per accedere al [!DNL ECID].

A questo scopo, imposta il campo di origine sul seguente percorso:

```js
xdm.identityMap.ECID[0].id
```

Quindi, imposta il campo di destinazione su un percorso XDM in cui il campo è di tipo `string`.

![](../../tags/extensions/client/web-sdk/assets/access-ecid-data-prep.png)


### Recupera il [!DNL ECID] tramite `getIdentity()` comando {#retrieve-ecid-getidentity}


>[!IMPORTANT]
>
>È necessario recuperare l’ECID solo tramite `getIdentity()` se è necessario il comando [!DNL ECID] sul lato client. Se desideri mappare solo l’ECID a un campo XDM, utilizza [Preparazione per la raccolta dati](#retrieve-ecid-data-prep) invece.

Per recuperare l’ECID univoco per il visitatore corrente, utilizza `getIdentity` comando. Per i nuovi visitatori che non hanno un [!DNL ECID] tuttavia, questo comando genera un nuovo [!DNL ECID]. `getIdentity` restituisce anche l’ID di regione del visitatore.

>[!NOTE]
>
>Questo metodo viene in genere utilizzato con soluzioni personalizzate che richiedono la lettura di [!DNL Experience Cloud] ID o suggerimento di posizione per Adobe Audience Manager. Non viene utilizzato da un’implementazione standard.

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

## Utilizzo di `identityMap`

Utilizzo di un XDM [`identityMap` campo](../../xdm/schema/composition.md#identityMap), è possibile identificare un dispositivo/utente utilizzando più identità, impostarne lo stato di autenticazione e decidere quale identificatore è considerato quello principale. Se non è stato impostato alcun identificatore come `primary`, il valore predefinito è `ECID`.

`identityMap` vengono aggiornati utilizzando `sentEvent` comando.

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Notice how each namespace can contain multiple identifiers.
        {
          "id": "1234",
          "authenticatedState": "authenticated",
          "primary": true
        }
      ]
    }
  }
});
```

>[!NOTE]
>
>L’Adobe consiglia di inviare spazi dei nomi che rappresentano una persona, come `CRMID`, come identità primaria.


Ogni proprietà in `identityMap` rappresenta le identità appartenenti a un particolare [spazio dei nomi delle identità](../../identity-service/features/namespaces.md). Il nome della proprietà deve essere il simbolo dello spazio dei nomi dell’identità, che puoi trovare elencato nell’interfaccia utente di Adobe Experience Platform in &quot;[!UICONTROL Identità]&quot;. Il valore della proprietà deve essere un array di identità relative a tale spazio dei nomi di identità.

>[!IMPORTANT]
>
>L’ID dello spazio dei nomi passato nel `identityMap` distingue tra maiuscole e minuscole. Assicurati di utilizzare l’ID dello spazio dei nomi corretto per evitare la raccolta incompleta dei dati.

Ogni oggetto identità nell’array delle identità contiene le seguenti proprietà:

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `id` | Stringa | **(Obbligatorio)** ID che desideri impostare per lo spazio dei nomi specificato. |
| `authenticationState` | Stringa | **(Obbligatorio)** Stato di autenticazione dell&#39;ID. I valori possibili sono `ambiguous`, `authenticated`, e `loggedOut`. |
| `primary` | Booleano | Determina se questa identità deve essere utilizzata come frammento principale nel profilo. Per impostazione predefinita, l’ECID è impostato come identificatore principale dell’utente. Se omesso, il valore predefinito è `false`. |

Utilizzo di `identityMap` per identificare i dispositivi o gli utenti porta allo stesso risultato dell&#39;utilizzo del [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html) metodo da [!DNL ID Service API]. Consulta la [Documentazione API del servizio ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html) per ulteriori dettagli.

## Migrazione dall’API visitatore a ECID

Durante la migrazione da utilizzando l’API visitatore, puoi anche eseguire la migrazione dei cookie AMCV esistenti. Per abilitare la migrazione ECID, imposta `idMigrationEnabled` nella configurazione. La migrazione degli ID abilita i seguenti casi d’uso:

* Quando alcune pagine di un dominio utilizzano l’API Visitor e altre pagine utilizzano questo SDK. Per supportare questo caso, l’SDK legge i cookie AMCV esistenti e scrive un nuovo cookie con l’ECID esistente. Inoltre, l&#39;SDK scrive i cookie AMCV in modo che, se l&#39;ECID viene ottenuto per primo su una pagina instrumentata con l&#39;SDK, le pagine successive instrumentate con l&#39;API visitatore abbiano lo stesso ECID.
* Quando Adobe Experience Platform Web SDK è configurato in una pagina che dispone anche dell’API visitatore. Per supportare questo caso, se il cookie AMCV non è impostato, l&#39;SDK cerca l&#39;API visitatore nella pagina e la chiama per ottenere l&#39;ECID.
* Quando l’intero sito utilizza Adobe Experience Platform Web SDK e non dispone dell’API visitatore, è utile migrare gli ECID in modo che vengano conservate le informazioni sul visitatore restituite. Dopo che l’SDK è stato distribuito con `idMigrationEnabled` per un periodo di tempo tale da consentire la migrazione della maggior parte dei cookie del visitatore, l’impostazione può essere disattivata.

### Aggiornamento delle caratteristiche per la migrazione

Quando si inviano dati in formato XDM a Audienci Manager, questi devono essere convertiti in segnali durante la migrazione. Le caratteristiche devono essere aggiornate per riflettere le nuove chiavi fornite da XDM. Questo processo è semplificato utilizzando [Strumento BAAAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) l’Audience Manager è stato creato.

## Utilizzo nell’inoltro degli eventi

Se al momento hai [inoltro eventi](../../tags/ui/event-forwarding/overview.md) abilitato e utilizzato `appmeasurement.js` e `visitor.js`, puoi mantenere attiva la funzione di inoltro degli eventi, senza causare alcun problema. Nel back-end, Adobe recupera tutti i segmenti AAM e li aggiunge alla chiamata ad Analytics. Se la chiamata ad Analytics contiene tali segmenti, Analytics non chiamerà Audienci Manager per inoltrare alcun dato, quindi non esiste una doppia raccolta di dati. Inoltre, non è necessario usare il suggerimento posizione quando si utilizza l’SDK per web, in quanto nel back-end vengono chiamati gli stessi endpoint di segmentazione.
